# Automatic group closing (proposed fork enhancement)

> Status: **Documentation draft — implementation not yet imported or verified in this fork.**
>
> This document describes a customization tested in a local MTMR build. The current GitHub fork may still contain only upstream code. Do not assume the feature is available until the source changes are imported and reviewed.

## Purpose

Provide an opt-in behavior to close an expanded Touch Bar group automatically after a user activates an item in that group, avoiding an additional manual step to return to the main bar.

## Intended configuration

The local customization used a Boolean setting named `autoclosegroup`:

```json
{
  "type": "group",
  "autoclosegroup": true,
  "items": [
    {
      "type": "staticButton",
      "title": "Example",
      "action": "appleScript",
      "actionAppleScript": {
        "inline": "display notification \"Example action\""
      }
    }
  ]
}
```

The JSON above illustrates the *intended interface*, not a configuration confirmed to work with the present upstream-derived code.

## Intended behavior

- The option is per group and opt-in.
- After a supported action is activated within an expanded group, the group closes and the main Touch Bar becomes visible.
- The group should not close merely because it was opened.
- The expected behavior with nested groups and actions that fail or are cancelled still needs verification.

## Local implementation notes to verify

Earlier local development work involved the following Swift files:

- `ItemsParsing.swift`
- `TouchBarController.swift`
- `GroupBarItem.swift`

These are **investigation pointers**, not a verified diff. Actual changed paths, defaults, event handling, and version compatibility must be established by comparing the Mac's source tree with upstream.

## Acceptance checklist

- [ ] Import the local source changes into a separate branch.
- [ ] Compare the branch against the original `Toxblh/MTMR` source.
- [ ] Confirm that `autoclosegroup: true` is parsed and respected.
- [ ] Confirm behavior for buttons and other supported actionable items.
- [ ] Confirm existing groups behave unchanged when the option is absent or false.
- [ ] Check nested groups and repeated interactions.
- [ ] Compile and test on the target macOS / Apple Silicon configuration.
- [ ] Record exact source commit, build steps, and observed test results.

## Attribution

This repository is a fork of [Toxblh/MTMR](https://github.com/Toxblh/MTMR). The original project's MIT license and copyright notice remain applicable. The documentation of this enhancement does not imply endorsement by the upstream maintainers.
