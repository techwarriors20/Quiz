FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["Reflect.Api/Reflect.Api.csproj", "Reflect.Api/"]

RUN dotnet restore "Reflect.Api/Reflect.Api.csproj"
COPY . .
WORKDIR "/src/Reflect.Api"
RUN dotnet build "Reflect.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Reflect.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Reflect.Api.dll"]