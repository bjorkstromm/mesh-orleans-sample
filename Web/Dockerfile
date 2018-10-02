FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 20007

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Web/Web.csproj Web/
RUN dotnet restore Web/Web.csproj
COPY . .
WORKDIR /src/Web
RUN dotnet build Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Web.dll"]