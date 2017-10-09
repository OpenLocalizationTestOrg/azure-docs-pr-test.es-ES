---
title: "Guía de red de Site Recovery para la replicación de máquinas virtuales de Azure tooAzure aaaAzure | Documentos de Microsoft"
description: "Guía de redes para la replicación de máquinas virtuales de Azure"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/13/2017
ms.author: sujayt
ms.openlocfilehash: 3a3391b8c3512932d243458fd17d2a2b39248448
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="networking-guidance-for-replicating-azure-virtual-machines"></a>Guía de redes para la replicación de máquinas virtuales de Azure

>[!NOTE]
> La replicación de Site Recovery en máquinas virtuales de Azure se encuentra actualmente en versión preliminar.

Este artículo se detallan Hola guía sobre red de Azure Site Recovery durante la replicación y la recuperación de máquinas virtuales de Azure desde una región tooanother otra. Para obtener más información acerca de los requisitos de Azure Site Recovery, vea hello [requisitos previos](site-recovery-prereq.md) artículo.

## <a name="site-recovery-architecture"></a>Arquitectura de Site Recovery

Recuperación de sitio proporciona un tooreplicate de manera simple y fácil aplicaciones que se ejecutan en máquinas virtuales de Azure tooanother región de Azure para que puedan recuperar si se produce una interrupción en la región principal de Hola. Aprenda más sobre [este escenario y la arquitectura de Site Recovery](site-recovery-azure-to-azure-architecture.md).

## <a name="your-network-infrastructure"></a>La infraestructura

Hello siguiente diagrama muestra el entorno de Azure de hello típica para una aplicación que se ejecuta en máquinas virtuales de Azure:

![Entorno de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment.png)

Si utilizas Azure ExpressRoute o una conexión VPN desde un tooAzure de red local, entorno de Hola se ve así:

![Entorno de cliente](./media/site-recovery-azure-to-azure-architecture/source-environment-expressroute.png)

Normalmente, los clientes protegen sus redes mediante firewalls o grupos de seguridad de red (NSG). firewalls de Hello pueden usar la creación de listas blancas basado en la dirección URL o en IP para controlar la conectividad de red. Los NSG permiten las reglas para el uso de conectividad de red de toocontrol de intervalos IP.

>[!IMPORTANT]
> Si utilizas una conectividad de red de toocontrol proxy autenticado, no se admite y no se puede habilitar la replicación de Site Recovery. 

Hello siguientes secciones describen cambios de conectividad saliente de red Hola necesarios desde máquinas virtuales de Azure para toowork de replicación de Site Recovery.

## <a name="outbound-connectivity-for-azure-site-recovery-urls"></a>Conectividad saliente para direcciones URL de Azure Site Recovery

Si se utiliza cualquier conectividad saliente de firewall basado en la dirección URL del proxy toocontrol, ser toowhitelist seguro estos requiere direcciones URL de servicio de Azure Site Recovery:


**URL** | **Propósito**  
--- | ---
*.blob.core.windows.net | Necesario para que se pueden escribir datos toohello cuenta de almacenamiento de caché en la región de origen de Hola de hello máquina virtual.
login.microsoftonline.com | Se requiere para la autenticación y autorización de URL de servicio de Site Recovery toohello.
*.hypervrecoverymanager.windowsazure.com | Necesario para que puedan realizarse comunicación del servicio de Site Recovery Hola de hello máquina virtual.
*.servicebus.windows.net | Necesario para que se pueden escribir datos de supervisión y diagnóstico de Site Recovery Hola de hello máquina virtual.

## <a name="outbound-connectivity-for-azure-site-recovery-ip-ranges"></a>Conectividad saliente para intervalos IP de Azure Site Recovery

