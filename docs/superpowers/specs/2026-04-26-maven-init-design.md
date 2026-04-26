# Maven Init  libmgtDesign 

Date: 2026-04-26

Overview
- Goal: Initialize a single-module Maven Java project for the admin backend (libmgt) using Java 17.
- Coordinates: com.zahan.app:libmgt:0.1.0-SNAPSHOT
- Scope: project skeleton, POM with essential plugins/dependencies, example unit test, and CI workflow.

Project structure
- pom.xml
- src/main/java/com/zahan/app/libmgt
- src/test/java/com/zahan/app/libmgt
- README.md, .gitignore, docs/

POM essentials
- Properties:
  - maven.compiler.source = 17
  - maven.compiler.target = 17
  - project.version = 0.1.0-SNAPSHOT
- Dependencies:
  - junit-jupiter (test)
- Plugins:
  - maven-compiler-plugin (set release/target 17)
  - maven-surefire-plugin (JUnit 5)

Example POM fragment

```xml
<properties>
  <maven.compiler.source>17</maven.compiler.source>
  <maven.compiler.target>17</maven.compiler.target>
  <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>

<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.0</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

CI (GitHub Actions)
- Workflow: .github/workflows/ci.yml
- Trigger: push, pull_request
- Job: runs-on: ubuntu-latest; steps: checkout, setup JDK 17, mvn -B test

Testing
- Use JUnit 5; include a sample TestAppTest in src/test/java to validate setup.

Deliverables
- Committed spec: docs/superpowers/specs/2026-04-26-maven-init-design.md
- Project skeleton (next step: implement archetype or mvn archetype:generate)

Spec self-review checklist (applied)
- No TODO/TBD placeholders.
- Architecture matches feature: skeleton only.
- Scope: single-module init, small enough for one plan.
- Ambiguities: none remain; specific versions can be adjusted later.

Next steps (after your approval of this spec)
1. Create Maven project skeleton (mvn archetype:generate or handcraft pom + directories).
2. Add example unit test and .gitignore.
3. Add GitHub Actions CI workflow.
4. Run tests locally and push.
5. Invoke writing-plans skill to create a concrete implementation plan.

Please review the spec file and tell me if changes are needed before implementation planning.
