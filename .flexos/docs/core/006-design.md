---
id: design-system
title: Design System & Brand Identity
description: A guide to the visual and brand identity of PageTurners, including color palette, typography, core components, and accessibility standards.
type: doc
subtype: core
status: active
sequence: 6
tags:
  - design
  - ui
  - accessibility
createdAt: 2026-02-08T00:29:02.596Z
updatedAt: 2026-02-08T00:29:02.596Z
---

## 1. Brand Identity

*   **Name**: PageTurners
*   **Tagline**: Your digital home for vibrant book club discussions and shared reading journeys.
*   **Vibe**: Engaging, Organized, Community-focused, Modern, Clean, Inviting.
*   **Voice**: The brand voice is encouraging and friendly. We use clear, simple language that avoids technical jargon. We are the helpful facilitator that makes the book club experience smoother and more enjoyable for everyone.

## 2. Color System

Our color palette is designed to be modern and inviting, with a strong primary color for branding and clear neutrals for readability. We will use a utility-first CSS framework like Tailwind CSS, and these colors correspond to its naming convention.

*   **Primary**: `violet-500` (`#8b5cf6`)
    *   **Usage**: Primary buttons, active links, focused input borders, key icons, and major headings.
*   **Accent**: `yellow-400` (`#facc15`)
    *   **Usage**: Notification badges, special callouts, or celebratory UI elements (e.g., a confetti animation when a book is finished).
*   **Neutrals**:
    *   **Text**: `gray-800` (`#1f2937`) - For all primary body copy.
    *   **Text-Secondary**: `gray-500` (`#6b7280`) - For descriptions, timestamps, and placeholder text.
    *   **Borders/Dividers**: `gray-200` (`#e5e7eb`).
    *   **Surface**: `white` (`#ffffff`) - For card backgrounds, modals, and page content areas.
    *   **Background**: `gray-50` (`#f9fafb`) - The main background color for pages, providing a slight contrast to white surfaces.
*   **System Colors**:
    *   **Success**: `green-500` (`#22c55e`) - For success messages and validation.
    *   **Error**: `red-500` (`#ef4444`) - For error messages and validation.

## 3. Typography

*   **Font Family**: `Inter` (sans-serif)
    *   **Reasoning**: Chosen for its excellent readability at all sizes, modern aesthetic, and extensive weight options.
*   **Scale & Weight**:
    *   **H1 (Page Titles)**: 36px, Bold (700)
    *   **H2 (Section Titles)**: 24px, Bold (700)
    *   **H3 (Card Titles)**: 20px, Semi-Bold (600)
    *   **Body (Paragraphs)**: 16px, Regular (400)
    *   **Small/Meta Text**: 14px, Regular (400)
    *   **Button Text**: 16px, Medium (500)

## 4. Core UI Components

This is a preliminary list of key reusable components that will form our design system.

*   **Button**:
    *   *Primary*: Solid `violet-500` background, white text. Has a slightly darker shade on hover/focus.
    *   *Secondary*: Transparent background, `violet-500` text and border.
    *   *Tertiary/Link*: No border or background, `violet-500` text.
*   **Card**:
    *   The primary container for content like clubs, books, and discussion posts. It will have a `white` background, a subtle `box-shadow`, and rounded corners (e.g., `8px` radius).
*   **Input Fields**:
    *   Simple, clean inputs with a `gray-200` border. On focus, the border color will change to `violet-500`.
*   **Avatar**:
    *   Used to represent users. Circular shape. If a user has not uploaded a photo, a default will be generated with their initials on a colored background.
*   **Progress Bar**:
    *   Used for the `reading-progress-tracker`. It will have a light gray (`gray-200`) track and a `violet-500` fill to show progress.

## 5. Accessibility (A11y)

Accessibility is a core requirement, not an afterthought. We will adhere to WCAG 2.1 AA standards.

*   **Color Contrast**: All text and UI elements will meet minimum contrast ratios. Our chosen primary color (`#8b5cf6`) on white has a contrast ratio of 4.6:1, which passes the AA standard.
*   **Keyboard Navigation**: All interactive elements will be reachable and operable using the Tab key. Focus states will be clearly visible (e.g., using focus rings).
*   **Semantic HTML**: We will use proper HTML5 elements (`<nav>`, `<main>`, `<button>`, etc.) to ensure screen readers can correctly interpret the page structure.
*   **Forms**: All form inputs will be associated with a `<label>` for screen reader accessibility.
*   **Images**: All meaningful images will have descriptive `alt` text. Decorative images will have an empty `alt` attribute.

## 6. Prototypes

Interactive prototypes for the core application pages are currently being generated. Once complete, they can be viewed via the [Prototype Sitemap](/.flexos/design/prototype/sitemap.md).
