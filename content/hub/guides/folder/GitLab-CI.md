---
type: docs
url: "hub/docs/folder/CIPipeline"
---

# GitLab CI/CD Overview

Continuous Integration (CI) is a way to automatically test, build, and validate your code whenever changes are made. This reduces errors, speeds up development, and ensures that your project stays in a working state.

**GitLab** provides built-in CI/CD features through its `.gitlab-ci.yml` file. This file, placed in the root of your repository, tells GitLab how to build and test your project. It defines stages and scripts that are run in a clean environment every time changes are pushed.

Rather than manually running build commands or tests, GitLab CI does it for you in a controlled and repeatable way.

This document outlines how GitLab CI/CD works, including the role of the `.gitlab-ci.yml` file, shell scripts, and external tools such as build systems. This applies broadly across software projects, including those that use systems like Meson and Ninja.

## GitLab CI/CD Basics

GitLab CI/CD automates tasks such as building, testing, and deploying code. It is controlled by a file named `.gitlab-ci.yml` at the root of the repository. This file defines:

- **Stages**: Ordered groups of jobs (e.g., `build`, `test`, `deploy`)
- **Jobs**: Individual tasks to run within each stage
- **Scripts**: Shell commands executed for each job
- **Runners**: Agents (virtual machines, Docker containers, or shell environments) that GitLab uses to run jobs defined in the pipeline. They can be shared (hosted by GitLab) or custom (self-hosted).

> Note: The `.gitlab-ci.yml` file must follow strict YAML syntax. Indentation errors or syntax issues can break the pipeline.

### Minimal Example

```
stages:
  - build
  - test

build-job:
  stage: build
  script:
    - ./configure
    - make

test-job:
  stage: test
  script:
    - make check
```

Each job runs in its own environment and is triggered according to the stage order.

## Role of Shell Scripts

Jobs in `.gitlab-ci.yml` typically invoke shell commands directly. For better structure and reusability, complex operations are often moved into separate scripts stored in the repository.

```
script:
  - ./build/linux/appimage/
```

This keeps the `.gitlab-ci.yml` file clean and makes build logic easier to maintain.

## Integration with Build Systems

GitLab CI/CD is agnostic to the build system used. It simply executes the commands provided. GIMP uses **Meson** and **Ninja** to prepare and then compile the code.

For example, with Meson and Ninja:

```
script:
  - meson setup _build
  - ninja -C _build
```

Here:

- `meson setup` prepares the build directory and generates `build.ninja`
- `ninja` runs the build commands as defined

## Meson Build System Structure

The **Meson** build system uses a root `meson.build` file placed at the project’s root directory. This file defines the top-level build configuration and entry point for the build process.

- The root `meson.build` is typically located in the same directory as `.gitlab-ci.yml`
- From there, it **cascades recursively** into subdirectories, each of which may have its own `meson.build` file
- These subdirectory files define targets, sources, dependencies, and build instructions relevant to that directory

Meson automatically discovers and includes subdirectory build files when instructed via `subdir()` directives in the root or parent `meson.build` files.

> The `subdir()` function in Meson is used in a parent `meson.build` file to include another directory’s build file and its targets.

### Example Structure

```
project-root/
├── .gitlab-ci.yml
├── meson.build              <-- Root Meson file
├── src/
│   ├── meson.build          <-- Subdirectory Meson file
│   └── some_source.c
├── data/
│   ├── meson.build
│   └── icons/
```

In this structure:

- The root `meson.build` file configures the overall build environment
- Subdirectory `meson.build` files handle compilation details for specific components or modules
- This hierarchical layout keeps build logic modular and maintainable

## Pipeline Stages and Dependencies

A typical pipeline consists of multiple stages:

```
stages:
  - prepare
  - build
  - test
  - package
  - deploy
```

Each job within a stage runs in parallel. A stage only begins after the previous one completes successfully.

```
build:
  stage: build
  script:
    - ./ci/scripts/build.sh

test:
  stage: test
  script:
    - ./ci/scripts/test.sh
```

GitLab handles scheduling, isolation, logging, and failure propagation automatically.

## Summary

- `.gitlab-ci.yml` defines the structure and logic of the pipeline
- Jobs contain shell commands or external scripts
- GitLab CI/CD does not care which tools you use—it runs what you define
- Tools like Meson and Ninja are used inside jobs as part of the build process
- The `subdir()` directive allows Meson to include subdirectory build definitions

GitLab CI/CD’s modular and tool-agnostic architecture allows it to support diverse project structures and build systems with minimal changes. Artbox uses the GitLab CI to build it's AppImage for Debian based platforms.
