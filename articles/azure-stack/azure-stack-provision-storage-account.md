---
title: Cuentas de almacenamiento en Azure Stack | Microsoft Azure
description: Aprenda a crear una cuenta de almacenamiento en Azure Stack.
services: azure-stack
documentationcenter: 
author: vhorne
manager: byronr
editor: 
ms.assetid: e1152110-b756-4c1a-9fa2-73fe3ab0ad8e
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 3/1/2017
ms.author: victorh
ms.openlocfilehash: de32c0ce79e8357274cc19cd1ea4ec23b85b918f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="storage-accounts-in-azure-stack"></a><span data-ttu-id="16d17-103">Cuentas de almacenamiento en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="16d17-103">Storage accounts in Azure Stack</span></span>
<span data-ttu-id="16d17-104">Las cuentas de almacenamiento incluyen los servicios BLOB y Tabla y el espacio de nombres único para los objetos de datos de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d17-104">Storage accounts include Blob and Table services, and the unique namespace for your storage data objects.</span></span> <span data-ttu-id="16d17-105">De forma predeterminada, los datos de su cuenta están disponibles solo para usted, el propietario de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d17-105">By default, the data in your account is available only to you, the storage account owner.</span></span>

1. <span data-ttu-id="16d17-106">En el equipo de la prueba de concepto de Azure Stack, inicie sesión en `https://adminportal.local.azurestack.external` como [un administrador](azure-stack-connect-azure-stack.md) y, a continuación, haga clic en **Nuevo** > **Datos y almacenamiento**  >  **Cuenta de almacenamiento**.</span><span class="sxs-lookup"><span data-stu-id="16d17-106">On the Azure Stack POC computer, log in to `https://adminportal.local.azurestack.external` as [an admin](azure-stack-connect-azure-stack.md), and then click **New** > **Data + Storage** > **Storage account**.</span></span>

   ![](media/azure-stack-provision-storage-account/image01.png)
2. <span data-ttu-id="16d17-107">En la hoja **Crear cuenta de almacenamiento**, escriba un nombre para la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d17-107">In the **Create storage account** blade, type a name for your storage account.</span></span> <span data-ttu-id="16d17-108">Cree un nuevo **grupo de recursos**, o seleccione uno existente y, a continuación, haga clic en **Crear** para crear la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="16d17-108">Create a new **Resource Group**, or select an existing one, then click **Create** to create the storage account.</span></span>

   ![](media/azure-stack-provision-storage-account/image02.png)
3. <span data-ttu-id="16d17-109">Para ver la nueva cuenta de almacenamiento, haga clic en **Todos los recursos** y, a continuación, busque la cuenta de almacenamiento y haga clic en su nombre.</span><span class="sxs-lookup"><span data-stu-id="16d17-109">To see your new storage account, click **All resources**, then search for the storage account and click its name.</span></span>

    ![](media/azure-stack-provision-storage-account/image03.png)

### <a name="next-steps"></a><span data-ttu-id="16d17-110">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="16d17-110">Next steps</span></span>
[<span data-ttu-id="16d17-111">Utilización de plantillas del Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="16d17-111">Use Azure Resource Manager templates</span></span>](azure-stack-arm-templates.md)

[<span data-ttu-id="16d17-112">Más información acerca de las cuentas de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="16d17-112">Learn about Azure storage accounts</span></span>](../storage/common/storage-create-storage-account.md)

[<span data-ttu-id="16d17-113">Descargue la guía de validación de almacenamiento coherente con Azure para Azure Stack</span><span class="sxs-lookup"><span data-stu-id="16d17-113">Download the Azure Stack Azure-consistent Storage Validation Guide</span></span>](http://aka.ms/azurestacktp1doc)
