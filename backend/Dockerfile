# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /app

# Copy the csproj files and restore dependencies
COPY FooBooLooGameAPI/*.csproj FooBooLooGameAPI/
RUN dotnet restore FooBooLooGameAPI/FooBooLooGameAPI.csproj

# Copy the remaining source code and build the application
COPY . .
RUN dotnet publish FooBooLooGameAPI/FooBooLooGameAPI.csproj -c Release -o /app/out

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app
COPY --from=build /app/out .

# Expose the port your application is running on
EXPOSE 8080

# Run database migrations before starting the application
CMD ["dotnet", "FooBooLooGameAPI.dll", "ef", "database", "update"]
ENTRYPOINT ["dotnet", "FooBooLooGameAPI.dll"]
