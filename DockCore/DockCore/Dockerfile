FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["DockCore/DockCore.csproj", "DockCore/"]
RUN dotnet restore "DockCore/DockCore.csproj"
COPY . .
WORKDIR "/src/DockCore"
RUN dotnet build "DockCore.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "DockCore.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DockCore.dll"]