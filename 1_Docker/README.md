# Основы контейнеров
## Что такое Контейнеры?
Контейнеры — это логические конструкции, содержащие двоичные файлы приложения. Двоичные файлы контейнеров работают на более высоком уровне абстракции инфраструктуры, чем виртуальные машины. В отличие от виртуальной машины, которая предоставляет всю операционную систему для обеспечения среды выполнения двоичных файлов приложения, контейнер объединяет только двоичные файлы приложения и его необходимые библиотеки.

Важно отметить, что виртуальные машины и контейнеры не исключают друг друга. Инфраструктурой (сетями, серверами и хранилищем), необходимой для поддержки контейнеров, часто легче управлять с помощью виртуализации, поэтому эти две технологии дополняют друг друга.

Как правило, термин контейнер используется для обозначения либо образа контейнера, либо экземпляра работающего контейнера. Когда вы запускаете контейнер, уровень абстракции, среда выполнения контейнера, планирует доступ к общей операционной системе. Стандарты контейнеров разрабатываются инициативой [Open Container Initiative](https://opencontainers.org/), которая в настоящее время имеет спецификации как для среды выполнения контейнера, так и для образа контейнера.


## Среда выполнения контейнера

Хотя Docker является наиболее популярным примером среды выполнения контейнера, существуют и другие, такие как containerd, rkt и т. д.


Подобно тому, как ядро Linux помогает запускать процессы приложений, предоставляя аппаратные ресурсы, среда выполнения контейнера помогает разделить ядро Linux для запуска изолированных процессов Linux с определенными ограничениями ресурсов для ЦП, памяти и т. д. Среда выполнения также помогает изолировать процессы приложений, используя два ядра Linux. примитивы: [контрольные группы (cgroups)](https://man7.org/linux/man-pages/man7/cgroups.7.html) и [пространства имен](https://man7.org/linux/man-pages/man7/namespaces.7.html). Cgroups ограничивают ресурсы набором процессов, работающих на хосте Linux, а пространства имен изолируют процессы друг от друга.


![image](https://user-images.githubusercontent.com/79700810/196975434-bc0a0a42-e183-4af4-a701-3b063ceab4a4.png)

Работающий контейнер — это набор процессов (обычно приложение), которые поддерживает среда выполнения контейнера, обеспечивая создание необходимых конструкций в ядре для ограничения потребления ресурсов и обеспечения изоляции.

![image](https://user-images.githubusercontent.com/79700810/196975523-a735587c-182e-49e1-ac26-1a4f3edaff7a.png)

## Как помогают контейнеры?
Поскольку контейнеры работают на более высоком уровне абстракции, чем виртуальные машины, они улучшают переносимость приложений, эластичность сервера и использование ресурсов сервера. Среда выполнения контейнера может планировать работу нескольких контейнеров в общей операционной системе, что выгодно как операторам инфраструктуры, так и разработчикам приложений.

Преимущества для операционных, инфраструктурных и ИТ-команд

1. Снижает размер операционной системы, которой необходимо управлять на серверах.

2. Снижает зависимость приложения от операционной системы

3. Облегчает техническое обслуживание и сокращает периоды обслуживания


Преимущества для команд разработки приложений

1. Поскольку контейнеры отделяют приложение и его зависимости от операционной системы, команды разработчиков могут не создавать несколько тестовых сред с различными операционными системами для проверки поведения приложения.

2. Оптимизирует конвейер разработки, чтобы сократить время создания и доставки приложений.

Все эти преимущества дают убедительный результат: контейнеры сокращают время, необходимое для создания, тестирования и доставки приложений.

Контейнеры помогают ускорить конвейеры разработки, оптимизируя циклы разработки/тестирования и сокращая усилия, необходимые для развертывания приложений. Они последовательно выполняются в каждом развертывании, обеспечивая переносимость между платформами и между облаками. Контейнеры повышают эффективность и гибкость организации.

## Instal WSL
```powershell
wsl --unregister Ubuntu-20.04

wsl --list --onlin

wsl --install -d Ubuntu-20.04

wsl --list
```

![image](https://user-images.githubusercontent.com/79700810/196971403-0b6f821b-07d8-4896-8875-8e17e578f909.png)

# Install Docker
```
sudo -i
apt-get update
apt-get install -y ca-certificates curl gnupg lsb-release
```

![image](https://user-images.githubusercontent.com/79700810/196971710-b2e502cf-285a-42b1-8a83-ba462fe037aa.png)

```
mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
```
apt-get update
apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```

![image](https://user-images.githubusercontent.com/79700810/196971959-4b2a40e3-5803-4ada-91eb-62b4fe15e5d5.png)

```
service docker start
```

# Create folder

```
mkdir /home/user/docker
chmod -R 777 /home/user/docker/
```

![image](https://user-images.githubusercontent.com/79700810/196972322-82cf36d4-ad0c-4f89-ac51-770f1b4ed6f3.png)


## Dockerfile

hello.py

from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"



Dockerfile

# syntax=docker/dockerfile:1
FROM ubuntu:22.04

# install app dependencies
RUN apt-get update && apt-get install -y python3 python3-pip
RUN pip install flask==2.1.*

# install app
COPY hello.py /

# final configuration
ENV FLASK_APP=hello
EXPOSE 8000
CMD flask run --host 0.0.0.0 --port 8000


docker build -t hello:latest .


docker run --name hello -p 8000:8000 -d hello:latest










docker run docker.io/busybox:latest date



docker run -it busybox sh

ps

docker run --rm -d --name httpd -p 8080:80 busybox httpd -f -vv


###

docker ps -a
docker rm $(docker ps -aq)
###

docker build -t greeting .

docker history greeting


docker run --rm greeting

docker run --rm greeting /goodbye






docker rmi greeting
docker build -t greeting .
docker run -it --rm greeting /bin/bash
