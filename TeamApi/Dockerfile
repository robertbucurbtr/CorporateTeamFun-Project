FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY TeamApi/TeamApi.csproj TeamApi/
RUN dotnet restore TeamApi/TeamApi.csproj
COPY . .
WORKDIR /src/TeamApi
RUN dotnet build TeamApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish TeamApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TeamApi.dll"]
