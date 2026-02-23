---
layout: default
title: Use cases
nav_order: 6
permalink: /use-cases.html
---

# Use Cases
{: .no_toc }

This section provides practical implementation scenarios for the Autosuggest JS SDK, along with configuration examples and interactive demonstrations. Each use case highlights a specific feature or behavior and includes the relevant setup required to achieve it.

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Use Case 1: Focused Autosuggest with Initial Request and Trending Searches

This use case demonstrates how to configure the new Autosuggest JS SDK to provide a discovery-first search experience by displaying suggestions immediately when the search input gains focus.

By enabling `initialRequest` and `trendingSearches`, the SDK fetches and displays popular search terms even before the user begins typing. This approach improves engagement and supports product discovery by highlighting trending queries.

![Use case 1: Trending searches on focus — suggestions appear on focus, then update as you type]({{ 'assets/images/demo-1.gif' | relative_url }})

---

#### Configuration Overview

This behavior is achieved using the following API configuration options:

- **`initialRequest: true`**  
  Triggers an API request as soon as the search input receives focus, without requiring user input.

- **`trendingSearches`**  
  Enables trending search terms in the autosuggest response and allows configuration of the number of results to display.

---

#### Implementation Example

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

## Use Case 2: Initial Request Enabled with Trending Searches Disabled

This use case demonstrates how to configure the Autosuggest JS SDK to trigger suggestions on input focus while excluding trending searches from the response.

By enabling `initialRequest` and disabling `trendingSearches`, the SDK retrieves suggestions immediately when the search input gains focus, but limits the response to configured suggestion types such as top queries, keyword suggestions, in-fields, or products.

![Use case 2: Intial Request on focus — suggestions appear on focus, then update as you type]({{ 'assets/images/demo-2.gif' | relative_url }})

---

### Configuration Overview

This behavior is achieved using the following API configuration options:

- **`initialRequest: true`**  
  Initiates an API request when the search input receives focus, without requiring user input.

- **`trendingSearches: false`**  
  Disables trending search terms in the autosuggest response.

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
    trendingSearches: { count: 0 },
    topQueries: { count: 5 },
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
