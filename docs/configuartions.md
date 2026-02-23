---
layout: default
title: Configurations
nav_order: 4
has_children: true
permalink: /configurations.html
---

# Configurations
{: .no_toc }

## Overview

The Autosuggest JS SDK provides a flexible configuration model that allows developers to control behavior, API response types, UI rendering, and event handling.

Configurations are passed during SDK initialization and are grouped into logical sections such as:

- `inputBoxConfigs` — Controls search input behavior.
- `apiConfigs` — Defines API parameters and enabled suggestion types.
- `suggestionBoxConfigs` — Manages the suggestion container and rendering behavior.
- `onEvent` — Handles lifecycle and interaction events.

These configuration options enable fine-grained control over how autosuggest behaves and appears within your application.

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## Usage

All configurations are provided when instantiating the `Autosuggest` class.

```javascript
import Autosuggest from "@unbxd-ui/autosuggest-js-sdk";

const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",

  inputBoxConfigs: {
    searchInput: ".search-input",
    debounceDelay: 300,
    minChars: 2,
  },

  apiConfigs: {
    apiEndpoint: "https://search.unbxd.io",
    initialRequest: false,
    trendingSearches: false,
  },

  suggestionBoxConfigs: {
    containerTag: "div",
    attributes: {
      class: ["unbxd-autosuggest-box"],
    },
  },

  onEvent: ({ eventType, payload }) => {
    console.log("Autosuggest event:", eventType, payload);
  },
});
```

Each configuration section is documented below with detailed options, accepted values, and examples.

---

## Configuration Properties

## siteKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique identifier assigned by Unbxd to each site created in the Unbxd Console dashboard. It is required to associate new Autosuggest SDK API requests with the correct site. Refer to the [Unbxd documentation](https://docs.netcoreunbxd.com/docs/getting-started) for steps to retrieve the Site Key for your account.

### Default
{: .no_toc }

```js
siteKey: ""
```

---

## apiKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique API Key assigned to each site created in the Unbxd Console dashboard. Refer to the [Unbxd documentation](https://docs.netcoreunbxd.com/docs/getting-started) for steps to retrieve the API Key for your account.

### Default
{: .no_toc }

```js
apiKey: ""
```

---

## inputBoxConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Behavior and performance options that control **when** new Autosuggest SDK API calls are triggered and how frequently they are made. These settings help balance responsiveness with performance by reducing unnecessary network requests while maintaining a smooth user experience.


| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `searchInput` | String \| null | Yes | `null` | CSS selector for the input element where the SDK should be enabled. The SDK queries the DOM with this selector and attaches autosuggest behavior to the matched element (e.g. `".input-search"`, `"#search-box"`). |
| `debounceDelay` | Number | No | `0` | Delay in milliseconds after the user stops typing before triggering an Autosuggest API call. Reduces requests during rapid typing. A value of `0` disables debouncing (API is called on every input change once `minChars` is met). |
| `minChars` | Number | No | `3` | Minimum number of characters in the input before triggering an Autosuggest API call. Prevents fetching suggestions too early. The API is only called when input length is greater than or equal to this value. |


### Default
{: .no_toc }

```js
inputBoxConfigs: {
  searchInput: null,
  debounceDelay: 0,
  minChars: 3,
}
```

---

## suggestionBoxConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Container and DOM configuration options allow you to control **how and where** the new Autosuggest SDK container is rendered in the DOM. These settings help align the new Autosuggest SDK with your application’s markup structure, styling conventions, and testing requirements. You can also provide a custom template to fully override the default UI and render suggestions according to your design and layout requirements.


| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `containerTag` | String | No | `"div"` | HTML tag used for the autosuggestion container element (e.g. `"div"`, `"section"`). Choose a tag that fits your layout or accessibility needs. |
| `attributes` | Object | No | `{}` | HTML attributes applied to the container (e.g. `class`, `id`, `data-testid`). Useful for CSS classes, test IDs, or custom data attributes. Array values (e.g. for `class`) are supported. |
| `template` | Function \| null | No | `null` | Custom template function used to render the autosuggestion container. For details, examples, and template props, see [Template](configurations/template.html). |


