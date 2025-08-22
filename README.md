# dokuwiki-plugin-iframeinterwiki
Plugin dokuwiki for iframe using interwiki

## Overview

The iframeinterwiki plugin allows external URLs to be loaded into an iframe in your DokuWiki page using interwiki URI syntax. This plugin extends the standard iframe functionality by supporting interwiki shortcuts defined in your DokuWiki configuration.

**Compatible with DokuWiki:**
- 2025-05-14 "Librarian" and later versions

**Plugin Information:**
- **Author:** Steve Roques
- **Last Updated:** 2025-08-22 (Bug fixes applied)
- **License:** GPL 2
- **Type:** Syntax Plugin
- **Repository:** [https://www.dokuwiki.org/plugin:iframeinterwiki](https://www.dokuwiki.org/plugin:iframeinterwiki)

## Installation

### Automatic Installation
1. Go to your DokuWiki Admin Panel
2. Navigate to Extension Manager
3. Search for "iframeinterwiki"
4. Click Install

### Manual Installation
1. Download the plugin source
2. Extract to your DokuWiki `lib/plugins/` directory
3. The plugin folder structure should be:
   ```
   lib/plugins/iframeinterwiki/
   ├── conf/
   │   ├── default.php          # Default settings
   │   └── metadata.php         # Configuration metadata
   ├── lang/
   │   └── xx/lang.php          # Language files
   ├── syntax.php               # Main plugin script
   └── plugin.info.txt          # Plugin information
   ```

## Usage

### Basic Syntax
```wiki
{{url>http://www.example.com/somepage.html}}
```

### Complete Syntax
```wiki
{{url>someurl width,height noscroll noborder alignment|alternate-text}}
```

### Using Interwiki
```wiki
{{url>personalserver>test.html}}
```

Where `personalserver` is defined in your `conf/interwiki.local.conf` file.

### Parameters

**Size Parameters:**
- `width,height` - Specify dimensions (e.g., `100%,700px` or `800,600`)
- Units supported: `px`, `%`, `em`, `pt`
- Default: width=98%, height=400px

**Display Options:**
- `noscroll` or `noscrollbar` or `noscrolling` - Disable scrollbars
- `noborder` or `noframeborder` - Remove iframe border
- `left` or `right` - Float alignment

**Content:**
- `|alternate-text` - Text shown when iframe cannot load

### Interwiki Integration

The plugin supports interwiki shortcuts using these placeholders:
- `{NAME}` - Replaced by the page name part
- `{URL}` - URL-encoded parameter replacement

Example interwiki configuration in `conf/interwiki.local.conf`:
```
personalserver    http://myserver.com/{NAME}
api               https://api.example.com/embed?url={URL}
```

## Configuration

Access configuration via **Admin Panel → Configuration Settings**

### Available Settings

**JavaScript URLs (`js_ok`)**
- **Default:** `false`
- **Description:** Enable JavaScript URLs in iframes
- **Security Warning:** Never enable this on public wikis - it creates XSS vulnerabilities

## Troubleshooting

### Common Issues

**"Undefined array key" errors:**
- Update to the latest version (2025-08-22 or later)
- Ensure proper syntax: specify units for dimensions (`700px` instead of `700`)

**Iframe not loading:**
- Check if the target URL allows iframe embedding
- Verify interwiki configuration
- Ensure JavaScript URLs are properly configured if needed

**Security considerations:**
- Never enable `js_ok` on public wikis
- Validate external URLs before embedding
- Be cautious with user-generated iframe content

## Examples

### Simple iframe
```wiki
{{url>https://example.com}}
```

### Sized iframe with no scrollbars
```wiki
{{url>https://example.com 800px,600px noscroll noborder}}
```

### Using interwiki with alternate text
```wiki
{{url>docs>api/reference.html 100%,500px|API Documentation}}
```

### Responsive iframe
```wiki
{{url>app>dashboard.php 100%,80vh noscroll|Application Dashboard}}
```

## Support

- **Documentation:** [https://www.dokuwiki.org/plugin:iframeinterwiki](https://www.dokuwiki.org/plugin:iframeinterwiki)
- **Issues:** Report bugs through the DokuWiki plugin system
- **Community:** DokuWiki user forums

## License

This plugin is licensed under GPL 2. See the full license text at [http://www.gnu.org/licenses/gpl.html](http://www.gnu.org/licenses/gpl.html)

## Acknowledgments

Special thanks to Christopher Smith for the original iframe plugin that served as the foundation for this interwiki-enabled version.
