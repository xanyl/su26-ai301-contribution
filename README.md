# Contribution [2]: fix: zero contrast text on User Management hover in dark mode
**Contribution Number:** 2
**Student:** Anil Tiwari
**Issue:** [ls1intum/Artemis#12403](https://github.com/ls1intum/Artemis/issues/12403)
**Status:** Phase II

## Why I Chose This Issue
I chose issue #12403 in the Artemis repository because it's a well-defined UI bug with a clear reproduction path. It is labeled as a "good first issue" and "small", making it highly feasible to complete within the remaining timeframe of the AI301 capstone. It provides a great opportunity to dive into a new, large-scale codebase (Artemis) and learn about its frontend styling and dark mode implementation.

## Understanding the Issue
### Problem Description
In the Artemis application, when navigating to the 'Manage' -> 'Overview' page while using dark mode, hovering over the "User management" button causes the text to have zero contrast against the button background. This renders the text completely invisible and unreadable to the user.

### Expected Behavior
The "User management" text should remain clearly readable when hovered over, maintaining sufficient contrast against the button's hover-state background color in dark mode.

### Affected Components
The issue is isolated to the frontend user interface. It will likely require modifying the CSS/SCSS stylesheets—specifically targeting the hover state of the "User management" button (or the shared button component it utilizes) when the dark mode theme is active.

## Reproduction Process

### Environment Setup
1. Forked the `ls1intum/Artemis` repository.
2. Cloned the repository locally.
3. Followed the Artemis developer setup guide to install dependencies and start the local development environment (frontend and backend).
4. Created a local test account with appropriate permissions to access the 'Manage' dashboard.

### Steps to Reproduce
1. Start the Artemis development server and access the local instance in the browser.
2. Log in with an account that has access to the management features.
3. Enable **Dark Mode** in the application settings or user profile.
4. Navigate to **Manage -> Overview**.
5. Hover your cursor over the **User management** button.
6. *Observed result:* The text color blends into the button's hover background color, resulting in zero contrast and making the text entirely unreadable.

### Reproduction Evidence
- **Working Branch:** [https://github.com/xanyl/Artemis/tree/fix/12403-dark-mode-hover] 

## Solution Approach

### Implementation Plan
Using the UMPIRE framework:
- **Understand:** The CSS/SCSS styling for the "User management" button lacks a proper text color override for the `:hover` state when the dark theme is active, causing it to inherit a color that lacks contrast against the dark hover background.
- **Match:** I will inspect other standard buttons within the Artemis dark mode UI to identify the correct contrast variables (e.g., standard SCSS variables for text and background on hover) to ensure my fix matches the project's existing design system.
- **Plan:**
  1. Use browser developer tools to inspect the affected button and locate the exact component and SCSS file responsible for its styling.
  2. Identify how Artemis handles dark mode theming (e.g., through a `.theme-dark` class or specific CSS variables).
  3. Update the `:hover` state for this button class to use a high-contrast text color against the dark background.
  4. Check the button in Light Mode to ensure the CSS change doesn't cause unintended regressions.
- **Implement:** [Link to your commits as you work]
- **Review:** Ensure the CSS changes follow Artemis's styling guidelines, utilizing existing design tokens/variables rather than hardcoded hex values wherever possible.
- **Evaluate:** Manually toggle between light and dark themes to verify the expected behavior in both states.

### Testing Strategy

### Manual Tests
- [ ] Verify the text on the "User management" button is clearly readable when hovered in Dark Mode.
- [ ] Verify the text on the "User management" button remains readable when hovered in Light Mode.
- [ ] Verify that no other adjacent buttons on the 'Manage -> Overview' page were negatively impacted by the styling changes.

# Contribution [1]: feat: widget to display missing / queued movies & episodes

**Contribution Number:** [1]
**Student:** Anil Tiwari
**Issue:** [GitHub issue link](https://github.com/homarr-labs/homarr/issues/5336)
**Status:** [Phase I]

---

## Why I Chose This Issue
I chose issue #5336, "Widget to display missing / queued movies & episodes", because it is an excellent opportunity to work with React, TypeScript, and the Next.js framework in a popular open-source dashboard. Building a widget provides end-to-end experience in frontend component design, API data fetching, and integrating with external services (the *Arr stack) within a large monorepo structure.

---

## Understanding the Issue

### Problem Description
Homarr is a customizable dashboard for self-hosted applications. Many users integrate it with media management software like Radarr (for movies) and Sonarr (for TV shows). Currently, users have to open these individual apps to check if they have missing media or items stuck in their download queue. 

### Expected Behavior
A new widget needs to be created for the Homarr dashboard. This widget should connect to the user's configured media services (like Radarr/Sonarr), fetch the total number of missing and queued items, and display these counts clearly on the dashboard UI.

### Current Behavior
There is currently no dedicated widget to display missing or queued media statistics directly on the Homarr dashboard.

### Affected Components
The changes will primarily take place within the `packages/widgets` (or equivalent widget directory) of the Homarr monorepo, requiring a new UI component and likely leveraging existing API integration functions to fetch the data.

---

## Reproduction Process

### Environment Setup
1. Forked the `homarr-labs/homarr` repository.
2. Cloned the repository locally.
3. Updated the global `pnpm` engine to the required version (>=11.6.0).
4. Installed project dependencies using `pnpm install`.
5. Created a local `.env` file from the `.env.example` template.

### Steps to Reproduce
1. Start the development server using `pnpm dev`.
2. Access the local Homarr dashboard at `http://localhost:3000`.
3. Enter edit mode and attempt to add a new widget.
4. **Observed result:** There is no widget available for "Missing / Queued Media", confirming the feature needs to be implemented.

### Reproduction Evidence
- **Working Branch:** https://github.com/xanyl/homarr/tree/feat/missing-queued-widget

---

## Solution Approach

### Implementation Plan
Using UMPIRE framework (adapted):

* **Understand:** We need to build a new React component for the Homarr dashboard that connects to existing media integrations (like Radarr/Sonarr) to fetch and display the counts of missing and queued media.
* **Match:** I will look at existing widgets in the `packages/widgets` directory (such as the calendar or other Servarr-related widgets) to understand Homarr's pattern for component structure, styling (Mantine), and data fetching (tRPC/React Query).
* **Plan:**
    1.  Locate the widget directory and create a new folder/files for the `missing-queued` widget.
    2.  Investigate how Homarr currently communicates with the *Arr stack APIs to see if endpoints for "missing" and "queued" already exist or need to be added.
    3.  Build the frontend UI component to display the numbers clearly.
    4.  Register the new widget in Homarr's widget configuration so it appears in the "Add Widget" menu.
    5.  Test the widget locally using a mock or real connection to Radarr/Sonarr.
* **Implement:** [Link to your branch/commits as you work]
* **Review:** [Self-review checklist - does it follow the project's contribution guidelines?]
* **Evaluate:** [How will you verify it works?]

## Testing Strategy

### Unit / Manual Tests
- [ ] Verify the widget appears in the "Add Widget" menu.
- [ ] Verify the widget correctly displays the "missing" count from a connected integration.
- [ ] Verify the widget correctly displays the "queued" count from a connected integration.
- [ ] Verify the widget handles states where no integration is connected gracefully (e.g., shows a warning or placeholder). 


### Week 3 Progress (Phase III Build - In Progress)

**What I built so far:**
- Scaffolded the base React UI component for the "Missing / Queued Media" widget in the `packages/widgets` directory.
- Reviewed Homarr's existing Servarr (Radarr/Sonarr) widgets to understand the data fetching patterns.
- Started mapping out the tRPC endpoints needed to pull the "missing" and "queued" counts from the *Arr APIs.

**Challenges faced:**
- Currently figuring out the best way to mock the Radarr/Sonarr API response locally so I can test the UI without a full media server setup.
- Encountered some initial TypeScript type errors when passing the integration configuration props down to the new widget, but working through them.

**Next Steps:**
- Complete the tRPC integration to successfully fetch live data.
- Wire up the fetched data to the Mantine UI components.
- Write unit tests for the widget's empty/disconnected states.

## Phase IV: Submit & Iterate
**PR Link:** https://github.com/homarr-labs/homarr/pull/6078
**PR Description:** Implemented the requested widget to display missing and queued movies/episodes from Radarr and Sonarr integrations on the Homarr dashboard, complete with pagination and responsive sizing.
**Maintainer Feedback:** Received automated review feedback from CodeRabbit identifying a few minor adjustments needed. Addressed these, and the PR has now been successfully merged by the maintainer!
**Status:** Merged

## Learnings & Reflections

### Technical Skills Gained


### Challenges Overcome


### What I'd Do Differently Next Time


---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
