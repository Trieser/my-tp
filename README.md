# Company Profile

> A company profile website built with [Vite](https://github.com/vitejs/vite) and [Tailwind CSS](http://tailwindcss.com/)

## Features
- Fast development with Vite
- Responsive design using Tailwind CSS
- Modern UI components

## Tailwind UI Integration
This project uses Tailwind CSS plugins for enhanced UI components:

1. Install first-party plugins:
```sh
npm install --save-dev @tailwindcss/forms @tailwindcss/typography @tailwindcss/aspect-ratio
```

2. These plugins are already configured in `tailwind.config.js`:
```js
// tailwind.config.js
module.exports = {
  // ...
  plugins: [
    require('@tailwindcss/forms'),
    require('@tailwindcss/typography'),
    require('@tailwindcss/aspect-ratio'),
  ],
}
```

## Installation
```sh
npm install
```

## Development
```sh
npm run dev
```

## Build
```sh
npm run build
```

## Preview Production Build
```sh
npm run preview
```