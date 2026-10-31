---
name: log-reading
description: Log reading to the reader's ReadingRate account from what they say in plain words, such as "read 40 pages of Middlemarch", "I'm on page 212 of Stoner", "finished The Remains of the Day, four stars", "started Beloved" or "giving up on Ulysses". Use when the reader reports reading progress, or starting, finishing or abandoning a book.
---

# Log reading from a sentence

Needs the reader's ReadingRate account to be connected.

## 1. Find the book

Call `get_currently_reading`. It lists the books in progress with their ids and current pages. Match the reader's title to one of them.

If the book is not there:
- Find its id with `search_books`, by title and author.
- If the reader is reading it now, call `add_book_to_library` with `status` "reading" first.
- If the title matches several books, ask which one before logging anything.

## 2. Choose the call

| The reader says | Call |
|---|---|
| "read 40 pages" | `log_reading_session` with `pages_read` |
| "I'm on page 212" | `log_reading_session` with `current_page` |
| "I'm on page xii of the introduction" | `log_reading_session` with `roman_page` |
| "finished it", "four stars" | `update_book_status` with `status` "read", and `rating` from 1 to 5 if they gave one |
| "started it" | `update_book_status` with `status` "reading", or `add_book_to_library` if it is not in the library |
| "giving up on it" | `update_book_status` with `status` "stopped" |
| "I want to read it" | `add_book_to_library` (want-to-read is its default shelf) |

### Filling in `log_reading_session`

- **One count only.** Send `pages_read` or `current_page`, never both. A page the reader names is the page reached; a number of pages is pages read.
- **Printed page numbers.** A page is the page as printed in the reader's copy: page 212 is the page printed 212. Do not count the introduction's pages into it.
- **The introduction.** The first time a reader logs a page of a roman-numbered introduction, the call also needs `front_matter_ends_on`, the last roman page of their copy. If the tool asks for it, ask the reader where their introduction ends.
- **The date.** The server files the reading under the current date in UTC, and cannot log a past day. In the evening in the Americas, UTC is already the next day. If the reader describes an earlier day's reading, or it is late evening where they are, tell them the date it will be filed under before logging.

If the reader finished a book and also gives a final page, log the page first, then mark it read.

## 3. Notes and quotes

Save nothing the reader did not ask to keep.

- **A thought about the reading.** If the reader says something about it ("the chapter on the fire was astonishing"), you may offer to add their words to today's journal entry. Put the words in `notes` only after they say yes, or when they asked for it in the first place.
- **A passage.** If the reader shares one they want to keep, offer to save it with `save_quote`, with the page if they know it. Save the whole passage exactly as the reader gave it. Never shorten a quote or end it with an ellipsis.

## 4. Confirm

Answer in one line: the book, the page they are on now, and the pages this entry added.

- Use the result's `page_label` for the page when it has one: it is the page as printed.
- Add the hours left from `get_currently_reading` only if the reader asks how long the rest will take.