>[!NOTE]
> tooautomatically crear reglas del NSG Hola necesario en el grupo de seguridad de red de hello, puede [descargar y usar este script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

>[!IMPORTANT]
> * Se recomienda que cree reglas NSG de hello necesario en un grupo de seguridad de red de prueba y comprobar que no hay ningún problema antes de crear reglas de hello en un grupo de seguridad de la red de producción.
> * número de hello necesario toocreate de reglas NSG, asegúrese de que la suscripción está en la lista blanca. Póngase en contacto con soporte técnico tooincrease hello NSG regla límite en su suscripción.

Si usas cualquier proxy de servidor de seguridad basado en IP o la conectividad saliente de toocontrol de reglas NSG, hello siguientes intervalos IP necesitan toobe en la lista blanca, dependiendo de las ubicaciones de origen y destino de Hola de máquinas virtuales de hello:

- Ubicación de origen de todos los intervalos IP que corresponden toohello. (Puede descargar hello [intervalos IP](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Creación de listas blancas es necesaria para que se pueden escribir datos toohello cuenta de almacenamiento de caché de hello máquina virtual.

- Todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

    >[!NOTE]
    > Si IP nueva agréguese tooOffice 365 intervalos IP en hello futuras, deberá toocreate nuevas reglas de NSG.
    
- Las direcciones IP de punto de conexión del servicio de Site Recovery ([disponibles en un archivo XML](https://aka.ms/site-recovery-public-ips)), que dependen de la ubicación de destino: 

   **Ubicación de destino** | **Direcciones IP del servicio de Site Recovery** |  **IP de supervisión de Site Recovery**
   --- | --- | ---
   Asia oriental | 52.175.17.132</br>40.83.121.61 | 13.94.47.61
   Sudeste asiático | 52.187.58.193</br>52.187.169.104 | 13.76.179.223
   India Central | 52.172.187.37</br>52.172.157.193 | 104.211.98.185
   Sur de la India | 52.172.46.220</br>52.172.13.124 | 104.211.224.190
   Centro-Norte de EE. UU | 23.96.195.247</br>23.96.217.22 | 168.62.249.226
   Europa del Norte | 40.69.212.238</br>13.74.36.46 | 52.169.18.8
   Europa occidental | 52.166.13.64</br>52.166.6.245 | 40.68.93.145
   Este de EE. UU | 13.82.88.226</br>40.71.38.173 | 104.45.147.24
   Oeste de EE. UU | 40.83.179.48</br>13.91.45.163 | 104.40.26.199
   Centro-Sur de EE. UU | 13.84.148.14</br>13.84.172.239 | 104.210.146.250
   Central EE. UU: | 40.69.144.231</br>40.69.167.116 | 52.165.34.144
   Este de EE. UU. 2 | 52.184.158.163</br>52.225.216.31 | 40.79.44.59
   Este de Japón | 52.185.150.140</br>13.78.87.185 | 138.91.1.105
   Oeste de Japón | 52.175.146.69</br>52.175.145.200 | 138.91.17.38
   Sur de Brasil | 191.234.185.172</br>104.41.62.15 | 23.97.97.36
   Australia Oriental | 104.210.113.114</br>40.126.226.199 | 191.239.64.144
   Sudeste de Australia | 13.70.159.158</br>13.73.114.68 | 191.239.160.45
   Centro de Canadá | 52.228.36.192</br>52.228.39.52 | 40.85.226.62
   Este de Canadá | 52.229.125.98</br>52.229.126.170 | 40.86.225.142
   Centro occidental de EE.UU | 52.161.20.168</br>13.78.230.131 | 13.78.149.209
   Oeste de EE. UU 2 | 52.183.45.166</br>52.175.207.234 | 13.66.228.204
   Oeste de Reino Unido | 51.141.3.203</br>51.140.226.176 | 51.141.14.113
   Sur del Reino Unido 2 | 51.140.43.158</br>51.140.29.146 | 51.140.189.52

## <a name="sample-nsg-configuration"></a>Configuración de NSG de ejemplo
Esta sección explica las reglas de hello pasos tooconfigure NSG para que puedan funcionar replicación de Site Recovery en una máquina virtual. Si usas conectividad saliente de toocontrol de reglas NSG, usar reglas de "Permitir salientes HTTPS" para todos los intervalos IP de hello necesario.

>[!Note]
> tooautomatically crear reglas del NSG Hola necesario en el grupo de seguridad de red de hello, puede [descargar y usar este script](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).

Por ejemplo, si la ubicación de origen de la máquina virtual es "UU" y la ubicación de destino de replicación es "Central US", siga los pasos de hello en hello dos secciones siguientes.

>[!IMPORTANT]
> * Se recomienda que cree reglas NSG de hello necesario en un grupo de seguridad de red de prueba y comprobar que no hay ningún problema antes de crear reglas de hello en un grupo de seguridad de la red de producción.
> * número de hello necesario toocreate de reglas NSG, asegúrese de que la suscripción está en la lista blanca. Póngase en contacto con soporte técnico tooincrease hello NSG regla límite en su suscripción. 

### <a name="nsg-rules-on-hello-east-us-network-security-group"></a>Reglas NSG en el grupo de seguridad de red de hello este de EE.

* Crear reglas que corresponden demasiado[intervalos de direcciones IP de este de EE. UU.](https://www.microsoft.com/download/confirmation.aspx?id=41653). Esto es necesario para que se pueden escribir datos toohello cuenta de almacenamiento de caché de hello máquina virtual.

* Crear reglas para todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Crear reglas que corresponden toohello ubicación de destino:

   **Ubicación** | **Direcciones IP del servicio de Site Recovery** |  **IP de supervisión de Site Recovery**
    --- | --- | ---
   Central EE. UU.: | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

### <a name="nsg-rules-on-hello-central-us-network-security-group"></a>Reglas NSG en el grupo de seguridad de red de hello Central EE. UU.

Estas reglas son necesarias para que se puede habilitar la replicación de hello destino región toohello origen región post-conmutación por error:

* Las reglas que corresponden demasiado[intervalos de direcciones IP de EE. UU. Central](https://www.microsoft.com/download/confirmation.aspx?id=41653). Estas son necesarias para que se pueden escribir datos toohello cuenta de almacenamiento de caché de hello máquina virtual.

* Reglas para todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).

* Ubicación de origen de las reglas que corresponden toohello:

   **Ubicación** | **Direcciones IP del servicio de Site Recovery** |  **IP de supervisión de Site Recovery**
    --- | --- | ---
   Este de EE. UU. | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration"></a>Directrices para la configuración de ExpressRoute o VPN existente de Azure en el entorno local

Si tiene una conexión ExpressRoute o VPN entre hello y local del origen de ubicación de Azure, siga las instrucciones de hello en esta sección.

### <a name="forced-tunneling-configuration"></a>Configuración de la tunelización forzada

Una configuración de cliente común es toodefine una ruta predeterminada (0.0.0.0/0) que fuerza la salida tooflow de tráfico de Internet a través de la ubicación local de Hola. Esto no se recomienda. tráfico de replicación de Hola y comunicación del servicio de recuperación de sitio no deben dejar Hola límite de Azure. Hola solución es tooadd rutas definidas por el usuario (UDRs) para [estos intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges) para que el tráfico de replicación hello no entren en local.

### <a name="connectivity-between-hello-target-and-on-premises-location"></a>Conectividad entre la ubicación de destino y local de Hola

Siga estas directrices para las conexiones entre la ubicación de destino de Hola y ubicación local de Hola:
- Si la aplicación necesita máquinas locales de tooconnect toohello o si hay clientes que se conectan toohello aplicación desde local a través de VPN/ExpressRoute, asegúrese de que tiene al menos un [conexión de sitio a sitio](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) entre el centro de datos de destino Azure hello y región local.

- Si espera mucho tráfico tooflow entre la región de Azure de destino y el centro de datos de hello en local, debe crear otra [conexión ExpressRoute](../expressroute/expressroute-introduction.md) entre el centro de datos de hello Azure hello y región local de destino.

- Si desea tooretain direcciones IP para las máquinas virtuales de hello después de que una conmutación por error, tenga conexión de sitio a sitio o ExpressRoute de la región de destino de hello en estado desconectado. Se trata de toomake que no haya ningún conflicto de intervalo entre los intervalos IP de la región de origen de hello e intervalos IP de la región de destino.

### <a name="best-practices-for-expressroute-configuration"></a>Procedimientos recomendados para la configuración de ExpressRoute
Siga estos procedimientos recomendados para la configuración de ExpressRoute:

- Deberá toocreate un circuito ExpressRoute en ambas regiones de origen y de destino de Hola. A continuación, debe toocreate una conexión entre:
  - red virtual de origen de Hola y el circuito de ExpressRoute Hola.
  - red virtual de destino de Hola y el circuito de ExpressRoute Hola.

- Como parte del estándar de ExpressRoute, puede crear circuitos en hello misma región geopolíticos. circuitos ExpressRoute de toocreate en distintas regiones geopolíticas, Azure ExpressRoute Premium es necesario, lo que implica un costo incremental. (Si ya usa ExpressRoute Premium, no existen costos adicionales). Para obtener más información, vea hello [documento de ubicaciones de ExpressRoute](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) y [ExpressRoute precios](https://azure.microsoft.com/pricing/details/expressroute/).

- Se recomienda usar diferentes intervalos IP en las regiones de origen y destino. Hola circuito de ExpressRoute no podrá tooconnect con dos redes virtuales de Azure de hello misma IP de intervalos en hello mismo tiempo.

- Puede crear redes virtuales con hello misma IP está comprendido en ambas regiones y, a continuación, crear circuitos ExpressRoute en ambas regiones. En caso de hello de un evento de conmutación por error, desconectarse circuito Hola de red virtual de origen de Hola y conectar el circuito de hello en la red virtual de destino de Hola.

 >[!IMPORTANT]
 > Si la región principal de hello es completamente hacia abajo, la operación de desconexión Hola puede producir un error. Que impedirán red virtual de destino de hello conectividad de ExpressRoute.

## <a name="next-steps"></a>Pasos siguientes
Comience a proteger las cargas de trabajo mediante la [replicación de máquinas virtuales de Azure](site-recovery-azure-to-azure.md).
