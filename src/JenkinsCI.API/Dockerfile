FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src

COPY JenkinsCI.API.csproj .
RUN dotnet restore JenkinsCI.API.csproj

COPY . .
RUN dotnet build JenkinsCI.API.csproj -c Release -o /app/build

FROM build AS publish
RUN dotnet publish JenkinsCI.API.csproj -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsCI.API.dll"]
