# Trello-clon

This template should help get you started developing with Vue 3 in Vite.

## Recommended IDE Setup

[VSCode](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur).

## Type Support for `.vue` Imports in TS

TypeScript cannot handle type information for `.vue` imports by default, so we replace the `tsc` CLI with `vue-tsc` for type checking. In editors, we need [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) to make the TypeScript language service aware of `.vue` types.

## Customize configuration

See [Vite Configuration Reference](https://vite.dev/config/).

## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Type-Check, Compile and Minify for Production

```sh
npm run build
```

### Lint with [ESLint](https://eslint.org/)

```sh
npm run lint
```



# Instalación de Tailwincss

1º: npm install -D tailwindcss postcss autoprefixer

2º: npx tailwindcss init -p
### Si funciona el 2º:


3º: si se ha creado el archivo 'tailwind.config.js':

Lo modificamos a:
// tailwind.config.js
/** @type {import('tailwindcss').Config} */
export default {
  // Make changes below
  content: ["./index.html", "./src/**/*.{vue,js,ts,jsx,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};

4º: En el 'main.css':

@tailwind base;
@tailwind components;
@tailwind utilities;


### Si no funciona el 2º:

3º: Crear archivo: tailwindcss.config.js (igual que el de arriba).

4º: En 'vite.config.ts': 

import tailwindcss from '@tailwindcss/vite'
 y     tailwindcss()

5º: En 'package.json':

En dependencies:  "@tailwindcss/vite": "^4.1.4"
En devDependencies:     "tailwindcss": "^4.1.6",

6º: En 'index.html': 
  
   Dentro del <head>   <link href="/src/assets/main.css" rel="stylesheet">




