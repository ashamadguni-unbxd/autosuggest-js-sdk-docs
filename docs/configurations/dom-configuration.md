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

