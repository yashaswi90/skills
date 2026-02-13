---
name: java-coverage-enforcer
type: knowledge
version: 1.0.0
agent: CodeActAgent
triggers:
  - "java test coverage"
  - "jacoco"
  - "95% java"
  - "maven test"
  - "test report"
  - "java"
  - "coverage"
---

# Java Test Coverage Specialist

Your goal is to achieve **95% line coverage** and provide a detailed execution summary for this Java project.

## Step-by-Step Workflow

### 1. Detection & Setup
- Identify the build tool: Maven (`pom.xml`) or Gradle (`build.gradle`).
- **Plugin Check:** Ensure the **JaCoCo** plugin is present. If missing, you are authorized to add the standard JaCoCo Maven/Gradle plugin to enable coverage data collection.

### 2. Execution & Data Collection
- **Maven:** Run `mvn clean verify`. This executes tests and generates JaCoCo reports.
- **Gradle:** Run `./gradlew test jacocoTestReport`.
- **Parse Test Results:** Look into `target/surefire-reports` (Maven) or `build/test-results` (Gradle) to count Passed/Failed/Skipped tests.
- **Parse Coverage:** Look into `target/site/jacoco/index.html` or `jacoco.xml` to extract precise line coverage data.

### 3. Iterative Improvement (The 95% Loop)
- Identify uncovered classes and methods from the JaCoCo report.
- Create or update JUnit 5 tests in `src/test/java` using **Mockito** where necessary.
- **Repeat** execution until the total line coverage is $\ge 95\%$.

## Required Final Output
Once the goal is reached (or if you are blocked), you must display a final summary in this exact format:

### 📊 Test Execution & Coverage Summary
| Category | Metric | Value |
| :--- | :--- | :--- |
| **Test Results** | Total Tests Run | [Count] |
| | Tests Passed | [Count] |
| | Tests Failed | [Count] |
| **Line Metrics** | Total Lines of Code | [Count] |
| | Lines Covered | [Count] |
| | Lines Missed | [Count] |
| **Final Score** | **Total Coverage %** | **[Percentage]%** |
| | **Status** | **[PASSED/FAILED]** |

> **Note:** The status is PASSED only if Coverage $\ge 95\%$ and Failed Tests = 0.
