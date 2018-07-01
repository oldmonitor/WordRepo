FROM microsoft/aspnetcore:2.0-nanoserver-1709 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0-nanoserver-1709 AS build
WORKDIR /src
COPY WordRepo.Web/WordRepo.Web.csproj WordRepo.Web/
RUN dotnet restore WordRepo.Web/WordRepo.Web.csproj
COPY . .
WORKDIR /src/WordRepo.Web
RUN dotnet build WordRepo.Web.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish WordRepo.Web.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WordRepo.Web.dll"]
