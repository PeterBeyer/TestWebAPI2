FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["TestWebAPI2/TestWebAPI2.csproj", "TestWebAPI2/"]
RUN dotnet restore "TestWebAPI2/TestWebAPI2.csproj"
COPY . .
WORKDIR "/src/TestWebAPI2"
RUN dotnet build "TestWebAPI2.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "TestWebAPI2.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "TestWebAPI2.dll"]