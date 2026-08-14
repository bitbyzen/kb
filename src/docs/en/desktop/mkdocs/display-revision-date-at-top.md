# Displaying the Revision Date at the Top

Display the Git revision date at the top of each page using Material for MkDocs. Hide the default footer date and exclude the home pages.

## Steps

1. Enable theme overrides in `mkdocs.yml`.

    ```yml
    theme:
      name: material
      custom_dir: overrides
    ```

2. Create the override file.

    Create:

      ```
      `overrides/main.html`
      ```

3. Add the template logic.

      ```jinja2
      {% extends "base.html" %}

      {% block content %}

        {% set is_home = page.file.src_path.endswith("index.md") %}

        {% if page.meta.git_revision_date_localized and not is_home %}
          <div class="page-date">
            {% if config.theme.language == "ja" %}
              最終更新日: {{ page.meta.git_revision_date_localized }}
            {% else %}
              Last updated: {{ page.meta.git_revision_date_localized }}
            {% endif %}
          </div>
        {% endif %}

        {{ super() }}

      {% endblock %}
      ```

    This:

    * Displays the revision date above the page content.
    * Hides the date on `en/index.md` and `ja/index.md`.
    * Switches the label based on the active language.

4. Create the stylesheet.

    Create:

      ```
      `docs/stylesheets/extra.css`
      ```

5. Add the styling and hide the footer date.

      ```css
      .page-date {
        font-size: 0.8rem;
        color: #888;
        margin-bottom: 0.5rem;
        font-weight: 400;
      }

      .md-source-file {
        display: none;
      }
      ```

    This:

    * Styles the top date as metadata.
    * Removes the default footer revision block.

6. Register the stylesheet in `mkdocs.yml`.

    ```yml
    extra_css:
      - stylesheets/extra.css
    ```

7. Rebuild the Docker image.

    ```bash
    docker build --no-cache -t my-mkdocs .
    docker run --rm -it -p 8000:8000 -v $(pwd):/mkdocs my-mkdocs
    ```

## Note

Do not create `overrides/partials/content.html` with:

```
{% extends "partials/content.html" %}
```

This causes a recursion error because the override extends itself.

Verify:

* The date appears at the top of normal pages.
* The date does not appear on `index.md`.
* The footer revision block is no longer displayed.
