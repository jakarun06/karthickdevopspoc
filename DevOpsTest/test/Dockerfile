FROM microsoft/dotnet:2.1-aspnetcore-runtime-nanoserver-sac2016 AS base
WORKDIR /app
EXPOSE 44317

FROM microsoft/dotnet:2.1-sdk-nanoserver-sac2016 AS build
WORKDIR /src
COPY test.csproj .
RUN dotnet restore "test.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "test.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "test.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "test.dll"]