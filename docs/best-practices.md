---
layout: default
title: Best Practices
nav_order: 7
---

# Best Practices

This section provides recommendations for performance, reliability, and user experience when using the New Autosuggest SDK in production.

---

### Debouncing

Debouncing helps control how frequently new Autosuggest SDK API calls are made while the user is typing.

- A `debounceDelay` of **300–500 milliseconds** is recommended for most use cases.
- This improves performance and reduces unnecessary API calls.
- A value of `0` disables debouncing entirely.
- Disabling debouncing is **not recommended for production environments**, as it can lead to excessive API requests.

---

### Minimum Characters

The `minChars` configuration determines when new Autosuggest SDK API calls are triggered.

- A value of **2 or 3 characters** is recommended for a balanced user experience.
- Lower values may result in excessive API calls.
- Higher values may delay suggestions and negatively impact usability.

---

### Suggestion Counts

Each suggestion type supports configurable `count` values.

- Adjust counts based on available UI space and design requirements.
- Higher counts may increase API response time.
- Maintain a balance between richness of suggestions and performance.

---

### Template Customization

Custom templates allow you to fully control the look and structure of the autosuggestion UI.

- Use custom templates to align the new Autosuggest SDK UI with your site’s design system.
- The template function receives all suggestion data as props.
- Always return a valid HTML string from the template function.

---

### Error Handling

Proper error handling is critical for production applications.

- Always provide an **onEvent** callback in production when you need to handle errors or track events.
- Log errors for debugging and monitoring.
- Consider integrating with an error tracking or observability service to capture failures in real time.

---

### API Endpoint

The New Autosuggest SDK uses a default API endpoint.

- Use the default endpoint unless you have a custom deployment or setup.
- Ensure the endpoint is accessible from your domain and environment.

---

### Attributes

The **attributes** option (under `suggestionBoxConfigs`) allows you to attach HTML attributes to the autosuggestion container. See [Configuration](configuration.html#suggestionboxconfigs).

- Useful for applying CSS classes, IDs, and data attributes.
- Helps with styling, testing, and DOM querying.
- Array values (such as for `class`) are fully supported and handled appropriately by the SDK.
  
