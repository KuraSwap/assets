# Token Listing Guide

Welcome to the KuraSwap token listing repository! This guide will help you add your token to our tokenlist.

## Quick Start

To add your token to KuraSwap, you need to:
1. Add token information to `tokenlist.json`
2. Add your token logo to the `assets` folder

## Token Information Format

Add your token to the `tokens` array in `tokenlist.json`:

```json
{
  "chainId": 1329,
  "name": "Your Token Name",
  "symbol": "SYMBOL",
  "address": "0x...", 
  "decimals": 18
}
```

### Required Fields
- **chainId**: Must be `1329` (SEI Network)
- **name**: Full token name
- **symbol**: Token ticker symbol
- **address**: Token contract address (lowercase)
- **decimals**: Token decimals (usually 6 or 18)

## Logo Requirements

### File Specifications
- **Format**: PNG
- **Size**: 256x256px recommended
- **File name**: Must be `logo.png`
- **Location**: `/assets/{token_address}/logo.png`

### Logo Guidelines
- Clear background preferred (transparent PNG)
- High quality, no pixelation
- Centered design
- No text unless part of logo design

## Submission Process

### How to Submit via Pull Request
1. Fork this repository
2. Clone your fork locally
3. Add your token info to `tokenlist.json` (keep alphabetical order if possible)
4. Create folder: `assets/{your_token_address}/`
5. Add your `logo.png` to the folder
6. Commit your changes with message: `Add [TOKEN_SYMBOL] token`
7. Push to your fork
8. Create a Pull Request to our `main` branch

### PR Title Format
`Add [TOKEN_SYMBOL] - [Token Name]`

Example: `Add WETH - Wrapped ETH`

## Example

Adding WETH token:

1. **Update tokenlist.json:**
```json
{
  "chainId": 1329,
  "name": "WETH",
  "symbol": "WETH",
  "address": "0x160345fc359604fc6e70e3c5facbde5f7a9342d8",
  "decimals": 18
}
```

2. **Create logo directory:**
```
assets/0x160345fc359604fc6e70e3c5facbde5f7a9342d8/logo.png
```

## Validation Checklist

Before submitting:
- [ ] Token is deployed on SEI Network (chainId: 1329)
- [ ] Logo is PNG format
- [ ] Logo file is named exactly `logo.png`
- [ ] Logo is in correct directory path
- [ ] JSON syntax is valid