# Use the official .NET 9 SDK image to build the application
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS build-env
WORKDIR /app

# Copy the project files and restore any dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the remaining source code and build the application
COPY . ./
RUN dotnet publish -c Release -o out

# Use the official .NET 9 ASP.NET Core runtime image for the final stage
FROM mcr.microsoft.com/dotnet/aspnet:9.0
WORKDIR /app
COPY --from=build-env /app/out .

# Set the environment to Development
ENV ASPNETCORE_ENVIRONMENT=Development

# Expose port 5000
EXPOSE 5000

# Set the entry point for the container
ENTRYPOINT ["dotnet", "MyDotNetApp.dll"]