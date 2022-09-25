# Nbconvert docker

Docker container to run Nbconvert. There are two versions: a
complete one and another that does not install TeXLive, because it
takes a long time and occupies a lot of space.

## Image creation

### Complete

To create the image from the `Dockerfile`, run (inside the repository
folder):

```shell
docker build -f Dockerfile.Complete -t nbconvert-img:Complete .
```

### Without TeXLive

To create the image from the `Dockerfile`, run (inside the repository
folder):

```shell
docker build -f Dockerfile.NoTeX -t nbconvert-img:NoTeX .
```

## Running

To run the image, type the command:

```shell
docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v `(pwd)`/:/home/developer/develop nbconvert-img
```

It will create a container and map the current folder of your host to
the `~/develop` folder in the container. From there you can access the
files inside the folder you were in.

Obs.: If you have built the two versions of the image for some reason,
you may have to specify which one to run, `nbconvert-img:Complete` or
`nbconvert-img:NoTex`.

## Usage

Imagine you want to convert a notebook called `notebook.ipynb` that is
inside `~/Documents` to `webpdf`. Then just run:

```shell
cd ~/Documents
docker run --rm -it -e DISPLAY=$DISPLAY -v /tmp/.X11-unix/:/tmp/.X11-unix/ -v `(pwd)`/:/home/developer/develop nbconvert-img
cd develop
python3 -m nbconvert --to webpdf notebook.ipynb
```
