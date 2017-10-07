---
title: "una implementación de Dynamics AX de varios nivel con Azure Site Recovery aaaReplicate | Documentos de Microsoft"
description: "Este artículo se describe cómo tooreplicate y proteger con Azure Site Recovery de Dynamics AX"
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a>Replicación de una aplicación Dynamics AX de niveles múltiples mediante Azure Site Recovery

## <a name="overview"></a>Información general


Microsoft Dynamics AX es una solución ERP más popular de hello entre el proceso de toostandardized de las empresas en diferentes ubicaciones, administrar recursos y simplificar el cumplimiento. Considerando las aplicación hello es organización tooan críticos del negocio es muy importante toobe seguro de que si un desastre, aplicación debe estar activados y ejecutándose en un tiempo mínimo.

En la actualidad, la aplicación Microsoft Dynamics AX no tiene integrada ninguna funcionalidad de recuperación ante desastres. Microsoft Dynamics AX consta de muchos componentes de servidor como base de datos de servidor de objetos de aplicación, Active Directory (AD), SQL Server, SharePoint Server, recuperación de desastres de Reporting Server etc. toomanage Hola de cada uno de estos componentes manualmente es no solo costosa también propensas a errores.

En este artículo se explica en detalle cómo crear una solución de recuperación ante desastres para la aplicación Dynamics AX mediante [Azure Site Recovery](site-recovery-overview.md). También se describen las conmutaciones por error planeadas, no planeadas o de prueba con el plan de recuperación de un solo clic, las configuraciones admitidas y los requisitos previos.
La solución de recuperación ante desastres de Azure Site Recovery está totalmente probada, certificada y recomendada por Microsoft Dynamics AX.



## <a name="prerequisites"></a>Requisitos previos

La implementación de recuperación ante desastres para aplicaciones de Dynamics AX con Azure Site Recovery requiere Hola siguiendo los requisitos previos completados.

• Se ha instalado una implementación local de Dynamics AX

• Se ha creado un almacén de Azure Recovery Services en una suscripción de Microsoft Azure

• Si Azure es el sitio de recuperación, ejecutar herramienta de evaluación de preparación de máquina Virtual de Azure de hello en tooensure de máquinas virtuales que sean compatibles con máquinas virtuales de Azure y servicios de Azure Site Recovery


## <a name="site-recovery-support"></a>Compatibilidad de Site Recovery

A fin de Hola de creación de este artículo, se utilizaron máquinas virtuales VMware con 2012R3 de Dynamics AX en Windows Server 2012 R2 Enterprise. Como la replicación de recuperación de sitios es independiente de la aplicación, se proporcionan recomendaciones de hello aquí son toohold esperado en los escenarios siguientes también.

### <a name="source-and-target"></a>Origen y destino

**Escenario** | **sitio secundario tooa** | **tooAzure**
--- | --- | ---
**Hyper-V** | Sí | Sí
**VMware** | Sí | Sí
**Servidor físico** | Sí | Sí

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a>Habilitar la recuperación ante desastres de la aplicación Dynamics AX mediante Azure Site Recovery
### <a name="protect-your-dynamics-ax-application"></a>Proteger la aplicación Dynamics AX
Cada componente de hello Dynamics AX necesidades toobe protegido tooenable Hola aplicación completa replicación y la recuperación. En esta sección se describe:

**1. Protección de Active Directory**

**2. Protección del nivel de SQL**

**3. Protección de los niveles de aplicación y web**

**4. Configuración de red**

**5. Plan de recuperación**

### <a name="1-setup-ad-and-dns-replication"></a>1. Configuración de la replicación de DNS y AD

Active Directory es necesario en el sitio de recuperación ante desastres de Hola para toofunction de aplicación de Dynamics AX. Hay dos opciones recomendadas basándose en complejidad Hola Hola del local del entorno de cliente.

**Opción 1**

