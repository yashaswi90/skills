# Java Test Coverage Enforcer

## Overview

The **Java Test Coverage Enforcer** is an OpenHands skill that automatically achieves and enforces 95% line coverage for Java projects. It intelligently identifies your build tool, runs tests with JaCoCo coverage analysis, and iteratively creates missing tests until the coverage goal is met.

## Skill Details

- **Name**: `java-coverage-enforcer`
- **Type**: Knowledge Microagent
- **Version**: 1.0.0
- **Agent**: CodeActAgent

## Trigger Keywords

This skill is automatically activated when you mention any of the following in your conversation:

- `java test coverage`
- `jacoco`
- `95% java`
- `maven test`
- `test report`
- `java`
- `coverage`

## Features

### 🔍 Automatic Detection
- Automatically detects Maven or Gradle build systems
- Identifies existing JaCoCo configuration
- Adds JaCoCo plugin if missing (with authorization)

### 🧪 Smart Test Execution
- **Maven Projects**: Executes `mvn clean verify`
- **Gradle Projects**: Executes `./gradlew test jacocoTestReport`
- Parses test results from Surefire/Gradle reports
- Extracts coverage metrics from JaCoCo reports

### 📈 Iterative Improvement Loop
- Identifies uncovered classes and methods
- Creates or updates JUnit 5 tests automatically
- Uses Mockito for complex dependencies
- Repeats until ≥95% coverage is achieved

### 📊 Detailed Reporting
Provides a comprehensive summary table with:
- Total tests run, passed, and failed
- Total lines of code
- Lines covered and missed
- Final coverage percentage
- Pass/Fail status (PASSED only if coverage ≥95% and no failed tests)

## Usage Examples

### Example 1: Simple Coverage Request
```
User: "Check the java test coverage for this project"
```
The skill will automatically:
1. Detect the build tool
2. Run tests with coverage
3. Report current coverage
4. Suggest improvements if below 95%

### Example 2: Enforce 95% Coverage
```
User: "I need 95% java test coverage with a detailed report"
```
The skill will:
1. Run initial coverage analysis
2. Identify gaps
3. Create missing tests
4. Re-run until 95% is achieved
5. Provide final summary

### Example 3: JaCoCo Specific
```
User: "Generate jacoco test report"
```
The skill activates and provides JaCoCo-specific reporting.

## Workflow

```
┌─────────────────────────────────────┐
│ 1. Detection & Setup                │
│  - Identify Maven/Gradle            │
│  - Check/Add JaCoCo plugin          │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 2. Execution & Data Collection      │
│  - Run tests with coverage          │
│  - Parse test results               │
│  - Extract coverage metrics         │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 3. Coverage < 95%? (Loop)           │
│  - Identify uncovered code          │
│  - Generate missing tests           │
│  - Re-run tests                     │
└──────────────┬──────────────────────┘
               │
               ▼
┌─────────────────────────────────────┐
│ 4. Final Report                     │
│  - Display coverage summary         │
│  - Show PASSED/FAILED status        │
└─────────────────────────────────────┘
```

## Output Format

The skill provides a standardized summary table:

```markdown
### 📊 Test Execution & Coverage Summary
| Category | Metric | Value |
| :--- | :--- | :--- |
| **Test Results** | Total Tests Run | 45 |
| | Tests Passed | 45 |
| | Tests Failed | 0 |
| **Line Metrics** | Total Lines of Code | 1,250 |
| | Lines Covered | 1,200 |
| | Lines Missed | 50 |
| **Final Score** | **Total Coverage %** | **96.0%** |
| | **Status** | **PASSED** |
```

## Requirements

### Build Tools
- **Maven**: Requires `pom.xml` in project root
- **Gradle**: Requires `build.gradle` or `build.gradle.kts`

### Java Version
- Java 8 or higher
- JUnit 5 (Jupiter) for test creation
- Mockito for mocking dependencies

### JaCoCo Plugin
The skill will automatically add JaCoCo if not present:

**Maven:**
```xml
<plugin>
    <groupId>org.jacoco</groupId>
    <artifactId>jacoco-maven-plugin</artifactId>
    <version>0.8.11</version>
</plugin>
```

**Gradle:**
```groovy
plugins {
    id 'jacoco'
}
```

## Coverage Criteria

### PASSED Status Requirements
- ✅ Coverage ≥ 95%
- ✅ All tests passed (0 failures)

### Report Locations
- **Maven**: `target/site/jacoco/index.html` or `target/site/jacoco/jacoco.xml`
- **Gradle**: `build/reports/jacoco/test/html/index.html` or `build/reports/jacoco/test/jacocoTestReport.xml`

## Best Practices

1. **Start Early**: Run coverage checks early in development
2. **Incremental Testing**: Let the skill create tests incrementally
3. **Review Generated Tests**: While the skill creates tests automatically, review them for quality
4. **Mock Complex Dependencies**: The skill uses Mockito for external dependencies
5. **CI/CD Integration**: Use this skill as part of your CI/CD pipeline

## Troubleshooting

### Issue: Skill Not Triggering
**Solution**: Ensure you use one of the trigger keywords in your message:
- ✅ "Check the **java test coverage**"
- ✅ "Run **jacoco** report"
- ❌ "Test the application" (too generic)

### Issue: JaCoCo Plugin Not Found
**Solution**: The skill will automatically add it. If manual addition is needed:
```bash
# Maven
mvn org.jacoco:jacoco-maven-plugin:prepare-agent

# Gradle
./gradlew jacocoTestReport
```

### Issue: Coverage Stuck Below 95%
**Solution**: The skill will iterate and create tests. If stuck:
1. Check logs for uncovered classes
2. Verify test file locations (`src/test/java`)
3. Ensure proper test naming conventions

## Integration with OpenHands

This skill is part of the OpenHands skills library located in:
```
OpenHands/skills/java-test-enforcer.md
```

### Loading the Skill
The skill is automatically loaded when OpenHands starts. To reload after changes:
1. Restart OpenHands application
2. Use any trigger keyword to activate

### Verifying Skill is Loaded
Check OpenHands logs for:
```
Loading user workspace microagents: [..., 'java-coverage-enforcer', ...]
```

Or when triggered:
```
Microagent 'java-coverage-enforcer' triggered by keyword 'java test coverage'
```


## Contributing

To modify or enhance this skill:

1. Edit `skills/java-test-enforcer.md`
2. Update the frontmatter metadata if needed
3. Test with a Java project
4. Restart OpenHands to reload

**Last Updated**: February 13, 2026
**Maintained By**: OpenHands Community
