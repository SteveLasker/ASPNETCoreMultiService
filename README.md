# ASPNETCoreMultiService
A sample for scaling ASP.NET 5/Core
## Getting it going ##
Build the project
Using Visual Studio 2015, and the docker assets in the project, simply choose debug or release versions and F5 the project
Alternatively, from the root of the project, run the following PowerShell cmd

```  .\Docker\DockerTask.ps1 -Run -Environment release ```

## Scale Er Up ###
Once the project is built, use the docker-compose.scale.yml file with the following

``` docker-compose  -f .\docker\docker-compose.scale.yml up -d ```

That will instance 1 HAProxy load balancer, and one instance of your web container

``` docker-compose  -f .\docker\docker-compose.scale.yml scale web=3 ```

This will instance a total of 3 web containers

``` docker-compose  -f .\docker\docker-compose.scale.yml up --force-recreate -d ```

Since we're taking shortcuts here, just using the linked containers aspect of compose, instead of using the HAProxy configuration, we need to wait a bit for the --force-recreate to complete



