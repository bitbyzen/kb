# Installing Python Packages with pip in Docker

Install MkDocs and related plugins inside a Docker image using `requirements.txt`.

## What this guide does

* Explains how `pip install` works inside Docker
* Shows the correct `Dockerfile` setup
* Explains when you must rebuild the image
* Prevents common dependency issues

---

## Steps

1. Create or update `requirements.txt`.

    ```txt
    mkdocs<2
    mkdocs-material
    mkdocs-git-revision-date-localized-plugin
    mkdocs-static-i18n
    mkdocs-glightbox
    ```

    Add or remove packages as needed.

2. Install dependencies during Docker build.

    In your `Dockerfile`, include:

    ```dockerfile
    FROM python:3.12-slim

    RUN apt-get update \
    && apt-get install -y --no-install-recommends git \
    && rm -rf /var/lib/apt/lists/*

    RUN git config --system --add safe.directory /mkdocs

    WORKDIR /mkdocs

    COPY requirements.txt .
    RUN pip install --no-cache-dir -r requirements.txt

    COPY . .

    EXPOSE 8000
    CMD ["mkdocs", "serve", "-a", "0.0.0.0:8000"]
    ```

    Important:

    * `COPY requirements.txt .` happens **before** copying the whole project.
    * `pip install` runs during build, not during `docker run`.

3. Build the image.

    ```bash
    docker build -t my-mkdocs .
    ```

    If you changed `requirements.txt`, use:

    ```bash
    docker build --no-cache -t my-mkdocs .
    ```

4. Run the container.

    ```bash
    docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
    ```

---

## Important notes

### pip install does NOT run during docker run

This command:

```bash
docker run ...
```

does not install packages.

All Python dependencies must already be installed during:

```bash
docker build
```

---

### When you must rebuild

Rebuild if you change:

* `requirements.txt`
* `Dockerfile`
* Python version in `FROM python:...`

You do not need to rebuild for:

* Markdown changes
* CSS changes
* HTML override changes
* `mkdocs.yml` changes

---

## Optional: Verify installed packages

Run:

```bash
docker run --rm -it my-mkdocs pip list
```

Or check MkDocs version:

```bash
docker run --rm -it my-mkdocs mkdocs --version
```

---

## Why this pattern is recommended

This order:

```dockerfile
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
```

improves build caching.

Docker only re-installs dependencies when `requirements.txt` changes.

Content edits do not trigger re-installation.

---

This setup ensures:

* Clean dependency management
* Reproducible builds
* Correct behavior in Docker + GitHub Actions
* Stable MkDocs 1.x environment
