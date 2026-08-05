# VNAGY Android Mobile Assets

This directory contains Android-specific graphical assets prepared according to
Material Design and Adaptive Icon specifications. Assets include launcher icons,
adaptive icon layers, splash screens, and main screen graphics. For simplicity,
all assets are stored in a single directory, although production environments
should separate launcher, splash, and UI assets into dedicated folders.

## Contents
- Adaptive icon foreground/background (mdpi → xxxhdpi)
- Adaptive icon XML declaration (mipmap-anydpi-v26)
- Launcher icon master (512×512)
- Splash screen assets (mdpi → xxxhdpi)
- Main screen graphics (if present)

## Adaptive Icon Structure
- mipmap-mdpi/
- mipmap-hdpi/
- mipmap-xhdpi/
- mipmap-xxhdpi/
- mipmap-xxxhdpi/
- mipmap-anydpi-v26/ic_launcher.xml

The `mipmap-anydpi-v26` directory contains the adaptive icon XML declaration
referencing foreground and background layers.

## Splash Screen Structure
Splash screen PNGs are included in this directory for convenience. In a full
Android project, splash assets should be placed under drawable-* density folders.

## Licensing
Licensed under **VNAGY CC BY-NC 4.0 Extended License**.  
Short documents may use **VNAGY Minimal License (PSDL‑1.3)**.  
© **Viktorija Nađ, 2026 — All Rights Reserved.**


The full license text is located in the **LICENSE** directory.

## Script: Generate mipmap-anydpi-v26
The following script creates the required directory and places the adaptive icon
XML declaration inside it.

```bash
#!/bin/bash

TARGET_DIR="mipmap-anydpi-v26"

mkdir -p "$TARGET_DIR"

cat <<EOF > "$TARGET_DIR/ic_launcher.xml"
<adaptive-icon xmlns:android="http://schemas.android.com/apk/res/android">
    <background android:drawable="@mipmap/ic_launcher_background"/>
    <foreground android:drawable="@mipmap/ic_launcher_foreground"/>
</adaptive-icon>
EOF