### Default
{: .no_toc }

```js
suggestionBoxConfigs: {
  containerTag: "div",
  attributes: {},
  template: null,
}
```

---

## apiConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

The API configuration controls how the new Autosuggest SDK communicates with the Unbxd backend. It allows you to define the API endpoint and fine-tune the **types and number of suggestions** fetched for each request. These settings help tailor the new Autosuggest SDK experience to match business priorities and user behavior.

### apiConfigs options
{: .no_toc }

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `apiEndpoint` | String | `"https://search.unbxd.io"` | Base URL for the Unbxd Search API used to fetch autosuggestion data. In most cases use the default; useful for private cloud or custom routing. |
| `initialRequest` | Boolean | `false` | When `true`, an initial request is fired (e.g. on load) to prefetch suggestion data. |
| `inFields` | Object | `{ count: 2 }` | **In-field suggestions** — keyword suggestions matched against specific indexed fields (e.g. product name, category, brand). **`count`**: number of suggestions to fetch. |
| `popularProducts` | Object | `{ count: 3, fields: [] }` | **Popular product suggestions** — frequently viewed or searched products. **`count`**: number to retrieve. **`fields`**: optional array of fields to request per product. |
| `keywordSuggestions` | Object | `{ count: 2 }` | **Keyword-based suggestions** — commonly searched or relevant keywords. **`count`**: number of keyword suggestions to fetch. |
| `topQueries` | Object | `{ count: 2 }` | **Top search queries** — most frequently searched queries across the site. **`count`**: number to include in results. |
| `promotedSuggestions` | Object | `{ count: 2 }` | **Promoted suggestions** — keywords or results boosted by merchandising rules in the Unbxd Console. **`count`**: number to fetch. |
| `trendingSearches` | Object | `{ count: 5 }` | **Trending search** suggestions. **`count`**: number of trending searches to fetch. |

### Default
{: .no_toc }

```js
apiConfigs: {
  apiEndpoint: "https://search.unbxd.io",
  initialRequest: false,
  inFields: { count: 2 },
  popularProducts: { count: 3, fields: [] },
  keywordSuggestions: { count: 2 },
  topQueries: { count: 2 },
  promotedSuggestions: { count: 2 },
  trendingSearches: { count: 5 }
}
```

### Example
{: .no_toc }

```js
apiConfigs: {
  apiEndpoint: "https://search.unbxd.io",
  initialRequest: true,
  inFields: { count: 5 },
  popularProducts: { count: 5, fields: [] },
  keywordSuggestions: { count: 5 },
  topQueries: { count: 5 },
  promotedSuggestions: { count: 5 },
  trendingSearches: { count: 5 }
}
```

---

## onEvent
{: .d-inline-block }
Function
{: .label }
Optional
{: .label .label-blue }

Callback function triggered on Autosuggest lifecycle and interaction events.  
Useful for logging, analytics integration, error handling, or debugging.

The function receives an object containing at least **`eventType`**.

### Default
{: .no_toc }

```js
onEvent: function ({ eventType }) {
  console.log(`Unbxd Running onEvent with ${eventType}`);
}
```

### Parameters
{: .no_toc }

- **eventType** — A string identifying the lifecycle event.

### Example
{: .no_toc }

```js
const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",
  inputBoxConfigs: {
    searchInput: ".input-search",
    debounceDelay: 200,
    minChars: 2,
  },
  suggestionBoxConfigs: {
    containerTag: "div",
    attributes: { class: ["unbxd-auto-suggest"] },
    template: null,
  },
  apiConfigs: {
    initialRequest: true,
    popularProducts: { count: 5, fields: [] },
    keywordSuggestions: { count: 5 },
    trendingSearches: { count: 5 },
  },
  onEvent: ({ eventType }) => {
    console.log("Autosuggest event:", eventType);
    // Optional: send to analytics or error tracking
  },
});
```