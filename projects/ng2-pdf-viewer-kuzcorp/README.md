# @kuzcorp/ng2-pdf-viewer-kuzcorp

Angular PDF viewer component with PDF.js 5.x support.

This is a forked version of ng2-pdf-viewer updated to work with `pdfjs-dist` version 5.4.0+.

## Installation

```bash
npm install @kuzcorp/ng2-pdf-viewer-kuzcorp pdfjs-dist
```

## Usage

### 1. Import the module

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { PdfViewerModule } from '@kuzcorp/ng2-pdf-viewer-kuzcorp';

import { AppComponent } from './app.component';

@NgModule({
  imports: [BrowserModule, PdfViewerModule],
  declarations: [AppComponent],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

### 2. Use in your component

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: `
    <pdf-viewer
      [src]="pdfSrc"
      [render-text]="true"
      [original-size]="false"
      style="width: 400px; height: 500px">
    </pdf-viewer>
  `
})
export class AppComponent {
  pdfSrc = "https://example.com/sample.pdf";
}
```

### 3. Configure PDF.js Worker (Optional)

By default, the component will use a CDN for the PDF.js worker. To use a local worker file:

```typescript
// In your app component or main.ts
(window as any).pdfWorkerSrc = '/assets/pdf.worker.min.mjs';
(window as any).wasmUrl = '/assets/wasm/'; // Optional: for JPEG2000 support
```

## Options

| Input | Type | Default | Description |
|-------|------|---------|-------------|
| `[src]` | `string \| Uint8Array \| PDFSource` | - | PDF source (URL, ArrayBuffer, or object) |
| `[page]` | `number` | `1` | Current page number |
| `[render-text]` | `boolean` | `true` | Enable text layer rendering |
| `[render-text-mode]` | `RenderTextMode` | `RenderTextMode.ENABLED` | Text rendering mode |
| `[original-size]` | `boolean` | `true` | Use original PDF size |
| `[show-all]` | `boolean` | `true` | Show all pages or single page |
| `[zoom]` | `number` | `1` | Zoom level |
| `[zoom-scale]` | `'page-width' \| 'page-height' \| 'page-fit'` | `'page-width'` | Zoom scale mode |
| `[rotation]` | `number` | `0` | Page rotation (0, 90, 180, 270) |
| `[stick-to-page]` | `boolean` | `false` | Stick to current page |
| `[external-link-target]` | `string` | `'blank'` | External link target |
| `[autoresize]` | `boolean` | `true` | Auto-resize on window resize |
| `[fit-to-page]` | `boolean` | `false` | Fit PDF to page |
| `[show-borders]` | `boolean` | `false` | Show page borders |
| `[c-maps-url]` | `string` | - | Custom CMaps URL |

## Events

| Output | Type | Description |
|--------|------|-------------|
| `(after-load-complete)` | `PDFDocumentProxy` | Emitted when PDF is loaded |
| `(page-rendered)` | `CustomEvent` | Emitted when a page is rendered |
| `(pages-initialized)` | `CustomEvent` | Emitted when pages are initialized |
| `(text-layer-rendered)` | `CustomEvent` | Emitted when text layer is rendered |
| `(error)` | `any` | Emitted on error |
| `(on-progress)` | `PDFProgressData` | Emitted during PDF loading |
| `(pageChange)` | `number` | Emitted when page changes |

## Types

You can import types from the package:

```typescript
import {
  PDFDocumentProxy,
  PDFPageProxy,
  PDFProgressData,
  PDFSource,
  PDFViewerOptions,
  ZoomScale
} from '@kuzcorp/ng2-pdf-viewer-kuzcorp';
```

## Building the Library

To build the library for distribution:

```bash
npm run build:lib
```

The built files will be in `dist/ng2-pdf-viewer-kuzcorp/`.

## Publishing

After building, navigate to the dist folder and publish:

```bash
cd dist/ng2-pdf-viewer-kuzcorp
npm publish
```

Or publish from the root:

```bash
npm publish --workspace=dist/ng2-pdf-viewer-kuzcorp
```

## Requirements

- Angular 16+ or 17+
- pdfjs-dist 5.4.0+
- rxjs 7.0+

## License

MIT
