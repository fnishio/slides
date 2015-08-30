Docker Meetup Tokyo #5
================================
2015年8月19日のDocker Meetup Tokyo #5のメモ

Docker for Developer Experience
---------------------------------
by Nathan LeClaire@Docker (@upthecyberpunks)

- Who is Nathan ?
 - open source
 - docker-machineの中の人
- docker
 - container = process with special peroperties.
 - cgroup name space
 - setting up and maintaining a developement environment.
- docker machine demo
 - customize docker daemon with 'create' settings
 - `--engine-log-driver=fluentd`
- docker compose
 - gitlabをdockerで動かす
- docker toolbox でたよ！
- Future
 - __toward production solution__ !
 - production-grade logging, load balancing, failover etc.

My notes:
ProductionでDocker使っている人はまだ多くない。会場のアンケートでもそんな感じ。
Productionがつぎのステップ。これ見とけ→
[Running Aground: Debugging Docker in Prodution](https://www.youtube.com/watch?v=sYQ8j02wbCY)@YouTube


未定(Kubernetes)
----------------------------------
by Mandy Waite@google (@tekgrri)

- Kubernetes
 - orchestrator for doker
 - supports multi-cloud environments
 - manage applications, not machines.
 - cluster matrix
 - pods
   - the atom of scheduling for containers.
   - "logical host"
   - can be used to group containers & shared volumes
 - Borgs
 - Labels
 - Replication Controllers
- demo
  - visualization

My notes: termからして未知のものでした。Kubernetesは__k8s__と略すと玄人っぽい、ということだけはわかった（笑）


Building Distributed Systems with CoreOS
-----------------------------------------
by Kelsey Highttower@CoreOS

- Distributed System
  - scalability
  - high available
  - fault tolerance
  - consist operation
- CoreOS Linux
 - docker
 - etcd
  - key value store
  - lock service
- k8s

My notes:
CoreOSの話というよりk8s. で撃沈。

docker and fluentd
--------------------
by Masahiro Nakagawa@Treasure Data

- fluentd
 - Logging for containers
 - unified logging layer
- log aggregation
 - 1-level aggregation
 - 2-level aggregation 1つのHOSTに1つ集約用のfluentd
- fluentd driver is coming from docker 1.8
 - `--log-driver=fluentd`
 - see fluent/fluentd

My notes:
docker containerのlogはfluentdで！

LT: http2
--------
Go langの@bradfitzがhttp2。
