---
title: "aaaPlan de red para la replicación de tooAzure de VMware con Site Recovery | Documentos de Microsoft"
description: "Este artículo describe el planeamiento de las redes necesarias al replicar máquinas virtuales de Azure con Azure Site Recovery"
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
ms.date: 08/01/2017
ms.author: sujayt
ms.openlocfilehash: e4036351ca707bd4966cf2a855d4a162f88153e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-networking-for-azure-vm-replication"></a>Paso 3: Plan sobre las redes para la replicación de máquinas virtuales de Azure

Una vez comprobado hello [requisitos previos de implementación](azure-to-azure-walkthrough-prerequisites.md), leer este Hola de toounderstand artículo redes consideraciones al replicar y recuperación de máquinas virtuales de Azure (VM) de una región de Azure tooanother, utilizando Hola Servicio de Azure Site Recovery. 

- Cuando termine de artículo hello, debe tener una clara comprensión de cómo tooset una salida de acceso para las máquinas virtuales de Azure desee tooreplicate y cómo tooconnect de sus instalaciones de sitio toothose las máquinas virtuales.
- Registrar los comentarios de la parte inferior de Hola de este artículo, o formular alguna pregunta en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
> La replicación de máquinas virtuales de Azure con Site Recovery está actualmente en versión preliminar.



## <a name="network-overview"></a>Información general sobre redes

Normalmente se encuentran las máquinas virtuales de Azure en una red/subred Azure virtual, y no hay una conexión desde su tooAzure de sitio local con Azure ExpressRoute o una conexión VPN.

Normalmente, los clientes protegen sus redes mediante firewalls o grupos de seguridad de red (NSG). Firewalls pueden usar basados en direcciones URL en las listas basadas en IP, conectividad de red toocontrol. NSG usan reglas basadas en intervalos IP. 


Para toowork de Site Recovery espera, deberá toomake algunos cambios en la conectividad de red saliente, desde máquinas virtuales que desea tooreplicate. Recuperación de sitio no admite el uso de una conectividad de red toocontrol de autenticación proxy. Si tiene un servidor proxy de autenticación, no se puede habilitar la replicación. 


Hello siguiente diagrama muestra un entorno típico de una aplicación que se ejecutan en máquinas virtuales de Azure.

![Entorno de cliente](./media/azure-to-azure-walkthrough-network/source-environment.png)

**Entorno de máquina virtual de Azure**

También tendrá una conexión tooAzure configurar desde el sitio local, mediante una conexión VPN o ExpressRoute de Azure. 

![Entorno de cliente](./media/azure-to-azure-walkthrough-network/source-environment-expressroute.png)

**TooAzure de conexión local**



## <a name="outbound-connectivity-for-urls"></a>Conectividad de salida para las direcciones URL

Si utilizas un firewall basado en la dirección URL del proxy toocontrol salientes la conectividad, asegúrese de que permite que estas direcciones URL usadas por Site Recovery

**URL** | **Detalles**  
--- | ---
*.blob.core.windows.net | Permite toobe datos escrito de Hola de máquina virtual, cuenta de almacenamiento de caché toohello en la región de origen de Hola.
login.microsoftonline.com | Proporciona autenticación y autorización tooSite direcciones URL del servicio de recuperación.
*.hypervrecoverymanager.windowsazure.com | Permite la comunicación con hello servicio Site Recovery de hello máquina virtual.
*.servicebus.windows.net | Necesario para que se pueden escribir datos de supervisión y diagnóstico de Site Recovery Hola de hello máquina virtual.

## <a name="outbound-connectivity-for-ip-address-ranges"></a>Conectividad de salida para rangos de direcciones IP

