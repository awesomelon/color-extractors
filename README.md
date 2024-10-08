# Image-Colors

Image-Colors is a powerful and flexible library for extracting dominant colors from images. It uses k-means clustering to identify and analyze the main colors in an image.

## Key Features

- Extract dominant colors from images
- Option to filter similar colors
- Support for both browser and Node.js environments
- Written in TypeScript for type safety
- Support for various image formats (PNG, JPG, etc.)

## Installation

You can install Image-Colors using npm:

```bash
npm install @j-ho/image-colors
```

## Usage

### Browser Environment

```typescript
import { createColorExtractor } from '@j-ho/image-colors/browser';

(async () => {
  const colorExtractor = await createColorExtractor();
  
  const img = document.getElementById('myImage');
  const { colors, dominantColor } = await colorExtractor.extractColors({
    imageSource: img,
    k: 5,
    sampleRate: 0.1,
    onFilterSimilarColors: true,
    useHex: true
  });

  console.log('Dominant Color:', dominantColor);
  console.log('Other Colors:', colors);    
})();

```

### Node.js Environment

```typescript
import { createColorExtractor } from '@j-ho/image-colors/node';

async function handleUploads(req, res) {
    const colorExtractor = await createColorExtractor();
    
    const result = await colorExtractor.extractColors({
        imageSource: req.file.path,
        k: 5,
        sampleRate: 0.1,
        onFilterSimilarColors: true,
        useHex: true
    });

    res.json({ colors, dominantColor });
}
```

## API

### createColorExtractor(environment: 'browser' | 'node')

Creates a ColorExtractor instance suitable for your environment.

**extractColors(options)** Extracts colors from an image.

- **Options:**
  - `imageSource`: Image source (Image object in the browser, file path in Node.js)
  - `k`: Number of colors to extract (default: 5)
  - `sampleRate`: Pixel sampling rate (0-1, default: 0.1)
  - `onFilterSimilarColors`: Whether to filter similar colors (default: false)
  - `useHex`: Whether to return colors in HEX format (default: false)

- **Returns:**
  - `dominantColor`: The most dominant color
  - `colors`: Array of other extracted colors

## License

This project is licensed under the MIT License.

## Contributing

We welcome all forms of contributions, including bug reports, feature suggestions, and pull requests. For major changes, please open an issue first to discuss what you would like to change.