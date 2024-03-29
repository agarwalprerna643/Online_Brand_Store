#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 81

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Auth API/Auth API.csproj", "Auth API/"]
COPY ["AuthRepositories/AuthRepositories.csproj", "AuthRepositories/"]
COPY ["AuthInterfaces/AuthInterfaces.csproj", "AuthInterfaces/"]
COPY ["AuthModels/AuthModels.csproj", "AuthModels/"]
COPY ["AuthServices/AuthServices.csproj", "AuthServices/"]
COPY ["AuthExceptions/AuthExceptions.csproj", "AuthExceptions/"]
RUN dotnet restore "Auth API/Auth API.csproj"
COPY . .
WORKDIR "/src/Auth API"
RUN dotnet build "Auth API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Auth API.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Auth API.dll"]