# ReservaHub — Space Reservation System

## Description
A Single Page Application (SPA) for managing shared workspace reservations inside a company. Employees can book spaces, and administrators can manage all reservations and spaces.

## Technologies Used
- Vanilla JavaScript (ES Modules)
- HTML5 / CSS3
- json-server (mock REST API)
- localStorage (session persistence)
- Google Fonts (Syne + DM Sans)

## Installation

### Prerequisites
- [Node.js](https://nodejs.org/) v16 or higher
- npm (comes with Node.js)

### Steps

**1. Clone or download the project**
```bash
git clone <your-repo-url>
cd crud
```
Or simply extract the ZIP and open the folder.

**2. Install json-server globally**
```bash
npm install -g json-server
```

That's it — no other dependencies. The project uses pure Vanilla JS with no build step required.

## Running the Project

You need **two terminals** running at the same time:

**Terminal 1 — Start the API (json-server)**
```bash
cd /path/to/crud
json-server --watch db.json --port 3000
```
You should see:
```
Resources
  http://localhost:3000/users
  http://localhost:3000/spaces
  http://localhost:3000/reservations
```
Keep this terminal open — closing it will break the app.

**Terminal 2 — Serve the frontend**
```bash
cd /path/to/crud
npx serve . --listen 5500
```
Then open your browser at:
```
http://localhost:5500
```

> **Alternative:** If you use VS Code, right-click `index.html` → **Open with Live Server**.

## Running json-server
```bash
json-server --watch db.json --port 3000
```
The API will be available at `http://localhost:3000`.

## Test Users
| Role  | Email             | Password   |
|-------|-------------------|------------|
| admin | admin@test.com    | Admin123*  |
| user  | user@test.com     | User123*   |
| user  | maria@test.com    | User123*   |

## Project Structure
```
crud/
├── index.html
├── db.json
├── css/
│   └── styles.css
└── js/
    ├── app.js              # Entry point, route registration, navbar
    ├── modules/
    │   ├── api.js          # Fetch wrapper for all API calls
    │   ├── auth.js         # Session management (localStorage)
    │   ├── router.js       # Hash-based SPA router with route guards
    │   └── ui.js           # Shared helpers: toast, loader, modal, badges
    └── views/
        ├── login.js        # Login form and credential validation
        ├── dashboard.js    # Stats and recent reservations overview
        ├── reservations.js # CRUD for reservations (admin + user)
        └── spaces.js       # CRUD for spaces (admin only)
```

## Role Permissions
| Action                        | Admin | User         |
|-------------------------------|-------|--------------|
| View all reservations         | ✅    | ❌           |
| View own reservations         | ✅    | ✅           |
| Create reservation            | ✅    | ✅           |
| Edit any reservation          | ✅    | ❌           |
| Edit own pending reservation  | ✅    | ✅           |
| Approve / Reject reservation  | ✅    | ❌           |
| Cancel own reservation        | ✅    | ✅           |
| Delete reservation            | ✅    | ❌           |
| Manage spaces (CRUD)          | ✅    | ❌           |

## Technical Decisions
- **Hash-based routing** (`#dashboard`, `#admin-reservations`, etc.) — simple and works without a server.
- **Route guards** in `router.js` prevent users from navigating to admin-only routes via URL hash.
- **Duplicate check** before creating/editing a reservation: same space + date + overlapping time block.
- **Modular architecture**: each concern lives in its own file; views are stateful modules loaded on demand.
- **No frameworks** — demonstrates native DOM manipulation, fetch API, and ES module imports.

