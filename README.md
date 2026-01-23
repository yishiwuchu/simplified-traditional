# simplified-traditional v1.1.0

A lightweight JavaScript library for bidirectional conversion between Simplified and Traditional Chinese characters, with full support for regional differences (Taiwan, Hong Kong, Macao) and IE9+ compatibility.

## Features

### 🔤 Core Conversion
- **Multi-Region Support**: Convert between Simplified Chinese and regional Traditional variants (Taiwan, Hong Kong, Macao)
- **Bidirectional Conversion**: Convert between Simplified and Traditional Chinese
- **High Performance**: Optimized character mapping algorithm
- **Large Dictionary**: Comprehensive character coverage
- **Comprehensive Dictionary**: 2500+ character mappings with regional variations

### 🌐 DOM Manipulation
- **Selective Conversion**: Convert specific elements, sections, or entire pages
- **CSS Selector Support**: Target elements using standard CSS selectors
- **Title Conversion**: Automatic page title conversion
- **Smart Exclusion**: Configurable exclusion of specific HTML tags

### 🛠️ Utilities
- **Regional Dictionary Management**: Extend/modify dictionaries per region
- **Performance Monitoring**: Built-in performance statistics
- **Intelligent Detection**: Auto-detect text region based on character usage
- **Cross-Region Conversion**: Direct conversion between regional variants
- **Cache Management**: Manual cache control for memory optimization

## Installation

### Direct Script Include
```html
<script src="chinese-converter.min.js"></script>
``` 
## Global Access
### After including the script, the library is available globally:

``` javascript
// Full name
SimplifiedTraditionalConverter

// Short alias
STC
```

## API Reference
### Core Conversion Functions

### toTraditional(text, region) Converts Simplified Chinese to Traditional Chinese for the specified region.
- **Parameters**:
    1. text (String): The Simplified Chinese text to convert
    2. region (String, optional): Target region - 'taiwan', 'hongkong', 'macao', or 'base' (default: current region)
- **Returns**: Converted Traditional Chinese text
### Example:
``` javascript
// Basic conversion (uses current region)
const traditional = STC.toTraditional('这是一个简体中文示例');
console.log(traditional); // Output depends on current region

// Taiwan Traditional
const twText = STC.toTraditional('简体文本', 'taiwan');
console.log(twText); // '簡體文本' with Taiwan-specific characters (衛, 線, 著)

// Hong Kong Traditional
const hkText = STC.toTraditional('简体文本', 'hongkong');
console.log(hkText); // '簡體文本' with Hong Kong-specific characters (衞, 綫, 着)

// Macao Traditional
const moText = STC.toTraditional('简体文本', 'macao');
console.log(moText); // '簡體文本' with Macao-specific characters (衞, 鋭, 閲)

// Handles mixed content
const mixed = STC.toTraditional('Hello 世界, 这是一个test', 'taiwan');
console.log(mixed); // 'Hello 世界, 這是一個test'

// Returns empty string for falsy input
console.log(STC.toTraditional('')); // ''
console.log(STC.toTraditional(null)); // ''
console.log(STC.toTraditional(undefined)); // ''
```

### toSimplified(text, region) Converts Traditional Chinese from a specific region to Simplified Chinese.
- **Parameters**:
    1. text (String): The Simplified Chinese text to convert
    2. region (String, optional): Target region - 'taiwan', 'hongkong', 'macao', or 'base' (default: current region)
- **Returns**: Converted Traditional Chinese text
Example:
``` javascript
// Basic conversion (uses current region)
const traditional = STC.toTraditional('这是一个简体中文示例');
console.log(traditional); // Output depends on current region

// Taiwan Traditional
const twText = STC.toTraditional('简体文本', 'taiwan');
console.log(twText); // '簡體文本' with Taiwan-specific characters (衛, 線, 著)

// Hong Kong Traditional
const hkText = STC.toTraditional('简体文本', 'hongkong');
console.log(hkText); // '簡體文本' with Hong Kong-specific characters (衞, 綫, 着)

// Macao Traditional
const moText = STC.toTraditional('简体文本', 'macao');
console.log(moText); // '簡體文本' with Macao-specific characters (衞, 鋭, 閲)

// Handles mixed content
const mixed = STC.toTraditional('Hello 世界, 这是一个test', 'taiwan');
console.log(mixed); // 'Hello 世界, 這是一個test'

// Returns empty string for falsy input
console.log(STC.toTraditional('')); // ''
console.log(STC.toTraditional(null)); // ''
console.log(STC.toTraditional(undefined)); // ''
```

