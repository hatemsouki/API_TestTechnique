# Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY "API_TestTechnique.csproj" .
RUN dotnet restore "API_TestTechnique.csproj"
COPY . .
RUN dotnet build "API_TestTechnique.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "API_TestTechnique.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "API_TestTechnique.dll"]