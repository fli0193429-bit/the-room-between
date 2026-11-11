# The Room Between / 房间之外
Firebase #BuildHybridAI 2026 work in progress. A peaceful room puzzle with deterministic, solvable mechanics and optional Firebase-generated object narratives.

## Current status
Playable handcrafted prototype, NOT a completed contest submission. Firebase SDK integration builds but live model inference and App Check have not yet been tested with an authorized project. No project credentials included. AI setup is explicitly optional; handwritten content is never labeled AI output.

## Run
`npm install`, `npm run build`, serve `dist/` on localhost or HTTPS. `npm test` verifies progression, wrong answers, prerequisite gating and save recovery.

## Firebase setup
Create or select an authorized Firebase project on the free Spark plan, enable AI Logic with Gemini Developer API, register web app, configure production App Check reCAPTCHA v3 and allowed domain. Enter the public web configuration and public App Check site key in AI settings. Do not enter Gemini secret keys, service account credentials or App Check debug tokens. Config is held only in memory. Refresh to clear/reconfigure. Default inference is ONLY_ON_DEVICE; cloud fallback is a separate explicit user choice. Model download can take several minutes and requires a supported Chrome desktop/device. No software flags or billing are changed automatically.

All inference calls are through Firebase AI Logic. `src/firebase.js` initializes App Check, creates a hybrid model with constrained JSON output, initializes the on-device model on a user gesture, calls generateContent and displays the actual inferenceSource. Raw room photos are not collected. Only three user-selected object labels are passed to the model. The core puzzle remains deterministic and cached for offline play.

## Verification still required before submission
1. Finish Devpost registration; verify Google developer account answer.
2. Configure and test a real Firebase project, App Check, local inference and fallback independently.
3. Capture accurate 3-minute English demo with both verified inference modes; do not present handwritten demo as model output.
4. Publish a public source repository, provide test access, and finalize Devpost submission before Nov 30 2026 22:00 UTC.

## Walkthrough (spoilers)
Turn on lamp, rotate mirror to 90°, inspect book (417), open drawer with 417, follow brass leaf directions N E W to open garden.

## Sources
https://firebase.google.com/docs/ai-logic/hybrid/web/get-started
https://firebase.google.com/docs/ai-logic/hybrid/web/configuration-options
https://firebase.google.com/docs/ai-logic/hybrid/web/generate-structured-output
