---
name: generate_ci_pipeline
description: Generate a GitHub Actions or GitLab CI pipeline file. Use after detect_ci_platform.
---

# Skill: generate_ci_pipeline

## Goal
Generate a production-ready CI pipeline file.

## Instructions

### For GitHub Actions → `.github/workflows/ci.yml`
- Trigger on: `push` and `pull_request` to `main`
- Use `actions/checkout@v4` and appropriate setup action:
  - node: `actions/setup-node@v4` with `cache: npm`
  - python: `actions/setup-python@v5` with pip cache
  - go: `actions/setup-go@v5`
  - java: `actions/setup-java@v4` with temurin distribution
  - rust: `dtolnay/rust-toolchain@stable`
  - ruby: `ruby/setup-ruby@v1` with bundler-cache
- Steps: checkout → setup → install deps → lint (if available) → test → build
- Cache dependencies using the appropriate cache key

### For GitLab CI → `.gitlab-ci.yml`
- Stages: `install`, `lint`, `test`, `build`
- Use official language images (e.g. `node:lts-alpine`, `python:3.12-slim`)
- Cache `node_modules` / `.venv` / Go module cache between jobs
- Only run `build` on `main` branch

### General rules
- Skip lint stage if no lint command detected
- Skip build stage if no build command detected
- Always run tests

## Output
CI pipeline file written to the project