- Automáticamente puede crear reglas de hello necesario en hello NSG descargue ni ejecute [esta secuencia de comandos](https://gallery.technet.microsoft.com/Azure-Recovery-script-to-0c950702).
- Se recomienda que cree reglas NSG de Hola necesario en una prueba de NSG y comprobar que no hay ningún problema, antes de crear reglas de hello en un NSG de producción.
- número de hello necesario toocreate de reglas NSG, asegúrese de que la suscripción está en la lista blanca. Póngase en contacto con soporte técnico tooincrease hello NSG regla límite en su suscripción.
Si usas cualquier proxy de servidor de seguridad basado en IP o la conectividad saliente de toocontrol de reglas NSG, hello siguientes intervalos IP necesitan toobe en la lista blanca, dependiendo de las ubicaciones de origen y destino de Hola de máquinas virtuales de hello:

    - Ubicación de origen de todos los intervalos de direcciones IP que corresponden toohello. Descarga hello [intervalos](https://www.microsoft.com/download/confirmation.aspx?id=41653).) Creación de listas blancas es necesario, para que se pueden escribir datos toohello cuenta de almacenamiento de caché de hello máquina virtual.
    - Todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity). Si IP nueva agréguese tooOffice 365 intervalos IP, deberá toocreate nuevas reglas de NSG.
-     Las direcciones IP de punto de conexión del servicio de Site Recovery ([disponibles en un archivo XML](https://aka.ms/site-recovery-public-ips)), que dependen de la ubicación de destino: 

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

## <a name="example-nsg-configuration"></a>Configuración de NSG de ejemplo

Esta sección muestra cómo las reglas de tooconfigure NSG, por lo que las replicaciones funciona para una máquina virtual. Si usas conectividad saliente de toocontrol de reglas NSG, usar reglas de "Permitir salientes HTTPS" para todos los intervalos IP de hello necesario.

En este ejemplo, hello ubicación de origen de máquina virtual es "UU". ubicación de destino de replicación de Hello es US Central.


### <a name="example"></a>Ejemplo

#### <a name="east-us"></a>Este de EE. UU.

1. Crear reglas que corresponden demasiado[intervalos de direcciones IP de este de EE. UU.](https://www.microsoft.com/download/confirmation.aspx?id=41653). Esto es necesario para que se pueden escribir datos toohello cuenta de almacenamiento de caché de hello máquina virtual.
2. Crear reglas para todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crear reglas que corresponden toohello ubicación de destino:

   **Ubicación** | **Direcciones IP del servicio de Site Recovery** |  **IP de supervisión de Site Recovery**
    --- | --- | ---
   Central EE. UU.: | 40.69.144.231</br>40.69.167.116 | 52.165.34.144

#### <a name="central-us"></a>Central EE. UU.:

Estas reglas son necesarias para que se puede habilitar la replicación de la región de origen del toohello Hola de región de destino, después de la conmutación por error.

1. Crear reglas que corresponden demasiado[intervalos de direcciones IP de EE. UU. Central](https://www.microsoft.com/download/confirmation.aspx?id=41653).
2. Crear reglas para todos los intervalos IP que corresponden tooOffice 365 [puntos de conexión de IP V4 de autenticación e identidad](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_identity).
3. Crear reglas que corresponden toohello ubicación de origen:

   **Ubicación** | **Direcciones IP del servicio de Site Recovery** |  **IP de supervisión de Site Recovery**
    --- | --- | ---
   Este de EE. UU. | 13.82.88.226</br>40.71.38.173 | 104.45.147.24


## <a name="existing-on-premises-connection"></a>Conexión existente a local

Si tiene una conexión ExpressRoute o VPN entre el sitio local y la ubicación de origen de hello en Azure, siga estas instrucciones:

**Configuración** | **Detalles**
--- | ---
**Tunelización forzada** | Normalmente una ruta predeterminada (0.0.0.0/0) fuerza tooflow de tráfico saliente de internet a través de la ubicación local de Hola. Esta opción no se recomienda. El tráfico de replicación y las comunicaciones de Site Recovery deben permanecer dentro de Azure.<br/><br/> Como una solución, agregar rutas definidas por el usuario (UDRs) para [estos intervalos IP](#outbound-connectivity-for-azure-site-recovery-ip-ranges), para que el tráfico de hello no entren en local.
**Conectividad** | Si las aplicaciones necesitan máquinas de tooconnect tooon local o los clientes en entornos conectan toohello aplicación a través de local a través de VPN/ExpressRoute, asegúrese de que tiene al menos un [conexión de sitio a sitio](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md), entre el destino de hello región de Azure y sitio local de Hola.<br/><br/> Si los volúmenes de tráfico son altos entre Hola destino región de Azure y sitio local de hello, crear otro [conexión ExpressRoute](../expressroute/expressroute-introduction.md), entre la región de destino de Hola y local.<br/><br/> Si desea tooretain direcciones IP para las máquinas virtuales después de la conmutación por error, tenga conexión de sitio a sitio o ExpressRoute de la región de destino de hello en estado desconectado. Esto no garantiza que no habrá ningún conflictos de intervalo entre los intervalos de direcciones IP de origen y destino Hola.
**ExpressRoute** | Crear un circuito ExpressRoute en hello regiones de origen y destino.<br/><br/> Crear una conexión entre la red de origen de Hola y el circuito de ExpressRoute de Hola y entre la red de destino de Hola y el circuito de Hola.<br/><br/> Se recomienda usar diferentes intervalos IP en las regiones de origen y destino. Hello circuito no sea capaz de tooconnect toomore de redes de uno Azure con hello mismo intervalos IP, en hello mismo tiempo.<br/><br/> Puede crear redes virtuales con hello misma IP comprendido en ambas regiones y, a continuación, crear circuitos ExpressRoute en ambas regiones. Para la conmutación por error, desconéctese circuito Hola de red virtual de origen de Hola y conéctese circuito hello en la red virtual de destino de Hola.<br/><br/> Si la región principal de hello es completamente hacia abajo, la operación de desconexión Hola podría producir un error. En este caso, la red virtual de destino de hello no obtendrá conectividad de ExpressRoute.
**ExpressRoute Premium** | Puede crear circuitos en hello misma región geopolíticos.<br/><br/> circuitos toocreate en distintas regiones geopolíticas, necesita Azure ExpressRoute Premium.<br/><br/> Con Premium, el costo de hello es incremental. Si ya está usándolo, no hay ningún costo adicional.<br/><br/> Obtenga más información sobre [ubicaciones](../expressroute/expressroute-locations.md#azure-regions-to-expressroute-locations-within-a-geopolitical-region) y [precios](https://azure.microsoft.com/pricing/details/expressroute/).



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 4: crear un almacén](azure-to-azure-walkthrough-vault.md)

