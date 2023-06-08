#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["network_monitoring_web/network_monitoring_web.csproj", "network_monitoring_web/"]
RUN dotnet restore "network_monitoring_web/network_monitoring_web.csproj"
COPY . .
WORKDIR "/src/network_monitoring_web"
RUN dotnet build "network_monitoring_web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "network_monitoring_web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "network_monitoring_web.dll"]