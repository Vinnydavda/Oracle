# Oracle Agamemnon

Oracle Agamemnon is a macOS SwiftUI companion for local conversation, system status, schematics, and opt-in voice and visual experiments. This repository is a **development source snapshot** of the canonical Oracle workspace on November 11, 2026. It is ready to import into a GitHub repository; it is not a released or installed app update.

## Project status

| Item | Status at packaging |
| --- | --- |
| Source | Current canonical Swift sources and tests, including the November 11 presentation and speech-cue changes |
| Staged app | Earlier signed 0.9.6/build 21 candidate; the newer source changes have not been incorporated into it |
| Installed app | 0.8.3/build 13 on the owner's Mac |
| `Resources/Info.plist` | Preserved workspace metadata, 0.9.5/build 20; it is **not** a release version for this source snapshot |
| 3D avatar | Experimental asset included for source fidelity; it has failed the approved visual likeness gate |
| Voice | Local Qwen and speech paths are in development; live microphone transcription and speech-timed 3D performance are unverified |

The snapshot includes the latest available source, not an assertion that every feature has passed runtime acceptance. The approved visual reference and current experimental 3D asset are both present so that the source can be built and reviewed accurately.

## What is included

- `Sources/` — the macOS app and its local integration, conversation, voice, security, memory, and presentation code.
- `Resources/` — app icons, approved reference images, experimental 3D USDZ, and an audition audio sample used by the current source.
- `Tests/` — focused Swift test programs preserved from the canonical workspace.
- `scripts/build.sh` — a local build recipe. Its output stays in ignored `.build/`.

Development backups, runtime state, chat history, recordings, API credentials, generated build products, and rejected art studies are excluded.

## Requirements

- macOS with Apple's Swift compiler and command line developer tools.
- The system frameworks named in `scripts/build.sh`.
- Ollama with a locally available model for the optional local conversation path. No model weights are bundled.

Some dashboard integrations refer to other apps or handoff folders on the owner's Mac. They report unavailable when those local resources are absent. The Fish Audio path is optional and requires a separately configured Keychain credential and deliberate in-app action; no credential is included here.

## Build

From the repository root:

```sh
sh scripts/build.sh
```

The script creates `.build/Oracle Agamemnon.app` and does not install or launch it. `Resources/Info.plist` retains historical candidate metadata. Set reviewed version metadata and sign a release build separately before distributing an app.

## Verify the source

For a compiler check without launching the app:

```sh
swiftc -typecheck \
  -framework AppKit -framework SwiftUI -framework AVFoundation \
  -framework Speech -framework CoreImage -framework CoreVideo \
  -framework IOKit -framework Vision -framework Security \
  Sources/*.swift
```

The standalone test programs under `Tests/` are compiled with their matching source files. For example:

```sh
mkdir -p .build
swiftc Sources/OracleMotionEngine.swift Sources/OracleBehaviorContract.swift \
  Tests/OracleBehaviorContractTests.swift \
  -o .build/oracle-behavior-tests
.build/oracle-behavior-tests
```

## Data and permissions

Oracle stores its working state under `~/Documents/ORACLE/Agamemnon`. The app can request microphone, speech recognition, or camera access only through the relevant opt-in controls. Optional Fish Audio requests leave the Mac after the owner configures a Keychain credential and chooses the external voice action. Review those flows before enabling them.

The bundled reference art, 3D candidate, and audition audio are project assets. Keep the GitHub repository **private** unless the owner has reviewed publication rights for each asset and the code. No open-source license is granted by this snapshot.

## Current limitations

- The experimental 3D candidate does not match the approved Oracle character and lacks accepted facial, hand, hair, and speech-synchronized performance.
- Recent source changes have passed targeted local checks in the canonical workspace, but this snapshot has not been promoted to an installed release.
- Speech Recognition permission handling did not produce a live transcript in the last recorded Mac QA; microphone input remains unverified.
- The repository does not include a public distribution workflow or release signing identity.

This package preserves a reviewable starting point for continued development while keeping the distinction between source, staged candidate, and installed app explicit.
