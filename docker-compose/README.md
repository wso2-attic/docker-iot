# WSO2 IoT Server and Broker with Analytics support

## Prerequisites

 * Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git), [Docker](https://www.docker.com/get-docker) and [Docker Compose](https://docs.docker.com/compose/install/#install-compose)
   in order to run the steps provided in following Quick start guide. <br><br>
  * In order to run this Docker Compose setup, you will need an active [Free Trial Subscription](https://wso2.com/free-trial-subscription) 
   from WSO2 since the referring Docker images hosted at docker.wso2.com contains the latest updates and fixes for WSO2 IoT Server. You can sign up for a Free Trial Subscription [here](https://wso2.com/free-trial-subscription). <br><br>
  * If you wish to run the Docker Compose setup using Docker images built locally, build IoT Server, Broker,
   Analytics Images using [Dockerfiles](../dockerfiles/README.md) and remove the `docker.wso2.com/` prefix 
   from the `image` name In the `docker-compose.yml`. For example, change the line `image: docker.wso2.com/wso2iot-server:3.2.0` 
   to `image: wso2iot-server:3.2.0`. <br><br>

## How to Run

  1. Clone WSO2 IoT Server Docker git repository.
     ```
      git clone https://github.com/wso2/docker-iot
     ```
     > Note that the local copy of `docker-iot` repository will be referred to as `[docker-iot]` from this point onwards.

  2. Switch to docker-compose folder :
     ```
     cd docker-iot/docker-compose
     ```

  3. Execute following Docker Compose command to start the deployment :
     ```
     docker-compose up
     ```

  4. Access management console via a web browser :
     ```
     For Devicemgt - https://localhost:9443/devicemgt
     For App Publisher - https://localhost:9443/publisher
     ```


