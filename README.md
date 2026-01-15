# Meme Generator

A simple React app that pulls meme templates from the Imgflip API and lets you slap custom text on them.


<img width="1914" height="848" alt="image" src="https://github.com/user-attachments/assets/f5fddc2a-a516-4c50-a2fb-9ac1ba08e3d7" />

---

## Why I Built This

I'm working through React fundamentals and this project hit several concepts I needed to get comfortable with: managing state across a form, fetching external data on component mount, and handling controlled inputs. It's not a complex app, but it forced me to actually understand how these pieces connect rather than just copying patterns.

## Technical Decisions

### State Structure

I went with a single state object for the meme data instead of three separate `useState` calls:

```jsx
const [meme, setMeme] = useState({
    topText: "One does not simply",
    bottomText: "Walk into Mordor",
    imageUrl: "http://i.imgflip.com/1bij.jpg"
})
```

This made the update logic cleaner since `topText`, `bottomText`, and `imageUrl` are conceptually one thing—the current meme being edited. The tradeoff is slightly more verbose updates with the spread operator, but it keeps related data together.

### Form Handling

Rather than writing separate handlers for each input, I used the `name` attribute to make one handler work for both:

```jsx
function handleChange(event) {
    const {value, name} = event.currentTarget
    setMeme(prevMeme => ({
        ...prevMeme,
        [name]: value
    }))
}
```

The computed property name `[name]` was new to me, it lets you dynamically set which property gets updated based on which input fired the event.

### Data Fetching

The `useEffect` with an empty dependency array runs once when the component mounts. I store all the meme templates in state, then pick randomly from that array when the user clicks the button. This avoids hitting the API on every click.

```jsx
useEffect(() => {
    fetch("https://api.imgflip.com/get_memes")
        .then(res => res.json())
        .then(data => setAllMemes(data.data.memes))
}, [])
```

No loading state or error handling here—something I'd add in a production app, but kept it minimal for learning purposes.

## The CSS

The text overlay effect uses absolute positioning on the spans within a relative container. The text shadow creates that classic meme outline:

```css
text-shadow:
    2px 2px 0 #000,
    -2px -2px 0 #000,
    2px -2px 0 #000,
    -2px 2px 0 #000,
    /* ... all 8 directions */
```

This is a common trick, you can't do a true text stroke in CSS that works everywhere, so stacking shadows in every direction fakes it.

## Running Locally

```bash
git clone https://github.com/Robotbino/MemeGenerator.git
cd meme-generator
npm install
npm run dev
```

## What I'd Do Differently

If I revisited this, I'd probably:

- Add proper error handling for the API call
- Include a loading indicator while memes are fetching
- Let users download the finished meme (would need canvas or a backend)
- Add keyboard support (Enter to get new image)

## Stack

React 18, Vite, vanilla CSS

---

Part of my React learning projects. I'm a junior developer building out my frontend skills, other projects in this series are in my [repositories](https://github.com/Robotbino?tab=repositories).
