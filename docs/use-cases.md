---
layout: default
title: Use cases
nav_order: 6
permalink: /use-cases.html
---

# Use Cases

This section provides practical implementation scenarios for the Autosuggest JS SDK, along with configuration examples and interactive demonstrations. Each use case highlights a specific feature or behavior and includes the relevant setup required to achieve it.

---

## Use Case 1: Discovery-Focused Autosuggest with Initial Request and Trending Searches

This use case demonstrates how to configure the Autosuggest JS SDK to provide a discovery-first search experience by displaying suggestions immediately when the search input gains focus.

By enabling `initialRequest` and `trendingSearches`, the SDK fetches and displays popular search terms even before the user begins typing. This approach improves engagement and supports product discovery by highlighting trending queries.

![Use case 1: Trending searches on focus — suggestions appear on focus, then update as you type]({{ 'assets/images/demo-1.gif' | relative_url }})

---

### Configuration Overview

This behavior is achieved using the following API configuration options:

- **`initialRequest: true`**  
  Triggers an API request as soon as the search input receives focus, without requiring user input.

- **`trendingSearches`**  
  Enables trending search terms in the autosuggest response and allows configuration of the number of results to display.

---

### Implementation Example

```javascript
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

---

### Expected Behavior

With this configuration:

- The autosuggest panel opens immediately when the search input gains focus.
- Trending search terms are displayed before the user enters any query.
- As the user types, the suggestions dynamically update based on the input.
- Multiple suggestion types (top queries, keyword suggestions, products, etc.) are returned according to the configured counts.

---

### Recommended Use Cases

This configuration is suitable for:

- E-commerce storefronts prioritizing product discovery
- Sites that want to surface trending or high-performing queries
- Experiences where engagement should begin immediately on search interaction

