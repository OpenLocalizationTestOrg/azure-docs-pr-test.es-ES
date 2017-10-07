---
title: "aaaInfrastructure y conectividad tooSAP HANA en Azure (instancias de gran tamaño) | Documentos de Microsoft"
description: "Configure la conectividad necesaria infraestructura toouse SAP HANA en Azure (instancias de gran tamaño)."
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0af34fbd82413bf63981036a76eaa264d8299ec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a>Infraestructura y conectividad con SAP HANA en Azure (instancias grandes) 

Algunas definiciones iniciales antes de leer esta guía. En [Introducción y arquitectura de SAP HANA en Azure (instancias grandes)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) se presentan dos clases distintas de unidades de HANA (Instancias grandes) con:

- S72, S72m, S144, S144m, S192 y S192m, que nos referiremos tooas hello 'Tipo clase' de SKU.
- S384, S384m, S384xm, S576, S768 y S960, que nos referiremos tooas Hola 'Clase de tipo II' de SKU.

especificadores de clase de Hello son toobe continuo utilizada a lo largo de hello HANA instancia grande documentación tooeventually consulte toodifferent capacidades y requisitos basándose en las SKU de HANA grandes instancia.

Otras definiciones que se usan con frecuencia son:
- **Marca de la instancia de gran tamaño:** una pila de infraestructura de hardware que es SAP HANA TDI certificadas y dedicado instancias de SAP HANA toorun dentro de Azure.
- **SAP HANA en Azure (instancias de gran tamaño):** nombre oficial de oferta de hello en instancias HANA toorun Azure en SAP HANA TDI certificadas hardware que se implementa en marcas de instancia grande en diferentes regiones de Azure. Hola relacionadas con los términos **instancia grande de HANA** es corto para SAP HANA en Azure (instancias de gran tamaño) y es muy utilizado esta guía de implementación técnica.
 

Después de finalización compra Hola de SAP HANA en Azure (instancias de gran tamaño) entre el usuario y Hola, equipo de cuentas de empresa de Microsoft, hello información siguiente requieren Microsoft toodeploy HANA grandes unidades de instancia:

- Nombre del cliente
- Información del contacto de la empresa (incluida la dirección de correo electrónico y el número de teléfono)
- Información del contacto técnico (incluida la dirección de correo electrónico y el número de teléfono)
- Información del contacto técnico de red (incluida la dirección de correo electrónico y el número de teléfono)
- Región de implementación de Azure (oeste de EE. UU., este de EE. UU., este de Australia, sudeste de Australia, Europa Occidental y Europa del Norte a partir de julio) 
- 2017)
- Confirmación de la SKU de SAP HANA en Azure (Instancias grandes) (configuración)
- Como ya detallados en el en hello información general y documento de arquitectura HANA instancias grandes, para cada región de Azure está implementando en:
    - / 29 intervalo de direcciones IP para las conexiones de ER P2P que se conectan a instancias de gran tamaño tooHANA de redes virtuales de Azure
    - Un /24 bloque CIDR destinadas Hola HANA grandes instancias grupo IP del servidor
- utilizado en hello atributo de espacio de direcciones de red virtual de cada red virtual de Azure que se conecta a instancias de gran tamaño de HANA toohello de valores del intervalo de direcciones IP Hola
- Datos para cada sistema Instancias grandes de HANA:
  - Nombre de host deseado, preferiblemente el nombre de dominio completo.
  - Dirección IP deseada para unidad de instancia grande de HANA Hola fuera Hola intervalo de direcciones del grupo de IP de servidor: tenga en cuenta que hello primeros 30 direcciones IP en hello grupo de IP del servidor intervalo de direcciones están reservados para uso interno dentro de instancias grandes HANA
  - Nombre de SAP HANA SID de instancia de SAP HANA hello (toocreate necesario Hola necesario en disco relacionados con SAP HANA volúmenes). Hola HANA SID es necesario para crear permisos de Hola para <sidadm> en volúmenes NFS de hello, que está obteniendo la unidad de instancia grande de HANA toohello adjunto. También se utiliza como uno de los componentes del nombre Hola Hola de volúmenes de disco que se monte. Si desea toorun más de una instancia HANA en la unidad de hello, deberá a toolist varios SID de HANA. Cada uno obtiene un conjunto independiente de volúmenes asignados.
  - Hello groupid Hola hana-SIDADM usuario tiene en el sistema operativo Linux hello es necesario toocreate volúmenes de disco necesario relacionados con SAP HANA Hola. Hola instalación de SAP HANA crea normalmente grupo de hello sapsys con un identificador de grupo de 1001. usuario de hana-SIDADM Hola forma parte de ese grupo
  - Hello userid Hola hana-SIDADM usuario tiene en el sistema operativo Linux hello es necesario toocreate volúmenes de disco necesario relacionados con SAP HANA Hola. Si está ejecutando varias instancias HANA en la unidad de hello, necesita toolist Hola a todos <sid>usuarios de adm 
