#See https://aka.ms/customizecontainer to learn how to customize your debug container and how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 8005
EXPOSE 8005
ENV SimpleProperty="hello-from-BASE-dockerfile"

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["LearnSmartCoding.API/LearnSmartCoding.API.csproj", "LearnSmartCoding.API/"]
RUN dotnet restore "LearnSmartCoding.API/LearnSmartCoding.API.csproj"
COPY . .
WORKDIR "/src/LearnSmartCoding.API"
RUN dotnet build "LearnSmartCoding.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "LearnSmartCoding.API.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENV SimpleProperty="hello-from-FINAL-dockerfile"
ENTRYPOINT ["dotnet", "LearnSmartCoding.API.dll"]
