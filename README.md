# ASPNETCoreMultiService
A sample for scaling ASP.NET 5 Core that uses:
- ASP.NET 5
- HAProxy
- Docker Containers
- Running in Linux
- [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)
 

## Getting it going ##
First, lets clear out any containers. It's a good idea to give us a clean state
``` docker rm -f $(docker ps -a -q) ```

Build the project
Using Visual Studio 2015, open the project. We've already included the docker assets for debug, release, and scale. 

From within Visual Studio, simply choose debug or release and build the project. 

Alternatively, from the root of the project, run the following PowerShell cmd

```  .\Docker\DockerTask.ps1 -Run -Environment release -ProjectName web -machine default ```

## Scale Er Up ###
Scale up to a total of 3 web containers

``` docker-compose -f .\docker\docker-compose.scale.yml -p web scale web=3 ```

Reset HAProxy to route to the additional containers:

``` docker-compose -f .\docker\docker-compose.scale.yml -p web up --force-recreate -d ```

*Since we're taking shortcuts here, just using the linked containers aspect of compose, instead of using the HAProxy configuration, we need to wait a bit for the --force-recreate to complete*

## It's a visual world ##
To get a sense of what's going on, use this handy dandy visualizer from the docker team:

``` docker run -d -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock dockerui/dockerui ```
