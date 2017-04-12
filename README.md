# freenas-docker-validate
Utility to validate FreeNAS specific parameters in FreeNAS Dockerfiles

The org.freenas.* labels are parsed out of the Dockerfile and are
syntax checked.  This can help find non-obvious problems setting
parameters on FreeNAS docker images.

This script *must* be run on a FreeNAS Corral installation.  It
imports files that only exist there.

When using the *--search* option, only Docker Hub repositories that
are automatically built will be shown.  Repositories that are not
automatically build will not contain a Dockerfile.

# Usage
```
freenas-docker-validate [-h] [--search SEARCH [SEARCH ...]]
                             [--dockerfile DOCKERFILE [DOCKERFILE ...]]
                             [--dockerurl DOCKERURL [DOCKERURL ...]]
                             [--verbose | --quiet]

Query FreeNAS docker containers

optional arguments:
  -h, --help            show this help message and exit
  --search SEARCH [SEARCH ...]
                        Search Docker Hub for the string COLLECTION/FILTER,
                        i.e. jchonig/freenas-
  --dockerfile DOCKERFILE [DOCKERFILE ...], -f DOCKERFILE [DOCKERFILE ...]
                        Run a syntax check on the specified Dockerfile
  --dockerurl DOCKERURL [DOCKERURL ...], -u DOCKERURL [DOCKERURL ...]
                        Run a syntax check on the Dockerfile at given url
  --verbose, -v         Pretty-print the contents of the org.freenas labels
  --quiet, -q           Do not list the names of the images found
```

# Examples

## List all the offical FreeNAS containers
This will be prefixed with any errors found
```
$ freenas-docker-validate --search freenas/
```

## Only syntax check all the FreeNAS official containers
The *-q* option surpesses the list
```
$ freenas-docker-validate -q --search freenas/
```

## Pretty-print all the FreeNAS specific parameters 
The *-v* option causes the parameters to be pretty-printed.  This will
be long
```
$ freenas-docker-validate -q --search freenas/
```

## Check a local Dockerfile
```
$ freenas-docker-validate --dockerfile Dockerfile
```

## Check a local git repo
This will check any Dockerfile in the specified directory tree.
```
$ freenas-docker-validate --dockerfile docker-images
```

## Check a Docketfile on github
```
$ freenas-docker-validate --dockerurl https://raw.githubusercontent.com/freenas/docker-images/master/xdm/Dockerfile
```
