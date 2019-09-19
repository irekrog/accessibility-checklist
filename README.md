# Accessibility Checklist

## Table of Contents

* **[HTML](#html)**
* **[CSS](#css)**
* **[OTHER](#other)**
* **[BEHAVIOR](#behavior)**
* **[TOOLS](#tools)**
* **[USEFUL LINKS](#useful-links)**

## HTML

**Add `alt` attribute with description or not (then empty) to every `<img>` tag**
> * [1.1.1 - Non-text Content - Level](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=111#qr-text-equiv-all)

**Use only one `<h1>` per page**
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=131#qr-content-structure-separation-programmatic)
> * [Creating on outline (look at the Warning)](http://w3c.github.io/html/sections.html#creating-an-outline)
> * [Computer says NO to HTML5 document outline](http://html5doctor.com/computer-says-no-to-html5-document-outline/)

**Use proper and semantic HTML tags to presenting and behavior of content**
* Examples:
  * Date and time should be in the `<time>` tag
  * Table data should be in the `<table>` tag
  * Use `<caption>` to title of the table
  * If you have "Back to top" button on the page you should use `<button>` tag to this
  * To listed items use `<ul>` `<li>` (items ordered isn't important) or `<ol>` `<li>` (items ordered is important)
  * Use `<figure`> tag with `<figcaption>` to embeds
  * Watch out for the difference between `<b>` / `<strong>` and `<i>` / `<em>`
  * Use `<label>`s tag to `<input>`s tags
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=131#qr-content-structure-separation-programmatic)

**Separating content layer (HTML) from presentation layer (CSS)**
> * [1.3.1 - Info and Relationships - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=131#content-structure-separation-programmatic)

**Add `dir` attribute to `<html>` tag**
> * [1.3.2 - Meaningful Sequence - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=132#qr-content-structure-separation-sequence)

**Don't use `maximum-scale=1.0` in viewport `<meta>` tag**
> * [1.4.4 - Resize text - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=144#qr-visual-audio-contrast-scale)

**Use skip links navigation**
> * [2.4.1 - Bypass Blocks - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=241#qr-navigation-mechanisms-skip)

**Use `<title>` tag**
> * [2.4.2 - Page Titled - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=242#qr-navigation-mechanisms-title)

**Add `lang` attribute to `<html>` tag**
> * [3.1.2 - Language of Parts - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=312#qr-meaning-other-lang-id)

## CSS

**Contrast ratio should be 4.5:1 for normal text and 3:1 for large text**
> * [1.4.3 - Contrast (Minimum) - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=143#qr-visual-audio-contrast-contrast)
> * [1.4.6 - Contrast (Enhanced) - Level AAA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=146#qr-visual-audio-contrast7)

**Don't remove focus (outline property in CSS) from interactive tags (`<a>`, `<button>`, `<input>` etc.)**
> * [2.4.7 - Focus Visible - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=247#qr-navigation-mechanisms-focus-visible)
> * [3.2.1 - On Focus - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=321#qr-consistent-behavior-receive-focus)
> * [DON'T DO IT - CSS outline property - outline: none and outline: 0](http://www.outlinenone.com/)

## OTHER
**Provide transcript for video or audio media (prerecorded)**
> * [1.2.1 - Audio-only and Video-only (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=121#qr-text-equiv-all)

**Provide captions for video or audio media (prerecorded)**
> * [1.2.2 - Captions (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=122#media-equiv-captions)

**Provide audiodescripton or alternative media (prerecorded)**
> * [1.2.3 - Audio Description or Media Alternative (Prerecorded) - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=123#media-equiv-audio-desc)

**Provide captions for live audio or video**
> * [1.2.4 - Captions (Live) - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=124#media-equiv-audio-desc)

**Provide audiodescription for prerecorded video**
> * [1.2.5 - Audio Description (Prerecorded) - Level AA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=125#media-equiv-audio-desc)

**Provide sign language for media content**
> * [1.2.6 - Sign Language (Prerecorded) - Level AAA](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=126#media-equiv-audio-desc)

## BEHAVIOR
**Don't use shapes, colors, sounds to continue execute instructions. (Click on the red shape to continue)**
> * [1.3.3 - Sensory Characteristics - Level A](https://www.w3.org/WAI/WCAG20/quickref/#content-structure-separation-understanding)

**If you have a form with required inputs don't use only colors to provide information about that**
> * [1.4.1 - Use of Color - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=141#visual-audio-contrast-without-color)

**If you have an audio automatically plays for more than 3 second should have mechanism to play, pause and stop this or control audio volume independent from OS**
> * [1.4.2 - Audio Control - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=142#visual-audio-contrast-dis-audio)

**Ensure tab sequence is logical**
> * [2.4.3 - Focus Order - Level A](https://www.w3.org/WAI/WCAG20/quickref/?showtechniques=243#qr-navigation-mechanisms-focus-order)

## TOOLS 
* [NVDA (NonVisual Desktop Access)](https://www.nvaccess.org/)
* Accessibility Tab in Chrome DevTools
* [Lighthouse](https://github.com/GoogleChrome/lighthouse)

## USEFUL LINKS
* http://www.html5accessibility.com/
* https://webaim.org/
* https://bbc.github.io/accessibility-news-and-you/
