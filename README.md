# Keyboard Layout Switcher (Georgian / Armenian)

I've been learning Georgian for some time now, and I've found that I need to type in Georgian on my desktop every now and then. Adding another keyboard layout didn't work for me, since switching between more than three languages on Windows, honestly, is a nightmare (alhough, on mobile platforms it works perfectly). So my next thought was using an online service - virtual keyboard to type in Georgian. Sadly, I never found one to suit me, for different reasons. So I kindly ask AI to help me with creating such service of my own. And here it is: an app that converts pressing Latin keys into Georgian letters. When your Georgian text is finished, you copy it and paste wherever you need.
- Works when keyboard is switched to Latin
- Uses standart "phonetic" layout: 't' for 'ტ', 'x' for 'ხ'. Sometimes you need to use SHIFT: 'z' for 'ზ', 'Z' for 'ძ'
- Is a HTML page with JavaScript, just open it with a browser and use
- Also an SPA version using Vue, this one you have to build first
- Can work from a web server and be installed as PWA and work offline 
Later I added Armenian layout too.


## Features
Single-page web app that converts Latin keystrokes into Georgian or Armenian characters in real time. Pure HTML/CSS/JS — no frameworks, no build step. Installable as a PWA.

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
