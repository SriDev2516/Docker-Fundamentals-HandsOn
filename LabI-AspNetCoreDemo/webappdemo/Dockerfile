FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 5298
EXPOSE 4040

ENV ASPNETCORE_URLS=http://+:5298

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["webappdemo.csproj", "./"]
RUN dotnet restore "webappdemo.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "webappdemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "webappdemo.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "webappdemo.dll"]
