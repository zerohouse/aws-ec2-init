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

### 4. 스프링부트 서비스 등록
    sudo ln -s /var/myapp/myapp.jar /etc/init.d/myapp
    service myapp start
