# Setup Vagrant , DNS, create virtual lab with virual box

    vagrant up
    vagrant ssh control
    cd /vagrant
   sudo cp /vagrant/hosts /etc/hosts
   cat /etc/hosts
   sudo apt-get install ansible -y

 # Add .gitignore  " .vagrant/"
# SSH control

    ssh-keygen -t ed25519 -C "vagrant default"
    ssh-copy-id node1 && ssh-copy-id node2 && ssh-copy-id node3
     
# Install Ansible

    ansible nodes -i inventory -m command -a 'sudo apt-get -y install python-simplejson'

# Test

    mkdir ansible
# make playbook   
   
    cd /ansible
    ansible nodes -i inventory -m command -a hostname
    ansible nodes -i inventory -m ping

# Ansible 'Play'book

    ansible-playbook -i inventory -K playbook1.yml
# Test docker

    ssh node1
    docker
    docker run hello-world
    
# Docker Compose node1

    cd /vagrant/docker
    docker-compose up

# Open new Terminal

    vagrant ssh control
    curl node1:5000

# Back to control and clon already swarm config from git

    git clone https://github.com/devopsjourney1/ansible-swarm-playbook.git
    
# Delete unusable file, rewrite config ethernet and copy inventory file there.

    cd /vagrant/ansible_swarm_playbook 
    ansible-playbook -i inventory -K swarm.yml
# Test 

    ssh node1
    docker node ls
    cd /vagrant/docker
    docker-compose down
    docker ps

# Connect container to Swarm, make new dir myapp, copy from docker folder file
    cd /vagrant/myapp
     
   # Edit docker-compose "  build: >>> image: devopsjourney1/myflaskimg:1 . " 
    
    docker stack deploy --compose-file docker-compose.yml myapp
    docker stack ls
    docker stack services myapp
    docker service logs -f myapp_web
    docker service ps myapp_web
    docker service update --force myapp_web
    docker stack deploy --compose-file docker-compose.yml myapp
    curl node1:5000
    docker service scale myapp_web=3








  




