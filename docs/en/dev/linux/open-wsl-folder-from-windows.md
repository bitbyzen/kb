# Open a WSL Folder from Windows

Open a Linux directory in File Explorer using the WSL network path.

## Steps

1. Open **File Explorer**.

2. Enter the following path in the address bar:

    ```
    \\wsl$\Ubuntu\home\kuroraiun\projects\docker\python\mkdocs\docs\en\02-dev
    ```

3. Press **Enter**.

    The Linux directory opens in File Explorer.

## Note

* Replace `Ubuntu` with your WSL distribution name if different.
* You can access any WSL path using the format:

  ```
  \\wsl$\DistributionName\path\to\directory
  ```
