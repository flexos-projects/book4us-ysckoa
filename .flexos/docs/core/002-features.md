---
id: features-mvp
title: Feature Inventory & MVP Scope
description: A prioritized list of all planned features for PageTurners, defining the scope for the Minimum Viable Product (MVP) and future releases.
type: doc
subtype: core
status: draft
sequence: 2
tags:
  - features
  - mvp
  - product
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

## 1. Feature Prioritization

Features are categorized into three priority levels: P0 (essential for MVP), P1 (high-value additions post-launch), and P2 (future enhancements).

### P0: MVP Scope

The MVP is defined as the minimum set of features required to deliver the core value proposition: enabling a private book club to successfully choose, read, and discuss a book together. The user should be able to complete the entire cycle as described in the [Vision Doc](.flexos/docs/core/001-vision.md).

*   **`user-authentication-profiles` (P0)**: Secure user signup and login (email/password and Google). Users must have a basic profile with a display name and avatar.
*   **`club-creation-management` (P0)**: Users can create a private club, give it a name and description, and receive a unique invite code to share with friends. The creator is designated as the club admin.
*   **`book-voting-selection` (P0)**: The club admin can propose a list of books for the next read. Members can cast one vote for their preferred book. The system automatically tallies votes and designates a winner as the 'current read'.
*   **`reading-progress-tracker` (P0)**: For the 'current read', members can update their progress by page number. The app will display individual progress and an aggregated club-wide progress bar on the [Individual Club Page](.flexos/docs/core/003-pages.md).
*   **`private-club-discussion-feeds` (P0)**: Each club has a private feed. The MVP will support two types of posts: 'general' and 'chapter-specific'. Chapter-specific posts prevent spoilers and keep conversations organized, which is a key differentiator.

### P1: Post-MVP Enhancements

These features will be prioritized immediately after a successful MVP launch to enhance the user experience and drive deeper engagement.

*   **`goodreads-integration` (P1)**: While the MVP might use a simplified, manually-seeded book database, full Goodreads API integration is a top priority. This will allow users to search a comprehensive catalog when proposing books and will automatically pull in rich metadata (cover art, synopsis, page count), as detailed in the [Database Doc](.flexos/docs/core/004-database.md).
*   **`notifications-alerts` (P1)**: A robust notification system is crucial for re-engagement. This includes in-app and email alerts for new discussion posts, voting round starts/ends, and reminders to update reading progress.
*   **`book-ratings-reviews` (P1)**: Users can leave a 5-star rating and a written review on any book they've read. This builds a valuable internal content library and helps users discover new books based on their network's opinions.

### P2: Future Roadmap

These are features we plan to explore in the long term, based on user feedback and growth.

*   **Public Clubs & Discovery**: A directory of public book clubs that users can search, browse by genre, and request to join.
*   **Advanced Admin Tools**: More granular permissions for club management, member analytics, and the ability to schedule meetings.
*   **Reading History & Stats**: Enhanced user profiles showing detailed reading history, stats (pages read, books finished), and achievements.
*   **Mobile App**: Native iOS and Android applications for a better on-the-go experience.

## 2. Feature Dependencies

Several features are interconnected and must be developed with these dependencies in mind.

*   **Book Data Dependency**: The quality of `book-voting-selection`, `reading-progress-tracker`, and `private-club-discussion-feeds` is highly dependent on having good book data. The MVP will require a basic `books` collection, but the P1 `goodreads-integration` will significantly enhance it.
*   **Club Membership Dependency**: All core club features (`book-voting-selection`, `reading-progress-tracker`, `private-club-discussion-feeds`) are gated by membership. The logic for checking if a user belongs to a club, as defined in the `club_members` collection, is a foundational piece of the architecture and its security rules.
*   **Current Book Dependency**: The `reading-progress-tracker` and chapter-specific discussions are only active when a `currentBookId` is set on the `book_clubs` document. This means the `book-voting-selection` flow must successfully complete and update this value.