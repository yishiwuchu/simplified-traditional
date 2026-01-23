# SimplifiedTraditionalConverter

A lightweight JavaScript library for converting between Simplified and Traditional Chinese characters, with full support for IE10+ browsers.

## Features

### 🔤 Core Conversion
- **Bidirectional Conversion**: Convert between Simplified and Traditional Chinese
- **High Performance**: Optimized character mapping algorithm
- **Large Dictionary**: Comprehensive character coverage

### 🌐 DOM Manipulation
- **Element Conversion**: Convert specific DOM elements or sections
- **Full Page Support**: Convert entire page content including title
- **Selector Support**: Use CSS selectors to target multiple elements

### 🛠️ Utilities
- **Dictionary Management**: Extend or modify conversion dictionary
- **Version Information**: Built-in version tracking
- **Browser Compatibility**: Works on IE9+ and all modern browsers

## Installation

### Direct Script Include
```html
<script src="chinese-converter.min.js"></script>
``` 
## Global Access
### After including the script, the library is available globally as:

``` javascript
// Full name
SimplifiedTraditionalConverter

// Short alias
STC
```
## API Reference
### Core Conversion Functions


### toTraditional(text) Converts Simplified Chinese to Traditional Chinese.
- **Parameters**: text (String): The Simplified Chinese text to convert
- **Returns**: Converted Traditional Chinese text
### Example:
``` javascript
// Basic conversion
const traditional = STC.toTraditional('这是一个简体中文示例');
console.log(traditonal); // '這是一個簡體中文示例'

// Handles mixed content
const mixed = STC.toTraditional('Hello 世界, 这是一个test');
console.log(mixed); // 'Hello 世界, 這是一個test'

// Returns empty string for falsy input
console.log(STC.toTraditional('')); // ''
console.log(STC.toTraditional(null)); // ''
console.log(STC.toTraditional(undefined)); // ''
```
### Performance Note: For batch processing, consider:
``` javascript
// Process array of strings
const texts = ['文本1', '文本2', '文本3'];
const traditionalTexts = texts.map(text => STC.toTraditional(text));

// Large text processing
const largeText = '...'; // Large Chinese text
const start = performance.now();
const result = STC.toTraditional(largeText);
const end = performance.now();
console.log(`Conversion took ${end - start}ms for ${largeText.length} characters`);
```



### toSimplified(text) Converts Traditional Chinese to Simplified Chinese.
Parameters:
- **text (String)**: The Traditional Chinese text to convert
- **Returns**: Converted Simplified Chinese text
Example:
``` javascript
// Basic conversion
const simplified = STC.toSimplified('這是一個繁體中文示例');
console.log(simplified); // '这是一个繁体中文示例'

// Handles edge cases
const withNumbers = STC.toSimplified('第1個測試項目');
console.log(withNumbers); // '第1个测试项目'

// Preserves punctuation
const withPunctuation = STC.toSimplified('你好，世界！「引號」測試');
console.log(withPunctuation); // '你好，世界！「引号」测试'
```
Caching Note: The reverse dictionary is cached after first use:
``` javascript
// First call builds cache
STC.toSimplified('測試');

// Subsequent calls use cached dictionary
STC.toSimplified('另一個測試'); // Faster execution
```

### getDictionarySize() Returns the number of character mappings in the dictionary.
- **Returns**: Integer count of dictionary entries
Example:
``` javascript
console.log(`Dictionary contains ${STC.getDictionarySize()} entries`);
// Output: Dictionary contains 12345 entries (example)

// Monitor dictionary growth
const initialSize = STC.getDictionarySize();
STC.extendDictionary({ '新': '新' });
console.log(`Dictionary now has ${STC.getDictionarySize()} entries`);
```

### extendDictionary(newEntries) Extends the conversion dictionary with custom mappings.
- **Parameters**: newEntries (Object): Key-value pairs of Simplified→Traditional character mappings
Example:
``` javascript
// Add regional variants
STC.extendDictionary({
  // Taiwan-specific mappings
  '台': '臺',
  '里': '裡',
  
  // Hong Kong-specific mappings
  '着': '著',
  '么': '麼',
  
  // Domain-specific terms
  '软件': '軟體',
  '博客': '部落格'
});

// Verify new mappings work
const result1 = STC.toTraditional('台湾的软件博客');
console.log(result1); // '臺灣的軟體部落格'

const result2 = STC.toSimplified('臺灣的軟體部落格');
console.log(result2); // '台湾的软件博客'
```
Important Notes:
- **Dictionary** is case-sensitive
- **Multi-character** phrases supported
- **Cache** is automatically cleared after extension
- **Mappings** are immediately available

``` javascript
// Multi-character mappings
STC.extendDictionary({
  '鼠标': '滑鼠',
  '优盘': '隨身碟',
  '网吧': '網咖'
});

// Complex example with overlapping characters
const test = STC.toTraditional('我去网吧用鼠标拷贝文件到优盘');
console.log(test); // '我去網咖用滑鼠拷貝文件到隨身碟'
```

### version Library version string (read-only).
Example:
``` javascript
// Check version
console.log(`Using SimplifiedTraditionalConverter v${STC.version}`);

// Version comparison
if (STC.version < '1.1.0') {
  console.warn('Consider updating to latest version');
}

// In your application
const appInfo = {
  name: 'MyApp',
  converterVersion: STC.version,
  dictionarySize: STC.getDictionarySize()
};
console.table(appInfo);
```
## DOM Element Conversion Functions

