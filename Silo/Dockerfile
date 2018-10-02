FROM microsoft/dotnet:2.1-runtime-nanoserver-1709 AS base
WORKDIR /app

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Silo/Silo.csproj Silo/
RUN dotnet restore Silo/Silo.csproj
COPY . .
WORKDIR /src/Silo
RUN dotnet build Silo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Silo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Silo.dll"]