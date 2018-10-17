FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 17093
EXPOSE 44356

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/RPistorello.WebAPI/RPistorello.WebAPI.csproj", "src/RPistorello.WebAPI/"]
RUN dotnet restore "src/RPistorello.WebAPI/RPistorello.WebAPI.csproj"
COPY . .
WORKDIR "/src/src/RPistorello.WebAPI"
RUN dotnet build "RPistorello.WebAPI.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "RPistorello.WebAPI.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RPistorello.WebAPI.dll"]