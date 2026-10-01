# Adding Multiple Images to a Markdown File

When you drag multiple images into a Markdown file in VS Code, they are inserted on a single line like this:

```
![Photo](img/00-images/room01-01.jpg) ![Photo](img/00-images/room01-02.jpg) ![Photo](img/00-images/room01-03.jpg)
```

But often you want each image on its own line:

```
![Photo](img/00-images/room01-01.jpg)
![Photo](img/00-images/room01-02.jpg)
![Photo](img/00-images/room01-03.jpg)
```

You can fix this instantly using **Find and eeplace with regular expressions**.

---

## Step-by-step instructions

### Step 1: Open Find and Replace

Press:

* **Windows / Linux:** `Ctrl + H`
* **Mac:** `Cmd + H`

This opens the Replace panel.

---

### Step 2: Enable Regular Expression Mode

Click the **`.*` icon** (Use Regular Expression), or press:

* **Alt + R** (Windows/Linux)

Make sure the `.*` icon is highlighted.

---

### Step 3: Enter Find and Replace Patterns

**Find:**

```
\s!\[
```

**Replace:**

```
\n![
```

---

### Step 4: Click Replace All

Click:

```
Replace All
```

Result: Every image will move to its own line.

---

## Why this works

| Pattern | Meaning                          |
| ------- | -------------------------------- |
| `\s`    | matches a space                  |
| `![`    | matches the Markdown image start |
| `\n`    | inserts a newline                |

So this converts:

```
(space)![
```

into

```
(newline)![
```

---

## Faster alternative (more precise)

This version only affects Markdown images:

**Find:**

```
\)\s+!\[
```

**Replace:**

```
)\n![
```

This ensures replacement only happens between images.

---

## Example

Before:

```
![Photo](img/a.jpg) ![Photo](img/b.jpg) ![Photo](img/c.jpg)
```

After:

```
![Photo](img/a.jpg)
![Photo](img/b.jpg)
![Photo](img/c.jpg)
```

---

## Optional: Assign a keyboard shortcut

You can speed this up by recording a macro using an extension like:

* **Multi Command**
* **Macros**

Then run it with one shortcut.

---

## Summary

Quick version:

1. Press `Ctrl + H`
2. Enable `.*`
3. Find: `\s!\[`
4. Replace: `\n![`
5. Click **Replace All**

