# Contributing to Edge AI on Android 🚀

Thank you for your interest in contributing to **Edge AI on Android: Running Local Gemma 4 & Gemini Nano with LiteRT!**

This project explores the practical challenges of running generative AI directly on Android devices, combining CameraX, LiteRT-LM, locally deployed Gemma models, and real-time workshop presentation synchronization.

Whether you're an Android developer, an ML engineer, a student, or a member of the Google Developer Groups (GDG) community, your contributions can help make edge AI more accessible, efficient, and reproducible.

We welcome contributions of all sizes — from correcting a typo to improving inference performance on resource-constrained devices.

> **Our goal:** Build an inclusive, practical, and community-driven resource for learning, experimenting with, and improving on-device AI.

---

## 📋 Table of Contents

- [Code of Conduct](#-code-of-conduct)
- [Ways to Contribute](#-ways-to-contribute)
- [Getting Started](#-getting-started)
- [Development Guidelines](#-development-guidelines)
- [Android and Edge AI Guidelines](#-android-and-edge-ai-guidelines)
- [Performance Testing and Benchmarks](#-performance-testing-and-benchmarks)
- [Presentation and Slide Synchronization](#-presentation-and-slide-synchronization)
- [Commit Message Convention](#-commit-message-convention)
- [Submitting a Pull Request](#-submitting-a-pull-request)
- [Reporting Bugs and Requesting Features](#-reporting-bugs-and-requesting-features)
- [Security and Model Artifacts](#-security-and-model-artifacts)
- [Community Recognition](#-community-recognition)
- [License](#-license)

---

## 🤝 Code of Conduct

We are committed to providing a welcoming, respectful, and harassment-free environment for everyone, regardless of experience level, background, identity, or technical specialization.

All contributors are expected to:

- Be respectful and constructive in discussions and code reviews.
- Welcome questions from beginners and first-time contributors.
- Provide actionable feedback focused on the work rather than the individual.
- Accept reasonable criticism and differing technical opinions.
- Respect other contributors' time, contributions, and perspectives.
- Help maintain an inclusive environment for all GDG participants.

Harassment, discrimination, personal attacks, and deliberate disruption are not acceptable.

If you experience or witness inappropriate behavior, contact the repository maintainers through the communication channel listed in the repository profile.

---

## 💡 Ways to Contribute

You do not need to be an expert in machine learning to contribute!

### Android application

- Improve Kotlin code quality and application architecture.
- Improve CameraX lifecycle handling and image processing.
- Improve loading, error handling, and inference-state feedback.
- Investigate crashes, memory pressure, and UI responsiveness.
- Improve compatibility across Android devices and chipsets.

### Edge AI and model optimization

- Evaluate compatible Gemma model configurations.
- Investigate quantization, memory usage, and inference latency.
- Improve context-length and output-token management.
- Profile CPU inference and supported XNNPACK execution paths.
- Document model compatibility and runtime limitations.
- Add reproducible tests for local and offline inference.

### Web presentation

- Improve presentation accessibility and responsive layouts.
- Improve presenter controls and audience synchronization.
- Handle Supabase Realtime disconnections and reconnections.
- Improve slide-state recovery for late-joining attendees.
- Improve error messages and browser compatibility.

### Documentation and community

- Improve installation and troubleshooting instructions.
- Add architecture diagrams and technical explanations.
- Share reproducible benchmark results.
- Add beginner-friendly tutorials and workshop exercises.
- Review pull requests and help other contributors get started.

Good first contributions include documentation corrections, reproducible bug reports, tests, and improvements to setup instructions.

---

## 🛠️ Getting Started

### 1. Check the project prerequisites

Before contributing code, review the main [README.md](README.md) and verify the requirements for the component you want to change.

| Component | Prerequisites |
|---|---|
| Android application | Android Studio, compatible JDK, Android SDK, and Gradle wrapper |
| Local AI inference | Compatible LiteRT-LM runtime and model artifact |
| Device testing | Physical Android device or an appropriate development environment |
| Web presentation | Node.js and the package manager specified by the presentation project |
| Slide synchronization | Supabase project configuration, if testing real-time features |
| Documentation | Markdown editor and Git |

Use the versions specified by the repository rather than upgrading build tools or runtime dependencies without checking compatibility.

### 2. Fork the repository

Fork this repository through GitHub, then clone your fork:

```bash
git clone https://github.com/<YOUR_GITHUB_USERNAME>/<YOUR_REPOSITORY>.git
cd <YOUR_REPOSITORY>
```

Replace the placeholders with your GitHub username and repository name.

Configure the upstream repository:

```bash
git remote add upstream https://github.com/<UPSTREAM_OWNER>/<UPSTREAM_REPOSITORY>.git
git remote -v
```

### 3. Create a feature branch

Start from the latest upstream branch used by the project:

```bash
git fetch upstream
git checkout main
git merge upstream/main
git checkout -b feat/your-feature-name
```

If the repository uses a different default branch, substitute its actual name.

Use a descriptive branch name:

```text
feat/improve-model-loading
fix/camera-resource-leak
docs/update-installation-guide
perf/tune-cpu-inference
test/add-offline-inference-check
```

### 4. Make your changes

Keep contributions focused and easy to review.

- Follow the existing project structure.
- Prefer small, maintainable changes over unrelated refactoring.
- Reuse existing abstractions where practical.
- Add tests for new behavior where feasible.
- Update documentation when setup, behavior, or requirements change.
- Avoid introducing dependencies without a clear technical reason.

### 5. Test your changes

Run the checks appropriate to your contribution.

For Android changes, use the project's Gradle wrapper:

```bash
cd android
./gradlew assembleDebug
./gradlew test
```

Run these commands from the directory containing the Gradle wrapper. If the project uses a different directory layout, adjust the path accordingly.

For web presentation changes, install dependencies using the package manager and lockfile already present in the project. Then run the scripts defined in `package.json`, for example:

```bash
npm ci
npm run build
```

These web commands apply only if the presentation uses npm and defines the corresponding scripts.

Before opening a pull request, review the changed files:

```bash
git status
git diff --check
git diff
```

---

## 🧑‍💻 Development Guidelines

### Kotlin and Android

- Follow established Kotlin conventions and the project's existing architecture.
- Use clear names for classes, functions, and variables.
- Keep expensive inference and image-processing operations off the main thread.
- Handle exceptions and model-loading failures explicitly.
- Respect Android lifecycle boundaries.
- Release camera frames, model sessions, and other resources when appropriate.
- Request only the Android permissions the feature actually needs.
- Avoid logging sensitive prompts, images, or other user data.
- Keep UI state consistent during model loading, inference, and cancellation.

### Web development

- Follow the project's existing formatting, linting, and component conventions.
- Keep slide content separate from synchronization logic where practical.
- Handle network failures and reconnects gracefully.
- Validate incoming broadcast events before updating application state.
- Ensure the presentation remains usable on mobile screens.
- Do not expose privileged Supabase credentials in client-side code.

### Documentation

- Use clear headings and concise paragraphs.
- Include runnable commands when appropriate.
- Explain prerequisites before presenting setup instructions.
- Use tables for compact reference information.
- Include Mermaid diagrams when they clarify architecture or data flow.
- Identify assumptions and device-specific limitations explicitly.
- Avoid claiming that an untested configuration is supported.

---

## 📱 Android and Edge AI Guidelines

Contributions that affect local inference require special care because performance and compatibility vary across devices.

### CameraX integration

When changing camera behavior:

- Respect the camera lifecycle.
- Close each `ImageProxy` when processing is complete.
- Avoid accumulating frames when inference is slower than camera capture.
- Keep expensive image conversion off the main thread.
- Avoid launching overlapping inference requests unintentionally.
- Test camera permission denial and recovery.
- Verify that camera resources are released when the relevant screen is closed.

### LiteRT-LM and Gemma

When changing model-loading or inference code:

- Verify compatibility with the model format and selected runtime version.
- Document any required tokenizer, metadata, or auxiliary files.
- Handle model initialization failures gracefully.
- Keep inference local unless a change explicitly introduces a network-based feature.
- Bound input size, context length, and generated output where supported.
- Close model sessions and runtime resources according to the runtime's API.
- Document device-specific limitations and unsupported configurations.

### Quantization

Quantization changes how model weights are represented and may affect memory use, accuracy, and execution speed.

When introducing or changing a quantized model:

1. Identify the exact model variant and source.
2. Record the quantization format and any relevant conversion details.
3. Verify that the runtime supports the artifact.
4. Compare output quality against an appropriate baseline.
5. Measure performance on the intended device.
6. Document any trade-offs or compatibility limitations.

Do not assume that every INT4 model is compatible with every LiteRT-LM release or that lower-bit quantization automatically improves inference speed.

### Offline-first behavior

When changing the Android inference pipeline, verify whether the feature still works without a network connection.

Distinguish between:

- **Local inference:** Model execution occurs on the Android device.
- **Offline readiness:** All resources required for the tested workflow are already available locally.
- **Networked functionality:** A feature depends on remote services, downloads, or live synchronization.

The hosted presentation and Supabase Realtime features may require connectivity even when the Android model executes entirely locally.

---

## 📊 Performance Testing and Benchmarks

Performance claims should be measurable, reproducible, and tied to a specific configuration.

For contributions that affect inference performance, include the following details whenever possible:

| Field | What to report |
|---|---|
| Device | Manufacturer and exact model |
| Chipset | SoC and relevant hardware details |
| Android version | OS version and API level where relevant |
| Runtime | LiteRT-LM version and execution backend |
| Model | Exact model variant and quantization format |
| Input | Prompt length and image-processing configuration, if applicable |
| Output | Maximum generated token count |
| Model load time | Time required to initialize the model |
| Time to first token | Delay before generation begins producing output |
| Generation speed | Measured tokens per second |
| Memory | Observed application memory usage and measurement method |
| Test conditions | Repetitions, device temperature, and relevant background activity |

### Recommended testing approach

1. Use the same model artifact and input for each comparison.
2. Separate model initialization from inference measurements.
3. Measure prompt processing and token generation separately where possible.
4. Repeat tests rather than relying on a single result.
5. Account for thermal throttling and background activity.
6. Record the exact configuration used.
7. Document any regression alongside the proposed optimization.

For the workshop's reference device, the Redmi Pad 2 with MediaTek Helio G100-Ultra provides a useful baseline. Results from other devices are welcome and should be identified separately.

**Please distinguish measured results from estimates.** Do not present theoretical quantization savings as measured RAM reductions or describe a device as supported solely because the application compiles.

---

## 🌐 Presentation and Slide Synchronization

The web-based presentation uses Supabase Realtime Broadcast to synchronize slide changes between the presenter and audience devices.

Contributions to this subsystem should consider:

- Correct slide-state propagation.
- Late-joining audience members.
- Temporary network disconnections.
- Reconnection and recovery behavior.
- Duplicate or out-of-order events.
- Input validation and session boundaries.
- Mobile browser usability and accessibility.

### Supabase security requirements

- Never commit a Supabase service-role key or other privileged credentials.
- Use environment variables or the project's established configuration mechanism.
- Treat browser-visible configuration as public.
- Apply appropriate access controls and authorization rules.
- Validate event payloads before applying them.
- Avoid placing sensitive attendee data in broadcast messages.

When reporting synchronization issues, include the relevant browser, reproduction steps, expected behavior, and actual behavior. Never include access tokens or private credentials.

---

## 📝 Commit Message Convention

Use descriptive commit messages that make changes easy to understand during reviews and when examining project history.

We recommend a lightweight Conventional Commits format:

```text
<type>(optional-scope): <description>
```

### Common types

| Type | Purpose | Example |
|---|---|---|
| `feat` | New functionality | `feat(android): add model loading feedback` |
| `fix` | Bug fix | `fix(camera): release frames after analysis` |
| `perf` | Performance improvement | `perf(inference): reduce redundant preprocessing` |
| `docs` | Documentation change | `docs(readme): clarify model setup` |
| `test` | Test additions or changes | `test(android): cover model initialization errors` |
| `refactor` | Code restructuring without intended behavior changes | `refactor(android): simplify inference state handling` |
| `build` | Build and dependency configuration | `build(android): align runtime dependencies` |
| `chore` | Maintenance tasks | `chore(repo): update development instructions` |

Keep messages concise and specific. Explain the motivation in the commit body when the change requires additional context.

---

## 🔍 Submitting a Pull Request

Before opening a pull request:

- [ ] The change has a clear purpose.
- [ ] The branch contains only relevant changes.
- [ ] Code follows the project's conventions.
- [ ] Relevant builds and tests have been run.
- [ ] Device-specific behavior has been checked when applicable.
- [ ] Documentation has been updated.
- [ ] No secrets, credentials, or unintended model binaries are included.
- [ ] Performance claims include supporting measurements where applicable.
- [ ] Known limitations are documented.

### Pull request workflow

1. Push your feature branch to your fork.
2. Open a pull request against the upstream repository's default branch.
3. Describe the problem and why the change is useful.
4. Explain your implementation and any important trade-offs.
5. Include test results, screenshots, logs, or benchmark measurements where relevant.
6. Respond constructively to review feedback.
7. Update the pull request until the agreed requirements are satisfied.

### Suggested pull request template

**Summary**

Describe what changed and why.

**Related issue**

Link the relevant issue or discussion, if applicable.

**Implementation**

Explain the main technical decisions.

**Testing**

List the commands, test cases, and devices used.

**Performance impact**

Describe measured changes, if relevant.

**Limitations**

Document known issues, compatibility constraints, or follow-up work.

**Checklist**

- [ ] Tests or builds completed where applicable.
- [ ] Documentation updated.
- [ ] No secrets or restricted artifacts committed.

---

## 🐛 Reporting Bugs and Requesting Features

Before creating an issue, check whether a similar report already exists.

### Bug reports

A useful bug report includes:

- A concise, descriptive title.
- Steps to reproduce the problem.
- Expected behavior.
- Actual behavior.
- Android version and device model, if relevant.
- Runtime and model configuration, if relevant.
- Relevant logs with sensitive information removed.
- Whether the problem occurs offline, online, or in both conditions.

For model-loading and inference failures, include the exact model variant and runtime version when known.

### Feature requests

Please explain:

1. The problem or user need.
2. The proposed improvement.
3. Who would benefit from it.
4. Any compatibility or performance implications.
5. How success could be tested.

Feature proposals involving new models, backends, or external services should include a brief explanation of the added dependencies and operational trade-offs.

---

## 🔒 Security and Model Artifacts

Security issues should not be disclosed publicly before maintainers have had a reasonable opportunity to investigate them.

For sensitive vulnerabilities, contact the repository maintainer through the private reporting mechanism listed in the repository's GitHub security settings, if available.

### Model and dataset responsibilities

Before contributing model files, datasets, or other third-party assets:

- Confirm the license and redistribution permissions.
- Document the original source.
- Include relevant attribution and usage restrictions.
- Verify that the repository is permitted to host the artifact.
- Avoid committing large generated files without maintainer approval.
- Prefer documented download and verification instructions when hosting binaries is unnecessary.

Do not assume that the repository's software license automatically covers model weights, datasets, or third-party assets.

### Protect user data

Never commit:

- API keys or access tokens.
- Supabase service-role credentials.
- Private configuration files.
- Personal camera images or private prompts collected during testing.
- Logs containing sensitive information.
- Model artifacts that cannot legally be redistributed.

If a secret is accidentally committed, removing it from the latest commit may not remove it from Git history. Revoke or rotate the credential immediately and follow the repository's incident-response process.

---

## 🌍 Community Recognition

This project is intended to grow through collaboration, shared experimentation, and practical learning within the GDG ecosystem.

We value contributions from:

- First-time open-source contributors.
- Android developers.
- Machine learning and edge AI engineers.
- Technical writers and documentation contributors.
- Students and workshop attendees.
- Developers testing on underrepresented devices and chipsets.

Contributors should receive appropriate credit for their work. If your contribution introduces a useful benchmark, tutorial, or device-specific finding, include enough context for others to reproduce and build upon it.

**You do not need to submit a major feature to make a meaningful contribution.** A clear bug report, a verified setup correction, or a well-documented performance observation can help the entire community.

---

## 📄 License

By contributing to this repository, you agree that your contributions will be distributed under the license governing the project, subject to its terms.

Review the root-level [`LICENSE`](LICENSE) file before submitting a contribution. If the repository does not yet contain a license, contact the maintainers before contributing substantial code.

Third-party libraries, model weights, datasets, and other assets may have separate license terms.

---

## 🙌 Thank You!

Thank you for helping make on-device AI more practical, accessible, and understandable.

Every useful issue, code improvement, benchmark, and documentation contribution helps the next developer learn faster and build better.

**Build locally. Learn openly. Contribute together. 🚀**

If you're joining through a Google Developer Groups workshop, welcome to the community — we look forward to seeing what you build!
