# Senpai's Choice

## Overview
Senpai's Choice is a React-based anime recommendation platform that uses moods to suggest anime genres. Users can filter anime recommendations based on their mood and explore curated lists of anime for each genre. The project integrates Tailwind CSS, DaisyUI, and the Jikan API for fetching anime data.

---

## Features
- **Mood-Based Filtering:** Select a mood to view corresponding anime genres.
- **Dynamic Anime Recommendations:** Fetches anime data dynamically based on selected genres and moods.
- **Pagination:** Navigate through anime lists with ease.
- **Genre-Based Filtering:** Choose genres for a more refined search.
- **Responsive Design:** Fully responsive layout built with Tailwind CSS and DaisyUI.

---

## Tech Stack
- **Frontend Framework:** React.js (with Vite for setup)
- **Styling:** Tailwind CSS, DaisyUI
- **API:** Jikan API for anime data
- **Package Management:** npm
- **State Management:** useState, useEffect hooks

---

## Setup and Installation

### 1. Initialize the Project with Vite
```bash
npm create vite@latest
```

### 2. Tailwind CSS Setup
Follow the official Tailwind CSS setup guide for Vite:
[Tailwind CSS with Vite](https://tailwindcss.com/docs/guides/vite)

### 3. Install DaisyUI
Install DaisyUI for UI components:
```bash
npm install daisyui
```
Customize DaisyUI themes by adding the following configuration in your `tailwind.config.js` file:
```javascript
module.exports = {
  daisyui: {
    themes: [
      {
        dracula: {
          ...require("daisyui/src/theming/themes")['dracula'],
          primary: "#de1614",
          secondary: "#FF6723",
        },
      },
    ],
  },
};
```

---

## Project Structure
```
├── src
│   ├── components
│   │   ├── Navbar.jsx
│   │   ├── MoodFilter.jsx
│   │   ├── AnimeList.jsx
│   │   ├── Footer.jsx
│   ├── assets
│   │   ├── mood.js
│   ├── App.jsx
│   ├── main.jsx
├── public
├── index.html
├── package.json
├── tailwind.config.js
```

---

## Key Components

### Navbar.jsx
Displays the navigation bar with the selected mood or a default title.
```jsx
const Navbar = ({ onBackClick, selectedMood }) => {
  return (
    <div className="navbar">
      <button onClick={onBackClick}>Back</button>
      <h1>{selectedMood ? `Mood: ${selectedMood}` : 'Anime App'}</h1>
    </div>
  );
};
```

### MoodFilter.jsx
Renders mood-based genre filters.
```jsx
const MoodFilter = ({ selectedGenres, toggleGenre }) => {
  const moods = [
    { moodName: 'Happy', genreName: 'Comedy' },
    { moodName: 'Adventurous', genreName: 'Adventure' },
    { moodName: 'Romantic', genreName: 'Romance' },
    { moodName: 'Highrated Anime this year', genreName: 'Highrated Anime this year' },
  ];

  return (
    <div className="mood-filter">
      {moods.map(({ moodName, genreName }) => (
        <button
          key={genreName}
          className={selectedGenres.includes(genreName) ? 'selected' : ''}
          onClick={() => toggleGenre(moodName, genreName)}
        >
          {moodName}
        </button>
      ))}
    </div>
  );
};
```

### AnimeContainer.jsx
Handles fetching genres and anime data, as well as managing state for the entire app.

---

## API Integration

### Jikan API
- **Fetch Genres:** `https://api.jikan.moe/v4/genres/anime`
- **Fetch Anime:** `https://api.jikan.moe/v4/anime`
  - Parameters include:
    - `order_by`: Popularity
    - `sort`: Ascending
    - `page`: Pagination
    - `limit`: Number of results per page
    - `genres`: Filter by selected genres
    - `min_score`: Minimum rating filter

### Example Genre Fetch
```javascript
useEffect(() => {
  axios.get('https://api.jikan.moe/v4/genres/anime')
    .then(response => setGenres(response.data.data))
    .catch(err => console.error('Failed to fetch genres:', err));
}, []);
```

---

## How to Use
1. Run the app locally:
```bash
npm install
npm run dev
```
2. Open your browser at the given URL (usually `http://localhost:5173`).
3. Select a mood to filter anime recommendations.
4. Navigate through the anime list using the pagination controls.

---

## Future Enhancements
- **User Authentication:** Allow users to save their preferences.
- **Advanced Search Filters:** Add additional filters like release year, rating, etc.
- **Favorite List:** Enable users to bookmark their favorite anime.
- **Dark Mode Toggle:** Implement a theme switcher.

---

## License
This project is open-source and available under the [MIT License](LICENSE).

