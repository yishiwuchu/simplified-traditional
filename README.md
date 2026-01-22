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
- **Browser Compatibility**: Works on IE10+ and all modern browsers

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

``` javascript
toTraditional(text)
```
Converts Simplified Chinese to Traditional Chinese.
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

``` javascript
toSimplified(text)
```
Converts Traditional Chinese to Simplified Chinese.
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

``` javascript
getDictionarySize()
```
Returns the number of character mappings in the dictionary.
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

``` javascript
extendDictionary(newEntries)
```
Extends the conversion dictionary with custom mappings.
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
Dictionary is case-sensitive
Multi-character phrases supported
Cache is automatically cleared after extension
Mappings are immediately available

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
``` javascript
version
```
Library version string (read-only).
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
The sample file is: demo.html
