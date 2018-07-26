# Easy startup viabtc_exchange_server with docker

This is docker config to startup [viabtc_exchange_server](https://github.com/viabtc/viabtc_exchange_server) simply.
Forked from and inspired by [gyk001/viabtc_exchange_server_docker](https://github.com/gyk001/viabtc_exchange_server_docker)

This repo do this things automatic:

* Startup a ubuntu docker container
* Prepare requirements environment
* Build viabtc_exchange_server from sourcecode
* Set up requirement service( redis kafka mysql...)
* Startup viabtc_exchange_server service

New improvements:

* No need to rebuild container after every config editing, just restart btc-service container
* Possibility to connect source code as git submodule

# Screenshots

![screenshots](imgs/screenshots.jpg)

# Prepare

* docker with compose: https://docs.docker.com/compose/install/
* git: not require, you also can download repo from webpage
* curl: not require, just for test

# Startup

Open a terminal(linux/mac) or cmd(windows)

```bash
git clone git@github.com:kot9pko/viabtc_exchange_server_docker.git
cd viabtc_exchange_server_docker
git submodule update --init
docker-compose up
```

Just wait it startup and then test use curl

```bash
curl  http://127.0.0.1:18080/ -d '{"method": "market.list", "params": [], "id": 1516681174}'
```

All is done, just play it!


Tips: if you don't install git, you can startup it like this

* Download https://codeload.github.com/gyk001/viabtc_exchange_server_docker/zip/master
* Extract viabtc_exchange_server_docker-master.zip
* cd into the target directory
* run `docker-compose up`

# Donation

Bitcoin: 12bKPV6B9yCWnWjChNM8E1faYmphC4T42v
Ethereum: 0x8ad65ee865c176cc1a8d637439abd9f335f8d14f

# Links

* https://github.com/viabtc/viabtc_exchange_server
* https://github.com/docker-library/mysql
* https://github.com/docker-library/redis
* https://github.com/wurstmeister/kafka-docker
* https://github.com/s7anley/redis-sentinel-docker
* https://github.com/vishnubob/wait-for-it

