# Class 11: Responsive Forms

Forms are one of the hardest UI elements to get right on mobile. Small touch targets, the virtual keyboard covering inputs, placeholder text mistaken for labels, and tiny checkboxes are all common failures. This class covers how to build forms that work well on every device.

## Objectives

- Use correct input types to trigger appropriate mobile keyboards
- Size inputs and controls for touch interaction
- Structure labels for responsive layouts
- Write error states with ARIA
- Style forms with Tailwind CSS

---

## Why Forms Fail on Mobile

Four common failures:

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

## Challenge

If your Project 2 includes a form, build it now following the patterns above. If it doesn't, build a contact form as a standalone exercise.

Your form must:
- [ ] Use correct `type` attributes for every input
- [ ] Include `autocomplete` on all fields
- [ ] Have visible `<label>` elements above every input (not placeholder-only)
- [ ] Have inputs at least 44px tall
- [ ] Stack fields single-column on mobile, allow multi-column on desktop where appropriate
- [ ] Submit button is full width on mobile
- [ ] Include at least one error state with `aria-invalid` and `aria-describedby`
- [ ] Pass Lighthouse accessibility audit on the form page

**Stretch challenge:** Add client-side validation in React. When a field fails validation, set `aria-invalid="true"` and show the error message. Clear the error when the user corrects the input.

```jsx
const [emailError, setEmailError] = useState('')

function validateEmail(value) {
  if (!value.includes('@')) {
    setEmailError('Enter a valid email address.')
  } else {
    setEmailError('')
  }
}

<input
  type="email"
  aria-invalid={emailError ? 'true' : 'false'}
  aria-describedby={emailError ? 'email-error' : undefined}
  onBlur={(e) => validateEmail(e.target.value)}
/>
{emailError && (
  <span id="email-error" className="text-red-600 text-sm">{emailError}</span>
)}
```

---

## Assess your work

| Category | Does not meet | Meets | Exceeds |
|----------|--------------|-------|---------|
| Input types | Default `type="text"` on all inputs | Correct type on every input (email, tel, etc.) | `autocomplete` added to all fields |
| Touch sizing | Inputs shorter than 44px | All inputs and buttons ≥ 44px tall | Checkboxes/radios wrapped in labels for full-width tap target |
| Labels | Placeholder-only or labels missing | Visible label above every input | Labels on desktop adapt to side-by-side layout where space allows |
| Error states | No error handling | Error message present, not color-only | `aria-invalid` and `aria-describedby` wired correctly |
| Tailwind | Minimal or no Tailwind styling | Form styled with Tailwind, mobile layout works | Responsive layout (stacked mobile, multi-column desktop on name fields) |
