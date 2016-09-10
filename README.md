# lampv1

A Dockerfile that installs the apache2,mysql5.6,php5,phpmyadmin on ubuntu14.04 LST.

## Installation

If you'd like to build the image yourself then:

```bash
$ git clone https://github.com/myzero1/lampv1.git
$ cd lampv1
$ sudo docker build -t="myzero1/lampv1" .
```

## Usage

To spawn a new instance of wordpress on port 80.  The -p 80:80 maps the internal docker port 80 to the outside port 80 of the host machine.

```bash
$ sudo docker run -p 80:80 --name lampv1 -d myzero1/lampv1
```

Start your newly created docker.

```
$ sudo docker start lampv1
```

After starting the docker-wordpress-nginx check to see if it started and the port mapping is correct.  This will also report the port mapping between the docker container and the host machine.

```
$ sudo docker ps

0.0.0.0:80 -> 80/tcp lampv1
```

You can the visit the following URL in a browser on your host machine to get started:

```
http://127.0.0.1:80
```

