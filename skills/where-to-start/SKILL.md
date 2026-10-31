---
name: where-to-start
description: Build a reading path into a country's, a language's, a period's or a genre's literature, from ReadingRate's ranked lists and difficulty scores. It covers where to start, what to read next, and what to save for later. Use when the reader asks where to start with Russian novels, Japanese literature, poetry, the Victorians, or any tradition, or wants a reading plan for one.
---

# Where to start with a literature

Works without an account. A connected ReadingRate account adds the reader's pace and their shelves.

## 1. Get the ranked list

Call `get_top_books` with the reader's subject:
- a `country`, a `language`, a `genre`, or a `subject` (a period, a theme, a region);
- `author_gender` if they asked for books by women or by men;
- `limit` 30, so there is room to choose.

The answer gives the list's title, how it is ranked, and its address on readingrate.com.

If the answer has a note, pass it on in a sentence. A note says, for example, that a country has no list page, or that the list is short.

## 2. Lay out a path in three steps

Sort the list into three steps by difficulty score:
- **Start here:** under 45.
- **Next:** 45 to 64.
- **Later:** 65 and over.

Within each step, pick two or three books:
- prefer the higher-ranked;
- prefer the shorter, when ranks are close;
- prefer different authors.

A path that opens with a book the reader can finish keeps them reading.

## 3. Say why, briefly

For each book give its rank on the list, its difficulty score, and its reading hours. Add one line on what it opens up in the tradition.

`compare_books` with the opening book and a later one shows where the later one is harder, dimension by dimension. Use it to explain the order in a sentence.

If the reader's account is connected:
- `get_reading_stats` gives their reading speed. Scale the hours to it only when its `velocity` `confidence` is not "low"; a low confidence means the average reader's speed.
- `get_reading_history` shows books on the list they have already read. Mark those, and start the path after them.

## 4. Point to the full list

When the list has an address, give it, so the reader can see the whole ranking. A country or language with no list page has none.

If their account is connected, offer to put the opening book on their want-to-read shelf with `add_book_to_library`.
