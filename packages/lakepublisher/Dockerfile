# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:9.0 AS builder

WORKDIR /app

# Copia file di progetto
COPY *.csproj ./

# Restore delle dipendenze
RUN dotnet restore

# Copia tutto il codice
COPY . .

# Build dell'applicazione
RUN dotnet publish -c Release -o out

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/runtime:9.0

WORKDIR /app

# Copia i binari compilati
COPY --from=builder /app/out .

# Crea directory per output
RUN mkdir -p data

# Comando di avvio
ENTRYPOINT ["dotnet", "lakepublisher.dll"]