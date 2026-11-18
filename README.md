# Keyboard Layout Switcher (Georgian / Armenian)

Single-page web app that converts Latin keystrokes into Georgian or Armenian characters in real time. Pure HTML/CSS/JS — no frameworks, no build step. Installable as a PWA.

## Features

- Live transliteration: type Latin → get Georgian or Armenian characters
- Two layouts (Georgian / Armenian) switchable via dropdown
- Toggle on/off to type plain Latin
- Copy to clipboard and clear field
- Layout and toggle state persist in `localStorage`, synced across tabs
- Mobile-friendly: full-width input, `beforeinput` handling for virtual keyboards
- Installable PWA with offline mode and auto-update

## Tech Stack

Vanilla HTML, CSS, JavaScript. Service worker + `manifest.json` for PWA. No dependencies.

Works as a single HTML page opened with a browser locally. Also works from a web server. HTTPS is required for PWA (except on localhost). 

### Icons
Manifest references icon-192.png and icon-512.png, both marked purpose: "any maskable". 

### Cache Management
Bump CACHE_VERSION in sw.js on each release. The activate handler deletes caches not matching the current version; skipWaiting() + clients.claim() activate the new version immediately. To reset during development: DevTools → Application → Unregister SW, clear Cache Storage and Local Storage.

### Project Structure
```text
/
├── index.html
├── manifest.json
├── sw.js
├── icon-192.png
└── icon-512.png
```

### How It Works
Each layout is a plain object mapping Latin keys to target characters ('a': 'ა' / 'a': 'ա').

Conversion hooks: keydown (desktop) and beforeinput (mobile virtual keyboards). Both skip Ctrl/Alt/Meta combos and IME composition.

Settings persist in localStorage under keyboard.layoutName and keyboard.layoutEnabled.

### Customization
To add a language: define a layout object, register it in LAYOUTS, add an `<option>` to the `<select>`.

### License
MIT

### AI
Designed by DeepSeek
