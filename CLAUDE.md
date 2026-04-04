# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static HTML website for artist **Juan Luis Landaeta** (juanluislandaeta.com). No build step is required to view the site — open any `.html` file directly in a browser or serve it with any static file server.

## Build / Asset Pipeline

The only build tooling is a Gulp task for converting images to WebP format:

```bash
# Install dependencies (first time only)
npm install

# Convert images in img/ to WebP → outputs to dist/images/
npx gulp
```

Source images live in `img/`. The pipeline converts `.jpg`, `.jpeg`, `.png`, `.svg`, `.gif` to `.webp` and places them in `dist/images/`. All HTML files reference images from `dist/images/`.

## Architecture

- **Layout pattern**: Every page uses a two-panel flex layout — a fixed left nav (`.nav`, 20vw) and a scrollable right content area (`.main` or `.artwork`). Mobile breakpoint at 600px collapses the nav and hides decorative panels.
- **Navigation**: Static `<ul>` inside `.nav` on every page — there is no shared include or template system. Nav must be updated manually across all HTML files.
- **CSS**: `css/css-test.css` is the primary stylesheet (resets + layout + all component styles). `css/style.css` adds grid/column utilities. `css/menu.css` handles the mobile overlay menu. These are loaded per-page via `<link>` tags.
- **JavaScript**: `js/jquery-3.4.0.min.js` + `js/jquery.fancybox.min.js` for lightbox galleries. `js/menu.js` handles the mobile hamburger overlay (`openNav`/`closeNav`). `js/slide.js` for any slideshow pages.
- **Catalogues**: PDF files with `.jpg` cover thumbnails stored in `catalogues/`. Referenced directly from `catalogues.html`.
- **Google Analytics**: GA4 tag (`G-VBM4TZ75X1`) is included inline at the top of every page.

## Conventions

- Images must be in WebP format (`dist/images/*.webp`) before being referenced in HTML.
- The `<hea>` tag (not `<head>`) appears in several files — this is an existing quirk, not a typo to fix unless explicitly asked.
- The site is bilingual (English/Spanish); OG locale tags include both `en_US` and `es_ES`.
