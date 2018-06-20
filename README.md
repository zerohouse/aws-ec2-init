# aws-ec2-init


    
    sudo su
    yum install git
    
    yum install java-1.8.0-openjdk-devel
    sudo wget http://repos.fedorapeople.org/repos/dchen/apache-maven/epel-apache-maven.repo -O /etc/yum.repos.d/epel-apache-maven.repo
    sudo sed -i s/\$releasever/6/g /etc/yum.repos.d/epel-apache-maven.repo
    sudo yum install -y apache-maven
    mvn --version
    update-alternatives --config java #pick java 1.8
    update-alternatives --config javac #pick java 1.8
    
    curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash
    . ~/.nvm/nvm.sh
    nvm install 8.11.2
      필요하면 (nvm install --lts)
      
    yum install nginx
