---
id: user-system-flows
title: User & System Flows
description: Detailed step-by-step descriptions of key user interactions and corresponding system processes, including error handling.
type: doc
subtype: core
status: draft
sequence: 5
tags:
  - ux
  - flows
  - technical
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

This document outlines the critical user and system flows for PageTurners. These flows provide a detailed, step-by-step narrative of how users will accomplish tasks and how the system will respond.

## 1. Flow: Onboarding and First Club Creation (`user-onboarding-club-creation`)

*   **Goal**: A new user signs up, creates their first book club, and is ready to invite members.
*   **Trigger**: A new, unauthenticated user lands on the `/` (Landing Page).

| Step | Actor  | Action                                                                                                                              |
| :--- | :----- | :---------------------------------------------------------------------------------------------------------------------------------- |
| 1    | User   | Clicks the 'Sign Up' button.                                                                                                       |
| 2    | System | Navigates the user to the `/auth` page.                                                                                             |
| 3    | User   | Fills out the registration form with email/password and submits.                                                                    |
| 4    | System | 1. Calls Firebase Authentication to create a new user. <br> 2. A Cloud Function triggers on user creation to create a corresponding document in the `users` collection. <br> 3. Redirects the authenticated user to `/dashboard`. |
| 5    | System | Displays a 'Welcome to PageTurners!' modal with two primary actions: 'Create a Club' and 'Join a Club'.                             |
| 6    | User   | Clicks 'Create a Club'.                                                                                                             |
| 7    | System | Navigates the user to the `/clubs/new` page.                                                                                        |
| 8    | User   | Enters a club name and description, then submits the form.                                                                          |
| 9    | System | 1. Creates a new document in the `book_clubs` collection. <br> 2. Creates a corresponding document in `club_members` linking the user to the new club with the `role` of 'admin'. <br> 3. Redirects the user to the new club's page at `/clubs/:id`. |
| 10   | System | On the club page, displays a prominent 'Invite Members' component showing the shareable invite code.                                  |

## 2. Flow: Tracking Reading Progress & Discussion (`track-progress-chapter-discussion`)

*   **Goal**: A club member updates their reading progress and participates in a chapter-specific discussion.
*   **Trigger**: User navigates to their `/clubs/:id` page for a club with an active book.

| Step | Actor  | Action                                                                                                                            |
| :--- | :----- | :---------------------------------------------------------------------------------------------------------------------------------- |
| 1    | User   | On the 'Current Book Card', interacts with the progress input (e.g., a slider or text field) and updates their current page to '150'. |
| 2    | System | 1. Updates the `progress` map in the user's specific `club_members` document in Firestore. <br> 2. The UI on the page reacts in real-time, showing the updated progress for the user. <br> 3. The aggregated 'Club Progress' bar also updates to reflect the new average. |
| 3    | User   | Scrolls to the 'Discussion Feed' and clicks on the filter for 'Chapter 10'.                                                         |
| 4    | System | The feed is filtered to show only discussion threads where `type` is 'chapter' and `chapterNumber` is 10.                            |
| 5    | User   | Writes a comment in the 'Add a post...' text area for that chapter and submits it.                                                |
| 6    | System | 1. Creates a new document in the `discussions` collection with the relevant `clubId`, `userId`, `bookId`, `type`, `chapterNumber`, and `content`. <br> 2. Due to Firestore's real-time listeners, the new post instantly appears in the feed for all other members currently viewing the page. <br> 3. A Cloud Function is triggered to send notifications to other club members about the new post. |

## 3. System Flow: Ending a Vote and Selecting a Book

*   **Goal**: The system automatically concludes a voting round and updates the club's status.
*   **Trigger**: A scheduled Cloud Function runs periodically (e.g., every hour).

| Step | Actor  | Action                                                                                                                                                                                                    |
| :--- | :----- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | System | The scheduled function queries the `book_clubs` collection for all documents where the `vote.endDate` is in the past and a `vote.votingRoundId` exists.                                                     |
| 2    | System | For each expired vote, the function queries the `club_votes` collection for all documents matching the `clubId` and `votingRoundId`.                                                                        |
| 3    | System | It aggregates the votes to determine the `bookId` with the highest count. In case of a tie, it can be programmed to randomly select one of the winners.                                                      |
| 4    | System | The function executes a batched write to Firestore: <br> 1. Updates the `book_clubs` document, setting the `currentBookId` to the winning book's ID. <br> 2. Clears the `vote` map to indicate the voting round is over. |
| 5    | System | The function triggers notifications (in-app, email) to all members of the club, announcing the winning book and encouraging them to start reading.                                                            |

## 4. Error Handling Flow: Invalid Invite Code

*   **Goal**: Provide clear feedback when a user tries to join a club with an incorrect code.
*   **Trigger**: User submits the 'Join a Club' form with a code.

| Step | Actor  | Action                                                                                                                                                                                                    |
| :--- | :----- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1    | User   | Enters an invite code (e.g., 'ABC-123') in the 'Join a Club' modal and clicks 'Join'.                                                                                                                      |
| 2    | System | The frontend client makes a query to the `book_clubs` collection `where('inviteCode', '==', 'ABC-123')`.                                                                                                  |
| 3    | System | The query returns zero documents.                                                                                                                                                                         |
| 4    | System | Instead of proceeding, the UI displays an inline error message below the input field: "Club not found. Please check the code and try again." The input field border may also turn red to indicate the error. |
| 5    | User   | The user can now correct the code and re-submit without leaving the modal.                                                                                                                                |