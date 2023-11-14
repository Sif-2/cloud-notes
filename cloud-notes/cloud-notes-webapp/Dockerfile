FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["cloud-notes-webapp/cloud-notes-webapp.csproj", "cloud-notes-webapp/"]
RUN dotnet restore "cloud-notes-webapp/cloud-notes-webapp.csproj"
COPY . .
WORKDIR "/src/cloud-notes-webapp"
RUN dotnet build "cloud-notes-webapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "cloud-notes-webapp.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "cloud-notes-webapp.dll"]
