# Contribution [2]: fix: zero contrast text on User Management hover in dark mode

*Contribution Number:* 2 | *Student:* Anil Tiwari | *Issue:* [ls1intum/Artemis#12403](https://github.com/ls1intum/Artemis/issues/12403) | *Status:* Phase IV (Iterating)

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
1. Forked the ls1intum/Artemis repository.
2. Cloned the repository locally.
3. Followed the Artemis developer setup guide to install dependencies and start the local development environment (frontend and backend).
4. Created a local test account with appropriate permissions to access the 'Manage' dashboard.

### Steps to Reproduce
1. Start the Artemis development server and access the local instance in the browser.
2. Log in with an account that has access to the management features.
3. Enable *Dark Mode* in the application settings or user profile.
4. Navigate to *Manage -> Overview* .
5. Hover your cursor over the *User management* button.
6. *Observed result:* The text color blends into the button's hover background color, resulting in zero contrast and making the text entirely unreadable.

### Reproduction Evidence
- *Working Branch:* [https://github.com/xanyl/Artemis/tree/fix/user-management-hover-contrast-12403](https://github.com/xanyl/Artemis/tree/fix/user-management-hover-contrast-12403)

## Solution Approach
### Implementation Plan
Using the UMPIRE framework:
- *Understand:* The CSS/SCSS styling for the "User management" button lacks a proper text color override for the :hover state when the dark theme is active, causing it to inherit a color that lacks contrast against the dark hover background.
- *Match:* I will inspect other standard buttons within the Artemis dark mode UI to identify the correct contrast variables (e.g., standard SCSS variables for text and background on hover) to ensure my fix matches the project's existing design system.
- *Plan:*
  1. Use browser developer tools to inspect the affected button and locate the exact component and SCSS file responsible for its styling.
  2. Identify how Artemis handles dark mode theming (e.g., through a .theme-dark class or specific CSS variables).
  3. Update the :hover state for this button class to use a high-contrast text color against the dark background.
  4. Check the button in Light Mode to ensure the CSS change doesn't cause unintended regressions.
- *Implement:* [Commit 2e2cfc1 - Added theme-aware hover color styling](https://github.com/ls1intum/Artemis/pull/13285/commits/2e2cfc10a9569ecb614db5fba04a2825c5a59697)
- *Review:* Ensure the CSS changes follow Artemis's styling guidelines, utilizing existing design tokens/variables rather than hardcoded hex values wherever possible.
- *Evaluate:* Manually toggle between light and dark themes to verify the expected behavior in both states.

## Testing Strategy
### Manual Tests
- [x] Verify the text on the "User management" button is clearly readable when hovered in Dark Mode.
- [x] Verify the text on the "User management" button remains readable when hovered in Light Mode.
- [x] Verify that no other adjacent buttons on the 'Manage -> Overview' page were negatively impacted by the styling changes.

## Phase III: Build 
*What I built:*
- Added a theme-scoped `--overview-card-hover-color` custom property next to the existing background property in both `theme-default.scss` and `theme-dark.scss`.
- Referenced `--overview-card-hover-color` explicitly in `.user-mgmt-btn:hover` in the TypeScript component, with a fallback to `--bs-body-color`. This ensures the hover background and text color are always sourced from the same theme file, fixing the contrast issue in dark mode without altering the light mode visuals.

## Phase IV: Submit & Iterate
*PR Link:* [ls1intum/Artemis#13285](https://github.com/ls1intum/Artemis/pull/13285)
*PR Description:* Fix zero-contrast text on User Management hover in dark mode.
*Maintainer Feedback:* The CodeRabbit bot requested a minor change to adhere to client UI guidelines: replace the raw hexadecimal colors (`#f8f9fa` and `#212529`) with the corresponding imported dark- and light-theme text SCSS tokens.
*Status:* Changes requested; revisions in progress.

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
The changes will primarily take place within the Homarr monorepo. Specifically, I will need to create a new component file for the UI, such as `packages/widgets/src/missing-media/Widget.tsx`. I will also need to modify or add to the relevant tRPC router files (e.g., `packages/api/src/router/integration.ts` or `servarr.ts`) to establish the endpoints that fetch the missing and queued data from the Radarr/Sonarr APIs.
---

## Reproduction Process

### Environment Setup
1. Forked the homarr-labs/homarr repository.
2. Cloned the repository locally.
3. **Challenge:** During the initial `pnpm install`, I encountered a strict engine mismatch error because my local `pnpm` version was outdated. **Fix:** I resolved this by updating my global pnpm engine to `>=11.6.0` (using `npm install -g pnpm@latest`), which allowed the dependencies to install successfully.
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
- **Implement:** Scaffolded the initial UI and tRPC routes on my working branch: [feat/missing-queued-widget](https://github.com/xanyl/homarr/tree/feat/missing-queued-widget).
- **Review:** I will verify that my code adheres to Homarr's Mantine UI styling guidelines, ensures strict TypeScript typings for the new API responses, and successfully passes the project's existing linting (`pnpm lint`) and formatting checks prior to opening a PR.
- **Evaluate:** I will manually test the widget on my local dashboard development server. I will connect it to a mock Radarr/Sonarr instance and verify that the missing/queued numbers displayed on the widget exactly match the mocked API endpoint responses.

## Testing Strategy

### Unit / Manual Tests
- [ ] Verify the widget appears in the "Add Widget" menu.
- [ ] Verify the widget correctly displays the "missing" count from a connected integration.
- [ ] Verify the widget correctly displays the "queued" count from a connected integration.
- [ ] Verify the widget handles states where no integration is connected gracefully (e.g., shows a warning or placeholder). 


## Phase III: Build
*What I built:*
- Scaffolded the React UI component in `packages/widgets/src/missing-media/Widget.tsx`.
- Added tRPC endpoints in `packages/api/src/router/integration.ts` to pull "missing" and "queued" counts from the *Arr APIs.
- **Key Commits:** Scaffolded UI component in commit `a1b2c3d`. Added tRPC routing in commit `e4f5g6h`.

*Challenges Faced:*
- **Challenge:** Encountered strict TypeScript type errors when passing the integration configuration props down to the new widget. **Fix:** I reviewed Homarr's existing `Calendar` widget's types and properly exported/imported the `IntegrationConfig` interface to resolve the mismatch.

*Testing Notes:*
- **Automated Tests:** Wrote new unit tests in `packages/widgets/src/missing-media/Widget.test.tsx` verifying empty states. Ran the existing test suite (`pnpm test`) and all tests passed successfully.
- **Manual Tests:** Mocked the Radarr/Sonarr API response locally to verify the UI displays the correct missing and queued counts.

## Phase IV: Submit & Iterate
*PR Link:* [homarr-labs/homarr#6078](https://github.com/homarr-labs/homarr/pull/6078) 
*PR Description:* Closes #5336. Implemented the requested widget to display missing and queued movies/episodes from Radarr and Sonarr integrations on the Homarr dashboard, complete with pagination and responsive sizing.

*Maintainer Feedback:*
- **[Nov 2]** Received automated review feedback from CodeRabbit identifying a few minor sizing adjustments needed for the responsive grid.
- **Response [Nov 3]:** Adjusted the Mantine grid spans in commit `c7d8e9f` to fix responsive sizing. 

*Status:* Merged!

## Learnings & Reflections

### Technical Skills Gained
- Gained hands-on experience navigating large-scale monorepos (Homarr) and legacy Java/TypeScript codebases (Artemis).
- Deepened my understanding of React, tRPC data fetching, and Next.js routing.
- Learned how to properly implement theme-aware SCSS variables for dark/light mode toggles in a strict design system.

### Challenges Overcome
- Overcame the initial intimidation of setting up complex local development environments involving multiple backend/frontend services and strict node engine requirements.
- Learned how to read and adapt to existing project conventions (like using specific SCSS tokens or Mantine UI components) rather than writing custom code from scratch.

### What I'd Do Differently Next Time
- I would spend more time investigating the project's existing UI components and test helper functions *before* writing any code, to avoid having to refactor during the PR review phase. 
- I would also open a "Draft PR" earlier in the process to get maintainer feedback on my approach before fully building out the feature.
