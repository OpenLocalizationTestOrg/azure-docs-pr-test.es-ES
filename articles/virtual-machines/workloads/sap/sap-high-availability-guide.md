---
title: "Máquinas virtuales de alta disponibilidad para SAP NetWeaver aaaAzure | Documentos de Microsoft"
description: "Guía de alta disponibilidad para SAP NetWeaver en Azure Virtual Machines"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Máquinas virtuales de Azure es la solución de Hola para organizaciones que necesitan cálculo, almacenamiento y recursos de red, en un tiempo mínimo y sin ciclos de adquisición prolongados. Puede usar máquinas virtuales de Azure toodeploy aplicaciones clásicas como ABAP basadas en SAP NetWeaver, Java y una pila ABAP + Java. Amplíe la confiabilidad y disponibilidad sin recursos locales adicionales. Azure Virtual Machines admite la conectividad entre locales, así que podrá integrar Azure Virtual Machines a los dominios locales, las nubes privadas y la infraestructura de sistema SAP de la organización.

En este artículo, se incluyen los pasos de Hola que debe seguir toodeploy sistemas SAP de alta disponibilidad en Azure utilizando el modelo de implementación de hello Azure Resource Manager. Le guiaremos por estas tareas principales:

* Buscar Hola derecho guías de instalación y las notas de SAP, aparecen en hello [recursos] [ sap-ha-guide-2] sección. En este artículo complementa la documentación de la instalación de SAP y las notas de SAP, que son recursos principales de Hola que pueden ayudarle a instalar e implementar el software SAP en plataformas específicas.
* Obtenga información acerca de las diferencias de hello entre modelo de implementación de Azure Resource Manager Hola y Hola implementación clásico de Azure.
* Obtenga información acerca de los modos de quórum de clúster de conmutación por error de Windows Server, por lo que puede seleccionar el modelo de Hola que es adecuado para la implementación de Azure.
* Obtener información sobre el almacenamiento compartido de Clústeres de conmutación por error de Windows Server en los servicios de Azure.
* Obtenga información acerca de cómo proteger los componentes de único punto de error como SAP Central servicios (ASCS) de Advanced Business aplicación Programming (ABAP) toohelp / Services Central (SCS) de SAP y sistemas de administración de bases de datos (DBMS) y componentes redundantes, como SAP Servidor de aplicaciones, en Azure.
* Seguir un ejemplo detallado de la instalación y configuración de un sistema SAP de alta disponibilidad en un clúster de Clústeres de conmutación por error de Windows Server mediante Azure Resource Manager.
* Obtenga información acerca de los clústeres de conmutación por error del servidor de Windows en Azure de toouse requiere pasos adicionales, pero que no son necesarios en una implementación local.

implementación de toosimplify y la configuración, en este artículo, usamos Hola plantillas del Administrador de recursos de alta disponibilidad de tres niveles SAP. plantillas de Hello automatizan la implementación de hello toda la infraestructura que necesite para un sistema SAP de alta disponibilidad. infraestructura Hola también admite el ajuste de tamaño de SAP aplicación rendimiento estándar (SAPS) del sistema SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Requisitos previos
Antes de empezar, asegúrese de que se cumplen los requisitos previos de Hola que se describen en las secciones siguientes de Hola. Además, puede toocheck seguro de que todos los recursos enumerados en hello [recursos] [ sap-ha-guide-2] sección.

