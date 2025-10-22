# Image Retrieval and Processing Workflow

This document outlines the proper workflow for finding, verifying, and using images from archives in Slidev presentations.

## Step 1: Finding Images in Archives

### Recommended Archives
- **Wikimedia Commons**: https://commons.wikimedia.org/
- **Dutch RKD Archive**: https://research.rkd.nl/en
- **Rijksmuseum**: https://www.rijksmuseum.nl/en/search

### Search Strategy
1. Use simple search terms (e.g., "waffle" or "wafel" for Dutch archives)
2. Most archive content is already historical, so no need to add "historical" to searches
3. Look for paintings, engravings, photographs, or artifacts
4. Check licensing - prefer Public Domain or CC0 images

## Step 2: Getting the Correct Image URL

### ⚠️ CRITICAL: Avoid Thumbnail URLs

**DO NOT use thumbnail URLs** - they often return 404 errors.

❌ **WRONG** - Thumbnail URL format:
```
https://upload.wikimedia.org/wikipedia/commons/thumb/0/0f/filename.jpg/1024px-filename.jpg
```

✅ **CORRECT** - Direct file URL format:
```
https://upload.wikimedia.org/wikipedia/commons/0/0f/filename.jpg
```

### How to Find the Correct URL

1. Go to the file page on Wikimedia Commons (e.g., `File:Artwork_name.jpg`)
2. Use WebFetch to extract the direct download URL
3. Look for patterns like: `https://upload.wikimedia.org/wikipedia/commons/[hash]/[hash]/filename.jpg`
4. The URL should NOT contain `/thumb/` in the path

## Step 3: Verify Image URLs

**Always verify URLs work before adding to slides:**

```bash
curl -I "https://upload.wikimedia.org/wikipedia/commons/[path]/image.jpg"
```

Expected response: `HTTP/2 200`

If you get `HTTP/2 404`, the URL is incorrect - get the direct file URL instead.

## Step 4: Get Accurate Dating Information

### Use WebFetch to find exact dates:

1. Visit the Wikimedia Commons file page
2. Look for "Date" field in the metadata
3. Record exact year when available
4. Use "c." (circa) for approximate dates
5. Use date ranges when exact year is unknown (e.g., "c. 1850-1882")

### Citation Format Examples:
- Exact year: `Artist Name (1762)`
- Circa: `Artist Name (c. 1650)`
- Date range: `Artist Name (c. 1850-1882)`
- Century only (last resort): `Artist Name (17th century)`

## Step 5: Adding Images to Slidev

### Full Page Image:
```markdown
---
layout: image
image: https://upload.wikimedia.org/wikipedia/commons/[path]/image.jpg
---

# `Artwork Title`
*Artist Name (Year)*
```

### Image on Right Side:
```markdown
---
layout: image-right
image: https://upload.wikimedia.org/wikipedia/commons/[path]/image.jpg
---

# Slide Title

*"Artwork Title"*
Artist Name (Year)

Additional context text
```

## Step 6: Test Locally

1. Ensure dev server is running with hot reload: `npm run dev`
2. Server automatically reloads when files change
3. Check images display correctly in browser at http://localhost:3030/
4. If images don't load, verify URLs with curl
5. Hard refresh browser (Cmd+Shift+R) if needed

## Common Issues and Solutions

### Images Not Loading
- **Check URL format**: Remove `/thumb/` and resize parameters
- **Verify with curl**: Test URL returns HTTP 200
- **Check browser console**: Look for CORS or network errors
- **Hard refresh**: Clear browser cache

### Wrong Image Dimensions
- Use full-resolution URLs, Slidev will resize automatically
- Avoid specifying pixel dimensions in URL

### Attribution Issues
- Always include artist name and date
- Use exact dates when available
- Cite the source archive if relevant

## Best Practices

1. ✅ Test every image URL with curl before committing
2. ✅ Use direct file URLs, never thumbnails
3. ✅ Include accurate dating information
4. ✅ Verify images display correctly locally
5. ✅ Keep aspect ratios in mind for layouts
6. ✅ Use Public Domain or properly licensed images only

## Quick Verification Checklist

- [ ] Image URL is direct (no `/thumb/` in path)
- [ ] URL verified with curl (returns HTTP 200)
- [ ] Exact or approximate date included in citation
- [ ] Artist/creator properly credited
- [ ] Image displays correctly in local dev server
- [ ] Licensing allows use (Public Domain/CC0 preferred)

---

**Last Updated**: October 2025
