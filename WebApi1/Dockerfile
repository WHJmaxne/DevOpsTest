FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["WebApi1/WebApi1.csproj", "WebApi1/"]
RUN dotnet restore "WebApi1/WebApi1.csproj"
COPY . .
WORKDIR "/src/WebApi1"
RUN dotnet build "WebApi1.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "WebApi1.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "WebApi1.dll"]