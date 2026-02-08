---
id: database-books
title: Books Collection Database Specification
description: Detailed specification for the `books` data collection, outlining its structure, fields, and relationships.
type: spec
subtype: database
status: draft
sequence: 7
tags:
  - database
  - collection
  - books
  - schema
relatesTo:
  - book-voting-selection
  - reading-progress-tracker
  - book-ratings-reviews
  - goodreads-integration
  - individual-club-page
  - book-details-page
  - club_votes
  - discussions
  - reviews
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Books Collection (`books`)

The `books` collection stores information about all books referenced within PageTurners. This includes details fetched from external APIs (like Goodreads) and user-generated ratings or reviews. Each document represents a unique book.

<flex_block type="schema">
{
  "collection": "books",
  "fields": [
    { "name": "id", "type": "string", "required": true, "description": "Unique ID for the book (e.g., ISBN or Goodreads ID)." },
    { "name": "title", "type": "string", "required": true, "description": "The title of the book." },
    { "name": "author", "type": "string", "required": true, "description": "The author(s) of the book." },
    { "name": "coverImageUrl", "type": "url", "optional": true, "description": "URL to the book's cover image." },
    { "name": "description", "type": "string", "optional": true, "description": "A brief summary or synopsis of the book." },
    { "name": "isbn", "type": "string", "optional": true, "description": "International Standard Book Number." },
    { "name": "pageCount", "type": "integer", "optional": true, "description": "Total number of pages in the book." },
    { "name": "goodreadsRating", "type": "float", "optional": true, "description": "Average rating from Goodreads." },
    { "name": "goodreadsId", "type": "string", "optional": true, "description": "Goodreads specific ID for the book." },
    { "name": "publishedDate", "type": "date", "optional": true, "description": "Date the book was first published." }
  ]
}
</flex_block>

**Relationships:**
*   **One-to-Many (Club Books):** A book can be the `currentBookId` for multiple `book_clubs`.
*   **One-to-Many (Votes):** A book can be nominated in many `club_votes`.
*   **One-to-Many (Reviews):** A book can have many `reviews` from users.
*   **One-to-Many (Discussions):** A book can be the subject of many `discussions`.

**Acceptance Criteria:**
1.  Every `book` document must have a unique `id`, `title`, and `author`.
2.  `id` should ideally be derived from a globally unique identifier like ISBN or a Goodreads ID.
3.  Optional fields should be correctly stored and retrieved when provided, and gracefully absent otherwise.
4.  `goodreadsRating` should be a valid float if present.

**Edge Cases:**
*   **Missing Metadata:** The application must handle books where optional fields (e.g., `coverImageUrl`, `description`, `isbn`, `pageCount`) are not available from the external API.
*   **Goodreads Sync Issues:** If Goodreads integration fails, the system should allow manual input or flag the book for review.
*   **Duplicate Books:** Implement mechanisms to prevent or merge duplicate book entries (e.g., same book, different ISBNs).
