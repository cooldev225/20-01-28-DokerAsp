FROM mcr.microsoft.com/dotnet/core/aspnet:3.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.0 AS build
WORKDIR /src
COPY ["DockerEXE1/DockerEXE1.csproj", "DockerEXE1/"]

RUN dotnet restore "DockerEXE1/DockerEXE1.csproj"
COPY . .
WORKDIR "/src/DockerEXE1"
RUN dotnet build "DockerEXE1.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockerEXE1.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockerEXE1.dll"]