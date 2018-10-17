FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 16827
EXPOSE 44366

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY ["src/RPistorello.Apresentacao/RPistorello.Apresentacao.csproj", "src/RPistorello.Apresentacao/"]
RUN dotnet restore "src/RPistorello.Apresentacao/RPistorello.Apresentacao.csproj"
COPY . .
WORKDIR "/src/src/RPistorello.Apresentacao"
RUN dotnet build "RPistorello.Apresentacao.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "RPistorello.Apresentacao.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RPistorello.Apresentacao.dll"]