# Copy an Image File from Windows to Linux

!!! Note
    **Are there any relevant extensions?** — No specific ones.

## Option 1: Best drag-and-drop solution

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

## Option 2: Best terminal solution

```bash
cp /mnt/c/Users/YourName/Pictures/*.png docs/images/
```

## Option 3: VS Code–native workaround (sometimes helpful)

1. Open the target folder in the VS Code Explorer.
2. Right-click the folder, then select **Reveal in File Explorer**.
3. Drag the images into that window.