- Id. de suscripción de Azure para toowhich de suscripción de Azure Hola SAP HANA en instancias de Azure HANA grandes va toobe conectado directamente. Hola suscripción de Azure, que queda toobe cobra con hello instancia grande de HANA unidades hace referencia a este identificador de suscripción.

Después de proporcionar Hola información, disposiciones Microsoft SAP HANA en Azure (instancias de gran tamaño) y devolverá Hola información necesarios toolink las redes virtuales de Azure tooHANA instancias grandes y tooaccess Hola instancia grande de HANA unidades.

## <a name="connecting-azure-vms-toohana-large-instances"></a>Conectar máquinas virtuales de Azure tooHANA grandes instancias

Como ya se mencionó en [información general de SAP HANA (instancias de gran tamaño) y la arquitectura en Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) implementación mínima Hola de HANA instancias de gran tamaño con nivel de aplicación de SAP de hello en busca de Azure, como:

![Red virtual de Azure conectado tooSAP HANA en Azure (instancias de gran tamaño) y local](./media/hana-overview-architecture/image3-on-premises-infrastructure.png)

Examinar más de cerca en hello lado de la red virtual de Azure, somos conscientes de la necesidad de hello para:

- definición de Hola de una red virtual de Azure es continuo toobe utiliza toodeploy hello las máquinas virtuales de nivel de aplicación de SAP de hello en.
- Esto automáticamente significa que una subred predeterminada de Hola se define la red virtual de Azure que está realmente Hola uno usa toodeploy hello las máquinas virtuales en.
- Hola red virtual de Azure que se crea debe toohave al menos una subred VM y una subred de puerta de enlace de ExpressRoute. Estas subredes se deben asignar intervalos de direcciones IP de hello como especificado y se ha descrito en hello las secciones siguientes.

Por lo tanto, echemos un vistazo un poco más de cerca en hello creación de red virtual de Azure para instancias de gran tamaño de HANA

### <a name="creating-hello-azure-vnet-for-hana-large-instances"></a>Crear red virtual de Azure de Hola para instancias de gran tamaño de HANA

>[!Note]
>Hola red virtual de Azure para instancia grande de HANA debe crearse con el modelo de implementación de hello Azure Resource Manager. modelo de implementación de Azure antiguo Hello, que normalmente se conoce como modelo de implementación clásico, no es compatible con hello solución instancia grande de HANA.

Hello red virtual puede crearse con hello portal de Azure, PowerShell, plantilla de Azure o CLI de Azure (consulte [crear una red virtual con el portal de Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)). En el siguiente ejemplo de Hola, ponemos atención a una red virtual se creó mediante Hola portal de Azure.

Si tomamos en definiciones de Hola de una red virtual de Azure a través del portal de Azure de hello, echemos un vistazo a algunas de las definiciones de Hola y cómo los que se relacionan con toowhat se lista de intervalos de direcciones IP diferentes. Como estamos hablando de hello **espacio de direcciones**, se entiende el espacio de direcciones de Hola Hola red virtual de Azure se permite toouse. Este espacio de direcciones también es el intervalo de direcciones de Hola que Hola usos de la red virtual para la propagación de la ruta BGP. Este **espacio de direcciones** puede verse a continuación:

![Espacio de direcciones de red Azure virtual muestra de Hola portal de Azure](./media/hana-overview-connectivity/image1-azure-vnet-address-space.png)

En caso de hello anterior, con 10.16.0.0/16, Hola red virtual de Azure se asignó un toouse de intervalo de direcciones IP anchas y de gran tamaño en su lugar. Significa que todos los intervalos de direcciones IP de Hola de subredes subsiguientes dentro de esta red virtual pueden tener sus intervalos dentro de ese espacio de direcciones de' '. Normalmente no se recomienda un intervalo de direcciones tan grande para una única red virtual de Azure. Pero recibe un paso más allá, echemos un vistazo en subredes Hola definidos en hello red virtual de Azure:

![Subredes de la red virtual de Azure y sus intervalos de direcciones IP](./media/hana-overview-connectivity/image2b-vnet-subnets.png)

