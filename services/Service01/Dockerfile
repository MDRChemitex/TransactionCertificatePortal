# Build stage
FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src/Service01

COPY src/Service01/*.csproj .
RUN dotnet restore

COPY src/Service01/. .
RUN dotnet publish -c Release -o /app --no-restore

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0

WORKDIR /app

ENV ASPNETCORE_URLS=http://+:80

COPY --from=build /app ./

EXPOSE 80

ENTRYPOINT ["dotnet", "Service01.dll"]