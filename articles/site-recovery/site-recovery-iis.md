---
title: "aaaReplicate un IIS de varios niveles según la aplicación web con Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo describe cómo tooreplicate IIS web máquinas virtuales de granja de servidores con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: nisoneji
ms.openlocfilehash: 1974265b3cb05f6dc57049876306d2e08424bb97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-iis-based-web-application-using-azure-site-recovery"></a>Replicación de una aplicación web basada en IIS de niveles múltiples con Azure Site Recovery

## <a name="overview"></a>Información general


Software de la aplicación es motor Hola de productividad empresarial en una organización. En una organización, puede haber diversas aplicaciones web con diferentes propósitos. Algunas de ellas, como las aplicaciones financieras, los programas de procesamiento de nóminas y los sitios web destinados a los clientes, pueden resultar extremadamente cruciales para la organización. Será importante para hello organización toohave les seguridad y en funcionamiento con pérdida de tooprevent de todas las horas de productividad y más importante evitar cualquier imagen de marca de daños toohello de organización de Hola.

Las aplicaciones críticas web normalmente se configuran como aplicaciones de varios niveles con web hello, base de datos y aplicaciones en distintos niveles. Además de repartida entre distintos niveles, las aplicaciones de Hola también pueden usar varios servidores en cada capa tooload equilibrar Hola del tráfico. Además, las asignaciones de hello entre distintos niveles y en el servidor web de hello pueden basarse en direcciones IP estáticas. En la conmutación por error, algunas de estas asignaciones debe toobe actualizado, especialmente, si tiene varios sitios Web configurados en el servidor web de Hola. En el caso de aplicaciones web mediante SSL, los enlaces de certificados tendrá toobe actualizado.

Métodos de recuperación en función de replicación no tradicionales implican la copia de seguridad de varios archivos de configuración, configuración del registro, enlaces, componentes personalizados (COM o. NET), contenido y también certificados y recuperar archivos de Hola a través de un conjunto de pasos manuales. Estas técnicas resultan engorrosas, suelen generar errores y no son escalables. Es, por ejemplo, fácilmente posible tooforget copia de seguridad de certificados y se quedaría sin opción pero toobuy nuevos certificados de servidor hello después de la conmutación por error.

Una solución de recuperación ante desastres conveniente, debe permitir que el modelo de planes de recuperación alrededor de Hola por encima de arquitecturas de aplicación compleja y también tienen Hola capacidad tooadd personalizar pasos toohandle aplicación asignaciones entre los distintos niveles, por lo que proporciona un con un solo clic que captura la solución en caso de hello de un desastre iniciales tooa reducir el RTO.


Este artículo describe cómo tooprotect un servicio de IIS según la aplicación web utilizando un [Azure Site Recovery](site-recovery-overview.md). Este artículo explica las prácticas recomendadas para la replicación de un nivel tres basados en IIS tooAzure de aplicación web, cómo se puede hacer una exploración de recuperación ante desastres, y cómo se tooAzure de aplicación Hola de conmutación por error.


## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que comprende siguiente hello:

1. [Replicar una máquina virtual tooAzure](site-recovery-vmware-to-azure.md)
1. Cómo demasiado[el diseño de una red de recuperación](site-recovery-network-design.md)
1. [Realizar una tooAzure de conmutación por error de prueba](./site-recovery-test-failover-to-azure.md)
1. [Realizar una conmutación por error tooAzure](site-recovery-failover.md)
1. Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)
1. Cómo demasiado[replicar SQL Server](site-recovery-sql.md)

## <a name="deployment-patterns"></a>Modelos de implementación
Una aplicación web IIS según sigue normalmente uno de los siguientes patrones de implementación de Hola:

**Modelo de implementación 1 ** Granja de servidores web de IIS con Enrutamiento de solicitud de aplicaciones (ARR), IIS Server y Microsoft SQL Server.

![Modelo de implementación](./media/site-recovery-iis/deployment-pattern1.png)

**Modelo de implementación 2** Granja de servidores web basada IIS con Enrutamiento de solicitud de aplicaciones (ARR), IIS Server, servidor de aplicaciones y Microsoft SQL Server.


![Modelo de implementación](./media/site-recovery-iis/deployment-pattern2.png)

## <a name="site-recovery-support"></a>Compatibilidad de Site Recovery

Se utilizaron para el propósito de Hola de creación de este artículo las máquinas virtuales VMware con el servidor IIS versión 7.5 en Windows Server 2012 R2 Enterprise. Como la replicación de recuperación de sitios es independiente de la aplicación, se proporcionan recomendaciones de hello aquí son toohold esperado en los escenarios siguientes también y otra versión de IIS.

### <a name="source-and-target"></a>Origen y destino

