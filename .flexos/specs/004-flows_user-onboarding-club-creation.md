---
id: flow-user-onboarding-club-creation
title: User Onboarding & Club Creation Flow Specification
description: Detailed specification for the primary user journey from signing up to creating their first book club.
type: spec
subtype: flow
status: draft
sequence: 4
tags:
  - flow
  - onboarding
  - signup
  - club-creation
relatesTo:
  - user-authentication-profiles
  - club-creation-management
  - landing-page
  - auth-page
  - create-edit-club
  - users
  - book_clubs
  - club_members
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## User Onboarding & Club Creation Flow

This critical user flow guides a new user from their initial discovery of PageTurners through the registration process and culminates in the creation of their very first book club. It's designed to be intuitive and immediately demonstrate the platform's core value.

**Flow Steps:**
1.  **Arrive on Landing Page (`/home`):** User lands on the public-facing PageTurners website, encountering the value proposition.
2.  **Sign Up (`/auth`):** User clicks "Sign Up," chooses between email/password or social login (Google), and completes the registration.
3.  **Profile Setup (Optional):** Post-registration, the user is prompted to set a display name, upload an avatar, and optionally link their Goodreads account. This step can be skipped.
4.  **Welcome & Call to Action:** The system displays a personalized welcome and presents clear options: "Create Your First Club" or "Join a Club."
5.  **Create Club Form (`/clubs/new`):** If "Create Your First Club" is chosen, the user fills out a form including club name and description.
6.  **Club Created & Invite Members:** Upon successful club creation, the user is directed to the new club's page and presented with options to invite members (e.g., shareable link).

**Acceptance Criteria:**
1.  New users can successfully register via email/password or Google authentication.
2.  Upon successful registration, a `users` record is created in the database.
3.  The optional profile setup allows users to update `displayName`, `avatarUrl`, and `goodreadsId`.
4.  The welcome screen clearly presents options for club creation or joining.
5.  Users can successfully create a new club, resulting in a `book_clubs` record and a `club_members` record linking the user as an admin.
6.  A unique `inviteCode` is generated for new clubs.

**Edge Cases:**
*   **Registration Failure:** Handle email already in use, weak passwords, or social login errors gracefully.
*   **Network Interruption:** Ensure robust handling of network issues during signup or club creation.
*   **Invalid Club Name:** Prevent creation of clubs with empty or excessively long names.
*   **Skipped Profile:** The system should function correctly if the user skips optional profile setup steps.

**Cross-references:**
*   **Features:** `user-authentication-profiles`, `club-creation-management`, `goodreads-integration`
*   **Pages:** `landing-page`, `auth-page`, `dashboard`, `create-edit-club`
*   **Collections:** `users`, `book_clubs`, `club_members`
