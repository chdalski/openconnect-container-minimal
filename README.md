# OpenConnect docker minimal

Derived from: https://github.com/aw1cks/openconnect

A template for creating a vpn proxy suitable for [Development Containers](https://containers.dev/).

It can be used to:

- proxy traffic via a vpn
- use development containers with visual studio code via proxy
- run docker in docker

> **_NOTE:_**
> See [OpenConnect remote minimal](https://github.com/chdalski/openconnect-remote-minimal) for a all in one remote container.

## Prerequisites

- copy company.cer, user.key and user.pem into `certs` directory
- create `.vpn-env` file (copy sample) and fill out the missing values

## Start vpn

```shell
docker compose up -d
```

## Using the Proxy with Devcontainer

Start by using the [devcontainer template](.devcontainer-template) as follows:

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

> **_NOTE:_**
> The Proxy settings might not be automatically applied for all applications in the devcontainer and you might need to specify it explicitly.

## Using the Proxy locally

The Proxy is forwarded to `localhost:3128` and currently configured to allow http and https connections (see [squid.conf](vpn/squid.conf)).
Use [Foxy Proxy](https://getfoxyproxy.org/help/browsers/) or similar tools in your browser to access it.

## TODO

- run vpn container unprivileged: https://www.infradead.org/openconnect/nonroot.html (socks forwarding)
