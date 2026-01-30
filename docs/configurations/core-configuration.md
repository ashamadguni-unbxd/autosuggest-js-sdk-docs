---
layout: default
title: Core Configuration
parent: Configurations
nav_order: 1
---

# Core Configuration

Core configuration options are required to initialize the Autosuggest JS SDK. These settings authenticate API requests, associate them with the correct Unbxd site, and bind autosuggest behavior to a search input element. If any required configuration is missing, the SDK will not initialize.

---

## siteKey (String, Required)

The siteKey is a unique identifier assigned to your site in the Unbxd Console. It is used to associate all Autosuggest API requests with the correct site and search index.

Default  
    siteKey: ""

Example  
    const autosuggest = new Autosuggest({
      siteKey: "ss-unbxd-aus-demo-fashion831421736321881"
    });

Notes  
- Required  
- Must match the site created in the Unbxd Console  
- Site keys are environment-specific (staging and production)

---

## apiKey (String, Required)

The apiKey is used to authenticate Autosuggest API requests. It ensures that only authorized clients can access Autosuggest data for your site.

Default  
    apiKey: ""

Example  
    const autosuggest = new Autosuggest({
      apiKey: "1ccbb7fcb0faf770d1c228be80ba16d9"
    });

Notes  
- Required  
- Keep this key secure  
- Do not expose API keys in public repositories

---

## searchInput (String | null, Required)

The searchInput configuration specifies the CSS selector of the input element where autosuggestions should be enabled. The SDK queries the DOM using this selector and attaches autosuggest behavior to the matched element.

Default  
    searchInput: null

Example  
    const autosuggest = new Autosuggest({
      searchInput: ".search-input"
    });

    const autosuggest = new Autosuggest({
      searchInput: "#search-box"
    });

Notes  
- Required  
- The selector must resolve to a valid input element  
- The input must exist in the DOM before initializing the SDK  
- Autosuggest will not render if the selector is invalid

---

## Minimal Required Configuration

    const autosuggest = new Autosuggest({
      siteKey: "your-site-key",
      apiKey: "your-api-key",
      searchInput: ".search-input"
    });

---

## Next Steps

After completing the core configuration, proceed to the following sections to further customize Autosuggest behavior and appearance:

- Container & DOM Configuration  
- Behavior & Performance Configuration  
- Rendering & Customization  
