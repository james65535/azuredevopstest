FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY Hello-Again/Hello-Again.csproj Hello-Again/
RUN dotnet restore "Hello-Again/Hello-Again.csproj"
COPY . .
WORKDIR "/src/Hello-Again"
RUN dotnet build "Hello-Again.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Hello-Again.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Hello-Again.dll"]
