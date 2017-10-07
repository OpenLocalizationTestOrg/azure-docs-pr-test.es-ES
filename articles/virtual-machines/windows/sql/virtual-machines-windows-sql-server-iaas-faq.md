---
title: "aaaSQL Server en máquinas virtuales de Azure preguntas más frecuentes | Documentos de Microsoft"
description: "Este artículo ofrecen respuestas toofrequently preguntas más frecuentes sobre la ejecución de SQL Server en máquinas virtuales de Azure."
services: virtual-machines-windows
documentationcenter: 
author: v-shysun
manager: felixwu
editor: 
tags: azure-service-management
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: v-shysun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70a8777bf765dcc69f433aa1fb59eb94929caab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-sql-server-on-azure-virtual-machines"></a>Preguntas más frecuentes para SQL Server en Azure Virtual Machines
Este tema proporcionan respuestas toosome de hello preguntas más frecuentes acerca de cómo ejecutar [SQL Server en máquinas virtuales Azure](https://azure.microsoft.com/services/virtual-machines/sql-server/).

[!INCLUDE [support-disclaimer](../../../../includes/support-disclaimer.md)]

## <a name="frequently-asked-questions"></a>Preguntas frecuentes

1. **¿Cómo puedo crear una máquina virtual de Azure con SQL Server?**

    solución más fácil de Hello es toocreate una máquina Virtual que incluye SQL Server. Para obtener un tutorial sobre cómo suscribirse a Azure y crear una VM de SQL desde el portal de hello, consulte [aprovisionar una máquina virtual de SQL Server en el Portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md). Puede seleccionar una imagen de máquina virtual que usa SQL Server de pago por minuto de licencias, o puede utilizar una imagen que le permite toobring su propia licencia de SQL Server. También tiene Hola opción de instalación de SQL Server en una máquina virtual manualmente y volver a usar una licencia local. Si trae su propia licencia, debe disponer de [Movilidad de Licencias a través de Software Assurance en Azure](https://azure.microsoft.com/pricing/license-mobility/). Para más información, vea [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Orientación de precios de máquinas virtuales de SQL Server Azure).

1. **¿Cuál es la diferencia de hello entre máquinas virtuales de SQL y Hola servicio de base de datos SQL?**

    De manera conceptual, ejecutar SQL Server en una máquina virtual de Azure no es diferente a ejecutar SQL Server en un centro de datos remoto. En cambio, [SQL Database](../../../sql-database/sql-database-technical-overview.md) ofrece base de datos como servicio. Con la base de datos de SQL, no es necesario acceder a toohello máquinas que hospedan las bases de datos. Para ver una comparación completa, consulte [Selección de una opción de SQL Server en la nube: Azure SQL (PaaS) Database o SQL Server en máquinas virtuales de Azure (IaaS)](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md).

1. **¿Cómo puedo migrar mi toohello de base de datos de SQL Server local en la nube?**

    En primer lugar, cree una máquina virtual de Azure con una instancia de SQL Server. A continuación, migrar la instancia de toothat de las bases de datos local. Para las estrategias de migración de datos, vea [migrar un tooSQL de base de datos de servidor de SQL Server en una máquina virtual de Azure](virtual-machines-windows-migrate-sql.md).

1. **¿Se puede instalar una segunda instancia de SQL Server en hello misma máquina virtual? ¿Se puede cambiar las características instaladas de la instancia predeterminada de hello?**

    Sí. Hola medios de instalación de SQL Server se encuentra en una carpeta en hello **C** unidad. Ejecutar **Setup.exe** desde esa ubicación tooadd nuevas instancias o SQL Server toochange otros instala características de SQL Server en la máquina de Hola. Tenga en cuenta que algunas características, como copia de seguridad automatizada, la aplicación de revisiones automatizada y la integración del almacén de claves de Azure, solo funcionan con la instancia predeterminada de Hola.

1. **¿Se puede desinstalar la instancia predeterminada de Hola de SQL Server?**

    Sí. Pero hay algunas consideraciones. Como se indica en la respuesta anterior de hello, características que se basan en hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md) solo funcionan en la instancia predeterminada de Hola. Si desinstala la instancia predeterminada de hello, extensión de hello continúa toolook para ella y puede generar errores de registro de eventos. Estos errores son de hello siguientes dos orígenes: **administración de credenciales de Microsoft SQL Server** y **agente de IaaS de Microsoft SQL Server**. Uno de los errores de hello podría ser similar siguiente toohello:
    
        A network-related or instance-specific error occurred while establishing a connection tooSQL Server. hello server was not found or was not accessible. 
        
    Si decide instancia predeterminada de toouninstall hello, desinstalar hello [extensión del agente de IaaS de SQL Server](virtual-machines-windows-sql-server-agent-extension.md) así.

1. **¿Cómo puedo actualizar tooa nueva versión o edición de hello SQL Server en una máquina virtual de Azure?**

    Actualmente, no hay ninguna actualización para SQL Server que se ejecute en una máquina virtual de Azure. Crear una nueva máquina virtual de Azure con la versión o edición de SQL Server Hola deseado y, a continuación, migre el servidor nuevo de toohello de las bases de datos mediante el estándar [técnicas de migración de datos](virtual-machines-windows-migrate-sql.md).

1. **¿Cómo puedo instalar mi copia de SQL Server con licencia en una máquina virtual de Azure?**

    Hay dos toodo formas esto. Puede aprovisionar una hello [imágenes de máquina virtual que admite licencias](virtual-machines-windows-sql-server-iaas-overview.md#BYOL). Otra opción es toocopy Hola SQL Server instalación media tooa VM de Windows Server y, a continuación, instalar SQL Server en VM de Hola. En lo que respecta a la licencia, debe tener [Movilidad de Licencias a través de Software Assurance en Azure](https://azure.microsoft.com/pricing/license-mobility/). Para más información, vea [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Orientación de precios de máquinas virtuales de SQL Server Azure).

1. **¿Se puede cambiar una máquina virtual toouse mi propio licencia de SQL Server si se ha creado una de las imágenes de la Galería de pago por uso de hello?**

    No. No puede cambiar de pago por minuto licencias toousing su propia licencia. Crear una nueva máquina virtual Azure mediante uno de hello [imágenes BYOL](virtual-machines-windows-sql-server-iaas-overview.md#BYOL), y, a continuación, migre el servidor nuevo de toohello de las bases de datos mediante el estándar [técnicas de migración de datos](virtual-machines-windows-migrate-sql.md).

1. **¿Son compatibles las instancias del clúster de conmutación por error (FCI) de SQL Server con Azure Virtual Machines?**

   Sí. También puede [crear un clúster de conmutación por error de Windows en Windows Server 2016](virtual-machines-windows-portal-sql-create-failover-cluster.md) y usar espacios de almacenamiento directo (S2D) para el almacenamiento de clúster de Hola. También puede usar soluciones de agrupación en clústeres o almacenamiento de terceros como se describe en [Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md#azure-only-high-availability-solutions).

1. **¿Es necesario toopay toolicense SQL Server en una máquina virtual de Azure si solo está usándola para conmutación por error en espera /?**

    No tiene toopay toolicense un SQL Server participan como una réplica secundaria pasiva en una implementación de alta disponibilidad, si dispone de Software Assurance y usar la portabilidad de licencia como se describe en [p+f sobre licencias de máquina Virtual](http://azure.microsoft.com/pricing/licensing-faq/).

1. **¿Cómo se aplican las actualizaciones y los Service Packs en una máquina virtual de SQL Server?**

    Máquinas virtuales le permiten controlar el equipo de host de hello, incluyendo cuándo y cómo aplicar las actualizaciones. Para el sistema operativo de hello, puede aplicar manualmente las actualizaciones de windows, o puede habilitar un servicio de programación denominado [aplicación de revisiones automatizada](virtual-machines-windows-sql-automated-patching.md). Aplicación de revisión automatizada instala las actualizaciones marcadas como importantes, incluidas las actualizaciones de SQL Server que tienen esa categoría. Otro tooSQL actualizaciones opcionales que servidor debe instalarse manualmente.

1. **¿Es posible tooset configuraciones que no se muestran en la Galería de máquinas virtuales de hello (por ejemplo Windows 2008 R2 + SQL Server 2012)?**

    No. Para las imágenes de la Galería de máquina virtual que incluyen SQL Server, debe seleccionar una de hello proporcionada imágenes.

1. **¿Cómo instalo herramientas de datos de SQL en mi máquina virtual de Azure?**

     Descargar e instalar herramientas de datos de SQL de Hola de [Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013](https://www.microsoft.com/en-us/download/details.aspx?id=42313).

## <a name="resources"></a>Recursos

Para obtener información general de SQL Server en máquinas virtuales de Azure, vea el vídeo de hello [máquina virtual de Azure es Hola mejor plataforma para SQL Server 2016](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/Azure-VM-is-the-best-platform-for-SQL-Server-2016). También puede obtener una buena introducción en el tema de hello, [SQL Server en máquinas virtuales de Azure información general sobre](virtual-machines-windows-sql-server-iaas-overview.md).

Otros recursos son los siguientes:

* [Aprovisionar una máquina virtual de SQL Server en hello Portal de Azure](virtual-machines-windows-portal-sql-server-provision.md)
* [Migrar un servidor en una máquina virtual de Azure de tooSQL de base de datos](virtual-machines-windows-migrate-sql.md)
* [Alta disponibilidad y recuperación ante desastres para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md)
* [Procedimientos recomendados para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-performance.md)
* [Estrategias de desarrollo y patrones de aplicación de SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-server-app-patterns-dev-strategies.md) 