Si el cliente hello tiene un número pequeño de aplicaciones y un controlador de dominio para su toda sitio local y se se conmuta por error todo el sitio Hola juntas, a continuación, se recomienda utilizar la replicación de ASR tooreplicate Hola DC máquina toosecondary sitio ( es aplicable para el sitio tooSite y tooAzure de sitio).

**Opción 2**

Si cliente hello tiene un gran número de aplicaciones y ejecuta un bosque de Active Directory y conmutará pocas aplicaciones a la vez, se recomienda configurar un controlador de dominio adicional en el sitio de recuperación ante desastres de hello (sitio secundario o en Azure).

Consulte demasiado[guía complementaria sobre la realización de un controlador de dominio disponible en el sitio de recuperación ante desastres](site-recovery-active-directory.md). Para el resto de este documento, supondremos que habrá un controlador de dominio disponible en el sitio de recuperación ante desastres.

### <a name="2-setup-sql-server-replication"></a>2. Configuración de la replicación de SQL Server
Consulte la Guía de toocompanion para orientación técnica detallada sobre Hola recomendada la opción para proteger [nivel SQL](site-recovery-sql.md).

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a>3. Habilitar la protección del cliente de Dynamics AX y las máquinas virtuales de AOS
Realizar la configuración de Azure Site Recovery pertinentes en función de si se implementan máquinas virtuales de hello en [Hyper-V](site-recovery-hyper-v-site-to-azure.md) o en [VMware](site-recovery-vmware-to-azure.md).

> [!TIP]
> Tooconfigure de frecuencia coherente de bloqueo recomendado es de 15 minutos.
>

Hola por debajo de instantánea muestra el estado de protección de Hola de máquinas virtuales de componente de Dynamics en escenario de protección 'TooAzure de sitio de VMware'.
![Elementos protegidos ](./media/site-recovery-dynamics-ax/protecteditems.png)

### <a name="4-configure-networking"></a>4. Configuración de red
Configuración de procesos de máquina virtual y configuración de red

Cliente AX hello y las máquinas virtuales de AOS configurar configuración de red en Azure Site Recovery para que redes de VM de hello obtener toohello adjunto red de recuperación ante desastres apropiado después de la conmutación por error. Asegúrese de red de recuperación ante desastres de Hola para estos niveles es enrutable toohello nivel de SQL.

Puede seleccionar Hola VM Hola replica configuración de red de elementos tooconfigure Hola tal y como se muestra en la instantánea de Hola a continuación.

* Para los servidores AOS seleccione conjunto de disponibilidad correcta de Hola.

* Si está usando una dirección IP estática y luego especifique Hola IP que desee Hola tootake de máquina virtual en hello **IP de destino** campo ![configuración de red](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)



### <a name="5-creating-a-recovery-plan"></a>5. Creación de un plan de recuperación

Puede crear un plan de recuperación en proceso de conmutación por error de Azure Site Recovery tooautomate Hola. Agregar capa de aplicación y de nivel web Hola Plan de recuperación. Ordénelas en grupos diferentes, por lo Hola front-end cierre antes de nivel de aplicación.

1)  Seleccionar almacén de Azure Site Recovery de hello en su suscripción y haga clic en el icono de planes de recuperación.

2)  Haga clic en Plan de recuperación y especifique un nombre.

3)  Seleccione hello 'Source' y 'Target'. destino de Hello puede ser el sitio secundario o de Azure. Si elige Azure, debe especificar el modelo de implementación de Hola

