# Move Files Safely in Linux or WSL Using VS Code

Avoid accidental folder replacement when moving files in Linux or WSL.

## Steps

### Restore overwritten files

If a folder was accidentally replaced and changes were not committed:

1. Open a terminal at the repository root.

2. Run:

    ```bash
    git restore .
    ```

3. Verify:

    ```bash
    git status
    ```

    Confirm that the working tree is clean.

---

### Understand Linux folder behavior

In Linux and WSL, moving a folder with the same name can replace the existing folder instead of merging it.

Example behavior:

```
mv new_folder existing_folder
```

If both names match, the original folder may be replaced.

---

### Move files safely

#### Copy file contents instead of replacing the folder

```
cp -r source_folder/* existing_folder/
```

#### Move a single file

```
mv source_folder/file.md existing_folder/
```

#### Commit before major changes

```
git add .
git commit -m "Checkpoint before refactor"
```

This allows safe recovery if a mistake occurs.

## Note

Linux file operations behave differently from Windows folder merging.
Use terminal commands instead of drag and drop when folder names are identical.
