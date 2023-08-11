# Deploying web app using Docker Swarm
1. In AWS portal create 3 Ubuntu instances with names:
  · Swarm-manager
  · Swarm-worker1
  · Swarm-worker2
2. In all three instances, inside the inbound rules, allow
  · Custom TCP -- 2377 -- Anywhere IPv4
  · Custom TCP -- 8001 -- Anywhere IPv4
3. Install docker with docker engine on all three nodes:
   - sudo apt update
   - sudo apt install apt-transport-https ca-certificates curl software-properties-common
   - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   - echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   - sudo apt install docker-ce
   - sudo systemctl start docker
   - sudo systemctl enable docker
   - sudo docker --version
   - sudo docker run hello-world
4. Open the “Swarm Manager” node and run the command “sudo docker swarm init”. This will be creating an empty swarm
5. After initializing the swarm on the “swarm-manager” node, there will be one key generated to add other nodes into the swarm as a worker. Copy and run that key on the rest of the servers with sudo privileges
6. Check the nodes on Swarm-manager: "sudo docker node ls"
7. On Manager Node we will create a service: “sudo docker service create --name django-app-service –replicas 3 --publish 8001:8001 trainwithshubham/react-django-app:latest”
8. Run: “sudo docker service ls"
9. Check container: "sudo docker ps"
10. This service will be running on all three nodes. To check this, grab the Ip address of any nodes followed by port 8001. As <ip_of_3_ec2>:8001
11. If you want to remove any node from the environment, just run:
    - sudo docker swarm leave

Credits to Chetan Rakhra