### toSimplified(text, region) Converts Traditional Chinese from a specific region to Simplified Chinese.
- **Parameters**:
    1. text (String): The Traditional Chinese text to convert
    2. region (String, optional): Source region - 'taiwan', 'hongkong', 'macao', or 'base' (default: current region)
- **Returns**: Converted Simplified Chinese text
Example:
``` javascript
// Taiwan Traditional to Simplified
const simplified = STC.toSimplified('這是一個繁體中文示例', 'taiwan');
console.log(simplified); // '这是一个繁体中文示例'

// Hong Kong Traditional to Simplified
const hkSimplified = STC.toSimplified('衞生防護中心', 'hongkong');
console.log(hkSimplified); // '卫生防护中心'

// Handles edge cases
const withNumbers = STC.toSimplified('第1個測試項目', 'taiwan');
console.log(withNumbers); // '第1个测试项目'

// Preserves punctuation and symbols
const withPunctuation = STC.toSimplified('你好，世界！「引號」測試', 'taiwan');
console.log(withPunctuation); // '你好，世界！「引号」测试'
```

### convertBetweenRegions(text, fromRegion, toRegion) Converts text directly between two regional variants.
- **Parameters**:
    1. text (String): The text to convert
    2. fromRegion (String): Source region ('taiwan', 'hongkong', 'macao')
    3. toRegion (String): Target region ('taiwan', 'hongkong', 'macao')
- **Returns**: Text converted to target regional variant
Example:
``` javascript
// Taiwan to Hong Kong conversion
const twToHk = STC.convertBetweenRegions('這是台灣繁體', 'taiwan', 'hongkong');
console.log(twToHk); // '這是香港繁體' with appropriate character changes

// Hong Kong to Macao conversion
const hkToMo = STC.convertBetweenRegions('香港繁體', 'hongkong', 'macao');
console.log(hkToMo); // Appropriate regional character adjustments
```

## Region Management Functions

### setRegion(region) Sets the current default region.
- **Parameters**:
    1. region (String): Region to set - 'base', 'taiwan', 'hongkong', or 'macao'
- **Returns**: Boolean indicating success
Examples:
``` javascript
// Set Taiwan as default region
const success = STC.setRegion('taiwan');
if (success) {
    console.log('Region set to Taiwan');
}

// All subsequent conversions use Taiwan region
const text = STC.toTraditional('简体文本'); // Uses Taiwan mapping
```

### getRegion() Gets the current default region.
- **Returns**: Current region string
Examples:
``` javascript
const currentRegion = STC.getRegion();
console.log(`Current region: ${currentRegion}`); // 'taiwan', 'hongkong', 'macao', or 'base'
```

### getSupportedRegions() Gets all supported regions.
- **Returns**: Array of supported region strings
Examples:
``` javascript
const regions = STC.getSupportedRegions();
console.log('Supported regions:', regions); // ['base', 'taiwan', 'hongkong', 'macao']
```

### detectRegion(text) Detects the most likely region of the given Traditional Chinese text.
- **Parameters**:
    1. text (String): Traditional Chinese text to analyze
- **Returns**: Detected region string or null if cannot determine
Examples:
``` javascript
const region1 = STC.detectRegion('這是台灣繁體文字');
console.log(region1); // 'taiwan'

const region2 = STC.detectRegion('衞生防護中心報告');
console.log(region2); // 'hongkong'

const region3 = STC.detectRegion('鋭利閲讀');
console.log(region3); // 'macao'
```
## Dictionary Management Functions

