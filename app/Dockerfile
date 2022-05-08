FROM mcr.microsoft.com/dotnet/sdk:3.1-buster AS build
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY WebApplication7/*.csproj .
RUN dotnet restore

# Copy everything else and build website
COPY WebApplication7/. .
RUN dotnet publish -c release -o /WebApp --no-restore

# Final stage / image
FROM mcr.microsoft.com/dotnet/aspnet:3.1-buster-slim AS base
WORKDIR /WebApp
COPY --from=build /WebApp ./
ENTRYPOINT ["dotnet", "WebApplication7.dll"]
