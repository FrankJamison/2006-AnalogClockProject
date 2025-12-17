# 2006 Analog Clock Project

A small, self-contained HTML/CSS/JavaScript project that renders **two animated analog clocks** using SVG:

- **Local Time** (your device’s current local time)
- **UTC Time** (Coordinated Universal Time)

The clock hands are rotated with CSS transforms and updated every second with JavaScript.

> Note: The current date is **December 17, 2025** (per workspace context). The clocks themselves always use the viewer’s current system time.

---

## Features

- Two side-by-side clocks (Local + UTC)
- SVG-based clock face (scales cleanly without pixelation)
- Smooth-ish hand animation via CSS transform transitions (configured for the Local Time clock)
- No dependencies, build steps, or frameworks

---

## Project Structure

```
2006-AnalogClockProject/
  index.html
  css/
    style.css
  js/
    script.js
```

### What each file does

- `index.html`
  - Defines the page layout and contains the SVG markup for both clocks.
  - Each clock has three SVG groups (`<g>`) representing the hands:
    - Clock 1: `#hour1`, `#minute1`, `#second1`
    - Clock 2: `#hour2`, `#minute2`, `#second2`

- `css/style.css`
  - Handles the side-by-side layout.
  - Styles the SVG face and hands.
  - Sets the rotation pivot point via `transform-origin: 300px 300px;` for all hands.
  - Adds a transition for Clock 1 hands (`#hour1`, `#minute1`, `#second1`) to smooth motion.

- `js/script.js`
  - Reads the time and calculates hand angles in degrees.
  - Updates the SVG hand groups using `element.style.transform = "rotate(Xdeg)"`.
  - Runs updates every second using `setInterval(..., 1000)`.

---

## How It Works (High-Level)

### Hand rotation math

Each hand’s angle is computed in degrees:

- **Second hand**: $\text{seconds} \times 6$ (because $360/60 = 6$)
- **Minute hand**: $\text{minutes} \times 6$ plus a fraction based on seconds
- **Hour hand**: $\text{hours} \times 30$ plus a fraction based on minutes (because $360/12 = 30$)

### Clock update strategies

- **Local Time clock (Clock 1)**
  - Initializes hand positions once, then increments the angles every tick.

- **UTC clock (Clock 2)**
  - Recomputes the current UTC time on every tick using:
    - `getUTCHours()`
    - `getUTCMinutes()`
    - `getUTCSeconds()`

---

## Run It Locally

This is a static site, so there are a few easy options.

### Option A: Open the HTML file directly

1. Open `index.html` in your browser.

This works for most browsers because the project doesn’t make network requests.

### Option B: Start a quick local static server

If you want a real local server (recommended):

- **Python (if installed):**
  - From the project folder:
    - `python -m http.server 8080`
  - Then open:
    - `http://localhost:8080/`

- **Node.js (if installed):**
  - Install once:
    - `npm i -g serve`
  - From the project folder:
    - `serve .`

---

## Customization

Common tweaks you might want:

- **Resize the clocks**
  - The SVG is set to `width="600" height="600" viewBox="0 0 600 600"`.
  - The CSS currently applies `width: 100%` to `#clock1` and `#clock2`.

- **Change colors / stroke weights**
  - Edit the stroke/fill rules in `css/style.css` for:
    - `.circle`, `.hour-marks`, `.hour-arm`, `.minute-arm`, `.second-arm`, `.mid-circle`

- **Layout changes**
  - The page uses a flex container (`.main`) for side-by-side layout.

---

## Browser Compatibility

Works in any modern browser that supports:

- SVG
- CSS transforms (`transform`, `transform-origin`)

---

## Troubleshooting

- **Hands are not moving**
  - Confirm JavaScript is enabled.
  - Check the DevTools console for errors.

---

## Credits / Notes

- The clock face and hands are drawn in SVG.
- The animation is driven by updating each hand’s `transform: rotate(...)` in JavaScript.
