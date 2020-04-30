Using docker
=============

Pull or build docker image
---------------------------

MACE provides docker images with dependencies installed and also Dockerfiles for images building,
you can pull the existing ones directly or build them from the Dockerfiles.
In most cases, the ``lite edition`` image can satisfy developer's basic needs.

.. note::
    It's highly recommended to pull built images.

- ``lite edition`` docker image.

.. code-block:: sh

    # You can pull lite edition docker image from docker repo (recommended)
    docker pull registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev-lite
    # Or build lite edition docker image by yourself
    docker build -t registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev-lite ./docker/mace-dev-lite

- ``full edition`` docker image (which contains multiple NDK versions and other dev tools).

.. code-block:: sh

    # You can pull full edition docker image from docker repo (recommended)
    docker pull registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev
    # Or build full edition docker image by yourself
    docker build -t registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev ./docker/mace-dev

.. note::

    We will show steps with lite edition later.


Using the image
-----------------

Create container with the following command

.. code-block:: sh

    # Create a container named `mace-dev`
    docker run -it --privileged -d --name mace-dev \
               -v /dev/bus/usb:/dev/bus/usb --net=host \
               -v /local/path:/container/path \
               -v /usr/bin/docker:/usr/bin/docker \
               -v /var/run/docker.sock:/var/run/docker.sock \
               registry.cn-hangzhou.aliyuncs.com/xiaomimace/mace-dev-lite
    # Execute an interactive bash shell on the container
    docker exec -it mace-dev /bin/bash


Update images to repository
---------------------------

If you are mace inner developer and need update images in remote repository,
it can be achieved by `docker/update_images.sh` script.

.. code-block:: sh

    cd docker/
    ./update_images.sh

