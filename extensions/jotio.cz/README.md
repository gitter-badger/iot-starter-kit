# Setting up a Platforms

# Run Docker 
Install Docker -> See the inspiration [here](https://github.com/iqrfsdk/iqrf-daemon/blob/master/DOCKER.md)

# Setup Node-RED ecosystem 
### docker_net
```Bash
sudo docker network create -d bridge --subnet 172.25.0.0/16 isolated_nw
```
### MQTT Broker
```Bash
sudo docker run -d --name mqtt -p 1883:1883 -p 9001:9001 --network=isolated_nw --ip=172.25.3.1 --restart=always eclipse-mosquitto 
```
### NodeRed
```Bash
sudo docker run -d -p 1880:1880 --restart=always --name redgw nodered/node-red-docker
sudo docker network connect isolated_nw redgw
sudo docker exec -it redgw /bin/bash
npm i node-red/node-red-dashboard
npm i node-red-node-watson
npm i node-red-contrib-scx-ibmiotapp
exit
sudo docker restart redgw
```
### configure NodeRed Flow
Open:
http://[IP address of UpBoard]:1880

Import the contents of this [file](https://github.com/iqrfsdk/iot-starter-kit/blob/master/extensions/jotio.cz/Nodered_Local_demo.json) into nodered. 



