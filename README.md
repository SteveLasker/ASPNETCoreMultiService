# ASPNETCoreMultiService
A sample for scaling ASP.NET 5 Core
Uses 
- ASP.NET 5
- HAProxy
- Docker Containers
- Running in Linux
- [Docker Tools for Visual Studio](http://aka.ms/DockerToolsForVS)
 

## Getting it going ##
Build the project
Using Visual Studio 2015, and the docker assets in the project, simply choose debug or release versions and F5 the project
Alternatively, from the root of the project, run the following PowerShell cmd

```  .\Docker\DockerTask.ps1 -Run -Environment release ```

## Scale Er Up ###
Once the project is built, use the DockerTask.ps1 script with the docker-compose.scale.yml config file:

``` .\Docker\DockerTask.ps1 -Run -Environment scale -machine default ```

Or, use docker-compose directly

``` docker-compose  -f .\docker\docker-compose.scale.yml up -d ```

That will instance 1 HAProxy load balancer, and one instance of your web container

``` docker-compose  -f .\docker\docker-compose.scale.yml scale web=3 ```

This will instance a total of 3 web containers

``` docker-compose  -f .\docker\docker-compose.scale.yml up --force-recreate -d ```

Since we're taking shortcuts here, just using the linked containers aspect of compose, instead of using the HAProxy configuration, we need to wait a bit for the --force-recreate to complete

## It's a visual world ##
To get a sense of what's going on, use this handy dandy visualizer from the docker team:

``` docker run -d -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock dockerui/dockerui ```
