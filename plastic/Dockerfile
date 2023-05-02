FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build

WORKDIR /app

# Install PlasticSCM CLI
RUN apt-get update && apt-get install -y --no-install-recommends curl gpg && \
    curl https://www.plasticscm.com/plasticrepo/stable/5.4.16.824/plasticscm5-client.tar.gz -o plasticscm.tar.gz && \
    curl https://www.plasticscm.com/plasticrepo/stable/5.4.16.824/plasticscm5-client.tar.gz.sig -o plasticscm.tar.gz.sig && \
    gpg --no-default-keyring --keyring gnupg-ring:/etc/apt/trusted.gpg.d/plasticscm.gpg --import /plasticscmpublickey.asc && \
    gpg --verify plasticscm.tar.gz.sig plasticscm.tar.gz && \
    tar zxvf plasticscm.tar.gz && \
    rm -rf /var/lib/apt/lists/* /plasticscmpublickey.asc

# Copy your Plastic SCM repository (optional)
COPY .plastic /app/.plastic

# Set Plastic SCM variables
ENV PATH="/app/plasticscm5-client:${PATH}"
ENV PLASTIC_HOME="/app/plasticscm5-client"
ENV PLASTIC_CONFIGDIR="/app/.plastic"

# Set up entrypoint command
COPY entrypoint.sh /app
RUN chmod +x entrypoint.sh
ENTRYPOINT ["/app/entrypoint.sh"]
