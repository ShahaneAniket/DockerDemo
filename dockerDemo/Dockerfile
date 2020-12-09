FROM microsoft/dotnet:3.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet/core/sdk:3.1 AS base
WORKDIR /src 
COPY ["dockerDemo/dockerDemo.csproj", "dockerDemo/dockerDemo/"]
RUN dotnet restore "dockerDemo/dockerDemo.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "dockerDemo/dockerDemo.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "dockerDemo/dockerDemo.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "dockerDemo.dll"]