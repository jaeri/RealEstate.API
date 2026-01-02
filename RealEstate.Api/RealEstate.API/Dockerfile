# Build stage
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy only the project file first for caching
COPY RealEstate.API/*.csproj ./RealEstate.API/
WORKDIR /src/RealEstate.API
RUN dotnet restore

# Copy everything else
COPY RealEstate.API/. .
RUN dotnet publish -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "RealEstate.API.dll"]
