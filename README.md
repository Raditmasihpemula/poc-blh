# OPPO Video h5_detail JSBridge PoC

Harmless proof-of-concept pages for authorized HackerOne testing.

## Files

```text
index.html    # Payload PoC loaded inside OPPO Video WebView
landing.html  # Normal HTTPS launcher page to send/open first
```

## Deploy to GitHub Pages

1. Upload both `index.html` and `landing.html` to the repo root.
2. Enable GitHub Pages: Settings → Pages → Deploy from branch → `main` / root.
3. Open the launcher URL:

```text
https://raditmasihpemula.github.io/poc-blh/landing.html
```

4. Tap **Open in OPPO Video**.
5. OPPO Video should open and load `index.html` inside its WebView.
6. Tap **Run harmless PoC tests** on the payload page.

## Expected evidence

Inside OPPO Video WebView:

- `window.appJsBridge` exists.
- `setValueFromMMKV` returns `code:0`.
- `getValueFromMMKV` returns the PoC value.
- `copyText` returns `code:0`.
- Sensitive APIs such as `getOpenId` and `getGaid` return `404 no such method` in the tested context.

## Manual ADB equivalent

```bash
adb shell am start -W -a android.intent.action.VIEW -d 'heyvideo://global/h5_detail?url=https%3A%2F%2Fraditmasihpemula.github.io%2Fpoc-blh%2F%3FnotDarkMode%3Dtrue' com.coloros.video
```

The PoC does not exfiltrate data or contact third-party servers.
