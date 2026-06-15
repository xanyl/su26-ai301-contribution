# Contribution [#]: [Issue Title]

**Contribution Number:** [1]  
**Student:** Anil Tiwari  
**Issue:** [[GitHub issue link]  ](https://github.com/documentdb/functional-tests/issues/207)
**Status:** [Phase I]

---

## Why I Chose This Issue

I chose issue #207, "Add compatibility test for $bsonSize", because it aligns perfectly with my Python skills and my goal to learn more about database testing frameworks. The issue is well-scoped, labeled as a "good first issue," and has clear existing patterns to follow for expression-operator tests.

---

## Understanding the Issue

### Problem Description

The documentdb/functional-tests framework is designed to validate DocumentDB functionality against MongoDB. Currently, the framework lacks automated test coverage for the $bsonSize aggregation operator, meaning there is no automated way to ensure DocumentDB calculates BSON expression sizes correctly.

### Expected Behavior

The testing framework should include functional tests (using pytest) that verify the $bsonSize operator correctly calculates and returns the size of a given BSON object/expression in bytes.

### Current Behavior

No tests exist for the $bsonSize operator.

### Affected Components

The tests/aggregate/ directory (where a new test file, e.g., test_bsonsize.py, will be created).

---

## Reproduction Process

### Environment Setup
Cloned the `documentdb/functional-tests` repository and set up a Python virtual environment. Installed dependencies using `pip install -r requirements.txt`. Started a local MongoDB instance to serve as the baseline test engine.

### Steps to Reproduce
1. Search the codebase for existing `$bsonSize` tests using the command: `grep -r "$bsonSize" tests/`
2. Observe that there are no existing functional test files or assertions covering the `$bsonSize` operator.
3. Run the existing aggregation test suite to ensure the baseline environment works: `pytest -m aggregate --connection-string mongodb://localhost:27017`
4. **Observed result:** Tests pass, but no `$bsonSize` tests are executed. The missing test coverage gap is confirmed.

### Reproduction Evidence
- **Working Branch:** https://github.com/xanyl/functional-tests/

---

## Solution Approach

### Implementation Plan
Using UMPIRE framework (adapted):

* **Understand:** The DocumentDB functional testing framework lacks test coverage for the `$bsonSize` aggregation operator. We need to add tests to verify that DocumentDB correctly calculates and returns the BSON size of a given expression in bytes.
* **Match:** Existing tests in the `tests/aggregate/` directory (like `test_query_operators.py`) provide a pattern for testing expression operators. I will match their structure for fixtures, data insertion, and custom assertions (e.g., `assert_document_match`).
* **Plan:**
    1. Create a new test file `tests/aggregate/test_bsonsize.py`.
    2. Write a `test_bsonsize_basic` function that inserts documents with various data types (string, object, array, integer).
    3. Execute an aggregate pipeline using `{"$project": {"size": {"$bsonSize": "$field"}}}`.
    4. Write tests for edge cases (e.g., when the field is null or missing).
    5. Add appropriate standard markers like `@pytest.mark.aggregate`.

**Implement:** [Link to your branch/commits as you work]

**Review:** [Self-review checklist - does it follow the project's contribution guidelines?]

**Evaluate:** [How will you verify it works?]

---

## Testing Strategy

### Unit Tests

- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]
- [ ] Test case 3: [Description]

### Integration Tests

- [ ] Integration scenario 1
- [ ] Integration scenario 2

### Manual Testing

[What you tested manually and results]

---

## Implementation Notes

### Week [X] Progress

[What you built this week, challenges faced, decisions made]

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
