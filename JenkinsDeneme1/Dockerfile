FROM mcr.microsoft.com/dotnet/runtime:9.0 AS base
USER $APP_UID
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build
ARG BUILD_CONFIGURATION=Release
WORKDIR /src
COPY ["JenkinsDeneme1/JenkinsDeneme1.csproj", "JenkinsDeneme1/"]
RUN dotnet restore "JenkinsDeneme1/JenkinsDeneme1.csproj"
COPY . .
WORKDIR "/src/JenkinsDeneme1"
RUN dotnet build "JenkinsDeneme1.csproj" -c $BUILD_CONFIGURATION -o /app/build

FROM build AS publish
ARG BUILD_CONFIGURATION=Release
RUN dotnet publish "JenkinsDeneme1.csproj" -c $BUILD_CONFIGURATION -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "JenkinsDeneme1.dll"]
