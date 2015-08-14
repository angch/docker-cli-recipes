# Docker CLI recipes

## Stops all running docker containers

When doing development, and some clusters of containers are still using some of your ports

```
docker ps | awk '{print $1}' | tail -n+2 | xargs docker stop
```

## Mirror/vendor an external docker image

If all developers are using the same large external image and you want to save 10+ developers
from hammering docker's official servers (or when it's slow), and you have a local docker registry
on your LAN that's faster

```
IMAGE=postgres:9.4
LOCALREG=myregistry.local
docker pull $IMAGE
docker tag $IMAGE $LOCALREG/$IMAGE
docker push $LOCALREG/$IMAGE
```
So other developers and your project's docker-compose can just refer to $LOCALREG/$IMAGE for faster
image downloads
