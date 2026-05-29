FROM frrouting/frr:v8.4.0

# Instalar herramientas de red obligatorias que exige el proyecto y GNS3
RUN apk add --no-cache \
    busybox-extras \
    iputils \
    iproute2

# Activar los demonios requeridos por el enunciado (bgpd, ospfd, isisd)
RUN sed -i \
    -e 's/bgpd=no/bgpd=yes/' \
    -e 's/ospfd=no/ospfd=yes/' \
    -e 's/isisd=no/isisd=yes/' \
    /etc/frr/daemons
