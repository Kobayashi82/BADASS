FROM alpine:3.17

# Install FRR and required tools
RUN apk add --no-cache \
    frr \
    busybox-extras \
    iputils \
    iproute2

# Create required runtime directory
RUN mkdir -p /run/frr && chown frr:frr /run/frr

# Enable required daemons
RUN sed -i \
    -e 's/bgpd=no/bgpd=yes/' \
    -e 's/ospfd=no/ospfd=yes/' \
    -e 's/isisd=no/isisd=yes/' \
    /etc/frr/daemons

# Create startup script
RUN cat > /start.sh << 'EOF'
#!/bin/sh

# Start FRR daemons in background
/usr/lib/frr/watchfrr zebra bgpd ospfd isisd &

# Keep container alive so GNS3 can manage the console
tail -f /dev/null
EOF
RUN chmod +x /start.sh

CMD ["/start.sh"]
