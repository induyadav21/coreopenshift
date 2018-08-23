FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY coreopenshift/coreopenshift.csproj coreopenshift/
RUN dotnet restore coreopenshift/coreopenshift.csproj
COPY . .
WORKDIR /src/coreopenshift
RUN dotnet build coreopenshift.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish coreopenshift.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "coreopenshift.dll"]
