# pixelmatch

Diff images on CPU. Small, fast pixel-level image comparison library for e2e testing.

## Features

- Pixel-by-pixel image comparison
- Customizable threshold and colors for diff output
- Anti-aliasing detection
- Fast and memory efficient

| expected | actual | diff |
| --- | --- | --- |
| ![](test/fixtures/4a.png) | ![](test/fixtures/4b.png) | ![diff](test/fixtures/4diff.png) |

## Getting started

Add library to your package and give Uint8List with RGBA canvas to it somehow.

## Usage

```dart
import 'package:pixelmatch/pixelmatch.dart';
import 'dart:typed_data';

void main() {
  // Prepare your image data as RGBA Uint8Lists
  final img1 = Uint8List(width * height * 4); // First image
  final img2 = Uint8List(width * height * 4); // Second image
  final diff = Uint8List(width * height * 4); // Output diff (or null)

  // Compare images
  final numDiffPixels = pixelmatch(img1, img2, diff, width, height, { 'threshold': 0.1 });

  print('Found $numDiffPixels different pixels');
}
```

#### Options

- `threshold` (default: 0.1): Matching threshold (0 to 1); smaller is more sensitive
- `includeAA` (default: false): Whether to skip anti-aliasing detection
- `alpha` (default: 0.1): Opacity of original image in diff output
- `aaColor` (default: [255, 255, 0]): Color of anti-aliased pixels in diff output
- `diffColor` (default: [255, 0, 0]): Color of different pixels in diff output
- `diffColorAlt` (default: null): Alternative color for dark on light differences
- `diffMask` (default: false): Draw the diff over a transparent background

## Additional information

This is a Dart port of [mapbox/pixelmatch](https://github.com/mapbox/pixelmatch).