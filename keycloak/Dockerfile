# Use the latest Keycloak image from quay.io as the base image
FROM quay.io/keycloak/keycloak:latest

# Switch to root user to perform operations that require elevated privileges
USER root

# Copy the SSL certificate and key from the local certs folder into the image
COPY certs/keycloak.crt /etc/x509/https/tls.crt
COPY certs/keycloak.key /etc/x509/https/tls.key

# Change ownership and set proper permissions on the key file for security
RUN chown keycloak:root /etc/x509/https/tls.key && chmod 600 /etc/x509/https/tls.key

# Switch back to the Keycloak user for normal operations
USER keycloak

# Set environment variables for Keycloak admin credentials
ENV KEYCLOAK_ADMIN=admin
ENV KEYCLOAK_ADMIN_PASSWORD=admin

# Define the container's entrypoint to start Keycloak with HTTPS enabled and custom settings
ENTRYPOINT ["/opt/keycloak/bin/kc.sh", "start", "--hostname=keycloak", "--https-certificate-file=/etc/x509/https/tls.crt", "--https-certificate-key-file=/etc/x509/https/tls.key", "--hostname-strict=false", "--https-port=8443"]
