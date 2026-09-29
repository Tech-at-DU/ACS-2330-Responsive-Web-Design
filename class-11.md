# Class 11: Responsive Forms

Forms are one of the hardest UI elements to get right on mobile. Small touch targets, the virtual keyboard covering inputs, placeholder text mistaken for labels, and tiny checkboxes are all common failures. This class covers how to build forms that work well on every device.

## Objectives

- Use correct input types to trigger appropriate mobile keyboards
- Size inputs and controls for touch interaction
- Structure labels for responsive layouts
- Group related radios/checkboxes with `<fieldset>` and `<legend>`
- Write error states with ARIA
- Style forms with Tailwind CSS
- Build a required new-page form (Submit a Space) into the SFPOPOS project

---

## Warmup: Diagnose a Broken Form (10 mins)

Before the lecture, break this down yourselves. Pair up.

```html
<form>
  <input type="text" placeholder="First Name">
  <input type="text" placeholder="Email">
  <input type="text" placeholder="Phone">
  <input type="checkbox"> I agree to the terms
  <button>Submit</button>
</form>
```

**Part 1 (5 mins):** With your partner, list every mobile problem you can find in this form. Don't fix it — just diagnose. Write down what would go wrong and why.

**Part 2 (5 mins):** Pull this form up on your own phone (or paste it into a codepen and open that on your phone). Tap into the email field. Try to see the submit button while the keyboard is up. Tap the checkbox with your thumb. Note what actually breaks versus what you predicted.

This is the same idea as the VoiceOver exercise from class-6 — feeling a failure sticks better than reading about it. You'll compare your list against the section below.

---

## Why Forms Fail on Mobile

Check your warmup list against these four. Did you find all of them?

1. **Touch targets too small** — default input height is often ~34px. Minimum for reliable tapping is 44px.
2. **Wrong keyboard** — `type="text"` on an email field shows a standard keyboard, not the email keyboard with `@`. The user has to hunt for it.
3. **Placeholder as label** — placeholder text disappears when the user starts typing. Now they can't remember what the field was for. It also has low contrast by default and is not announced reliably by screen readers.
4. **Virtual keyboard covers inputs** — on mobile, the keyboard takes ~40% of the screen. Fields near the bottom get hidden behind it. Labels stacked above inputs solve this.

---

## Input Types

Using the correct `type` attribute gives mobile users the right keyboard automatically — no extra code required.

| Input type | Mobile keyboard | Use for |
|-----------|----------------|---------|
| `type="text"` | Standard | Default — only use when nothing else fits |
| `type="email"` | Email (shows `@`, `.com`) | Email addresses |
| `type="tel"` | Numeric keypad | Phone numbers |
| `type="number"` | Number keyboard | Quantities, ages |
| `type="search"` | Search (shows search/done button) | Search fields |
| `type="url"` | URL keyboard (shows `.com`, `/`) | URLs |
| `type="password"` | Standard + masked | Passwords |
| `type="date"` | Date picker | Dates |

```html
<!-- Wrong — user has to find @ manually -->
<input type="text" name="email" placeholder="Email">

<!-- Right — email keyboard appears automatically -->
<input type="email" name="email" autocomplete="email">
```

### `autocomplete`

The `autocomplete` attribute lets the browser and password managers pre-fill fields. On mobile this saves significant typing. Always add it.

```html
<input type="text"     name="name"    autocomplete="name">
<input type="email"    name="email"   autocomplete="email">
<input type="tel"      name="phone"   autocomplete="tel">
<input type="password" name="pass"    autocomplete="current-password">
```

Common values: `name`, `given-name`, `family-name`, `email`, `tel`, `street-address`, `postal-code`, `current-password`, `new-password`.

---

## Touch-Friendly Sizing

Minimum touch target: **44 × 44px** (WCAG 2.5.5). This applies to inputs, buttons, checkboxes, and radio buttons.

```css
input,
select,
textarea {
  min-height: 44px;
  padding: 10px 12px;
  width: 100%;
  box-sizing: border-box;
}
```

