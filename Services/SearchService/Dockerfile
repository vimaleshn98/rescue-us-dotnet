# Base runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 8081

ENV ASPNETCORE_ENVIRONMENT=Development


# Build image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Services/SearchService/SearchService.csproj", "./"]
RUN dotnet restore "SearchService.csproj"

COPY . .
WORKDIR "/src/Services/SearchService"

RUN dotnet build "SearchService.csproj" -c Release -o /app/build

# Publish image
FROM build AS publish
RUN dotnet publish "SearchService.csproj" -c Release -o /app/publish

# Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SearchService.dll"]
