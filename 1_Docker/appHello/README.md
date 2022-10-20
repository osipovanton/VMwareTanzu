docker run -it busybox sh
ps

docker build -t hellogoodbye .
docker history hellogoodbye

docker run --rm hellogoodbye
docker run --rm hellogoodbye /goodbye