`width: 100%` — inputs should fill their container on mobile. Fixed-width inputs overflow or leave dead space on small screens.

For checkboxes and radio buttons, the default click target is the tiny box or circle. Wrap them in a `<label>` so the entire label text is also clickable:

```html
<!-- Bad — only the 16px checkbox is tappable -->
<input type="checkbox" id="agree"> <label for="agree">I agree</label>

<!-- Good — label text is also tappable -->
<label>
  <input type="checkbox" name="agree">
  I agree to the terms
</label>
```

---

## Labels

Labels must always be visible. Placeholder text is not a label.

**Mobile layout — label above input:**

```html
<div class="field">
  <label for="email">Email address</label>
  <input type="email" id="email" name="email" autocomplete="email">
</div>
```

```css
.field {
  display: flex;
  flex-direction: column;
  gap: 4px;
}
```

Label above the input stays visible when the user focuses and the keyboard appears. Side-by-side labels (inline) get pushed off screen when the keyboard slides up.

**Responsive — side by side on desktop:**

For a name row on desktop, two fields can sit side by side:

```html
<div class="name-row">
  <div class="field">
    <label for="first-name">First name</label>
    <input type="text" id="first-name" name="first-name" autocomplete="given-name">
  </div>
  <div class="field">
    <label for="last-name">Last name</label>
    <input type="text" id="last-name" name="last-name" autocomplete="family-name">
  </div>
</div>
```

```css
.name-row {
  display: flex;
  flex-direction: column;  /* mobile: stacked */
  gap: 1rem;
}

@media (min-width: 768px) {
  .name-row {
    flex-direction: row;   /* desktop: side by side */
  }
}
```

---

## Error States

Error messages need to be visible, not color-only, and connected to the input for screen readers.

```html
<div class="field">
  <label for="email">Email address</label>
  <input
    type="email"
    id="email"
    name="email"
    aria-describedby="email-error"
    aria-invalid="true"
  >
  <span id="email-error" class="error">
    Enter a valid email address.
  </span>
</div>
```

- `aria-invalid="true"` — tells screen readers the field has an error
- `aria-describedby="email-error"` — connects the error message to the input; screen reader reads both label and error
- Error message below the field, not above (below = visible when keyboard is open)
- Don't use color alone — include text and/or an icon

```css
.error {
  color: #dc2626;
  font-size: 0.875rem;
}

/* Also add a visual indicator on the input */
input[aria-invalid="true"] {
  border-color: #dc2626;
  outline-color: #dc2626;
}
```

---

## Tailwind Form Styling

Tailwind resets all browser form styles, so inputs look flat. The `@tailwindcss/forms` plugin restores sensible defaults you can build on.

Install it:

```bash
npm install @tailwindcss/forms
```

Add to your CSS:

```css
@import "tailwindcss";
@plugin "@tailwindcss/forms";
```

Without the plugin, style inputs manually:

```html
<input
  type="email"
  class="w-full rounded border border-gray-300 px-3 py-3 text-base
         focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200"
>
```

### Full Tailwind Form Example

```html
<form class="flex flex-col gap-6 max-w-lg mx-auto p-4">

  <!-- Name row: stacked mobile, side by side desktop -->
  <div class="flex flex-col md:flex-row gap-4">
    <div class="flex flex-col gap-1 flex-1">
      <label for="first" class="font-medium text-gray-700">First name</label>
      <input
        type="text" id="first" name="first" autocomplete="given-name"
        class="w-full rounded border border-gray-300 px-3 py-3 text-base
               focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200"
      >
    </div>
    <div class="flex flex-col gap-1 flex-1">
      <label for="last" class="font-medium text-gray-700">Last name</label>
      <input
        type="text" id="last" name="last" autocomplete="family-name"
        class="w-full rounded border border-gray-300 px-3 py-3 text-base
               focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200"
      >
    </div>
  </div>

  <!-- Email -->
  <div class="flex flex-col gap-1">
    <label for="email" class="font-medium text-gray-700">Email address</label>
    <input
      type="email" id="email" name="email" autocomplete="email"
      class="w-full rounded border border-gray-300 px-3 py-3 text-base
             focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200"
    >
  </div>

  <!-- Message -->
  <div class="flex flex-col gap-1">
    <label for="message" class="font-medium text-gray-700">Message</label>
    <textarea
      id="message" name="message" rows="4"
      class="w-full rounded border border-gray-300 px-3 py-3 text-base
             focus:border-blue-500 focus:outline-none focus:ring-2 focus:ring-blue-200"
    ></textarea>
  </div>

  <!-- Submit — full width on mobile -->
  <button
    type="submit"
    class="w-full md:w-auto md:self-end bg-blue-600 text-white font-medium
           px-6 py-3 rounded hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-blue-400"
  >
    Send message
  </button>

</form>
```

