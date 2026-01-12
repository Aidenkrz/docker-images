FROM        --platform=$TARGETOS/$TARGETARCH ubuntu:jammy

LABEL       author="Durk" maintainer="administrator@goobstation.com"
LABEL       org.opencontainers.image.source="https://github.com/aidenkrz/docker-images"
LABEL       org.opencontainers.image.licenses=MIT
LABEL       org.opencontainers.image.description="Pterodactyl installer image with .NET SDK support"

ENV         DEBIAN_FRONTEND=noninteractive

RUN         apt update \
            && apt upgrade -y \
            && apt -y --no-install-recommends install \
                ca-certificates \
                curl \
                wget \
                git \
                unzip \
                zip \
                tar \
                jq \
                apt-transport-https \
                iproute2 \
                libgdiplus \
                libicu70 \
                tini \
            && apt clean \
            && rm -rf /var/lib/apt/lists/*

RUN         wget https://dot.net/v1/dotnet-install.sh \
            && D_V="$(curl -sSL https://dotnet.microsoft.com/en-us/download/dotnet/10.0 | grep -i  '<h3 id="sdk-10.*">SDK 10.*.*</h3>'  | head -1 | awk -F\" '{print $3}' | awk '{print $2;}' | sed 's/<\/h3>//g')" \
            && chmod +x dotnet-install.sh \
            && ./dotnet-install.sh -i /usr/share -v $D_V \
            && ln -s /usr/share/dotnet /usr/bin/dotnet \
            && rm dotnet-install.sh
