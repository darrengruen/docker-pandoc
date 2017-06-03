# Pandoc... Containerized!!!

For information on pandoc please see the [http://pandoc.org](http://pandoc.org/)

## Usage

Running pandoc from a container is as simple as the following:

```
docker run -it --rm \
    --name pandoc_"$(date +%s) \
    gruen/pandoc 
```

This is the same as running `pandoc` when it is installed locally.

A better example would be converting all markdown files in the current directory to a docx in the same directory. Here's how to do that:
```
docker run -it --rm \
    -v "$(pwd)":/root/pandoc:rw \
    --name pandoc_"$(date +%s)" \
    gruen/pandoc ./*.md -f markdown -t docx -s -o output.docx
```

I have a simple shell script in my `$PATH` named `pandoc` that looks like the following:

```
#!/usr/bin/env sh

docker run \
    -it \
    --rm \
    -v "$(pwd)":/root/pandoc:rw \
    --name pandoc_"$(date +%s)" \
    gruen/pandoc "${@}"
```

This is the same as the `pandoc` file [here](./pandoc)
