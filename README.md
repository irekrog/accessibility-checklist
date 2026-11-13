# Accessibility Checklist

A practical checklist for building accessible websites, mapped to **[WCAG 2.2](https://www.w3.org/TR/WCAG22/)** success criteria (W3C Recommendation).

Level **AA** is the usual target: it is what the European Accessibility Act (EN 301 549), Section 508, the ADA case law and most national laws point to.

> Automated tools find only part of the issues. Always test with a keyboard and at least one screen reader.

## Table of Contents

* **[Document & semantics](#document--semantics)**
* **[Images & non-text content](#images--non-text-content)**
* **[Color, contrast & visual presentation](#color-contrast--visual-presentation)**
* **[Keyboard & focus](#keyboard--focus)**
* **[Pointer & touch](#pointer--touch)**
* **[Forms](#forms)**
* **[ARIA & custom components](#aria--custom-components)**
* **[Media](#media)**
* **[Motion, timing & animation](#motion-timing--animation)**
* **[Consistency & help](#consistency--help)**
* **[Testing tools](#testing-tools)**
* **[Useful links](#useful-links)**

## Document & semantics

**Add `lang` attribute to `<html>` tag, and to parts of the page in a different language**
* `<html lang="en">`, `<span lang="pl">Dzień dobry</span>`
> * [3.1.1 - Language of Page - Level A](https://www.w3.org/WAI/WCAG22/Understanding/language-of-page)
> * [3.1.2 - Language of Parts - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/language-of-parts)

**Add `dir="rtl"` for right-to-left languages (Arabic, Hebrew etc.)**
> * [1.3.2 - Meaningful Sequence - Level A](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence)

**Give every page a unique, descriptive `<title>`**
* Pattern: `Page name – Section – Site name`. In SPAs update `document.title` on every route change.
> * [2.4.2 - Page Titled - Level A](https://www.w3.org/WAI/WCAG22/Understanding/page-titled)

**Don't block zoom in the viewport `<meta>` tag**
* Avoid `maximum-scale=1` and `user-scalable=no`. Use `<meta name="viewport" content="width=device-width, initial-scale=1">`.
> * [1.4.4 - Resize Text - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text)

**Use landmarks: `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`**
* Exactly one `<main>` per page. If there are several `<nav>`s, name them (`aria-label="Main"`, `aria-label="Breadcrumbs"`).
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)

**Use a logical heading structure (`<h1>`–`<h6>`) and don't skip levels**
* One `<h1>` describing the page is a good practice (not a WCAG requirement).
* Don't rely on `<section>` / `<article>` to change heading levels – the HTML "document outline" algorithm was never implemented and has been removed from the HTML spec.
* Never pick a heading level for its visual size – style it with CSS.
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [2.4.6 - Headings and Labels - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels)

**Use semantic HTML for content and behavior**
* Examples:
  * Actions use `<button>`, navigation uses `<a href>`. Never `<div onclick>`.
  * Table data goes in `<table>` with `<th scope>` and a `<caption>`. Don't use tables for layout.
  * Lists use `<ul>` / `<ol>` + `<li>`, and `<dl>` for term–description pairs.
  * Dates use `<time datetime="2026-11-13">`.
  * Use `<figure>` with `<figcaption>` for illustrations and embeds.
  * Use `<strong>` / `<em>` for importance and emphasis; `<b>` / `<i>` carry no semantics.
  * Use native `<dialog>`, `<details>` / `<summary>` before building your own.
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [4.1.2 - Name, Role, Value - Level A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Keep DOM order equal to visual order**
* Watch out for CSS `order`, `flex-direction: row-reverse`, `grid-area` and absolute positioning.
> * [1.3.2 - Meaningful Sequence - Level A](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence)
> * [2.4.3 - Focus Order - Level A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)

**Add a "Skip to main content" link as the first focusable element**
> * [2.4.1 - Bypass Blocks - Level A](https://www.w3.org/WAI/WCAG22/Understanding/bypass-blocks)

**Write link text that makes sense on its own (no "click here", "read more")**
* If you must use "Read more", extend the name so it starts with the visible text: `aria-label="Read more about pricing"`.
> * [2.4.4 - Link Purpose (In Context) - Level A](https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context)

**Provide more than one way to find a page (navigation, search, sitemap)**
> * [2.4.5 - Multiple Ways - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/multiple-ways)

## Images & non-text content

**Add an `alt` attribute to every `<img>`**
* Informative image: describe its meaning, not its look.
* Decorative image: `alt=""` (empty, never missing).
* Image inside a link or button: describe the action / destination.
* Complex image (chart, diagram): short `alt` + longer description nearby.
* Inline `<svg>`: `role="img"` + `<title>` (or `aria-label`); decorative SVG: `aria-hidden="true"`.
* Icon-only buttons need an accessible name (visually hidden text or `aria-label`).
> * [1.1.1 - Non-text Content - Level A](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content)
> * [WAI Images Tutorial – alt decision tree](https://www.w3.org/WAI/tutorials/images/decision-tree/)

**Use real text instead of images of text**
> * [1.4.5 - Images of Text - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/images-of-text)

## Color, contrast & visual presentation

**Text contrast ratio is at least 4.5:1 (3:1 for large text: 24px, or 18.66px bold)**
> * [1.4.3 - Contrast (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum)
> * [1.4.6 - Contrast (Enhanced) - Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced) – 7:1 / 4.5:1

**UI components and meaningful graphics have contrast at least 3:1**
* Input borders, icons, focus indicators, chart lines, checkbox states.
> * [1.4.11 - Non-text Contrast - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast)

**Don't use color as the only way to convey information**
* Links in text need more than color (e.g. underline). Required fields and errors need text or an icon, not only red.
> * [1.4.1 - Use of Color - Level A](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color)

**Don't rely on shape, color, size, position or sound alone in instructions ("click the red button on the right")**
> * [1.3.3 - Sensory Characteristics - Level A](https://www.w3.org/WAI/WCAG22/Understanding/sensory-characteristics)

**Page works at 200% text zoom and at 320 CSS px width (400% zoom) without horizontal scrolling**
* Use relative units (`rem`, `em`, `%`) and responsive layouts.
> * [1.4.4 - Resize Text - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text)
> * [1.4.10 - Reflow - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/reflow)

**Don't lock orientation (portrait / landscape)**
> * [1.3.4 - Orientation - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/orientation)

**Content doesn't break when users override text spacing**
* Line height 1.5, paragraph spacing 2×, letter spacing 0.12em, word spacing 0.16em. Avoid fixed heights on text containers.
> * [1.4.12 - Text Spacing - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing)

**Tooltips and popovers shown on hover/focus are dismissible (Esc), hoverable and persistent**
> * [1.4.13 - Content on Hover or Focus - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus)

**Support Windows High Contrast / forced colors mode**
* Test with `@media (forced-colors: active)`; don't convey state only via `background-color` or `box-shadow`.

## Keyboard & focus

**Everything works with keyboard only, without timing requirements**
* Test: `Tab`, `Shift+Tab`, `Enter`, `Space`, arrow keys, `Esc`.
> * [2.1.1 - Keyboard - Level A](https://www.w3.org/WAI/WCAG22/Understanding/keyboard)

**No keyboard traps – focus can always move away from a component**
> * [2.1.2 - No Keyboard Trap - Level A](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap)

**Single-key shortcuts can be turned off or remapped, or only work on focus**
> * [2.1.4 - Character Key Shortcuts - Level A](https://www.w3.org/WAI/WCAG22/Understanding/character-key-shortcuts)

**Tab order is logical; don't use positive `tabindex` values**
* `tabindex="0"` – make a custom element focusable; `tabindex="-1"` – focusable only from script.
> * [2.4.3 - Focus Order - Level A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)

**Never remove the focus indicator without a visible replacement**
* Don't use `outline: none` / `outline: 0` alone. Use `:focus-visible` for a clear custom style, e.g. `outline: 2px solid; outline-offset: 2px;`.
> * [2.4.7 - Focus Visible - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible)
> * [2.4.13 - Focus Appearance - Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance) (new in 2.2)

**Focused element is not hidden behind sticky headers, cookie banners or chat widgets**
* Use `scroll-padding-top` for sticky headers.
> * [2.4.11 - Focus Not Obscured (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum) (new in 2.2)

**Receiving focus or changing a value doesn't trigger an unexpected change of context**
* No auto-submit on `<select>` change, no opening new windows on focus.
> * [3.2.1 - On Focus - Level A](https://www.w3.org/WAI/WCAG22/Understanding/on-focus)
> * [3.2.2 - On Input - Level A](https://www.w3.org/WAI/WCAG22/Understanding/on-input)

**Manage focus in dynamic UIs**
* Modal dialog: move focus inside on open, keep it there (or use native `<dialog>` + `showModal()`), close with `Esc`, return focus to the trigger on close.
* SPA route change: move focus to the new page's `<h1>` (or main region) and update the title.
* Deleting an item: move focus to a sensible neighbour, not `<body>`.
* Use the `inert` attribute to disable content behind a modal.
> * [2.4.3 - Focus Order - Level A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)
> * [ARIA APG – Dialog (Modal) Pattern](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)

## Pointer & touch

**Interactive targets are at least 24×24 CSS px (or have enough spacing)**
* 44×44 px is the recommended size (AAA, and Apple/Google guidelines). Inline links in text are excepted.
> * [2.5.8 - Target Size (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum) (new in 2.2)
> * [2.5.5 - Target Size (Enhanced) - Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced)

**Every drag action has a single-pointer alternative (e.g. buttons for reordering, click on slider track)**
> * [2.5.7 - Dragging Movements - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements) (new in 2.2)

**Multipoint or path-based gestures (pinch, swipe) have a single-tap alternative**
> * [2.5.1 - Pointer Gestures - Level A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures)

**Actions fire on pointer up (`click`), not on `mousedown` / `touchstart`**
> * [2.5.2 - Pointer Cancellation - Level A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-cancellation)

**Accessible name contains the visible label text (ideally starts with it)**
* A button showing "Search" must not have `aria-label="Find products"` – voice control users say "click Search".
> * [2.5.3 - Label in Name - Level A](https://www.w3.org/WAI/WCAG22/Understanding/label-in-name)

**Features triggered by device motion (shake, tilt) have a UI alternative and can be disabled**
> * [2.5.4 - Motion Actuation - Level A](https://www.w3.org/WAI/WCAG22/Understanding/motion-actuation)

## Forms

**Every input has a visible, programmatically associated `<label>`**
* `<label for="email">` or wrap the input. Placeholder is not a label.
* Group related controls (radio buttons, checkboxes) with `<fieldset>` + `<legend>`.
* Give instructions and the expected format before the field (connect them with `aria-describedby`).
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [3.3.2 - Labels or Instructions - Level A](https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions)

**Use `autocomplete` attributes for personal data fields**
* `autocomplete="name"`, `"email"`, `"tel"`, `"street-address"`, `"current-password"`, `"one-time-code"` etc.
> * [1.3.5 - Identify Input Purpose - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose)

**Identify errors in text and suggest how to fix them**
* Mark invalid fields with `aria-invalid="true"`, link the message via `aria-describedby`.
* On submit, move focus to an error summary or the first invalid field.
> * [3.3.1 - Error Identification - Level A](https://www.w3.org/WAI/WCAG22/Understanding/error-identification)
> * [3.3.3 - Error Suggestion - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/error-suggestion)

**For legal, financial or data-changing submissions allow review, correction or undo**
> * [3.3.4 - Error Prevention (Legal, Financial, Data) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/error-prevention-legal-financial-data)

**Don't ask users to re-enter information they already provided in the same process**
* Auto-fill it or let them select it ("Billing address same as shipping").
> * [3.3.7 - Redundant Entry - Level A](https://www.w3.org/WAI/WCAG22/Understanding/redundant-entry) (new in 2.2)

**Login doesn't require a cognitive test (remembering, transcribing, solving puzzles)**
* Allow paste and password managers in password / code fields. Support passkeys, magic links or OAuth. Avoid text CAPTCHAs.
> * [3.3.8 - Accessible Authentication (Minimum) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum) (new in 2.2)

## ARIA & custom components

**First rule of ARIA: if a native HTML element exists, use it**
* No ARIA is better than bad ARIA. Don't override native semantics (`<ul role="navigation">`, `<button role="link">`).
> * [Read Me First – ARIA APG](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/)
> * [Using ARIA – W3C](https://www.w3.org/TR/using-aria/)

**Custom widgets expose correct name, role, state and value**
* Toggle: `aria-pressed`; accordion / disclosure: `aria-expanded` + `aria-controls`; current page in nav: `aria-current="page"`.
* Follow keyboard interaction from the [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) (tabs, menus, combobox, etc.).
> * [4.1.2 - Name, Role, Value - Level A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Never put `aria-hidden="true"` on focusable elements or their ancestors**
> * [4.1.2 - Name, Role, Value - Level A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Announce status messages without moving focus**
* Use `role="status"` (polite) or `role="alert"` (assertive) for "Added to cart", "3 results found", form errors. The live region must exist in the DOM before its content changes.
> * [4.1.3 - Status Messages - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/status-messages)

**Validate your HTML anyway**
* 4.1.1 Parsing was removed in WCAG 2.2, but duplicate `id`s still break `<label for>`, `aria-labelledby` and `aria-describedby`.

## Media

**Provide a transcript for audio-only and a text or audio alternative for video-only content (prerecorded)**
> * [1.2.1 - Audio-only and Video-only (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/Understanding/audio-only-and-video-only-prerecorded)

**Provide captions for prerecorded video with audio**
* Use `<track kind="captions">` (WebVTT). Auto-generated captions must be reviewed.
> * [1.2.2 - Captions (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded)

**Provide audio description or a full text alternative for prerecorded video**
> * [1.2.3 - Audio Description or Media Alternative (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG22/Understanding/audio-description-or-media-alternative-prerecorded)
> * [1.2.5 - Audio Description (Prerecorded) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/audio-description-prerecorded)

**Provide captions for live audio/video**
> * [1.2.4 - Captions (Live) - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/captions-live)

**Provide sign language interpretation for prerecorded media**
> * [1.2.6 - Sign Language (Prerecorded) - Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/sign-language-prerecorded)

**Audio that plays automatically for more than 3 seconds can be paused/stopped or its volume controlled independently**
* Better: never autoplay audio.
> * [1.4.2 - Audio Control - Level A](https://www.w3.org/WAI/WCAG22/Understanding/audio-control)

**Media players are keyboard and screen reader accessible**
> * [2.1.1 - Keyboard - Level A](https://www.w3.org/WAI/WCAG22/Understanding/keyboard)

## Motion, timing & animation

**Moving, blinking, scrolling or auto-updating content (carousels, tickers) lasting more than 5 seconds can be paused, stopped or hidden**
> * [2.2.2 - Pause, Stop, Hide - Level A](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide)

**Time limits (session timeouts) can be turned off, adjusted or extended**
> * [2.2.1 - Timing Adjustable - Level A](https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable)

**Nothing flashes more than 3 times per second**
> * [2.3.1 - Three Flashes or Below Threshold - Level A](https://www.w3.org/WAI/WCAG22/Understanding/three-flashes-or-below-threshold)

**Respect `prefers-reduced-motion`**
* Disable or reduce parallax, large transitions and auto-playing animations.
> * [2.3.3 - Animation from Interactions - Level AAA](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions)

## Consistency & help

**Navigation repeated across pages is in the same relative order**
> * [3.2.3 - Consistent Navigation - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/consistent-navigation)

**Components with the same function are labelled consistently**
> * [3.2.4 - Consistent Identification - Level AA](https://www.w3.org/WAI/WCAG22/Understanding/consistent-identification)

**Help mechanisms (contact, chat, FAQ link) are in the same place on every page**
> * [3.2.6 - Consistent Help - Level A](https://www.w3.org/WAI/WCAG22/Understanding/consistent-help) (new in 2.2)

## Testing tools

**Automated checks**
* [axe DevTools](https://www.deque.com/axe/devtools/) / [axe-core](https://github.com/dequelabs/axe-core) (also for CI: `@axe-core/playwright`, `jest-axe`, `cypress-axe`)
* [WAVE](https://wave.webaim.org/)
* [Lighthouse](https://developer.chrome.com/docs/lighthouse/accessibility/scoring)
* [Accessibility Insights](https://accessibilityinsights.io/) – includes guided manual "Assessment"
* [eslint-plugin-jsx-a11y](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y) for React

**Browser DevTools**
* Chrome / Edge: Accessibility pane and full accessibility tree, CSS Overview contrast issues, emulation of vision deficiencies, `prefers-reduced-motion` and `forced-colors`
* Firefox: Accessibility Inspector (tab order overlay, contrast and keyboard checks)

**Screen readers**
* [NVDA](https://www.nvaccess.org/) (Windows, free) – test with Firefox or Chrome
* JAWS (Windows, commercial)
* VoiceOver (macOS / iOS, built-in) – test with Safari
* TalkBack (Android, built-in) – test with Chrome
* Narrator (Windows, built-in)

**Contrast checkers**
* [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
* [Colour Contrast Analyser (TPGi)](https://www.tpgi.com/color-contrast-checker/)

## Useful links

* [WCAG 2.2 – How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/)
* [What's New in WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)
* [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
* [WAI Easy Checks – A First Review of Web Accessibility](https://www.w3.org/WAI/test-evaluate/easy-checks/)
* [WebAIM](https://webaim.org/) and the [WebAIM Million](https://webaim.org/projects/million/) report
* [The A11Y Project Checklist](https://www.a11yproject.com/checklist/)
* [MDN – Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)
* [GOV.UK Design System](https://design-system.service.gov.uk/) – well-tested accessible components
* [Inclusive Components](https://inclusive-components.design/)
* [HTML5 Accessibility](https://www.html5accessibility.com/)
* [BBC Accessibility News and You](https://bbc.github.io/accessibility-news-and-you/)
* [European Accessibility Act](https://commission.europa.eu/strategy-and-policy/policies/justice-and-fundamental-rights/disability/union-equality-strategy-rights-persons-disabilities-2021-2030/european-accessibility-act_en) – applies since 28 June 2025
* [WCAG 3.0 (Working Draft)](https://www.w3.org/TR/wcag-3.0/) – not yet a standard, keep an eye on it
