# GitHub Actions CI Troubleshooting Report

## Overview

During development of the GitHub Actions CI pipeline, workflow execution was monitored through the GitHub Actions interface.

A controlled test failure was introduced to demonstrate the troubleshooting and recovery process.

---

## Issue Identified

One of the automated calculator tests was temporarily changed from:

```python
assert add(2, 3) == 5
```

to:

```python
assert add(2, 3) == 7
```

The GitHub Actions workflow correctly detected the failure.

The `Run tests` step was marked as failed.

---

## Investigation

The GitHub Actions job logs were opened and the failed `Run tests` step was inspected.

The test output showed an assertion failure because the calculator returned:

```text
5
```

while the test incorrectly expected:

```text
7
```

The failure demonstrated that the CI pipeline was correctly executing the automated test suite and stopping the workflow when a test did not pass.

---

## Resolution

The incorrect assertion was corrected:

```python
assert add(2, 3) == 7
```

The change was committed and pushed to GitHub.

The GitHub Actions workflow automatically executed again.

---

## Result

The second workflow execution completed successfully.

The final pipeline showed:

```text
✓ Checkout repository
✓ Set up Python
✓ Install dependencies
✓ Run tests
✓ Run application validation
✓ Build validation
```

The test suite completed with:

```text
5 passed
```

---

## Troubleshooting Process

The troubleshooting process followed this sequence:

```text
Workflow Failure
      ↓
Open GitHub Actions
      ↓
Identify Failed Job
      ↓
Open Failed Step
      ↓
Review Test Logs
      ↓
Identify Assertion Error
      ↓
Correct Source Code
      ↓
Commit and Push
      ↓
Re-run CI Automatically
      ↓
Successful Pipeline
```

---

## Lessons Learned

The exercise demonstrated the value of Continuous Integration because problems are identified automatically after code changes.

The GitHub Actions logs provide useful information for identifying:

* Failed tests
* Dependency problems
* Python errors
* Configuration issues
* Build failures

The troubleshooting exercise also demonstrated the importance of maintaining reliable automated tests and reviewing CI logs before making changes to the pipeline configuration.

---

## Final Status

**Issue:** Automated test failure.

**Cause:** Incorrect expected test value.

**Resolution:** Corrected the test assertion.

**Result:** CI pipeline passed successfully.

**Status:** Resolved.