Key Tailwind patterns in this form:
- `flex flex-col gap-6` — stacks fields with consistent spacing
- `flex flex-col md:flex-row` — name fields stack on mobile, sit side by side on desktop
- `w-full` — inputs fill container on all sizes
- `py-3` — 12px vertical padding gets input height to ~44px
- `w-full md:w-auto md:self-end` — submit button full width on mobile, natural width on desktop

---

## Challenge: Submit a Public Space

**This is required — not optional, and not a generic contact form.** Add a new page to your SFPOPOS React project where a user can submit a new public space for the site. This is the same repo you've been building since class-1 — add a route/component for it (`/submit`, `SubmitSpace.jsx`, whatever fits your project's structure).

A contact form only exercises text and email inputs — too easy to skip the hard parts of this lesson. A "submit a space" form forces grouped checkboxes, exclusive radio choices, and numeric fields with real validation ranges, on top of everything a contact form would cover.

### Required fields

| Field | Input pattern | Why it's here |
|-------|---------------|----------------|
| Space name | `type="text"`, required | Baseline text input — label, autocomplete, error state |
| Address | `type="text"`, `autocomplete="street-address"`, required | Real autocomplete value, not just `name`/`email` |
| Description | `<textarea>`, required | Multi-line input, different sizing rules than a single-line field |
| Indoor / Outdoor / Both | Radio group, required | Mutually exclusive choice — grouped with `<fieldset>` + `<legend>`, not covered elsewhere in this class |
| Amenities (seating, public art, restrooms, coffee/food nearby, power outlets, wifi) | Checkbox group, at least one selectable | Multiple related checkboxes grouped under one accessible label |
| Latitude | `type="number"`, `min="-90"`, `max="90"`, `step="any"`, required | Numeric keyboard + range validation, not just "is this a number" |
| Longitude | `type="number"`, `min="-180"`, `max="180"`, `step="any"`, required | Same, second axis |
| Submit button | full width on mobile | Ties back to the Tailwind pattern above |

Feel free to add more fields (hours, photo, contact email for the submitter) if you want to push further — the list above is the floor, not the ceiling.

### The `<fieldset>` / `<legend>` pattern

A group of checkboxes or radios needs one label for the whole group, not just labels on each option. `<fieldset>` and `<legend>` do that — screen readers announce the group name before reading each option.

```html
<fieldset>
  <legend>Space type</legend>
  <label><input type="radio" name="spaceType" value="indoor" required> Indoor</label>
  <label><input type="radio" name="spaceType" value="outdoor" required> Outdoor</label>
  <label><input type="radio" name="spaceType" value="both" required> Both</label>
</fieldset>

<fieldset>
  <legend>Amenities</legend>
  <label><input type="checkbox" name="amenities" value="seating"> Seating</label>
  <label><input type="checkbox" name="amenities" value="art"> Public art</label>
  <label><input type="checkbox" name="amenities" value="restrooms"> Restrooms</label>
  <label><input type="checkbox" name="amenities" value="coffee"> Coffee/food nearby</label>
  <label><input type="checkbox" name="amenities" value="power"> Power outlets</label>
  <label><input type="checkbox" name="amenities" value="wifi"> Wifi</label>
</fieldset>
```

```css
fieldset {
  border: 1px solid #d1d5db;
  border-radius: 8px;
  padding: 1rem;
}

legend {
  font-weight: 600;
  padding: 0 4px;
}
```