### getDictionarySize(region) Gets the size of the specified dictionary.
- **Parameters**:
    1. region (String, optional): Region to check - 'base', 'taiwan', 'hongkong', or 'macao' (default: current merged dictionary)
- **Returns**: Number of entries in the dictionary
Examples:
``` javascript
// Get base dictionary size
const baseSize = STC.getDictionarySize('base');
console.log(`Base dictionary: ${baseSize} entries`);

// Get Taiwan region dictionary size
const twSize = STC.getDictionarySize('taiwan');
console.log(`Taiwan dictionary: ${twSize} entries`);

// Get merged dictionary size (base + current region)
const mergedSize = STC.getDictionarySize();
console.log(`Merged dictionary: ${mergedSize} entries`);
```
### extendDictionary(mappings) Extends the base dictionary with new mappings.
- **Parameters**:
    1. mappings (Object): Key-value pairs of Simplified→Traditional character mappings
- **Returns**: Boolean indicating success
Examples:
``` javascript
// Add domain-specific terms
STC.extendDictionary({
    '软件': '軟體',
    '博客': '部落格',
    '鼠标': '滑鼠',
    '优盘': '隨身碟',
    '网吧': '網咖'
});

// New mappings are available immediately
const result = STC.toTraditional('我去网吧用鼠标拷贝文件到优盘', 'taiwan');
console.log(result); // '我去網咖用滑鼠拷貝文件到隨身碟'
```
### addRegionalMapping(region, mappings) Adds mappings to a specific region's dictionary.
- **Parameters**:
    1. region (String): Target region ('taiwan', 'hongkong', 'macao')
    2. mappings (Object): Key-value pairs of Simplified→Traditional character mappings
- **Returns**: Boolean indicating success
Examples:
``` javascript
// Add Taiwan-specific mappings
STC.addRegionalMapping('taiwan', {
    '优化': '優化',
    '屏幕': '螢幕',
    '视频': '影片'
});

// Add Hong Kong-specific mappings
STC.addRegionalMapping('hongkong', {
    '的': '嘅',
    '和': '同',
    '吗': '嗎'
});

// Verify mappings work
const twText = STC.toTraditional('优化屏幕视频', 'taiwan');
console.log(twText); // '優化螢幕影片'
```
### getBaseDictionary() Gets a read-only copy of the base dictionary.
- **Returns**: Object containing base dictionary mappings
Examples:
``` javascript
const baseDict = STC.getBaseDictionary();
console.log('Base dictionary entries:', Object.keys(baseDict).length);

// Check specific mapping
if (baseDict['为']) {
    console.log('"为" maps to:', baseDict['为']);
}
```
### getCurrentDictionary(region) Gets the merged dictionary for a specific region.
- **Parameters**:
    1. region (String, optional): Region to get dictionary for (default: current region)
- **Returns**: Object containing merged dictionary mappings
Examples:
``` javascript
// Get Taiwan merged dictionary
const twDict = STC.getCurrentDictionary('taiwan');
console.log('Taiwan dictionary entries:', Object.keys(twDict).length);

// Get current region dictionary
const currentDict = STC.getCurrentDictionary();
console.log('Current dictionary entries:', Object.keys(currentDict).length);
```

## DOM Element Conversion Functions

### convertElementToTraditional(element, region) Converts all text content within a DOM element to Traditional Chinese.
- **Parameters**:
    1. element (HTMLElement|String): DOM element or CSS selector
    2. region (String, optional): Target region (default: current region)
- **Returns**: Boolean indicating success
Examples:
``` javascript
// Convert specific element using reference
const myDiv = document.getElementById('content');
const success1 = STC.convertElementToTraditional(myDiv, 'taiwan');
console.log(`Conversion ${success1 ? 'succeeded' : 'failed'}`);

// Convert using CSS selector
const success2 = STC.convertElementToTraditional('.article-content', 'hongkong');
console.log(`Conversion ${success2 ? 'succeeded' : 'failed'}`);

// Convert multiple elements
STC.convertBySelector('.blog-post', true, 'macao');
```
### convertElementToSimplified(element, region) Converts all text content within a DOM element to Simplified Chinese.
- **Parameters**:
    1. element (HTMLElement|String): DOM element or CSS selector
    2. region (String, optional): Source region for Traditional text (default: current region)
