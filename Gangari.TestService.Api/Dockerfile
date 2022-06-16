FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["Gangari.TestService.Api/Gangari.TestService.Api.csproj", "Gangari.TestService/"]
RUN dotnet restore "Gangari.TestService/Gangari.TestService.csproj"
COPY . .
WORKDIR "/src/Gangari.TestService"
RUN dotnet build "Gangari.TestService.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Gangari.TestService.Api.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Gangari.TestService.Api.dll"]
