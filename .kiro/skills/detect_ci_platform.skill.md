---
name: detect_ci_platform
description: Detect whether the project uses GitHub or GitLab for CI. Use before generating a CI pipeline.
---

# Skill: detect_ci_platform

## Goal
Detect the CI platform and existing pipeline config.

## Instructions
- Run `git remote -v` or read `.git/config` to check remote URL
  - `github.com` → platform = github
  - `gitlab.com` → platform = gitlab
- Check for existing config:
  - `.github/workflows/*.yml` → github (already configured)
  - `.gitlab-ci.yml` → gitlab (already configured)
- If undetectable → platform = github (default)

### Also detect from project files:
- `package.json` scripts: extract `test`, `build`, `lint` commands
- `Makefile`: extract `test`, `build`, `lint` targets
- `pyproject.toml` / `setup.cfg`: extract test command (pytest, unittest)
- `go.mod`: test = `go test ./...`, build = `go build ./...`
- `pom.xml`: build = `mvn package`, test = `mvn test`
- `build.gradle`: build = `./gradlew build`, test = `./gradlew test`
- `Cargo.toml`: build = `cargo build --release`, test = `cargo test`
- `Gemfile`: test = `bundle exec rspec` or `bundle exec rake test`

## Output
platform, test_command, build_command, lint_command
