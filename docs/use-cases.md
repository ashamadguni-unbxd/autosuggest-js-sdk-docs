---
layout: default
title: Use cases
nav_order: 6
permalink: /use-cases.html
---

# Use cases

This page shows real-world use cases for the Autosuggest SDK with configuration examples and demos.

---

## Use case 1: Discovery on focus with trending searches

Show suggestions as soon as the user focuses the search box—**before** they type—using **trending searches**. This is useful for discovery: users see what’s popular or trending right away.

**Configuration used:**

- **`apiConfigs.initialRequest`** — Set to `true` so the SDK fetches suggestions when the input is focused (e.g. on load or on first focus).
- **`apiConfigs.trendingSearches`** — Configure the number of trending search terms to display (e.g. `count: 8`).

### Demo

![Use case 1: Trending searches on focus — suggestions appear on focus, then update as you type]({{ 'assets/images/demo-1.gif' | relative_url }})

### Code sample

```js
const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",

  inputBoxConfigs: {
    searchInput: ".search-input",
    debounceDelay: 300,
    minChars: 2,
  },

  suggestionBoxConfigs: {
    containerTag: "div",
    attributes: {
      class: ["unbxd-autosuggest-box"],
    },
    template: MyCustomTemplate,
  },

  apiConfigs: {
    apiEndpoint: "https://search.unbxd.io",
    initialRequest: true,
    trendingSearches: { count: 8 },
    topQueries: { count: 4 },
    keywordSuggestions: { count: 3 },
    inFields: { count: 2 },
    popularProducts: { count: 2, fields: [] },
    promotedSuggestions: { count: 2 },
  },

  onEvent: ({ eventType }) => {
    console.log("Autosuggest event:", eventType);
  },
});
```

**What this does:**

- When the user **focuses** the search input, the SDK immediately requests suggestions (no typing required).
- **Trending searches** are emphasized (`count: 8`); **top queries** and other types can still appear.
- Adjust `trendingSearches.count` and other `apiConfigs` to match your UI and performance needs.

For more options, see [Configuration](configurations.html).
