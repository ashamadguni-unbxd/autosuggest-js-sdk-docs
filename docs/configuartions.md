---
layout: default
title: Configurations
nav_order: 5
has_children: true
permalink: /configurations.html
---

# Configurations

Configuration is passed when the New Autosuggest SDK is initialized. All options are optional unless marked as required.

Core options authenticate requests with Unbxd, bind the SDK to a search input, and control the suggestion container, request behavior, API parameters, and lifecycle events.

---

## Configuration Options

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `siteKey` | String | Yes | `""` | Unique identifier for your Unbxd site. Used to associate all Autosuggest API requests with the correct site. Obtain it from the Unbxd Console. |
| `apiKey` | String | Yes | `""` | API key for your Unbxd site. Used to authenticate requests to the Autosuggest API. Obtain it from the Unbxd Console. |
| `inputBoxConfigs` | Object | No | — | Configuration for the search input and request behavior: CSS selector for the input, debounce delay, minimum characters before fetching suggestions, and related options. |
| `suggestionBoxConfigs` | Object | No | — | Configuration for the suggestion dropdown: container tag, HTML attributes, and an optional custom template function for rendering each suggestion. |
| `apiConfigs` | Object | No | — | API endpoint URL and per-type suggestion counts (in-fields, popular products, keyword suggestions, top queries, promoted suggestions, trending searches). |
| `onEvent` | Function | No | — | Callback invoked for SDK lifecycle events (e.g. open, close, select). Use for logging, analytics, or error handling in production. |

---

## siteKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique identifier assigned by Unbxd to each site created in the Unbxd Console dashboard. It is required to associate new Autosuggest SDK API requests with the correct site. Refer to the [Unbxd documentation](https://docs.netcoreunbxd.com/docs/getting-started) for steps to retrieve the Site Key for your account.

### Default (placeholder)

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

### Default (placeholder)

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

### Default

```js
inputBoxConfigs: {
  searchInput: null,
  debounceDelay: 0,
  minChars: 3,
}
```

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `searchInput` | String \| null | Yes | `null` | CSS selector for the input element where the SDK should be enabled. The SDK queries the DOM with this selector and attaches autosuggest behavior to the matched element (e.g. `".input-search"`, `"#search-box"`). |
| `debounceDelay` | Number | No | `0` | Delay in milliseconds after the user stops typing before triggering an Autosuggest API call. Reduces requests during rapid typing. A value of `0` disables debouncing (API is called on every input change once `minChars` is met). |
| `minChars` | Number | No | `3` | Minimum number of characters in the input before triggering an Autosuggest API call. Prevents fetching suggestions too early. The API is only called when input length is greater than or equal to this value. |

---

## suggestionBoxConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Container and DOM configuration options allow you to control **how and where** the new Autosuggest SDK container is rendered in the DOM. These settings help align the new Autosuggest SDK with your application’s markup structure, styling conventions, and testing requirements. You can also provide a custom template to fully override the default UI and render suggestions according to your design and layout requirements.

### Default

```js
suggestionBoxConfigs: {
  containerTag: "div",
  attributes: {},
  template: null,
}
```

| Option | Type | Required | Default | Description |
|--------|------|----------|---------|-------------|
| `containerTag` | String | No | `"div"` | HTML tag used for the autosuggestion container element (e.g. `"div"`, `"section"`). Choose a tag that fits your layout or accessibility needs. |
| `attributes` | Object | No | `{}` | HTML attributes applied to the container (e.g. `class`, `id`, `data-testid`). Useful for CSS classes, test IDs, or custom data attributes. Array values (e.g. for `class`) are supported. |
| `template` | Function \| null | No | `null` | Custom template function used to render the autosuggestion container. For details, examples, and template props, see [Template](configurations/template.html). |

---

## apiConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

The API configuration controls how the new Autosuggest SDK communicates with the Unbxd backend. It allows you to define the API endpoint and fine-tune the **types and number of suggestions** fetched for each request. These settings help tailor the new Autosuggest SDK experience to match business priorities and user behavior.

### Default

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

### apiConfigs options

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

### Example

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

The event callback allows you to hook into key lifecycle events of the new Autosuggest SDK. This is especially useful for error handling, debugging, logging, and integrating new Autosuggest SDK events with analytics or monitoring tools. Callbacks are optional; if not provided, the SDK will function normally using default internal behavior.

The callback is invoked with an object that includes at least **`eventType`**. You can use it to gracefully handle errors or track user actions without breaking the user experience. Common use cases include logging events to the console, reporting to monitoring tools, or displaying fallback UI.

### Default

```js
onEvent: function ({ eventType }) {
  console.log(`Unbxd Running onEvent with ${eventType}`);
}
```

### Parameters

- **eventType** — A string identifying the lifecycle event.

### Example

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