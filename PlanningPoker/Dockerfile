FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["PlanningPoker/PlanningPoker.csproj", "PlanningPoker/"]
RUN dotnet restore "PlanningPoker/PlanningPoker.csproj"
COPY . .
WORKDIR "/src/PlanningPoker"
RUN dotnet build "PlanningPoker.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "PlanningPoker.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PlanningPoker.dll"]