# Configurations

Use the configuration object to initialize the Autosuggest SDK.  
Pass the Site Key and API Key obtained from the Unbxd Console in the `siteKey` and `apiKey` properties.  
All configuration options are optional unless explicitly marked as required.

---

## siteKey `String`

The unique Site Key assigned by Unbxd for each site created in the Unbxd Console.  
This key is required to authenticate Autosuggest API requests.

Refer to the **Site Setup** section in the documentation for steps to retrieve your Site Key.

### Default Value
```js
siteKey: ""
```

---

## apiKey `String`

The API Key associated with your Unbxd site.  
This key is required for authorization and must be provided during SDK initialization.

Ensure that the API Key corresponds to the configured Site Key.

### Default Value
```js
apiKey: ""
```

---

## searchInput `String | null`

Specifies the CSS selector of the input element to which autosuggest functionality will be attached.  
The SDK queries the DOM using this selector and binds autosuggest behavior to the matched element.

### Default Value
```js
searchInput: null
```

---

## containerTag `String`

Defines the HTML tag used to create the autosuggestion container element.  
This allows flexibility in choosing semantic markup based on layout or accessibility requirements.

### Default Value
```js
containerTag: "div"
```

---

## attributes `Object`

Defines HTML attributes applied to the autosuggestion container element.  
This can be used to assign CSS classes, IDs, or custom data attributes for styling, testing, or analytics.

Array values (for example, `class`) are supported and handled internally by the SDK.

### Default Value
```js
attributes: {}
```

---

## debounceDelay `Number`

Specifies the delay (in milliseconds) before triggering an Autosuggest API request after the user stops typing.  
This helps reduce unnecessary API calls and improves overall performance.

A value of `0` disables debouncing.

### Default Value
```js
debounceDelay: 0
```

---

## minChars `Number`

Defines the minimum number of characters required in the search input before autosuggestions are fetched.  
The API is triggered only when the input length meets or exceeds this value.

### Default Value
```js
minChars: 3
```

---

## template `Function`

Allows customization of the autosuggestion UI by providing a custom rendering function.  
The function receives structured suggestion data and must return a valid HTML string.

If not provided, the default Autosuggest template is used.

### Default Value
```js
template: AutosuggestionBoxTemplate
```

### Template Data
The template function receives the following properties:
- `POPULAR_PRODUCTS`
- `IN_FIELD`
- `KEYWORD_SUGGESTION`
- `PROMOTED_SUGGESTION`
- `TOP_SEARCH_QUERIES`

---
