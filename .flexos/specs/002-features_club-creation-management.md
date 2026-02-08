---
id: feature-club-creation-management
title: Club Creation & Management Feature Specification
description: Detailed specification for the core feature allowing users to create, manage, and invite members to book clubs.
type: spec
subtype: feature
status: draft
sequence: 2
tags:
  - feature
  - club
  - management
  - admin
relatesTo:
  - user-authentication-profiles
  - my-clubs
  - create-edit-club
  - users
  - book_clubs
  - club_members
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---
## Club Creation & Management

This feature enables users to establish and oversee book clubs within PageTurners. It covers the full lifecycle from initial club creation to inviting members, assigning administrative roles, and managing club settings. This is a foundational P0 feature, crucial for the platform's core functionality.

**User Stories:**
*   As a user, I want to create a private book club for my friends so we can manage our reading together.
*   As a club admin, I want to invite new members to my book club via a shareable link or email.
*   As a club member, I want to see a list of all book clubs I belong to.

**Acceptance Criteria:**
1.  A logged-in user can successfully create a new book club by providing a unique name and optional description via the `/clubs/new` page.
2.  Upon creation, the user is automatically designated as the club's administrator.
3.  Club admins can generate a unique, shareable invitation link for their club.
4.  Club admins can send email invitations to specific users.
5.  Non-members can join a private club using a valid invitation link or by accepting an email invite.
6.  The `My Clubs` page (`/clubs`) accurately displays all clubs a user is a member of.
7.  Club admins can remove members from their club.
8.  Club admins can transfer admin privileges to another member.

**Edge Cases:**
*   **Duplicate Club Names:** The system should prevent clubs from having identical names within a user's context or globally (TBD).
*   **Invalid Invitation Links:** Expired or malformed invitation links should display an appropriate error message.
*   **Admin Departure:** If the sole admin leaves a club, the system must prompt them to assign a new admin or, if not possible, archive the club.
*   **Max Members:** Consider implementing a soft or hard limit on club members.

**Cross-references:**
*   **Pages:** `create-edit-club`, `my-clubs`, `individual-club-page`
*   **Flows:** `user-onboarding-club-creation`
*   **Collections:** `users`, `book_clubs`, `club_members`
