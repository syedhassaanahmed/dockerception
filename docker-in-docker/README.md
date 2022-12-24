# docker-in-docker
In this approach, we base our image from `docker:dind` ([see more](https://www.docker.com/blog/docker-can-now-run-within-docker/)).

- To build the container `docker build . -t dind`
- To run the container `docker run -d --name dind --privileged dind`
- To connect inside the container `docker exec -it dind sh`
- Once inside,
  - `docker ps -a` should be empty.
  - Trying to mount the `/mydir` directory will succeed 
  ```sh
  docker run -it --rm -v /mydir:/innerdir busybox cat /innerdir/myfile.txt
  ```