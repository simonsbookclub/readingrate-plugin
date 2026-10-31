---
name: shelf-to-library
description: Identify the books in a photo of a bookshelf, a stack of books or a pasted list with ReadingRate, and add them to the reader's ReadingRate library when they ask. Use when the reader shares a picture of book spines or covers, or a list of titles, and wants to know what the books are or to put them in their library.
---

# Shelf photo to ReadingRate library

Identifying books needs no account. Adding them needs the reader's ReadingRate account to be connected.

## 1. Read the books

Read every spine or cover you can make out. For each one, note the title and the author as printed. A barcode's ISBN identifies a book more surely than a title.

- Leave out a spine you cannot read, and tell the reader which ones you left out ("the third from the left is too blurred to read").
- Do not fill in a title from a partial spine by guessing what it probably is.

## 2. Match them

Call `lookup_books_batch` with all of them, up to 20 books per call. A longer shelf goes in several calls of 20.

Each match comes back with a confidence. A "low" match may be a different book with a similar title: name it as uncertain.

## 3. Show the reader

List the matched books in shelf order, each with its title and author. List the unmatched ones separately: the catalog does not hold them.

If the reader asked what the books are, answer that and stop. A photo alone is not a request to add anything.

## 4. Add them, when asked

When the reader asks to add the books:

1. If they have not said which shelf, they go to want-to-read. If the reader says they have read them, or are reading one, use that shelf.
2. Call `add_matched_books_to_library` with the matched ids, at most 40 per call, and `status` when the shelf is reading, read or stopped. A book already in the library stays where it is, so there is no need to check the library first. Books going to different shelves take one call per shelf.
3. For an unmatched book the reader still wants, confirm the exact title and author with them, then call `add_book_to_library` with `title_author`.

## 5. Report

Say in one or two lines how many books were added, how many were already in the library, and which were not found.