Como se puede ver, hay una primera subred de máquina virtual (denominada "default") y una subred llamada "GatewaySubnet".
En los pasos de la sección de hello, nos referimos toohello intervalo de direcciones IP de subred de hello, que se llamó a 'default' en gráficos de hello como **intervalo de dirección IP de subred de VM de Azure**. En las secciones siguientes de hello, nos referimos toohello intervalo de direcciones IP de subred de puerta de enlace de hello como **intervalo de direcciones IP de subred de puerta de enlace de red virtual**. 

En el caso de hello muestra gráficos de hello dos anteriores, verá que hello **espacio de direcciones de red virtual** cubre ambos, hello **intervalo de dirección IP de subred de VM de Azure** hello y **dirección IP de subred de puerta de enlace de red virtual intervalo**. 

En otros casos donde necesita tooconserve o ser específico con los intervalos de direcciones IP, puede restringir hello **espacio de direcciones de red virtual** de una red virtual toohello determinados intervalos usándola cada subred. En este caso, puede definir hello **espacio de direcciones de red virtual** de una red virtual específica como varios intervalos como se muestra aquí:

![Espacio de direcciones de red virtual de Azure con dos espacios](./media/hana-overview-connectivity/image3-azure-vnet-address-space_alternate.png)

En este caso, Hola **espacio de direcciones de red virtual** tiene dos espacios definidos. Estos dos espacios, se definen los intervalos de direcciones IP idénticas toohello para **intervalo de dirección IP de subred de VM de Azure** hello y **intervalo de direcciones IP de subred de puerta de enlace de red virtual.**

Puede usar la nomenclatura que desee para estas subredes de inquilino (subredes de máquina virtual). Sin embargo, **siempre debe haber uno y solo una subred de puerta de enlace para cada red virtual** que conecta toohello SAP HANA en el circuito de ExpressRoute de Azure (instancias de gran tamaño). Y **esta subred de puerta de enlace siempre debe denominada "GatewaySubnet"** tooensure selección de ubicación correcta de puerta de enlace de ExpressRoute de Hola.

> [!WARNING] 
> Es fundamental que esa subred de puerta de enlace de hello siempre se denomina "GatewaySubnet".

Se pueden utilizar varias subredes de máquina virtual, incluso con intervalos de direcciones no contiguas. Pero como se mencionó anteriormente, estos intervalos de direcciones deben ser abarcados por hello **espacio de direcciones de red virtual** de hello red virtual en forma agregada o en una lista de hello exacta intervalos de subredes de VM de Hola y Hola subred de puerta de enlace.

Resumir los hechos importantes de hello sobre una red virtual de Azure que se conecta a instancias de gran tamaño tooHANA:

- Necesita toosubmit tooMicrosoft hello **espacio de direcciones de red virtual** al realizar la implementación inicial de instancias de HANA grandes. 
- Hola **espacio de direcciones de red virtual** puede ser un intervalo mayor que abarque el intervalo de Hola para intervalos de direcciones IP de subred de VM de Azure y el intervalo de direcciones IP de subred de puerta de enlace de red virtual de Hola.
- O puede enviar como **espacio de direcciones de red virtual** intervalos de rangos de direcciones IP de subred VM y el intervalo de direcciones IP de subred de puerta de enlace de red virtual de Hola de direcciones de varios intervalos que cubren Hola otra dirección IP.
- Hola definido **espacio de direcciones de red virtual** es usada propagación de enrutamiento de BGP.
- nombre de Hola de subred de puerta de enlace de hello debe ser: **"GatewaySubnet".**
- Hola **espacio de direcciones de red virtual** se usa como un filtro en hello instancia grande de HANA lado tooallow o no permitir unidades de instancia grande de HANA toohello de tráfico de Azure. Si no coinciden Hola información de enrutamiento de BGP de hello red virtual de Azure e intervalos de direcciones IP de hello configurados para el filtrado en hello lado de la instancia de HANA grande, pueden surgir problemas de conectividad.
- Hay algunos detalles acerca de la subred de puerta de enlace de Hola que describen más adelante en la sección 'Conectar un tooHANA de red virtual grande de instancia de ExpressRoute'



### <a name="different-ip-address-ranges-toobe-defined"></a>Diferentes toobe de intervalos de direcciones IP definido 

Ya presentamos algunos de hello IP dirección intervalos necesario toodeploy HANA instancias grandes en las secciones anteriores. Pero hay algunos otros intervalos de direcciones IP que son importantes. Analicemos algunos detalles adicionales. Hello siguientes direcciones IP de los cuales no todas ellas deben toobe envían tooMicrosoft necesita toobe definido, antes de enviar una solicitud para la implementación inicial:

