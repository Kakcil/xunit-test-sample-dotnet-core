#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-bionic AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-bionic AS build
WORKDIR /src
COPY ["sample-service/sample-service.csproj", "sample-service/"]
RUN dotnet restore "sample-service/sample-service.csproj"
COPY . .
WORKDIR "/src/sample-service"
RUN dotnet build "sample-service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "sample-service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "sample-service.dll"]
