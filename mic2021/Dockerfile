#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["mic2021/mic2021.csproj", "mic2021/"]
RUN dotnet restore "mic2021/mic2021.csproj"
COPY . .
WORKDIR "/src/mic2021"
RUN dotnet build "mic2021.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "mic2021.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "mic2021.dll"]