FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base

WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

WORKDIR /src
COPY ["orchardcorecms/orchardcorecms.csproj", "orchardcorecms/"]
RUN dotnet restore "orchardcorecms/orchardcorecms.csproj"

COPY . .
WORKDIR "/src/orchardcorecms"
RUN dotnet build "orchardcorecms.csproj" -c Release -o /app/build

FROM build AS publish


RUN dotnet publish "orchardcorecms.csproj" -c Release  -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "orchardcorecms.dll"]