- **Returns**: Boolean indicating success
Examples:
``` javascript
// Convert specific element
STC.convertElementToSimplified('#traditional-content', 'taiwan');

// Handle conversion result
const element = document.querySelector('.user-content');
if (STC.convertElementToSimplified(element, 'hongkong')) {
    console.log('Content converted successfully');
} else {
    console.error('Failed to convert content');
}

// Real-world usage in language toggle
function switchToSimplified() {
    const mainContent = document.querySelector('main');
    const sidebar = document.querySelector('.sidebar');
    
    STC.convertElementToSimplified(mainContent, 'taiwan');
    STC.convertElementToSimplified(sidebar, 'taiwan');
}
```
### convertBodyToTraditional(region) Converts the entire document body to Traditional Chinese.
- **Parameters**:
    1. region (String, optional): Target region (default: current region)
Examples:
``` javascript
// Convert entire page to Taiwan Traditional
STC.convertBodyToTraditional('taiwan');

// Convert to Hong Kong Traditional
STC.convertBodyToTraditional('hongkong');

// Usage in language switching
document.getElementById('tw-btn').addEventListener('click', function() {
    STC.convertBodyToTraditional('taiwan');
    localStorage.setItem('language-preference', 'traditional-tw');
});
```
### convertBodyToSimplified(region) Converts the entire document body to Simplified Chinese.
- **Parameters**:
    1. region (String, optional): Source region for Traditional text (default: current region)
Examples:
``` javascript
// Initial page load based on user preference
document.addEventListener('DOMContentLoaded', function() {
    const pref = localStorage.getItem('language-preference');
    if (pref === 'simplified') {
        STC.convertBodyToSimplified();
    } else if (pref === 'traditional-tw') {
        STC.convertBodyToTraditional('taiwan');
    }
});

// Integration with existing systems
function switchToSimplifiedWithNotification() {
    STC.convertBodyToSimplified('taiwan');
    
    const notification = document.createElement('div');
    notification.textContent = '已切换至简体中文';
    notification.className = 'language-notification';
    document.body.appendChild(notification);
    
    setTimeout(() => notification.remove(), 2000);
}
```
### convertBySelector(selector, toTraditional, region) Converts all elements matching a CSS selector.
- **Parameters**:
    1. selector (String): CSS selector string
    2. toTraditional (Boolean): true for Simplified→Traditional, false for Traditional→Simplified
    3. region (String, optional): Target or source region (default: current region)
- **Returns**: Number of elements converted
Examples:
``` javascript
// Convert all articles to Taiwan Traditional
const count1 = STC.convertBySelector('article', true, 'taiwan');
console.log(`Converted ${count1} articles`);

// Convert all comments to Simplified (from Hong Kong Traditional)
const count2 = STC.convertBySelector('.comment', false, 'hongkong');
console.log(`Converted ${count2} comments`);

// Complex selectors
STC.convertBySelector('section.content:not(.code-sample)', true, 'macao');

// Progressive conversion for large pages
function convertPageSections() {
    const sections = ['header', 'nav', 'main', 'aside', 'footer'];
    
    sections.forEach(selector => {
        const count = STC.convertBySelector(selector, true, 'taiwan');
        console.log(`Converted ${count} ${selector} elements`);
    });
}
```

## Configuration Functions

### config(options) Configures library settings at runtime.
- **Parameters**:
    1. options (Object): Configuration object with optional properties:
         1. debug (Boolean): Enable/disable debug logging
         2. excludeTags (Array): HTML tags to exclude from conversion
         3. currentRegion (String): Set default region
         4. dictionary (Object): Add dictionary mappings
         5. performance.enableMonitoring (Boolean): Enable performance monitoring