![Creación del plan de recuperación](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  Seleccione Hola AOS y el plan de recuperación de toohello de máquinas virtuales de cliente y haga clic en ✓.
![Crear plan de recuperación](./media/site-recovery-dynamics-ax/selectvms.png)


![Plan de recuperación](./media/site-recovery-dynamics-ax/recoveryplan.png)

Puede personalizar el plan de recuperación de Hola para aplicación de Dynamics AX mediante la adición de varios pasos tal como se detalla a continuación. Hola por encima de instantánea muestra hello el plan de recuperación completo después de agregar todos los pasos de Hola.

*Pasos:*

*1. Pasos de conmutación por error de SQL Server*

Consulte demasiado['Solución de recuperación ante desastres de SQL Server'](site-recovery-sql.md) guía complementaria para obtener más información acerca de servidor de tooSQL concreto de pasos de recuperación.

*2. Conmutación por error el grupo 1: Conmutar por error las máquinas virtuales de hello AOS*

Asegúrese de que el punto de recuperación de hello seleccionado es lo más cerca posible toohello de base de datos PIT pero no con antelación.

*3. Script: Equilibrador de carga del complemento (solo E-A)* agregar una secuencia de comandos (a través de la automatización de Azure) después del grupo de AOS VM aparece tooadd un tooit de equilibrador de carga. Puede usar una secuencia de comandos toodo esta tarea. Consulte el artículo [cómo tooadd equilibrador de carga para recuperación ante desastres de aplicación de varios niveles](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)

*4. Grupo de conmutación por error 2: Conmutar por error cliente AX hello las máquinas virtuales.*
Conmutar por error el nivel de web de hello las máquinas virtuales como parte del plan de recuperación de Hola.


### <a name="doing-a-test-failover"></a>Realización de una conmutación por error de prueba

Consulte too'AD DR Solution ' y 'Solución de recuperación ante desastres de SQL Server' las guías complementarias para consideraciones específicas tooAD y SQL server respectivamente durante la conmutación por error de prueba.

1.  Vaya tooAzure portal y seleccione el almacén de Site Recovery.
2.  Haga clic en el plan de recuperación de hello creado para Dynamics AX.
3.  Haga clic en Probar conmutación por error.
4.  Seleccione el proceso de conmutación por error de prueba de hello red virtual toostart Hola.
5.  Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.
6.  Después de completar las validaciones de hello, puede seleccionar 'Validaciones completar' y entorno de conmutación por error de prueba de Hola se borrarán.

Siga [esta guía](site-recovery-test-failover-to-azure.md) toodo una conmutación por error de prueba.

### <a name="doing-a-failover"></a>Realización de una conmutación por error

1.  Vaya tooAzure portal y seleccione el almacén de Site Recovery.
2.  Haga clic en el plan de recuperación de hello creado para Dynamics AX.
3.  Haga clic en Conmutación por error y seleccione Conmutación por error.
4.  Seleccionar red de destino de Hola y haga clic en el proceso de conmutación por error ✓ toostart Hola.

Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.

### <a name="perform-a-failback"></a>Realización de una conmutación por recuperación

Consulte too'SQL solución de recuperación ante desastres del servidor ' guía complementaria de consideraciones específicas tooSQL server durante la conmutación por recuperación.

1.  Vaya tooAzure portal y seleccione el almacén de Site Recovery.
2.  Haga clic en el plan de recuperación de hello creado para Dynamics AX.
3.  Haga clic en Conmutación por error y seleccione Conmutación por error.
4.  Haga clic en Cambiar dirección.
5.  Seleccione opciones adecuadas de hello - sincronización de datos y las opciones de creación de máquinas virtuales
6.  Haga clic en el proceso ✓ toostart hello 'Conmutación por recuperación'.


Siga [estas directrices](site-recovery-failback-azure-to-vmware.md) cuando realice una conmutación por recuperación.

##<a name="summary"></a>Resumen
Con Azure Site Recovery, puede crear un plan completo de recuperación ante desastres automatizado para su aplicación Dynamics AX. Se puede iniciar la conmutación por error de hello en segundos desde cualquier lugar en Hola eventos de interrupción y poner la aplicación hello en ejecución en minutos.

## <a name="next-steps"></a>Pasos siguientes
Lectura [¿qué cargas de trabajo se debe proteger?](site-recovery-workload.md) toolearn más sobre la protección de cargas de trabajo empresariales con Azure Site Recovery.
