---
id: technical-architecture
title: Technical Architecture & Stack
description: An overview of the technical stack, architecture, API integrations, and deployment strategy for PageTurners.
type: doc
subtype: core
status: draft
sequence: 7
tags:
  - technical
  - architecture
  - firebase
  - nuxt
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

## 1. High-Level Architecture

PageTurners will be built using a modern **Jamstack architecture**. The frontend will be a Server-Side Rendered (SSR) Single Page Application (SPA) built with Nuxt. The backend will be a suite of serverless services provided by Google Firebase. This approach offers excellent performance, scalability, security, and a streamlined developer experience.

## 2. Frontend Stack

*   **Framework**: **Nuxt 4** (Vue 3)
    *   **Reasoning**: Nuxt provides a powerful, opinionated framework on top of Vue. We will leverage its file-based routing, server-side rendering for SEO and fast initial loads, and a rich ecosystem of modules.
*   **State Management**: **Pinia**
    *   **Reasoning**: As the official state management library for Vue, Pinia is lightweight, intuitive, and has excellent TypeScript support. We will create stores for managing authentication state (`authStore`), club data (`clubStore`), and user profile information.
*   **Styling**: **Tailwind CSS**
    *   **Reasoning**: A utility-first CSS framework that allows for rapid development of custom designs without leaving our HTML. It pairs perfectly with a component-based framework like Vue.
*   **UI Components**: **Headless UI**
    *   **Reasoning**: Provides completely unstyled, fully accessible UI components (like modals, dropdowns, tabs) that we can style from scratch with Tailwind CSS, giving us full design control while ensuring accessibility.
*   **Icons**: **Heroicons**
    *   **Reasoning**: A high-quality set of SVG icons designed by the makers of Tailwind CSS, ensuring a consistent visual style.

## 3. Backend Stack (Firebase)

*   **Database**: **Firebase Firestore**
    *   **Reasoning**: A scalable NoSQL document database with powerful real-time capabilities, which is essential for our discussion feeds and progress trackers. The security model is robust and integrates directly with Firebase Auth. See the [Database Doc](.flexos/docs/core/004-database.md) for the full schema.
*   **Authentication**: **Firebase Authentication**
    *   **Reasoning**: Provides a secure, managed solution for user identity, supporting email/password, Google, and other social providers out of the box.
*   **Serverless Logic**: **Firebase Cloud Functions**
    *   **Reasoning**: For any backend logic that cannot or should not run on the client. Key use cases will include:
        *   **`onUserCreate`**: An auth trigger to create a user profile document in Firestore.
        *   **`processVoteResults`**: A scheduled (cron) function to tally votes and select a new book.
        *   **`sendNotifications`**: Database triggers that send notifications when new discussions are posted.
        *   **API Proxies**: HTTP-triggered functions to securely interact with third-party APIs.
*   **Hosting**: **Firebase Hosting**
    *   **Reasoning**: Provides a global CDN for our static assets, free SSL, and seamless CI/CD integration. It's optimized for hosting modern web apps.

## 4. API Integrations

*   **Goodreads API**
    *   **Usage**: This is our primary external dependency for book data.
    *   **Implementation**: We will **not** call the Goodreads API directly from the frontend client. This would expose our API key. Instead, we will create an HTTP-triggered Firebase Cloud Function to act as a secure proxy. The Nuxt frontend will call our own API endpoint (e.g., `https://us-central1-pageturners-prod.cloudfunctions.net/searchBooks?q=...`), which will then securely call the Goodreads API on the server-side and return the results.

## 5. Deployment & DevOps

*   **Source Control**: **GitHub**.
*   **CI/CD**: **GitHub Actions**.
*   **Environments**:
    *   `development`: Local developer machines.
    *   `staging`: A separate Firebase project for pre-production testing.
    *   `production`: The live application.
*   **Deployment Workflow**:
    1.  A developer pushes a feature branch and opens a Pull Request against the `main` branch.
    2.  A GitHub Action workflow is triggered, running linters, unit tests (Vitest), and end-to-end tests (Cypress).
    3.  Upon successful tests and code review, the PR is merged into `main`.
    4.  The merge to `main` triggers a separate deployment workflow in GitHub Actions.
    5.  This workflow builds the Nuxt application and uses the Firebase CLI to deploy the static assets to Firebase Hosting and the serverless functions to Firebase Cloud Functions for the production environment.