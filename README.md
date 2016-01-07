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

6. To access Ceph via the command line, run `docker exec`:

  ```
  › docker exec -it ceph /bin/bash
  root@ceph:/# ceph health
  HEALTH_OK
  root@ceph:/# ceph status
      cluster f9b95f58-b260-4f2b-9e29-64e0defe55d6
       health HEALTH_OK
       monmap e1: 1 mons at {ceph=192.168.99.107:6789/0}
              election epoch 2, quorum 0 ceph
       mdsmap e5: 1/1/1 up {0=0=up:active}
       osdmap e16: 1 osds: 1 up, 1 in
              flags sortbitwise
        pgmap v22: 128 pgs, 9 pools, 2808 bytes data, 190 objects
              1079 MB used, 16556 MB / 18603 MB avail
                   128 active+clean
  ```
