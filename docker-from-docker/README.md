# docker-from-docker
In this approach, we install [Docker CLI](https://docs.docker.com/engine/reference/commandline/cli/) in our Dockerfile and then on container creation, mount the [docker daemon socket](https://docs.docker.com/engine/reference/commandline/dockerd/#daemon-socket-option). This way the container can access the Docker daemon running on the host machine.

- To build the container `docker build . -t dfd`
- To run the container
  - On Linux `docker run -it --rm -v /var/run/docker.sock:/var/run/docker.sock dfd bash`
  - On Windows `docker run -it --rm -v //var/run/docker.sock:/var/run/docker.sock dfd bash`
- Once inside the container
  - `docker ps -a` should list all the containers running on the host machine.
  - Trying to mount the `/mydir` directory will fail 
  ```sh
  docker run -it --rm -v /mydir:/innerdir busybox cat /innerdir/myfile.txt
  ```