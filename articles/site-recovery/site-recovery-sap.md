---
title: "una implementación de aplicación de SAP NetWeaver de varios nivel con Azure Site Recovery aaaProtect | Documentos de Microsoft"
description: "Este artículo describe cómo tooprotect SAP NetWeaver las implementaciones de aplicaciones con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: manayar
ms.openlocfilehash: 34651c7b14d23a44005372f4f923c401e0224231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-a-multi-tier-sap-netweaver-application-deployment-using-azure-site-recovery"></a>Protección de la implementación de una aplicación SAP NetWeaver de niveles múltiples mediante Azure Site Recovery

La mayor parte de las implementaciones SAP grandes y medianas incluyen algún tipo de solución de recuperación ante desastres.  importancia de Hola de sólido y probar soluciones de recuperación ante desastres ha aumentado a medida que más negocio principal son procesos pase tooapplications como SAP.  Azure Site Recovery ha sido probadas y se integra con aplicaciones de SAP y excede las capacidades de Hola de mayoría soluciones de recuperación ante desastres local, en un menor costo total de propiedad (TCO) de soluciones de la competencia.
Con Azure Site Recovery, puede:
* Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver que se ejecutan de forma local, replicando tooAzure de componentes.
* Habilitar la protección de aplicaciones de SAP NetWeaver y no es de producción NetWeaver ejecuta Azure, mediante la replicación de componentes tooanother centro de datos de Azure.
* Simplificar la migración a la nube, mediante el uso de Site Recovery toomigrate su tooAzure de implementación de SAP.
* Simplificar las actualizaciones de los proyectos SAP, las pruebas y la creación de prototipos, mediante la creación de una clon en producción a petición para probar las aplicaciones SAP.

Este artículo describe cómo tooprotect SAP NetWeaver las implementaciones de aplicaciones mediante [Azure Site Recovery](site-recovery-overview.md). Este artículo tratan los procedimientos recomendados de Hola para proteger una implementación de SAP NetWeaver de tres niveles en Azure mediante la replicación tooanother centro de datos de Azure con Azure Site Recovery, Hola admitida escenarios y configuraciones, y cómo tooperform las conmutaciones por error, las pruebas las conmutaciones por error (recuperación ante desastres) y las conmutaciones por error real.


## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, asegúrese de que comprende siguiente hello:

1. [Replicar una máquina virtual tooAzure](azure-to-azure-walkthrough-enable-replication.md)
2. Cómo demasiado[el diseño de una red de recuperación](site-recovery-azure-to-azure-networking-guidance.md)
3. [Realizar una tooAzure de conmutación por error de prueba](azure-to-azure-walkthrough-test-failover.md)
4. [Realizar una conmutación por error tooAzure](site-recovery-failover.md)
5. Cómo demasiado[replicar un controlador de dominio](site-recovery-active-directory.md)
6. Cómo demasiado[replicar SQL Server](site-recovery-sql.md)

