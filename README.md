sudo yum install nginx
sudo dnf install java-17-amazon-corretto-devel


### aws-ec2-init


 
    sudo su
    
### 1. 깃 깔고
    yum install git
    
### 2. 자바 / 메이븐 깔고
    yum install java-1.8.0-openjdk-devel
    sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
    sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
    sudo yum install -y apache-maven
    mvn --version
    update-alternatives --config java #pick java 1.8
    update-alternatives --config javac #pick java 1.8
    
### 3. 노드 깔고
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
    . ~/.nvm/nvm.sh
    nvm install 8.11.2
    nvm install --lts
      
### 3. 엔진엑스 깔고
    yum install nginx
    amazon-linux-extras install nginx1.12

### 4. 스프링부트 서비스 등록
    sudo ln -s /var/myapp/myapp.jar /etc/init.d/myapp
    service myapp start

### 5. Nginx 설정해볼까
     location /api {
         proxy_pass   http://127.0.0.1:8080;
     }

### 6. 시간 설정
    sudo rm /etc/localtime
    sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

### 7. Nginx에서 프록시 IP 가져오려면

    http {
    real_ip_header X-Forwarded-For;
    set_real_ip_from 0.0.0.0/0;
    ...
    }
    and with main nginx proxy gitlab.conf

    server {
        listen       80;
        server_name  gitlab-domain.com;
        client_max_body_size 640M;
        client_body_buffer_size 1M;

       location / {

        proxy_set_header  Host $host;
        proxy_set_header  X-Real-IP $remote_addr;
        proxy_set_header  X-Forwarded-Proto https;
        proxy_set_header  X-Forwarded-For $remote_addr;
        proxy_set_header  X-Forwarded-Host $server_name;
        proxy_pass http://gitlab-ec2-ip:10080/;

            }
    }

### 8. Ngix swagger host
  
            proxy_pass         http://localhost:8080; #change to your port
            proxy_redirect     off;

            proxy_set_header   Host              $host;
            proxy_set_header   X-Real-IP         $remote_addr;
            proxy_set_header   X-Forwarded-For   $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Proto $scheme;


### 9. 그래들 서비스 레지스트레이션시 
    chmod 500 [name].jar
    
    +build.gralde내에 아래 내용 추가
    
    bootJar {
     launchScript()
    }



## 10 이미지 서버

  https://drive.google.com/file/d/1bwvoHU72rgYdLbTS42gKVXo73AQzMUh1/view?usp=sharing
  https://aws.amazon.com/ko/blogs/compute/resize-images-on-the-fly-with-amazon-s3-aws-lambda-and-amazon-api-gateway/
  

