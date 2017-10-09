---
title: "una aplicación de SharePoint de varios niveles con Azure Site Recovery aaaReplicate | Documentos de Microsoft"
description: "Este artículo se describe cómo tooreplicate una aplicación de SharePoint de varios niveles con capacidades de Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sutalasi
ms.openlocfilehash: d856034ac2a3c95b0c1f0cf85e62c4e7a5a3210f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-sharepoint-application-for-disaster-recovery-using-azure-site-recovery"></a>Replicación de una aplicación de SharePoint de niveles múltiples para una recuperación ante desastres mediante Azure Site Recovery | Microsoft Docs

Este artículo se describen en detalle cómo tooprotect una aplicación de SharePoint con [Azure Site Recovery](site-recovery-overview.md).


## <a name="overview"></a>Información general

Microsoft SharePoint es una aplicación eficaz que puede ayudar a un grupo o departamento a organizarse, colaborar y compartir información. SharePoint proporciona portales de intranet, administración de archivos y documentos, colaboración, redes sociales, extranets, sitios web, motor de búsqueda Enterprise Search e inteligencia empresarial. También dispone de integración de sistemas, integración de procesos y funcionalidades de automatización de flujos de trabajo. Normalmente, las organizaciones consideran como una nivel 1 aplicación confidencial toodowntime y pérdida de datos.

En la actualidad, la aplicación Microsoft SharePoint no tiene integrada ninguna funcionalidad de recuperación ante desastres. Independientemente del tipo hello y la escala de un desastre, la recuperación implica usar Hola de un centro de datos en espera que se puede recuperar la granja de servidores de Hola a. Centros de datos en espera se requieren en escenarios donde no se pueden recuperar los sistemas locales de redundancia y copias de seguridad de interrupción de hello en el centro de datos principal de Hola.

Una solución de recuperación ante desastres conveniente debe permitir que el modelo de planes de recuperación alrededor de arquitecturas de aplicación compleja de hello como SharePoint. También debe tener Hola capacidad tooadd personalizar pasos toohandle aplicación asignaciones entre los distintos niveles y, por tanto, proporcionar un solo clic, conmutación por error con un RTO inferior en caso de hello de un desastre.

Este artículo se describen en detalle cómo tooprotect una aplicación de SharePoint con [Azure Site Recovery](site-recovery-overview.md). Este artículo explica las prácticas recomendadas para la replicación de una tooAzure de aplicación de SharePoint de tres niveles, cómo se puede hacer una exploración de recuperación ante desastres y cómo puede tooAzure de aplicación Hola de conmutación por error.

Puede ver hello debajo de vídeo acerca de cómo recuperar un tooAzure de aplicación de varios niveles.

> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/Disaster-Recovery-of-load-balanced-multi-tier-applications-using-Azure-Site-Recovery/player]


## <a name="prerequisites"></a>Requisitos previos

Antes de empezar, asegúrese de que comprende siguiente hello:

1. [Replicar una máquina virtual tooAzure](site-recovery-vmware-to-azure.md)
2. Cómo demasiado[el diseño de una red de recuperación](site-recovery-network-design.md)
3. [Realizar una tooAzure de conmutación por error de prueba](site-recovery-test-failover-to-azure.md)
4. [Realizar una conmutación por error tooAzure](site-recovery-failover.md)
5. Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)
6. Cómo demasiado[replicar SQL Server](site-recovery-sql.md)

## <a name="sharepoint-architecture"></a>Arquitectura de SharePoint

