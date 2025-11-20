## Secure Development Governance — Branching Strategy

The following defines our mandated Gitflow branching strategy for secure development governance. This file documents expectations for feature development, hotfixes, and releases.

```markdown
## Branching Strategy: Gitflow Workflow

We use the Gitflow model to manage our development lifecycle. All feature development must be done against the 'develop' branch.

**Feature Branches:** Branch from `develop`. Merge back to `develop` via Pull Request.
**Hotfixes:** Branch from `main`. Merge to `main`, then merge immediately to `develop`.

No direct pushes to 'main' or 'develop' are allowed.
```

Please follow these rules when contributing. If you need an exception (emergency hotfix with org approval), open an issue describing the reason and obtain an explicit approval before bypassing the rules.
## Prerequisites
To contribute code changes to this project you will need the following development kits.
 * [Go](https://golang.org/doc/install)
 * [Docker](https://docs.docker.com/engine/installation/)
 
As watchtower utilizes go modules for vendor locking, you'll need at least Go 1.11.
You can check your current version of the go language as follows:
```bash
  ~ $ go version
  go version go1.12.1 darwin/amd64
```


## Checking out the code
Do not place your code in the go source path.
```bash
git clone git@github.com:<yourfork>/watchtower.git
cd watchtower
```

## Building and testing
watchtower is a go application and is built with go commands. The following commands assume that you are at the root level of your repo.
```bash
go build                               # compiles and packages an executable binary, watchtower
go test ./... -v                       # runs tests with verbose output
./watchtower                           # runs the application (outside of a container)
```

If you dont have it enabled, you'll either have to prefix each command with `GO111MODULE=on` or run `export GO111MODULE=on` before running the commands. [You can read more about modules here.](https://github.com/golang/go/wiki/Modules)

To build a Watchtower image of your own, use the self-contained Dockerfiles. As the main Dockerfile, they can be found in `dockerfiles/`:
- `dockerfiles/Dockerfile.dev-self-contained` will build an image based on your current local Watchtower files.
- `dockerfiles/Dockerfile.self-contained` will build an image based on current Watchtower's repository on GitHub.

e.g.:
```bash
sudo docker build . -f dockerfiles/Dockerfile.dev-self-contained -t containrrr/watchtower # to build an image from local files
```