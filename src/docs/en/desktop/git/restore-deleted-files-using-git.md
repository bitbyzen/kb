# Restoring Deleted Files Using Git

Restore deleted files that have not been committed.

## Steps

### Restore all deleted files

1. Open a terminal at the repository root.

2. Run:

    ```bash
    git restore .
    ```

    This restores all deleted files to the state of `HEAD`.

---

### Restore a specific folder

Run:

```bash
git restore docs
```

Or restore a specific path:

```bash
git restore docs/en/01-apps
```

---

### Use checkout if needed

If `git restore` does not restore some files, run:

```bash
git checkout -- docs/en/01-apps
```

---

### Verify the result

Run:

```bash
git status
```

Confirm that the deleted files are restored and no unintended deletions remain.

## Note

This method works only if the deletions were not committed.
Files are restored from the latest commit (`HEAD`).
