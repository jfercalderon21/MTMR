# Apple Silicon and universal builds

> **Status: draft / verification pending.** This fork currently inherits the upstream Xcode project. The locally modified source and its exact build settings have not yet been imported from the author's Mac. The commands below are a diagnostic workflow, **not** a claim that the upstream project currently builds without errors on a specific Xcode/macOS version.

## Goal

Build MTMR for Apple Silicon (`arm64`), and, if both slices are supported by the project and dependencies, produce a universal macOS app containing `arm64` and `x86_64`.

## Known local work (not yet reproduced from this repository)

An earlier local MTMR development session included:

- An Apple Silicon-native build.
- A universal build reported to contain `arm64` and `x86_64`.
- An ad hoc signing adjustment and a subsequent check of Accessibility permissions.
- Performance sampling. The measurements **do not** establish a proven CPU optimization.

The exact source revision, Xcode settings, dependencies, build logs, and signing details must still be checked against the preserved Mac source tree.

## 1. Inspect the source and toolchain

On the Mac that holds the modified source, record the following **without changing the installed app**:

```sh
xcodebuild -version
xcrun --sdk macosx --show-sdk-version
uname -m
git status --short
git remote -v
git log -1 --format='%h %s'
xcodebuild -list -project MTMR.xcodeproj
```

Run these from the project root. Do not assume the local folder contains a Git repository; if `git` reports that it does not, record that result and continue with the Xcode checks.

## 2. Inspect build architecture settings

```sh
xcodebuild -showBuildSettings -project MTMR.xcodeproj -scheme MTMR -configuration Release | grep -E '(^| )(ARCHS|ONLY_ACTIVE_ARCH|SDKROOT|MACOSX_DEPLOYMENT_TARGET|CODE_SIGN_STYLE|CODE_SIGN_IDENTITY|SUPPORTED_PLATFORMS) ='
```

The scheme name `MTMR` must be confirmed by step 1. These settings alone do not prove that a successful universal build is possible.

## 3. Build and verify (after checking source and dependencies)

Use a separate DerivedData directory to avoid interfering with existing build products. A candidate Apple Silicon build command is:

```sh
xcodebuild -project MTMR.xcodeproj -scheme MTMR -configuration Release -destination 'generic/platform=macOS' -derivedDataPath /tmp/MTMR-fork-verify ARCHS=arm64 ONLY_ACTIVE_ARCH=NO build
```

If the build succeeds, inspect the binary in the produced `MTMR.app` using `file` and `lipo -archs`. Resolve its actual location from the build output rather than guessing it. To attempt a universal build, first review `ARCHS`, architectures supported by every dependency, and any project-specific settings; then run a separate build with `ARCHS='arm64 x86_64'` and `ONLY_ACTIVE_ARCH=NO`. **Neither build has yet been executed for the published fork.**

## 4. Signing and Accessibility

- Inspect the app's existing signature with `codesign -dv --verbose=4 /path/to/MTMR.app` (replace the path with the verified build result).
- Ad hoc signing (`codesign --force --deep --sign -`) was used locally in prior work. This is a **local testing technique**, not Developer ID notarization or a distribution trust guarantee. Do not apply it blindly to the running installation.
- macOS may require a renewed Accessibility authorization after replacing or re-signing an app. Check System Settings > Privacy & Security > Accessibility if controls do not function.
- Do not publish a binary release until architecture, signing, launch behavior, and configuration behavior have been verified on the target system.

## 5. Acceptance checklist

- [ ] Identify the local source revision and record `git diff` or an equivalent source comparison.
- [ ] Verify Xcode version, target scheme, deployment target, and dependencies.
- [ ] Build an `arm64` app successfully.
- [ ] Confirm `arm64` with `lipo -archs`.
- [ ] Attempt a universal build and verify both slices, if supported.
- [ ] Verify app launch and Touch Bar actions.
- [ ] Verify the `autoclosegroup` feature described in [automatic group closing](automatic-group-closing.md).
- [ ] Inspect signing and Accessibility permission behavior.
- [ ] Document exact working build commands and outputs before publishing a release.

## Upstream credits

MTMR was created by the original [Toxblh/MTMR](https://github.com/Toxblh/MTMR) contributors. This fork retains the original MIT license. The workflow here describes a proposed verification process for the fork; it does not represent an official upstream build guide.
