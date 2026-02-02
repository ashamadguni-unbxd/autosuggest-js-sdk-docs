---
layout: default
title: Rendering & Customization
parent: Configurations
nav_order: 4
---

# Rendering & Customization

Rendering and customization configuration allows you to control how the autosuggestion box is displayed. Using a custom template, you can fully override the default UI and render suggestions according to your design and layout requirements.

---

## template
{: .d-inline-block }
Function
{: .label }
Optional
{: .label .label-blue }

Defines a custom template function used to render the autosuggestion container. This function receives structured suggestion data as input and must return an HTML string. Providing a custom template completely overrides the default autosuggestion UI.

### Default Value

```
template: AutosuggestionBoxTemplate
```

(The SDK’s built-in default template is used when no custom template is provided.)

Example Usage:
```
function CustomTemplate(props) {
    const { POPULAR_PRODUCTS, IN_FIELD, KEYWORD_SUGGESTION, 
            PROMOTED_SUGGESTION, TOP_SEARCH_QUERIES } = props;
    return `<div>Custom HTML here</div>`;
}
        
const autosuggest = new Autosuggest({
    template: CustomTemplate
});
```

### Template Props

The `template` function receives an object containing the following properties:

- **POPULAR_PRODUCTS**  
  Array of popular product suggestions returned by the Autosuggest API.

- **IN_FIELD**  
  Array of in-field suggestions based on the user’s current input.

- **KEYWORD_SUGGESTION**  
  Array of keyword-based search suggestions.

- **PROMOTED_SUGGESTION**  
  Array of promoted or sponsored suggestions configured in the Unbxd Console.

- **TOP_SEARCH_QUERIES**  
  Array of top search queries based on overall user search trends.
