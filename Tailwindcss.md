
### Extending Themes. 

Extending `tailwind.config.js` to create our own themes, here we are adding our own colours to tailwind. extend will make sure that default tailwind theming properties are extending and not replaced. for more information on this refer to [theming with tailwind](https://tailwindcss.com/docs/theme)

```typescript
const colors = require('tailwindcss/colors')

module.exports = {
  content: ['./src/**/*.{js,jsx}', './public/index.html'],
  darkMode: 'class', // class, 'media' or boolean
  theme: {
    extend: {
      colors: {
        gray: {
          900: '#202225',
          800: '#2f3136',
          700: '#36393f',
          600: '#4f545c',
          400: '#d4d7dc',
          300: '#e3e5e8',
          200: '#ebedef',
          100: '#f2f3f5',
        },
      },
      spacing: {
        88: '22rem',
      },
    },
  },
  plugins: [],
};
```

I am also using `darkMode: 'class'` here to add __darkmode__ to our app with tailwind, with this tailwind will add dark value to any markup that is child to a element that has dark class on it. we can use libraries like __next-theme__ for this functionality. next theme will help us to add a global dark class on root html element. For more information on this follow this article [next-themes with tailwind](https://dev.to/mnamesujit/implementing-dark-and-light-themes-in-nextjs-13-with-tailwind-css-57l5)

### Extending tailwindcss with more functionality

Our `global.css` file will look something like this.

```css
@import-normalize;
@tailwind base;
@tailwind components;
@tailwind utilities;

@layer components {
  .sidebar-icon {
    @apply relative flex items-center justify-center 
    h-12 w-12 mt-2 mb-2 mx-auto  
    bg-gray-400 hover:bg-green-600 dark:bg-gray-800 
    text-green-500 hover:text-white
    hover:rounded-xl rounded-3xl
    transition-all duration-300 ease-linear
    cursor-pointer shadow-lg;
  }
}
```

In above example we are creating a custom class of our own called `sidebar-icon` that can letter be used on elements like this.

Here I am also using tailwind __groups__. Tailwind __groups__ is a clever way of adding css to child when state of the parent changes 🤩 
```tsx
<div className="sidebar-icon group">
    {icon}
    <span class="sidebar-tooltip group-hover:scale-100">
      {text}
    </span>
</div>
```

For tailwind css cheatsheet refer to this class : [tailwind cheatsheet](https://tailwindcomponents.com/cheatsheet/)

---
### tricks

1. divide
2. snap
3. sr-only
4. accent-color
5. outline and carret
6. 