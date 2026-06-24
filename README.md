# Property Mini-Listings 🏡

A modern, responsive Vue 3 single-page application that allows users to search, filter, sort, and bookmark rental properties in Cape Town. Built explicitly using the **Options API** (`data`, `computed`, `methods`, `props`), this project demonstrates high-fidelity component structure, clean state management, and strict adherence to responsive design parameters.

---

##  Live Demo & Repository
- **GitHub Repository**: [https://github.com](https://github.com)

---

##  Features Implemented

### Core Deliverables
* **Component-Based Architecture**: Modular design consisting of `AppHeader.vue`, `PropertyCard.vue`, and a centralized state controller in `App.vue`.
* **Dynamic Property Counter**: The header component automatically receives and displays the real-time count of currently visible properties via `props`.
* **Robust Filtering & Search Engine**: A text input binds reactively to filter the property listings down instantly by matching characters in either the **title** or **location** (case-insensitive).
* **Ascending & Descending Price Sorting**: Users can actively sort filtered results by price point seamlessly via a native select dropdown element.
* **Conditional Visibility & Visual Indicators**: Custom styled badges explicitly alert users to listing operational availability (`Available` vs `Not Available`) using structural `v-if` directives.
* **Interactive Bookmarking Ecosystem**: Clicking the custom action star on any given property triggers custom component events (`$emit`), passing unique identifying IDs up to the main array registry.

### Extra Stretch Goals Met 
* **Persistent Local Browser Memory**: Bookmarked listings are instantly cached into browser `localStorage`. Refreshing or closing the tab preserves user selections automatically.

---

##  Architecture & Tech Stack
- **Framework**: Vue 3 (Options API paradigm)
- **Tooling**: Vite (Hot Module Replacement development server)
- **Styling**: Pure scoped CSS3 variables, Flexbox layouts, CSS Grid grids, and responsive Media Queries.

### Data Structure Schema
Each item in the curated listing database conforms to the following schema definition:
```typescript
interface Property {
  id: number;
  title: string;
  location: string;
  price: number;
  type: string;
  available: boolean;
  image: string;
}
```

---

##  Local Installation & Setup

Follow these steps to run the application locally on your machine:

1. **Clone the Repository**
   ```bash
   git clone https://github.com.git
   cd property-mini-listings
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Run the Development Server**
   ```bash
   npm run dev
   ```
   Open your browser and navigate to the local link outputted in your terminal (typically `http://localhost:5173`).

4. **Build for Production**
   ```bash
   npm run build
   ```

---

##  Project Directory Structure

```text
property-mini-listings/
├── src/
│   ├── components/
│   │   ├── AppHeader.vue      # Top header branding & property counting component
│   │   └── PropertyCard.vue   # Individual listing component using props & custom events
│   ├── App.vue                # Core application entrypoint, state management, & filtering computation
│   ├── main.js                # Application bootstrapper file
│   └── mockData.js            # Mock dataset containing diverse property listings
├── public/                    # Static assets folder
├── index.html                 # Main markup layout index
├── package.json               # Manifest dependencies configurations file
└── README.md                  # Project documentation overview
```

---

##  Design Philosophy & Choices
- **Separation of Concerns**: State is stored high up in `App.vue` to ensure data consistently flows downward, while child components remain stateless ("dumb components") and dispatch changes back upward through explicit events.
- **Performant UI Updates**: Search logic and sorting mechanics are processed entirely within a `computed` property structure. This optimizes execution speed, preventing unnecessary re-rendering arrays.
- **CSS Architecture**: Scoped stylesheets are bundled inside each independent component interface, isolating layout overrides and safely eliminating global cascade leaks.
