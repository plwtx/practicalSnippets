## My Code Snippets
Just some usefull code snippets i use in my projects. I made this repository to make my daily work easy and share it with my friends when necessary. Feel free to use it as you wish. Snippets are short, reusable code blocks that can be used on projects.
Please keep in mind that these are the snippets i use and it can be a bad practice. As time goes and as i learn more about web development i will come back and fix stuff that i did wrong.

##### Thank you for your understanding.
---
### Contents
#### 1.0 - [Initialization](#10-initialization)
##### 1.1 - Installation of Vite
##### 1.2 - Installation of Tailwind
#### 2.0 - [Basic code snippets / blocks](#20-basic-code-snippets)
##### 2.1 - Div with background image optimnized for mobile:
##### 2.2 - Custom Scroll Wheel + Tailwind + Font Import
#### 3.0 - [Et cetera](#30-et-cetera)
##### 3.1 - Adding TypeScript to existing Vite application

---



## 1.0 Initialization

### Vite with React.js or React.ts template:
```
npm create vite@latest name -- --template react
```
```
cd name
```

### Tailwind (OLD / deprecated):
```
npm install tailwindcss @tailwindcss/vite
```
```
npx tailwindcss init -p
```

###### tailwind.config.js:
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
###### index.css:
```
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Prettier with Tailwind:

```
npm install -D prettier prettier-plugin-tailwindcss
```
##### .prettierrc:
```
{
  "plugins": ["prettier-plugin-tailwindcss"]
}
```


### i18n React Localization:
```
npm install react-i18next i18next
```

##### i18n.ts:

```
import i18n from "i18next";
import { initReactI18next, Translation } from "react-i18next";

i18n.use(initReactI18next).init({
  // {t("word")}
  // debug: true,
  fallbackLng: "en",
  resources: {
    en: {
      translation: {
        word: "Word",
      },
    },
    zh: {
      translation: {
        word: "Word",
      },
    },
  },
});
```


Navigation language setting (used only once per app load)
Inside higher level component (usually app.jsx):
```
import "./i18n";
import { useEffect } from "react";
import { useTranslation } from "react-i18next";
```
```
useEffect(() => {
  i18n.changeLanguage(navigator.language);
}, []);
```

Other components / Language set button:
```
import "../i18n";
import { useTranslation } from "react-i18next";
```
```
  const { t, i18n } = useTranslation();
  const [chinese, setChinese] = useState(false);
  const changeLanguageEN = (lang) => {
    i18n.changeLanguage("en");
    setChinese(false);
  };

  const changeLanguageCN = (lang) => {
    i18n.changeLanguage("zh");
    setChinese(true);
  };
```
Button:
```
onClick={changeLanguageCN}
```

Language specified content (other necessary parameters given above):
```
 <div className={`h-6 w-[0.1rem] ${chinese ? "invisible absolute" : ""} ${scrolled ? "bg-black" : "bg-white"}`}></div>
```


### Is window scrolled
```
 const [scrolled, setScrolled] = useState(false);

 const handleScroll = () => {
    if (window.scrollY > 0) {
      setScrolled(true);
    } else {
      setScrolled(false);
    }
  };

  useEffect(() => {
    window.addEventListener("scroll", handleScroll);
    return () => {
      window.removeEventListener("scroll", handleScroll);
    };
  }, []);

```


## 2.0 Basic code snippets

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

### Additional CSS ***on top of Tailwind (main.css / index.css):***
```
@layer utilities {

   .clipp{

       clip-path: polygon(0 0, 100% 0, 100% 100%, 0 calc(100% - 6vw));

   }

}
```
---
### Show or hide component depending on state:
```
  const [loading, setLoading] = useState(false);

  const handleLoading = () => {
    setLoading(false);
    setTimeout(() => {
      setLoading(true);
    }, 2500);
  };

  useEffect(() => {
    setLoading(true);
    setTimeout(() => {
      setLoading(false);
    }, 2500);
  }, []);



{loading ? (
        <Loading />
      ) : ( <div> <div/> )}

{loading ? ( ) : ( )}

{/* Button version:  */}

