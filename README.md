# Redis-Demo
* https://youtu.be/PpkPTviLTLs
* https://spring.io/projects/spring-data-redis

Other videos
* https://youtu.be/cVdQIWpuZk8
* https://youtu.be/p8mK8GBCARE
* https://youtu.be/GEg7s3i6Jak
* https://youtu.be/3WOfXRjYnGA
* https://youtu.be/N8BkmdZzxDg
* https://youtu.be/OqCK95AS-YE
* https://youtu.be/RAPKJFAiBb4
* https://youtu.be/infTV4ifNZY
* https://youtu.be/VLTPqImLapM
* https://youtu.be/jgpVdJB2sKQ
* https://youtu.be/85HzpIk7Mq8
* https://youtu.be/U4WspAKekqM
* https://youtu.be/esbRryo0Ty8
* https://youtu.be/Z8qcpXyMAiA
* https://www.youtube.com/channel/UCD78lHSwYqMlyetR0_P4Vig


## Redis runbook

https://redis.io/docs/getting-started/installation/install-redis-on-mac-os/ 

* **brew install redis** 
* **redis-server** : to start redis in master slave mode

* **brew services start redis** : same as above 
* **brew services stop redis** 
* **brew services info redis** : check status


### Connect to Redis:
Once Redis is running, you can test it by running redis command line interface (CLI):
* **redis-cli**
* keys *
* **set mykey somevalue**
* **get mykey**
* **flushdb**
* **info stats**
* **info memory**

## Doc:
* https://redis.io/docs/getting-started/ 
* https://redis.io/docs/ 
* https://docs.spring.io/spring-data/redis/docs/current/api/org/springframework/data/redis/core/RedisTemplate.html


## Jedis vs Lettuce
* https://redis.com/blog/jedis-vs-lettuce-an-exploration/
* Lettuce
  - Thread safe
  - supports cluster
  - capable of synchronous, asynchronous, and reactive interaction with the cluster
  - relatively difficult to use

* Jedis
  - Not thread safe; Need to create connection pool
  - supports cluster
  - capable of only synchronous interaction
  - relatively easy to use


## Clustering
* https://redis.io/docs/reference/cluster-spec/
* https://docs.spring.io/spring-data/data-redis/docs/current/reference/html/#cluster


## Creating and running a redis cluster
* https://wp.huangshiyang.com/creating-and-using-a-redis-cluster
* https://iamvishalkhare.medium.com/create-a-redis-cluster-faa89c5a6bb4
* mkdir cluster-test
* cd cluster-test
* mkdir 7000 7001 7002 7003 7004 7005
* cd 7000
* touch redis.conf
* then edit and add following content to the redis.conf file
```
port 7000
cluster-enabled yes
cluster-config-file nodes.conf
cluster-node-timeout 5000
appendonly yes
```
* then copy the file to all other folders (7001 .. 7005) and change the port accordingly
* ![image](https://user-images.githubusercontent.com/58611230/163294743-28c07974-0c3d-46c8-8314-b3e595289145.png)

* copy **/usr/local/Cellar/redis/6.2.6/bin/redis-server** and paste it in **cluster-test** folder that we created in the first step
* open 7 tabs in a separate command window
* in 6 tabs go to folders (7000 .. 7005) and run **../redis-server ./redis.conf**
* ![image](https://user-images.githubusercontent.com/58611230/163295308-c4b19287-da54-448d-a193-c7b4da7fdd63.png)

* in the 7th tab run **redis-cli --cluster create 127.0.0.1:7000 127.0.0.1:7001 127.0.0.1:7002 127.0.0.1:7003 127.0.0.1:7004 127.0.0.1:7005 --cluster-replicas 1**
* type **yes** to confirm 
* your redis cluster should be up and running and it should look something like below -
* ![image](https://user-images.githubusercontent.com/58611230/163295267-bbadb002-7468-4414-bf9b-c22c0d03b2cf.png)
* Now run redis CLI **redis-cli -c -p 7001** for different ports and then execute commands as usual
