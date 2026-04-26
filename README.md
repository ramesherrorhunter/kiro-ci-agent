# ci-agent

An intelligent Kiro CLI agent that auto-generates GitHub Actions or GitLab CI pipelines by analyzing your codebase — no manual configuration needed.

---

## Purpose

Eliminate the manual effort of writing CI pipelines. The agent inspects your project, detects your language, framework, and available scripts, then produces a production-ready pipeline file.

---

## Solutions Offered

| Problem | Solution |
|---|---|
| Writing CI pipelines from scratch | Auto-generates based on project files |
| Missing cache configuration | Automatically caches dependencies |
| Wrong test/build commands | Infers commands from package.json, Makefile, etc. |
| GitHub vs GitLab confusion | Auto-detects platform from git remote |
| Skipping lint/build steps | Includes all available steps automatically |

---

## Benefits

- **Zero config** — infers everything from your project files
- **Platform-aware** — detects GitHub Actions vs GitLab CI automatically
- **Multi-language support** — Node.js, Python, Go, Java, Rust, Ruby
- **Dependency caching** — faster pipeline runs out of the box
- **Consistent output** — follows the same best-practice sequence every time

---

## How It Works

The agent runs 3 skills in sequence:

```
analyze_project → detect_ci_platform → generate_ci_pipeline
```

| Skill | What it does |
|---|---|
| `analyze_project` | Detects language, framework, and port in a single pass |
| `detect_ci_platform` | Detects GitHub vs GitLab and extracts test/build/lint commands |
| `generate_ci_pipeline` | Writes the pipeline file with caching and all steps |

---

## Installation

**1. Clone the repo**
```bash
git clone https://github.com/ramesherrorhunter/kiro-ci-agent.git
```

**2. Copy the agent into your project**
```bash
cp -r kiro-ci-agent/.kiro /path/to/your/project/
```

Or copy into the current directory:
```bash
cp -r kiro-ci-agent/.kiro .
```

That's it — the agent and all skills are now available in your project.

---

## SOP — Standard Operating Procedure

### Prerequisites
- Kiro CLI installed
- Project directory accessible

### Steps

**1. Navigate to your project**
```bash
cd /path/to/your/project
```

**2. Start Kiro CLI**
```bash
kiro-cli
```

**3. Select the agent**

Type `/agent` and from the dropdown select `ci-agent`

**4. Review generated file**
```
.github/workflows/ci.yml    ← for GitHub
.gitlab-ci.yml              ← for GitLab
```

### Expected Outputs

| Platform | File | Stages |
|---|---|---|
| GitHub Actions | `.github/workflows/ci.yml` | install → lint → test → build |
| GitLab CI | `.gitlab-ci.yml` | install → lint → test → build |

### Supported Languages

| Indicator File | Detected Language |
|---|---|
| `package.json` | Node.js |
| `requirements.txt` / `pyproject.toml` | Python |
| `go.mod` | Go |
| `pom.xml` / `build.gradle` | Java |
| `Cargo.toml` | Rust |
| `Gemfile` | Ruby |

### Notes
- Lint and build stages are skipped if no corresponding command is detected
- Default platform is GitHub Actions if remote URL cannot be determined
- Re-run the agent after adding new scripts or switching CI platforms

## License

MIT