Style the same fieldset with Tailwind: `class="border border-gray-300 rounded-lg p-4"` on the fieldset, `class="font-semibold px-1"` on the legend.

### Requirements checklist

- [ ] New page/route exists for submitting a space, reachable in your app
- [ ] Every field from the table above is present
- [ ] Correct `type` on every input — text, textarea, radio, checkbox, number
- [ ] `autocomplete` set where it makes sense (address, not lat/long)
- [ ] Indoor/Outdoor/Both and Amenities are each wrapped in `<fieldset>` + `<legend>`
- [ ] Visible `<label>` on every field, including each radio/checkbox option (not placeholder-only)
- [ ] Every input, radio, checkbox, and the submit button is at least 44px tall/wide
- [ ] Latitude/longitude use `type="number"` with `min`/`max` matching real coordinate ranges
- [ ] Fields stack single-column on mobile; name/lat-long or similar pairs can sit side by side on desktop
- [ ] Submit button is full width on mobile
- [ ] At least one required field shows a real error (`aria-invalid` + `aria-describedby`) when submitted empty
- [ ] Styled with Tailwind, matching the rest of your site
- [ ] Passes a Lighthouse accessibility audit on this page

**Stretch challenge:** wire up validation on the required fields in React — block submission and show errors until every required field is valid:

```jsx
const [nameError, setNameError] = useState('')

function validateName(value) {
  setNameError(value.trim() ? '' : 'Space name is required.')
}

<input
  type="text"
  aria-invalid={nameError ? 'true' : 'false'}
  aria-describedby={nameError ? 'name-error' : undefined}
  onBlur={(e) => validateName(e.target.value)}
/>
{nameError && (
  <span id="name-error" className="text-red-600 text-sm">{nameError}</span>
)}
```

**Further stretch:** add a "Use my location" button that fills latitude/longitude automatically with the Geolocation API:

```jsx
function useMyLocation() {
  navigator.geolocation.getCurrentPosition((pos) => {
    setLat(pos.coords.latitude)
    setLng(pos.coords.longitude)
  })
}
```

---

## Peer Review (10 mins)

Before you self-assess, trade with a partner.

1. Open your partner's form on your phone, or resize your browser to 375px.
2. Try to complete and submit it — mobile keyboard only, no mouse.
3. Check their form against this list:
   - [ ] Right keyboard type appears for each field (number pad for lat/long, standard for text)
   - [ ] Labels stay visible when the virtual keyboard is open
   - [ ] Every input, checkbox, and button is comfortably tappable
   - [ ] Entering something invalid produces a clear, visible error
4. Give your partner one specific thing that worked and one specific thing to fix. "The phone field brought up the number pad" beats "looks good."

Fix whatever your partner flags before moving on.

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Required fields | Missing one or more fields from the required table (name, address, description, space type, amenities, lat, long) | All required fields present and functional | Extra fields added beyond the floor (hours, photo, contact email) |
| Input types | Default `type="text"` on most inputs | Correct type on every input, including `number` for lat/long with `min`/`max` | `autocomplete` added everywhere it applies |
| Grouped inputs | Radios/checkboxes have no group label, or `<fieldset>`/`<legend>` missing | Space type and amenities each wrapped in `<fieldset>` + `<legend>` | Group labels are specific enough to be understood out of context by a screen reader |
| Touch sizing | Inputs, radios, or checkboxes shorter than 44px, or hard to tap | All inputs, radios, checkboxes, and the button ≥ 44px tall/wide | Checkbox/radio label text is part of the tap target, not just the input |
| Labels | Placeholder-only or labels missing | Visible label above every field, including each radio/checkbox option | Labels on desktop adapt to side-by-side layout where space allows |
| Error states | No error handling | At least one required field shows a real error on empty submit, not color-only | `aria-invalid`/`aria-describedby` wired on every required field, errors clear on correction |
| Tailwind & layout | Minimal or no Tailwind styling | Form styled with Tailwind, stacks correctly on mobile | Multi-column layout on desktop where it makes sense (e.g. lat/long side by side) |
