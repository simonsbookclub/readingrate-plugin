---
name: next-book
description: Help a reader choose their next book with ReadingRate's difficulty scores, reading times and ranked lists, fitted to the time they have and to what they have read. Use when the reader asks what to read next, wants a book for a trip, a weekend or a month, or asks for a book like one they loved.
---

# What to read next

The catalog tools work without an account. With the reader's ReadingRate account connected, the reader's own history and pace make the answer theirs.

## 1. Learn what you can look up

If the reader's account is connected, call these and ask nothing they answer:
- `get_reading_history`: what they have read, so you never suggest a book they finished, and their want-to-read list.
- `get_reading_stats`: their reading speed and the difficulty range they usually read. These are the reader's own only when they have logged enough: a `velocity` whose `confidence` is "low" is the average reader's speed, and a difficulty range whose description says there is not enough data is a default. Treat those as unknown.
- `get_personalized_recommendations`: first with `from_tbr` true, when they have a want-to-read list; it leaves out books they have read.

If a tool says the account does not include it, or no account is connected, ask at most one question: a book they loved recently, and how much time they have.

## 2. Find candidates

- **A kind of book:** `search_books` with `genres`, `themes` and a difficulty range.
- **A country, language, period or theme:** `get_top_books`. It returns the ranked list from readingrate.com with the list's address.
- **"Something like X":** `get_book_details` for X with `include_similar` true.

## 3. Fit each candidate to their time

1. Call `get_book_details` with `include_time_estimate` true. It gives the hours an average reader takes.
2. When `get_reading_stats` has the reader's own speed, scale those hours to their pace. Otherwise give the average reader's hours, and say so.
3. Set the result against the time they named, in plain words: "about 9 hours, two weekends at your pace".

## 4. Fit each candidate to their reading

- When the reader's own difficulty range is known, set the score against it: "62, a little above the 45 to 55 you usually read". Otherwise give the score on its own.
- For two or three finalists, `compare_books` shows where each one is hard: the sentences, the structure, or the meaning.

## 5. Recommend two or three

For each book, give:
- why it fits this reader, from their history and what they asked for, not general praise;
- the hours, at their pace when you know it;
- its difficulty against their usual range;
- the list's address, when it came from `get_top_books`.

If the reader picks one, offer to put it on their want-to-read or reading shelf with `add_book_to_library`.
