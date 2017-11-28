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
# <a name="configure-azure-key-vault-integration-for-sql-server-on-azure-virtual-machines-resource-manager"></a><span data-ttu-id="55de0-104">Configurar la integración de Azure Key Vault para SQL Server en máquinas virtuales de Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="55de0-104">Configure Azure Key Vault Integration for SQL Server on Azure Virtual Machines (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="55de0-105">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="55de0-105">Resource Manager</span></span>](virtual-machines-windows-ps-sql-keyvault.md)
> * [<span data-ttu-id="55de0-106">Clásico</span><span class="sxs-lookup"><span data-stu-id="55de0-106">Classic</span></span>](../classic/ps-sql-keyvault.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="55de0-107">Información general</span><span class="sxs-lookup"><span data-stu-id="55de0-107">Overview</span></span>
<span data-ttu-id="55de0-108">SQL Server tiene varias características de cifrado, como el [cifrado de datos transparente (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), el [cifrado de nivel de columna (CLE)](https://msdn.microsoft.com/library/ms173744.aspx) y el [cifrado de copia de seguridad](https://msdn.microsoft.com/library/dn449489.aspx).</span><span class="sxs-lookup"><span data-stu-id="55de0-108">There are multiple SQL Server encryption features, such as [transparent data encryption (TDE)](https://msdn.microsoft.com/library/bb934049.aspx), [column level encryption (CLE)](https://msdn.microsoft.com/library/ms173744.aspx), and [backup encryption](https://msdn.microsoft.com/library/dn449489.aspx).</span></span> <span data-ttu-id="55de0-109">Estas formas de cifrado requieren toomanage y almacenan las claves criptográficas de Hola que utilice para el cifrado.</span><span class="sxs-lookup"><span data-stu-id="55de0-109">These forms of encryption require you toomanage and store hello cryptographic keys you use for encryption.</span></span> <span data-ttu-id="55de0-110">Hola servicio de almacén de claves de Azure (claves) está diseñado tooimprove Hola seguridad y la administración de estas claves en una ubicación segura y altamente disponible.</span><span class="sxs-lookup"><span data-stu-id="55de0-110">hello Azure Key Vault (AKV) service is designed tooimprove hello security and management of these keys in a secure and highly available location.</span></span> <span data-ttu-id="55de0-111">Hola [conector de SQL Server](http://www.microsoft.com/download/details.aspx?id=45344) permite a SQL Server toouse estas claves del almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="55de0-111">hello [SQL Server Connector](http://www.microsoft.com/download/details.aspx?id=45344) enables SQL Server toouse these keys from Azure Key Vault.</span></span>

<span data-ttu-id="55de0-112">Si se ejecuta SQL Server local de equipos, se están [pasos que puede seguir tooaccess el almacén de claves de Azure desde el equipo de SQL Server local](https://msdn.microsoft.com/library/dn198405.aspx).</span><span class="sxs-lookup"><span data-stu-id="55de0-112">If you running SQL Server with on-premises machines, there are [steps you can follow tooaccess Azure Key Vault from your on-premises SQL Server machine](https://msdn.microsoft.com/library/dn198405.aspx).</span></span> <span data-ttu-id="55de0-113">Pero para SQL Server en máquinas virtuales de Azure, puede ahorrar tiempo mediante el uso de hello *integración del almacén de claves de Azure* característica.</span><span class="sxs-lookup"><span data-stu-id="55de0-113">But for SQL Server in Azure VMs, you can save time by using hello *Azure Key Vault Integration* feature.</span></span>

<span data-ttu-id="55de0-114">Cuando esta característica está habilitada, Hola conector de SQL Server se instala, configura Hola EKM proveedor tooaccess el almacén de claves de Azure y automáticamente crea Hola credencial tooallow se tooaccess el almacén.</span><span class="sxs-lookup"><span data-stu-id="55de0-114">When this feature is enabled, it automatically installs hello SQL Server Connector, configures hello EKM provider tooaccess Azure Key Vault, and creates hello credential tooallow you tooaccess your vault.</span></span> <span data-ttu-id="55de0-115">Si busca en pasos de Hola Hola se ha mencionado previamente documentación local, puede ver que esta característica automatiza los pasos 2 y 3.</span><span class="sxs-lookup"><span data-stu-id="55de0-115">If you looked at hello steps in hello previously mentioned on-premises documentation, you can see that this feature automates steps 2 and 3.</span></span> <span data-ttu-id="55de0-116">lo único que Hola todavía necesitaría toodo manualmente es claves y el almacén de claves de hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="55de0-116">hello only thing you would still need toodo manually is toocreate hello key vault and keys.</span></span> <span data-ttu-id="55de0-117">Desde allí, se automatiza la instalación completa de hello de la VM de SQL.</span><span class="sxs-lookup"><span data-stu-id="55de0-117">From there, hello entire setup of your SQL VM is automated.</span></span> <span data-ttu-id="55de0-118">Una vez completada la instalación, esta característica puede ejecutar toobegin de instrucciones de T-SQL cifrar sus bases de datos o las copias de seguridad, tal y como lo haría normalmente.</span><span class="sxs-lookup"><span data-stu-id="55de0-118">Once this feature has completed this setup, you can execute T-SQL statements toobegin encrypting your databases or backups as you normally would.</span></span>

[!INCLUDE [AKV Integration Prepare](../../../../includes/virtual-machines-sql-server-akv-prepare.md)]

## <a name="enabling-and-configuring-akv-integration"></a><span data-ttu-id="55de0-119">Habilitación y configuración de la integración de Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="55de0-119">Enabling and configuring AKV integration</span></span>
<span data-ttu-id="55de0-120">Puede habilitar la integración de Almacén de claves de Azure durante el aprovisionamiento o configurarlo para las máquinas virtuales existentes.</span><span class="sxs-lookup"><span data-stu-id="55de0-120">You can enable AKV integration during provisioning or configure it for existing VMs.</span></span>

### <a name="new-vms"></a><span data-ttu-id="55de0-121">Nuevas máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="55de0-121">New VMs</span></span>
<span data-ttu-id="55de0-122">Si va a aprovisionar una nueva máquina virtual con el Administrador de recursos de SQL Server, Hola portal de Azure proporciona un tooenable paso integración del almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="55de0-122">If you are provisioning a new SQL Server virtual machine with Resource Manager, hello Azure portal provides a step tooenable Azure Key Vault integration.</span></span> <span data-ttu-id="55de0-123">característica de almacén de claves de Azure de Hello solo está disponible para hello Enterprise, Developer y Evaluation ediciones de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55de0-123">hello Azure Key Vault feature is available only for hello Enterprise, Developer and Evaluation Editions of SQL Server.</span></span>

![Integración de Azure Key Vault con SQL](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-arm-akv.png)

<span data-ttu-id="55de0-125">Para obtener un tutorial detallado de aprovisionamiento, vea [aprovisionar una máquina virtual de SQL Server en el Portal de Azure hello](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="55de0-125">For a detailed walkthrough of provisioning, see [Provision a SQL Server virtual machine in hello Azure Portal](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

### <a name="existing-vms"></a><span data-ttu-id="55de0-126">Máquinas virtuales existentes</span><span class="sxs-lookup"><span data-stu-id="55de0-126">Existing VMs</span></span>
<span data-ttu-id="55de0-127">Para las máquinas virtuales de SQL Server existentes, seleccione su máquina virtual de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="55de0-127">For existing SQL Server virtual machines, select your SQL Server virtual machine.</span></span> <span data-ttu-id="55de0-128">A continuación, seleccione hello **configuración de SQL Server** sección de hello **configuración** hoja.</span><span class="sxs-lookup"><span data-stu-id="55de0-128">Then select hello **SQL Server configuration** section of hello **Settings** blade.</span></span>

![Integración de Almacén de claves de Azure de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-existing-vms.png)

<span data-ttu-id="55de0-130">Hola **configuración de SQL Server** hoja, haga clic en hello **editar** botón Hola sección de la integración del almacén de claves automatizada.</span><span class="sxs-lookup"><span data-stu-id="55de0-130">In hello **SQL Server configuration** blade, click hello **Edit** button in hello Automated Key Vault integration section.</span></span>

![Configuración de Almacén de claves de Azure de SQL para máquinas virtuales existentes](./media/virtual-machines-windows-ps-sql-keyvault/azure-sql-rm-akv-configuration.png)

<span data-ttu-id="55de0-132">Cuando termine, haga clic en hello **Aceptar** botón en la parte inferior de Hola de hello **configuración de SQL Server** toosave hoja los cambios.</span><span class="sxs-lookup"><span data-stu-id="55de0-132">When finished, click hello **OK** button on hello bottom of hello **SQL Server configuration** blade toosave your changes.</span></span>

> [!NOTE]
> <span data-ttu-id="55de0-133">También puede usar una plantilla para configurar la integración de Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="55de0-133">You can also configure AKV integration using a template.</span></span> <span data-ttu-id="55de0-134">Para más información, consulte la [plantilla de inicio rápido de Azure para la integración de Almacén de claves de Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span><span class="sxs-lookup"><span data-stu-id="55de0-134">For more information, see [Azure quickstart template for Azure Key Vault integration](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-sql-existing-keyvault-update).</span></span>
> 
> 

[!INCLUDE [AKV Integration Next Steps](../../../../includes/virtual-machines-sql-server-akv-next-steps.md)]

