# VNAGY iOS Asset Specification

This document defines the official VNAGY asset structure for iOS, including
AppIcon.appiconset, splash screens, and export rules. All assets follow the
VNAGY deterministic, minimal, monochrome visual standard.

## 1. Purpose

VNAGY iOS assets provide a consistent, security-focused visual identity across
all iOS builds. The icon and splash pipeline is designed to be:

- deterministic (no implicit visual variation),
- minimal (no decorative noise),
- cross-platform aligned with Android, Windows, and Linux,
- suitable for offline-first security tooling and frameworks.

## 2. Directory Structure

ios/
│
├── AppIcon.appiconset/
│   ├── icon-20.png
│   ├── icon-20@2x.png
│   ├── icon-20@3x.png
│   ├── icon-29.png
│   ├── icon-29@2x.png
│   ├── icon-29@3x.png
│   ├── icon-40.png
│   ├── icon-40@2x.png
│   ├── icon-40@3x.png
│   ├── icon-60@2x.png
│   ├── icon-60@3x.png
│   ├── icon-76.png
│   ├── icon-76@2x.png
│   ├── icon-83.5@2x.png
│   ├── icon-1024.png
│   └── Contents.json
│
├── splash-ios.png
└── readme-ios.md

## 3. Icon Master Source

All iOS icons are generated from a single master file:

- **app-icon-1024.png**
- Resolution: 1024×1024 px
- Format: PNG (no background layer)
- Style: VNAGY monochrome, deterministic grid, no gradients

## 4. iOS Icon Requirements (Industry Standard)

iOS requires multiple fixed-resolution icons. VNAGY follows the official Apple
Human Interface Guidelines:

- 20×20 (1x, 2x, 3x)
- 29×29 (1x, 2x, 3x)
- 40×40 (1x, 2x, 3x)
- 60×60 (2x, 3x)
- 76×76 (1x, 2x)
- 83.5×83.5 (2x)
- 1024×1024 (App Store marketing icon)

All icons must be exported as individual PNG files and placed inside
`AppIcon.appiconset/`.

## 5. Contents.json

The `Contents.json` file defines the mapping between icon files, resolutions,
scale factors, and device idioms (iPhone, iPad, marketing). It is required by
Xcode to correctly assemble the AppIcon asset.

## 6. Splash Screen

`splash-ios.png
