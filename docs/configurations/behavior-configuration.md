---
layout: default
title: Behavior & Performance Configuration
parent: Configurations
nav_order: 3
---

# Behavior & Performance Configuration

Behavior and performance configuration options control when Autosuggest API calls are triggered and how frequently they are made. These settings help balance responsiveness with performance by reducing unnecessary network requests while maintaining a smooth user experience.

---

## debounceDelay
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Specifies the delay (in milliseconds) to wait after the user stops typing before triggering the Autosuggest API call. This helps reduce the number of API requests made during rapid typing.

### Default Value

```
debounceDelay: 0
```

Example Usage:
```
const autosuggest = new Autosuggest({
  debounceDelay: 500
});
```
**Note:** A value of `0` disables debouncing, meaning the Autosuggest API will be called on every input change once the `minChars` threshold is met.


## minChars
{: .d-inline-block }
Number
{: .label }
Optional
{: .label .label-blue }

Defines the minimum number of characters required in the input field before triggering an Autosuggest API call. This prevents suggestions from being fetched too early and helps improve overall performance.

### Default Value
```
minChars: 3
```

Example Usage:
```
const autosuggest = new Autosuggest({
  minChars: 2
});
```

**Note:** The Autosuggest API will only be called when the input length is greater than or equal to the specified `minChars` value.
