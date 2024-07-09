#Documentação projeto docker



**VPC**  
**Sub-net**  

    2 subnets publicas  
    2 privadas  
**config nat-gatway e internet gatway**   
**route table***  

    **publico**   
        igw-  
        subnet publica  
    **privado**
        nat-
        subnet privada
**instancias**

    ubuntu t3.small
    2 instancias privadas  
    us-east-1b | us-east-1c
**classic load balancer** 

    vicular 2 instancias
**script user_data**  

    #!/bin/bash  
    apt update
    apt install -y docker.io
    systemctl start docker
    systemctl enable docker

**configuração console aws**

    endpoint
    classic load balancer
    efs
    rds


**acessando ec2 via endpoint***

    **verificando docker --version**
    **instalando docker-compose** 
        apt install docker-compose

    **verificando status do docker**
        systemctl status docker
    **mkdir Wordpress-DockerCompose**
        cd Wordpress-DockerCompose

 nano docker-compose.yml

    version: '3.1'

    services:

    wordpress:
        image: wordpress
        restart: always
        environment:
        WORDPRESS_DB_HOST: mysqlwordpress.cpiwgcu2cf0j.us-east-1.rds.amazonaws.com
        WORDPRESS_DB_USER: leninha
        WORDPRESS_DB_PASSWORD: Senha123
        WORDPRESS_DB_NAME: mysqlwordpress
        volumes:
        - wordpress:/var/www/html

    db:
        image: mysql:8.0
        restart: always
        environment:
        MYSQL_DATABASE: mysqlwordpress
        MYSQL_USER: leninha
        MYSQL_PASSWORD: Senha123
        MYSQL_RANDOM_ROOT_PASSWORD: '1'
        volumes:
        - db:/var/lib/mysql

    volumes:
    wordpress:
    db:

**deploy**  
    docker-compose up -d  
**verificar**  
docker ps -a
