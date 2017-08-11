# opentracker-i2p-docker

Using
=====

Build image:

    git clone https://github.com/l-n-s/opentracker-i2p-docker
    cd opentracker-i2p-docker/docker && docker build -t opentracker-i2p .

Run:

    docker run --name=ot-i2p -dt opentracker-i2p

Get container IP :

    docker inspect ot-i2p | jq '.[0].NetworkSettings.Networks.bridge.IPAddress'

Don't have jq? Do `apt install jq`, it's useful.

Add I2P tunnel to i2pd container (assuming OT IP is 172.17.0.3):

    docker exec -it i2pd-container /bin/sh -c 'printf "\n[opentracker]\ntype = http\nhost = 172.17.0.3\nport = 6969\nkeys = opentracker.dat\n" >> /home/i2pd/data/tunnels.conf && kill -HUP `cat /home/i2pd/data/i2pd.pid` '


Find b32 address of your tracker:

    docker logs i2pd-container | grep opentracker.dat

