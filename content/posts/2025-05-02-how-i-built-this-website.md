---
title: How I built this website (v.1.0.3)
date: 2025-05-01
---




# The Big Refactor: Improving My Website's Structure and Styles

Recently, I undertook a major refactor of my website to improve its structure, maintainability, and aesthetics. This update focuses on better-organized styles, enhanced animations, and a more polished homepage. Here’s a breakdown of what changed:

## 🔹 Style Refactoring

- **Blog Section:** The styles for the blog section were cleaned up and improved for better readability and consistency.
- **Navbar:** The navigation bar received a design overhaul.
- **Home & Contact Me:** The styles for the homepage and the contact section were revamped.

## ✨ New Animations

- **Hero Section:** I added subtle animations to the hero section to make the website feel more dynamic and engaging.

## 🏗️ Projects Display

- **Minimal Projects Section:** Added styles to ensure project previews look neat and visually consistent.
- **Projects Intro:** Styled the new introduction section for the projects page on the homepage.
- **Projects Data:** Created dummy data in `data/projects.yaml` to dynamically populate the projects list.

## 🏡 Homepage Enhancements

- **Updated HTML Structure:** Modified `layouts/default/index.html` to include the projects intro, projects list, and contact me sections.
- **Contact Me Partial:** Hardcoded `layouts/partials/homepage/contact-me.html` and linked it to its SCSS file for styling.
- **Projects Preview:** Now all projects listed in `projects.yaml` are displayed in `layouts/partials/homepage/minimal-projects.html`.
- **Projects Intro Section:** Added `layouts/partials/homepage/projects-intro.html` and linked it to its corresponding styles.

## 📄 Blog Section Improvements

- **Updated Blog Posts List:** The blog post listing in `layout/posts/list.html` now has a more structured layout with proper sections and divs.

## 🎨 Global Styles Update

- **SCSS Imports:** Updated `main.scss` to ensure all new and refactored styles are properly imported and structured.

This refactor not only cleans up the structure but also makes future updates easier. More improvements are on the way, but for now, the site is looking and feeling much better! 🚀

Feel free to deep dive into the code changes in this [commit](https://github.com/NotYetFound404/personal-website/commit/335bc0f31b03fcdb1de2aadf5e58181031862c98)