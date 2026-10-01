# Creating a File and Opening It in VS Code

Create a file in WSL2 and open it directly in Visual Studio Code.

## Steps

1. Set a file name and create the file:

    ```bash
    d=filename.md
    touch "$d"
    ```

2. Open the file in Visual Studio Code:

    ```bash
    code "$d"
    ```
