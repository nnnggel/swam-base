# swam-base is a docker image for ethereum-swam based on centos7

# install docker
See: [https://docs.docker.com/engine/install/](https://docs.docker.com/engine/install/)

# pull image
> docker pull qnzxbyz735/swam-base:v1

*Image: [https://hub.docker.com/r/qnzxbyz735/swam-base](https://hub.docker.com/r/qnzxbyz735/swam-base)*  

# run container
> docker run -d -i --network host --name swam qnzxbyz735/swam-base:v1

*For convenience, here we use the host network mode.*  

# start bash-shell in container
> docker exec -it swam /bin/bash

*Now, you're in container.*


# command in container

## install clef and bee
> cd /mnt/bee
> rpm -i bee-clef_0.4.10_amd64.rpm
> rpm -i bee_0.5.3_amd64.rpm

### Find out ADDRESS
> ls /var/lib/bee-clef/keystore/

*You can see a file named 'UTC--datetime--XXX' here, let's say the ADDRESS is XXX.*

## transfer gBZZ and eth to address(XXX)
### option1(easy way) - discord
https://discord.gg/zCwPuTvgtY

### option2 - DIY
https://bzz.ethswarm.org/?transaction=buy&amount=10&slippage=30&receiver=XXX
*Replace the last XXX with your address.*
![image](https://user-images.githubusercontent.com/17697169/117391599-d6a7c480-af22-11eb-924a-77ec404b9e58.png)


## start clef
### start with screen
> screen -S clef
> ./clef-service.sh start
> →Ctrl a+d

*Ctrl a+d means "let current screen run in background".*

## start bee
### create node on infura
[infura](https://infura.io/)
*regist(free account) -> create new project -> copy endpoint(gorli) url, let's say the endpoint url is  ENDPOINT_URL.*
![image](https://user-images.githubusercontent.com/17697169/117391556-baa42300-af22-11eb-9ba4-ae39d6557358.png)


### start with screen
> screen -S bee
> vi ./bee-start.sh
bee start --verbosity 5 --swap-endpoint ENDPOINT_URL --api-addr :1633 --p2p-addr :1634 --debug-api-addr :1635 --debug-api-enable --clef-signer-enable
./bee-start.sh
→Ctrl a+d

*Replace the ENDPOINT_URL with your endpoint url which you copied on infura.*
*Here we use 1633/1634/1635 as the default ports, you can replace it with other ports.*
*You need to set a password at startup.*
*Ctrl a+d means "let current screen run in background".*

## !!! the last and the most important thing: save your credential infomation !!!
### password file
> /var/lib/bee-clef/password

### keystore file
> /var/lib/bee-clef/keystore/UTC--datetime--XXX

**These two files are important, copy them to a save place. Or you'll lost control of your account.**  


