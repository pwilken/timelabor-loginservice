FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY LoginService.sln ./
COPY LoginService/LoginService.csproj LoginService/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/LoginService
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LoginService.dll"]
