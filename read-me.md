From this link
https://dotnet.microsoft.com/learn/aspnet/microservice-tutorial/run-docker

fsutil file createnew Dockerfile 0
```
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY MyMicroservice.csproj .
RUN dotnet restore
COPY . .
RUN dotnet publish -c release -o /app

FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "MyMicroservice.dll"]
```
3. fsutil file createnew .dockerignore 0
4. 
```
Dockerfile
[b|B]in
[O|o]bj
```
5. ```docker build -t mymicroservice .
```
6. docker images
7. docker run -it --rm -p 3000:80 --name mymicroservicecontainer mymicroservice

