# Creating Links That Open in a New Tab

Use HTML anchor tags to open links in a new browser tab.

## Steps

1. Use the HTML `<a>` tag instead of Markdown link syntax.

    ```
    <a href="URL" target="_blank">Link text</a>
    ```

2. Add security attributes.

    ```
    <a href="URL"
        target="_blank"
        rel="noopener noreferrer">
        Link text
    </a>
    ```

3. Replace `URL` and `Link text` with your values.

## Examples

### External link

```
<a href="https://youtube.com/"
   target="_blank"
   rel="noopener noreferrer">
   Watch on YouTube
</a>
```

### Internal link

```
<a href="../getting-started/"
   target="_blank"
   rel="noopener noreferrer">
   Open getting started guide
</a>
```

### Display URL as text

```
<a href="https://example.com"
   target="_blank"
   rel="noopener noreferrer">
   https://example.com
</a>
```

### Use inside a list

```
1. Go to the official website:
   <a href="https://simplenote.com/"
      target="_blank"
      rel="noopener noreferrer">
      Visit Simplenote
   </a>
```

## Note

* Markdown links:

  ```
  [Example](https://example.com)
  ```

  Open in the same tab and do not support `target` attributes.

* Always use:

  ```
  target="_blank" rel="noopener noreferrer"
  ```

  for compatibility and security.
