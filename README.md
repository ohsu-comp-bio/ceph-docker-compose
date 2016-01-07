### Docker Compose Configuration for Ceph ###

This is a simple Docker Compose configuration for spinning up the Ceph demo
docker image.

1. If using Docker Machine, create a new instance called `ceph`:

  ```
    docker-machine create -d virtualbox ceph
  ```

2. Update your environment. Ceph relies on fixed IP topologies.

  ```
  export MON_IP=$(docker-machine ip ceph)
  export CEPH_NETWORK=$(docker-machine ip ceph | sed -e 's/[0-9]*$/0\/24/g')
  ```

3. Run Docker Compose!

  ```
    docker-compose up
  ```

4. If using [Pow](http://pow.cx), update your Pow configuration:

  ```
    echo http://$(docker-machine ip ceph) > ~/.pow/ceph
    touch ~/.pow/restart.txt
  ```

5. Access Ceph in the browser: [http://ceph.dev](http://ceph.dev)
