## Runtime image
#FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
#WORKDIR /app
#EXPOSE 80
#
## Build image
#FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
#WORKDIR /src
#
#COPY JenkinsCI.API.csproj .
#RUN dotnet restore JenkinsCI.API.csproj
#
#COPY . .
#RUN dotnet build JenkinsCI.API.csproj -c Release -o /app/build
#
## Publish
#FROM build AS publish
#RUN dotnet publish JenkinsCI.API.csproj -c Release -o /app/publish
#
## Final image
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "JenkinsCI.API.dll"]
#
# Runtime image
FROM mcr.microsoft.com/dotnet/aspnet:9.0 AS base
WORKDIR /app
EXPOSE 80
ENV ASPNETCORE_URLS=http://+:80

# Build image
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
WORKDIR /src

# Copy csproj and restore
COPY JenkinsCI.API.csproj .
RUN dotnet restore JenkinsCI.API.csproj

# Copy rest of the files and build
COPY . .
RUN dotnet build JenkinsCI.API.csproj -c Release -o /app/build

# Publish
FROM build AS publish
RUN dotnet publish JenkinsCI.API.csproj -c Release -o /app/publish

# Final image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsCI.API.dll"]
