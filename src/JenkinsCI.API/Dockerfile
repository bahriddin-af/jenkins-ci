FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["src/JenkinsCI.API/JenkinsCI.API.csproj", "JenkinsCI.API/"]
RUN dotnet restore "JenkinsCI.API/JenkinsCI.API.csproj"
COPY . .
WORKDIR "/src/JenkinsCI.API"
RUN dotnet build "JenkinsCI.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "JenkinsCI.API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsCI.API.dll"]
