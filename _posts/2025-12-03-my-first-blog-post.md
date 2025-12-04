---
layout: post
title:  "HoopCounter Pro: Building a Multi-Language Basketball Scoreboard from Scratch"
date:   2025-12-04 14:30:00 +0800
categories: [Project, Frontend]
tags: [JavaScript, GitHub Pages, Basketball, Open Source]
---

# 🏀 HoopCounter Pro: A Multi-Language Basketball Scoreboard with Smart Foul Alerts

Welcome to my blog! Following the setup of the blog framework, I'm excited to share my first complete frontend project today — **HoopCounter Pro**. This is a single-page application deployed on GitHub Pages. It's not just a scoreboard; it's a practical case study integrating international basketball rules, multi-language support, and local storage technology.

## Project Quick Links

Before diving into the details, you can experience the final product directly:

*   **🌐 Live Demo**: [https://bannnnnana.github.io/HoopCounter-Pro/](https://bannnnnana.github.io/HoopCounter-Pro/)
*   **💻 Source Code**: [https://github.com/bannnnnana/HoopCounter-Pro](https://github.com/bannnnnana/HoopCounter-Pro)

## Inspiration & Core Objectives

As a basketball enthusiast and a frontend learner, I noticed the lack of convenient and rule-aware digital tools for informal games. My goal was to build a tool that is:

1.  **Immediately Usable**: No installation, accessible via any modern web browser.
2.  **Globally Relevant**: Adapts to different basketball rules (FIBA, NBA, NCAA) and languages.
3.  **Persistent & Reliable**: Saves the game state locally so that accidentally refreshing the page doesn't ruin the match.
4.  **Visually Pleasing**: Employs a clean, dark-themed UI inspired by developer-friendly interfaces like GitHub's.

## Technical Deep Dive: Key Features & Implementation

### 1. Intelligent Foul Tracking & Alert System
The core differentiator of HoopCounter Pro is its rule-aware foul system. Instead of just counting, it actively monitors limits.

**How it works:**
- A configuration object defines foul limits for different rule sets (e.g., 4 fouls/quarter for FIBA).
- The app listens to every foul increment.
- Upon reaching the threshold, it triggers a visual warning badge on the team card *and* a modal alert.
- This was implemented using a state management pattern and event listeners.

### 2. Multi-Language Engine with Dynamic UI Update
Supporting 8 languages required a scalable approach.

**Implementation Strategy:**
- Created a central `translations` object acting as a key-value store for all UI strings in every language.
- Wrote a `updateUI()` function that doesn't just translate text but also switches attributes like `placeholder` or `title`.
- The language switch is handled by a `change` event listener on the dropdown, which updates the global `state.language` and re-renders the UI.

### 3. Single-File Application Architecture
For portability and simplicity, the entire project is one `index.html` file containing all HTML, CSS, and JavaScript.

**The Challenge & Solution:**
- **Challenge**: Avoiding a tangled, unmaintainable codebase.
- **Solution**: Adopting a modular structure *within* the single file:
    - **CSS**: Used clear, commented sections (Reset, Layout, Components, etc.).
    - **JavaScript**: Employed an object-oriented pattern, encapsulating state, methods, and initialization logic within a main `app` object or using modules conceptually.

### 4. State Persistence with `localStorage`
To prevent data loss, the game state is saved after every action.

**Code Snippet:**
```javascript
const state = {
    teamA: { score: 0, fouls: 0 },
    teamB: { score: 0, fouls: 0 },
    language: 'en',
    // ... other state
};

function saveState() {
    localStorage.setItem('hoopCounterState', JSON.stringify(state));
}

// Called after every score change, foul change, or setting update
