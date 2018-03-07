# Dockerfiles for WSO2 IoT Server #
This section defines dockerfiles and step-by-step instructions to build docker images for multiple profiles <br>
provided by WSO2 IoT 3.1.0, namely : <br>
1. IoT Server
2. Analytics
3. Broker

## Prerequisites
* [Docker](https://www.docker.com/get-docker) v17.09.0 or above

## How to build an image and run

1. Checkout this repository into your local machine using the following git command.
```
git clone https://github.com/wso2/docker-iot.git
```

>The local copy of the `dockerfiles` directory will be referred to as `DOCKERFILE_HOME` from this point onwards.

2. Add JDK, WSO2 IoT distribution and required libraries
- Download [JDK 1.8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) and
extract into `<DOCKERFILE_HOME>/base/files`.
- Download [WSO2 Enterprise Integrator 6.1.1 distribution](https://wso2.com/iot) and 
extract into `<DOCKERFILE_HOME>/base/files`.
- Once both JDK and WSO2 IoT distribution is extracted, it should be as follows:
```
<DOCKERFILE_HOME>/base/files/jdk<version>
<DOCKERFILE_HOME>/base/files/wso2iot-3.1.0
```
- Download [MySQL Connector/J](https://dev.mysql.com/downloads/connector/j/) v5.1.45 and then copy that to `<DOCKERFILE_HOME>/base/files` folder

>Please refer to [WSO2 Update Manager documentation](https://docs.wso2.com/display/ADMIN44x/Updating+WSO2+Products)
in order to obtain latest bug fixes and updates for the product.

3. Build the base docker image.
- For base, navigate to `<DOCKERFILE_HOME>/base` directory. <br>
  Execute `docker build` command as shown below.
    + `docker build -t wso2iot-base:3.1.0 .`
        
4. Build docker images specific to each profile.
- For analytics, navigate to `<DOCKERFILE_HOME>/analytics` directory. <br>
  Execute `docker build` command as shown below. 
    + `docker build -t wso2iot-analytics:3.1.0 .`
- For broker, navigate to `<DOCKERFILE_HOME>/broker` directory. <br>
  Execute `docker build` command as shown below. 
    + `docker build -t wso2iot-broker:3.1.0 .`
- For iot-server, navigate to `<DOCKERFILE_HOME>/iot-server` directory. <br>
  Execute `docker build` command as shown below. 
    + `docker build -t wso2iot-server:3.1.0 .`
    
5. Running docker images specific to each profile.
- For analytics,
    + `docker run -p 9445:9445 -p 9612:9612 -p 9712:9712 wso2iot-analytics:3.1.0`
- For broker,
    + `docker run -p 9446:9446 -p 5675:5675 wso2iot-broker:3.1.0`
- For iot-server,
    + `docker run -p 9443:9443 -p 9612:9612 -p 9712:9712 wso2iot-server:3.1.0`

6. Accessing management consoles.
- For Devicemgt,
    + `https:<DOCKER_HOST>:9443/devicemgt`
- For App publisher,
    + `https:<DOCKER_HOST>:9443/publisher`
    
>In here, <DOCKER_HOST> refers to hostname or IP of the host machine on top of which containers are spawned.

## How to update configurations
Configurations would lie on the Docker host machine and they can be volume mounted to the container. <br>
As an example, steps required to change the port offset of integrator profile using `carbon.xml` is as follows.

##### 1. Stop the iot-server container if it's already running.
In WSO2 IoT 3.1.0 product distribution, carbon.xml file for the iot-server profile <br>
can be found at `<DISTRIBUTION_HOME>/conf`. Copy the file to some suitable location of the host machine, <br>
referred to as `<SOURCE_CONFIGS>/carbon.xml` and change the offset value under ports to 1.

##### 2. Grant read permission to `other` users for `<SOURCE_CONFIGS>/carbon.xml`
```
chmod o+r <SOURCE_CONFIGS>/carbon.xml
```

##### 3. Run the image by mounting the file to container as follows.
```
docker run 
-p 9444:9444 -p 9613:9613 -p 9713:9713
--volume <SOURCE_CONFIGS>/carbon.xml:<TARGET_CONFIGS>/carbon.xml
wso2iot-server:3.1.0
```

>In here, <TARGET_CONFIGS> refers to /home/wso2carbon/wso2iot-3.1.0/conf folder of the container.


## Docker command usage references

* [Docker build command reference](https://docs.docker.com/engine/reference/commandline/build/)
* [Docker run command reference](https://docs.docker.com/engine/reference/run/)
* [Dockerfile reference](https://docs.docker.com/engine/reference/builder/)