En este artículo usamos plantillas de Azure Resource Manager para [SAP NetWeaver de tres niveles con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Consulte [Plantillas de Azure Resource Manager para SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/) para ver información general útil sobre las plantillas.

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Recursos
Estos artículos también se refieren a las implementaciones de SAP en Azure:

* [Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver][planning-guide]
* [Implementación de Azure Virtual Machines para SAP NetWeaver][deployment-guide]
* [Implementación de DBMS de Azure Virtual Machines para SAP NetWeaver][dbms-guide]
* [Alta disponibilidad de Azure Virtual Machines para SAP NetWeaver (esta guía)][sap-ha-guide]

> [!NOTE]
> Siempre que sea posible, le ofrecemos un toohello de vínculo que hace referencia la Guía de instalación de SAP (consulte hello [guías de instalación de SAP][sap-installation-guides]). Los requisitos previos y obtener información sobre el proceso de instalación de hello, que una instalación de SAP NetWeaver buena idea tooread Hola guía cuidadosamente. En este artículo solo se abarcan tareas específicas para los sistemas basados en SAP NetWeaver que puede usar con Azure Virtual Machines.
>
>

Estas notas de SAP están relacionadas toohello tema de SAP en Azure:

| Número de nota | Título |
| --- | --- |
| [1928533] |SAP Applications on Azure: Supported Products and Sizing (Aplicaciones SAP en Azure: productos y tamaños compatibles) |
| [2015553] |SAP on Microsoft Azure: Support Prerequisites (SAP en Microsoft Azure: requisitos previos de compatibilidad) |
| [1999351] |Enhanced Azure Monitoring for SAP (Supervisión mejorada de Azure para SAP) |
| [2178632] |Key Monitoring Metrics for SAP on Microsoft Azure (Métricas de supervisión clave para SAP en Microsoft Azure) |
| [1999351] |Virtualization on Windows: Enhanced Monitoring (Virtualización en Windows: supervisión mejorada) |
| [2243692] |Uso de almacenamiento SSD premium de Azure para la instancia DBMS de SAP |

Obtener más información sobre hello [limitaciones de las suscripciones de Azure][azure-subscription-service-limits-subscription], incluidas las limitaciones de general predeterminado y máximo.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>SAP de alta disponibilidad con Azure Resource Manager frente a modelo de implementación clásica Azure Hola
Hola, Administrador de recursos de Azure y modelos de implementación clásico de Azure son diferentes en hello siguientes áreas:

- Grupos de recursos
- Azure interno cargar la dependencia de equilibrador de grupo de recursos de Azure Hola
- Soporte técnico para el escenario de varios SID de SAP

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Grupos de recursos
En el Administrador de recursos de Azure, puede usar toomanage de grupos de recursos todos los recursos de la aplicación hello en su suscripción de Azure. Un enfoque integrado en un grupo de recursos, todos los recursos se Hola mismo ciclo de vida. Por ejemplo, todos los recursos se crean en hello mismo tiempo y se eliminan al Hola mismo tiempo. Más información sobre los [grupos de recursos](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Azure interno cargar la dependencia de equilibrador de grupo de recursos de Azure Hola

En el modelo de implementación clásica Azure hello, hay una dependencia entre el equilibrador de carga interno de Azure de hello (servicio del equilibrador de carga de Azure) y el servicio de nube de Hola. Cada equilibrador de carga interno precisa de un servicio en la nube.

En el Administrador de recursos de Azure, cada recurso de Azure necesita toobe parte de un grupo de recursos de Azure, y esto también es válido para el equilibrador de carga de Azure. Sin embargo, hay ningún grupo de recursos de Azure una necesidad toohave por el equilibrador de carga de Azure, por ejemplo, un grupo de recursos de Azure puede contener varios equilibradores de carga de Azure. entorno de Hello es más sencillo y flexible. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Soporte técnico para el escenario de varios SID de SAP

En Azure Resource Manager, puede instalar varias instancias de ASCS/SCS de identificador de sistema SAP (SID) en un clúster. Esto es posible gracias a la compatibilidad con las distintas direcciones IP de cada equilibrador de carga interno de Azure.

toouse Hola modelo de implementación clásico de Azure, siga los procedimientos de hello descritos en [SAP NetWeaver en Azure: instancias de clústeres de SAP ASCS/SCS mediante el uso de clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Se recomienda encarecidamente que utilice el modelo de implementación de hello Azure Resource Manager para las instalaciones de SAP. Ofrece numerosas ventajas que no están disponibles en el modelo de implementación clásica de Hola. Obtenga más información sobre los [modelos de implementación de Azure][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Clústeres de conmutación por error de Windows Server
Clústeres de conmutación por error de Windows Server es el fundamento de Hola de una instalación de SAP ASCS/SCS de alta disponibilidad y DBMS en Windows.

Un clúster de conmutación por error es un grupo de 1 + n servidores independientes (nodos) que funcionan conjuntamente disponibilidad de hello tooincrease de aplicaciones y servicios. Si se produce un error en un nodo, clústeres de conmutación por error de Windows Server calcula el número de Hola de errores que pueden producirse al mantener un buen estado tooprovide aplicaciones y servicios de clúster. Puede elegir entre diferentes quórum modos tooachieve conmutación por error.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Modos de cuórum
Puede elegir entre cuatro modos de cuórum cuando use Clústeres de conmutación por error de Windows Server:

* **Mayoría de nodo**. Cada nodo del clúster de Hola puede votar. Hola clúster solo funciona con una mayoría de votos, es decir, con más de la mitad de los votos de Hola. Se recomienda esta opción para los clústeres con un número impar de nodos. Por ejemplo, pueden producir un error en tres nodos en un clúster de siete nodos e imágenes fijas de clúster de hello logra una mayoría y continúa toorun.  
* **Mayoría de disco y nodo**. Todos los nodos y un disco designado (un testigo de disco) en el almacenamiento de clúster de hello pueden votar cuando estén disponibles y en la comunicación. Hola clúster solo funciona con una mayoría de hello votos, es decir, con más de la mitad de los votos de Hola. Este modo resulta útil en un entorno de clúster con un número par de nodos. Si nodos mitad hello y disco Hola estén en línea, clúster de hello permanece en un estado correcto.
* **Mayoría de recurso compartido de archivos y nodo**. Cada nodo más crea un recurso compartido de archivo designado (un testigo de recurso compartido de archivos) que Hola administrador puede votar, independientemente de si están disponibles para los nodos de Hola y recurso compartido de archivos y en la comunicación. Hola clúster solo funciona con una mayoría de hello votos, es decir, con más de la mitad de los votos de Hola. Este modo resulta útil en un entorno de clúster con un número par de nodos. Es similar toohello nodo y el modo de mayoría de disco, pero usa un recurso compartido de archivos de testigo en lugar de un disco testigo. Este modo es fácil tooimplement, pero si el recurso compartido de archivos de hello sí mismo no es de alta disponibilidad, es posible que un único punto de error.
* **Sin mayoría: solo disco**. clúster de Hello tiene un quórum si un nodo está disponible y en la comunicación con un disco concreto hello en almacenamiento de clúster. Sólo los nodos Hola que también están en comunicación con ese disco pueden unirse a clústeres de Hola. No se recomienda usar este modo.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Clústeres de conmutación por error de Windows Server local
En la figura 1 se muestra un clúster de dos nodos. Si hello se produce un error en la conexión de red entre los nodos de Hola y ambos nodos se mantienen actualizados y en ejecución, un recurso compartido de archivo o el disco de quórum determina qué nodo continuará servicios y aplicaciones del clúster de tooprovide Hola. nodo de Hola que tiene el disco de quórum de toohello de acceso o recurso compartido de archivo es Hola que garantiza que los servicios continúen.

Dado que este ejemplo utiliza un clúster de dos nodos, utilizamos Hola nodo y modo de quórum de mayoría de recurso compartido de archivos. Hola nodo y mayoría de disco también es una opción válida. En un entorno de producción, se recomienda usar un disco de cuórum. Puede utilizar toomake de tecnología de sistema de almacenamiento y de red está altamente disponible.

![Figura 1: Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure][sap-ha-guide-figure-1000]

_**Figura 1:** Ejemplo de una configuración de Clústeres de conmutación por error de Windows Server para ASCS/SCS de SAP en Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Almacenamiento compartido
En la figura 1 también se muestra un clúster de almacenamiento compartido de dos nodos. En un clúster de almacenamiento compartido local, todos los nodos de clúster de hello detectan almacenamiento compartido. Un mecanismo de bloqueo protege los datos de hello frente a daños. Todos los nodos pueden detectar si se produce un error en otro nodo. Si se produce un error en un nodo, los nodos restantes Hola toma posesión de recursos de almacenamiento de Hola y garantiza la disponibilidad de hello de servicios.

> [!NOTE]
> No necesita discos compartidos para obtener alta disponibilidad con algunas aplicaciones de DBMS, como SQL Server. SQL Server Always On replica los archivos de datos y de registro DBMS desde el disco local de hello un nodo toohello local del disco de clúster de otro nodo del clúster. En ese caso, la configuración de clúster de Windows hello no necesita un disco compartido.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Redes y resolución de nombres
Los equipos cliente comunicarse con clúster Hola mediante una dirección IP virtual y un nombre de host virtual que Hola proporciona el servidor DNS. Hola nodos locales y de servidor DNS de hello puede administrar varias direcciones IP.

En una configuración típica, puede usar dos o más conexiones de red:

* Un almacenamiento de información de conexión dedicada toohello
* Una conexión de red interna del clúster para el latido de Hola
* Una red pública que los clientes usan tooconnect toohello clúster

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Clústeres de conmutación de Windows Server en Azure
En comparación con las implementaciones de nube privada o metal toobare, máquinas virtuales de Azure requiere tooconfigure pasos adicionales clústeres de conmutación por error de Windows Server. Cuando se compila un disco de clúster compartido, debe tooset nombres de varias direcciones IP y el host virtual para la instancia de SAP ASCS/SCS Hola.

En este artículo se tratan los conceptos clave y Hola pasos adicionales necesarios toobuild un clúster de alta disponibilidad de servicios centrales de SAP en Azure. Le mostramos cómo tooset una herramienta de terceros de hello SIOS DataKeeper y cómo tooconfigure hello Azure interno equilibrador de carga. Puede usar estos toocreate herramientas un clúster de conmutación por error de Windows con un testigo de recurso compartido de archivos en Azure.

![Figura 2: Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido][sap-ha-guide-figure-1001]

_**Figura 2:** Configuración de Clústeres de conmutación por error de Windows Server en Azure sin un disco compartido_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Disco compartido en Azure con SIOS DataKeeper
Se necesita almacenamiento compartido de clúster para una instancia de ASCS/SCS de SAP de alta disponibilidad. Como de septiembre de 2016, Azure no ofrece almacenamiento compartido puede usar toocreate un clúster de almacenamiento compartido. Puede utilizar software de terceros SIOS DataKeeper Cluster Edition toocreate un almacenamiento de reflejo que simula el almacenamiento compartido de clúster. Hola solución SIOS proporciona replicación sincrónica de datos en tiempo real. Este es el procedimiento para crear un recurso de disco compartido para un clúster:

1. Adjuntar un tooeach de disco adicional de hello las máquinas virtuales (VM) en una configuración de clúster de Windows.
2. Ejecute SIOS DataKeeper Cluster Edition en ambos nodos de la máquina virtual.
3. Configurar SIOS DataKeeper Cluster Edition de modo que refleje el contenido de Hola Hola adicional conectado del volumen de disco de volumen adicional en el disco adjuntada toohello de máquina virtual de origen de Hola Hola máquina virtual de destino. SIOS DataKeeper abstrae volúmenes locales de origen y de destino de Hola y a continuación, presenta tooWindows agrupación en clústeres de conmutación por error de servidor como un disco compartido.

Obtenga más información sobre [SIOS DataKeeper](http://us.sios.com/products/datakeeper-cluster/).

![Figura 3: Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 3:** Configuración de Clústeres de conmutación por error de Windows Server en Azure con SIOS DataKeeper_

> [!NOTE]
> No necesita discos compartidos para obtener alta disponibilidad con algunos productos de DBMS, como SQL Server. SQL Server Always On replica los archivos de datos y de registro DBMS desde el disco local de hello un nodo toohello local del disco de clúster de otro nodo del clúster. En este caso, la configuración de clúster de Windows hello no necesita un disco compartido.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Resolución de nombres en Azure
plataforma de nube de Azure de Hello no ofrecen Hola opción tooconfigure direcciones IP virtuales, como las direcciones IP flotantes. Es necesario un tooset de solución alternativa de un virtual tooreach Hola clúster recurso de dirección IP en la nube de Hola.
Azure tiene un equilibrador de carga interno en hello servicio del equilibrador de carga de Azure. Con el equilibrador de carga interno de hello, los clientes tener acceso a clúster de Hola a través de la dirección IP virtual del clúster Hola.
Necesita el equilibrador de carga interno de toodeploy Hola Hola grupo de recursos que contiene los nodos del clúster Hola. A continuación, configure todas las reglas de reenvío con el sondeo de Hola puertos del equilibrador de carga interno de Hola de puerto es necesario.
Hola clientes pueden conectarse a través del nombre de host virtual Hola. el servidor DNS de Hello resuelve la dirección IP del clúster hello y puerto de identificadores del equilibrador de carga interno de hello toohello nodo activo del clúster de Hola de reenvío.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Alta disponibilidad de SAP NetWeaver en infraestructura como servicio (IaaS) de Azure
tooachieve SAP de alta disponibilidad de aplicaciones, como para los componentes de software SAP, necesita hello tooprotect los componentes siguientes:

* Instancia de servidores de aplicaciones de SAP
* instancia de SAP ASCS/SCS,
* servidor DBMS

Para obtener más información sobre cómo proteger los componentes SAP en escenarios de alta disponibilidad, consulte [Implementación y planeamiento de Azure Virtual Machines para SAP NetWeaver][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Alta disponibilidad en los servidores de aplicaciones de SAP
Normalmente, no necesita una solución de alta disponibilidad específica para las instancias de servidor de aplicaciones de SAP y cuadro de diálogo de Hola. Obtiene alta disponibilidad mediante redundancia y configurará varias instancias de diálogo en distintas instancias de Azure Virtual Machines. Debe tener, como mínimo, 2 instancias de aplicaciones de SAP instaladas en 2 instancias de Azure Virtual Machines.

![Figura 4: Alta disponibilidad en los servidores de aplicaciones de SAP][sap-ha-guide-figure-2000]

_**Figura 4**: Alta disponibilidad en los servidores de aplicaciones de SAP_

Debe colocar todas las máquinas virtuales que instancias de servidor de aplicaciones de SAP de host en Hola mismo conjunto de disponibilidad de Azure. Un conjunto de disponibilidad de Azure garantiza lo siguiente:

* Todas las máquinas virtuales forman parte del programa Hola mismo dominio de actualización. Un dominio de actualización, por ejemplo, se asegura de que no se actualizan las máquinas virtuales hello en hello vez durante el tiempo de inactividad de mantenimiento planeado.
* Todas las máquinas virtuales forman parte del programa Hola mismo dominio de error. Un dominio de error, por ejemplo, se asegura que las máquinas virtuales se implementan para que ningún punto único de error afecta a la disponibilidad de Hola de todas las máquinas virtuales.

Más información acerca de cómo demasiado[administrar Hola disponibilidad de máquinas virtuales][virtual-machines-manage-availability].

Solo el disco no administrado: dado que hello cuenta de almacenamiento de Azure es un posible punto de error único, es importante toohave al menos dos cuentas de almacenamiento de Azure, en el que se distribuyen al menos dos máquinas virtuales. En una configuración ideal, discos de Hola de cada máquina virtual que está ejecutando una instancia del cuadro de diálogo SAP se implementaría en una cuenta de almacenamiento diferente.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Instancia de ASCS/SCS de SAP de alta disponibilidad
La figura 5 es un ejemplo de una instancia de ASCS/SCS de SAP de alta disponibilidad.

![Figura 5: Instancia de ASCS/SCS de SAP de alta disponibilidad][sap-ha-guide-figure-2001]

_**Figura 5:** Instancia de ASCS/SCS de SAP de alta disponibilidad_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Alta disponibilidad de instancia de ASCS/SCS de SAP con Clústeres de conmutación por error de Windows Server en Azure
En comparación con las implementaciones de nube privada o metal toobare, máquinas virtuales de Azure requiere tooconfigure pasos adicionales clústeres de conmutación por error de Windows Server. toobuild un clúster de conmutación por error de Windows, necesita un disco de clúster compartido, varias direcciones IP, varios nombres de host virtual y un equilibrador de carga interno de Azure para una instancia de SAP ASCS/SCS de agrupación en clústeres. Esto se describe con más detalle más adelante en el artículo de Hola.

![Figura 6: Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Figura 6:** Clústeres de conmutación por error de Windows Server para una configuración de ASCS/SCS de SAP en Azure con SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a>Alta disponibilidad para la instancia de DBMS
Hola DBMS es también un único punto de contacto en un sistema SAP. Necesita tooprotect mediante una solución de alta disponibilidad. La figura 7 muestra una solución de alta disponibilidad AlwaysOn de SQL Server en Azure, con clústeres de conmutación por error de Windows Server y hello Azure interno equilibrador de carga. SQL Server AlwaysOn replica los archivos de datos y de registro de DBMS con su propia replicación DBMS. En este caso, no necesita agrupar discos compartidos, lo que simplifica el programa de instalación completa de Hola.

![Figura 7: Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)][sap-ha-guide-figure-2003]

_**Figura 7:** Ejemplo de DBMS de SAP de alta disponibilidad (SQL Server AlwaysOn)_

Para obtener más información acerca de la agrupación en clústeres de SQL Server en Azure mediante el modelo de implementación de hello Azure Resource Manager, vea estos artículos:

* [Configuración manual de grupos de disponibilidad AlwaysOn en Azure Virtual Machines con Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Configuración de un equilibrador de carga interno para un grupo de disponibilidad AlwaysOn en Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Escenarios de implementación completa de alta disponibilidad

### <a name="deployment-scenario-using-architectural-template-1"></a>Escenario de implementación con la plantilla 1 de arquitectura

En la figura 8 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP. Este escenario se configura como se indica a continuación:

- Se utiliza un clúster dedicado para la instancia de SAP ASCS/SCS Hola.
- Se utiliza un clúster dedicado para la instancia DBMS Hola.
- Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.

![Figura 8: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS][sap-ha-guide-figure-2004]

_**Figura 8**: Plantilla 1 de arquitectura de alta disponibilidad de SAP con un clúster dedicado para ASCS/SCS y DBMS_

### <a name="deployment-scenario-using-architectural-template-2"></a>Escenario de implementación con la plantilla 2 de arquitectura

En la figura 9 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **UN** sistema SAP. Este escenario se configura como se indica a continuación:

- Se utiliza un clúster dedicado para **ambos** Hola SAP ASCS/SCS de la instancia y Hola DBMS.
- Se implementan instancias de servidores de aplicaciones SAP en máquinas virtuales dedicadas propias.

![Figura 9: Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS][sap-ha-guide-figure-2005]

_**Figura 9:** Plantilla 2 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para ASCS/SCS y otro para la instancia de DBMS_

### <a name="deployment-scenario-using-architectural-template-3"></a>Escenario de implementación con la plantilla 3 de arquitectura

En la figura 10 se muestra un ejemplo de una arquitectura de SAP NetWeaver de alta disponibilidad en Azure para **DOS** sistemas SAP, con &lt;SID1&gt; y &lt;SID2&gt;. Este escenario se configura como se indica a continuación:

- Se utiliza un clúster dedicado para **ambos** instancia Hola SAP ASCS/SCS SID1 *y* instancia Hola SAP ASCS/SCS SID2 (un clúster).
- Se usa un clúster dedicado para SID 1 de DBMS y otro para SID2 de DBMS (dos clústeres).
- Instancias de servidor de aplicaciones de SAP para hello sistema SAP SID1 tienen sus propias máquinas virtuales dedicadas.
- Instancias de servidor de aplicaciones de SAP para hello sistema SAP SID2 tienen sus propias máquinas virtuales dedicadas.

![Figura 10: Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS][sap-ha-guide-figure-6003]

_**Figura 10:** Plantilla 3 de arquitectura de alta disponibilidad de SAP, con un clúster dedicado para las diferentes instancias de ASCS/SCS_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Preparar la infraestructura de Hola

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Preparar la infraestructura de Hola para arquitectura de plantilla de 1
Las plantillas de Azure Resource Manager para SAP ayudan a simplificar la implementación de los recursos necesarios.

plantillas de tres niveles de Hello en el Administrador de recursos de Azure también admiten escenarios de alta disponibilidad, como en la arquitectura 1 de plantilla, que tiene dos clústeres. Cada clúster es un único punto de error de SAP para ASCS/SCS de SAP y DBMS.

Aquí es donde puede obtener plantillas del Administrador de recursos de Azure para el escenario de ejemplo de Hola que se describen en este artículo:

* [Imagen de Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Imagen de Azure Marketplace con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Imagen personalizada con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

infraestructura de hello tooprepare de arquitectura 1 de plantilla:

- En el portal de Azure, en Hola Hola **parámetros** hoja en hello **SYSTEMAVAILABILITY** cuadro, seleccione **HA**.

  ![Figura 11: Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP][sap-ha-guide-figure-3000]

_**Figura 11:** Especificación de los parámetros de Azure Resource Manager para alta disponibilidad de SAP_


  crean plantillas de Hello:

  * **Máquinas virtuales**:
    * Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-di-<*Número*>
    * Máquinas virtuales de clúster de ASCS/SCS: <*SIDSistemaSAP*>-ascs-<*Número*>
    * Un clúster de DBMS: <*SIDSistemaSAP*>-db-<*Número*>

  * **Tarjetas de red para todas las máquinas virtuales con direcciones IP asociadas**:
    * <*SIDSistemaSAP*&gt;-nic-di-&lt;*Número*>
    * <*SIDSistemaSAP*&gt;-nic-ascs-&lt;*Número*>
    * <*SIDSistemaSAP*&gt;-nic-db-&lt;*Número*>

  * **Cuentas de Azure Storage (solo discos no administrados)**

  * **Grupos de disponibilidad** para:
    * Máquinas virtuales de Servidor de aplicaciones de SAP: <*SIDSistemaSAP*>-avset-di
    * Máquinas virtuales de clúster de ASCS/SCS de SAP: <*SIDSistemaSAP*>-avset-ascs
    * Máquinas virtuales de clúster de DBMS: <*SIDSistemaSAP*>-avset-db

  * **Equilibrador de carga interno de Azure**:
    * Con todos los puertos para la instancia ASCS/SCS de Hola y la dirección IP <*SAPSystemSID*> - lb - ascs
    * Con todos los puertos para hello DBMS de SQL Server y la dirección IP <*SAPSystemSID*> - lb - db

  * **Grupo de seguridad de red**: &lt;*SIDSistemaSAP*&gt;-nsg-ascs-0  
    * Con un toohello de puerto de protocolo de escritorio remoto (RDP) externo abierto <*SAPSystemSID*> 0 - ascs - virtual machine

> [!NOTE]
> Todas las direcciones IP de las tarjetas de red de Hola y equilibradores de carga interno de Azure son **dinámica** de forma predeterminada. Cambiarlos demasiado**estático** direcciones IP. Se describe cómo toodo esto más adelante en el artículo de Hola.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Implementar máquinas virtuales con la red corporativa conectividad (entre entornos) toouse en producción
Para los sistemas de producción de SAP, implemente máquinas virtuales de Azure con [conectividad de red corporativa (entre locales)][planning-guide-2.2] mediante el uso de VPN de sitio a sitio de Azure o Azure ExpressRoute.

> [!NOTE]
> Puede usar la instancia de Azure Virtual Network. subred y red virtual de hello ya se crearon y preparados.
>
>

1.  En el portal de Azure, en Hola Hola **parámetros** hoja en hello **NEWOREXISTINGSUBNET** cuadro, seleccione **existente**.
2.  Hola **SUBNETID** , agregue la cadena completa de saludo de la red de Azure preparada SubnetID donde piensa toodeploy máquinas virtuales de Azure.
3.  tooget una lista de todas las subredes de red de Azure, ejecute este comando de PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Hola **identificador** campo muestra hello **SUBNETID**.
4. tooget una lista de todos los **SUBNETID** valores, ejecute este comando de PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Hola **SUBNETID** tiene este aspecto:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Implementación solo en la nube de instancias de SAP para prueba o demostración
Puede implementar el sistema de SAP de alta disponibilidad en un modelo de implementación solo en la nube. Este tipo de implementación se usa principalmente para demostrar o probar casos de uso. No es idóneo para los casos de uso de producción.

- En el portal de Azure, en Hola Hola **parámetros** hoja en hello **NEWOREXISTINGSUBNET** cuadro, seleccione **nueva**. Deje hello **SUBNETID** campo vacío.

  Hola SAP Azure Resource Manager plantilla crea automáticamente Hola subred y red virtual de Azure.

> [!NOTE]
> También debe toodeploy al menos uno dedicado máquina virtual de Active Directory y DNS en Hola la misma instancia de la red Virtual de Azure. plantilla de Hello no crea estas máquinas virtuales.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Preparar la infraestructura de Hola para arquitectura de plantilla de 2

Puede usar esta plantilla de administrador de recursos de Azure para SAP toohelp simplificar la implementación de recursos de la infraestructura necesaria para SAP arquitectura plantilla 2.

Aquí puede obtener las plantillas de Azure Resource Manager para este escenario de implementación:

* [Imagen de Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Imagen de Azure Marketplace con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Imagen personalizada](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Imagen personalizada con Managed Disks](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Preparar la infraestructura de Hola para arquitectura de plantilla de 3

Puede preparar la infraestructura de Hola y configurar SAP para **multi-SID**. Por ejemplo, puede agregar una instancia de ASCS/SCS de SAP adicional en una configuración de clúster *existente*. Para obtener más información, consulte [configurar una instancia de SAP ASCS/SCS adicional en un toocreate de configuración de clúster una configuración de múltiples SID de SAP existente en el Administrador de recursos de Azure][sap-ha-multi-sid-guide].

Si desea toocreate un nuevo clúster de múltiples SID, puede usar Hola multi-SID [plantillas de inicio rápido en GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate un nuevo clúster de múltiples SID, necesita hello toodeploy después de tres plantillas:

* [Plantilla de ASCS/SCS](#ASCS-SCS-template)
* [Plantilla de base de datos](#database-template)
* [Plantilla de servidores de aplicaciones](#application-servers-template)

Hello siguientes secciones contienen más detalles sobre las plantillas de Hola y parámetros de hello necesita tooprovide en las plantillas de Hola.

#### <a name="ASCS-SCS-template"></a>Plantilla de ASCS/SCS

plantilla de Hello ASCS/SCS implementa dos máquinas virtuales que se puede usar un clúster de conmutación por error de Windows Server que hospeda varias instancias ASCS/SCS toocreate.

tooset plantilla Hola ASCS/SCS multi-SID, Hola [plantilla de varias SID ASCS/SCS] [ sap-templates-3-tier-multisid-xscs-marketplace-image] o [plantilla de varias SID ASCS/SCS mediante discos administrados] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], escriba los valores de hello parámetros siguientes:

  - **Prefijo de recurso**.  Establezca el prefijo del recurso de hello, que es usado tooprefix todos los recursos que se crean durante la implementación de Hola. Dado que no pertenecen a recursos de hello tooonly un sistema SAP, el prefijo de hello del recurso de hello no es Hola SID de un sistema SAP.  Hola prefijo debe estar entre **tres y seis caracteres**.
  - **Tipo de pila**. Seleccione el tipo de pila de Hola de hello sistema SAP. Según el tipo de la pila de hello, equilibrador de carga de Azure tiene uno (ABAP o Java solo) o dos (ABAP + Java) las direcciones IP privadas por el sistema SAP.
  -  **Tipo de sistema operativo**. Seleccione sistema de operativo Hola de máquinas virtuales de Hola.
  -  **Recuento de sistema SAP**. Seleccione el número de Hola de sistemas SAP que desee tooinstall en este clúster.
  -  **Disponibilidad del sistema**. Seleccione **Alta disponibilidad**.
  -  **Nombre de usuario y contraseña del administrador**. Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.
  -  **Subred nueva o existente**. Establezca si es necesario crear una red virtual y subred nuevas o si se debe usar una subred existente. Si ya tiene una red virtual que es la red local de tooyour conectado, seleccione **existente**.
  -  **Identificador de subred**. Id. de Hola de conjunto de máquinas virtuales de hello subred toowhich Hola debe estar conectado. Seleccione subred Hola de su red privada virtual (VPN) o red de ExpressRoute red virtual tooconnect Hola máquina virtual tooyour local. Id. de Hello normalmente este aspecto:

   /subscriptions/<*identificador de suscripción*>/resourceGroups/<*nombre del grupo de recursos*>/providers/Microsoft.Network/virtualNetworks/<*nombre de la red virtual*>/subnets/<*nombre de la subred*>

plantilla de Hello implementa una instancia de equilibrador de carga de Azure, lo que es compatible con varios sistemas SAP.

- Hola ASCS se configuran para el número de instancia de 00, 10, 20...
- Hola SCS se configuran para el número de instancia 01, 11, 21...
- Hola ASCS Enqueue Replication Server (ERS) (solamente para Linux) se configuran para el número de instancia 02, 12, 22...
- Hola SCS ERS (solamente para Linux) se configuran para el número de instancia 03, 13, 23...

Hello equilibrador de carga contiene 1 (2 para Linux) VIP(s), 1 x VIP para ASCS/SCS y 1 x VIP para ERS (solamente para Linux).

Hello siguiente lista contiene todas las reglas (donde x es el número de Hola de hello sistema SAP, por ejemplo, 1, 2, 3...) de equilibrio de carga:
- Puertos específicos de Windows para cada sistema SAP 445, 5985
- Puertos ASCS (número de instancia x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016
- Puertos SCS (número de instancia x1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116
- Puertos ASCS ERS en Linux (número de instancia x2): 33x2, 5x213, 5x214, 5x216
- Puertos SCS ERS en Linux (número de instancia x3): 33x3, 5x313, 5x314, 5x316

equilibrador de carga de Hello es hello toouse configurado siguiendo los puertos de sondeo (donde x es el número de Hola de hello sistema SAP, por ejemplo, 1, 2, 3...):
- Puerto de sondeo del equilibrador de carga interno de ASCS/SCS: 620x0
- Puerto de sondeo del equilibrador de carga interno de ERS (solo para Linux): 621x2

#### <a name="database-template"></a> Plantilla de base de datos

plantilla de la base de datos de Hello implementa uno o dos máquinas virtuales que se puede usar tooinstall Hola sistema de administración de bases de datos relacionales (RDBMS) para un sistema SAP. Por ejemplo, si implementa una plantilla de ASCS/SCS de cinco sistemas SAP, debe toodeploy esta plantilla cinco veces.

tooset plantilla de multi-SID de base de datos de Hola Hola [plantilla de SID de varias bases de datos] [ sap-templates-3-tier-multisid-db-marketplace-image] o [plantilla de SID de varias bases de datos mediante discos administrados] [ sap-templates-3-tier-multisid-db-marketplace-image-md], escriba los valores de hello parámetros siguientes:

  -  **Identificador de sistema SAP**. Escriba Hola identificador de hello sistema SAP que desee tooinstall el sistema SAP. Identificador de Hola se utilizará como prefijo para los recursos de Hola que se implementan.
  -  **Tipo de sistema operativo**. Seleccione sistema de operativo Hola de máquinas virtuales de Hola.
  -  **Dbtype**. Seleccione el tipo de saludo de la base de datos de hello desea tooinstall en clúster de Hola. Seleccione **SQL** si desea tooinstall Microsoft SQL Server. Seleccione **HANA** si tiene previsto tooinstall SAP HANA en máquinas virtuales de Hola. Asegúrese de que tooselect Hola tipo de sistema operativo correcto: seleccione **Windows** para SQL y seleccione una distribución de Linux para HANA. Hello equilibrador de carga de Azure que está conectado toohello máquinas virtuales estarán configurar tipo de base de datos de toosupport Hola seleccionado:
    * **SQL**. equilibrador de carga de Hello realizará el puerto 1433 de equilibrio de carga. Asegúrese de que toouse este puerto para la instalación de SQL Server Always On.
    * **HANA**. equilibrador de carga de Hello va a equilibrar la carga de los puertos 35015 y 35017. Asegúrese de que tooinstall SAP HANA con el número de instancia **50**.
    equilibrador de carga de Hello usará el puerto de sondeo 62550.
  -  **Tamaño del sistema SAP**. Número de conjunto de Hola de nuevo sistema de SAPS Hola proporcionará. Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, pregunte al socio de tecnología de SAP o integrador de sistema.
  -  **Disponibilidad del sistema**. Seleccione **Alta disponibilidad**.
  -  **Nombre de usuario y contraseña del administrador**. Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.
  -  **Identificador de subred**. Escriba Hola Id. de subred de Hola que usó durante la implementación de Hola de plantilla ASCS/SCS de Hola o de Hola de subred de Hola que se creó como parte de la implementación de plantilla ASCS/SCS Hola.

#### <a name="application-servers-template"></a>Plantilla de servidores de aplicaciones

plantilla de servidores de aplicación Hola implementa dos o más máquinas virtuales que puede utilizarse como instancias del servidor de aplicaciones de SAP para un sistema SAP. Por ejemplo, si implementa una plantilla de ASCS/SCS de cinco sistemas SAP, debe toodeploy esta plantilla cinco veces.

tooset plantilla de multi-SID en servidores de aplicación de hello, Hola [plantilla de SID de varios servidores de aplicación] [ sap-templates-3-tier-multisid-apps-marketplace-image] o [plantilla de SID de varios servidores de aplicación mediante discos administrados] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], escriba los valores de hello parámetros siguientes:

  -  **Identificador de sistema SAP**. Escriba Hola identificador de hello sistema SAP que desee tooinstall el sistema SAP. Identificador de Hola se utilizará como prefijo para los recursos de Hola que se implementan.
  -  **Tipo de sistema operativo**. Seleccione sistema de operativo Hola de máquinas virtuales de Hola.
  -  **Tamaño del sistema SAP**. número de Hola de nuevo sistema de SAPS Hola proporcionará. Si no estás seguro de sistema de Hola de SAPS cuántos requerirá, pregunte al socio de tecnología de SAP o integrador de sistema.
  -  **Disponibilidad del sistema**. Seleccione **Alta disponibilidad**.
  -  **Nombre de usuario y contraseña del administrador**. Cree un nuevo usuario que puede ser toosign usado en la máquina toohello.
  -  **Identificador de subred**. Escriba Hola Id. de subred de Hola que usó durante la implementación de Hola de plantilla ASCS/SCS de Hola o de Hola de subred de Hola que se creó como parte de la implementación de plantilla ASCS/SCS Hola.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Azure Virtual Network
En nuestro ejemplo, el espacio de direcciones de Hola de hello red virtual de Azure es 10.0.0.0/16. Hay una subred llamada **Subnet**, con un intervalo de direcciones de 10.0.0.0/24. Todas las máquinas virtuales y los equilibradores de carga internos están implementados en esta red virtual.

> [!IMPORTANT]
> No realiza ningún cambio toohello configuración de red dentro de hello sistema operativo. Esto incluye direcciones IP, servidores DNS y subred. Ajuste toda la configuración de red de Azure. Hola servicio de protocolo de configuración dinámica de Host (DHCP) propaga la configuración.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> Direcciones IP de DNS

Hola tooset requiere que direcciones IP de DNS, Hola pasos.

1.  En el portal de Azure, en Hola Hola **servidores DNS** hoja, asegúrese de que la red virtual **servidores DNS** opción se establece demasiado**DNS personalizada**.
2.  Seleccione la configuración en función de tipo de Hola de red que tiene. Para obtener más información, vea Hola recursos siguientes:
    * [Conectividad de red corporativa (entre entornos)][planning-guide-2.2]: agregar las direcciones IP de servidores DNS local Hola Hola.  
    Puede extender local DNS servidores toohello máquinas virtuales que se ejecutan en Azure. En ese caso, puede agregar direcciones IP de Hola de hello Azure máquinas virtuales en el que se ejecuta el servicio DNS Hola.
    * [Implementación solo en la nube][planning-guide-2.1]: implementar una máquina virtual adicional en hello misma instancia de la red Virtual que actúa como un servidor DNS. Agregar direcciones IP de Hola de hello Azure máquinas virtuales que ha configurado el servicio DNS toorun.

    ![Figura 12: Configuración de servidores DNS para Azure Virtual Network][sap-ha-guide-figure-3001]

    _**Figura 12:** Configuración de servidores DNS para Azure Virtual Network_

  > [!NOTE]
  > Si cambia las direcciones IP de servidores DNS de Hola Hola, necesita toorestart Hola máquinas virtuales de Azure tooapply Hola cambio y propagar los nuevos servidores DNS Hola.
  >
  >

En nuestro ejemplo, hello servicio DNS está instalado y configurado en estas máquinas virtuales de Windows:

| Rol de máquina virtual | Nombre de host de máquina virtual | Nombre de tarjeta de red | Dirección IP estática |
| --- | --- | --- | --- |
| Primer servidor DNS |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| Segundo servidor DNS |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Los nombres de host y direcciones IP estáticas para la instancia en clúster de SAP ASCS/SCS de Hola y de instancia en clúster de DBMS

Para la implementación local, necesita estas direcciones IP y nombres de host reservados:

| Rol de nombre de host virtual | Nombre de host virtual | Dirección IP estática virtual |
| --- | --- | --- |
| Primer nombre de host virtual de clúster de ASCS/SCS de SAP (para la administración del clúster) |pr1-ascs-vir |10.0.0.42 |
| Nombre de host virtual de la instancia de ASCS/SCS de SAP |pr1-ascs-sap |10.0.0.43 |
| Segundo nombre de host virtual de clúster de DBMS de SAP (administración del clúster) |pr1-dbms-vir |10.0.0.32 |

Al crear el clúster de hello, crear Hola nombres de host virtual **pr1-ascs-EE.** y **pr1-dbms-EE.** y Hola asociadas direcciones IP que administración el propio clúster Hola. Para obtener información acerca de cómo toodo, vea [recopilar los nodos del clúster en una configuración de clúster][sap-ha-guide-8.12.1].

Puede crear manualmente Hola otros dos nombres de host virtual **pr1-ascs-sap** y **pr1-dbms-sap**, y Hola asociadas direcciones IP, en el servidor DNS de Hola. Hello instancia SAP ASCS/SCS en clúster y la instancia DBMS de hello en clúster usan estos recursos. Para obtener información acerca de cómo toodo, vea [crear un nombre de host virtual para una instancia agrupada de SAP ASCS/SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Conjunto de direcciones IP estáticas para máquinas virtuales SAP de Hola
Después de implementar hello toouse de máquinas virtuales en el clúster, debe tooset las direcciones IP estáticas para todas las máquinas virtuales. Haga esto en la configuración de red Virtual de Azure de hello y no en el sistema operativo de Hola.

1.  Hola portal de Azure, seleccione **grupo de recursos** > **tarjeta de red** > **configuración** > **dirección IP** .
2.  En hello **direcciones IP** hoja, en **asignación**, seleccione **estático**. Hola **dirección IP** cuadro, escriba la dirección IP de Hola que desea toouse.

  > [!NOTE]
  > Si cambia la dirección IP de Hola Hola de tarjeta de red, necesita toorestart Hola máquinas virtuales de Azure tooapply Hola cambio.  
  >
  >

  ![Figura 13: Conjunto de direcciones IP estáticas para la tarjeta de red de Hola de cada máquina virtual][sap-ha-guide-figure-3002]

  _**Figura 13:** establecer direcciones IP estáticas para la tarjeta de red de Hola de cada máquina virtual_

  Repita este paso para todas las interfaces de red, es decir, para todas las máquinas virtuales, incluidas las máquinas virtuales que necesite toouse para el servicio de Active Directory/DNS.

En este ejemplo, aparecen estas máquinas virtuales y direcciones IP estáticas:

| Rol de máquina virtual | Nombre de host de máquina virtual | Nombre de tarjeta de red | Dirección IP estática |
| --- | --- | --- | --- |
| Primer servidor de aplicaciones de SAP |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| Segundo servidor de aplicaciones de SAP |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Último servidor de aplicaciones de SAP |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| Primer nodo de clúster para la instancia de ASCS/SCS |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| Segundo nodo de clúster para la instancia de ASCS/SCS |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| Primer nodo de clúster para la instancia de DBMS |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| Segundo nodo de clúster para la instancia de DBMS |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Establecer una dirección IP estática para el equilibrador de carga interno de Azure Hola

plantilla de SAP Azure Resource Manager Hola crea un equilibrador de carga interno de Azure que se utiliza para el clúster de instancia de SAP ASCS/SCS de Hola y Hola DBMS.

> [!IMPORTANT]
> Hello dirección IP del nombre de host virtual Hola de hello SAP ASCS/SCS es Hola igual como dirección IP de Hola de hello equilibrador de carga interno de SAP ASCS/SCS: **pr1-lb-ascs**.
> Hello dirección IP del nombre virtual de Hola de hello DBMS es Hola igual como dirección IP de Hola de hello equilibrador de carga interno de DBMS: **pr1 lb-dbms**.
>
>

equilibrador de carga de tooset una dirección IP estática para hello Azure interna:

1.  Hello implementación inicial establece dirección IP del equilibrador de carga interno de hello demasiado**dinámica**. En el portal de Azure, en Hola Hola **direcciones IP** hoja, en **asignación**, seleccione **estático**.
2.  Configurar dirección IP de hello del equilibrador de carga interno de hello **pr1-lb-ascs** toohello dirección IP del nombre de host virtual Hola de instancia de SAP ASCS/SCS Hola.
3.  Configurar dirección IP de hello del equilibrador de carga interno de hello **pr1 lb-dbms** toohello dirección IP del nombre de host virtual Hola de instancia DBMS Hola.

  ![Figura 14: Establecer las direcciones IP estáticas para el equilibrador de carga interno de hello para la instancia de SAP ASCS/SCS de Hola][sap-ha-guide-figure-3003]

  _**Figura 14:** configurar direcciones IP estáticas para el equilibrador de carga interno de hello para la instancia de SAP ASCS/SCS Hola_

En este ejemplo, aparecen 2 equilibradores de carga internos de Azure que tienen estas direcciones IP estáticas:

| Rol del equilibrador de carga interno de Azure | Nombre del equilibrador de carga interno de Azure | Dirección IP estática |
| --- | --- | --- |
| Equilibrador de carga interno de instancia de ASCS/SCS de SAP |pr1-lb-ascs |10.0.0.43 |
| Equilibrador de carga interno de DBMS de SAP |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>Reglas para el equilibrador de carga interno de Azure de Hola de equilibrio de carga ASCS/SCS de forma predeterminada

plantilla de SAP Azure Resource Manager Hola crea puertos de Hola que tiene:
* Una instancia de ABAP ASCS, con el número de instancia predeterminado de hello **00**
* Una instancia de Java SCS, con el número de instancia predeterminado de hello **01**

Cuando se instala la instancia de SAP ASCS/SCS, debe utilizar el número de instancia predeterminado de hello **00** para el número de instancia ABAP ASCS hello y la instancia predeterminada **01** para la instancia de Java SCS.

A continuación, crear puntos de conexión para puertos de SAP NetWeaver Hola de equilibrio de carga interno necesario.

toocreate requieren extremos de equilibrio de carga interno, en primer lugar, cree estos extremos para los puertos de SAP NetWeaver ABAP ASCS Hola de equilibrio de carga:

| Nombre de regla de equilibrio de carga/servicio | Números de puerto predeterminados | Puertos concretos para (instancia de ASCS con el número de instancia 00) (ERS con 10) |
| --- | --- | --- |
| Enqueue Server/ *lbrule3200* |32<*NúmeroInstancia*> |3200 |
| ABAP Message Server/ *lbrule3600* |36<*NúmeroInstancia*> |3600 |
| Internal ABAP Message/ *lbrule3900* |39<*NúmeroInstancia*> |3900 |
| Message Server HTTP/ *Lbrule8100* |81<*NúmeroInstancia*> |8100 |
| SAP Start Service ASCS HTTP/ *Lbrule50013* |5<*NúmeroInstancia*>13 |50013 |
| SAP Start Service ASCS HTTPS/ *Lbrule50014* |5<*NúmeroInstancia*>14 |50014 |
| Enqueue Replication/ *Lbrule50016* |5<*NúmeroInstancia*>16 |50016 |
| SAP Start Service ERS HTTP/ *Lbrule51013* |5<*NúmeroInstancia*>13 |51013 |
| SAP Start Service ERS HTTP/ *Lbrule51014* |5<*NúmeroInstancia*>14 |51014 |
| Win RM/ *Lbrule5985* | |5985 |
| File Share/ *Lbrule445* | |445 |

_**Tabla 1:** números de instancias de SAP NetWeaver ABAP ASCS Hola de puerto_

A continuación, cree estos extremos para los puertos de SAP NetWeaver Java SCS Hola de equilibrio de carga:

| Nombre de regla de equilibrio de carga/servicio | Números de puerto predeterminados | Puertos concretos para (instancia de SCS con el número de instancia 01) (ERS con 11) |
| --- | --- | --- |
| Enqueue Server/ *lbrule3201* |32<*NúmeroInstancia*> |3201 |
| Gateway Server/ *lbrule3301* |33<*NúmeroInstancia*> |3301 |
| Java Message Server/ *lbrule3900* |39<*NúmeroInstancia*> |3901 |
| Message Server HTTP/ *Lbrule8101* |81<*NúmeroInstancia*> |8101 |
| SAP Start Service SCS HTTP/ *Lbrule50113* |5<*NúmeroInstancia*>13 |50113 |
| SAP Start Service SCS HTTPS/ *Lbrule50114* |5<*NúmeroInstancia*>14 |50114 |
| Enqueue Replication/ *Lbrule50116* |5<*NúmeroInstancia*>16 |50116 |
| SAP Start Service ERS HTTP/ *Lbrule51113* |5<*NúmeroInstancia*>13 |51113 |
| SAP Start Service ERS HTTPS/ *Lbrule51114* |5<*NúmeroInstancia*>14 |51114 |
| Win RM/ *Lbrule5985* | |5985 |
| File Share/ *Lbrule445* | |445 |

_**Tabla 2:** números de instancias de SAP NetWeaver Java SCS Hola de puerto_

![Figura 15: Reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado ASCS/SCS][sap-ha-guide-figure-3004]

_**Figura 15:** carga predeterminada ASCS/SCS reglas para el equilibrador de carga interno de Azure Hola de equilibrio_

Establecer dirección IP de Hola Hola de equilibrador de carga **pr1 lb-dbms** toohello dirección IP del nombre de host virtual Hola de instancia DBMS Hola.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Cambiar las reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado de hello ASCS/SCS

Si desea toouse un número diferente de Hola SAP ASCS o instancias SCS, debe cambiar Hola nombres y valores de sus puertos de valores predeterminados.

1.  Hola portal de Azure, seleccione  **<* SID*> cargar - lb - ascs equilibrador ** > **reglas de equilibrio de carga**.
2.  Para todas las reglas que pertenezcan toohello SAP ASCS o instancia SCS de equilibrio de la carga, cambiar estos valores:

  * Nombre
  * Port
  * Puerto de back-end

  Por ejemplo, si desea que el número de instancia de toochange Hola predeterminado ASCS de too31 00, necesita cambios de hello toomake para todos los puertos enumerados en la tabla 1.

  A continuación, se muestra un ejemplo de una actualización para el puerto *lbrule3200*.

  ![Figura 16: Cambiar las reglas para el equilibrador de carga interno de Azure Hola de equilibrio de carga de predeterminado de hello ASCS/SCS][sap-ha-guide-figure-3005]

  _**Figura 16:** cambio Hola ASCS/SCS predeterminado equilibrar las reglas para el equilibrador de carga interno de Azure Hola_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Agregar dominio de toohello de máquinas virtuales de Windows

Después de asignar un máquinas de virtuales de toohello de dirección IP estática, agregar dominio toohello de hello máquinas virtuales.

![Figura 17: Agregar un dominio de tooa de máquina virtual][sap-ha-guide-figure-3006]

_**Figura 17:** agregar un dominio de tooa de máquina virtual_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Agregar entradas del registro en ambos nodos del clúster de instancia de SAP ASCS/SCS Hola

Equilibrador de carga de Azure tiene un equilibrador de carga interno que se cierra conexiones cuando las conexiones de hello están inactivas durante un determinado intervalo de tiempo (un tiempo de inactividad). Procesos de trabajo SAP en el cuadro de diálogo instancias conexiones abiertas toohello SAP enqueue procesan tan pronto como Hola primera enqueue y dequeue solicitar toobe necesidades enviado. Estas conexiones normalmente permanecen establecidas hasta que el proceso de trabajo de Hola o reinicios del proceso de poner en cola Hola. Sin embargo, si conexión Hola está inactivo durante un período de tiempo establecido, Hola conexiones Hola de carga interno de Azure equilibrador se cierra. Esto no es un problema porque Hola proceso de trabajo SAP restablece el proceso de poner en cola de hello conexión toohello si ya no existe. Estas actividades se documentan en los seguimientos de desarrollador de Hola de procesos SAP, pero crean una gran cantidad de contenido adicional en los seguimientos. Es un Hola de toochange buena idea TCP/IP `KeepAliveTime` y `KeepAliveInterval` en ambos nodos del clúster. Combinar estos cambios en los parámetros de TCP/IP Hola con parámetros de perfil SAP, que se describe más adelante en el artículo de Hola.

las entradas del registro de tooadd en ambos nodos del clúster de instancia de SAP ASCS/SCS de hello, en primer lugar, agregan estas entradas del registro de Windows en ambos nodos de clúster de Windows para SAP ASCS/SCS:

| Ruta de acceso | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nombre de la variable |`KeepAliveTime` |
| Tipo de variable |REG_DWORD (Decimal) |
| Valor |120000 |
| Vínculo toodocumentation |[https://technet.microsoft.com/es-es/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Tabla 3:** cambio Hola TCP/IP primero_

Luego, agregue estas entradas del Registro de Windows en los nodos de clúster de Windows para ASCS/SCS de SAP:

| path | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Nombre de la variable |`KeepAliveInterval` |
| Tipo de variable |REG_DWORD (Decimal) |
| Valor |120000 |
| Vínculo toodocumentation |[https://technet.microsoft.com/es-es/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Tabla 4:** parámetro cambio Hola de segundo TCP/IP_

**los cambios de hello tooapply, reinicie ambos nodos de clúster**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Configuración del clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP

Para configurar el clúster de Clústeres de conmutación por error de Windows para la instancia de ASCS/SCS de SAP, hay que realizar estas tareas:

- Recopilación de nodos de clúster de hello en una configuración de clúster
- Configuración de un testigo de recurso compartido de archivos de clúster

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Recopilar los nodos de clúster de hello en una configuración de clúster

1.  Hola Add Role y Asistente para características, agregar tooboth nodos del clúster de agrupación en clústeres de conmutación por error.
2.  Configurar el clúster de conmutación por error de hello mediante el Administrador de clústeres de conmutación por error. En el Administrador de clústeres de conmutación por error, seleccione **crear clúster**y, a continuación, agregue solo Hola nombre del primer clúster hello, nodo A. No agregue el segundo nodo de hello aún; podrá agregar Hola segundo nodo en un paso posterior.

  ![Figura 18: Agregar servidor de Hola o un nombre de máquina virtual del primer nodo del clúster Hola][sap-ha-guide-figure-3007]

  _**Figura 18:** los nombre de servidor o una máquina virtual de hello agregar del primer nodo del clúster Hola_

3.  Escriba el nombre de red de hello (nombre de host virtual) de clúster de Hola.

  ![Figura 19: Escriba el nombre del clúster de Hola][sap-ha-guide-figure-3008]

  _**Figura 19:** escriba el nombre de clúster de Hola_

4.  Después de crear el clúster de hello, ejecute una prueba de validación de clúster.

  ![Figura 20: Ejecutar la comprobación de validación de clúster de Hola][sap-ha-guide-figure-3009]

  _**Figura 20:** Ejecutar comprobación de validación de clúster de Hola_

  Puede pasar por alto las advertencias acerca de los discos en este momento en el proceso de Hola. Podrá agregar que un recurso compartido de archivos y Hola SIOS discos comparten más adelante. En esta fase, no es necesario tooworry relacionado con un quórum.

  ![Figura 21: No se encuentra disco de cuórum][sap-ha-guide-figure-3010]

  _**Figura 21:** No se encuentra disco de cuórum_

  ![Figura 22: El recurso de clúster principal necesita una dirección IP nueva][sap-ha-guide-figure-3011]

  _**Figura 22:** El recurso de clúster principal necesita una dirección IP nueva_

5.  Cambiar la dirección IP de hello del servicio de cluster Server core Hola. clúster de Hello no se iniciará hasta que cambie la dirección IP de hello del servicio de Cluster Server core de hello, como dirección IP de saludo del servidor de hello apunta tooone de nodos de la máquina virtual de Hola. Hacer esto en hello **propiedades** página del recurso IP del servicio de Cluster Server de hello core.

  Por ejemplo, necesitamos tooassign una dirección IP (en nuestro ejemplo, **10.0.0.42**) para el nombre de host virtual del clúster de hello **pr1-ascs-EE.**.

  ![Figura 23: En el cuadro de diálogo de propiedades de hello, cambiar la dirección IP de Hola][sap-ha-guide-figure-3012]

  _**Figura 23:** en hello **propiedades** cuadro de diálogo, cambiar dirección IP de Hola_

  ![Figura 24: Asignar dirección IP de Hola que está reservado para el clúster de Hola][sap-ha-guide-figure-3013]

  _**Figura 24:** asignar dirección IP de Hola que está reservado para el clúster de Hola_

6.  Ponga el nombre de host virtual de clúster de hello en línea.

  ![Figura 25: Servicio de Cluster Server core está activo y ejecutándose y con hello corrija la dirección IP][sap-ha-guide-figure-3014]

  _**Figura 25:** servicio de clúster principal está activo y en ejecución y con hello corrija la dirección IP_

7.  Agregue el segundo nodo de clúster Hola.

  Ahora que el servicio de Cluster Server core de hello está en funcionamiento, puede agregar el segundo nodo de clúster Hola.

  ![Ilustración 26: Agregar Hola segundo nodo de clúster][sap-ha-guide-figure-3015]

  _**Ilustración 26:** segundo nodo de clúster de agregar Hola_

8.  Escriba un nombre de host del nodo de clúster segundo Hola.

  ![Figura 27: Escriba el nombre de host de nodo de segundo clúster de Hola][sap-ha-guide-figure-3016]

  _**Figura 27:** ENTRAR Hola segundo clúster host nombre de nodo_

  > [!IMPORTANT]
  > Asegúrese de que hello **agregar todo el almacenamiento apto toohello clúster** casilla de verificación está **no** seleccionado.  
  >
  >

  ![Figura 28: No seleccione la casilla de verificación de Hola][sap-ha-guide-figure-3017]

  _**Figura 28:** hacer **no** seleccione Hola casilla de verificación_

  Puede pasar por alto las advertencias sobre el cuórum y los discos. Se configuran Hola quórum y recurso compartido de hello el disco de una versión posterior, como se describe en [instalar SIOS DataKeeper Cluster Edition para el disco del recurso compartido de clúster de SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Figura 29: Ignorar las advertencias sobre el quórum de disco Hola][sap-ha-guide-figure-3018]

  _**Figura 29:** ignorar las advertencias sobre el quórum de disco Hola_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Configuración de un testigo de recurso compartido de archivos de clúster

Para configurar un testigo de recurso compartido de archivos de clúster, hay que realizar las siguientes tareas:

- Creación de un recurso compartido de archivos
- Configuración de quórum de testigo de recurso compartido de archivos de hello en el Administrador de clústeres de conmutación por error

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Creación de un recurso compartido de archivos

1.  Seleccione un testigo de recurso de archivos en lugar de un disco de cuórum. SIOS DataKeeper admite esta opción.

  En los ejemplos de hello en este artículo, Hola testigo de recurso compartido de archivos está en hello Active Directory o servidor DNS que se ejecuta en Azure. Hello testigo de recurso compartido de archivo se denomina **domcontr-0**. Dado que habría configuró un tooAzure de conexión VPN (a través de VPN de sitio a sitio o ExpressRoute de Azure), su Active Directory/DNS service es local y no es adecuado toorun un archivo de testigo de recurso compartido.

  > [!NOTE]
  > Si el servicio de Active Directory/DNS ejecuta solo en local, no configure el testigo de recurso compartido de archivo hello Active Directory y DNS en sistemas operativos en que se ejecuta en local. La latencia de red entre los nodos de clúster que se ejecutan en Azure y Active Directory/DNS local puede ser demasiado grande y provocar problemas de conectividad. Ser seguro tooconfigure Hola archivo testigo de recurso compartido en una máquina virtual de Azure que está ejecutando el nodo del clúster toohello cerrar.  
  >
  >

  unidad de quórum de Hello necesita al menos 1024 MB de espacio libre. Se recomienda 2.048 MB de espacio libre para la unidad de quórum de Hola.

2.  Agregue el objeto de nombre de clúster de Hola.

  ![Figura 30: Asignar permisos de hello en recurso compartido de hello para el objeto de nombre de clúster de Hola][sap-ha-guide-figure-3019]

  _**Figura 30:** asignar permisos de hello en el recurso compartido de hello para el objeto de nombre de clúster de Hola_

  Asegúrese de que los permisos de hello incluyen datos de la CA toochange hello en recurso compartido de hello para el objeto de nombre de clúster de hello (en nuestro ejemplo, **pr1-ascs-EE. $**).

3.  tooadd Hola clúster nombre toohello lista de objetos, seleccione **agregar**. Cambiar hello toocheck de filtro para los objetos de equipo, en toothose de suma que se muestra en la figura 31.

  ![Figura 31: Cambia los equipos de tooinclude de tipos de objeto de Hola][sap-ha-guide-figure-3020]

  _**Figura 31:** cambia los equipos de tooinclude de tipos de objeto de Hola_

  ![Figura 32: Active la casilla de verificación de los equipos de Hola][sap-ha-guide-figure-3021]

  _**Figura 32:** Hola seleccione **equipos** casilla de verificación_

4.  Especifique el objeto de nombre de clúster de hello tal y como se muestra en la figura 31. Porque ya se ha creado el registro de hello, puede cambiar los permisos de hello, tal como se muestra en la figura 30.

5.  Seleccione hello **seguridad** ficha del recurso compartido de hello y, después, establezca más detallados permisos de objeto de nombre de clúster de Hola.

  ![Figura 33: Establecer atributos de seguridad de hello para el objeto de nombre de clúster de hello en el quórum de recurso compartido de archivos de Hola][sap-ha-guide-figure-3022]

  _**Figura 33:** establecer atributos de seguridad de hello para el objeto de nombre de clúster de hello en el quórum de recurso compartido de archivos de Hola_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Establecer en el Administrador de clústeres de conmutación por error de quórum de testigo de recurso compartido de archivos de Hola

1.  Abra Hola Asistente de configuración de quórum de configuración.

  ![Figura 34: Hola Asistente de configuración de quórum de clúster de configuración de inicio][sap-ha-guide-figure-3023]

  _**Figura 34:** inicio Hola configurar Asistente de configuración de quórum de clúster_

2.  En hello **Seleccionar configuración de quórum** , seleccione **seleccionar testigo de quórum de hello**.

  ![Figura 35: Configuraciones de cuórum que puede elegir][sap-ha-guide-figure-3024]

  _**Figura 35:** Configuraciones de cuórum que puede elegir_

3.  En hello **seleccionar testigo de quórum** , seleccione **configurar un testigo de recurso compartido de archivos**.

  ![Figura 36: Testigo de recurso compartido de archivo Hola Select][sap-ha-guide-figure-3025]

  _**Figura 36:** seleccionar testigo de recurso compartido de archivos de Hola_

4.  Escriba Hola ruta de acceso toohello recurso compartido UNC (en nuestro ejemplo, \\domcontr 0\FSW). una lista de cambios de Hola que puede realizar, seleccione toosee **siguiente**.

  ![Figura 37: Definir la ubicación del recurso compartido de archivo hello para el recurso compartido de testigo de Hola][sap-ha-guide-figure-3026]

  _**Figura 37:** definir la ubicación del recurso compartido de archivo hello para el recurso compartido de testigo de Hola_

5.  Seleccione Hola cambios que desee y, a continuación, seleccione **siguiente**. Necesita toosuccessfully volver a configurar la configuración de clúster de hello tal como se muestra en la figura 38.  

  ![Figura 38: Confirmación que ha configurado de nuevo clúster Hola][sap-ha-guide-figure-3027]

  _**Figura 38:** confirmación de que ha configurado de nuevo clúster Hola_

Después de instalar correctamente el clúster de conmutación por error de Windows hello, cambios necesitan toobe realizado tooconditions de detección de conmutación por error de toosome umbrales tooadapt en Azure. Hello toobe parámetros cambiado documentados en este blog: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. Si damos por hecho que los dos máquinas virtuales que generar Hola configuración de clúster de Windows para ASCS/SCS están en Hola misma subred, los parámetros siguientes hello necesitan toobe cambiado toothese valores:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Esta configuración se han probado con los clientes y proporciona un toobe buen compromiso suficientemente resistente en el lado "uno" Hola. En hello otra parte dicha configuración proporciona rápido suficiente conmutación por error en las condiciones de error real en caso de error de software o nodo/VM de SAP. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Instalar SIOS DataKeeper Cluster Edition para el disco del recurso compartido de clúster de hello SAP ASCS/SCS

Ahora tiene una configuración de Clústeres de conmutación por error de Windows Server activa en Azure. Pero, tooinstall una instancia de SAP ASCS/SCS, necesita un recurso de disco compartido. No se puede crear recursos de disco de Hola compartido que necesita en Azure. SIOS DataKeeper Cluster Edition es una solución de terceros pueden usar recursos de disco de toocreate compartido.

Instalar SIOS DataKeeper Cluster Edition para hello SAP ASCS/SCS disco del recurso compartido de clúster implica estas tareas:

- Agregar Hola .NET Framework 3.5
- Instalación de SIOS DataKeeper
- Configuración de SIOS DataKeeper

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Agregar Hola .NET Framework 3.5
Hola Microsoft .NET Framework 3.5 automáticamente no está activado o instalado en Windows Server 2012 R2. Dado que SIOS DataKeeper requiere toobe de .NET Framework de hello en todos los nodos que se instala DataKeeper en, debe instalar Hola .NET Framework 3.5 en hello sistema operativo de todas las máquinas virtuales en clúster de Hola.

Hay dos Hola de tooadd maneras .NET Framework 3.5:

- Utilice Hola agregar Roles y características de Asistente de Windows como se muestra en la Figura 39.

  ![Figura 39: Instalar Hola .NET Framework 3.5 mediante Hola agregar Roles y características de Asistente][sap-ha-guide-figure-3028]

  _**Figura 39:** Hola de instalar .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente_

  ![La figura 40: Progreso de la instalación barra cuando instala Hola .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente][sap-ha-guide-figure-3029]

  _**Figura 40:** barra cuando instala Hola .NET Framework 3.5 mediante el uso de hello agregar Roles y características de Asistente de progreso de instalación_

- Usar dism.exe de la herramienta de línea de comandos de Hola. Para este tipo de instalación, deberá directorio tooaccess Hola SxS Hola medios de instalación de Windows. En un símbolo del sistema con privilegios elevados, escriba:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> Instalación de SIOS DataKeeper

Instale SIOS DataKeeper Cluster Edition en cada nodo de clúster de Hola. almacenamiento compartido virtual de toocreate con SIOS DataKeeper, crear un espejo sincronizado y, a continuación, simular almacenamiento compartido de clúster.

Antes de instalar software SIOS hello, cree el usuario del dominio de hello **DataKeeperSvc**.

> [!NOTE]
> Agregar hello **DataKeeperSvc** usuario toohello **administrador Local** grupo en ambos nodos del clúster.
>
>

tooinstall SIOS DataKeeper:

1.  Instalar software SIOS hello en ambos nodos del clúster.

  ![Instalador de SIOS][sap-ha-guide-figure-3030]

  ![Figura 41: La primera página de hello instalación SIOS DataKeeper][sap-ha-guide-figure-3031]

  _**Figura 41:** primera página de hello instalación SIOS DataKeeper_

2.  En el cuadro de diálogo de Hola se muestra en la Figura 42, seleccione **Sí**.

  ![Figura 42: DataKeeper le informa que se deshabilitará un servicio][sap-ha-guide-figure-3032]

  _**Figura 42:** DataKeeper le informa que se deshabilitará un servicio_

3.  En el cuadro de diálogo de Hola se muestra en figura 43, le recomendamos que seleccione **cuenta de dominio o servidor**.

  ![Figura 43: Selección del usuario para SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Figura 43:** Selección del usuario para SIOS DataKeeper_

4.  Escriba el nombre de usuario de cuenta de dominio de Hola y las contraseñas que ha creado para SIOS DataKeeper.

  ![Figura 44: Escriba nombre de usuario de dominio de hello y una contraseña para hello instalación SIOS DataKeeper][sap-ha-guide-figure-3034]

  _**Figura 44:** escriba nombre de usuario de dominio de hello y una contraseña para hello instalación SIOS DataKeeper_

5.  Instale la clave de licencia de hello para la instancia de SIOS DataKeeper tal y como se muestra en figura 45.

  ![Figura 45: Ingreso de la licencia de SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Figura 45:** Especificación de la licencia de SIOS DataKeeper_

6.  Cuando se le solicite, reinicie la máquina virtual de Hola.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Configuración de SIOS DataKeeper

Después de instalar SIOS DataKeeper en ambos nodos, necesita una configuración toostart Hola. objetivo de Hola de configuración de hello es toohave la replicación de datos sincrónica entre discos adicionales de hello adjunta tooeach de máquinas virtuales de Hola.

1.  Inicie hello DataKeeper administración y herramienta de configuración y, a continuación, seleccione **conectar servidor**. (En la figura 46, esta opción aparece rodeada de un círculo de color rojo).

  ![Figura 46: Herramienta de configuración y administración de SIOS DataKeeper][sap-ha-guide-figure-3036]

  _**Figura 46:** Herramienta de configuración y administración de SIOS DataKeeper_

2.  Escriba el nombre de Hola o dirección TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y, en una segunda fase, el segundo nodo de Hola.

  ![Figura 47: Nombre de Hola de inserción o la dirección de TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y en un segundo paso, el segundo nodo de Hola][sap-ha-guide-figure-3037]

  _**Figura 47:** nombre de Hola de inserción o la dirección de TCP/IP de hello primer nodo Hola administración herramienta de configuración y debe conectarse a y en un segundo paso, el segundo nodo de Hola_

3.  Crear trabajo de replicación de hello entre dos nodos de Hola.

  ![Figura 48: Creación de un trabajo de replicación][sap-ha-guide-figure-3038]

  _**Figura 48:** Creación de un trabajo de replicación_

  Un asistente le guía a través del proceso de Hola de creación de un trabajo de replicación.
4.  Definir nombre de hello, la dirección TCP/IP y el volumen de disco Hola del nodo de origen.

  ![Figura 49: Definir nombre de Hola de trabajo de replicación de Hola][sap-ha-guide-figure-3039]

  _**Figura 49:** Definir nombre de Hola de trabajo de replicación de Hola_

  ![Figura 50: Definir datos de base de Hola de nodo de hello, que debe ser el nodo de origen actual de Hola][sap-ha-guide-figure-3040]

  _**Figura 50:** definir datos de base de Hola de nodo de hello, que debe ser el nodo de origen actual de Hola_

5.  Definir nombre hello, dirección TCP/IP y el volumen de disco de nodo de destino de Hola.

  ![Figura 51: Definir datos de base de Hola de nodo de hello, que debe ser el nodo de destino actual de Hola][sap-ha-guide-figure-3041]

  _**Figura 51:** definir datos de base de Hola de nodo de hello, que debe ser el nodo de destino actual de Hola_

6.  Definir los algoritmos de compresión de Hola. En nuestro ejemplo, le recomendamos que comprima el flujo de replicación de Hola. Especialmente en situaciones de resincronización, compresión de Hola de flujo de replicación de hello reduce considerablemente el tiempo de resincronización. Tenga en cuenta que la compresión utiliza recursos de CPU y RAM Hola de una máquina virtual. A medida que aumenta la velocidad de compresión de hello, por lo que Hola volumen de recursos de CPU que se usa. También puede ajustar esta configuración más adelante.

7.  Otra configuración necesita toocheck es si se produce la replicación Hola sincrónica o asincrónica. *Cuando proteja las configuraciones de ASCS/SCS de SAP, debe usar la replicación sincrónica*.  

  ![Figura 52: Definición de los detalles de la replicación][sap-ha-guide-figure-3042]

  _**Figura 52:** Definición de los detalles de la replicación_

8.  Definir si volumen Hola que se replica mediante replicación Hola debe ser la configuración de clúster de clústeres de conmutación por error de Windows Server de tooa representado como un disco compartido. Para la configuración de SAP ASCS/SCS de hello, seleccione **Sí** para que Windows hello clúster ve Hola replicada volumen como un disco compartido que puede usar como un volumen de clúster.

  ![Figura 53: Seleccione la opción Sí tooset Hola replica volumen como un volumen de clúster][sap-ha-guide-figure-3043]

  _**Figura 53:** seleccione **Sí** tooset Hola replica volumen como volumen de clúster_

  Después de crea el volumen de hello, herramienta de configuración y administración de DataKeeper de hello muestra que ese trabajo de replicación Hola está activo.

  ![Figura 54: DataKeeper sincrónica creación de reflejo de disco del recurso compartido de SAP ASCS/SCS Hola está activo][sap-ha-guide-figure-3044]

  _**Figura 54:** DataKeeper creación de reflejos sincrónica para SAP ASCS/SCS hello compartir disco está activo_

  El Administrador de clústeres de conmutación por error muestra ahora disco Hola como un disco DataKeeper, tal como se muestra en la figura 55.

  ![Figura 55: Muestra el Administrador de clústeres de conmutación por error de disco Hola que replican DataKeeper][sap-ha-guide-figure-3045]

  _**Figura 55:** Administrador de clústeres de conmutación por error muestra disco Hola ese DataKeeper replicado_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Instalar el sistema de SAP NetWeaver Hola

No describimos el programa de instalación DBMS de hello porque configuraciones varían en función hello sistema DBMS que use. Sin embargo, se supone que se solucionan los problemas de alta disponibilidad con hello DBMS con funcionalidades de hello admiten distintos proveedores DBMS Hola de Azure. Por ejemplo, AlwaysOn o creación de reflejo de la base de datos para SQL Server y Oracle Data Guard para Oracle. En el escenario de Hola que se usa en este artículo, no agregamos más protección toohello DBMS.

No hay ninguna consideración especial cuando distintos servicios de DBMS interactúan con esta variante de configuración de ASCS/SCS de SAP en clúster en Azure.

> [!NOTE]
> procedimientos de instalación de Hola de sistemas de ABAP de SAP NetWeaver, sistemas de Java y sistemas ABAP + Java son casi idénticos. diferencia más importante de Hello es que un sistema SAP ABAP tiene una instancia ASCS. Hola sistema SAP Java tiene una instancia SCS. Hola sistema SAP ABAP + Java tiene una instancia ASCS y ejecuta en una instancia SCS Hola mismo grupo de clústeres de conmutación por error de Microsoft. Cualquier diferencia de instalación de cada pila de instalación de SAP NetWeaver se menciona explícitamente. Se puede suponer que se Hola a todos los demás elementos iguales.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Instalación de SAP con una instancia de ASCS/SCS de alta disponibilidad

> [!IMPORTANT]
> Asegúrese de no tooplace la página de archivos en DataKeeper volúmenes reflejados. DataKeeper no admite los volúmenes reflejados. Puede dejar el archivo de paginación en la unidad temporal de hello D de una máquina virtual de Azure, que es el valor predeterminado de Hola. Si aún no está allí, mueva Hola Windows página archivo toodrive D: de la máquina virtual de Azure.
>
>

Para instalar SAP con una instancia de ASCS/SCS de alta disponibilidad, siga estos pasos:

- Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster
- Instalar el primer nodo de clúster de hello SAP
- Modificar perfil de SAP de Hola de instancia de hello ASCS/SCS
- Incorporación de un puerto de sondeo
- Abrir el puerto de sondeo de firewall de Windows hello

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Crear un nombre de host virtual para la instancia de SAP ASCS/SCS de hello en clúster

1.  En el Administrador de DNS de Windows hello, cree una entrada DNS para el nombre de host virtual Hola de instancia de hello ASCS/SCS.

  > [!IMPORTANT]
  > Hello dirección IP que asigna el nombre de host virtual toohello de hello ASCS/SCS instancia debe ser Hola igual como dirección IP de Hola que asigna tooAzure equilibrador de carga (**<*SID*> - lb - ascs **).  
  >
  >

  Hola dirección IP del nombre de host de SAP ASCS/SCS virtual hello (**pr1-ascs-sap**) Hola igual como dirección IP de hello del equilibrador de carga de Azure (**pr1-lb-ascs**).

  ![Figura 56: Definir la entrada DNS de hello para el nombre virtual del clúster de SAP ASCS/SCS hello y dirección TCP/IP][sap-ha-guide-figure-3046]

  _**Figura 56:** definir Hola entrada DNS para el nombre virtual del clúster de SAP ASCS/SCS hello y una dirección TCP/IP_

2.  toodefine Hola IP dirección asignada toohello nombre de host virtual, seleccione **el Administrador de DNS** > **dominio**.

  ![Figura 57: Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP][sap-ha-guide-figure-3047]

  _**Figura 57:** Nuevo nombre virtual y dirección TCP/IP para la configuración del clúster de ASCS/SCS de SAP_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Instalar el primer nodo de clúster de hello SAP

1.  Ejecutar Hola primera opción de nodo de clúster en el nodo de clúster a Por ejemplo, en hello **pr1-ascs-0** host.
2.  puertos predeterminados que hello tookeep para hello Azure interno equilibrador de carga, seleccione:

  * **Sistema ABAP**: número de instancia de **ASCS****00**
  * **Sistema Java**: número de instancia de **SCS****01**
  * **Sistema ABAP+Java**: número de instancia de **ASCS****00** y número de instancia de **SCS****01**

  instancia de toouse números distinto de 00 para hello ABAP ASCS 01 para la instancia de Java SCS de Hola e instancia, en primer lugar debe toochange Hola carga interno de Azure equilibrador predeterminado equilibrio de carga, se describe en [carga predeterminada de cambio Hola ASCS/SCS reglas para el equilibrador de carga interno de Azure Hola de equilibrio][sap-ha-guide-8.9].

Hello siguientes algunas tareas no se describen en la documentación de instalación de SAP estándar Hola.

> [!NOTE]
> Hola documentación de la instalación de SAP describe cómo tooinstall Hola primer nodo del clúster ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Modificar perfil SAP de Hola de instancia de hello ASCS/SCS

Deberá tooadd un nuevo parámetro de perfil. parámetro del perfil Hola evita que las conexiones entre los procesos de trabajo SAP y el servidor de poner en cola Hola cierre cuando están inactivos durante demasiado tiempo. Hemos mencionado escenario de problema de hello en [agregar entradas del registro en ambos nodos del clúster de instancia de SAP ASCS/SCS de hello][sap-ha-guide-8.11]. En esa sección, también presentamos dos cambios toosome básica TCP/IP parámetros de conexión. En un segundo paso, necesita tooset Hola enqueue server toosend un `keep_alive` de señal para que las conexiones de hello no supere el umbral de inactividad del equilibrador de carga interno de Azure Hola.

Hola toomodify perfil SAP de instancia ASCS/SCS de hello:

1.  Agregue este toohello de parámetro perfil de la instancia de SAP ASCS/SCS de perfil:

  ```
  enque/encni/set_so_keepalive = true
  ```
  En nuestro ejemplo, ruta de acceso de hello es:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Por ejemplo, perfil de instancia de toohello SCS de SAP y ruta de acceso correspondiente:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  cambios de hello tooapply, reinicie la instancia de SAP ASCS /SCS de Hola.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Incorporación de un puerto de sondeo

Use el trabajo de la configuración del equilibrador de carga interno de hello sondeo funcionalidad toomake Hola todo el clúster con el equilibrador de carga de Azure. equilibrador de carga interno de Azure Hola normalmente distribuye la carga de trabajo entrante de Hola por igual entre las máquinas virtuales participantes. Sin embargo, esto no funcionará en algunas configuraciones de clúster porque solo hay una instancia activa. Hola otra instancia es pasivo y no puede aceptar cualquier carga de trabajo de Hola. Le ayuda una funcionalidad de sondeo cuando asigna de equilibrador de carga interno de Azure de hello trabajan tooan solo de instancias activas. Con la funcionalidad de sondeo de hello, equilibrador de carga interno de hello puede detectar las instancias que están activas y, a continuación, solo el Hola instancia con cargas de trabajo de Hola de destino.

tooadd un puerto de sondeo:

1.  Comprobar Hola actual **ProbePort** configuración ejecutando el siguiente comando de PowerShell de Hola. Ejecutarlo desde dentro de una de las máquinas virtuales de hello en configuración de clúster de Hola.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Defina un puerto de sondeo. número de puerto de sondeo de Hello predeterminada es **0**. En el ejemplo, se usa el puerto de sondeo **62000**.

  ![Figura 58: puerto de sondeo de configuración de clúster de hello es 0 de forma predeterminada][sap-ha-guide-figure-3048]

  _**Figura 58:** puerto de sondeo de configuración de clúster de hello predeterminado es 0_

  número de puerto de Hola se define en plantillas de SAP Azure Resource Manager. Puede asignar el número de puerto de hello en PowerShell.

  un nuevo valor de ProbePort para hello tooset  **SAP <*SID*> IP ** recurso de clúster, ejecute el siguiente script de PowerShell de Hola. Actualice las variables de PowerShell de Hola para su entorno. Después de ejecutar el script de Hola, podrá toorestart solicitadas Hola SAP clúster grupo tooactivate Hola cambios.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  Después de conectar hello  **SAP <*SID*> ** clúster en línea, compruebe que **ProbePort** se establece toohello nuevo valor.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Figura 59: Sondeo de puerto de clúster de hello después de establecer el nuevo valor de Hola][sap-ha-guide-figure-3049]

  _**Figura 59:** sondeo de puerto de clúster de hello después de establecer el nuevo valor de Hola_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Abra el puerto de sondeo de firewall de Windows hello

Deberá tooopen un puerto de sondeo de firewall de Windows en ambos nodos del clúster. Usar hello sigue la secuencia de comandos tooopen un puerto de sondeo de firewall de Windows. Actualice las variables de PowerShell de Hola para su entorno.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Hola **ProbePort** se establece demasiado**62000**. Ahora puede tener acceso a recurso compartido de archivos de hello  **\\\ascsha-clsap\sapmnt** de otros hosts, tales como from **ascsha DBA**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Instalar la instancia de base de datos de Hola

base de datos de tooinstall Hola instancia, siga el proceso de hello descrito en hello documentación de la instalación de SAP.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Instalar el segundo nodo de clúster Hola

tooinstall Hola segundo clúster, siga los pasos de Hola Hola Guía de instalación de SAP.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Cambiar tipo de inicio de Hola de instancia de servicio de SAP ERS Windows hello

Cambiar el tipo de inicio de Hola de hello servicio SAP ERS Windows demasiado**automático (Inicio retrasado)** en ambos nodos del clúster.

![Figura 60: Cambiar el tipo de servicio de Hola para hello SAP ERS instancia toodelayed automática][sap-ha-guide-figure-3050]

_**Figura 60:** cambiar tipo de servicio de Hola de hello SAP ERS instancia toodelayed automática_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Instalar Hola servidor principal de aplicaciones de SAP

Instalar la instancia de servidor de aplicación principal (PAS) Hola <*SID*> - di - 0 en la máquina virtual de Hola que ha designado toohost Hola PA. No hay ninguna dependencia de Azure ni aspectos específicos de DataKeeper.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Instalar Hola adicional servidor de aplicaciones SAP

Instalar un servidor de aplicación adicionales (AAS) de SAP en todas las máquinas virtuales de Hola que ha designado toohost una instancia de servidor de aplicaciones SAP. Por ejemplo, en <*SID*> - di - 1 demasiado <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Esto finaliza la instalación de Hola de un sistema SAP NetWeaver de alta disponibilidad. Después, continúe con las pruebas de conmutación por error.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Probar la replicación de SIOS y conmutación por error de hello SAP ASCS/SCS instancia
Es fácil tootest y supervisar una instancia de SAP ASCS/SCS conmutación por error y replicación de disco SIOS mediante el Administrador de clústeres de conmutación por error y la herramienta de configuración y administración de SIOS DataKeeper de Hola.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> La instancia de ASCS/SCS de SAP se ejecuta en el nodo de clúster A

Hola **PR1 de SAP** grupo de clúster se ejecuta en el nodo de clúster A. Por ejemplo, en **pr1-ascs-0**. Asignar la unidad de disco de hello compartido S, que forma parte del programa Hola a **PR1 de SAP** grupo de clúster, y qué instancia ASCS/SCS hello usa, toocluster nodo A.

![Figura 61: El Administrador de clústeres de conmutación por error: grupo de clústeres SAP < SID > Hola se ejecuta en el nodo de clúster A][sap-ha-guide-figure-5000]

_**Figura 61:** Administrador de clústeres de conmutación por error: Hola SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster A_

En hello SIOS DataKeeper administración y herramienta de configuración, puede ver ese disco compartido Hola datos se replican de forma sincrónica de la unidad de volumen de origen Hola S en el nodo de clúster de una unidad de volumen de destino toohello S en el nodo de clúster B. Por ejemplo, se replique desde **pr1-ascs-0 [10.0.0.40]** demasiado**pr1-ascs-1 [10.0.0.41]**.

![Figura 62: En SIOS DataKeeper, replicar volumen local Hola desde el nodo de clúster un nodo toocluster B][sap-ha-guide-figure-5001]

_**Figura 62:** en DataKeeper de SIOS, replicar volumen local Hola desde el nodo de clúster un nodo toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Conmutación por error de nodo A toonode B

1.  Elija una de estas opciones tooinitiate una conmutación por error de hello SAP <*SID*> grupo de clúster de nodo de clúster nodo A toocluster B:
  - Uso del Administrador de clústeres de conmutación por error  
  - Uso de PowerShell del clúster de conmutación por error

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Reinicie el nodo de clúster A sistema de operativo de invitado de Windows hello (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).  
3.  Reinicie el nodo de clúster A de hello portal de Azure (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).  
4.  Reinicie un nodo de clúster mediante el uso de PowerShell de Azure (este comando inicia una conmutación por error automática del programa Hola a SAP <*SID*> grupo de clúster de nodo A toonode B).

  Después de la conmutación por error, Hola SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster B. Por ejemplo, se está ejecutando en **pr1-ascs-1**.

  ![Figura 63: En el Administrador de clústeres de conmutación por error, grupo de clústeres SAP < SID > Hola se ejecuta en el nodo de clúster B][sap-ha-guide-figure-5002]

  _**Figura 63**: conmutación por error de administrador de clústeres de hello SAP <*SID*> grupo de clúster se ejecuta en el nodo de clúster B_

  Hello disco compartido está ahora montado en clúster de nodo B. SIOS DataKeeper es replicar datos de la unidad de volumen de origen S en el nodo B tootarget volumen unidad agrupada S en el nodo de clúster A. Por ejemplo, está replicando de **pr1-ascs-1 [10.0.0.41]** demasiado**pr1-ascs-0 [10.0.0.40]**.

  ![Figura 64: SIOS DataKeeper replica volumen local Hola del clúster B toocluster nodo A][sap-ha-guide-figure-5003]

  _**Figura 64:** SIOS DataKeeper replica volumen local Hola del nodo de clúster nodo B toocluster A_
