# Creating a New File in a Specific Directory

Create a new file in a target directory using the terminal in WSL.

## Steps

### Create the file after changing directory

1. Navigate to the target directory:

    ```bash
    cd docs/en/01-apps/google-drive/operations
    ```

2. Create the file:

    ```bash
    touch filename.md
    ```

---

### Return to the previous directory

After changing directories, run:

```bash
cd -
```

This returns to the previous directory.

---

### Temporarily move using pushd and popd

Run:

```bash
pushd docs/en/01-apps/google-drive/operations
touch file.md
popd
```

This moves to the directory, creates the file, then returns to the original location.

## Note

These commands work in most shells such as `bash` inside WSL.
