# Vizio TV Remote Key Test

Answers one question: **once a custom Cast app is running on the Vizio, does the TV's own remote control it?**

- `receiver.html` runs on the TV. It shows every button press it receives, in big text plus a log.
- `index.html` is the launcher. You open it once in Chrome to start the receiver, then put the device away.

## Setup (one time, ~20 min plus waiting)

### 1. Host the files on GitHub Pages
Cast apps must be served over HTTPS.

1. Create a new public GitHub repo, e.g. `tv-keytest`.
2. Upload `index.html` and `receiver.html` to the repo root.
3. Repo **Settings → Pages →** Source: *Deploy from a branch*, branch `main`, folder `/ (root)`. Save.
4. After a minute your URLs will be:
   - Launcher: `https://<your-username>.github.io/tv-keytest/`
   - Receiver: `https://<your-username>.github.io/tv-keytest/receiver.html`

### 2. Register as a Cast developer
1. Go to the Google Cast SDK Developer Console: https://cast.google.com/publish
2. Pay the one-time $5 registration fee.

### 3. Register the app
1. **Add New Application → Custom Receiver.**
2. Name: `TV Key Test`. Receiver Application URL: your `receiver.html` URL from step 1.
3. Save, then copy the 8-character **Application ID**.
4. Leave it unpublished.

### 4. Register the TV
Unpublished apps only run on devices you've registered.

1. In the console: **Add New Device.**
2. For the serial number: with the console open in Chrome on your PC, cast that tab to the Vizio (Chrome menu → Cast). The console can read the serial that way. If not, look in the TV's Settings → System → System Information, or its Cast settings.
3. Status will show "Registering." This takes anywhere from 15 minutes to an hour.
4. **When it says "Ready for Testing," fully restart the TV.** Unplug it for 30 seconds; the remote's power button only puts it to sleep.

## Run the test
1. Open the launcher URL in **Chrome** (Android phone or PC).
2. Paste the Application ID, then tap **Save & reload**.
3. Tap the cast icon and pick the Vizio.
4. When the TV shows "Receiver running on the TV," lock your phone or close the tab. **Don't tap "Stop casting,"** since that would close the app.
5. Press every button on the Vizio remote: arrows, OK, Back, Home, Menu, play/pause, volume, numbers, any app buttons.
6. Write down or photograph which buttons appear on screen.

## Reading the results

| What you see | What it means |
|---|---|
| Arrows and OK show up as keys (`ArrowUp`, `Enter`, …) | **Best case.** You can build a full TV-remote-driven interface that runs on the TV itself. Launch once from the phone, then browse with the remote. |
| Only play/pause shows up (as a key or "cast media command") | The remote is limited to media controls. Good for a passive display or slideshow, not for browsing. |
| Nothing shows up | The TV keeps the remote for itself. The cast route is display-only, and a streaming box is the way to get a remote-driven setup. |
| "Launcher gone — receiver still running on its own" | Confirms the app keeps running after the phone disconnects. |

Also check:
- **Back:** does it close the app, or show up as a key?
- **Home:** almost certainly exits to the Vizio home screen. That's expected.
- The **UA / Screen** line on the left shows the TV's browser engine and resolution. Send it over; it tells us how capable the TV's web runtime is.

## Troubleshooting
- **No cast icon in the launcher:** the phone and TV need to be on the same Wi-Fi. Make sure you're using Chrome; on a phone, try Chrome on your PC instead.
- **"Launch failed":** the device isn't registered yet, or the TV hasn't been fully restarted since it became "Ready for Testing."
- **Receiver shows a blank or default screen:** check that the receiver URL in the Cast console exactly matches your GitHub Pages URL, including `receiver.html`.
