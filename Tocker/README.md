# Tocker
Docker Container Tor Proxy

This is a simple and lightweight Docker image for running a Tor proxy based on palnabarun/tor-docker ( https://github.com/palnabarun/tor-docker)

This image is not hosted in Docker Hub, utilizes a local dockerfile, and will be apart of a bigger project (Stay-tuned)

For now, I am copyint Palnabarun's Readme until I can tweak further

# Usage

It is pretty simple to run and has some sane defaults.

After cloning the repo, the first thing you will need to do is build the dockar image outside of the project directory

```
$ docker build tocker .
```

Verify the creation of the image

```
$ docker image ls
```
Run the proxy

```
$ docker run \
    --rm \
    --detach \
    --name tor \
    --publish 9050:9050 \ # change the port to whatever you put in the torrc
    tocker
...

```

The Tor proxy would be coming up shortly after establishing a Tor circuit.

If you want to customize the Tor configuration, create a `torrc` locally and the mount the same as a volume.

```
$ docker run \
    --rm \
    --detach \
    --name tor \
    --volume $PWD/torrc:/etc/tor/torrc
    --publish 9050:9050 \ # change the port to whatever you put in the torrc
    palnabarun/tor
...
```

The options in `torrc` are documented [here](https://2019.www.torproject.org/docs/tor-manual.html.en)

# Contributing

Please feel free to create issues and file PRs with any change that you wish to see.

# License

The repository is licensed under [GPLv3](https://choosealicense.com/licenses/gpl-3.0).
