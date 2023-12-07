FROM mcr.microsoft.com/dotnet/runtime:8.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["SayHello/SayHello.csproj", "SayHello/"]
RUN dotnet restore "SayHello/SayHello.csproj"
COPY . .
WORKDIR "/src/SayHello"
RUN dotnet build "SayHello.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SayHello.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SayHello.dll"]
