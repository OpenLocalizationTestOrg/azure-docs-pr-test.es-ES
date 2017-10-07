---
title: "el almacén de claves con SQL Server en máquinas virtuales de Windows Azure (Administrador de recursos) aaaIntegrate | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooautomate Hola configuración de cifrado de SQL Server para su uso con el almacén de claves de Azure. Este tema explica cómo toouse integración del almacén de claves de Azure con máquinas virtuales de SQL Server creado con el Administrador de recursos."
services: virtual-machines-windows
documentationcenter: 
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: cd66dfb1-0e9b-4fb0-a471-9deaf4ab4ab8
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/23/2017
ms.author: jroth
ms.openlocfilehash: 0d36d3d075d6538c18cd5ecb43c19a4b000a99e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a>Configurar la integración de Azure Key Vault para SQL Server en máquinas virtuales de Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-ps-sql-keyvault.md)
> * [Clásico](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a>Información general
SQL Server tiene varias características de cifrado, como el [cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), el [cifrado de nivel de columna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) y el [cifrado de copia de seguridad](https://msdn.microsoft.com/library/dn449489.aspx). Estas formas de cifrado requieren toomanage y almacenan las claves criptográficas de Hola que utilice para el cifrado. Hola servicio de almacén de claves de Azure (claves) está diseñado tooimprove Hola seguridad y la administración de estas claves en una ubicación segura y altamente disponible. Hola [conector de SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite a SQL Server toouse estas claves del almacén de claves de Azure.

Si se ejecuta SQL Server local de equipos, se están [pasos que puede seguir tooaccess el almacén de claves de Azure desde el equipo de SQL Server local](https://msdn.microsoft.com/library/dn198405.aspx). Pero para SQL Server en máquinas virtuales de Azure, puede ahorrar tiempo mediante el uso de hello *integración del almacén de claves de Azure* característica.

Cuando esta característica está habilitada, Hola conector de SQL Server se instala, configura Hola EKM proveedor tooaccess el almacén de claves de Azure y automáticamente crea Hola credencial tooallow se tooaccess el almacén. Si busca en pasos de Hola Hola se ha mencionado previamente documentación local, puede ver que esta característica automatiza los pasos 2 y 3. lo único que Hola todavía necesitaría toodo manualmente es claves y el almacén de claves de hello toocreate. Desde allí, se automatiza la instalación completa de hello de la VM de SQL. Una vez completada la instalación, esta característica puede ejecutar toobegin de instrucciones de T-SQL cifrar sus bases de datos o las copias de seguridad, tal y como lo haría normalmente.

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a>Habilitación y configuración de la integración de Almacén de claves de Azure
Puede habilitar la integración de Almacén de claves de Azure durante el aprovisionamiento o configurarlo para las máquinas virtuales existentes.

### <a name="new-vms"></a>Nuevas máquinas virtuales
Si va a aprovisionar una nueva máquina virtual con el Administrador de recursos de SQL Server, Hola portal de Azure proporciona un tooenable paso integración del almacén de claves de Azure. característica de almacén de claves de Azure de Hello solo está disponible para hello Enterprise, Developer y Evaluation ediciones de SQL Server.

![Integración de Azure Key Vault con SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

Para obtener un tutorial detallado de aprovisionamiento, vea [aprovisionar una máquina virtual de SQL Server en el Portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="existing-vms"></a>Máquinas virtuales existentes
Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server. A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.

![Integración de Almacén de claves de Azure de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola sección de la integración del almacén de claves automatizada.

![Configuración de Almacén de claves de Azure de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.

> [!NOTE]
> También puede usar una plantilla para configurar la integración de Almacén de claves de Azure. Para más información, consulte la [plantilla de inicio rápido de Azure para la integración de Almacén de claves de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

