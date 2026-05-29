<div align="center">

![GNS3](https://img.shields.io/badge/GNS3-Lab-blue?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-Networking-2496ED?style=for-the-badge)
![BGP](https://img.shields.io/badge/BGP-EVPN-orange?style=for-the-badge)

*BGP EVPN and VXLAN network simulation with Docker and GNS3*

</div>

<div align="center">
	<img src="/images/BADASS.jpg">
</div>

# BADASS

[README en Espanol](README_es.md)

`Bgp At Doors of Autonomous Systems is Simple` or `BADASS` is a network project that simulates modern datacenter infrastructure using `GNS3` and `Docker`. It implements technologies like `BGP EVPN` and `VXLAN` to understand large-scale networking through virtual routers, tunneling, and dynamic routing.

## Vagrant

```bash
vagrant up                     # Start the VM
vagrant halt                   # Stop the VM
vagrant destroy -f             # Destroy the VM
vagrant ssh                    # SSH into the VM
vagrant ssh -- -X -t gns3      # Start GNS3
```

## Part 1 (GNS3 configuration with Docker)

- Two `Docker` images are used in `GNS3`.
- `Image 1`: minimal system with `busybox`.
- `Image 2`: routing-capable system with `BGPD`, `OSPFD`, `IS-IS` and `busybox`.

## Part 2: (discovering VXLAN)

- `VXLAN` with `VNI 10` and `bridge br0`.
- Implementation in `static` and `multicast` mode.
- `MAC` learning verified on both routers without `IP` on hosts.

## Part 3: (discovering BGP with EVPN)

- `EVPN` configured over `VXLAN` with `VNI 10`.
- Route reflection enabled, `VTEP` learns `MACs` dynamically.
- `OSPF` as underlay for connectivity.

## License

This project is licensed under the WTFPL - [Do What the Fuck You Want to Public License](http://www.wtfpl.net/about/).

---

<div align="center">

**🖧 Developed as part of the 42 School curriculum 🖧**

*"BGP is just controlled chaos"*

</div>