<button
  onClick={() => { handleLoading }}
>
</button>
```
---
### OnClick show component:

```
<button
  onClick={() => {
    someSound.play(); 
    setCopiedMsg(true);
    setTimeout(() => { 
      setCopiedMsg(false);
    }, 1000);
  }}
>
</button>
```
---

## Set theme according to user preference:


```
  // Get initial theme:
  const getInitialTheme = () => {
    // Local storage preference:
    const storedTheme = localStorage.getItem("theme");
    if (storedTheme) return storedTheme;
    // Browser preference:
    const prefersDark = window.matchMedia(
      "(prefers-color-scheme: dark)",
    ).matches;
    return prefersDark ? "dark" : "light";
  };

  const [theme, setTheme] = useState(getInitialTheme());
  useEffect(() => {
    document.documentElement.className = theme;
    localStorage.setItem("theme", theme);
  }, [theme]);

  useEffect(() => {
    const handleChange = (e) => {
      setTheme(e.matches ? "dark" : "light");
    };

    // Listener for changes in the theme preference
    const mediaQuery = window.matchMedia("(prefers-color-scheme: dark)");
    mediaQuery.addEventListener("change", handleChange);

    // Cleanup event listener on unmount
    return () => {
      mediaQuery.removeEventListener("change", handleChange);
    };
  }, []);

  const toggleTheme = () => {
    setTheme((prevTheme) => (prevTheme === "light" ? "dark" : "light"));
  };
```

##### Theme change button:
```
        {/* Theme change button: */}
          <div className="group z-50 m-3 flex justify-start gap-3">
            <div className="absolute -right-12 -top-20 z-0 h-20 w-72 rounded-full bg-gray-300 opacity-0 blur-3xl transition-all duration-1000 group-hover:opacity-100 dark:bg-blux"></div>
            <p className="z-10 translate-x-20 font-AfacadFlux text-base tracking-widest text-gray-700 opacity-0 blur-sm transition-all duration-500 group-hover:translate-x-0 group-hover:tracking-normal group-hover:opacity-100 group-hover:blur-0 dark:text-gray-300">
              Click to toggle dark mode{" "}
              <span className="pl-1 font-sans font-black text-blux">
                &rarr;
              </span>
            </p>

            <button
              onClick={toggleTheme}
              class="z-30 h-6 w-6 cursor-pointer transition-all duration-500 group-hover:rotate-45"
            >
              <svg
                class="block fill-gray-300 hover:fill-blux dark:hidden"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"></path>
              </svg>
              <svg
                class="hidden fill-gray-500 hover:fill-blux dark:block"
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path
                  d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
                  fill-rule="evenodd"
                  clip-rule="evenodd"
                ></path>
              </svg>
            </button>
          </div>
```
##### tailwind.config.js

```
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  darkMode: "selector",
```

---

## 3.0 Et cetera

### Adding TypeScript to existing Vite application:

Credits to: [NetYogi](https://stackoverflow.com/users/7157170/netyogi)


Firstly, install TypeScript and types for react and react-dom:
```
npm install -D typescript @types/react @types/react-dom
```

Next, rename the vite.config.js file to vite.config.ts.
Thirdly, configure your tsconfig.json as follows,
```
{
  "compilerOptions": {
    "target": "ESNext",
    "useDefineForClassFields": true,
    "lib": ["DOM", "DOM.Iterable", "ESNext"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": false,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": ["src"],
  "references": [{ "path": "./tsconfig.node.json" }]
}
```
,and a tsconfig.node.json,
```
{
  "compilerOptions": {
    "composite": true,
    "module": "ESNext",
    "moduleResolution": "Node",
    "allowSyntheticDefaultImports": true
  },
  "include": ["vite.config.ts"]
}
```
Next, create a file named vite-env.d.ts inside your src/ folder and copy and paste the following (with the three slashes at the beginning):
```
/// <reference types="vite/client" />
```
This creates a type file for the vite client.
Lastly, in your index.html, change the name of your index.jsx to index.tsx as,
```
<script type="module" src="/src/index.tsx"></script>
```
TypeScript should now work on your Vite React project.



