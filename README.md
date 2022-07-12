# Feature oriented Next.js
This proposes a truly feature-oriented structure to Next.js.

## 🪂 Looking for an module?
- [devxoul/next-route-map](https://github.com/devxoul/next-route-map)

## 🔋 Included
- [TypeScript](https://github.com/microsoft/TypeScript)
- [styled-components](https://github.com/styled-components/styled-components)
- [styled-normalize](https://github.com/sergeysova/styled-normalize): normalize.css for styled-components

## Structure

### 👩‍❤️‍👨 Tightly coupled, Feature-oriented

### ❌ As-is
```text
.
├── components/ 1️⃣
│   ├── Home/
│   │   ├── Button.tsx
│   │   ├── Header.tsx
│   │   ├── FirstSection.tsx
│   │   └── SecondSection.tsx
│   └── Profile/
├── utils/
│   ├── Home/
│   └── Profile/
├── public/
└── pages/ 2️⃣
    ├── index.tsx # Home
    └── profile.tsx # Profile
```

The most commonly used structure for Next.js is like the above; Each *page component* goes into the `pages` folder, with the intended route as their filename. *Uncommon code fragments* used only by specific pages, like components and utilities, are grouped inside each folder named after the page component. So the pages and their components were bound to be **loosely coupled.**

Because pages are strongly dependent on components of the same interest, this makes it difficult to find the fragments used in the page - or identify related changes inside your domain.

### ✅ To-be
```
.
├── public/
└── src/
    ├── domains/
    │   ├── Home/ 1️⃣
    │   │   ├── components/
    │   │   ├── utils/
    │   │   ├── hooks/
    │   │   └── HomePage.tsx
    │   └── Profile/
    └── pages/ ⭐️
        ├── index.tsx
        └── profile.tsx
```

How's this? 🙋

**The pages are separated by each domain and tightly coupled to the components it consumes.**

```tsx
// index.tsx
import { HomePage } from 'src/domains/Home/HomePage'

const Home = () => <HomePage />

export default Home
```

In this structure, the files inside the original `pages` folder have only one lightweight role: Importing *'real' page components* from the domain folder and *linking them to the desired path.*

This way we can...

### 🔗 Link multiple routes to one page
You can easily link multiple routes to one page. You can just import the page with another route and that's it.

```tsx
// index.tsx
import { HomePage } from 'src/domains/Home/HomePage'

const Index = () => <HomePage />

export default Index
```

```tsx
// home.tsx
import { HomePage } from 'src/domains/Home/HomePage'

const Home = () => <HomePage />

export default Home
```

### Write tests next each page
TBD
