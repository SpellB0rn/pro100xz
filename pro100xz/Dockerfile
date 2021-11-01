FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["pro100xz/pro100xz.csproj", "pro100xz/"]

RUN dotnet restore "pro100xz/pro100xz.csproj"
COPY . .
WORKDIR "/src/pro100xz"
RUN dotnet build "pro100xz.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "pro100xz.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "pro100xz.dll"]