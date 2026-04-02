# Fix "GET /ja/sitemap.xml HTTP/1.1" Code 404

```bash title="terminal"
"GET /ja/sitemap.xml HTTP/1.1" code 404
```

This happens because:

- MkDocs does not generate sitemaps by default.
- Material tries to probe for them.
- Browser/devtools sometimes request them automatically.

To fix this, you can:

- Ignore them, or
- Add a sitemap plugin later if you care about SEO
