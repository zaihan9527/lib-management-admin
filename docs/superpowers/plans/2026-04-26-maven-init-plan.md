# Maven Init Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Initialize a single-module Maven Java 17 project skeleton for the admin backend (libmgt) with example tests and CI.

**Architecture:** Minimal single-module project: Java sources, tests, and build config. No external services.

**Tech Stack:** Maven, Java 17, JUnit 5, GitHub Actions.

---

### Task 1: Create project skeleton and POM

**Files:**
- Create: `pom.xml`
- Create: `src/main/java/com/zahan/app/libmgt/App.java`
- Create: `src/test/java/com/zahan/app/libmgt/AppTest.java`
- Create: `.gitignore`

- [ ] **Step 1: Add pom.xml**

Add the following complete pom.xml at project root:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.zahan.app</groupId>
  <artifactId>libmgt</artifactId>
  <version>0.1.0-SNAPSHOT</version>
  <packaging>jar</packaging>

  <properties>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <junit.jupiter.version>5.10.0</junit.jupiter.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter</artifactId>
      <version>${junit.jupiter.version}</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>
    <plugins>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.11.0</version>
        <configuration>
          <release>17</release>
        </configuration>
      </plugin>
      <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-surefire-plugin</artifactId>
        <version>3.1.2</version>
        <configuration>
          <useModulePath>false</useModulePath>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

- [ ] **Step 2: Add App.java**

Create `src/main/java/com/zahan/app/libmgt/App.java` with:

```java
package com.zahan.app.libmgt;

public class App {
    public static String greet() {
        return "Hello, libmgt";
    }

    public static void main(String[] args) {
        System.out.println(greet());
    }
}
```

- [ ] **Step 3: Add AppTest.java**

Create `src/test/java/com/zahan/app/libmgt/AppTest.java` with:

```java
package com.zahan.app.libmgt;

import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class AppTest {
    @Test
    void testGreet() {
        assertEquals("Hello, libmgt", App.greet());
    }
}
```

- [ ] **Step 4: Add .gitignore**

Create `.gitignore` with common Java/Maven ignores:

```
/target/
/.idea/
*.iml
*.class
.DS_Store
```

- [ ] **Step 5: Run mvn -B test to validate**

Run:

```
mvn -B test
```

Expected: build success and tests pass. Output contains: "BUILD SUCCESS"

- [ ] **Step 6: Commit these files**

Commands:

```
git add pom.xml src/main/java src/test/java .gitignore
git commit -m "feat: init maven single-module project (Java 17)"
```

---

### Task 2: Add GitHub Actions CI workflow

**Files:**
- Create: `.github/workflows/ci.yml`

- [ ] **Step 1: Add workflow file**

Create `.github/workflows/ci.yml` with:

```yaml
name: CI

on:
  push:
    branches: [ main, master ]
  pull_request:
    branches: [ main, master ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Set up JDK 17
        uses: actions/setup-java@v4
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build and test
        run: mvn -B test
```

- [ ] **Step 2: Commit workflow**

```
git add .github/workflows/ci.yml
git commit -m "ci: add GitHub Actions workflow for Maven build"
```

---

### Task 3: Verify CI locally (optional) and final checks

- [ ] **Step 1: Run mvn -B test locally again** (ensure no flakiness)
- [ ] **Step 2: Push to remote**

```
git push origin HEAD
```

Expected: GitHub shows workflow run for push.

---

## Self-review mapping back to spec

- Spec: project skeleton, POM, example unit test,  covered by Tasks 3.1CI 
- No placeholders; all steps contain exact files and code.

---

Plan saved to `docs/superpowers/plans/2026-04-26-maven-init-plan.md`.

Execution options:
1. Subagent-Driven (recommended)
2. Inline Execution (run commands here)

Which execution option to use?
