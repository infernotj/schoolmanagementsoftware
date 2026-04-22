# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands
- Build and run in development: `npm run dev` (starts Vite and Electron concurrently)
- Vite dev server only: `npm run dev:vite`
- Electron process only: `npm run dev:electron`
- Build for production: `npm run build` (Vite build + electron-builder)
- Rebuild native modules: `npm run rebuild`

## Architecture
The project is an Electron application using a React frontend and a local SQLite database.

### High-Level Structure
- `src/`: React frontend (Vite)
  - `pages/`: Main application views
  - `components/`: Reusable UI components
  - `hooks/`: Custom React hooks
  - `utils/`: Frontend utility functions
- `electron/`: Backend Electron processes
  - `main.js`: Entry point for Electron
  - `preload.js`: Bridge between main and renderer processes
  - `database/`: SQLite migration and connection logic (using `better-sqlite3`)
  - `controllers/`: Business logic and API handlers for the main process
  - `models/`: Data models and schema definitions

### Data Layer
- Database: SQLite (`better-sqlite3`)
- Schema: Managed via migrations in `electron/database/migrations/`
- Core Entities: `Company_Profile`, `Financial_Years`, `Classes_Master`, `Students`, `Payments`

### Key Features
- **PDF Generation**: Uses `@react-pdf/renderer` and `jspdf` for generating admission forms and ID cards.
- **Image Handling**: Photo capture via `react-webcam` and storage in local app data folders to keep the DB lightweight.
- **Dynamic Branding**: UI elements and PDF outputs are driven by the `Company_Profile` table.
