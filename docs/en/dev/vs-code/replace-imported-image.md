# Replace an Imported Image

Replace an existing image file in an MkDocs project without changing the Markdown reference.

## Steps

1. Locate the image file used in the Markdown document.

    ```
    Example:

    `![Architecture](img/images/diagram.webp)`

    The file is stored in:

    `docs/images/diagram.webp`
    ```

2. Edit the image using an external image editor.

    ```
    Examples:
    - Crop unnecessary whitespace.
    - Adjust dimensions.
    - Export as `webp` if needed.
    ```

3. Export the edited image using the same file name.

    ```
    Ensure the file name matches exactly:

    `diagram.webp`
    ```

4. Replace the original file in the project directory.

    ```
    Overwrite:

    `docs/images/diagram.webp`
    ```

5. Refresh the MkDocs development server.

    ```
    If using:

    `mkdocs serve`

    Perform a hard refresh in the browser:

    `Ctrl + Shift + R`
    ```

## Note

* Keeping the same file name avoids updating Markdown references.
* If the browser cache prevents updates from appearing, rename the file and update the Markdown reference.
* When using Docker with bind mounts, file replacement is detected automatically.
* Store the project inside the WSL Linux filesystem for consistent permissions and performance.
