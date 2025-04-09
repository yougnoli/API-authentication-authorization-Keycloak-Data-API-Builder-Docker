# Use the Data API Builder image as the base image
FROM mcr.microsoft.com/azure-databases/data-api-builder:latest

# Switch to root user to perform system updates and install dependencies
USER root

# Update the system and install CA certificates, then clean up to reduce image size
RUN tdnf -y update && tdnf -y install ca-certificates && tdnf clean all

# Copy the Keycloak certificate into the trusted certificates directory for the system
COPY keycloak.crt /etc/pki/ca-trust/source/anchors/keycloak.crt

# Update the CA trust store to include the newly added certificate
RUN update-ca-trust extract
