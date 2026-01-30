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
{: .label .label-blue }
String
{: .label }
Required
{: .label .label-red }
Default: ""
{: .label .label-grey }

The `siteKey` uniquely identifies your site within the Unbxd platform. All Autosuggest API requests are scoped to the site associated with this key.

```
const autosuggest = new Autosuggest({
  siteKey: "ss-unbxd-aus-demo-fashion831421736321881"
});
```

---

## apiKey
{: .label .label-blue }
String
{: .label }
Required
{: .label .label-red }
Default: ""
{: .label .label-grey }

The `apiKey` is used to authenticate Autosuggest API requests and ensures that only authorized clients can access Autosuggest data.

```
const autosuggest = new Autosuggest({
  apiKey: "1ccbb7fcb0faf770d1c228be80ba16d9"
});
```

---

## searchInput
{: .label .label-blue }
String | null
{: .label }
Required
{: .label .label-red }
Default: null
{: .label .label-grey }

Specifies the CSS selector of the input element where Autosuggest should be enabled. The SDK queries the DOM using this selector and attaches autosuggest behavior to the matched element.

```
const autosuggest = new Autosuggest({
  searchInput: ".search-input"
});
```

```
const autosuggest = new Autosuggest({
  searchInput: "#search-box"
});
```

---

## Minimal Required Configuration

The following configuration represents the minimum setup required to initialize the Autosuggest JS SDK:

```
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

