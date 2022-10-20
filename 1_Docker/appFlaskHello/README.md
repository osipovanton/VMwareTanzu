https://docs.docker.com/build/building/packaging/

docker build -t FlaskHello:latest .

docker run -p 8000:8000 FlaskHello:latest
