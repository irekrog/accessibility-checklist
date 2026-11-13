# Checklista dostępności

[English](README.md) | **Polski**

Praktyczna checklista do tworzenia dostępnych stron internetowych, powiązana z kryteriami sukcesu **[WCAG 2.2](https://www.w3.org/TR/WCAG22/)** (rekomendacja W3C).

Zwykle celem jest poziom **AA**: do niego odwołują się Europejski Akt o Dostępności (norma EN 301 549), Section 508, orzecznictwo ADA i większość przepisów krajowych, w tym polska ustawa o dostępności cyfrowej.

> Narzędzia automatyczne wykrywają tylko część problemów. Zawsze testuj samą klawiaturą i co najmniej jednym czytnikiem ekranu.

> Wersja angielska ([README.md](README.md)) jest wersją główną. Linki do kryteriów prowadzą do angielskich stron „Understanding WCAG 2.2”.

## Spis treści

* **[Dokument i semantyka](#dokument-i-semantyka)**
* **[Obrazy i treści nietekstowe](#obrazy-i-treści-nietekstowe)**
* **[Kolor, kontrast i prezentacja](#kolor-kontrast-i-prezentacja)**
* **[Klawiatura i fokus](#klawiatura-i-fokus)**
* **[Wskaźnik i dotyk](#wskaźnik-i-dotyk)**
* **[Formularze](#formularze)**
* **[ARIA i komponenty niestandardowe](#aria-i-komponenty-niestandardowe)**
* **[Multimedia](#multimedia)**
* **[Ruch, czas i animacje](#ruch-czas-i-animacje)**
* **[Spójność i pomoc](#spójność-i-pomoc)**
* **[Narzędzia do testowania](#narzędzia-do-testowania)**
* **[Przydatne linki](#przydatne-linki)**

## Dokument i semantyka

**Dodaj atrybut `lang` do `<html>` oraz do fragmentów strony w innym języku**
* `<html lang="pl">`, `<span lang="en">Good morning</span>`
> * [3.1.1 - Język strony - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/language-of-page)
> * [3.1.2 - Język części - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/language-of-parts)

**Dodaj `dir="rtl"` dla języków pisanych od prawej do lewej (arabski, hebrajski itp.)**
> * [1.3.2 - Zrozumiała kolejność - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence)

**Nadaj każdej stronie unikalny, opisowy `<title>`**
* Wzorzec: `Nazwa strony – Sekcja – Nazwa serwisu`. W aplikacjach SPA aktualizuj `document.title` przy każdej zmianie trasy.
> * [2.4.2 - Tytuł strony - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/page-titled)

**Nie blokuj powiększania w znaczniku `<meta>` viewport**
* Unikaj `maximum-scale=1` i `user-scalable=no`. Używaj `<meta name="viewport" content="width=device-width, initial-scale=1">`.
> * [1.4.4 - Zmiana rozmiaru tekstu - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text)

**Używaj regionów (landmarków): `<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`**
* Dokładnie jeden `<main>` na stronie. Jeśli jest kilka `<nav>`, nazwij je (`aria-label="Główna"`, `aria-label="Okruszki"`).
> * [1.3.1 - Informacje i relacje - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)

**Stosuj logiczną strukturę nagłówków (`<h1>`–`<h6>`) i nie pomijaj poziomów**
* Jeden `<h1>` opisujący stronę to dobra praktyka (nie wymóg WCAG).
* Nie polegaj na `<section>` / `<article>` przy zmianie poziomów nagłówków – algorytm „document outline” nigdy nie został zaimplementowany i usunięto go ze specyfikacji HTML.
* Nigdy nie dobieraj poziomu nagłówka ze względu na wielkość tekstu – wygląd ustaw w CSS.
> * [1.3.1 - Informacje i relacje - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [2.4.6 - Nagłówki i etykiety - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/headings-and-labels)

**Używaj semantycznego HTML do treści i zachowań**
* Przykłady:
  * Akcje to `<button>`, nawigacja to `<a href>`. Nigdy `<div onclick>`.
  * „Wróć na górę” to nawigacja w obrębie strony, więc użyj linku: `<a href="#top">Wróć na górę</a>` (lub `href="#main"`). Działa bez JavaScriptu i przenosi fokus do celu, więc użytkownik klawiatury kontynuuje od tego miejsca. Wskaż konkretny element (np. `<header id="top">`), żeby cel był jednoznaczny.
  * Dane tabelaryczne umieszczaj w `<table>` z `<th scope>` i `<caption>`. Nie używaj tabel do układu strony.
  * Listy to `<ul>` / `<ol>` + `<li>`, a pary termin–opis to `<dl>`.
  * Daty umieszczaj w `<time datetime="2026-11-13">`.
  * Ilustracje i osadzone treści umieszczaj w `<figure>` z `<figcaption>`.
  * `<strong>` / `<em>` oznaczają ważność i emfazę; `<b>` / `<i>` nie niosą znaczenia.
  * Zanim napiszesz własny komponent, użyj natywnego `<dialog>` lub `<details>` / `<summary>`.
> * [1.3.1 - Informacje i relacje - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [4.1.2 - Nazwa, rola, wartość - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Kolejność w DOM musi odpowiadać kolejności wizualnej**
* Uważaj na CSS `order`, `flex-direction: row-reverse`, `grid-area` i pozycjonowanie absolutne.
> * [1.3.2 - Zrozumiała kolejność - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/meaningful-sequence)
> * [2.4.3 - Kolejność fokusu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)

**Dodaj link „Przejdź do treści” jako pierwszy element przyjmujący fokus**
> * [2.4.1 - Możliwość pominięcia bloków - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/bypass-blocks)

**Pisz teksty linków zrozumiałe bez kontekstu (bez „kliknij tutaj”, „czytaj więcej”)**
* Jeśli musisz użyć „Czytaj więcej”, rozszerz nazwę tak, by zaczynała się od widocznego tekstu: `aria-label="Czytaj więcej o cenniku"`.
> * [2.4.4 - Cel łącza (w kontekście) - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/link-purpose-in-context)

**Zapewnij więcej niż jeden sposób dotarcia do strony (nawigacja, wyszukiwarka, mapa strony)**
> * [2.4.5 - Wiele dróg - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/multiple-ways)

## Obrazy i treści nietekstowe

**Dodaj atrybut `alt` do każdego `<img>`**
* Obraz informacyjny: opisz jego znaczenie, nie wygląd.
* Obraz dekoracyjny: `alt=""` (pusty, nigdy nieobecny).
* Obraz w linku lub przycisku: opisz akcję lub cel.
* Złożony obraz (wykres, diagram): krótki `alt` + dłuższy opis obok.
* Inline `<svg>`: `role="img"` + `<title>` (lub `aria-label`); dekoracyjne SVG: `aria-hidden="true"`.
* Przyciski z samą ikoną potrzebują nazwy dostępnej (tekst ukryty wizualnie lub `aria-label`).
> * [1.1.1 - Treść nietekstowa - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/non-text-content)
> * [WAI Images Tutorial – drzewo decyzyjne dla alt](https://www.w3.org/WAI/tutorials/images/decision-tree/)

**Używaj prawdziwego tekstu zamiast obrazów tekstu**
> * [1.4.5 - Obrazy tekstu - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/images-of-text)

## Kolor, kontrast i prezentacja

**Kontrast tekstu wynosi co najmniej 4.5:1 (3:1 dla dużego tekstu: 24px lub 18.66px pogrubiony)**
> * [1.4.3 - Kontrast (minimum) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum)
> * [1.4.6 - Kontrast (podwyższony) - Poziom AAA](https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced) – 7:1 / 4.5:1

**Komponenty interfejsu i istotne grafiki mają kontrast co najmniej 3:1**
* Obramowania pól, ikony, wskaźniki fokusu, linie wykresów, stany checkboxów.
> * [1.4.11 - Kontrast elementów nietekstowych - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast)

**Nie przekazuj informacji wyłącznie kolorem**
* Linki w tekście potrzebują czegoś więcej niż koloru (np. podkreślenia). Pola wymagane i błędy potrzebują tekstu lub ikony, nie tylko czerwieni.
> * [1.4.1 - Użycie koloru - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/use-of-color)

**W instrukcjach nie polegaj wyłącznie na kształcie, kolorze, rozmiarze, położeniu ani dźwięku („kliknij czerwony przycisk po prawej”)**
> * [1.3.3 - Właściwości zmysłowe - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/sensory-characteristics)

**Strona działa przy powiększeniu tekstu do 200% i przy szerokości 320 CSS px (zoom 400%) bez przewijania w poziomie**
* Używaj jednostek względnych (`rem`, `em`, `%`) i responsywnych układów.
> * [1.4.4 - Zmiana rozmiaru tekstu - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/resize-text)
> * [1.4.10 - Dopasowanie do ekranu - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/reflow)

**Nie blokuj orientacji ekranu (pionowej / poziomej)**
> * [1.3.4 - Orientacja - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/orientation)

**Treść nie psuje się, gdy użytkownik zmieni odstępy w tekście**
* Wysokość linii 1.5, odstęp między akapitami 2×, odstęp między literami 0.12em, odstęp między słowami 0.16em. Unikaj stałych wysokości kontenerów z tekstem.
> * [1.4.12 - Odstępy w tekście - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/text-spacing)

**Podpowiedzi i popovery pokazywane po najechaniu lub fokusie można zamknąć (Esc), najechać na nie kursorem i nie znikają same**
> * [1.4.13 - Treść spod kursora lub fokusu - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus)

**Obsługuj tryb wysokiego kontrastu w Windows (forced colors)**
* Testuj z `@media (forced-colors: active)`; nie przekazuj stanu wyłącznie przez `background-color` lub `box-shadow`.

## Klawiatura i fokus

**Wszystko działa z samej klawiatury, bez wymagań czasowych**
* Testuj: `Tab`, `Shift+Tab`, `Enter`, `Spacja`, strzałki, `Esc`.
> * [2.1.1 - Klawiatura - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/keyboard)

**Brak pułapek klawiaturowych – fokus zawsze może opuścić komponent**
> * [2.1.2 - Bez pułapki na klawiaturę - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/no-keyboard-trap)

**Skróty jednoklawiszowe można wyłączyć lub zmienić, albo działają tylko przy fokusie**
> * [2.1.4 - Jednoznakowe skróty klawiaturowe - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/character-key-shortcuts)

**Kolejność tabulacji jest logiczna; nie używaj dodatnich wartości `tabindex`**
* `tabindex="0"` – element niestandardowy przyjmuje fokus; `tabindex="-1"` – fokus tylko ze skryptu.
> * [2.4.3 - Kolejność fokusu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)

**Nigdy nie usuwaj wskaźnika fokusu bez widocznego zamiennika**
* Nie używaj samego `outline: none` / `outline: 0`. Użyj `:focus-visible` z wyraźnym stylem, np. `outline: 2px solid; outline-offset: 2px;`.
> * [2.4.7 - Widoczny fokus - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-visible)
> * [2.4.13 - Wygląd fokusu - Poziom AAA](https://www.w3.org/WAI/WCAG22/Understanding/focus-appearance) (nowe w 2.2)

**Element z fokusem nie jest zasłonięty przez przyklejone nagłówki, banery cookies ani widżety czatu**
* Przy przyklejonym nagłówku użyj `scroll-padding-top`.
> * [2.4.11 - Fokus niezasłonięty (minimum) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/focus-not-obscured-minimum) (nowe w 2.2)

**Otrzymanie fokusu lub zmiana wartości nie powoduje nieoczekiwanej zmiany kontekstu**
* Bez automatycznego wysyłania formularza po zmianie `<select>`, bez otwierania nowych okien przy fokusie.
> * [3.2.1 - Po otrzymaniu fokusu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/on-focus)
> * [3.2.2 - Podczas wprowadzania danych - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/on-input)

**Zarządzaj fokusem w dynamicznych interfejsach**
* Okno modalne: po otwarciu przenieś fokus do środka, trzymaj go tam (albo użyj natywnego `<dialog>` + `showModal()`), zamykaj klawiszem `Esc`, po zamknięciu wróć fokusem do elementu, który je otworzył.
* Zmiana trasy w SPA: przenieś fokus na `<h1>` nowej strony (lub region główny) i zaktualizuj tytuł.
* Usunięcie elementu: przenieś fokus na sensownego sąsiada, nie na `<body>`.
* Użyj atrybutu `inert`, aby wyłączyć treść pod oknem modalnym.
> * [2.4.3 - Kolejność fokusu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/focus-order)
> * [ARIA APG – wzorzec Dialog (Modal)](https://www.w3.org/WAI/ARIA/apg/patterns/dialog-modal/)

## Wskaźnik i dotyk

**Elementy interaktywne mają co najmniej 24×24 CSS px (lub wystarczające odstępy)**
* Zalecany rozmiar to 44×44 px (AAA oraz wytyczne Apple i Google). Linki w treści tekstu są wyjątkiem.
> * [2.5.8 - Rozmiar celu (minimum) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum) (nowe w 2.2)
> * [2.5.5 - Rozmiar celu (podwyższony) - Poziom AAA](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced)

**Każda akcja przeciągania ma alternatywę jednym wskaźnikiem (np. przyciski do zmiany kolejności, kliknięcie w ścieżkę suwaka)**
> * [2.5.7 - Ruchy przeciągania - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/dragging-movements) (nowe w 2.2)

**Gesty wielopunktowe lub po ścieżce (szczypanie, przesunięcie) mają alternatywę jednym dotknięciem**
> * [2.5.1 - Gesty dotykowe - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-gestures)

**Akcje uruchamiają się przy puszczeniu wskaźnika (`click`), nie przy `mousedown` / `touchstart`**
> * [2.5.2 - Rezygnacja ze wskazania - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/pointer-cancellation)

**Nazwa dostępna zawiera widoczny tekst etykiety (najlepiej od niego się zaczyna)**
* Przycisk z napisem „Szukaj” nie może mieć `aria-label="Znajdź produkty"` – użytkownicy sterowania głosem mówią „kliknij Szukaj”.
> * [2.5.3 - Etykieta w nazwie - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/label-in-name)

**Funkcje uruchamiane ruchem urządzenia (potrząśnięcie, przechylenie) mają alternatywę w interfejsie i można je wyłączyć**
> * [2.5.4 - Aktywowanie ruchem - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/motion-actuation)

## Formularze

**Każde pole ma widoczną, programowo powiązaną etykietę `<label>`**
* `<label for="email">` lub pole umieszczone w etykiecie. Placeholder nie jest etykietą.
* Grupuj powiązane kontrolki (radio, checkboxy) w `<fieldset>` + `<legend>`.
* Instrukcje i oczekiwany format podawaj przed polem (powiąż je przez `aria-describedby`).
> * [1.3.1 - Informacje i relacje - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/info-and-relationships)
> * [3.3.2 - Etykiety lub instrukcje - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/labels-or-instructions)

**Używaj atrybutów `autocomplete` w polach z danymi osobowymi**
* `autocomplete="name"`, `"email"`, `"tel"`, `"street-address"`, `"current-password"`, `"one-time-code"` itd.
> * [1.3.5 - Określenie pożądanej wartości - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/identify-input-purpose)

**Opisuj błędy tekstem i podpowiadaj, jak je poprawić**
* Oznacz błędne pola `aria-invalid="true"`, a komunikat powiąż przez `aria-describedby`.
* Po wysłaniu formularza przenieś fokus do podsumowania błędów lub pierwszego błędnego pola.
> * [3.3.1 - Identyfikacja błędu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/error-identification)
> * [3.3.3 - Sugestie korekty błędów - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/error-suggestion)

**Przy zgłoszeniach prawnych, finansowych lub zmieniających dane pozwól na sprawdzenie, poprawienie lub cofnięcie**
> * [3.3.4 - Zapobieganie błędom (prawnym, finansowym, w danych) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/error-prevention-legal-financial-data)

**Nie każ użytkownikom ponownie wpisywać danych, które już podali w tym samym procesie**
* Uzupełnij je automatycznie lub pozwól je wybrać („Adres rozliczeniowy taki sam jak adres dostawy”).
> * [3.3.7 - Zbędne wprowadzanie danych - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/redundant-entry) (nowe w 2.2)

**Logowanie nie wymaga testu poznawczego (zapamiętywania, przepisywania, rozwiązywania zagadek)**
* Pozwól na wklejanie i menedżery haseł w polach hasła i kodu. Obsługuj passkeys, magic linki lub OAuth. Unikaj tekstowych CAPTCHA.
> * [3.3.8 - Dostępne uwierzytelnianie (minimum) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/accessible-authentication-minimum) (nowe w 2.2)

## ARIA i komponenty niestandardowe

**Pierwsza zasada ARIA: jeśli istnieje natywny element HTML, użyj go**
* Brak ARIA jest lepszy niż złe ARIA. Nie nadpisuj natywnej semantyki (`<ul role="navigation">`, `<button role="link">`).
> * [Read Me First – ARIA APG](https://www.w3.org/WAI/ARIA/apg/practices/read-me-first/)
> * [Using ARIA – W3C](https://www.w3.org/TR/using-aria/)

**Niestandardowe widżety udostępniają poprawną nazwę, rolę, stan i wartość**
* Przełącznik: `aria-pressed`; akordeon / disclosure: `aria-expanded` + `aria-controls`; bieżąca strona w nawigacji: `aria-current="page"`.
* Obsługę klawiatury wzoruj na [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/patterns/) (zakładki, menu, combobox itd.).
> * [4.1.2 - Nazwa, rola, wartość - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Nigdy nie dawaj `aria-hidden="true"` elementom przyjmującym fokus ani ich przodkom**
> * [4.1.2 - Nazwa, rola, wartość - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/name-role-value)

**Ogłaszaj komunikaty o stanie bez przenoszenia fokusu**
* Użyj `role="status"` (grzecznie) lub `role="alert"` (natychmiast) dla „Dodano do koszyka”, „Znaleziono 3 wyniki”, błędów formularza. Region live musi istnieć w DOM, zanim zmieni się jego treść.
> * [4.1.3 - Komunikaty o stanie - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/status-messages)

**Mimo wszystko waliduj HTML**
* Kryterium 4.1.1 Parsowanie usunięto w WCAG 2.2, ale zduplikowane `id` nadal psują `<label for>`, `aria-labelledby` i `aria-describedby`.

## Multimedia

**Zapewnij transkrypcję dla nagrań tylko audio oraz alternatywę tekstową lub dźwiękową dla nagrań tylko wideo**
> * [1.2.1 - Tylko audio lub tylko wideo (nagranie) - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/audio-only-and-video-only-prerecorded)

**Zapewnij napisy do nagranych filmów z dźwiękiem**
* Użyj `<track kind="captions">` (WebVTT). Napisy generowane automatycznie trzeba sprawdzić.
> * [1.2.2 - Napisy rozszerzone (nagranie) - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/captions-prerecorded)

**Zapewnij audiodeskrypcję lub pełną alternatywę tekstową dla nagranych filmów**
> * [1.2.3 - Audiodeskrypcja lub alternatywa tekstowa dla mediów (nagranie) - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/audio-description-or-media-alternative-prerecorded)
> * [1.2.5 - Audiodeskrypcja (nagranie) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/audio-description-prerecorded)

**Zapewnij napisy do transmisji audio/wideo na żywo**
> * [1.2.4 - Napisy rozszerzone (na żywo) - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/captions-live)

**Zapewnij tłumaczenie na język migowy dla nagranych materiałów**
> * [1.2.6 - Język migowy (nagranie) - Poziom AAA](https://www.w3.org/WAI/WCAG22/Understanding/sign-language-prerecorded)

**Dźwięk odtwarzany automatycznie dłużej niż 3 sekundy można wstrzymać/zatrzymać lub regulować jego głośność niezależnie od systemu**
* Lepiej: nigdy nie odtwarzaj dźwięku automatycznie.
> * [1.4.2 - Kontrola odtwarzania dźwięku - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/audio-control)

**Odtwarzacze multimediów są dostępne z klawiatury i dla czytników ekranu**
> * [2.1.1 - Klawiatura - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/keyboard)

## Ruch, czas i animacje

**Ruchome, migające, przewijane lub automatycznie aktualizowane treści (karuzele, paski informacyjne) trwające dłużej niż 5 sekund można wstrzymać, zatrzymać lub ukryć**
> * [2.2.2 - Pauza, zatrzymanie, ukrycie - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide)

**Limity czasu (wygasanie sesji) można wyłączyć, dostosować lub wydłużyć**
> * [2.2.1 - Dostosowanie czasu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/timing-adjustable)

**Nic nie miga częściej niż 3 razy na sekundę**
> * [2.3.1 - Trzy błyski lub wartości poniżej progu - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/three-flashes-or-below-threshold)

**Respektuj `prefers-reduced-motion`**
* Wyłącz lub ogranicz paralaksę, duże przejścia i automatycznie odtwarzane animacje.
> * [2.3.3 - Animacja z interakcji - Poziom AAA](https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions)

## Spójność i pomoc

**Nawigacja powtarzana na wielu stronach ma tę samą względną kolejność**
> * [3.2.3 - Spójna nawigacja - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/consistent-navigation)

**Komponenty o tej samej funkcji mają spójne etykiety**
> * [3.2.4 - Spójna identyfikacja - Poziom AA](https://www.w3.org/WAI/WCAG22/Understanding/consistent-identification)

**Mechanizmy pomocy (kontakt, czat, link do FAQ) są w tym samym miejscu na każdej stronie**
> * [3.2.6 - Spójna pomoc - Poziom A](https://www.w3.org/WAI/WCAG22/Understanding/consistent-help) (nowe w 2.2)

## Narzędzia do testowania

**Testy automatyczne**
* [axe DevTools](https://www.deque.com/axe/devtools/) / [axe-core](https://github.com/dequelabs/axe-core) (także w CI: `@axe-core/playwright`, `jest-axe`, `cypress-axe`)
* [WAVE](https://wave.webaim.org/)
* [Lighthouse](https://developer.chrome.com/docs/lighthouse/accessibility/scoring)
* [Accessibility Insights](https://accessibilityinsights.io/) – zawiera prowadzony test ręczny „Assessment”
* [eslint-plugin-jsx-a11y](https://github.com/jsx-eslint/eslint-plugin-jsx-a11y) dla Reacta

**Narzędzia deweloperskie przeglądarek**
* Chrome / Edge: panel Accessibility i pełne drzewo dostępności, problemy z kontrastem w CSS Overview, emulacja zaburzeń widzenia, `prefers-reduced-motion` i `forced-colors`
* Firefox: Accessibility Inspector (nakładka kolejności tabulacji, sprawdzanie kontrastu i klawiatury)

**Czytniki ekranu**
* [NVDA](https://www.nvaccess.org/) (Windows, darmowy) – testuj z Firefoksem lub Chrome
* JAWS (Windows, komercyjny)
* VoiceOver (macOS / iOS, wbudowany) – testuj z Safari
* TalkBack (Android, wbudowany) – testuj z Chrome
* Narrator (Windows, wbudowany)

**Sprawdzanie kontrastu**
* [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
* [Colour Contrast Analyser (TPGi)](https://www.tpgi.com/color-contrast-checker/)

## Przydatne linki

* [WCAG 2.2 – How to Meet WCAG (Quick Reference)](https://www.w3.org/WAI/WCAG22/quickref/)
* [Co nowego w WCAG 2.2](https://www.w3.org/WAI/standards-guidelines/wcag/new-in-22/)
* [ARIA Authoring Practices Guide (APG)](https://www.w3.org/WAI/ARIA/apg/)
* [WAI Easy Checks – pierwszy przegląd dostępności](https://www.w3.org/WAI/test-evaluate/easy-checks/)
* [WebAIM](https://webaim.org/) i raport [WebAIM Million](https://webaim.org/projects/million/)
* [The A11Y Project Checklist](https://www.a11yproject.com/checklist/)
* [MDN – Accessibility](https://developer.mozilla.org/en-US/docs/Web/Accessibility)
* [GOV.UK Design System](https://design-system.service.gov.uk/) – dobrze przetestowane dostępne komponenty
* [Inclusive Components](https://inclusive-components.design/)
* [HTML5 Accessibility](https://www.html5accessibility.com/)
* [BBC Accessibility News and You](https://bbc.github.io/accessibility-news-and-you/)
* [Europejski Akt o Dostępności](https://commission.europa.eu/strategy-and-policy/policies/justice-and-fundamental-rights/disability/union-equality-strategy-rights-persons-disabilities-2021-2030/european-accessibility-act_en) – obowiązuje od 28 czerwca 2025
* [WCAG 3.0 (Working Draft)](https://www.w3.org/TR/wcag-3.0/) – to jeszcze nie standard, warto śledzić