- **Espacio de direcciones de red virtual:** como ya introducidos anteriormente, está o dirección IP de hello intervalos que haya asignado (o planea tooassign) parámetro de espacio de dirección tooyour Hola redes virtuales de Azure (VNet) conectarse toohello instancia grande de SAP HANA entorno. Se recomienda que este parámetro de espacio de direcciones es un valor de varias líneas formado por intervalos de subred de VM de Azure de Hola y Hola intervalo de subred de puerta de enlace de Azure como se muestra en los gráficos de hello anteriormente. Este intervalo no se debe solapar con los intervalos de direcciones locales, ni con los del grupo de direcciones IP de servidor, ni con los de ER-P2P. ¿Cómo tooget esto o estos intervalos de direcciones IP? El equipo de redes corporativas o el proveedor de servicios deben proporcionar uno o varios intervalos de direcciones IP que no se usen en la red. Ejemplo: Si la subred de VM de Azure (vea anteriormente) es 10.0.1.0/24 y la subred de puerta de enlace de Azure (consulte la siguiente) es 10.0.2.0/28, a continuación, el espacio de direcciones de red virtual de Azure se recomienda toobe dos líneas; 10.0.1.0/24 y 10.0.2.0/28. Aunque se pueden agregar valores de espacio de direcciones de hello, se recomienda coincidencia de intervalos de subred toohello tooavoid reutilización accidental de IP sin usar intervalos de direcciones dentro de espacios de direcciones más grandes de hello futuras en otra parte de la red. **Hola espacio de direcciones de red virtual es un intervalo de direcciones IP, qué toobe necesidades enviado tooMicrosoft al solicitar la implementación inicial**

- **Intervalo de dirección IP de subred de VM de Azure:** intervalo de direcciones de esta dirección IP, como se ha explicado anteriormente ya, es hello uno que haya asignado (o planea tooassign) toohello parámetro de subred de red virtual de Azure en la red virtual de Azure conectar el entorno de la instancia de SAP HANA grande de toohello . Este intervalo de direcciones IP es tooyour de direcciones IP de tooassign usa máquinas virtuales de Azure. se permiten direcciones IP de Hello fuera de este intervalo tooconnect tooyour servidores de la instancia de SAP HANA grande. Si es necesario, se pueden utilizar varias subredes de máquina virtual de Azure. Microsoft recomienda un bloque CIDR /24 para cada subred de máquina virtual de Azure. Este intervalo de direcciones debe ser una parte de los valores de hello utilizados en hello espacio de direcciones de red virtual de Azure. ¿Cómo tooget este intervalo de direcciones IP? El equipo de redes corporativas o el proveedor de servicios deben proporcionar un intervalo de direcciones IP no utilizado actualmente en la red.

- **Intervalo de direcciones IP de subred de puerta de enlace de red virtual:** función hello características que piensa toouse, hello recomienda tamaño sería:
   - Puerta de enlace de ExpressRoute de ultrarrendimiento: bloque de direcciones /26: se necesita para la clase de tipo II de SKU
   - Coexistencia con VPN y ExpressRoute mediante una puerta de enlace de ExpressRoute de alto rendimiento (o inferior): bloque de direcciones /27
   - Resto de situaciones: bloque de direcciones /28. Este intervalo de direcciones debe ser una parte de los valores de hello utilizados en los valores de "Espacio de direcciones de red virtual" Hola. Este intervalo de direcciones debe ser una parte de los valores de hello utilizados en los valores de espacio de direcciones de red virtual de Azure de Hola que necesita toosubmit tooMicrosoft. ¿Cómo tooget este intervalo de direcciones IP? El equipo de redes corporativas o el proveedor de servicios deben proporcionar un intervalo de direcciones IP no utilizado actualmente en la red. 

- **Intervalo para la conectividad de ER P2P de direcciones:** este intervalo representa el intervalo IP de hello para la conexión de ExpressRoute de instancia grande (ER) de SAP HANA P2P. Este intervalo de direcciones IP debe ser un intervalo de direcciones IP CIDR /29. Este intervalo no se debe superponer con los intervalos de direcciones locales ni con otros intervalos de direcciones IP de Azure. Este intervalo de direcciones IP es tooset usa la conectividad de hello ER desde los servidores de puerta de enlace de ExpressRoute de red virtual de Azure toohello instancia grande de SAP HANA. ¿Cómo tooget este intervalo de direcciones IP? El equipo de redes corporativas o el proveedor de servicios deben proporcionar un intervalo de direcciones IP no utilizado actualmente en la red. **Este intervalo es un intervalo de direcciones IP, qué toobe necesidades enviado tooMicrosoft al solicitar la implementación inicial**
  
