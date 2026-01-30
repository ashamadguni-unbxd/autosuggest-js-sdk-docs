---
layout: default
title: Configuration
nav_order: 3
---

# Configuration

This section describes the configuration options available in the Unbxd Autosuggest JavaScript SDK.  
The SDK is initialized using a configuration object that controls authentication, DOM binding, request behavior, and rendering of autosuggestions.

Each configuration property is documented with its data type, requirement level, default value, and usage example to ensure correct and consistent integration.

---

## Basic Configuration

Basic configuration properties are essential for enabling autosuggest functionality.  
These options allow the SDK to authenticate with Unbxd services and attach autosuggestions to a search input element on the page.

---

### siteKey

**Type:** String  
**Required:** Yes  
**Default:** `""`

The `siteKey` uniquely identifies your Unbxd account and is required for all Autosuggest API requests.  
This value is provided during site onboarding and must be included during SDK initialization.

**Example:**
```
ss-unbxd-aus-demo-fashion831421736321881
```

**Usage:**
```js
const autosuggest = new Autosuggest({
  siteKey: "ss-unbxd-aus-demo-fashion831421736321881"
});
```

---

### apiKey

**Type:** String  
**Required:** Yes  
**Default:** `""`

The `apiKey` is used to authorize requests made by the Autosuggest SDK.  
It must correspond to the configured Unbxd site and should be kept secure.

**Example:**
```
1ccbb7fcb0faf770d1c228be80ba16d9
```

**Usage:**
```js
const autosuggest = new Autosuggest({
  apiKey: "your-api-key-here"
});
```

---

### searchInput

**Type:** String  
**Required:** Yes  
**Default:** `null`

A CSS selector that identifies the input element to which autosuggest behavior will be applied.  
The SDK queries the DOM using this selector and binds input, focus, and keyboard events to the matched element.

**Examples:**
```
".search-input"
"#search-box"
```

**Usage:**
```js
const autosuggest = new Autosuggest({
  searchInput: ".search-input"
});
```

---

### containerTag

**Type:** String  
**Required:** No  
**Default:** `"div"`

Specifies the HTML tag used to create the autosuggestion container element.  
This allows flexibility in choosing semantic HTML elements based on layout requirements.

**Usage:**
```js
const autosuggest = new Autosuggest({
  containerTag: "section"
});
```

---

### attributes

**Type:** Object  
**Required:** No  
**Default:** `{}`

Defines HTML attributes applied to the autosuggestion container element.  
This can be used to assign CSS classes, element IDs, or custom data attributes for styling, testing, or analytics.

Array values (such as `class`) are handled appropriately by the SDK.

**Usage:**
```js
const autosuggest = new Autosuggest({
  attributes: {
    class: ["unbxd-autosuggest", "search-suggestions"],
    id: "autosuggest-container",
    "data-testid": "autosuggest"
  }
});
```

---

### debounceDelay

**Type:** Number  
**Required:** No  
**Default:** `0`

Specifies the delay (in milliseconds) before triggering the Autosuggest API request after the user stops typing.  
This option helps reduce the number of API calls and improves performance.

A value of `0` disables debouncing and triggers requests immediately after input changes.

**Usage:**
```js
const autosuggest = new Autosuggest({
  debounceDelay: 300
});
```

---

### minChars

**Type:** Number  
**Required:** No  
**Default:** `3`

Defines the minimum number of characters required in the search input before the Autosuggest API is invoked.  
Requests are triggered only when the input length is greater than or equal to this value.

**Usage:**
```js
const autosuggest = new Autosuggest({
  minChars: 2
});
```

---

### template

**Type:** Function  
**Required:** No  
**Default:** `AutosuggestionBoxTemplate`

Allows customization of the autosuggestion UI by providing a custom template function.  
The function receives structured suggestion data and must return a valid HTML string.

If no custom template is provided, the SDK renders the default autosuggestion layout.

**Usage:**
```js
function CustomTemplate(props) {
  return `<div>Custom Autosuggest UI</div>`;
}

const autosuggest = new Autosuggest({
  template: CustomTemplate
});
```

**Template Properties:**
- `POPULAR_PRODUCTS` – Popular product suggestions
- `IN_FIELD` – In-field suggestions
- `KEYWORD_SUGGESTION` – Keyword-based suggestions
- `PROMOTED_SUGGESTION` – Promoted suggestions
- `TOP_SEARCH_QUERIES` – Frequently searched queries

---