### convertElementToTraditional(element) Converts all text content within a specific DOM element from Simplified to Traditional Chinese.
- **Parameters**: element (HTMLElement|String): DOM element or CSS selector
- **Returns**: Boolean indicating success
Example:
``` javascript
// Using element reference
const myDiv = document.getElementById('content');
const success1 = STC.convertElementToTraditional(myDiv);
console.log(`Conversion ${success1 ? 'succeeded' : 'failed'}`);

// Using CSS selector
const success2 = STC.convertElementToTraditional('.article-content');
console.log(`Conversion ${success2 ? 'succeeded' : 'failed'}`);

// Multiple elements (use convertBySelector instead)
STC.convertBySelector('.blog-post', true);
```

### convertElementToSimplified(element) Converts all text content within a specific DOM element from Traditional to Simplified Chinese.
- **Parameters**: element (HTMLElement|String): DOM element or CSS selector
- **Returns**: Boolean indicating success
Example:
``` javascript
// Convert specific element
STC.convertElementToSimplified('#traditional-content');

// Handle conversion result
const element = document.querySelector('.user-content');
if (STC.convertElementToSimplified(element)) {
  console.log('Content converted successfully');
} else {
  console.error('Failed to convert content');
}

// Real-world usage in a language toggle feature
function switchToSimplified() {
  const mainContent = document.querySelector('main');
  const sidebar = document.querySelector('.sidebar');
  
  STC.convertElementToSimplified(mainContent);
  STC.convertElementToSimplified(sidebar);
}
```

### convertBodyToTraditional() Converts the entire document body from Simplified to Traditional Chinese, including page title.
Example:
``` javascript
// Convert entire page
STC.convertBodyToTraditional();

// Usage in language switching
document.getElementById('traditional-btn').addEventListener('click', function() {
  STC.convertBodyToTraditional();
  localStorage.setItem('language-preference', 'traditional');
});

// With animation to show conversion
function animateTraditionalConversion() {
  document.body.style.opacity = '0.7';
  setTimeout(() => {
    STC.convertBodyToTraditional();
    document.body.style.opacity = '1';
  }, 300);
}
```

### convertBodyToSimplified() Converts the entire document body from Traditional to Simplified Chinese, including page title.
Example:
``` javascript
// Initial page load based on user preference
document.addEventListener('DOMContentLoaded', function() {
  const pref = localStorage.getItem('language-preference') || 'simplified';
  if (pref === 'simplified') {
    STC.convertBodyToSimplified();
  }
});

// Integration with existing language systems
function switchToSimplifiedWithNotification() {
  STC.convertBodyToSimplified();
  
  // Show notification
  const notification = document.createElement('div');
  notification.textContent = '已切换至简体中文';
  notification.className = 'language-notification';
  document.body.appendChild(notification);
  
  setTimeout(() => notification.remove(), 2000);
}
```

### convertBySelector(selector, toTraditional) Converts all elements matching a CSS selector.

- **Parameters**:
    selector (String): CSS selector string
    toTraditional (Boolean): true for Simplified→Traditional, false for Traditional→Simplified
- **Returns**: Number of elements converted
Example:
``` javascript
// Convert all articles to Traditional Chinese
const count1 = STC.convertBySelector('article', true);
console.log(`Converted ${count1} articles`);

// Convert all user comments to Simplified Chinese
const count2 = STC.convertBySelector('.comment', false);
console.log(`Converted ${count2} comments`);

// Complex selectors
STC.convertBySelector('section.content:not(.code-sample)', true);

// Progressive conversion for large pages
function convertPageSections() {
  const sections = [
    'header', 'nav', 'main', 'aside', 'footer'
  ];
  
  sections.forEach(selector => {
    const count = STC.convertBySelector(selector, true);
    console.log(`Converted ${count} ${selector} elements`);
  });
}
```

### config(options) Configures library settings at runtime.
- **Parameters**: options (Object): Configuration object
    debug (Boolean): Enable/disable debug logging
    excludeTags (Array): HTML tags to exclude from conversion
    dictionary (Object): Additional character mappings
- **Returns**: Current configuration object
Example:

``` javascript
// Enable debug mode
STC.config({
  debug: true,
  excludeTags: ['SCRIPT', 'STYLE', 'CODE', 'PRE', 'INPUT', 'TEXTAREA']
});

// Add custom dictionary entries through config
STC.config({
  dictionary: {
    '的': '嘅',  // Hong Kong variant
    '和': '同'   // Cantonese usage
  }
});

// Get current configuration
const currentConfig = STC.config();
console.log('Current config:', currentConfig);

// Development vs production setup
if (window.location.hostname === 'localhost') {
  STC.config({ debug: true });
} else {
  STC.config({ debug: false });
}
```

### clearCache() Clears internal caches for improved memory management.
Example:
``` javascript
// Clear cache after heavy usage
STC.clearCache();

// Periodic cache clearing for long-running applications
setInterval(() => {
  STC.clearCache();
  console.log('Cache cleared');
}, 60 * 60 * 1000); // Every hour

// Usage with dictionary extension
function updateDictionaryWithReload(newMappings) {
  STC.extendDictionary(newMappings);
  STC.clearCache(); // Ensure fresh start
  console.log('Dictionary updated and cache cleared');
}
```

### Browser Compatibility
The library is compatible with:
- **Internet Explorer 9+**
- **Edge (all versions)**
- **Chrome 23+**
- **Firefox 21+**
- **Safari 6.1+**
- **Opera 15+**
- **iOS Safari 7+**
- **Android Browser 4.4+**

### Performance Tips
- **Cache Results: Store converted results if content is static**
- **Selective Conversion: Use convertElementToTraditional() instead of converting the entire body when possible**
- **Batch Processing: For large documents, process in chunks**
- **Avoid Over-conversion: Use excludeTags to skip non-text content**

## License
MIT License - see LICENSE file for details.

## Support
For support, please open an issue in the GitHub repository or contact the maintainers.

## The sample file is: demo.html
