# Local Music Player (PWA)

A Spotify-style local music web app that runs entirely in your browser. Upload MP3s, extract metadata and album art, organize playlists, and enjoy offline playback with a modern, responsive UI.

**Live Demo:** Deploy to Vercel for instant access

## Features

- **Upload & Import**: Drag-and-drop MP3 files; extracts ID3 tags (title, artist, album, year, genre) and embedded artwork
- **Local-First Storage**: All data stored in IndexedDB via Dexie (tracks, audio blobs, artwork, playlists, settings)
- **Library Management**: Search, filter, and sort your music collection
- **Playlists**: Create, rename, delete playlists; add/remove/reorder tracks with drag-and-drop
- **Media Player**: Persistent player bar + full Now Playing view with scrubbing, shuffle, repeat
- **Queue System**: Collapsible queue drawer with enqueue, Play Next, reorder, and clear functionality
- **PWA Support**: Installable on desktop/mobile, works offline with cached app shell
- **Media Session API**: Lock screen and hardware media key integration
- **Data Backup**: Export/import library metadata as JSON
- **Accessibility**: Keyboard navigable, focus rings, ARIA labels, reduced motion support

## Tech Stack

- React 18 + Vite + TypeScript
- Tailwind CSS
- Dexie (IndexedDB wrapper)
- React Router
- music-metadata-browser (ID3 parsing)
- Media Session API

## Getting Started

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

## Deploy to Vercel

1. Push this repo to GitHub
2. Import in Vercel dashboard
3. Build command: `npm run build`
4. Output directory: `dist`
5. No additional configuration needed - `vercel.json` handles SPA routing

## Data Model

```
Track {
  id, title, artist, album, duration, year?, genre?
  artworkBlobId?, audioBlobId, createdAt, updatedAt
}

BlobDoc {
  id, type ('audio'|'artwork'), blob, createdAt
}

Playlist {
  id, name, trackIds[], createdAt, updatedAt
}

AppSettings {
  id='settings', theme, shuffle, repeat
  lastQueue[], lastIndex, lastPosition
}
```

## PWA & Offline

- Install via browser "Add to Home Screen" or "Install App"
- First load must be online to cache assets
- Imported music persists in IndexedDB for offline playback
- Service worker provides offline fallback page

## Development Tips

- Visit `/upload?seed=1` in development to auto-generate demo tracks
- Replace SVG icons in `public/icons/` with PNG 192x192 and 512x512 for better cross-platform support

## License

MIT
