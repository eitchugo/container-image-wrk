# wrk container image

This repository contains the instructions to build container with the `wrk`
http benchmarking tool.

It uses the alpine linux image for the base and contains some lua libraries
to use with its scripting capabilities.

For more information about `wrk`, check [its repository](https://github.com/wg/wrk).

## Usage

```bash
# run help with docker
docker run --rm eitch/wrl

# run help with podman
podman run --rm eitch/wrk

# run a benchmark with some script in current dir
podman run --rm -v $(pwd):/home/wrk eitch/wrk -s script.lua https://www.example.com
```

## Other information and thanks

* Some ideas came from [skandyla/docker-wrk](https://github.com/skandyla/docker-wrk). Thanks!
* I've been trying to use `podman` more :)
* If you encounter any problems with using alpine, let me know and we can build with
  other distros.
