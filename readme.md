# Project TvCast  
## TvCast.Api  
Main Api to Access show and cast data.  

## TvCast.ApiWorker  
Worker process to find show information in tvmaze and download the show data.

## TvCast.Domain  
Domain library to translate entities to the view engines.  

## TvCast.Entity  
Entity Frameowkr 6 project to perform data access operations.

## Requirements
* NodeJS for gulp tasks : https://nodejs.org/en/  
* Docker Toolbox for testing in containers: https://github.com/docker/toolbox/releases  
* `dotnet 3.1` installed and available. Run the command `dotnet --info`: https://dotnet.microsoft.com/download/dotnet-core/3.1  
* Postman to test the environments: https://www.postman.com/  



## Obs  
The models and entities are self explanatory.  
* There is only one Api called shows, which requires a page and a page size to query. 
* There is a worker to fetch data from the tvmaze api into the database. 
* I decided to use postgresql as database for the fast implementation to query json data columns. 
`This Can be replaced by azure tables and azure storage if needed`  
* The cycle for the worker is set to 3s to avoid blockage on the tvmaze api, otherwise it'll throw 403.  
* `Install NodeJS 10+ in order to perform tasks automatically.`  
* `The solution is supposed to run on Docker, to make it easier to deploy tagged images into azure containers.` 
* `There are unit tests only for the Repositories using Moq`. 
* `Some actors don't have birthday due to tvmaze missing data`.

# Running on Docker  
On the parent solution folder perform the commands:  
`Attention: NodeJS installation is required for running gulp`.
```
yarn
gulp
```

## Testing With Postman  
Install Postman  
Import the files:
* `TvCast.postman_collection.json`
* `local.postman_environment.json`
* `docker.postman_environment.json`

`WARNING: the docker.postman_environment.json is pointing to the ip 192.168.99.101, change it to your docker-machine ip instead`'.

## Check what's going on  
It's simple to see what's up within the containers  
Just issue the following command in a shell under the project folder: 
```
gulp logs
```

## Stop Containers  
If you want to stop the containers just issue the command:  
```
gulp stop
```

## Destroy the Containers 
To completely destroy the containers.
```
gulp down
```