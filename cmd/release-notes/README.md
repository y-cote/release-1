# OpenShift Azure (based on Kubernetes) Release Notes Generator

This directory contains a tool called `release-notes` and a set of library utilities at which aim to provide a simple and extensible set of tools for fetching, contextualizing, and rendering release notes for the [OpenShift Azure](https://github.com/openshift/openshift-azure) repository.

## Install

The simplest way to install the `release-notes` CLI is via `go get`:

```
go get github.com/y-cote/release-1/cmd/release-notes
```

This will install `release-notes` to `$GOPATH/bin/release-notes`. If you're new to Go, `$GOPATH` default to `~/go`, so look for the binary at `~/go/bin/release-notes`.

## Usage

To run the command line you will need a github API token. To do so, you can follow the instructions found at [Github Personal Token](https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line).

To generate release notes for a commit range, run:

```
$ export GITHUB_TOKEN=a_github_api_token
$ release-notes \
  -start-sha 4877fb04d9a6c508d553ea311603c1d3ef03b0a4 \
  -end-sha   2b17c675923b8438f04faf68206ce601310ed8a7
level=info msg="fetching all commits. this might take a while..."
level=info msg="got the commits, performing rendering"
level=info msg="release notes written to file" path=/tmp/release-notes-141665182 format=markdown
```

You can also generate the raw notes data into JSON. You can then use a variety of tools (such as `jq`) to slice and dice the output.

## Building From Source

To build the `release-notes` tool, check out this repo to your `$GOPATH`:

```
git clone git@github.com:y-cote/release-1.git $GOPATH/src/github.com/y-cote/release-1
```

Run the following from the root of the repository to build the `release-notes` binary:

```
bazel build //cmd/release-notes
```

Use the `-h` flag for help:

```
./bazel-bin/cmd/release-notes/darwin_amd64_stripped/release-notes -h
```

Install the binary into your path:

```
cp ./bazel-bin/cmd/release-notes/darwin_amd64_stripped/release-notes /usr/local/bin/release-notes
```

### What formats are supported?

Right now the tool can output release notes in Markdown and JSON.
