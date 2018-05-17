FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 64649
EXPOSE 44317

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY IntegrationManager/IntegrationManager.csproj IntegrationManager/
RUN dotnet restore IntegrationManager/IntegrationManager.csproj
COPY . .
WORKDIR /src/IntegrationManager
RUN dotnet build IntegrationManager.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish IntegrationManager.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "IntegrationManager.dll"]
