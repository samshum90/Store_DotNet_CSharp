FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build-env
WORKDIR /app

# FROM mcr.microsoft.com/dotnet/sdk:5.0
# COPY bin/Release/net5.0/ App/
# WORKDIR /App
# ENTRYPOINT ["dotnet", "aspnetapp.dll"]

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# # Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

FROM mcr.microsoft.com/dotnet/sdk:5.0
WORKDIR /App
COPY --from=build-env /app/out .
EXPOSE 5000/tcp
ENV ASPNETCORE_URLS http://*:5000
# ENTRYPOINT ["dotnet", "API.dll", "--urls", "http://*:5000;http://*:5001"]
ENTRYPOINT ["dotnet", "API.dll"]
