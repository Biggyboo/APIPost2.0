FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY ["APIPost2.0/APIPost2.0.csproj", "APIPost2.0/"]
RUN dotnet restore "APIPost2.0/APIPost2.0.csproj"
COPY . .
WORKDIR "/src/APIPost2.0"
RUN dotnet build "APIPost2.0.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "APIPost2.0.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "APIPost2.0.dll"]