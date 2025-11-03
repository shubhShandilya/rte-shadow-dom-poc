# Rich Text Editor POC - Test Pages

This directory contains test pages for verifying Low Code Automation (LCA) support for CKEditor and Jodit Editor within Shadow DOM.

## 📁 Files

- **`ckeditor-shadow-dom.html`** - CKEditor 5 test page with Shadow DOM implementation
- **`jodit-shadow-dom.html`** - Jodit Editor test page with Shadow DOM implementation
- **`start-server.sh`** - Shell script to quickly start a local HTTP server

## 🚀 Quick Start

### Option 1: Using the provided script

```bash
cd /Users/shubham.shan@browserstack.com/Developer/company/electron-app/products/lcnc/test-pages
./start-server.sh
```

Then open in your browser:
- CKEditor: http://localhost:8080/ckeditor-shadow-dom.html
- Jodit: http://localhost:8080/jodit-shadow-dom.html

### Option 2: Using Python directly

```bash
cd /Users/shubham.shan@browserstack.com/Developer/company/electron-app/products/lcnc/test-pages

# Python 3
python3 -m http.server 8080

# Python 2
python -m SimpleHTTPServer 8080
```

### Option 3: Using Node.js

```bash
npx http-server -p 8080
```

## 🧪 Test Scenarios

Each test page includes:

### 1. **Shadow DOM Editor**
- Editor wrapped in a Web Component with Shadow DOM (open mode)
- Tests LCA's ability to detect and interact with elements inside Shadow DOM
- Verifies selector generation for shadow-piercing

### 2. **Regular DOM Editor**
- Standard editor implementation without Shadow DOM
- Provides baseline comparison for functionality
- Helps identify Shadow DOM-specific issues

### 3. **Multiple Shadow DOM Editors**
- Two separate editors in different shadow roots
- Tests unique element identification
- Verifies LCA can distinguish between similar elements in different shadow contexts

## 🔍 Testing with LCA

### Step 1: Start Recording
1. Open the test page in your LCA recorder
2. Start a new recording session

### Step 2: Perform Actions
Test these interactions:

**Basic Actions:**
- Click toolbar buttons (Bold, Italic, etc.)
- Type text in the editor
- Select and format text
- Use keyboard shortcuts (Ctrl+B, Ctrl+I)

**Advanced Actions:**
- Insert images/tables
- Create lists (ordered/unordered)
- Change text alignment
- Switch to source code view (if available)

**Shadow DOM Specific:**
- Verify element highlighting works in shadow DOM
- Check generated selectors include shadow DOM notation
- Test selector stability across page reloads

### Step 3: Verify Recording
Check the recorded steps for:
- ✅ Presence of `shadowDOMSelectors` array
- ✅ Accurate CSS paths
- ✅ Stable, non-fragile selectors
- ✅ Unique identification of elements

### Step 4: Playback Test
1. Run the recorded test immediately
2. Refresh the page and run again
3. Close browser, reopen, and run again

All three should succeed for full compatibility.

## 🛠️ Built-in Verification Tools

Each test page includes these JavaScript functions accessible via browser console or UI buttons:

### `checkShadowDOM()`
Verifies Shadow DOM is properly implemented and accessible.

```javascript
checkShadowDOM()
```

**Output:**
- Shadow Root presence
- Shadow mode (open/closed)
- Child element count

### `inspectElements()`
Analyzes elements inside and outside Shadow DOM.

```javascript
inspectElements()
```

**Output:**
- CSS selectors
- Button counts
- Editable area detection
- Element attributes

### `getEditorContent()`
Retrieves content from all editors on the page.

```javascript
getEditorContent()
```

**Output:**
- HTML content from each editor
- Useful for verifying text input worked correctly

### `testToolbarInteraction()` (Jodit only)
Demonstrates programmatic interaction with Shadow DOM toolbar buttons.

```javascript
testToolbarInteraction()
```

**Output:**
- Button detection status
- Selector paths
- Clickability verification

## 📊 What to Test (Feature Checklist)

Use these test pages to verify the following features from your Confluence doc:

### Element Selection
- [ ] CSS selector generation
- [ ] XPath generation (if LCA supports it)
- [ ] Unique element identification
- [ ] Selector stability across sessions

### Shadow DOM
- [ ] Element detection in Shadow DOM
- [ ] Recording in Shadow DOM
- [ ] Selector includes shadow-piercing syntax
- [ ] Playback works reliably

### Basic Recording
- [ ] Click events on toolbar buttons
- [ ] Double-click events
- [ ] Right-click (context menu)
- [ ] Hover events

### Text Input
- [ ] Type text in editor
- [ ] Clear text
- [ ] Select all text
- [ ] Copy/Paste text

### Rich Text Formatting
- [ ] Bold text
- [ ] Italic text
- [ ] Underline text
- [ ] Font size/family change
- [ ] Text color change

### Toolbar Actions
- [ ] Click toolbar buttons
- [ ] Dropdown menu selection
- [ ] Modal/Dialog interactions

### Keyboard Shortcuts
- [ ] Ctrl/Cmd+B (Bold)
- [ ] Ctrl/Cmd+I (Italic)
- [ ] Ctrl/Cmd+Z (Undo)
- [ ] Ctrl/Cmd+Y (Redo)

## 🐛 Debugging Tips

### If editors don't load:
1. Check browser console for errors
2. Ensure you're serving via HTTP (not file://)
3. Check if CDN resources are accessible
4. Try opening in incognito/private mode

### If Shadow DOM isn't detected:
```javascript
// Run in browser console
document.querySelectorAll('*').forEach(el => {
  if (el.shadowRoot) {
    console.log('Shadow DOM found:', el);
  }
});
```

### If LCA can't detect elements:
1. Check if shadow mode is 'open' (not 'closed')
2. Verify your LCA version supports Shadow DOM
3. Review `getShadowDOMSelectors.js` in your LCA codebase
4. Check browser DevTools to manually inspect shadow elements

## 📝 Expected Selector Format

When LCA records actions in Shadow DOM, you should see selectors like:

```javascript
{
  "selector": "button.bold",
  "shadowDOMSelectors": [
    {
      "selectorType": "css",
      "selectorPath": "ckeditor-shadow-wrapper#shadow-editor-1",
      "htmlElementType": "shadowElement",
      "tagName": "CKEDITOR-SHADOW-WRAPPER"
    }
  ]
}
```

## 🎯 Real-World Alternatives

If you need to test on actual production sites with Shadow DOM:

### Salesforce Lightning
- URL: Any Salesforce Lightning Experience page
- Shadow DOM: ✅ Yes (enforced)
- Access: Requires Salesforce login
- Rich Text: Often uses custom editors

### Polymer Project Examples
- URL: https://www.polymer-project.org/
- Shadow DOM: ✅ May contain examples
- Access: Public

### Web Components Examples
- URL: https://webcomponents.dev/
- Shadow DOM: ✅ Most examples use it
- Access: Public

## 📞 Support

For questions or issues:
1. Check browser console for JavaScript errors
2. Review LCA documentation for Shadow DOM support
3. Test with regular DOM version first to isolate Shadow DOM issues
4. Capture screenshots/videos of failures for debugging

---

**Last Updated:** November 3, 2025
**Created By:** LCA Team
**Purpose:** POC for Rich Text Editor Shadow DOM Support
