# VPN container

Derived from: https://github.com/aw1cks/openconnect

## Prerequisites

- copy company.cer, user.key and user.pem into `certs` directory
- create `.vpn-env` file (copy sample) and fill out the missing values

## Start vpn

```shell
docker compose up -d
```

## Devcontainer

- create a directory for the repository on your host
- copy the `.devcontainer-template` into the repository directory as `.devcontainer`
- open the directory with vscode and use the container shell to clone the repository
  - as the directory itself is not empty because of the `.devcontainer` directory you need to move all files from the created subfolder
    ```shell
    git clone ...
    mv my-actual-repo/* .
    mv my-actual-repo/.* .
    rm -rf my-actual-repo
    ```
  - add `.devcontainer/` to your `.gitignore file`

## TODO

- run vpn container unprivileged: https://www.infradead.org/openconnect/nonroot.html (socks forwarding)
