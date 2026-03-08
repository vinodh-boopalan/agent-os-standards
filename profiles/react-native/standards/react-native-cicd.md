# React Native CI/CD Standards

## Build System
- Use EAS Build for all iOS and Android builds (cloud-based, no local Mac required for iOS)
- Configure build profiles in `eas.json`: development, preview, production
- Auto-increment `buildNumber` (iOS) and `versionCode` (Android) in CI

## EAS Build Profiles
- **development** — Development client with dev tools enabled
- **preview** — Internal distribution for QA testing (ad-hoc iOS, internal Android)
- **production** — Store-ready builds (App Store, Google Play)

## Over-the-Air Updates
- Use EAS Update for JavaScript-only changes (no native code changes)
- Configure update channels matching build profiles: development, preview, production
- Generate preview links on PRs for QA review before merge

## CI Pipeline (GitHub Actions)
- PR pipeline: lint → type-check → unit tests → EAS Update (preview)
- Main branch: lint → type-check → tests → EAS Build (production)
- Post preview build link as PR comment

## Code Signing
- Use EAS managed credentials for code signing (preferred)
- Store signing certificates and provisioning profiles in EAS, not in repo
- For custom credentials: encrypt and store securely, never commit to git

## Release Process
- Semantic versioning for app version
- Changelog auto-generated from conventional commits
- Submit to stores via EAS Submit
- Test on both iOS and Android before store submission
