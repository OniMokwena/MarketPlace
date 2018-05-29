FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 58996
EXPOSE 44373

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY MarketPlaceCode/MarketPlaceCode.csproj MarketPlaceCode/
RUN dotnet restore MarketPlaceCode/MarketPlaceCode.csproj
COPY . .
WORKDIR /src/MarketPlaceCode
RUN dotnet build MarketPlaceCode.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish MarketPlaceCode.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MarketPlaceCode.dll"]
