#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["R2D2Test.csproj", "."]
RUN dotnet restore "./R2D2Test.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "R2D2Test.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "R2D2Test.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "R2D2Test.dll"]