https://docs.docker.com/build/building/packaging/

docker build -t FlaskHello:latest .

docker run --name hello -p 8000:8000 -d hello:latest