- **Intervalo de direcciones de grupo IP del servidor:** este intervalo de direcciones IP es tooassign usado Hola individuales tooHANA instancia grandes servidores con direcciones IP. Hola recomendado de tamaño de la subred es un /24 CIDR bloquear - pero si necesita puede ser menor mínimo tooa de proporcionar 64 direcciones IP. De este intervalo, hello primeros 30 direcciones IP están reservadas para su uso por parte de Microsoft. Asegúrese de que este hecho se tiene en cuenta al elegir el tamaño de Hola de intervalo de Hola. Este intervalo no se debe superponer con los intervalos de direcciones locales ni con otras direcciones IP de Azure. ¿Cómo tooget este intervalo de direcciones IP? El equipo de redes corporativas o el proveedor de servicios deben proporcionar un intervalo de direcciones IP no utilizado actualmente en la red. Un /24 (recomendado) único CIDR bloquear toobe que se usa para asignar direcciones IP específicas Hola necesarias para SAP HANA en Azure (instancias de gran tamaño). **Este intervalo es un intervalo de direcciones IP, qué toobe necesidades enviado tooMicrosoft al solicitar la implementación inicial**
 
Aunque necesita toodefine y planear intervalos de direcciones IP de hello anteriores, no todas ellas necesitan tooMicrosoft toobe transmitida. Hola toosummarize anterior, intervalos de direcciones IP de hello son tooMicrosoft tooname necesarios son:

- Espacios de direcciones de la red virtual de Azure
- Intervalo de direcciones para conectividad ER-P2P
- Intervalo de direcciones del grupo de direcciones IP de servidor

Agregar redes virtuales adicionales que necesitan tooconnect tooHANA instancias de gran tamaño, requiere que toosubmit Hola nuevo espacio de direcciones de red virtual de Azure que va a agregar tooMicrosoft. 

Siguiente es un ejemplo de distintos intervalos de Hola y algunos intervalos de ejemplo como necesite tooconfigure y finalmente proporcionan tooMicrosoft. Como puede ver, valor de Hola para hello espacio de direcciones de red virtual de Azure no se agrega en el primer ejemplo de Hola, pero se define de intervalos de Hola de hello primera máquina virtual de Azure intervalo IP de subred dirección y el intervalo de direcciones IP de subred de puerta de enlace de red virtual de Hola. Con varias subredes VM en hello red virtual de Azure se trabajo según corresponda mediante la configuración y enviar Hola IP adicionales Hola intervalos de direcciones de subredes VM adicionales como parte del programa Hola espacio de direcciones de red virtual de Azure.

![Intervalos de direcciones IP necesarios en la implementación mínima de SAP HANA en Azure (Instancias grandes)](./media/hana-overview-connectivity/image4b-ip-addres-ranges-necessary.png)

También tiene posibilidad de Hola de agregación de datos de hello enviar tooMicrosoft. En ese caso, Hola espacio de direcciones de red virtual de Azure Hola sólo incluye un carácter de espacio. Uso de intervalos de direcciones IP de hello utilizados en el ejemplo de Hola anterior. Este espacio de direcciones de red virtual agregado podría tener un aspecto como este:

![Segunda posibilidad de intervalos de direcciones IP necesarios en la implementación mínima de SAP HANA en Azure (Instancias grandes)](./media/hana-overview-connectivity/image5b-ip-addres-ranges-necessary-one-value.png)

Como puede ver más arriba, en lugar de dos intervalos más pequeños que define el espacio de direcciones de Hola de hello red virtual de Azure, tenemos un intervalo mayor que abarque 4096 direcciones IP. Esa definición grande de espacio de direcciones de hello deja algunos intervalos bastante grandes sin usar. Puesto que los valores de espacio de direcciones de red virtual de Hola se usan para la propagación de la ruta BGP, el uso de Hola intervalos sin usar local o en otra parte de la red puede provocar problemas de enrutamientos. Por lo tanto es hello tookeep recomendada que espacio de direcciones estrechamente alineado con el espacio de direcciones de subred real Hola usado. Si es necesario, sin incurrir en tiempo de inactividad en Hola de red virtual, siempre puede agregar nuevos valores de espacio de direcciones más adelante.
 
> [!IMPORTANT] 
> Espacio de direcciones de red virtual de Azure de intervalo de ER-P2P, grupo de IP del servidor, de cada dirección IP debe **no** se superponen entre sí o cualquier otro intervalo utilizado en otro lugar de la red; cada uno de ellos debe ser discreta y como gráficos de hello dos mostrar anterior, no puede ser un subred de cualquier otro intervalo. Si se producen las superposiciones entre los intervalos, Hola red virtual de Azure no puede conectarse toohello circuito de ExpressRoute.