SharePoint se puede implementar en uno o más servidores usando topologías por niveles y roles de servidor tooimplement un diseño de granja de servidores que satisfaga determinados objetivos. Una granja de servidores de SharePoint típica de gran tamaño y alta demanda que admita un número elevado de usuarios simultáneos y elementos de contenido utiliza la agrupación de servicios como parte de su estrategia de escalabilidad. Este enfoque implica ejecutar servicios en servidores dedicados, agrupando estos servicios y, a continuación, escalar horizontalmente los servidores de Hola como un grupo. Hello topología siguiente ilustra el servicio de Hola y agrupaciones de servidores para una granja de servidores de SharePoint de tres niveles. Consulte tooSharePoint documentación y las arquitecturas de línea de producto para obtener instrucciones detalladas sobre diferentes topologías de SharePoint. Encontrará más detalles sobre la implementación de SharePoint 2013 en [este documento](https://technet.microsoft.com/en-us/library/cc303422.aspx).



![Modelo de implementación 1](./media/site-recovery-sharepoint/sharepointarch.png)


## <a name="site-recovery-support"></a>Compatibilidad de Site Recovery

Para elaborar este artículo, se utilizaron máquinas virtuales de VMware con Windows Server 2012 R2 Enterprise. Se utilizaron SharePoint 2013 Enterprise y SQL server 2014 Enterprise. Replicación de Site Recovery sea independiente de la aplicación, proporcionan recomendaciones de hello aquí son toohold esperado en para así los escenarios siguientes.

### <a name="source-and-target"></a>Origen y destino

**Escenario** | **sitio secundario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sí | Sí
**VMware** | Sí | Sí
**Servidor físico** | Sí | Sí

### <a name="sharepoint-versions"></a>Versiones de SharePoint
se admite Hola después de las versiones de servidor de SharePoint.

* SharePoint Server 2013 Standard
* SharePoint Server 2013 Enterprise
* SharePoint Server 2016 Standard
* SharePoint Server 2016 Enterprise

### <a name="things-tookeep-in-mind"></a>Tookeep de cosas en cuenta

Si está utilizando un clúster basado en el disco compartido como cualquier nivel de la aplicación y no podrá ser tooreplicate de replicación de Site Recovery toouse capaz de esas máquinas virtuales. Puede usar replicación nativa proporcionada por la aplicación hello y, a continuación, usar un [plan de recuperación](site-recovery-create-recovery-plans.md) toofailover todas las capas.

## <a name="replicating-virtual-machines"></a>Replicación de máquinas virtuales

Siga [esta guía](site-recovery-vmware-to-azure.md) toostart replicar hello tooAzure de máquina virtual.

* Una vez completada la replicación de hello, asegúrese de que vaya tooeach virtual machine de cada capa y seleccione el mismo conjunto de disponibilidad en ' replicadas elemento > Configuración > Propiedades > de proceso y de red '. Por ejemplo, si el nivel web tiene 3 máquinas virtuales, asegúrese de hello todos los 3 máquinas virtuales están configurados toobe parte del mismo conjunto de disponibilidad en Azure.

    ![Configuración de conjuntos de disponibilidad](./media/site-recovery-sharepoint/select-av-set.png)

* Para obtener instrucciones sobre la protección de Active Directory y DNS, consulte demasiado[proteger Active Directory y DNS](site-recovery-active-directory.md) documento.

* Para obtener instrucciones sobre la protección de nivel de base de datos que se ejecuta en SQL server, consulte demasiado[proteger SQL Server](site-recovery-active-directory.md) documento.

## <a name="networking-configuration"></a>Configuración de red

### <a name="network-properties"></a>Propiedades de red

* Hello aplicación y las máquinas virtuales de nivel de Web, configurar configuración de red en el portal de Azure para que las máquinas virtuales de Hola obtener toohello adjunto red de recuperación ante desastres apropiado después de la conmutación por error.

    ![Selección de la red](./media/site-recovery-sharepoint/select-network.png)


* Si usa una dirección IP estática, a continuación, especifique la IP de Hola que desee Hola tootake de máquina virtual en hello **IP de destino** campo

    ![Configuración de direcciones IP estáticas](./media/site-recovery-sharepoint/set-static-ip.png)

### <a name="dns-and-traffic-routing"></a>Enrutamiento de tráfico y DNS

Para orientado a sitios, internet [crear un perfil de Traffic Manager del tipo 'Priority'](../traffic-manager/traffic-manager-create-profile.md) Hola suscripción de Azure. Y, a continuación, configurar el perfil de DNS y el Administrador de tráfico en hello siguiente manera.


| **Where** | **Origen** | **Destino**|
| --- | --- | --- |
| DNS público | DNS público para sitios de SharePoint <br/><br/> Por ejemplo: sharepoint.contoso.com | Administrador de tráfico <br/><br/> contososharepoint.trafficmanager.net |
| DNS local | sharepointonprem.contoso.com | Dirección IP pública en hello granja local |


Hola perfil de Traffic Manager, [crear puntos de conexión principal y de recuperación de hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md). Usar extremo externo hello para el extremo local y la dirección IP pública para el extremo de Azure. Comprobar si prioridad Hola está establecido el punto de conexión mayor tooon local.

Host de una página de prueba en un puerto específico (por ejemplo, 800) en el nivel de web de SharePoint de hello en orden para Traffic Manager tooautomatically detectar conmutación por error de publicación de disponibilidad. Se trata de una solución alternativa en caso de que no se puede habilitar la autenticación anónima en alguno de los sitios de SharePoint.

[Configurar perfil de Traffic Manager de hello](../traffic-manager/traffic-manager-configure-priority-routing-method.md) con hello por debajo de la configuración.

* Método de enrutamiento: Prioridad
* DNS tiempo toolive (TTL) - 30 ' segundos'
* Configuración del monitor del punto de conexión: Si se puede habilitar la autenticación anónima, puede proporcionar un punto de conexión de sitio web específico. También puede usar una página de prueba en un puerto específico (por ejemplo, 800).

## <a name="creating-a-recovery-plan"></a>Creación de un plan de recuperación

Un plan de recuperación permite secuenciación Hola conmutación por error de distintos niveles de una aplicación de varios niveles, por lo tanto, mantener la coherencia de la aplicación. Siga Hola pasos siguientes al crear un plan de recuperación para una aplicación web de varios niveles. [Aprenda más sobre la creación de un plan de recuperación](site-recovery-runbook-automation.md#customize-the-recovery-plan).

### <a name="adding-virtual-machines-toofailover-groups"></a>Agregar grupos de toofailover de máquinas virtuales

1. Crear un plan de recuperación Hola agregar aplicaciones y las máquinas virtuales de nivel de Web.
2. Haga clic en 'Personalizar' toogroup hello las máquinas virtuales. De forma predeterminada, todas las máquinas virtuales forman parte del grupo 1.

    ![Personalizar RP](./media/site-recovery-sharepoint/rp-groups.png)

3. Cree otro grupo (grupo 2) y mover el nivel de Web de hello las máquinas virtuales en el nuevo grupo de Hola. Las máquinas virtuales de nivel de aplicación deben formar parte del grupo 1, mientras que las máquinas virtuales de nivel web deben formar parte del grupo 2. Se trata de tooensure que Hola aplicación arrancan las máquinas virtuales del nivel primero, seguido por máquinas virtuales del nivel de Web.


### <a name="adding-scripts-toohello-recovery-plan"></a>Agregar plan de recuperación de toohello de secuencias de comandos

Puede implementar secuencias de comandos de Azure Site Recovery Hola suelen usada en su cuenta de automatización botón hello 'Implementar tooAzure' a continuación. Cuando se utiliza cualquier secuencia de comandos publicado, asegúrese de que seguir instrucciones hello en el script de Hola.

[![Implementar tooAzure](https://azurecomcdn.azureedge.net/mediahandler/acomblog/media/Default/blog/c4803408-340e-49e3-9a1f-0ed3f689813d.png)](https://aka.ms/asr-automationrunbooks-deploy)

1. Agregar un script de acción previa too'Group 1' toofailover SQL grupo de disponibilidad. Usar script de 'ASR-SQL-FailoverAG' hello publicado en los scripts de ejemplo de Hola. Asegúrese de seguir las instrucciones de hello en el script de Hola y realizar cambios de hello necesario en el script de Hola adecuadamente.

    ![Paso 1 para agregar el script AG](./media/site-recovery-sharepoint/add-ag-script-step1.png)

    ![Paso 2 para agregar el script AG](./media/site-recovery-sharepoint/add-ag-script-step2.png)

2. Agregue un tooattach de script de acción de entrada de un equilibrador de carga en hello conmutado por error máquinas virtuales del nivel de Web (grupo 2). Usar script de 'ASR AddSingleLoadBalancer' hello publicado en los scripts de ejemplo de Hola. Asegúrese de seguir las instrucciones de hello en el script de Hola y realizar cambios de hello necesario en el script de Hola adecuadamente.

    ![Paso 1 para agregar el script LB](./media/site-recovery-sharepoint/add-lb-script-step1.png)

    ![Paso 2 para agregar el script LB](./media/site-recovery-sharepoint/add-lb-script-step2.png)

3. Agregar un paso manual tooupdate Hola DNS registros toopoint toohello nueva granja de servidores en Azure.

    * En sitios orientados a Internet no se requieren las actualizaciones DNS son posteriores a la conmutación por error. Siga los pasos de hello descritos en hello 'Guía de red' sección tooconfigure Traffic Manager. Si Hola perfil de Traffic Manager se ha configurado como se describe en la sección anterior de hello, agregar un puerto ficticio (800 en el ejemplo de Hola) tooopen de secuencia de comandos en Hola VM de Azure.

    * Para los sitios internos orientados al público, agregar IP de equilibrador de carga de paso manual tooupdate Hola DNS toopoint registros toohello nueva Web capa la máquina virtual.

4. Agregar una aplicación de búsqueda de toorestore paso manual desde una copia de seguridad o iniciar un nuevo servicio de búsqueda.

5. Para restaurar la aplicación de servicio de búsqueda desde una copia de seguridad, siga los pasos indicados a continuación.

    * Este método supone que se realizó una copia de seguridad de la aplicación de servicio de búsqueda de hello antes del evento grave hello y esa copia de seguridad de hello está disponible en el sitio de recuperación ante desastres de Hola.
    * Esto puede lograrse fácilmente programar copia de seguridad de hello (por ejemplo, una vez al día) y usando una copia de seguridad de hello tooplace de procedimiento en el sitio de recuperación ante desastres de Hola. Los procedimientos de copia pueden incluir programas con scripts, como AzCopy (Azure Copy), o la configuración de DFSR (replicación de servicios de archivos distribuida).
    * Ahora que Hola SharePoint granja está ejecutando, vaya Hola Administración Central, 'Copia de seguridad y restauración' y seleccione restauración. restauración Hello interroga ubicación de copia de seguridad de hello especificada (puede que tenga valor de hello tooupdate). Seleccione la copia de seguridad de aplicación de servicio de búsqueda de hello le gustaría toorestore.
    * Se restaura la búsqueda. Tenga en cuenta que Hola restauración espera toofind Hola misma topología (el mismo número de servidores) y las mismas unidad de disco duro letras toothose servidores asignados. Para obtener más información, consulte el documento [Restaurar las aplicaciones de servicio de búsqueda en SharePoint 2013](https://technet.microsoft.com/library/ee748654.aspx).


6. Para iniciar con una nueva aplicación de servicio de búsqueda, siga los pasos indicados a continuación.

    * Este método supone que una copia de seguridad de base de datos de "Administración de búsqueda" hello está disponible en el sitio de recuperación ante desastres de Hola.
    * Puesto que hello otras bases de datos de aplicación de servicio de búsqueda no se replican, deben toobe vuelve a crear. por lo tanto, toodo navegue tooCentral administración y eliminar Hola aplicación de servicio de búsqueda. En todos los servidores que Hola host índice de búsqueda, elimine los archivos de índice de Hola.
    * Hola volver a crear la aplicación de servicio de búsqueda y, por lo vuelve a crear las bases de datos de Hola. Se recomienda toohave una secuencia de comandos preparada que vuelve a crea esta aplicación de servicio ya que no es posible tooperform todas las acciones a través de hello GUI. Por ejemplo, ubicación de unidad de índice de Hola y configuración de la topología de búsqueda de hello son sólo es posible mediante el uso de cmdlets de PowerShell de SharePoint. Use el cmdlet de Windows PowerShell de hello SPEnterpriseSearchServiceApplication de restauración y especifique Hola trasvase de registros y de base de datos de administración de búsqueda, Search_Service__DB replicada. Este cmdlet ofrece configuración de búsqueda de hello, esquema, propiedades administradas, reglas y orígenes y crea un conjunto predeterminado de hello otros componentes.
    * Una vez hello que tiene la aplicación de servicio de búsqueda se volverá a crear, debe iniciar un rastreo completo para cada Hola de toorestore servicio de búsqueda de origen de contenido. Perder cierta información de análisis de hello local granja de servidores, como recomendaciones para la búsqueda.

7. Una vez completados todos los pasos de hello, Guardar plan de recuperación de Hola y plan de recuperación final Hola tendrá un aspecto similar a siguiente.

    ![RP guardado](./media/site-recovery-sharepoint/saved-rp.png)

## <a name="doing-a-test-failover"></a>Realización de una conmutación por error de prueba
Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.

1.  Vaya tooAzure portal y seleccione el almacén del servicio de recuperación.
2.  Haga clic en el plan de recuperación de hello creado para la aplicación de SharePoint.
3.  Haga clic en 'Probar conmutación por error'.
4.  Seleccione el punto de recuperación y el proceso de conmutación por error de prueba de red virtual de Azure toostart Hola.
5.  Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.
6.  Una vez validaciones de hello están completadas, puede hacer clic en 'Limpieza de conmutación por error de prueba' en el plan de recuperación de Hola y se limpia el entorno de conmutación por error de prueba de Hola.

Para obtener instrucciones sobre cómo realizar la conmutación por error para AD y DNS, consulte demasiado[probar consideraciones de conmutación por error para AD y DNS](site-recovery-active-directory.md#test-failover-considerations) documento.

Para obtener instrucciones sobre cómo realizar la conmutación por error de SQL siempre en grupos de disponibilidad, consulte demasiado[realizando probar conmutación por error de SQL Server Always On](site-recovery-sql.md#steps-to-do-a-test-failover) documento.

## <a name="doing-a-failover"></a>Realización de una conmutación por error
Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.

1.  Vaya tooAzure portal y seleccione el almacén de servicios de recuperación.
2.  Haga clic en el plan de recuperación de hello creado para la aplicación de SharePoint.
3.  Haga clic en 'Conmutación por error'.
4.  Seleccione el proceso de conmutación por error de Hola de toostart de punto de recuperación.

## <a name="next-steps"></a>Pasos siguientes
Puede obtener más información sobre la [replicación de otras aplicaciones](site-recovery-workload.md) a través de Site Recovery.
