mkdir mbcwebapi
cd mbcwebapi


Michaels-MacBook-Pro:mbcwebapi mbcrump$ dotnet new webapi
The template "ASP.NET Core Web API" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/template-3pn for details.

Processing post-creation actions...
Running 'dotnet restore' on /Users/mbcrump/mbcwebapi/mbcwebapi.csproj...
  Restoring packages for /Users/mbcrump/mbcwebapi/mbcwebapi.csproj...
  Restore completed in 35.83 ms for /Users/mbcrump/mbcwebapi/mbcwebapi.csproj.
  Generating MSBuild file /Users/mbcrump/mbcwebapi/obj/mbcwebapi.csproj.nuget.g.props.
  Generating MSBuild file /Users/mbcrump/mbcwebapi/obj/mbcwebapi.csproj.nuget.g.targets.
  Restore completed in 1.96 sec for /Users/mbcrump/mbcwebapi/mbcwebapi.csproj.


Restore succeeded.

Create Dockerfile

FROM microsoft/aspnetcore:2.0
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", "mbcwebapi.dll"]

docker-compose.yml

version: '3'

services:
  mbcwebapi:
    image: mbcrump/mbcwebapi
    build:
      context: ./mbcwebapi
      dockerfile: Dockerfile

Michaels-MacBook-Pro:mbcwebapi mbcrump$ dotnet restore
  Restore completed in 51.98 ms for /Users/mbcrump/mbcwebapi/mbcwebapi.csproj.
  Restore completed in 37.25 ms for /Users/mbcrump/mbcwebapi/mbcwebapi.csproj.

Michaels-MacBook-Pro:mbcwebapi mbcrump$ dotnet publish -c Release -o ./obj/Docker/publish
Microsoft (R) Build Engine version 15.3.409.57025 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  mbcwebapi -> /Users/mbcrump/mbcwebapi/bin/Release/netcoreapp2.0/mbcwebapi.dll
  mbcwebapi -> /Users/mbcrump/mbcwebapi/obj/Docker/publish/
Michaels-MacBook-Pro:mbcwebapi mbcrump$ 

make sure the folder is cleaned like the following

Michaels-MacBook-Pro:mbcwebapi mbcrump$ ls -l
total 8
-rw-rw-rw-@  1 mbcrump  staff  141 Nov 19 21:32 docker-compose.yml
drwxr-xr-x  12 mbcrump  staff  384 Nov 19 21:33 mbcwebapi
Michaels-MacBook-Pro:mbcwebapi mbcrump$ 


Michaels-MacBook-Pro:mbcwebapi mbcrump$ docker-compose up
Creating network "mbcwebapi_default" with the default driver
Building mbcwebapi
Step 1/6 : FROM microsoft/aspnetcore:2.0
 ---> 757f574feed9
Step 2/6 : ARG source
 ---> Using cache
 ---> 96deb3aec068
Step 3/6 : WORKDIR /app
 ---> Using cache
 ---> c0fecb757aa4
Step 4/6 : EXPOSE 80
 ---> Using cache
 ---> e4f034c54397
Step 5/6 : COPY ${source:-obj/Docker/publish} .
 ---> 6bd68f6553c4
Step 6/6 : ENTRYPOINT dotnet mbcwebapi.dll
 ---> Running in 7036d9913baa
 ---> 90384b8ed543
Removing intermediate container 7036d9913baa
Successfully built 90384b8ed543
Successfully tagged mbcrump/mbcwebapi:latest
WARNING: Image for service mbcwebapi was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating mbcwebapi_mbcwebapi_1 ... 
Creating mbcwebapi_mbcwebapi_1 ... done
Attaching to mbcwebapi_mbcwebapi_1
mbcwebapi_1  | warn: Microsoft.AspNetCore.DataProtection.Repositories.FileSystemXmlRepository[60]
mbcwebapi_1  |       Storing keys in a directory '/root/.aspnet/DataProtection-Keys' that may not be persisted outside of the container. Protected data will be unavailable when container is destroyed.
mbcwebapi_1  | warn: Microsoft.AspNetCore.DataProtection.KeyManagement.XmlKeyManager[35]
mbcwebapi_1  |       No XML encryptor configured. Key {70d9c953-b38f-4e26-92d2-6a07557aaefc} may be persisted to storage in unencrypted form.
mbcwebapi_1  | Hosting environment: Production
mbcwebapi_1  | Content root path: /app
mbcwebapi_1  | Now listening on: http://[::]:80
mbcwebapi_1  | Application started. Press Ctrl+C to shut down.

