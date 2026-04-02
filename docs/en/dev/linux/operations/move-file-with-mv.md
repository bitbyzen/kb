# Move a File Using mv

Move a file to another directory using the `mv` command.

## Steps

1. Open a terminal.

2. Run:

    ```
    mv test260129_1430.md docs/en/02-dev/vscode
    ```

    The file `test260129_1430.md` is moved to `docs/en/02-dev/vscode`.

## Note

* To rename the file while moving:

  ```
  mv test260129_1430.md docs/en/02-dev/vscode/new-name.md
  ```

* If the destination directory does not exist, create it first:

  ```
  mkdir -p docs/en/02-dev/vscode
  ```