- **Returns**: Current configuration object
Examples:
``` javascript
// Enable debug mode and performance monitoring
STC.config({
    debug: true,
    excludeTags: ['SCRIPT', 'STYLE', 'CODE', 'PRE', 'INPUT', 'TEXTAREA'],
    performance: {
        enableMonitoring: true
    }
});

// Set default region through config
STC.config({
    currentRegion: 'taiwan'
});

// Add custom mappings through config
STC.config({
    dictionary: {
        base: {
            '的': '嘅',  // Hong Kong variant
            '和': '同'   // Cantonese usage
        }
    }
});

// Get current configuration
const currentConfig = STC.config();
console.log('Current config:', currentConfig);
```

### clearCache() Clears internal caches for improved memory management.
Examples:
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

## Performance Functions 
### getPerformanceStats() Gets performance statistics.
- **Returns**: Object containing performance data
Examples:
``` javascript
// Enable performance monitoring first
STC.config({ performance: { enableMonitoring: true } });

// Perform some conversions
STC.toTraditional('测试文本', 'taiwan');
STC.toSimplified('測試文本', 'taiwan');

// Get statistics
const stats = STC.getPerformanceStats();
console.log('Performance stats:', stats);
// {
//     conversionCount: 2,
//     totalTime: 5,
//     averageTime: 2.5
// }
```
### getDictionaryStats() Gets dictionary statistics.
- **Returns**: Object containing dictionary size information
Examples:
``` javascript
const stats = STC.getDictionaryStats();
console.log('Dictionary stats:', stats);
// {
//     base: 2500,
//     regions: {
//         taiwan: 45,
//         hongkong: 35,
//         macao: 40
//     }
// }
```
## Utility Properties

### version Library version string (read-only).
Examples:
``` javascript
// Check version
console.log(`Using SimplifiedTraditionalConverter v${STC.version}`);

// Version comparison
if (STC.version < '1.1.0') {
    console.warn('Consider updating to latest version');
}

// Application info
const appInfo = {
    name: 'MyApp',
    converterVersion: STC.version,
    currentRegion: STC.getRegion()
};
console.table(appInfo);
```

## Regional Character Differences 
The library handles regional character variations automatically:
    1. Character: 卫  线  着  说  锐  阅  酝  钩  你
    2. Taiwan: 衛  線  著  說  銳  閱  醞  鉤  妳
    3. HongKong: 衛  綫  着  說  銳  閱  醞  鈎  你
    4. Macao:  衛  綫  着  説  鋭  閱  醞  鈎  你
    
## Browser Compatibility
The library is fully compatible with:
### Desktop Browsers
- **Internet Explorer 9+**
- **Microsoft Edge (all versions)**
- **Google Chrome 23+**
- **Mozilla Firefox 21+**
- **Apple Safari 6.1+**
- **Opera 15+**
### Mobile Browsers
- **iOS Safari 7+**
- **Android Browser 4.4+**
- **Chrome for Android 30+**
- **Firefox for Android 30+**
### Smart TV Browsers
- WebKit-based TV browsers
- Samsung Smart TV browsers
### Performance Tips
- **Cache Results: Store converted results if content is static**
- **Selective Conversion: Use convertElementToTraditional() instead of converting the entire body when possible**
- **Batch Processing: For large documents, process in chunks**
- **Avoid Over-conversion: Use excludeTags to skip non-text content**

## License
MIT License - see LICENSE file for details.

## Support 
For issues, feature requests, or contributions:
    1. GitHub Issues: Open an issue in the repository
    2. Documentation: Check the demo.html file for working examples
    3. Community: Join our discussion forum
    
## Contributing
- Fork the repository
- Create a feature branch
- Add tests for new functionality
- Ensure all tests pass
- Submit a pull request

## Acknowledgments
- Community contributors for dictionary improvements

Version: 1.1.0
Last Updated: 2025
Browser Support: IE9+ and all modern browsers
License: MIT
