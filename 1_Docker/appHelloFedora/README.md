docker build -t hellogoodbyefedora .
docker history hellogoodbyefedora

docker run --rm hellogoodbyefedora
docker run --rm hellogoodbyefedora /goodbye
docker run -it --rm hellogoodbyefedora /bin/bash