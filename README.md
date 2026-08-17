# Solace local build

## Quickest run
Open `frontend/solace.html` directly in a modern browser. This version includes a complete working local browser data layer, so all pages, auth, persistence, and interactions work without installing anything.

## Full local server foundation
Requires Node.js 26.x or Node.js 22+.

```bash
cd backend
npm install
node server.js
```
Then open http://localhost:3000. The backend includes SQLite schema, bcrypt password hashing, JWT auth, CORS, health check, user lookup, and scoped record endpoints. The current frontend remains the self-contained browser build so it is immediately runnable; use the API layer as the seam for wiring the full server persistence next.

## Signup fix
The signup form now navigates with an explicit hash route and calls the router after successful account creation, which fixes the button appearing to do nothing in direct-file and local-server runs.


## Node 26 compatibility

The backend now uses `better-sqlite3@^12.10.0`, which includes Node 26 prebuilt support, and declares the supported runtime range as Node >=22 and <27. After upgrading, delete the old install artifacts before reinstalling:

```powershell
Remove-Item -Recurse -Force node_modules -ErrorAction SilentlyContinue
Remove-Item -Force package-lock.json -ErrorAction SilentlyContinue
npm install
node server.js
```

Copy `.env.example` to `.env` and replace `SOLACE_JWT_SECRET` before using the backend beyond local development.
