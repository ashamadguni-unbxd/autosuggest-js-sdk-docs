---
layout: default
title: Core Configuration
parent: Configurations
nav_order: 1
---

# Core Configuration

Core configuration options are required to initialize the Autosuggest JS SDK. These settings authenticate API requests, associate them with the correct Unbxd site, and bind Autosuggest behavior to a search input element.

---

## siteKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique identifier assigned by Unbxd to each site created in the Unbxd Console dashboard. It is required to associate Autosuggest API requests with the correct site. Refer to [this section](https://unbxd.com/docs/site-search/documentation/configure-site-profile/) for steps to retrieve the Site Key for your account.

### Default Value

```js
siteKey:NA
```

---

## apiKey
{: .d-inline-block }
String
{: .label }
Required
{: .label .label-red }

A unique API Key assigned to each site created in the Unbxd console dashboard. Refer to [this section](https://unbxd.com/docs/site-search/documentation/configure-site-profile/) for steps to retrieve the API Key for your account.


### Default Value
```js
apiKey: NA
```

---

## searchInput
{: .d-inline-block }
String | null
{: .label }
Required
{: .label .label-red }

Specifies the CSS selector of the input element where Autosuggest should be enabled. The SDK queries the DOM using this selector and attaches autosuggest behavior to the matched element.

### Default Value

```js
searchInput: null
```

Example Usage:

```js
const autosuggest = new Autosuggest({
  searchInput: ".search-input"
});
```

```js
const autosuggest = new Autosuggest({
  searchInput: "#search-box"
});
```

---

## Minimal Required Configuration

The following configuration represents the minimum setup required to initialize the Autosuggest JS SDK:

```js
const autosuggest = new Autosuggest({
  siteKey: "your-site-key",
  apiKey: "your-api-key",
  searchInput: ".search-input"
});
```

---

## Next Steps

After completing the core configuration, continue with:

- Container & DOM Configuration  
- Behavior & Performance Configuration  
- Rendering & Customization  

