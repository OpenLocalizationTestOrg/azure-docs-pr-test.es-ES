---
title: "aaaDesigning su infraestructura de red para la recuperación ante desastres | Documentos de Microsoft"
description: "En este artículo se describen las consideraciones de diseño de red para Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: prateek9us
manager: jwhit
editor: 
ms.assetid: ce787731-d930-4f00-a309-e2fbc2e1f53b
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/20/2017
ms.author: pratshar
ms.openlocfilehash: 18bafa1b8b334192bfaf2f4aeba9f090011041ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="designing-your-network-for-disaster-recovery"></a>Diseñe su red para la recuperación ante desastres.

Este artículo está dirigido tooIT profesionales de TI que son responsables de diseñar, implementar y admitir continuidad del negocio y la infraestructura de recuperación (BCDR), y que desean tooleverage toosupport de Microsoft Azure Site Recovery (ASR) y mejorar sus servicios BCDR. En este artículo se tratan consideraciones prácticas para estructurar la red del sitio de recuperación ante desastres, ya sea en Azure o en otro sitio local. 

## <a name="overview"></a>Información general
[Azure Site Recovery (ASR)](https://azure.microsoft.com/services/site-recovery/) es un servicio de Microsoft Azure que orquesta Hola protección y recuperación de las aplicaciones virtualizadas para fines de recuperación (BCDR) de desastres de continuidad de negocio. Este documento está previsto tooguide Hola lector a través del proceso Hola del diseño de redes de hello, centrándose en diseñar intervalos de IP y subredes en el sitio de recuperación ante desastres de hello, al replicar las máquinas virtuales (VM) con Site Recovery.

Además, este artículo demuestra cómo Site Recovery permite diseñar e implementar un servicio de centro de datos virtual multisitio toosupport BCDR en tiempo de prueba o un desastre.

En un mundo donde todos los usuarios espera 24/7 conectividad, es más importante que alguna vez tookeep la infraestructura y las aplicaciones activos y en funcionamiento. Hola de continuidad del negocio y recuperación ante desastres (BCDR) sirve toorestore no se pudo componentes para que organización Hola rápidamente puede reanudar las operaciones normales. Desarrollar toodeal estrategias de recuperación ante desastres con eventos improbable, devastadoras es muy complicado. Esto es debido toohello inherente dificultades a la hora de predecir las futuras hello, especialmente en lo referente tooimprobable eventos y Hola alto costo tooprovide las medidas adecuadas de protección frente a catástrofes de largo alcance.

Es crucial para la planeamiento de BCDR que Objetivo de tiempo de recuperación (RTO) y Objetivo de punto de recuperación (RPO) se definan como parte de un plan de recuperación ante desastres. Cuando produzca un desastre centro de datos del cliente de hello, con Azure Site Recovery, los clientes pueden rápidamente (RTO bajo) poner en línea sus máquinas virtuales replicadas ubicados en el centro de datos secundario de Hola o Microsoft Azure con pérdida de datos mínima (RPO bajo).

Conmutación por error se realiza mediante ASR que copia inicialmente designadas máquinas virtuales del centro de datos secundario de toohello de centro de datos principal de Hola o tooAzure (según el escenario de hello) y, a continuación, actualiza periódicamente las réplicas de Hola. Durante el planeamiento de la infraestructura, el diseño de red debe considerarse un potencial cuello de botella que puede evitar que cumpla los objetivos de RTO y RPO de la compañía.  

Los administradores planear toodeploy una solución de recuperación ante desastres, una de hello preguntas clave en sus mentes es la máquina virtual de hello sería accesible una vez completada la conmutación por error de Hola. ASR permite Hola administrador toochoose Hola red toowhich una máquina virtual sería tooafter conectado conmutación por error. Si el sitio primario de hello es Azure o es un sitio local administrado por un servidor VMM, a continuación, esto se consigue mediante la asignación de red. Obtenga más información sobre [asignación de red en la recuperación ante desastres de Azure tooAzure](site-recovery-network-mapping-azure-to-azure.md) y [asignación de red de VMM](site-recovery-network-mapping.md)


Al diseñar la red de hello para el sitio de recuperación de Hola, Administrador de hello tiene dos opciones:

* Utilice un intervalo de direcciones IP diferente para la red de hello en el sitio de recuperación. En este escenario Hola máquina virtual después de conmutación por error obtendrá una nueva dirección IP y el Administrador de hello tendría toodo una actualización DNS. 
* Use el mismo intervalo de direcciones IP para red de hello en el sitio de recuperación de Hola. En determinados escenarios que los administradores prefieran direcciones IP de tooretain Hola que tienen en el sitio principal de hello incluso después de la conmutación por error de Hola. En un escenario normal, un administrador tendría tooupdate Hola rutas tooindicate Hola nueva ubicación de direcciones IP de Hola. Pero, en el escenario de Hola donde se implementa una subred con Stretch entre Hola principal y los sitios de recuperación de hello, conservando las direcciones IP de Hola para las máquinas virtuales de Hola se convierte en una opción atractiva. Ajuste de una subred de una tooan de red local red de Azure entre dos redes de Azure o no es posible.  

Los administradores planear toodeploy una solución de recuperación ante desastres, una de hello preguntas clave en su cuenta es cómo las aplicaciones de Hola será accesible una vez completada la conmutación por error de Hola. Aplicaciones modernas casi siempre son dependientes de grado de toosome, a redes físicamente mover un servicio de un sitio tooanother representa un desafío de red. Hay dos formas principales de abordar este problema en las soluciones de recuperación ante desastres. Hola primer enfoque es toomaintain direcciones IP fijas. A pesar de servicios de hello mover y Hola servidores están en diferentes ubicaciones físicas de hospedaje, las aplicaciones tener configuración de dirección IP de hello con ellos toohello nueva ubicación. Hola segundo método implica completamente cambiar dirección IP de Hola durante la transición de hello en el sitio recuperado Hola. Cada enfoque tiene distintas variaciones de implementación, que se resumen a continuación.

Al diseñar la red de hello para el sitio de recuperación de Hola, Administrador de hello tiene dos opciones:

## <a name="option-1-retain-ip-addresses"></a>Opción 1: Conservar las direcciones IP
Desde una perspectiva de proceso de recuperación ante desastres, con direcciones IP fijas aparece tooimplement de método más fácil de toobe Hola, pero tiene un número de posibles desafíos que, en la práctica, harán Hola enfoque menos popular. Azure Site Recovery proporciona capacidad de hello tooretain direcciones IP de hello en todos los escenarios. Antes de que uno decide tooretain IP, se debe conceder pensamiento adecuado restricciones toohello impone en las capacidades de conmutación por error de Hola. Echemos un vistazo en factores de Hola que pueden ayudar a toomake que una decisión tooretain dirección IP, o no. Esto se puede realizar de dos maneras: mediante una subred estirada o mediante una conmutación por error de subred completa.

### <a name="stretched-subnet"></a>Subred estirada
Aquí subred Hola debe ponerse a disposición en principal y ubicaciones de recuperación ante desastres, al mismo tiempo. En otras palabras, esto significa puede mover un servidor y sus toohello otro sitio de configuración de IP (nivel 3) y red de hello enrutará nueva ubicación de hello tráfico toohello automáticamente. Esto es trivial toodeal con desde la perspectiva del servidor, pero tiene una serie de desafíos:

* Desde una perspectiva del nivel 2 (nivel de vínculo de datos) requerirá equipamiento de redes que pueda administrar una VLAN estirada, pero esto es cada vez menos problemático ya que en la actualidad está ampliamente disponible. problema de segundo y más difícil de Hello es mediante la expansión de hello dominio de error potencial de VLAN Hola se extiende sitios tooboth, básicamente se convierta en un único punto de error. Aunque es improbable que suceda, lo que ha ocurrido es que se ha iniciado una tormenta de difusión que se ha podido aislar. Hay distintas opiniones sobre este problema y unos han realizado muchas implementaciones correctas, mientras que otros han indicado que nunca implementarán esta tecnología.
* No es posible si está utilizando Microsoft Azure como sitio de recuperación ante desastres de Hola subred con Stretch.

### <a name="subnet-failover"></a>Conmutación por error de subred
Es ventajas tooimplement posibles subred conmutación por error tooobtain Hola de solución de subred Hola extendido se ha descrito anteriormente sin ajuste de subred de hello en varios sitios. Aquí, cualquier subred determinada estaría presente en el sitio 1 o en el sitio 2, pero nunca en ambos sitios simultáneamente. En orden toomaintain Hola espacio de direcciones IP en el caso de hello de una conmutación por error, es posible organizar tooprogrammatically para subredes Hola enrutador infraestructura toomove Hola desde un sitio tooanother. En un Hola de escenario de conmutación por error podría subredes movimiento con hello asociados máquinas virtuales protegidas. Hola principal inconveniente toothis consiste en caso de hello de un error tiene toomove Hola todo subred, que puede aceptar, pero puede afectar a las consideraciones de granularidad de conmutación por error de Hola.

Examinemos cómo una empresa ficticia denominada Contoso es capaz de tooreplicate su ubicación de recuperación de máquinas virtuales tooa al conmutar por error subred completa Hola. En primer lugar veremos cómo Contoso es capaz de toomanage sus subredes durante la replicación de máquinas virtuales entre dos local ubicaciones y, a continuación, analizaremos cómo subred conmutación por error funciona cuando [Azure se utiliza como sitio de recuperación ante desastres de hello](#failover-to-azure).

#### <a name="failover-from-on-premises-tooazure"></a>Conmutación por error de local tooAzure 
Azure Site Recovery (ASR) permite toobe Azure utilizado como un sitio de recuperación ante desastres para las máquinas virtuales.  

Examinemos un escenario en el que una compañía ficticia denominada Woodgrove Bank tiene una infraestructura local que hospeda su línea de aplicaciones empresariales y que hospeda sus aplicaciones móviles en Azure. La conectividad entre las máquinas virtuales de Woodgrove Bank en los servidores locales y de Azure se proporciona mediante una red privada virtual (VPN) de sitio a sitio (S2S) o mediante ExpressRoute. VPN de S2S permite la red virtual de Woodgrove Bank en Azure toobe ver como una extensión de Woodgrove Bank red local. Esta comunicación la habilita una VPN de S2S entre el borde de Woodgrove Bank y la red virtual de Azure. Ahora Woodgrove desea toouse ASR tooreplicate sus cargas de trabajo que ejecutan tooanother región Azure principal región de Azure. Esta opción satisface las necesidades de hello Woodgrove, que se desea una opción de recuperación ante desastres económica y es capaz de toostore datos en entornos de nube pública. Woodgrove tiene toodeal con aplicaciones y configuraciones que dependen de las direcciones IP codificado de forma rígida, por lo tanto, tienen una dirección IP de requisito tooretain para sus aplicaciones después por error a través de la región de tooanother en Azure.

Woodgrove ha decidido tooassign las direcciones IP de recursos de tooits del intervalo (172.16.1.0/24, 172.16.2.0/24) de dirección IP ejecuta en Azure.

Para Woodgrove toobe capaz de tooreplicate su tooAzure de máquinas virtuales mientras se conservan las direcciones IP de hello, una red Virtual de Azure debe toobe creado. Debe ser una extensión de la red local de Hola para que las aplicaciones puedan conmutación por error de hello local sitio tooAzure sin problemas. Azure permite tooadd sitio a sitio, así como point-to-site VPN conectividad toohello redes virtuales creadas en Azure. Al configurar la conexión de sitio a sitio, red de Azure le permite tooroute tráfico toohello local ubicación (Azure lo llama red local) solo si el intervalo de direcciones IP de hello es diferente de intervalo de direcciones IP de hello local porque Azure no compatibilidad con el ajuste de subredes.  Esto significa que si tiene un 192.168.1.0/24 subred local, no se puede agregar una red local 192.168.1.0/24 Hola red de Azure. Esto es lo esperado porque Azure no sabe que hay máquinas virtuales activas en la subred de Hola y esa subred Hola se está creando solo con fines de recuperación ante desastres. toobe toocorrectly puede redirigir el tráfico de red fuera de un subredes hello Azure en red de Hola y Hola de red local no debe estar en conflicto.

![Antes de la conmutación por error de la subred](./media/site-recovery-network-design/network-design7.png)

Antes de la conmutación por error

toohelp Woodgrove satisfacen sus requisitos empresariales, necesitamos hello tooimplement después de los flujos de trabajo:

* Crear una red adicional, permítanos llamar a red de recuperación, donde se podría crear máquinas virtuales de Hola se conmutó por error.
* tooensure que Hola IP para una máquina virtual se conserva después de una conmutación por error, vaya a toohello configurar pestaña en Propiedades de la máquina virtual, debe especificar Hola misma dirección IP que Hola VM tiene en el servidor local y, a continuación, haga clic en Guardar. Cuando se conmuta Hola VM, Azure Site Recovery asignará Hola proporcionada la máquina virtual de toohello IP.

![Propiedades de red](./media/site-recovery-network-design/network-design8.png)

Una vez que se desencadena la conmutación por error de Hola y hello las máquinas virtuales se crean en hello red de recuperación con la dirección IP de hello deseado, red de toothis de conectividad se puede establecer usando una [tooVnet conexión de red virtual](../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md). Si se requiere, esta acción puede ejecutarse mediante script.  Como se explicó en la sección anterior de hello acerca de la conmutación por error de subred, incluso en caso de hello de tooAzure de conmutación por error, las rutas habría toobe modificado correctamente tooreflect ese 192.168.1.0/24 ahora se movió tooAzure.

![Después de la conmutación por error de la subred](./media/site-recovery-network-design/network-design9.png)

Después de la conmutación por error

Si no tiene una red de Azure' ' como se muestra en figura Hola anterior. Puede crear una conexión de vpn de sitio toosite entre el 'Sitio primario' y 'Red de recuperación' después de la conmutación por error de Hola.  


#### <a name="failover-tooa-secondary-on-premises-site"></a>Conmutación por error tooa secundaria sitio local
Echemos un vistazo en un escenario donde desea conservar Hola IP de cada una de las máquinas virtuales de Hola y Hola de conmutación por error complete subred juntos. sitio primario de Hello tiene aplicaciones que se ejecutan en la subred 192.168.1.0/24. Cuando se produce la conmutación por error de hello, todas las máquinas virtuales de Hola que forman parte de esta subred conmutarán por error toohello sitio de recuperación y conservan sus direcciones IP. Rutas tendrá toobe modificado correctamente hechos de hello tooreflect que todas las máquinas virtuales de Hola que pertenecen toosubnet 192.168.1.0/24 ahora se han movido toohello sitio de recuperación.

Hola Hola de ilustración siguientes enruta entre sitio primario y sitio de recuperación, tercer sitio y el sitio primario y tercer sitio y el sitio de recuperación tendrá toobe modificado correctamente.

Hola siguientes imágenes muestran Hola antes Hola conmutación por error. Subred 192.168.0.1/24 está activo en hello sitio primario antes de la conmutación por error de hello y pasa a estar activo de hello sitio de recuperación después de la conmutación por error de Hola

![Antes de la conmutación por error](./media/site-recovery-network-design/network-design2.png)

Antes de la conmutación por error

Figura Hola siguiente muestra redes y subredes después de la conmutación por error.

![Después de la conmutación por error](./media/site-recovery-network-design/network-design3.png)

Después de la conmutación por error

En el sitio secundario es local y está utilizando un toomanage de servidor VMM, a continuación, al habilitar la protección para una máquina virtual específica, ASR asignará los recursos de red según toohello siguiendo el flujo de trabajo:

* ASR asigna una dirección IP para cada interfaz de red en la máquina virtual de Hola Hola grupo direcciones IP estáticas definido en red relevantes de Hola para cada instancia de System Center VMM.
* Si define el Administrador de Hola Hola misma IP de grupo para la red de hello en el sitio de recuperación de hello como de direcciones que asignaría red en el sitio principal de hello, al asignar ASR de máquina virtual de réplica de hello IP dirección toohello del grupo de direcciones IP de Hola de Hola Hola igual Dirección IP que el de la máquina virtual principal de Hola.  Hola IP está reservada en VMM pero no se establece como IP de conmutación por error en el host de Hyper-v de Hola. Failover IP en un host de Hyper-v se establece justo antes de la conmutación por error de Hola.


Si hello misma IP no está disponible, ASR asignaría alguna otra dirección IP disponible del grupo de direcciones IP de hello definido.

Después de hello que VM está habilitada para la protección puede usar después IP Hola de tooverify de script de ejemplo que se ha asignado la máquina virtual de toohello. Hola misma IP se establece como Failover IP y asignado toohello VM en tiempo de Hola de conmutación por error:

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

> [!NOTE]
> En el escenario de hello en las máquinas virtuales usa DHCP, administración de Hola de direcciones IP está completamente fuera de control de Hola de ASR. Un administrador ha tooensure que pueden actuar Hola DHCP atendiendo Hola direcciones IP del servidor en el sitio de recuperación de Hola de hello mismo rango que la del sitio primario de Hola.
>
>



## <a name="option-2-changing-ip-addresses"></a>Opción 2: Cambio de las direcciones IP
Este enfoque parece predominantes toobe hello en función de lo que hemos visto. Toma forma Hola del cambio de dirección IP de Hola de cada máquina virtual que está implicado en hello conmutación por error. Un inconveniente de este enfoque requiere Hola entrantes red too'learn' esa aplicación Hola que estaba en IPx está ahora en IPy. Aunque IPx y IPy son nombres lógicos, las entradas DNS suelen tienen toobe cambiado o vaciar a lo largo de la red de hello y las entradas en caché en las tablas de red tienen toobe actualizado o vaciar, por lo tanto, podría verse un tiempo de inactividad dependiendo de la infraestructura DNS de hello tiene ha configurado. Estos problemas se pueden mitigar mediante valores TTL bajos en caso de hello de aplicaciones de intranet y [Traffic Manager de Azure con ASR](http://azure.microsoft.com/blog/2015/03/03/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/) aplicaciones para internet basadas en

### <a name="changing-hello-ip-addresses---illustration"></a>Cambiar las direcciones IP de hello - ilustración
Echemos un vistazo a un escenario de Hola donde piensa toouse diferentes direcciones IP en sitios de recuperación de Hola y Hola principal. En el siguiente ejemplo de Hola también tenemos un tercer sitio desde donde se pueden tener acceso a las aplicaciones de hello hospedadas en el sitio principal o de recuperación.

![Otra dirección IP: antes de la conmutación por error](./media/site-recovery-network-design/network-design10.png)


En la imagen de hello anterior hay algunas aplicaciones hospedadas en la subred de 192.168.1.0/24 de subred en el sitio principal de Hola y han sido configurado toocome seguridad en el sitio de recuperación de hello en subred 172.16.1.0/24 después de una conmutación por error. Las rutas de red/conexiones de VPN se han configurado correctamente de forma que los tres sitios son accesibles entre sí.

Como imagen de Hola a continuación se muestra, después de conmutar por error una o más aplicaciones, se restaurará en la subred de la recuperación de Hola. En este caso no somos toofailover restringida Hola toda subred en hello mismo tiempo. Ningún cambio es rutas de red o VPN tooreconfigure necesarios. Una conmutación por error y algunas actualizaciones de DNS garantizarán que las aplicaciones seguirán siendo accesibles. Si Hola DNS es actualizaciones dinámicas tooallow configurado máquinas virtuales de hello registraría a sí mismos mediante Hola nueva IP una vez que se inician después de una conmutación por error.

![Otra dirección IP: después de la conmutación por error](./media/site-recovery-network-design/network-design11.png)


Después de máquina virtual de réplica de Hola de conmutación por error puede tener una dirección IP que no es igual Hola como dirección IP de saludo de la máquina virtual principal de Hola. Máquinas virtuales se actualizará el servidor DNS de Hola que están utilizando después de que se inicien. Las entradas DNS tienen normalmente toobe cambiado o vaciar a lo largo de la red de Hola y las entradas en caché en las tablas de red tienen toobe actualizado o vacía, por lo que no es raro que toobe enfrentan con tiempo de inactividad mientras realicen estos cambios de estado. Este problema se puede mitigar con las acciones siguientes:

* Utilizando valores de TTL bajos para las aplicaciones de intranet.
* Utilizando el Administrador de tráfico de Azure con ASR para aplicaciones basadas en Internet.
* Con hello siguientes script dentro de la recuperación del plan tooupdate Hola servidor DNS tooensure oportuna actualización (script de Hola no es necesario si se configura el registro DNS dinámico de Hola)

        param(
        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord

### <a name="changing-hello-ip-addresses--dr-tooazure"></a>Variación hello las direcciones IP: tooAzure de recuperación ante desastres
Hola [configuración de infraestructura de red de Microsoft Azure como un sitio de recuperación ante desastres](http://azure.microsoft.com/blog/2014/09/04/networking-infrastructure-setup-for-microsoft-azure-as-a-disaster-recovery-site/) entrada de blog explica cómo toosetup Hola requiere la infraestructura de red de Azure para conservar las direcciones IP no es un requisito. Empiece con los que describe la aplicación hello y, a continuación, busque en cómo toosetup redes locales y en Azure y, a continuación, finalizando con cómo toodo una conmutación por error de prueba y una conmutación por error planeada.

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información acerca de](site-recovery-vmm-to-vmm.md#prepare-for-network-mapping) cómo Site Recovery asigna redes de origen y de destino cuando un servidor VMM se sitio primario de hello toomanage usado.
