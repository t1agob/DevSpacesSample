FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["chuck.web.csproj", "./"]
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
RUN dotnet build "chuck.web.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "chuck.web.csproj" -c Release -o /app

FROM base AS final
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "chuck.web.dll"]