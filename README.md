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

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

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

### Week [Y] Progress

[Continue documenting as you work]

### Code Changes

- **Files modified:** [List]
- **Key commits:** [Links to important commits]
- **Approach decisions:** [Why you chose certain approaches]

---

## Pull Request

**PR Link:** [GitHub PR URL when submitted]

**PR Description:** [Draft or final PR description - much of the content above can be adapted]

**Maintainer Feedback:**
- [Date]: [Summary of feedback received]
- [Date]: [How you addressed it]

**Status:** [Awaiting review / Iterating / Approved / Merged]

---

## Learnings & Reflections

### Technical Skills Gained

[What you learned technically]

### Challenges Overcome

[What was hard and how you solved it]

### What I'd Do Differently Next Time

[Reflection on your process]

---

## Resources Used

- [Link to helpful documentation]
- [Tutorial or Stack Overflow post that helped]
- [GitHub issues or discussions that helped]
