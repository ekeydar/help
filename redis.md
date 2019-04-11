## redis with docker

* Pull redis

```bash
docker pull redis
```


* Create local volumes (so it would be persistent)
```bash
mkdir -p $HOME/docker/volumes/redis 
```

* Run 
```bash
docker run --name my-redis -d redis redis-server --appendonly yes -v $HOME/docker/volumes/docker:/data
```

