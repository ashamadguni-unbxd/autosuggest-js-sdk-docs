---
layout: default
title: Configuration
nav_order: 4
permalink: /configuration.html
---

# Configuration

All configuration options are provided when initializing the Autosuggest SDK. Options are optional unless marked required.

Core configuration options authenticate API requests, associate them with the correct Unbxd site, and bind Autosuggest behavior to a search input element. Container, behavior, API, and callback settings allow you to control how and where the suggestion box is rendered, when API calls are triggered, and how to hook into lifecycle events.

---

## Top-level options

| Option | Type | Required | Description |
|--------|------|----------|-------------|
| `siteKey` | String | Yes | Unbxd site identifier. |
| `apiKey` | String | Yes | Unbxd API key for the site. |
| `inputBoxConfigs` | Object | No | Input element and request behavior. |
| `suggestionBoxConfigs` | Object | No | Container element and template. |
| `apiConfigs` | Object | No | API endpoint and suggestion counts. |
| `onEvent` | Function | No | Lifecycle event callback. |

---

## siteKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique identifier assigned by Unbxd to each site created in the Unbxd Console dashboard. It is required to associate Autosuggest API requests with the correct site. Refer to the [Unbxd documentation](https://docs.netcoreunbxd.com/docs/getting-started) for steps to retrieve the Site Key for your account.

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

Behavior and performance options that control **when** Autosuggest API calls are triggered and how frequently they are made. These settings help balance responsiveness with performance by reducing unnecessary network requests while maintaining a smooth user experience.

### Default

```js
inputBoxConfigs: {
  searchInput: null,
  debounceDelay: 0,
  minChars: 3,
}
```

### inputBoxConfigs.searchInput
{: .d-inline-block }
String | null
{: .label }
Required
{: .label .label-red }

Specifies the CSS selector of the input element where Autosuggest should be enabled. The SDK queries the DOM using this selector and attaches autosuggest behavior to the matched element.

```js
inputBoxConfigs: {
  searchInput: ".input-search"
}
```

```js
inputBoxConfigs: {
  searchInput: "#search-box"
}
```

### inputBoxConfigs.debounceDelay
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Specifies the delay (in milliseconds) to wait after the user stops typing before triggering the Autosuggest API call. This helps reduce the number of API requests made during rapid typing.

**Note:** A value of `0` disables debouncing, meaning the Autosuggest API will be called on every input change once the `minChars` threshold is met.

```js
inputBoxConfigs: {
  debounceDelay: 500
}
```

### inputBoxConfigs.minChars
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Defines the minimum number of characters required in the input field before triggering an Autosuggest API call. This prevents suggestions from being fetched too early and helps improve overall performance.

**Note:** The Autosuggest API will only be called when the input length is greater than or equal to the specified `minChars` value.

```js
inputBoxConfigs: {
  minChars: 2
}
```

---

## suggestionBoxConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Container and DOM configuration options allow you to control **how and where** the Autosuggest container is rendered in the DOM. These settings help align Autosuggest with your application’s markup structure, styling conventions, and testing requirements. You can also provide a custom template to fully override the default UI and render suggestions according to your design and layout requirements.

### Default

```js
suggestionBoxConfigs: {
  containerTag: "div",
  attributes: {},
  template: null,
}
```

### suggestionBoxConfigs.containerTag
{: .d-inline-block }
String
{: .label }
Optional
{: .label .label-blue }

Defines the HTML tag used to create the autosuggestion container element. This allows you to choose a semantic HTML tag that best fits your layout or accessibility requirements.

```js
suggestionBoxConfigs: {
  containerTag: "section"
}
```

### suggestionBoxConfigs.attributes
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Specifies the HTML attributes that should be applied to the autosuggestion container element. This is useful for adding CSS classes, IDs, test identifiers, or custom data attributes required by your application.

**Note:** Array values (such as `class`) will be handled appropriately by the SDK.

```js
suggestionBoxConfigs: {
  attributes: {
    "class": ["search-input", "unbxd-autosuggest-box"],
    "data-testid": "search-input",
    "id": "search-id"
  }
}
```

### suggestionBoxConfigs.template
{: .d-inline-block }
Function | null
{: .label }
Optional
{: .label .label-blue }

Defines a custom template function used to render the autosuggestion container. This function receives structured suggestion data as input and must return an HTML string. Providing a custom template completely overrides the default autosuggestion UI.

When not provided, the SDK uses its built-in default template.

```js
function CustomTemplate(props) {
  const { query, response } = props;
  const { popularProducts = [], keywordSuggestions = [], inFields = [],
         promotedSuggestions = [], topSearchQueries = [], trendingSearches = [] } = response || {};
  return `<div class="my-suggestions">Custom HTML here</div>`;
}

const autosuggest = new Autosuggest({
  suggestionBoxConfigs: {
    template: CustomTemplate
  }
});
```

#### Template props

The template function receives an object with at least:

- **query** — Current search query string.
- **response** — Object containing:
  - **popularProducts** — Array of popular product suggestions.
  - **inFields** — Array of in-field suggestions based on the user’s current input.
  - **keywordSuggestions** — Array of keyword-based search suggestions.
  - **promotedSuggestions** — Array of promoted or sponsored suggestions configured in the Unbxd Console.
  - **topSearchQueries** — Array of top search queries based on overall user search trends.
  - **trendingSearches** — Array of trending search suggestions (when available).

---

## apiConfigs
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

The API configuration controls how Autosuggest communicates with the Unbxd backend. It allows you to define the API endpoint and fine-tune the **types and number of suggestions** fetched for each autosuggest request. These settings help tailor the autosuggest experience to match business priorities and user behavior.

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

The event callback allows you to hook into key lifecycle events of the Autosuggest SDK. This is especially useful for error handling, debugging, logging, and integrating Autosuggest events with analytics or monitoring tools. Callbacks are optional; if not provided, the SDK will function normally using default internal behavior.

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

---

## Minimal required configuration

The following configuration represents the minimum setup required to initialize the Autosuggest JS SDK:

```js
const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",
  inputBoxConfigs: {
    searchInput: ".search-input"
  }
});
```

All other options use their default values.
