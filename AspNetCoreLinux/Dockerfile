FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 11400
EXPOSE 44321

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY AspNetCoreLinux/AspNetCoreLinux.csproj AspNetCoreLinux/
RUN dotnet restore AspNetCoreLinux/AspNetCoreLinux.csproj
COPY . .
WORKDIR /src/AspNetCoreLinux
RUN dotnet build AspNetCoreLinux.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish AspNetCoreLinux.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AspNetCoreLinux.dll"]
