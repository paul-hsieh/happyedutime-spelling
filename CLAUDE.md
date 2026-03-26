# Spelling Practice Web App

## Project Overview
A single-page spelling practice app for elementary school students. Hosted on GitHub Pages.

- **Repo**: github.com/paul-hsieh/happyedutime-spelling
- **Live URL**: https://paul-hsieh.github.io/happyedutime-spelling/
- **Structure**: Single file `index.html` (self-contained HTML/CSS/JS, no build step)

## How It Works
- Welcome screen with configurable word count (default 50)
- Randomly picks N words from a hardcoded list of ~500 English words
- Each word row shows: ordinal number, play buttons, hidden word
- "Reveal Spelling" button at bottom toggles word visibility
- When revealed, a wrong toggle (✗) appears next to each word — students mark words they got wrong
- Wrong words are persisted in localStorage (`spellingBee_wrongWords`) across sessions
- "New Set" picks previously-wrong words first (priority), fills remainder randomly, then shuffles all together

## Audio Sources
Two working pronunciation sources:
1. **Browser** - Web Speech API (`speechSynthesis`), synthetic voice, works offline
2. **Dictionary** - Human recordings from [dictionaryapi.dev](https://dictionaryapi.dev/) (CORS-enabled, free, sources from Wikimedia Commons)

Audio is pre-fetched on quiz start via `fetchAudio()` and cached in `audioCache`. The mp3 files are also pre-downloaded so they land in the browser's HTTP cache for instant playback and persistence across reloads.

### Sources That Don't Work (already tried, don't retry)
- **Google Translate TTS** - CORS blocks `new Audio()` playback; iframe approach also fails
- **Merriam-Webster direct audio URLs** - CORS blocked, URL pattern unreliable
- **Cambridge Dictionary audio** - CORS blocked, URL pattern unpredictable
- **Wikimedia Commons API** - Returns same audio files as dictionaryapi.dev (same source)
- **Puter.js** - Requires user authentication popup, unusable for this context

## Word List
- ~500 words embedded in `ALL_WORDS` array in the JS section
- Source: `spelling.txt` (original file, not in repo)
- Includes compound words ("real estate"), hyphenated ("stir-fry"), and semicolon variants ("froze; frozen")
- For pronunciation, word is cleaned: `word.split(';')[0].trim()`

## Design
- Kid-friendly: Baloo 2 Google Font, colorful gradients, bouncing mascot, bee theme
- Responsive single-column layout, max-width 800px
- Hidden words show "?" placeholder with gradient background

## Deployment
Push to `main` branch. GitHub Pages auto-deploys from root.
