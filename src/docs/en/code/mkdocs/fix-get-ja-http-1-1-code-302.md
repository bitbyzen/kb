# Fixing "GET /ja HTTP/1.1" Code 302

```bash title="terminal"
"GET /ja HTTP/1.1" code 302
```

No fix is needed.

This happens because:

- /ja redirects to /ja/.
- This is a standard behavior in MkDocs.





