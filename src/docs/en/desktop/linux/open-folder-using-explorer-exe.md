# Opening a Folder Using explorer.exe

Open a folder in File Explorer from the command line.

## Steps

1. Open **Command Prompt** or **PowerShell**.

2. Run:

    ```
    explorer.exe C:\path\to\your\folder
    ```

    Example:

    ```
    explorer.exe C:\Users\username\Documents
    ```

    The folder opens in File Explorer.

## Note

* If the path contains spaces, wrap it in quotes:

  ```
  explorer.exe "C:\path\with spaces\folder"
  ```

* To open the current directory:

  ```
  explorer.exe .
  ```
