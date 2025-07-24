# How to Export Marp Slides to PDF

## Method 1: Using VS Code with Marp Extension (Recommended)

### Prerequisites
1. Install VS Code: https://code.visualstudio.com/
2. Install Marp for VS Code extension:
   - Open VS Code
   - Go to Extensions (Ctrl+Shift+X or Cmd+Shift+X)
   - Search for "Marp for VS Code"
   - Install the extension by marp-team

### Steps to Export
1. Open your markdown file (`prompt-engineering-slides.md`)
2. Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (Mac)
3. Type "Marp: Export Slide Deck..."
4. Choose "PDF" as the output format
5. Select where to save the PDF file

### Alternative VS Code Commands
- `Marp: Export Slide Deck...` - Export to various formats
- `Marp: Open Preview` - Preview slides in browser
- `Marp: Open Preview to the Side` - Preview alongside editor

## Method 2: Using Marp CLI

### Install Marp CLI
```bash
# Using npm (requires Node.js)
npm install -g @marp-team/marp-cli

# Using Homebrew (Mac)
brew install marp-cli

# Using Chocolatey (Windows)
choco install marp-cli
```

### Export Commands
```bash
# Basic PDF export
marp slides/prompt-engineering-slides.md --pdf

# Export with custom filename
marp slides/prompt-engineering-slides.md --pdf --output prompt-engineering.pdf

# Export with custom theme
marp slides/prompt-engineering-slides.md --pdf --theme default

# Export with custom CSS
marp slides/prompt-engineering-slides.md --pdf --css custom.css
```

## Method 3: Using Marp Core (Programmatic)

### Install Marp Core
```bash
npm install @marp-team/marp-core
```

### Create Export Script
Create a file called `export.js`:
```javascript
const { Marp } = require('@marp-team/marp-core')
const fs = require('fs')

const marp = new Marp()
const markdown = fs.readFileSync('slides/prompt-engineering-slides.md', 'utf8')
const { html, css } = marp.render(markdown)

// Save HTML
fs.writeFileSync('output.html', html)

// You can then convert HTML to PDF using tools like Puppeteer
```

## Method 4: Online Marp Editor

1. Go to https://marp.app/
2. Copy your markdown content
3. Paste into the editor
4. Click "Export" → "PDF"

## Method 5: Using Docker

### Run Marp CLI in Docker
```bash
# Pull Marp CLI image
docker pull marpteam/marp-cli

# Export PDF
docker run --rm -v $PWD:/home/marp/app/ marpteam/marp-cli slides/prompt-engineering-slides.md --pdf
```

## Troubleshooting

### Common Issues

1. **Fonts not rendering correctly**
   - Install required fonts on your system
   - Use web-safe fonts in your CSS

2. **Images not showing**
   - Use absolute URLs for images
   - Or place images in the same directory as markdown

3. **PDF too large**
   - Optimize images before including
   - Use compressed image formats

4. **Layout issues**
   - Check your CSS for conflicts
   - Ensure proper Marp directives

### Best Practices

1. **Test your slides** in preview mode before exporting
2. **Use relative paths** for local images
3. **Optimize images** to reduce file size
4. **Check PDF quality** after export
5. **Keep backup** of your markdown file

## Advanced Configuration

### Custom Themes
Create a CSS file for custom styling:
```css
/* custom-theme.css */
section {
  background-color: #f0f0f0;
  color: #333;
  font-family: 'Arial', sans-serif;
}

h1 {
  color: #2c3e50;
}
```

### Export with Custom Theme
```bash
marp slides/prompt-engineering-slides.md --pdf --theme-set custom-theme.css
```

### Multiple Formats
```bash
# Export to multiple formats at once
marp slides/prompt-engineering-slides.md --pdf --html --pptx
```

## Quick Export Script

Create a shell script for easy export:
```bash
#!/bin/bash
# export.sh

echo "Exporting slides to PDF..."
marp slides/prompt-engineering-slides.md --pdf --output "prompt-engineering-$(date +%Y%m%d).pdf"
echo "Export completed!"
```

Make it executable:
```bash
chmod +x export.sh
./export.sh
``` 