---
layout: default
title: Container & DOM Configuration
parent: Configurations
nav_order: 2
---

# Container & DOM Configuration

Container and DOM configuration options allow you to control how and where the Autosuggest container is rendered in the DOM. These settings help align Autosuggest with your application’s markup structure, styling conventions, and testing requirements.

---

## containerTag
{: .d-inline-block }
String
{: .label }
Optional
{: .label .label-blue }

Defines the HTML tag used to create the autosuggestion container element. This allows you to choose a semantic HTML tag that best fits your layout or accessibility requirements.

### Default Value
```
containerTag: "div"
```

Example Usage:
```
const autosuggest = new Autosuggest({
  containerTag: "section"
});
```

---

## attributes
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

Specifies the HTML attributes that should be applied to the autosuggestion container element. This is useful for adding CSS classes, IDs, test identifiers, or custom data attributes required by your application.

Note: Array values (such as class) will be handled appropriately by the SDK.

### Default Value
```
attributes: {}
```

Example Usage:
```
const autosuggest = new Autosuggest({
  attributes: {
    "class": ["search-input", "unbxd-autosuggest-box"],
    "data-testid": "search-input",
    "id": "search-id"
  }
});
```
