FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY Players/PlayerApi.csproj Players/
RUN dotnet restore Players/PlayerApi.csproj
COPY . .
WORKDIR /src/Players
RUN dotnet build PlayerApi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish PlayerApi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PlayerApi.dll"]
