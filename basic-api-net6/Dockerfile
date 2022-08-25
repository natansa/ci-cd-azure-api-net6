#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["basic-api-net6/basic-api-net6.csproj", "basic-api-net6/"]
RUN dotnet restore "basic-api-net6/basic-api-net6.csproj"
COPY . .
WORKDIR "/src/basic-api-net6"
RUN dotnet build "basic-api-net6.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "basic-api-net6.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "basic-api-net6.dll"]