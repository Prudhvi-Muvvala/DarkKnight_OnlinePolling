FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["OnlineVoting/OnlineVoting.csproj", "OnlineVoting/"]
RUN dotnet restore "OnlineVoting/OnlineVoting.csproj"
COPY . .
WORKDIR "/src/OnlineVoting"
RUN dotnet build "OnlineVoting.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "OnlineVoting.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "OnlineVoting.dll"]