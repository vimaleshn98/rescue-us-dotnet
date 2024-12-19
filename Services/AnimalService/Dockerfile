# Base runtime image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 8080

ENV ASPNETCORE_ENVIRONMENT=Development


# Build image
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["Services/AnimalService/AnimalService.csproj", "./"]
RUN dotnet restore "AnimalService.csproj"

# Copy the rest of the project files
COPY . .
WORKDIR "/src/Services/AnimalService"

# Build the project
RUN dotnet build "AnimalService.csproj" -c Release -o /app/build

# Publish image
FROM build AS publish
RUN dotnet publish "AnimalService.csproj" -c Release -o /app/publish

# Final runtime image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "AnimalService.dll"]
