# expense-tracker

A simple web app for tracking income and expenses.

The project is structured as a Vue.js app with the following components:

- App: The main app component that renders the balance, income period, transaction form, and transaction history components.
- Assets: Contains the logo and CSS stylesheet for the app.
- Components: The subcomponents that make up the app, including the balance, income period, transaction form, and transaction history components.

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

```
expense-tracker
├─ .gitignore
├─ README.md
├─ jsconfig.json
├─ package-lock.json
├─ package.json
├─ public
│  ├─ favicon.ico
│  ├─ img
│  │  └─ icons
│  │     ├─ android-chrome-192x192.png
│  │     ├─ android-chrome-512x512.png
│  │     ├─ android-chrome-maskable-192x192.png
│  │     ├─ android-chrome-maskable-512x512.png
│  │     ├─ apple-touch-icon-120x120.png
│  │     ├─ apple-touch-icon-152x152.png
│  │     ├─ apple-touch-icon-180x180.png
│  │     ├─ apple-touch-icon-60x60.png
│  │     ├─ apple-touch-icon-76x76.png
│  │     ├─ apple-touch-icon.png
│  │     ├─ favicon-16x16.png
│  │     ├─ favicon-32x32.png
│  │     ├─ msapplication-icon-144x144.png
│  │     ├─ mstile-150x150.png
│  │     └─ safari-pinned-tab.svg
│  ├─ index.html
│  └─ robots.txt
└─ src
   ├─ App.vue
   ├─ assets
   │  ├─ logo.png
   │  └─ style.css
   ├─ components
   │  ├─ Balance.vue
   │  ├─ IncomeExpense.vue
   │  ├─ IncomePeriod.vue
   │  ├─ TransactionForm.vue
   │  └─ TransactionHistory.vue
   ├─ main.js
   └─ registerServiceWorker.js

```