#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
#COPY ["Maths-Service/Maths-Service.csproj", "Maths-Service/"]
COPY . Maths-Service/
RUN dotnet restore "Maths-Service/Maths-Service.csproj"
COPY . .
WORKDIR "/src/Maths-Service"
RUN ls
RUN dotnet build "Maths-Service.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Maths-Service.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
#ENTRYPOINT ["dotnet", "Maths-Service.dll"]
CMD ASPNETCORE_URLS=http://*:$PORT dotnet Maths-Service.dll