# Rebuild the MkDocs Docker Image Only When Needed

Use this guide to decide when you must run `docker build` before `docker run` for your MkDocs container.

## What this guide does

* Explains **when a rebuild is required**
* Explains **when a rebuild is not required** (because you mount the repo with `-v $(pwd):/mkdocs`)
* Provides a simple repeatable workflow

## When you must rebuild

Rebuild the image when you change something that affects what’s **installed inside the image**:

* `Dockerfile` (example: adding `git`, `safe.directory`, changing `CMD`, changing base image)
* `requirements.txt` (adding/removing/upgrading Python packages)
* Anything else that is only applied during `docker build` (system packages installed with `apt-get`, etc.)

Run:

```bash
docker build -t my-mkdocs .
```

Use `--no-cache` only when you want to force a completely fresh build (useful after dependency changes or when you suspect caching issues):

```bash
docker build --no-cache -t my-mkdocs .
```

## When you do not need to rebuild

Because you run with a bind mount:

```bash
docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
```

You do **not** need to rebuild when you change files that are read directly from the mounted repo at runtime, such as:

* Markdown content in `docs/**`
* CSS in `docs/stylesheets/**` (example: `extra.css`)
* Theme overrides in `overrides/**` (example: `overrides/main.html`)
* `mkdocs.yml` (config changes are picked up when MkDocs reloads)

In these cases, do this instead:

* Refresh the browser (hard refresh if needed)
* If live reload does not pick it up, stop the container and run `docker run ...` again

## Recommended workflow for local editing

1. Start the container:

    ```bash
    docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
    ```

2. Edit files (`.md`, `.css`, `overrides/*.html`, `mkdocs.yml`).

3. If you changed `Dockerfile` or `requirements.txt`, rebuild and restart:

    ```bash
    docker build -t my-mkdocs .
    docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
    ```

## Note

If you ever remove the `-v $(pwd):/mkdocs` mount and rely only on `COPY . .` inside the image, then **every content/CSS/HTML change will require a rebuild**.
