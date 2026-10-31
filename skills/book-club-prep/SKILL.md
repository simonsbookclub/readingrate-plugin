---
name: book-club-prep
description: Prepare the reader for their ReadingRate book club's next meeting, with the club's current book, how far the schedule says to read, how much the reader has left at their pace, and discussion questions that stay within the pages they have read. Use when the reader mentions their book club, an upcoming meeting, or wants questions for the club's book.
---

# Book club meeting prep

Needs the reader's ReadingRate account to be connected, with a club in it.

## 1. Find the club and its book

1. Call `list_book_clubs`. If the reader is in more than one club, ask which one, unless they named it.
2. Call `get_book_club_current_read` with the club's id. It returns the book, with its `book_id` for the other tools, and the reading schedule: each milestone's pages, due date and discussion questions.
3. The next meeting is the first milestone whose due date has not passed.

## 2. Where the reader is

Call `get_currently_reading` for the reader's page in the book and the hours left at their pace. Give the page as printed: the `page_label` when the book has one.

- If they are behind the milestone, say how many pages remain before its due date, and what that comes to per day.
- If they are ahead, say so, and keep everything that follows within the milestone's pages.
- If the book is not among the books they are reading, say that ReadingRate has no page for them in it, and ask where they are before writing any question.

## 3. Questions for the meeting

1. Start from the milestone's own discussion questions.
2. Where the reader saved quotes or notes about the book, build on those first. `list_saved_quotes` and `get_reading_notes` with the club book's `book_id` find them.
3. Add a question or two from the book's own text, when a tool returns it. Call `search_book_content` with the `book_id` and `spoiler_protection` true: then it searches only up to the reader's logged page, and withholds passages when no page is logged. Leave out any passage beyond the milestone's last page.

Passages and pages:
- **Text.** `search_book_content` returns text only for a book the reader uploaded their own copy of; otherwise it says the text is not available. Then the questions come from the milestone and the reader's own quotes and notes alone.
- **Only what a tool returned.** Never quote the book from memory, and never give a page number that no tool returned.
- **Whole quotes.** Quote a passage whole, with its page. Never shorten a quote or end it with an ellipsis.

## 4. What makes the book hard

If the club finds the book difficult, `get_book_details` gives its difficulty in nine dimensions: vocabulary, syntax, abstraction, information density, narrative indirection, symbolic density, ironic distance, resolution withholding and structural complexity. Name the one or two that score highest, and say what helps with each.

## 5. A sheet to bring

Offer the reader a short page for the meeting: where the schedule is, three or four questions, and any passages they point to, with page numbers.
