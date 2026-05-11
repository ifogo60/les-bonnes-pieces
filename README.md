 Web application for browsing, filtering, and reviewing automotive parts — powered by a local REST API.

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)
![JSON Server](https://img.shields.io/badge/JSON--Server-000000?style=for-the-badge&logo=json&logoColor=white)
![Chart.js](https://img.shields.io/badge/Chart.js-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)

---

## 📋 Table of Contents

- [About the project](#-about-the-project)
- [Demo](#-demo)
- [Features](#-features)
- [Project architecture](#-project-architecture)
- [Installation](#-installation)
- [Usage](#-usage)
- [File structure](#-file-structure)
- [Technical description](#-technical-description)
- [Known bugs & possible improvements](#-known-bugs--possible-improvements)
- [Author](#-author)

---

## 🎯 About the project

**Les Bonnes Pièces** is a dynamic web application for managing and browsing an automotive parts catalog. It fetches part data from a simulated REST API (`json-server`), stores it in `localStorage` for performance, and lets users filter, sort, and review parts — all without any page reload.

This project was built as part of the free OpenClassrooms course:
> 📚 [Créez un site dynamique avec JavaScript](https://openclassrooms.com/fr/courses/7697016-creez-un-site-dynamique-avec-javascript)

Technologies explored:
- ES6 modules (`import` / `export`)
- `fetch` API & async/await
- `localStorage` for client-side caching
- Dynamic DOM manipulation
- Chart.js for data visualization
- Faker.js for generating fake reviews

---

## 🖥️ Demo

```
┌─────────────────────────────────────────────────────┐
│  🔧  Les Bonnes Pièces                               │
├────────────────┬────────────────────────────────────┤
│   FILTERS      │  [Ampoule LED]   [Plaquettes frein] │
│                │   60€ €€€         40€ €€€            │
│ [Sort ↑ price] │   En stock        En stock           │
│ [Filter ≤35€]  │  [Voir les avis] [Voir les avis]    │
│ [With desc.]   │                                     │
│ [Sort ↓ price] │  [Liquide frein] [Balai essuie-glace│
│                │   9.60€ €          29.10€ €          │
│ Price max: 45€ │   En stock        En stock           │
│ ──────────────  │  [Voir les avis] [Voir les avis]    │
│ Add a review   │                                     │
│ [form...]      │  ★ Affordable parts: [list]         │
│                │  ✅ Available parts: [list]          │
│ [Bar chart]    │                                     │
└────────────────┴────────────────────────────────────┘
```

---

## ✨ Features

| Feature | Description |
|---|---|
| 📦 **Dynamic catalog** | Parts are fetched from a local REST API and displayed as cards |
| 💾 **localStorage caching** | Part data is cached to avoid unnecessary API calls on reload |
| 🔃 **Sort ascending** | Sort all parts by price from lowest to highest |
| 🔃 **Sort descending** | Sort all parts by price from highest to lowest |
| 💰 **Filter affordable parts** | Show only parts priced at €35 or less |
| 📝 **Filter by description** | Show only parts that have a description |
| 🎚️ **Price range slider** | Dynamically filter parts below a chosen max price |
| ⭐ **User reviews** | Click a part to fetch and display its reviews from the API |
| 📬 **Submit a review** | Submit a new review via a form (POST request to the API) |
| 📊 **Star rating chart** | Bar chart showing distribution of star ratings (Chart.js) |
| 📊 **Availability chart** | Bar chart showing comments by part availability |
| 🔄 **Refresh data** | Button to clear localStorage and reload fresh data from the API |

---

## 🗂️ Project architecture

```
les-bonnes-pieces/
│
├── index.html              # Main HTML structure
├── styles.css              # Stylesheet
│
├── pieces.js               # Main script: fetch, display, filter, sort
├── avis.js                 # Reviews module: display, submit, charts
│
├── generer-avis.js         # Script to generate fake reviews with Faker.js
│
├── db.json                 # json-server database (parts + reviews)
│
├── images/                 # Part images
│   ├── ampoule-led.png
│   ├── plaquettes-frein.png
│   ├── ampoule-boite-a-gants.png
│   ├── liquide-frein.png
│   └── balai-essuie-glace.png
│
└── node_modules/
    ├── chart.js/           # Chart.js library
    └── @faker-js/faker/    # Faker.js for generating fake data
```

---

## 🚀 Installation

### Prerequisites
- [Node.js](https://nodejs.org/) installed on your machine
- npm (comes with Node.js)

```bash
# 1. Clone the repository
git clone https://github.com/your-username/les-bonnes-pieces.git

# 2. Go to the project folder
cd les-bonnes-pieces

# 3. Install dependencies
npm install

# 4. Start the local API (json-server)
npx json-server --watch db.json --port 8081
```

Then open `index.html` in your browser (use **Live Server** on VS Code for best results).

> ⚠️ The app requires `json-server` to be running on port `8081`. Without it, the catalog will not load.

---

## 🕹️ Usage

1. **Browse the catalog**: parts are automatically fetched and displayed on load.
2. **Filter & sort**: use the buttons in the left panel to sort or filter the catalog.
3. **Adjust max price**: drag the slider to show only parts below a certain price.
4. **See reviews**: click the "Afficher les Avis" button on any part card.
5. **Submit a review**: fill in the review form (part ID, username, comment, stars) and click "Envoyer".
6. **Refresh data**: click "Mettre à jour les pièces" to clear the cache and fetch fresh data.
7. **Charts**: view star rating distribution and availability-based comment stats in the left panel.

---

## 📁 File structure

### `index.html`
The app shell. Contains:
- Header with logo and title
- Left panel: filter buttons, price slider, review form, charts
- Main content area: part cards, affordable parts list, available parts list
- Footer with author info and LinkedIn link

### `pieces.js`
The main script. Handles:
- Fetching parts from the API or reading from `localStorage`
- Dynamically building and inserting part cards into the DOM
- All filter, sort, and slider event listeners
- Building the "affordable" and "available" parts lists

### `avis.js`
ES6 module for reviews. Exports:
| Function | Role |
|---|---|
| `ajouListenersAvis()` | Attaches click listeners to "Afficher les Avis" buttons |
| `afficherAvis(pieceElement, avis)` | Renders review list inside a part card |
| `ajoutListenerEnvoyerAvis()` | Listens for form submit and POSTs a new review to the API |
| `afficherGraphiqueAvis()` | Fetches all reviews and renders two Chart.js bar charts |

### `generer-avis.js`
A standalone Node.js script that uses **Faker.js** to generate 20 fake reviews and output them as JSON. Run it once to populate `db.json`.

```bash
node generer-avis.js
```

### `db.json`
The `json-server` database. Contains two collections:
- `pieces`: the 5 automotive parts with name, price, category, image, description, and availability
- `avis`: user reviews with part ID, username, comment, and star rating

---

## 🔍 Technical description

### ES6 Modules
`avis.js` uses named exports and is imported at the top of `pieces.js`:
```javascript
import { ajouListenersAvis, ajoutListenerEnvoyerAvis, afficherAvis, afficherGraphiqueAvis } from "./avis.js";
```

### Fetch + async/await
All API calls use the modern `fetch` API with `async/await`:
```javascript
const reponse = await fetch("http://localhost:8081/pieces/");
const pieces = await reponse.json();
```

### localStorage caching
Parts are stored after the first fetch to avoid redundant requests:
```javascript
window.localStorage.setItem("pieces", JSON.stringify(pieces));
```

### Dynamic price display
Each part shows a visual price indicator based on its price:
```javascript
prixElement.innerText = `Prix : ${article.prix}€ (${article.prix < 35 ? "€" : "€€€"})`;
```

### Chart.js integration
Two horizontal bar charts are rendered in `<canvas>` elements:
- **Star chart**: distribution of 1–5 star ratings across all reviews
- **Availability chart**: number of reviews for available vs. unavailable parts

---

## 🐛 Known bugs & possible improvements

### Identified bugs

- **`localStorage.removeItem()` called with wrong argument**: the refresh button passes the `pieces` array object instead of the string key `"pieces"`:
```javascript
// ❌ Current (does nothing)
window.localStorage.removeItem(pieces)

// ✅ Fixed
window.localStorage.removeItem("pieces")
```

- **`localStorage` key mismatch for reviews**: parts are saved with key `avis-piece${id}` but retrieved with key `avis-piece-${id}` (missing dash), so cached reviews are never found.

- **Price element appended to `document.body`**: `prixElement` is incorrectly appended to `document.body` before being added to the card, causing duplicate price elements in the page.

- **Availability chart always shows 0**: the availability check uses `piece.disponibilite` on a single object instead of iterating over all pieces correctly.

### Suggested improvements

- [ ] Add a **search bar** to filter parts by name
- [ ] Display **star ratings visually** (★★★☆☆) in the review section
- [ ] Add **pagination** if the catalog grows beyond 10+ items
- [ ] Show a **loading spinner** while fetching data from the API
- [ ] Make the app **fully responsive** for mobile screens
- [ ] Add **error handling** when the API is unreachable (user-friendly message)

---

## 👤 Author

**Ifogo Malango Junior**


---

## 📄 License

This project is free to use for educational purposes.

---

*Project built as part of the free OpenClassrooms course — [Créez un site dynamique avec JavaScript](https://openclassrooms.com/fr/courses/7697016-creez-un-site-dynamique-avec-javascript).*
