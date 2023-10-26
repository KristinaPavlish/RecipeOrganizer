FROM mcr.microsoft.com/dotnet/runtime:6.0 AS base
WORKDIR /app

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["RecipeOrganizer.ConsoleApp/RecipeOrganizer.ConsoleApp.csproj", "RecipeOrganizer.ConsoleApp/"]
RUN dotnet restore "RecipeOrganizer.ConsoleApp/RecipeOrganizer.ConsoleApp.csproj"
COPY . .
WORKDIR "/src/RecipeOrganizer.ConsoleApp"
RUN dotnet build "RecipeOrganizer.ConsoleApp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "RecipeOrganizer.ConsoleApp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "RecipeOrganizer.ConsoleApp.dll"]
