# The Room Between / 房间之外

A peaceful room puzzle in which three everyday objects become a personal story. Built during Firebase #BuildHybridAI 2026 with JavaScript, SVG, a deterministic puzzle engine and Firebase AI Logic.

## What works

- Explore a moonlit study, redirect light with a mirror, open a coded drawer, and find the garden.
- Supply three object names; Firebase generates constrained JSON containing a personal introduction, object descriptions and an ending.
- The game engine owns inventory, prerequisites and solutions. Model output cannot unlock the door or change the puzzle graph.
- English and Chinese UI, keyboard-accessible controls, hints, local progress persistence and a service worker for offline replay after initial loading.
- Every AI inference call goes through Firebase AI Logic. No direct Gemini or Chrome Prompt API calls.

## Verified status — November 12, 2026

App Check verification and actual Firebase AI Logic cloud generation succeeded in local development using a private, project-scoped debug token. The returned SDK inference source was `in_cloud`. The full game was then completed with generated narrative content. Unit tests verify gating, wrong answers, reset of an incorrect direction sequence, completion and save recovery.

The test browser did **not** expose on-device AI: `ONLY_ON_DEVICE` returned `api-not-enabled`. On-device execution is implemented through the SDK but is not claimed as tested on this machine. `PREFER_ON_DEVICE` successfully used the cloud fallback. Supported desktop Chrome with an available model is required to test the local inference route.

This repository contains no project configuration, API credentials or App Check debug token. The hosted personal preview is private; use the source instructions below for judging. A production App Check provider has not been provisioned for a public hosted AI endpoint.

## Run and test

Requires Node.js 20+ and Python 3 (or another static web server).

```sh
npm ci
npm run build
npm test
python3 -m http.server 8080 --directory dist
```

Open `http://localhost:8080/`. The handcrafted chapter is playable immediately and needs no account. Use the EN button for the English UI.

For actual AI generation, follow [TESTING.md](TESTING.md). Reviewers must use an authorized Firebase project of their own; no production credentials are published or embedded in the submission.

## Firebase implementation

`src/firebase.js` initializes Firebase App Check and creates a model with `InferenceMode.PREFER_ON_DEVICE` when cloud fallback is selected, or `ONLY_ON_DEVICE` when local-only is selected. Both local and cloud paths use a matching schema for JSON output. `initializeDeviceModel()` runs on a user interaction; `generateContent()` creates the story. The actual SDK `inferenceSource` is shown in the UI. App Check debug credentials are accepted by the app only when served from localhost or 127.0.0.1, held in memory and never persisted.

Only the three entered labels and the story prompt are sent when cloud fallback is permitted. No room photographs, account records or saved game history are uploaded. Choosing local-only prevents cloud inference; an unavailable local model produces an error and preserves the previous game.

## Design decision

Generated stories should not create unsolvable games. A small authored puzzle graph controls mechanical progression while AI personalizes the narrative. This limits the current prototype to one chapter, but gives a complete beginning-to-ending experience and a stable foundation for additional puzzle graphs.

## Walkthrough (spoilers)

Turn on the lamp. Rotate the mirror to 90°. Inspect the book: 417. Open the drawer with 417. Follow the brass leaf: N, E, W.

## Tools and attribution

Built with AI coding assistance. The interface, illustration, game logic and Firebase adapter were created during the competition period. Dependencies are listed in package-lock.json. The artwork is SVG source rather than third-party imagery. Fonts are optional Google Fonts with system fallbacks; the game remains usable if fonts cannot load.

Official documentation used:
- https://firebase.google.com/docs/ai-logic/hybrid/web/get-started
- https://firebase.google.com/docs/ai-logic/hybrid/web/configuration-options
- https://firebase.google.com/docs/ai-logic/hybrid/web/generate-structured-output
- https://firebase.google.com/docs/app-check/web/recaptcha-enterprise-provider
- https://firebase.google.com/docs/app-check/web-debug-provider
