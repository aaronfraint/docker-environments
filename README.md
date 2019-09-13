# docker-environments
a place to store Dockerfiles that build GIS data science containers

The basic structure of this `Dockerfile` comes from [Geoff Boeing's `osmnx`](https://github.com/gboeing/osmnx) Dockerfile.

### Build an image from the dockerfile:

```bash
>>> docker build -t aaronfraint/gis-data-science-stack .
```

### Run bash in this container and export final conda environment to a yml file:
```bash
>>> docker run --rm -it -v "%cd%":/home/jovyan/work aaronfraint/gis-data-science-stack /bin/bash
>>> conda env export -n base > /home/jovyan/work/environment.yml
```


### Run jupyter lab in this container:
```bash
>>> docker run --rm -it -p 8888:8888 -v "%cd%":/home/jovyan/work aaronfraint/gis-data-science-stack
```

### Push the built image to hub so others can pull/run it:
```bash
>>> docker tag aaronfraint/gis-data-science-stack aaronfraint/gis-data-science-stack:v0.0.0
>>> docker login
>>> docker push aaronfraint/gis-data-science-stack
```

### Stop/delete all local docker containers/images:
```bash
>>> docker stop $(docker ps -aq)
>>> docker rm $(docker ps -aq)
>>> docker rmi $(docker images -q) --force
```
