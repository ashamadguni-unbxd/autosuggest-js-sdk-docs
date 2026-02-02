---
layout: default
title: Getting Started
nav_order: 3
---

# Getting Started
{: .no_toc }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc_levels: 2}

---

## Prerequisite

Before integrating the Autosuggest SDK, ensure the following:

- You have completed the **self-serve FTU flow**
- Your feed is successfully uploaded and indexed
- Required fields such as **title, imageUrl, price, categoryPath** are mapped correctly

> **Note:**  
> The configuration attributes shown in this document are based on a **sample apparel feed**.  
> These attributes **will vary depending on the site and feed schema** being used.

---

## Integration Instructions

Follow these steps to integrate Autosuggest into your site.

### 1\. Configure Site Credentials

Update the `siteKey` and `apiKey` with values specific to your account.

```js
siteKey: "<<site key>>",
apiKey: "<<api key>>"
```

### 2\. Attach Autosuggest to Search Input

Provide a valid CSS selector or DOM element for the search input field.

```js
searchInput: ".search-input"
```
This is mandatory for Autosuggest to initialize.

### 3\. Customize API Configuration

Control what type of suggestions appear and how many results are fetched.

* In-field suggestions
* Popular products
* Keyword suggestions
* Top queries
* Promoted suggestions

These should be adjusted based on UI space and performance needs.

### 4\. Handle Errors Gracefully

Always configure an `onError` callback in production environments to log or track errors.

---

## Complete Example
```js
const autosuggest = new Autosuggest({
    // Basic Configuration
    siteKey: "ss-unbxd-aus-demo-fashion831421736321881",
    apiKey: "1ccbb7fcb0faf770d1c228be80ba16d9",
    searchInput: ".search-input",
    containerTag: "div",

    attributes: {
        class: ["search-input", "unbxd-autosuggest-box"],
        "data-testid": "search-input",
        id: "search-id"
    },
    // Note: Array values (like class) will be handled appropriately by the SDK.

    debounceDelay: 500,
    minChars: 3,
    template: AutosuggestionBoxTemplate, // or a custom template function

    // API Configuration
    api: {
        apiEndpoint: "https://search.unbxd.io",
        inFields: { count: 2 },
        popularProducts: { count: 3 },
        keywordSuggestions: { count: 2 },
        topQueries: { count: 2 },
        promotedSuggestions: { count: 2 }
    },

    // Callback Configuration
    callbacks: {
        onError: (error) => {
            console.error("Autosuggest error:", error);
        }
    }
});
```

---

## Default Configuration
If no configuration is provided, the SDK falls back to the following defaults:

```js
{
    siteKey: "",
    apiKey: "",
    searchInput: null,
    containerTag: "div",
    attributes: {},
    debounceDelay: 0,
    minChars: 3,
    template: AutosuggestionBoxTemplate,
    api: {
        apiEndpoint: "https://search.unbxd.io",
        inFields: { count: 2 },
        popularProducts: { count: 3 },
        keywordSuggestions: { count: 2 },
        topQueries: { count: 2 },
        promotedSuggestions: { count: 2 }
    },
    callbacks: {
        onError: null
    }
}
```
