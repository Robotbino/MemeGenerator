# Meme Generator 🖼️

A React-based meme generator that allows users to create custom memes by adding text to randomly fetched images from the Imgflip API.

## About This Project

This project is part of my React learning journey. I'm documenting my progress by building practical projects and pushing them to GitHub as I advance through core React concepts. Each project represents a milestone in understanding different aspects of the React ecosystem.

## What I Learned

### React Fundamentals

**Component Architecture**
- Breaking down the UI into reusable, modular components (`Header`, `Main`, `App`)
- Understanding the parent-child relationship between components
- Organising project structure with separate component files

**JSX Syntax**
- Writing HTML-like syntax within JavaScript
- Embedding JavaScript expressions using curly braces `{}`
- Handling className instead of class for styling

### State Management with `useState`

```jsx
const [meme, setMeme] = useState({
    topText: "One does not simply",
    bottomText: "Walk into Mordor",
    imageUrl: "http://i.imgflip.com/1bij.jpg"
})
```

**Key Takeaways:**
- State is data that changes over time and triggers re-renders
- The `useState` hook returns an array with the current state and a setter function
- State should be updated immutably using the spread operator
- Complex state can be stored as objects for related data

### Side Effects with `useEffect`

```jsx
useEffect(() => {
    fetch("https://api.imgflip.com/get_memes")
        .then(res => res.json())
        .then(data => setAllMemes(data.data.memes))
}, [])
```

**Key Takeaways:**
- `useEffect` handles operations outside React's rendering cycle (API calls, subscriptions, DOM manipulation)
- The dependency array `[]` controls when the effect runs
- An empty array means the effect runs once on mount
- This is the standard pattern for fetching data when a component loads

### Controlled Components & Forms

```jsx
<input
    type="text"
    name="topText"
    onChange={handleChange}
    value={meme.topText}
/>
```

**Key Takeaways:**
- React controls the input's value through state (single source of truth)
- The `onChange` handler updates state on every keystroke
- Using `name` attributes enables dynamic property updates with computed property names `[name]: value`

### Event Handling

```jsx
function handleChange(event) {
    const {value, name} = event.currentTarget
    setMeme(prevMeme => ({
        ...prevMeme,
        [name]: value
    }))
}
```

**Key Takeaways:**
- Event handlers receive the synthetic event object
- Destructuring extracts needed properties cleanly
- Callback form of setState (`prevMeme => ...`) ensures updates based on the latest state
- Spread operator preserves existing state while updating specific properties

### Conditional Rendering & Dynamic Data

- Rendering content based on state values
- Mapping over arrays to display dynamic content
- Updating the UI reactively when state changes

## Features

- **Random Meme Generation**: Fetches random meme templates from the Imgflip API
- **Custom Text Overlay**: Add custom top and bottom text to any meme
- **Real-time Preview**: See changes instantly as you type
- **Responsive Design**: Works across different screen sizes

## Tech Stack

- **React 18** - UI library
- **Vite** - Build tool and dev server
- **CSS3** - Styling with Grid and Flexbox
- **Imgflip API** - Meme template source

## Project Structure

```
meme-generator/
├── index.html
├── index.jsx
├── index.css
├── App.jsx
├── components/
│   ├── Header.jsx
│   └── Main.jsx
└── images/
    └── troll-face.png
```

## Getting Started

### Prerequisites

- Node.js (v16 or higher)
- npm or yarn

### Installation

1. Clone the repository
   ```bash
   git clone https://github.com/yourusername/meme-generator.git
   ```

2. Navigate to the project directory
   ```bash
   cd meme-generator
   ```

3. Install dependencies
   ```bash
   npm install
   ```

4. Start the development server
   ```bash
   npm run dev
   ```

5. Open your browser and visit `http://localhost:5173`

## How It Works

1. On load, the app fetches meme templates from the Imgflip API
2. Users enter custom text in the input fields
3. Clicking "Get a new meme image" selects a random template
4. The meme preview updates in real-time with the custom text overlay

## My React Learning Path

This project is part of my ongoing journey to become a full-stack developer. Here's where it fits in my learning progression:

| Concept | Status |
|---------|--------|
| Components & Props | ✅ |
| State & useState | ✅ |
| Event Handling | ✅ |
| useEffect & API Calls | ✅ |
| Controlled Forms | ✅ |
| Conditional Rendering | ✅ |
| Context API | 🔄 Next |
| Custom Hooks | 🔄 Upcoming |
| React Router | 🔄 Upcoming |

## Future Improvements

- [ ] Add download functionality for created memes
- [ ] Implement drag-and-drop text positioning
- [ ] Add font size and colour customisation
- [ ] Save favourite memes to local storage
- [ ] Share directly to social media

## Connect With Me

I'm a Junior Java Developer transitioning into full-stack development. Follow my journey:

- **GitHub**: 
- **LinkedIn**: 

---

*Built with ☕ and curiosity while learning React*
