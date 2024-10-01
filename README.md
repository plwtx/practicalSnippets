## Usefull Code Snippets
Just some usefull code snippets i use in my projects. I made this repository to make my daily work easy and share it with my friends when necessary. Feel free to use it as you wish. Snippets are short, reusable code blocks that can be used on projects.

# I
initialization

### Vite with React.js or React.ts template:
```
npm create vite@latest name -- --template react / react-ts
cd name
```

### Tailwind:
```
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

### tailwind.config.js:
```
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```
```
// index.css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Prettier with Tailwind:

```
npm install -D prettier prettier-plugin-tailwindcss
```
```
// .prettierrc
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```

# II
Basic code snippets.

---

### Div with background image optimnized for mobile:
```
// Background:
    <div
      id="Home"
      className="w-dvh relative h-dvh snap-start overflow-hidden bg-cover bg-center object-cover md:bg-fixed"
      style={{
        backgroundImage: `url(${background})`,
      }}
    >
    {/* Content Here */}
    </div>
```

---

### Custom Scroll Wheel + Tailwind + Font Import:
```
@import url("https://fonts.googleapis.com/css2?family=Imbue:opsz,wght@10..100,100..900&family=Roboto+Condensed:ital,wght@0,100..900;1,100..900&family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap");
@tailwind base;
@tailwind components;
@tailwind utilities;

::-webkit-scrollbar {
  width: 3px;
}

::-webkit-scrollbar-track {
  background: rgb(37, 37, 37); /* Track color */
}

::-webkit-scrollbar-thumb {
  background-color: #343c79; /* Thumb color */
  border-radius: 0px;
}

```
---

### vite.config.js | Network run
Configurations to run server on network with "3333" port by default.
```
import { defineConfig } from "vite";
import react from "@vitejs/plugin-react";
import dns from "node:dns";

dns.setDefaultResultOrder("verbatim");

// https://vitejs.dev/config/
export default defineConfig({
  server: {
    port: "3333",
    host: true,
  },
  plugins: [react()],
});

```
---

### Additional CSS ***on top of Tailwind.***
```
@layer utilities {

   .clipp{

       clip-path: polygon(0 0, 100% 0, 100% 100%, 0 calc(100% - 6vw));

   }

}
```
