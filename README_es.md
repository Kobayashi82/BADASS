<div align="center">

![GNS3](https://img.shields.io/badge/GNS3-Lab-blue?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-Networking-2496ED?style=for-the-badge)
![BGP](https://img.shields.io/badge/BGP-EVPN-orange?style=for-the-badge)

*Simulación de red BGP EVPN y VXLAN con Docker y GNS3*

</div>

<div align="center">
	<img src="/images/BADASS.jpg">
</div>

# BADASS

[README in English](README.md)

`Bgp At Doors of Autonomous Systems is Simple` o `BADASS` es un proyecto de redes que simula infraestructuras de datacenter modernas usando `GNS3` y `Docker`. Implementa tecnologías como `BGP EVPN` y `VXLAN` para entender cómo funcionan las redes a gran escala mediante routers virtuales, túneles y enrutamiento dinámico.

## Vagrant

```bash
vagrant up						# Iniciar la VM
vagrant halt					# Apagar la VM
vagrant destroy -f				# Destruir la VM
vagrant ssh						# Entrar por SSH
vagrant ssh -- -X -t gns3		# Iniciar GNS3
```

## Parte 1 (Configuracion de GNS3 con Docker)

- Se usan dos imagenes `Docker` en `GNS3`.
- `Imagen 1`: sistema minimo con `busybox`.
- `Imagen 2`: sistema con enrutamiento y servicios `BGPD`, `OSPFD`,`IS-IS` y `busybox`.

## Parte 2: (descubriendo VXLAN)

- `VXLAN` con `VNI 10` y `bridge br0`.
- Implementacion en modo `estatico` y en `multicast`.
- Aprendizaje de `MAC` verificado en ambos routers sin `IP` en los hosts.

## Parte 3: (descubriendo BGP con EVPN)

- `EVPN` configurado sobre `VXLAN` con `VNI 10`.
- Route reflection activo, los `VTEP` aprenden `MACs` de forma dinamica.
- `OSPF` como underlay para conectividad.

## Licencia

Este proyecto esta licenciado bajo WTFPL - [Do What the Fuck You Want to Public License](http://www.wtfpl.net/about/).

---

<div align="center">

**🖧 Desarrollado como parte del curriculum de 42 🖧**

*"BGP is just controlled chaos"*

</div>
