# Stage 1 - Build Stage
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS builder

ARG TARGETARCH
WORKDIR /src
    
COPY cartservice.csproj ./
RUN dotnet restore cartservice.csproj \ 
    -a $TARGETARCH
   
COPY . .
RUN dotnet publish cartservice.csproj \
    -p:PublishSingleFile=true \
    -a $TARGETARCH \
    --self-contained true \
    -p:PublishTrimmed=true \
    -p:TrimMode=full \
    -c Release \
    -o /cartservice
    
# Stage 2 - Runtime Stage
FROM mcr.microsoft.com/dotnet/runtime-deps:9.0-chiseled
    
WORKDIR /app
COPY --from=builder /cartservice .
    
EXPOSE 7070
    
ENV DOTNET_EnableDiagnostics=0 \
    ASPNETCORE_HTTP_PORTS=7070
    
USER 1000
ENTRYPOINT ["/app/cartservice"]
    