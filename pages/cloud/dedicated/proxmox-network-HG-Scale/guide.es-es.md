---
title: 'Configurar la red en Proxmox VE en las gamas High Grade & SCALE'
slug: proxmox-network-hg-scale
excerpt: 'Cómo configurar la red en Proxmox VE en las gamas High Grade & SCALE'
section: 'Uso avanzado'
order: 5
---

> [!primary]
> Esta traducción ha sido generada de forma automática por nuestro partner SYSTRAN. En algunos casos puede contener términos imprecisos, como en las etiquetas de los botones o los detalles técnicos. En caso de duda, le recomendamos que consulte la versión inglesa o francesa de la guía. Si quiere ayudarnos a mejorar esta traducción, por favor, utilice el botón «Contribuir» de esta página.
> 

**Última actualización: 04/10/2021**

## Objetivo

En las gamas High Grade & SCALE, no es posible el funcionamiento de las IP failover en modo bridged (a través de MAC Virtuales). Por lo tanto, es necesario configurar las IP failover en modo enrutado o a través del vRack.

**Esta guía explica cómo configurar la red en Proxmox VE.**

## Requisitos

- Tener un [servidor dedicado de OVHcloud](https://www.ovhcloud.com/es-es/bare-metal/).
- Disponer de [IP Failover](https://www.ovhcloud.com/es-es/bare-metal/ip/).
- Tienes acceso a tu [Panel de configuración de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.es/&ovhSubsidiary=es).

> [!warning]
>
> No debe aplicarse ninguna MAC virtual a las IP failover en el panel de configuración de OVHcloud.
>

## Procedimiento

> [!primary]
>
> En estas gamas de servidores, hay 4 tarjetas de red. Las dos primeras para el público, las dos últimas para el privado. Para disfrutar del conjunto del ancho de banda, es necesario crear agregados.
>

### IP Failover en modo enrutado en las interfaces de red públicas - Proxmox V6 y anteriores.

#### Esquema de la configuración de destino

![schema route](images/schema_route2022.png){.thumbnail}

#### Explicaciones

Es necesario:

* crear un agregado;
* crear un bridge;
* autorizar el forwarding y añadir las rutas.

#### Configurar el hipervisor

Todo está en el archivo `/etc/network/interfaces` :

```bash
vi /etc/network/interfaces
```

```bash
auto lo
iface lo inet loopback

# public interface 1
auto ens33f0
iface ens33f0 inet manual

# public interface 2
auto ens33f1
iface ens33f1 inet manual

# private interface 1
auto ens35f0
iface ens35f0 inet manual

# private interface 2
auto ens35f1
iface ens35f1 inet manual

auto bond0
# LACP aggregate on public interfaces
# configured in DHCP mode on this example
# Has the server's public IP
iface bond0 inet dhcp
	bond-slaves ens33f0 ens33f1
        bond-miimon 100
	bond-mode 802.3ad
        post-up echo 1 > /proc/sys/net/ipv4/conf/bond0/proxy_arp
        post-up echo 1 > /proc/sys/net/ipv4/ip_forward

#Private

auto vmbr0
# Configure the bridge with a private address and add route(s) to send the failover IPs to it
# A.B.C.D/X => Subnet of failover IPs assigned to the server, this can be a host with /32
iface vmbr0 inet static
	address 192.168.0.1
        netmask 255.255.255.255
	bridge-ports none
	bridge-stp off
	bridge-fd 0
        post-up ip route add A.B.C.D/X dev vmbr0
```

En este punto, reinicie los servicios de red o reinicie el servidor.

#### Ejemplo de configuración VM Cliente Debian

Contenido del archivo `/etc/network/interfaces`:

```bash
auto lo ens18
iface lo inet loopback
iface ens18 inet static
    address IP_FO
    netmask 255.255.255.255
    gateway 192.168.0.1
```

### IP failover a través del vRack

#### Requisitos

* Tener un bloque público de direcciones IP reservado en su cuenta, con un mínimo de cuatro direcciones.
* Haber elegido un rango de direcciones IP privadas.
* Tener un [servidor compatible con el vRack](https://www.ovhcloud.com/es-es/bare-metal/){.external}.
* Haber activado un servicio [vRack](https://www.ovh.es/soluciones/vrack/){.external}.
* Tienes acceso a tu [Panel de configuración de OVHcloud](https://www.ovh.com/auth/?action=gotomanager&from=https://www.ovh.es/&ovhSubsidiary=es).

#### Esquema de la configuración de destino

![schema vrack](images/schema_vrack2022.png){.thumbnail}

#### Explicaciones

Debe:

* crear un agregado;
* crear un puente con el agregado;

#### Configurar una dirección IP útil

En el caso del vRack, la primera, la penúltima y la última direcciones de un bloque de IP siempre están reservadas a la dirección de red, la puerta de enlace y el *broadcast* de la red, respectivamente. Eso significa que la primera dirección útil es la segunda dirección del bloque, tal y como se muestra a continuación:

```sh
46.105.135.96 # Reserved: network address
46.105.135.97 # First usable IP
46.105.135.98
46.105.135.99
46.105.135.100
46.105.135.101
46.105.135.102
46.105.135.103
46.105.135.104
46.105.135.105
46.105.135.106
46.105.135.107
46.105.135.108
46.105.135.109 # Last usable IP
46.105.135.110 # Reserved: network gateway
46.105.135.111 # Reserved: network broadcast
```

Para configurar la primera dirección IP útil, edite el archivo de configuración de red como se indica a continuación. En este ejemplo, se utiliza la máscara de subred **255.255.255.240**.

> [!primary]
>
> La mascara de subred utilizada en el ejemplo es apropiada para nuestro bloque de IP. Su máscara de subred puede ser diferente en función del tamaño del bloque. Al contratar su bloque de IP, recibirá un mensaje de correo electrónico con la máscara de subred que debe utilizar.
>

#### Configurar el hipervisor

Todo está en el archivo `/etc/network/interfaces` :

```bash
vi /etc/network/interfaces
```

Lo que importa aquí es la configuración `bond1` y `vmbr1`:

```bash
auto lo
iface lo inet loopback

# public interface 1
auto ens33f0
iface ens33f0 inet manual

# public interface 2
auto ens33f1
iface ens33f1 inet manual

# private interface 1
auto ens35f0
iface ens35f0 inet manual

# private interface 2
auto ens35f1
iface ens35f1 inet manual

auto bond0
iface bond0 inet dhcp
	bond-slaves ens33f0 ens33f1
        bond-miimon 100
	bond-mode 802.3ad
        post-up echo 1 > /proc/sys/net/ipv4/conf/bond0/proxy_arp
        post-up echo 1 > /proc/sys/net/ipv4/ip_forward

auto bond1
# LACP Aggregate on private interfaces
# No IPs on it
iface bond1 inet manual
	bond-slaves ens35f0 ens35f1
        bond-miimon 100
	bond-mode 802.3ad


#Private

auto vmbr1
# Bridge connected to bond1 aggregate
# No need for IP
iface vmbr1 inet manual
	bridge-ports bond1
	bridge-stp off
	bridge-fd 0

```

En este punto, reinicie los servicios de red o reinicie el servidor.

#### Ejemplo de configuración VM Cliente Debian

Contenido del archivo `/etc/network/interfaces`:

```bash
auto lo ens18
iface lo inet loopback
iface ens18 inet static
    address 46.105.135.97
    netmask 255.255.255.240
    gateway 46.105.135.110
```

## Más información

Interactúe con nuestra comunidad de usuarios en <https://community.ovh.com>
