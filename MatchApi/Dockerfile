FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY MatchApi/MatchApi.csproj MatchApi/
RUN dotnet restore MatchApi/MatchApi.csproj
COPY . .
WORKDIR /src/MatchApi
RUN dotnet build MatchApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MatchApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MatchApi.dll"]
