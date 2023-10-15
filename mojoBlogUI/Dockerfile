FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["mojoBlogUI/mojoBlogUI.csproj", "mojoBlogUI/"]
RUN dotnet restore "mojoBlogUI/mojoBlogUI.csproj"
COPY . .
WORKDIR "/src/mojoBlogUI"
RUN dotnet build "mojoBlogUI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "mojoBlogUI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "mojoBlogUI.dll"]
