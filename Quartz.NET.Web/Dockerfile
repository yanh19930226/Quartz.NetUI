#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80
#EXPOSE 443

#FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
FROM registry.cn-hangzhou.aliyuncs.com/yoyosoft/dotnet/core/sdk AS build

WORKDIR /src
COPY ["Quartz.NET.Web.csproj", " Quartz.NET.Web/"]
RUN dotnet restore " Quartz.NET.Web/Quartz.NET.Web.csproj"
COPY . .
WORKDIR .
RUN dotnet build "Quartz.NET.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Quartz.NET.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Quartz.NET.Web.dll"]