## <a name="supported-scenarios"></a>Escenarios admitidos
Con Azure Site Recovery se puede implementar una solución de recuperación ante desastres para hello los escenarios siguientes:
* Sistemas SAP que se ejecutan en un centro de datos Azure replicar tooanother centro de datos de Azure (Azure a Azure DR), como la arquitectura [aquí](https://aka.ms/asr-a2a-architecture).
* Sistemas SAP que se ejecutan en servidores de VMWare (o físico) replicación sitio tooa recuperación ante desastres en un centro de datos Azure (VMware a Azure DR), lo que requiere algunos componentes adicionales como la arquitectura local [aquí](https://aka.ms/asr-v2a-architecture).
* Sistemas SAP que se ejecutan en Hyper-V continúa con la replicación sitio tooa recuperación ante desastres en un centro de datos Azure (Hyper-V a Azure DR), lo que requiere algunos componentes adicionales como la arquitectura local [aquí](https://aka.ms/asr-h2a-architecture).

Este documento usa las capacidades de recuperación ante desastres de hello primera mayúsculas - Azure a Azure DR - toodemonstrate Azure Site Recovery SAP. Replicación de Azure Site Recovery sea independiente de la aplicación, se describe el proceso de hello es toohold esperado para otros escenarios, así.

### <a name="required-foundation-services"></a>Servicios básicos requeridos
Este escenario de documentación todos está implementado con hello después servicios foundation implementados:
* Red de privada virtual (VPN) ExpressRoute o de sitio a sitio
* Al menos un servidor DNS y un controlador de dominio de Active Directory se ejecutan en Azure

Se recomienda que la infraestructura de hello anterior toodeploying anterior establecido Azure Site Recovery.


## <a name="typical-sap-application-deployment"></a>Implementación típica de la aplicación SAP
Los clientes de SAP grandes normalmente implementan entre 6 too20 las aplicaciones SAP individuales.  La mayoría de estas aplicaciones se basa en los motores de hello ABAP de SAP NetWeaver o Java.  Sirviendo de soporte para estas aplicaciones NetWeaver básicas se encuentran muchos motores menores e independientes SAP específicos que no son NetWeaver y, por lo general, algunas aplicaciones que no son SAP.  

Es crítico tooinventory que se ejecuta en un modo de implementación de hello horizontal y toodetermine (nivel 2 o 3 niveles), versiones, revisiones de todas las aplicaciones de SAP de hello, renovación de tamaños, las tasas y requisitos de persistencia en disco.

![Modelo de implementación](./media/site-recovery-sap/sap-typical-deployment.png)

capa de persistencia de base de datos de SAP de Hello debe protegerse mediante herramientas nativas de DBMS hello como AlwaysOn de SQL Server, Oracle DataGuard o replicación del sistema de archivos de HANA. nivel de cliente de Hello no también está protegido por Azure Site Recovery, pero es importante tooconsider temas que afectan a esta capa como retraso de propagación de DNS, seguridad y acceso remoto toohello centro de datos de recuperación ante desastres.

Azure Site Recovery es hello recomendada soluciones de nivel de aplicación Hola, incluidos (A) SCS. Otras aplicaciones, como aplicaciones SAP NetWeaver y las aplicaciones de SAP no forman parte del programa Hola general SAP entorno de implementación y también debería estar protegida con Azure Site Recovery.

## <a name="replicate-virtual-machines"></a>Replicación de máquinas virtuales
Siga [esta guía](azure-to-azure-walkthrough-enable-replication.md) toostart replicar todas Hola toohello de máquinas virtuales de aplicación de SAP Azure centro de datos de recuperación ante desastres.

Si usa una dirección IP estática, puede especificar Hola IP que desee Hola tootake de máquina virtual en la sección de tarjetas de interfaz de red de hello en configuración de red y proceso.

![IP de destino](./media/site-recovery-sap/sap-static-ip.png)


## <a name="creating-a-recovery-plan"></a>Creación de un plan de recuperación
Un plan de recuperación permite secuenciación Hola conmutación por error de distintos niveles de una aplicación de varios niveles, por lo tanto, mantener la coherencia de la aplicación. Siga los pasos de hello descritos [aquí](site-recovery-create-recovery-plans.md) al crear un plan de recuperación para una aplicación web de varios niveles.

### <a name="adding-scripts-toohello-recovery-plan"></a>Agregar plan de recuperación de toohello de secuencias de comandos
Quizás necesite toodo ciertas operaciones sobre Hola conmutación por error de máquinas virtuales de Azure post/prueba de conmutación por error para su toofunction aplicaciones correctamente. Puede automatizar la operación de conmutación por error de post hello como actualizar entrada DNS y el cambio de enlaces y las conexiones, agregando los scripts correspondientes en el plan de recuperación de hello tal y como se describe en [este artículo](site-recovery-create-recovery-plans.md#add-scripts).

### <a name="dns-update"></a>Actualización de DNS
Si Hola DNS está configurado para la actualización dinámica de DNS, entonces máquinas virtuales normalmente se haya actualizado Hola DNS con la dirección IP de hello nuevo una vez que se inician. Si desea que tooadd un tooupdate paso explícito DNS con hello nuevas direcciones IP de máquinas virtuales de hello, a continuación, agregue esto [tooupdate IP en DNS de script](https://aka.ms/asr-dns-update) como una acción posterior en grupos de planes de recuperación.  

## <a name="example-azure-to-azure-deployment"></a>Ejemplo de implementación de Azure a Azure
Se representa en diagrama de hello siguiente escenario de recuperación ante desastres de Azure en Azure de Azure Site Recovery de hello:
* Centro de datos principal se encuentra en Singapur (Asia Sureste de Azure) de Hola y Hola centro de datos de recuperación ante desastres es Hong Kong (Azure Asia oriental).  En este escenario, se proporciona una alta disponibilidad local al tener en Singapur dos máquinas virtuales que ejecutan SQL Server AlwaysOn en modo sincrónico.
* Hola ASCS de recurso compartido de archivo puede ser usado tooprovide alta disponibilidad para hello SAP puntos de error únicos. ASCS de recurso compartido de archivos no requiere un disco compartido de clúster y no son necesarias las aplicaciones como SIOS.
* Protección de recuperación ante desastres para capa de DBMS Hola se logra mediante la replicación asincrónica.
* Este escenario muestra "simétrico DR": usar un término toodescribe una solución de recuperación ante desastres que es una réplica exacta de producción, por lo tanto, Hola solución de recuperación ante desastres de SQL Server tiene alta disponibilidad local. no es obligatorio para la capa de base de datos de Hola Hola usar DR simétrico y muchos clientes aprovechan la flexibilidad de Hola de las implementaciones de nube toobuild un nodo de disponibilidad alta local rápidamente después de un evento de recuperación ante desastres.
* diagrama de Hello muestra hello ASCS de SAP NetWeaver y nivel de servidor de aplicación replicada por Azure Site Recovery.

![Escenario de replicación](./media/site-recovery-sap/sap-replication-scenario.png)

## <a name="doing-a-test-failover"></a>Realización de una conmutación por error de prueba
Siga [esta guía](azure-to-azure-walkthrough-test-failover.md) toodo una conmutación por error de prueba.

1.  Vaya tooAzure portal y seleccione el almacén de servicios de recuperación.
2.  Haga clic en el plan de recuperación de hello creado para aplicaciones de SAP (s).
3.  Haga clic en 'Probar conmutación por error'.
4.  Seleccione el punto de recuperación y el proceso de conmutación por error de prueba de red virtual de Azure toostart Hola.
5.  Una vez que el entorno secundario hello es hacia arriba, puede realizar sus validaciones.
6.  Después de completar las validaciones de hello, haga clic en 'Conmutación por error de limpieza prueba' y conmutación por error de tooclean Hola entorno.

## <a name="doing-a-failover"></a>Realización de una conmutación por error
Siga [estas directrices](site-recovery-failover.md) cuando realice una conmutación por error.

1.  Vaya tooAzure portal y seleccione el almacén de servicios de recuperación.
2.  Haga clic en el plan de recuperación de hello creado para aplicaciones de SAP.
3.  Haga clic en 'Conmutación por error'.
4.  Seleccione el proceso de conmutación por error de Hola de toostart de punto de recuperación.

## <a name="next-steps"></a>Pasos siguientes
Más información acerca de cómo crear una solución de recuperación ante desastres para las implementaciones SAP NetWeaver con Azure Site Recovery en [estas notas del producto](http://aka.ms/asr-sap). Hola notas del producto también artículo incluye recomendaciones para distintas arquitecturas SAP, listas de aplicaciones compatibles y los tipos VM para SAP en Azure y describen los posibles planes de pruebas para la solución de recuperación ante desastres.

Obtenga más información sobre la [replicación de otras cargas de trabajo](site-recovery-workload.md) con Site Recovery.
