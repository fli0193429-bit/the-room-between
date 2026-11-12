# Reviewer setup and testing

The handwritten game can be tested immediately after the build. To reproduce real model generation, use an authorized Firebase project. This avoids distributing live project credentials or a reusable debug credential.

1. Create/select a Firebase project on the free Spark plan. Register a web app and enable Firebase AI Logic with the Gemini Developer API. Leave paid billing disabled if testing only free-tier features.
2. Keep App Check enforcement enabled. For local development, go to App Check → Apps → your web app menu → Manage debug tokens, and register a private development token. Never commit it or put it in a video.
3. Build and serve the source on `http://localhost:8080/` as described in README.md. Open AI settings. Enter the Firebase public web configuration JSON and your local debug token into the private password field. For this localhost-only debug flow, the production reCAPTCHA site-key field can remain blank. Click Connect project. The app performs a real App Check token exchange before enabling generation.
4. Choose **Prefer device · allow object names in cloud** to test automatic fallback. Close settings. Choose Use my objects and enter three non-sensitive object names, then Generate with Firebase.
5. A successful model response replaces the chapter and reports the actual source. The tested cloud source is `in_cloud`. A failed request preserves the prior chapter; handwritten content is not labeled AI-generated.
6. To test local-only execution, use supported desktop Chrome with its on-device model available and choose **Device only**. Cloud Browser environments might return `api-not-enabled`; that is an availability failure, not successful local inference. See the official Firebase hybrid setup guide for current hardware/browser requirements.
7. Test the complete clue chain, then reload the page to check local progress persistence. After the first successful page load and service worker activation, disconnecting the network should still allow replay of the cached handwritten or previously generated chapter. Fresh generation requires a ready local model or a network connection for cloud fallback.
8. Revoke the development token after testing. Configuration and the entered token are in page memory only; refreshing clears them. Previously generated story text and puzzle progress stay in local browser storage until Start again is used.

## Expected game sequence

Lamp on → mirror 90° → book code 417 → drawer → N/E/W at the door → garden. A wrong drawer code does not advance progress. A wrong direction resets the direction sequence. Unlocking before prerequisites does not work.

## Test limitations

The submitted walkthrough was captured from actual working screens with cuts between interactions. Cloud generation, App Check and complete gameplay were verified. On-device generation was not verified on the test browser. The local debug credential used in the demonstration was kept private and revoked after capture. The optional hosted personal preview is not a public AI service.
