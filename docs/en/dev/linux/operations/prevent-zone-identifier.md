# Prevent Zone.Identifier Files in Linux

`Zone.Identifier` files can appear in repositories when Windows attaches security metadata to files downloaded from the internet. When working with Linux tools through WSL, Git, or Docker, these metadata streams may appear as real files and pollute the project directory.

## Steps

1. Work inside the Linux filesystem instead of Windows-mounted paths.

    Store projects inside the WSL Linux home directory:

    ```
    ~/projects/my-repo
    ```

    Avoid storing repositories in Windows-mounted locations such as:

    ```
    /mnt/c/Users/<user>/projects
    ```

    Linux filesystems do not support Windows Alternate Data Streams, so `Zone.Identifier` files are not created.

2. Clone repositories inside WSL.

    Run Git commands from the Linux shell:

    ```bash
    git clone https://github.com/example/repo.git
    ```

    Avoid cloning repositories through Windows Explorer or Windows Git clients.

3. Download files using Linux tools.

    Download files from inside WSL using tools such as:

    ```bash
    curl -O https://example.com/file.tar.gz
    ```

    or

    ```bash
    wget https://example.com/file.tar.gz
    ```

    Files downloaded in Linux do not receive Windows security streams.

4. Edit files using WSL-aware editors.

    Use editors that interact directly with the Linux filesystem:

    * Visual Studio Code with the **Remote – WSL** extension
    * `vim`
    * `nano`

    Avoid editing project files through Windows Explorer under `\\wsl$`.

5. Extract archives inside Linux.

    Extract downloaded archives using Linux tools:

    ```bash
    tar -xzf archive.tar.gz
    ```

    Avoid extracting archives using Windows Explorer before moving them into the repository.

6. Block metadata files in Git.

    Add rules to `.gitignore`:

    ```
    Thumbs.db
    desktop.ini
    *.Zone.Identifier
    ```

    This prevents accidental commits if the files appear.

7. Remove existing Zone.Identifier files.

    If metadata files already exist in a repository, remove them:

    ```bash
    find . -name "*:Zone.Identifier" -delete
    ```

    Verify the working tree afterwards:

    ```bash
    git status
    ```

## Note

Windows creates `Zone.Identifier` using the **Mark of the Web** security mechanism. When files are downloaded or copied from external sources in Windows environments, the metadata may appear as separate files when accessed from Linux tooling. Keeping repositories entirely inside the Linux filesystem prevents the issue. 
