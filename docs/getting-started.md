---
layout: default
title: Getting Started
nav_order: 2
---

## Getting Started

This guide explains how to install and initialize the Autosuggest JS SDK using the npm package.

---

### Prerequisites

Before installing and integrating the Autosuggest JS SDK, ensure the following requirements are met:

#### Environment Requirements

- Node.js (LTS version recommended)
- npm or Yarn package manager
- A JavaScript project setup (e.g., React, Vue, Angular, or a bundler such as Webpack or Vite)

#### Unbxd Account Setup

1. Create and configure a site in the Unbxd Self Serve Dashboard.
2. Upload your product feed.
3. Configure relevancy settings.
4. Retrieve your **Site Key** and **API Key** from the dashboard.

These credentials are required to authenticate and fetch autosuggest results.

---

### Install via npm

Install the Autosuggest JS SDK package:

```js
npm install @unbxd-ui/autosuggest-js-sdk
```

or using Yarn:

```js
yarn add @unbxd-ui/autosuggest-js-sdk
```

---

### Import the SDK

After installation, import the Autosuggest class into your project:

```javascript
import { Autosuggest } from "@unbxd-ui/autosuggest-js-sdk";
```

---

### Initialize Autosuggest

Instantiate the Autosuggest object and bind it to your search input element:

```javascript
const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",

  inputBoxConfigs: {
    searchInput: ".search-input",
    debounceDelay: 300,
    minChars: 2,
  },

  apiConfigs: {...},

  suggestionBoxConfigs: {...},
});
```