---
layout: default
title: Callbacks Configuration
parent: Configurations
nav_order: 6
---

# Callbacks Configuration

The Callbacks configuration allows you to hook into key lifecycle events of the Autosuggest SDK. These callbacks are especially useful for error handling, debugging, logging, and integrating Autosuggest events with analytics or monitoring tools.

Callbacks are optional. If not provided, the SDK will function normally using default internal behavior.

---

## callbacks
{: .d-inline-block }
Object
{: .label }
Optional
{: .label .label-blue }

The `callbacks` object groups all event-based callback functions supported by the Autosuggest SDK. Each callback corresponds to a specific event during the autosuggest lifecycle.

Currently, the SDK exposes callbacks primarily for error handling, with scope to add more event hooks in future versions.

### Default Value
```
callbacks: {
  onError: null
}
```


---

## callbacks.onError
{: .d-inline-block }
Function | null
{: .label }
Optional
{: .label .label-blue }

The `onError` callback is invoked whenever an error occurs during the Autosuggest lifecycle. This may include API failures, invalid configurations, network issues, or unexpected runtime errors.

This callback allows you to gracefully handle errors without breaking the user experience. Common use cases include logging errors to the console, reporting issues to monitoring tools, or displaying fallback UI behavior.

### Default Value
```
onError: null
```


### Parameters

- **error**  
  An error object or error message describing the failure. This may include API error details, configuration issues, or runtime exceptions.

### Example Usage
```
const autosuggest = new Autosuggest({
  callbacks: {
    onError: (error) => {
      console.error("Autosuggest error:", error);
        // Optional: send error details to a monitoring or analytics service
        // trackError(error);
    }
  }
});
```
