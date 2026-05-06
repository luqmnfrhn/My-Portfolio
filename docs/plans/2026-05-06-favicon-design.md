# Favicon Design: LF Logo

## Goal

Add browser tab icon to all portfolio pages using existing `logo_lf.png`.

## Approach

PNG favicon — add `<link rel="icon">` tag to each HTML file's `<head>`.

## Files to Update

- `index.html`
- `mediviron.html`
- `senada.html`
- `smartschool.html`
- `project.html`

## Change

```html
<link rel="icon" type="image/png" href="logo_lf.png">
```

Insert after existing `<link>` tags in `<head>`. No file moves or conversions needed.
