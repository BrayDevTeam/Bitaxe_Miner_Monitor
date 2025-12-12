# Image Folder Structure

This folder contains the background images used for different card types in the BitAxe Mining Dashboard.

## Folder Structure

```
images/
├── cards/
│   ├── hashrate/          - Background image for the Hashrate card
│   ├── temperature/       - Background image for Temperature card
│   ├── vr-temperature/    - Background image for VR Temperature card
│   ├── power/             - Background image for Power Consumption card
│   ├── blocks-found/      - Background image for Blocks Found card
│   └── info/              - Background image for all info cards
└── charts/
    ├── hashrate/          - Background image for Hashrate chart
    ├── temperature/       - Background image for Temperature chart
    └── vr-temperature/    - Background image for VR Temperature chart
```

## How to Use

1. **Place your image file** in the appropriate folder with the filename `background.jpg`
   - Example: `images/cards/hashrate/background.jpg`
   - Example: `images/charts/temperature/background.jpg`

2. **Supported image formats**: JPG, JPEG, PNG, GIF, WebP

3. **Image sizing**: Images will automatically stretch to fill the card/chart area (100% width and height)

4. **Fallback colors**: If an image is not found, the cards will fall back to their default gradient colors

## Notes

- If you want to use a different filename, you'll need to update the CSS in `index.html`
- Images are automatically resized to fit the card dimensions
- A semi-transparent overlay is applied to ensure text readability
- Text shadows are added to make text more visible over images