### <a name="next-steps-after-address-ranges-have-been-defined"></a>Pasos siguientes después de definir los intervalos de direcciones
Después de definir intervalos de direcciones IP de hello, hello actividades siguientes necesitan toohappen:

1. Enviar intervalos de direcciones IP de hello para el espacio de direcciones de red virtual de Azure, conectividad de ER P2P de Hola y el intervalo de direcciones de grupo de IP de servidor junto con otros datos que se haya indicado al principio de saludo del documento de Hola. En este momento, también puede iniciar toocreate Hola red virtual y subredes de VM de Hola. 
2. Un circuito de Express Route es creado por Microsoft entre la suscripción de Azure y la marca de la instancia de gran tamaño de HANA Hola.
3. Se crea una red de inquilinos en la marca de la instancia grande de Hola por Microsoft.
4. Microsoft configura la red en hello SAP HANA en tooaccept de infraestructura de Azure (instancias de gran tamaño) de direcciones IP de su Azure red virtual de espacio de direcciones que se comunica con instancias de gran tamaño de HANA.
5. Función hello adquirido específico de SAP HANA en SKU de Azure (instancias grandes), Microsoft le asigna una unidad de proceso en una red de inquilinos, asignar y montar almacenamiento e instalar sistema operativo de hello (SUSE o Red Hat Linux). Direcciones IP de estas unidades se quitara Hola dirección de grupo de IP del servidor intervalo enviado tooMicrosoft.

Al final de Hola Hola del proceso de implementación, Microsoft ofrece Hola después tooyou de datos:
- Información necesaria tooconnect el circuito de ExpressRoute de toohello VNet(s) de Azure que se conecta a instancias de gran tamaño tooHANA de redes virtuales de Azure:
     - Claves de autorización
     - PeerID de ExpressRoute
- Datos tooaccess instancias grandes HANA después de establecer circuito ExpressRoute y red virtual de Azure.

