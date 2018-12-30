FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY GameApi/GameApi.csproj GameApi/
RUN dotnet restore GameApi/GameApi.csproj
COPY . .
WORKDIR /src/GameApi
RUN dotnet build GameApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish GameApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "GameApi.dll"]