**Escenario** | **sitio secundario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sí | Sí
**VMware** | Sí | Sí
**Servidor físico** | No | Sí

## <a name="replicate-virtual-machines"></a>Replicación de máquinas virtuales

Siga [esta guía](site-recovery-vmware-to-azure.md) toostart replicar tooAzure de máquinas virtuales de granja de servidores web IIS de hello todos los.

Si está usando una dirección IP estática y luego especifique Hola IP que desee Hola tootake de máquina virtual en hello [ **IP de destino** ](./site-recovery-replicate-vmware-to-azure.md#view-and-manage-vm-properties) en configuración de red y proceso.

![IP de destino](./media/site-recovery-active-directory/dns-target-ip.png)


## <a name="creating-a-recovery-plan"></a>Creación de un plan de recuperación

Un plan de recuperación permite secuenciación Hola conmutación por error de distintos niveles de una aplicación de varios niveles, por lo tanto, mantener la coherencia de la aplicación. Siga Hola pasos siguientes al crear un plan de recuperación para una aplicación web de varios niveles.  [Aprenda más sobre la creación de un plan de recuperación](./site-recovery-create-recovery-plans.md).

### <a name="adding-virtual-machines-toofailover-groups"></a>Agregar grupos de toofailover de máquinas virtuales
Una aplicación típica de web IIS de varios nivel constará de un nivel de base de datos con máquinas virtuales, nivel de web Hola constituida por un servidor IIS y una capa de aplicación de SQL. Agregar todas estas máquinas virtuales toodifferent de grupo basándose en el nivel que a continuación. [Aprenda más sobre cómo personalizar los planes de recuperación](site-recovery-runbook-automation.md#customize-the-recovery-plan).

1. Cree un plan de recuperación. Agregar base de datos máquinas virtuales Hola capa en el grupo 1 tooensure que están última cierre y vuelva a la primera.

1. Agregar máquinas de virtuales de nivel de aplicación de hello en grupo 2, que se incorporan después de que se ha incluido el nivel de base de datos de hello.

1. Agregar hello web niveles las máquinas virtuales en el grupo 3, que se incorporan después de capa de aplicación Hola se ha incluido.

1. Agregar máquinas virtuales de equilibrio de carga en el grupo 4, que se incorporan después de que se ha incluido el nivel de web Hola.


### <a name="adding-scripts-toohello-recovery-plan"></a>Agregar plan de recuperación de toohello de secuencias de comandos
Puede que tenga toodo algunas operaciones en máquinas virtuales de Azure post pruebas de conmutación por error y conmutación por error toomake IIS web granja función hello correctamente. Puede automatizar la operación de conmutación por error de post hello como la actualización de la entrada DNS, cambiar el enlace del sitio, cambios en la cadena de conexión agregando correspondientes a los scripts en el plan de recuperación de hello como sigue. [Aprenda más sobre la incorporación de scripts al plan de recuperación](./site-recovery-create-recovery-plans.md#add-scripts).

#### <a name="dns-update"></a>Actualización de DNS
Si Hola DNS está configurado para la actualización dinámica de DNS, a continuación, máquinas virtuales normalmente se haya actualizado Hola DNS con la dirección IP de hello nuevo una vez que se inician. Si desea que tooadd un tooupdate paso explícito DNS con hello nuevas direcciones IP de máquinas virtuales de hello, a continuación, agregue esto [tooupdate IP en DNS de script](https://aka.ms/asr-dns-update) como una acción posterior en grupos de planes de recuperación.  

#### <a name="connection-string-in-an-applications-webconfig"></a>Cadena de conexión del archivo web.config de una aplicación
cadena de conexión de Hello especifica la base de datos de Hola Hola sitio web se comunica con.

Si cadena de conexión de hello lleva el nombre de Hola de máquina virtual de base de datos de hello, realizar ningún paso adicional será necesario posterior conmutación por error y se podrán aplicación hello tooautomatically comunicarse toohello base de datos. Además, si se mantiene la dirección IP de hello para la máquina virtual de base de datos de hello, no será necesaria la cadena de conexión de tooupdate Hola. Si la cadena de conexión de hello hace referencia la máquina virtual toohello base de datos a través de una dirección IP, será necesario toobe actualizado posterior conmutación por error. Por ejemplo, Hola por debajo de la cadena de conexión apunta toohello DB con la dirección IP 127.0.1.2

        <?xml version="1.0" encoding="utf-8"?>
        <configuration>
        <connectionStrings>
        <add name="ConnStringDb1" connectionString="Data Source= 127.0.1.2\SqlExpress; Initial Catalog=TestDB1;Integrated Security=False;" />
        </connectionStrings>
        </configuration>

Puede actualizar la cadena de conexión de hello en el nivel web agregando [secuencia de comandos de actualización de conexión de IIS](https://aka.ms/asr-update-webtier-script-classic) después de grupo 3 en el plan de recuperación de Hola.

#### <a name="site-bindings-for-hello-application"></a>Enlaces de sitios para la aplicación hello
Cada sitio consta de información que incluye el tipo de saludo de enlace, la dirección IP de hello en qué Hola servidor IIS escucha las solicitudes de toohello de sitio de hello, número de puerto de Hola y nombres de host de hello para el sitio de Hola de enlace. En tiempo de presentación de una conmutación por error, estos enlaces necesite toobe actualiza si hay un cambio en la dirección IP de hello asociado con ellos.

> [!NOTE]
>
> Si se ha marcado 'all unassigned' hello enlace de sitio como en el siguiente ejemplo de Hola, no será necesario tooupdate esta conmutación por error de enlace post. Además, si dirección IP de hello asociada con un sitio no se cambia post conmutación por error, el enlace del sitio de hello necesita no estén actualizado (retención de dirección IP de hello depende de la arquitectura de red de Hola y subredes asignan toohello sitios principal y de recuperación y, por lo que pueden o no sea factible para su organización).

![Enlace SSL](./media/site-recovery-iis/sslbinding.png)

Si la dirección IP de Hola que haya asociado con un sitio, deberá tooupdate todos los enlaces de sitio con la dirección IP de la nueva Hola. Puede agregar [script de actualización de nivel de Web de IIS](https://aka.ms/asr-web-tier-update-runbook-classic) después de grupo 3 en enlaces de sitios de recuperación plan toochange Hola.


#### <a name="update-load-balancer-ip-address"></a>Actualización de la dirección IP del equilibrador de carga
Si la máquina virtual de enrutamiento de solicitud de aplicación, agregue [secuencia de comandos de conmutación por error de IIS ARR](https://aka.ms/asr-iis-arrtier-failover-script-classic) después de la dirección IP de grupo 4 tooupdate Hola.

#### <a name="hello-ssl-cert-binding-for-an-https-connection"></a>enlace de certificado SSL de Hola para una conexión https
Sitios Web puede tener un certificado SSL asociado que ayuda a garantizar una comunicación segura entre el servidor Web de Hola y explorador del usuario de Hola. Si el sitio Web de hello tiene una conexión https y una dirección IP de https asociado sitio enlace toohello Hola del servidor de IIS con un enlace de certificado SSL, un nuevo enlace de sitio deberá toobe agregado para el certificado de hello con hello IP de la máquina virtual IIS de hello registrar conmutación por error.

se pueden emitir certificados SSL de Hello en:

a) nombre de dominio completo de Hola del sitio Web de Hola<br>
b) nombre de hello del servidor de Hola<br>
c) un certificado comodín con nombre de dominio de Hola<br>
d) una dirección IP: si se emite certificados SSL de hello en IP Hola Hola del servidor de IIS, otro toobe de necesidades de certificado SSL emitido en la dirección IP de Hola de hello servidor IIS en el sitio de Azure de Hola y un enlace de SSL adicional para este certificado será necesario toobe creado. Por lo tanto, es aconsejable toonot un certificado SSL emitido en IP. Esta es una opción que apenas se usa y que pronto quedará en desuso a tenor de los nuevos cambios de CA/Browser Forum.

#### <a name="update-hello-dependency-between-hello-web-and-hello-application-tier"></a>Dependencia de Hola de actualización entre web de Hola y de capa de aplicación Hola
Si tiene una dependencia de aplicación específico basada en dirección IP de Hola de máquinas virtuales de hello, necesita tooupdate esta conmutación por error de dependencia post.

## <a name="doing-a-test-failover"></a>Realización de una conmutación por error de prueba
Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.

1.  Vaya tooAzure portal y seleccione el almacén del servicio de recuperación.
1.  Haga clic en el plan de recuperación de hello creado para la granja de servidores de web IIS.
1.  Haga clic en 'Probar conmutación por error'.
1.  Seleccione el punto de recuperación y el proceso de conmutación por error de prueba de red virtual de Azure toostart Hola.
1.  Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.
1.  Después de completar las validaciones de hello, puede seleccionar 'Validaciones completar' y entorno de conmutación por error de prueba de Hola se borrarán.

## <a name="doing-a-failover"></a>Realización de una conmutación por error
Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.

1.  Vaya tooAzure portal y seleccione el almacén del servicio de recuperación.
1.  Haga clic en el plan de recuperación de hello creado para la granja de servidores de web IIS.
1.  Haga clic en 'Conmutación por error'.
1.  Seleccione el proceso de conmutación por error de Hola de toostart de punto de recuperación.

## <a name="next-steps"></a>Pasos siguientes
Puede obtener más información sobre la [replicación de otras aplicaciones](site-recovery-workload.md) a través de Site Recovery.
