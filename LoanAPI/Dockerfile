FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["LoanAPI.csproj", ""]
RUN dotnet restore "./LoanAPI.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "LoanAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "LoanAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LoanAPI.dll"]