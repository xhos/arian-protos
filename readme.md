# arian-protos

here lie `.proto` files used across arian for gRPC communication.

## development

### init

using git submodules is, in my opinion, the cleanest way to add these to a project.

to add a ./proto folder with the submodule in a new project, run:

```shell
git submodule add -b main git@github.com:xhos/arian-protos.git proto
git commit -m "Add arian-protos as submodule at proto/"
```

then to generate code you would add a `buf.gen.yaml` that looks something like this:

```yaml
version: v2

inputs:
  - directory: proto # note that this points to the submodule

plugins:
  - local: protoc-gen-go
    out: gen/go
    opt:
      - paths=source_relative

  - local: protoc-gen-go-grpc
    out: gen/go
    opt:
      - paths=source_relative
      - require_unimplemented_servers=false
```

```shell
buf generate
```

### update

to update the submodule to the latest version, run:

```shell
git submodule update --remote --merge
```