También puede encontrar la secuencia de Hola de conexión HANA instancias de gran tamaño en el documento de hello [finalizar el programa de instalación para instancias de gran tamaño de SAP HANA tooEnd](https://azure.microsoft.com/resources/sap-hana-on-azure-large-instances-setup/). Muchas de hello pasos se muestran en una implementación de ejemplo de dicho documento. 


## <a name="connecting-a-vnet-toohana-large-instance-expressroute"></a>Conectar un tooHANA de red virtual grandes ExpressRoute de instancia

Tal y como define todos los intervalos de direcciones IP de Hola y ahora tenemos datos Hola nuevo de Microsoft, puede iniciar conexión Hola red virtual que creó antes de tooHANA instancias de gran tamaño. Una vez Hola que se crea la red virtual de Azure, una puerta de enlace de ExpressRoute debe crearse en hello red virtual toolink Hola red virtual toohello circuito de ExpressRoute que se conecta a toohello inquilino de cliente en la marca de la instancia grande de Hola.

> [!NOTE] 
> Este paso puede tardar hasta too30 minutos toocomplete, tal y como nueva puerta de enlace de Hola se crea en Hola designado de suscripción de Azure y, a continuación, toohello conectado especifica red virtual de Azure.

Si ya existe una puerta de enlace, compruebe si se trata de una puerta de enlace de ExpressRoute o no. Si no es así, puerta de enlace de hello debe eliminarse y volver a crear como una puerta de enlace de ExpressRoute. Si una puerta de enlace de ExpressRoute ya establecida, puesto que Hola que red virtual de Azure ya está conectado toohello circuito de ExpressRoute para la conectividad local, continúe toohello vincular redes virtuales sección más adelante.

- Usar cualquier hello (nuevo) [portal de Azure](https://portal.azure.com/), o toocreate de PowerShell una puerta de enlace de ExpressRoute VPN conectado tooyour red virtual.
  - Si usas Hola portal de Azure, agregue un nuevo **puerta de enlace de red Virtual** y, a continuación, seleccione **ExpressRoute** como tipo de puerta de enlace de Hola.
  - Si ha elegido PowerShell en su lugar, descargar y usar hello más reciente [SDK de Azure PowerShell](https://azure.microsoft.com/downloads/) tooensure una experiencia óptima. Hola, siga los comandos crea una puerta de enlace de ExpressRoute. textos de Hello precedido por un  _$_  son variables definidas por el usuario que toobe necesidad actualizado con información específica de su.

```PowerShell
# These Values should already exist, update toomatch your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used toocreate hello gateway, update for how you wish hello GW components toobe named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create hello Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

En este ejemplo, se usó Hola SKU de puerta de enlace de alto rendimiento. Las opciones son alto rendimiento o UltraPerformance como Hola solo los SKU de puerta de enlace que son compatibles con SAP HANA en Azure (instancias de gran tamaño).

> [!IMPORTANT]
> Para tipos de instancias de gran tamaño de HANA de hello SKU S384, S384m, S384xm, S576, S768 y S960 (tipo de clase II SKU), hello uso de hello UltraPerformance SKU de puerta de enlace es obligatorio.

### <a name="linking-vnets"></a>Vinculación de redes virtuales

Ahora que hello red virtual de Azure tiene una puerta de enlace de ExpressRoute, use la información de autorización de hello proporcionada por Microsoft tooconnect hello ExpressRoute puerta de enlace toohello SAP HANA en circuito de ExpressRoute de Azure (instancias de gran tamaño) creado para esta conectividad. Este paso puede realizarse mediante el portal de Azure de Hola o PowerShell. se recomienda portal Hello, sin embargo son las siguientes instrucciones de PowerShell. 

- Ejecute hello siguientes comandos para cada puerta de enlace de red virtual con un AuthGUID diferente para cada conexión. en primer lugar dos entradas de Hola que se muestra en el siguiente script de Hola proceden de información de hello proporcionada por Microsoft. Además, hello AuthGUID es específica para cada red virtual y su puerta de enlace. Significa que si desea tooadd otra red virtual de Azure, necesitará tooget AuthID otro para el circuito de ExpressRoute que conecta instancias grandes HANA en Azure. 

```PowerShell
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define hello name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between hello ER Circuit and your Gateway using hello Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

Si desea tooconnect Hola puerta de enlace toomultiple circuitos ExpressRoute que están asociados a su suscripción, deberá tooexecute este paso más de una vez. Por ejemplo, es probable que se va tooconnect Hola mismo circuito de ExpressRoute de toohello de puerta de enlace de red virtual que conecta la red de hello tooyour de red virtual en local.

## <a name="adding-more-ip-addresses-or-subnets"></a>incorporación de más direcciones IP o subredes

Usar cualquier Hola portal de Azure, PowerShell o CLI al agregar más direcciones IP o subredes.

En este caso, recomendación de hello es intervalo de tooadd Hola direcciones IP como toohello de intervalo nuevo espacio de direcciones de red virtual en lugar de generar un nuevo intervalo agregado. En cualquier caso, es necesario toosubmit este cambio tooMicrosoft tooallow conectarse fuera de ese nuevas unidades IP dirección intervalo toohello HANA grandes instancia en el cliente. Puede abrir un soporte técnico de Azure solicitud tooget Hola nueva dirección de red virtual espacio que se agrega. Después de recibir la confirmación, realice los pasos siguientes de Hola.

toocreate una subred adicional de hello portal de Azure, vea el artículo de hello [crear una red virtual con el portal de Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), y toocreate desde PowerShell, consulte [crear una red virtual con PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="adding-vnets"></a>Incorporación de redes virtuales

Después de conectarse inicialmente una o varias redes virtuales de Azure, conviene tooadd perfiles adicionales que tienen acceso a SAP HANA en Azure (instancias de gran tamaño). En primer lugar, envíe una solicitud de soporte técnico de Azure, en esa solicitud incluya Hola información específica identificación Hola determinada implementación de Azure y de intervalos de espacio de direcciones IP de Hola de hello espacio de direcciones de red virtual de Azure. SAP HANA en administración de servicios de Azure, a continuación, proporciona información necesaria de hello necesita tooconnect Hola ExpressRoute y redes virtuales adicionales. Para cada red virtual, es necesario un único toohello de tooconnect instancias grandes de circuito de ExpressRoute tooHANA de clave de autorización.

Pasos tooadd una nueva red virtual de Azure:

1. Completar Hola primer paso en el proceso de incorporación de hello, vea hello _crear red virtual de Azure_ sección.
2. Completar Hola segundo paso en el proceso de incorporación de hello, vea hello _crear subred de puerta de enlace_ sección.
3. tooconnect su toohello de redes virtuales adicional circuito de ExpressRoute de instancia grande de HANA, abra una solicitud de soporte técnico de Azure con información en Hola red virtual nueva y solicitar una nueva clave de autorización.
4. Una vez que se le notifique que la autorización de hello es completar, use la información de autorización proporcionado por Microsoft de Hola Hola toocomplete tercer paso en el proceso de incorporación de hello, vea hello _vincular redes virtuales_ sección.

## <a name="increasing-expressroute-circuit-bandwidth"></a>Aumento del ancho de banda del circuito de ExpressRoute

Consulte con SAP HANA en Azure Service Management. Si es el ancho de banda de tooincrease aconsejable Hola de hello SAP HANA en el circuito de ExpressRoute de Azure (instancias grandes), cree una solicitud de soporte técnico de Azure. (Puede solicitar un aumento de un ancho de banda de circuito único seguridad tooa máximo de 10 Gbps). A continuación, recibir notificación cuando se complete; Hola operación necesaria ninguna otra acción tooenable esta velocidad superior en Azure.

## <a name="adding-an-additional-expressroute-circuit"></a>Incorporación de un circuito de ExpressRoute adicional

Consulte con SAP HANA en administración de servicios de Azure, si es preferible que se necesita un circuito de ExpressRoute adicional, realice una toocreate de solicitud de soporte técnico de Azure un nuevo circuito de ExpressRoute (y tooget autorización información tooconnect tooit). Puede utilizar espacio de direcciones de Hola que va en hello que redes virtuales deben definirse antes de realizar la solicitud de hello, en orden para SAP HANA a la autorización de tooprovide de administración de servicios de Azure.

Una vez que se crea el nuevo circuito de Hola y Hola SAP HANA en configuración de administración de servicios de Azure se completa, va tooreceive notificación con información de Hola que necesita tooproceed. Siga los pasos de hello descritos anteriormente para la creación y la conexión de circuito adicional de hello nueva red virtual toothis. No está tooconnect capaz de redes virtuales de Azure toothis adicional circuito si ya conectados tooanother SAP HANA en circuito de ExpressRoute de Azure (instancia grande) en hello misma región de Azure.

## <a name="deleting-a-subnet"></a>Eliminación de una subred

se puede utilizar tooremove una subred de red virtual, ya sea Hola portal de Azure, PowerShell o CLI. Si el intervalo de direcciones IP de la red virtual de Azure o el espacio de direcciones de la red virtual de Azure fuesen intervalos agregados, no son necesarias acciones con Microsoft. Salvo que Hola red virtual todavía está propagando espacio de direcciones de rutas BGP que incluye Hola eliminar subred. Si define Hola IP de red virtual de Azure dirección intervalo/Azure espacio de direcciones de red virtual como varios intervalos de direcciones IP de los cuales uno era subred asignado tooyour eliminado, debe eliminar fuera de su espacio de direcciones de red virtual y posteriormente informar a SAP HANA en administración de servicios de Azure tooremove de hello intervalos que SAP HANA en Azure (instancias de gran tamaño) se permite toocommunicate con.

Mientras no hay más específicos y dedicada Azure.com obtener instrucciones acerca de cómo quitar subredes, proceso de Hola de eliminación de subredes es Hola invertir del proceso de Hola para agregarlos. Vea el artículo de hello [crear una red virtual con el portal de Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información sobre la creación de subredes.

## <a name="deleting-a-vnet"></a>Eliminación de una red virtual

Usar cualquier hello portal de Azure, PowerShell o CLI al eliminar una red virtual. SAP HANA en administración de servicios de Azure quita las autorizaciones existentes de hello en hello SAP HANA en el circuito de ExpressRoute de Azure (instancias de gran tamaño) y quitar intervalo Hola IP de red virtual de Azure dirección/Azure espacio de direcciones de red virtual para la comunicación de hello con instancias de HANA grandes.

Una vez que se ha quitado Hola red virtual, abra un espacio de direcciones soporte técnico de Azure solicitud tooprovide Hola IP que quitó toobe intervalos.

Mientras no hay más específicos y dedicada Azure.com obtener instrucciones acerca de cómo quitar redes virtuales, proceso de Hola para quitar las redes virtuales es Hola invertir del proceso de Hola para agregarlos, que se ha descrito anteriormente. Consulte los artículos de hello [crear una red virtual con el portal de Azure hello](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) y [crear una red virtual con PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) para obtener más información acerca de cómo crear redes virtuales.

tooensure todo lo que se quita, eliminar Hola siguientes elementos:

- Hola conexión ExpressRoute, puerta de enlace de red virtual, IP pública de puerta de enlace de red virtual y red virtual

## <a name="deleting-an-expressroute-circuit"></a>Eliminación de un circuito de ExpressRoute

tooremove un SAP HANA adicionales en el circuito de ExpressRoute de Azure (instancias grandes), abra una solicitud de soporte técnico de Azure con SAP HANA en administración de servicios de Azure y solicitar que se debe eliminar el circuito de Hola. Dentro de hello suscripción de Azure, puede eliminar o conservar Hola red virtual según sea necesario. Sin embargo, debe eliminar Hola circuito de ExpressRoute de HANA grandes instancias cuando se conecta Hola y Hola vinculado la puerta de enlace de red virtual.

Si también desea tooremove una red virtual, siga instrucciones de hello acerca de cómo eliminar una red virtual en la sección de hello anterior.


