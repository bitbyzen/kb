# Copy an Image File from Windows to Linux

!!! Note
    **Are there any relevant extensions?** — No specific ones.

## Method 1: Best Drag-and-Drop Solution

1. Create a target folder:

    ```bash
    mkdir images
    ```

2. Create a dummy Markdown file and open it in VS Code:

    ```text
    .dummy.md
    ```

3. Drag and drop the image files into the Markdown file.

4. Delete the dummy Markdown file.

## Method 2: Best Terminal Solution

```bash
cp /mnt/c/Users/YourName/Pictures/*.png docs/images/
```

## Method 3: VS Code-Native Workaround (Sometimes Helpful)

1. Open the target folder in the VS Code Explorer.
2. Right-click the folder, then select **Reveal in File Explorer**.
3. Drag the images into that window.

