This is a sample repository showing an example use case for `envctl`.

This is pretty arbitrary, but the imporant thing to see is that you can clone
this go repo anywhere, including outside your `$GOPATH`, and you can still work
with it by running the environment.

## Configuration walkthrough

```yaml
---
# This is the golang image being used for the environment.
image: golang:1.10-stretch

# This is the shell that will be used for login.
shell: /bin/bash

# The bootstrap installs `dep` for use in vendoring things. Without all the
# dependencies vendored, cloning this outside `$GOPATH` will cause issues.
bootstrap:
- go get -u github.com/golang/dep/cmd/dep
- go install github.com/golang/dep/cmd/dep

# This mounts the current folder inside `$GOPATH/src` in the environment. This
# is why the repo can be cloned anywhere on the host machine. In the
# environment, the repo exists inside the `$GOPATH`.
mount: /go/src/github.com/juicemia/envctl-sample
```

## Playing with the repo

```bash
$ # Assumes you cloned the repo and you're at the root.
$ envctl create
$ envctl login # Play with all the tools in here. Do whatever you want.
$ envctl destroy
```

Go ahead, add dependencies, run `dep ensure` and `go build` to see how to work
with the environment first hand.