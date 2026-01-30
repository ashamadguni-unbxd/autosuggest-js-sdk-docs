# Installation

Autosuggest JS SDK provides real-time search suggestions as users type into a search input.  
The SDK is browser-ready and does not require any build tools, package managers, or additional dependencies.

This document explains how to include the SDK, add the required HTML markup, and initialize Autosuggest on a web page.

## Including the SDK

Add the Autosuggest JS SDK script to your HTML file.  
The script should be loaded before initializing the SDK.

```html
<script src="https://libraries.unbxdapi.com/search-sdk/v1/autosuggest.min.js"></script>
```

## HTML Setup

Add an input element that will act as the search box.  
The SDK attaches autosuggest functionality to this input using a CSS selector.

```html
<input
  type="text"
  class="search-input"
  placeholder="Search products..."
/>
```

## Initializing the SDK

Initialize the Autosuggest instance by passing the required configuration options.

```html
<script>
  const autosuggest = new Autosuggest({
    siteKey: "ss-unbxd-demo-site",
    apiKey: "demo-api-key",
    searchInput: ".search-input",
    minChars: 3,
    debounceDelay: 300
  });
</script>
```

### Configuration Options

- `siteKey` – Unbxd site identifier  
- `apiKey` – API key associated with the site  
- `searchInput` – CSS selector for the search input element  
- `minChars` – Minimum characters required to trigger autosuggest  
- `debounceDelay` – Delay (in milliseconds) before firing the request

## Complete Example

The following example shows a complete HTML file with Autosuggest enabled.

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Autosuggest JS SDK Example</title>
</head>
<body>

  <input
    type="text"
    class="search-input"
    placeholder="Search products..."
  />

  <script src="https://libraries.unbxdapi.com/search-sdk/v1/autosuggest.min.js"></script>

  <script>
    const autosuggest = new Autosuggest({
      siteKey: "ss-unbxd-demo-site",
      apiKey: "demo-api-key",
      searchInput: ".search-input",
      minChars: 3,
      debounceDelay: 300
    });
  </script>

</body>
</html>
```

Once initialized, the SDK automatically listens for user input and displays relevant suggestions based on the configured Unbxd site.
