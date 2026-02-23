---
layout: default
title: Getting Started
# nav_order: 3
---

# Getting Started
{: .no_toc }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Prerequisite

Before integrating the new Autosuggest SDK, ensure the following:

- You have completed the **self-serve FTU flow**
- Your feed is successfully uploaded and indexed
- Required fields such as **title, imageUrl, price, categoryPath** are mapped correctly

> **Note:**  
> The configuration attributes shown in this document are based on a **sample apparel feed**.  
> These attributes **will vary depending on the site and feed schema** being used.

---

## Integration Instructions

Follow these steps to integrate the new Autosuggest SDK into your site.

### Configure Site Credentials

Update the `siteKey` and `apiKey` with values specific to your account.

```js
siteKey: "<<site key>>",
apiKey: "<<api key>>"
```

### Attach the New Autosuggest SDK to Search Input

Provide a valid CSS selector for the search input via `inputBoxConfigs.searchInput`. This is mandatory for the new Autosuggest SDK to initialize. See [Configuration](configuration.html#inputboxconfigs) for all options.

### Customize API Configuration

Control what type of suggestions appear and how many results are fetched.

* In-field suggestions
* Popular products
* Keyword suggestions
* Top queries
* Promoted suggestions

These should be adjusted based on UI space and performance needs.

### Handle Errors Gracefully

Configure the **onEvent** callback in production to log or track errors. See [Configuration](configuration.html#onevent).

---

## Complete Example
```js
const autosuggest = new Autosuggest({
    siteKey: "ss-unbxd-aus-demo-fashion831421736321881",
    apiKey: "1ccbb7fcb0faf770d1c228be80ba16d9",

    inputBoxConfigs: {
        searchInput: ".search-input",
        debounceDelay: 500,
        minChars: 3,
    },

    suggestionBoxConfigs: {
        containerTag: "div",
        attributes: {
            class: ["search-input", "unbxd-autosuggest-box"],
            "data-testid": "search-input",
            id: "search-id"
        },
        template: null, // or a custom template function
    },

    apiConfigs: {
        apiEndpoint: "https://search.unbxd.io",
        initialRequest: false,
        inFields: { count: 2 },
        popularProducts: { count: 3, fields: [] },
        keywordSuggestions: { count: 2 },
        topQueries: { count: 2 },
        promotedSuggestions: { count: 2 },
        trendingSearches: { count: 5 },
    },

    onEvent: ({ eventType }) => {
        console.log("Autosuggest event:", eventType);
    }
});
```

---

## Default Configuration
If no configuration is provided, the SDK falls back to the defaults defined in `src/constants/options.js`. See [Configuration](configuration.html) for the full reference.

```js
{
    siteKey: "",
    apiKey: "",
    inputBoxConfigs: {
        searchInput: null,
        debounceDelay: 0,
        minChars: 3,
    },
    suggestionBoxConfigs: {
        containerTag: "div",
        attributes: {},
        template: null,
    },
    apiConfigs: {
        apiEndpoint: "https://search.unbxd.io",
        initialRequest: false,
        inFields: { count: 2 },
        popularProducts: { count: 3, fields: [] },
        keywordSuggestions: { count: 2 },
        topQueries: { count: 2 },
        promotedSuggestions: { count: 2 },
        trendingSearches: { count: 5 },
    },
    onEvent: function ({ eventType }) { ... }
}
```
