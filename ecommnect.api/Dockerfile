FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["ecommnect.api/ecommnect.api.csproj", "ecommnect.api/"]
RUN dotnet restore "ecommnect.api/ecommnect.api.csproj"
COPY . .
WORKDIR "/src/ecommnect.api"
RUN dotnet build "ecommnect.api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ecommnect.api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ecommnect.api.dll"]
