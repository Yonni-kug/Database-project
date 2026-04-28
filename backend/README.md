[README.md](https://github.com/user-attachments/files/27148576/README.md)
# Music Trends — Node.js Backend

## Requirements
- Node.js (v18 or higher) — https://nodejs.org
- MySQL database already set up with the project schema

## Setup

### 1. Install dependencies
Open a terminal in this folder and run:
```
npm install
```

### 2. Configure your database
Open the `.env` file and fill in your team's details:
```
DB_HOST=localhost
DB_PORT=3306
DB_NAME=your_database_name
DB_USER=your_username
DB_PASSWORD=your_password
```

### 3. Start the server
```
npm start
```
The server runs at http://localhost:8080

For development with auto-restart on file changes:
```
npm run dev
```

---

## API Endpoints

| Method | URL | Description |
|--------|-----|-------------|
| GET | /api/trending | Top trending songs globally |
| GET | /api/trending?region_id=1 | Trending in a specific region |
| GET | /api/search?q=espresso | Search by title, artist, or genre |
| GET | /api/map | Data for the world map |
| GET | /api/regions | All regions |
| GET | /api/songs/:id/detail | Trend details for one song |
| GET | /api/stats | Counts for the stats strip |
| POST | /api/survey | Save a survey response |

---

## Connecting to the Frontend

Once the server is running, open `index.html` and find the `initDB()` function.
Replace the sql.js calls with fetch calls to the API.

### Example
Find `loadTrendingGlobal()` and change it to:
```javascript
function loadTrendingGlobal() {
  fetch('http://localhost:8080/api/trending')
    .then(function(res) { return res.json(); })
    .then(function(rows) { renderSongCards(rows, true); });
}
```

Do the same for `filterRegion`, `handleSearch`, `buildMapFromDB`, and `updateStats`.

---

## Notes
- `.env` is already in `.gitignore` so your password won't be pushed to GitHub
- Make sure MySQL is running before starting the server
- The MUSIC table needs `title` and `artist` columns added before songs will show
