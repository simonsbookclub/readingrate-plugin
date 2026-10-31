---
name: book-debrief
description: Talk through a book the reader has just finished, starting from the passages and notes they saved in ReadingRate, one question at a time, and save the conclusions to their ReadingRate account if they want to keep them. Use when the reader says they finished a book and want to talk about it, reflect on it, or make sense of it.
---

# After finishing a book

Needs the reader's ReadingRate account to be connected. Their saved quotes and notes need an account that includes them; if a tool says it does not, talk about the book from what the reader tells you.

## 1. Mark it finished

If the book is on another shelf, call `update_book_status` with `status` "read", and `rating` if they gave one. If it is not in their library at all, call `add_book_to_library` with `status` "read" instead. Ask only when it is unclear which book they mean.

## 2. Gather what they kept

- `list_saved_quotes` with the book's `book_id`: the passages they saved.
- `get_reading_history` with `status` "read" and `include_sessions` true: for this book, the note and the quote the reader wrote on each of their last 20 reading days.
- `get_reading_notes` with the book's `book_id`: their highlights, and any insight they saved about it.

## 3. Find what lit them up

Rank what they kept by enthusiasm and by recurrence: the idea, the character or the passage they came back to most, wrote the most about, or quoted most often. Build the conversation on those.

- **Not their one complaint.** A single grumble is not the heart of their reading.
- **Not other books,** unless the reader's own note made the link.

## 4. Ask, one question at a time

Ask three or four questions in all. Each one starts from something the reader kept:
- quote their note or the passage they saved, whole;
- then ask a question that takes that thought further.

Wait for each answer before asking the next question, and let the next question build on it.

- **Passages.** Quote only words a tool returned: the reader's saved quotes and notes, or passages from `search_book_content`. That tool returns text only for a book the reader uploaded their own copy of; otherwise it says the text is not available. Never quote the book from memory, and never give a page number that no tool returned.
- **Whole quotes.** Never shorten a quote or end it with an ellipsis: quote a passage whole, or choose another.
- **The reader first.** Do not explain what the book means before the reader has said what they think.

## 5. Keep it, if they want

At the end, offer to save what came out of the conversation.

1. Show the reader what you would save: a summary of two to four sentences in their terms, and the key takeaways.
2. Only after they agree, call `save_reading_insight` with the book's id, the summary and the takeaways.

It appears in their ReadingRate journal.
