# Display the Revision Date at the Bottom

Display the Git revision date in the default Material footer area using `mkdocs-git-revision-date-localized-plugin`.

## Steps

1. Add the plugin to `requirements.txt`.

    ```txt
    mkdocs-git-revision-date-localized-plugin
    ```

    Pin MkDocs to 1.x:

      ```txt
      mkdocs<2
      ```

2. Enable the plugin in `mkdocs.yml`.

    ```yml
    plugins:
      - i18n:
          # your existing i18n configuration
      - git-revision-date-localized:
          type: date
          timezone: Asia/Tokyo
          custom_format: "%Y-%m-%d"
          fallback_to_build_date: true
      - search
      - glightbox
    ```

3. Configure GitHub Actions to fetch full history.

    In `.github/workflows/deploy.yml`:

      ```yml
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0
      ```

    Install dependencies:

      ```yml
      - run: pip install -r requirements.txt
      ```

4. Install `git` in the Docker image.

    Update `Dockerfile`:

      ```dockerfile
      FROM python:3.12-slim

      RUN apt-get update \
        && apt-get install -y --no-install-recommends git \
        && rm -rf /var/lib/apt/lists/*

      WORKDIR /mkdocs
      COPY requirements.txt .
      RUN pip install --no-cache-dir -r requirements.txt
      COPY . .
      EXPOSE 8000
      CMD ["mkdocs", "serve", "-a", "0.0.0.0:8000"]
      ```

5. Allow Git to read the mounted repository.

    Add after installing `git`:

      ```dockerfile
      RUN git config --system --add safe.directory /mkdocs
      ```

6. Rebuild and run.

    ```bash
    docker build --no-cache -t my-mkdocs .
    docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
    ```

7. Verify the result.

    Open:

    * `http://localhost:8000/kb/`
    * `http://localhost:8000/kb/ja/`

    Confirm that the revision date appears in the bottom metadata area (clock icon section).

## Note

If the message “Unable to read git logs… Falling back to build date” appears:

* Ensure `.git` exists in the mounted directory.
* Confirm `safe.directory /mkdocs` is configured.
* Confirm `fetch-depth: 0` is set in GitHub Actions.

If a MkDocs 2.0 compatibility warning appears, verify:

```bash
mkdocs --version
```

Ensure the version is 1.x and `mkdocs<2` is pinned in `requirements.txt`.
