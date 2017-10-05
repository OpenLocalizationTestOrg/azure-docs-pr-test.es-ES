---
title: Requerir transferencia segura en Azure Storage | Microsoft Docs
description: "Obtenga información acerca de la característica \"Requerir transferencia segura\" de Azure Storage y cómo habilitarla."
services: storage
documentationcenter: na
author: fhryo-msft
manager: Jason.Hogg
editor: fhryo-msft
ms.assetid: 
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 06/20/2017
ms.author: fryu
ms.openlocfilehash: bc5b7fc79869c632db96958f17aaf953a5fd3b19
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="080b6-103">Requerir transferencia segura</span><span class="sxs-lookup"><span data-stu-id="080b6-103">Require secure transfer</span></span>

<span data-ttu-id="080b6-104">La opción "Se requiere transferencia segura" mejora la seguridad de su cuenta de almacenamiento, ya que solo permite enviar solicitudes a la cuenta de almacenamiento desde conexiones seguras.</span><span class="sxs-lookup"><span data-stu-id="080b6-104">The "Secure transfer required" option enhances the security of your storage account by only allowing requests to the storage account from secure connections.</span></span> <span data-ttu-id="080b6-105">Por ejemplo, al llamar a las API de REST para acceder a una cuenta de almacenamiento, es preciso conectarse mediante HTTPS.</span><span class="sxs-lookup"><span data-stu-id="080b6-105">For example, when calling REST APIs to access your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="080b6-106">Si "Se requiere transferencia segura" está habilitada, se rechazan todas las solicitudes en que se use HTTP.</span><span class="sxs-lookup"><span data-stu-id="080b6-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="080b6-107">Si se usa el servicio Azure Files, se produce un error en todas las conexiones sin cifrado cuando la opción "Se requiere transferencia segura" está habilitada.</span><span class="sxs-lookup"><span data-stu-id="080b6-107">When you are using the Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="080b6-108">Aquí se incluyen los escenarios que usan SMB 2.1 y SMB 3.0 sin cifrado, y algunas versiones del cliente SMB de Linux.</span><span class="sxs-lookup"><span data-stu-id="080b6-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of the Linux SMB client.</span></span> 

<span data-ttu-id="080b6-109">De forma predeterminada, la opción "Se requiere transferencia segura" está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="080b6-109">By default, the "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="080b6-110">Dado que Azure Storage no admite HTTPS para los nombres de dominio personalizados, esta opción no se aplica cuando se utiliza un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="080b6-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-the-azure-portal"></a><span data-ttu-id="080b6-111">Habilitación de "Se requiere transferencia segura" en Azure Portal</span><span class="sxs-lookup"><span data-stu-id="080b6-111">Enable "Secure transfer required" in the Azure portal</span></span>

<span data-ttu-id="080b6-112">La opción de "Se requiere transferencia segura" se puede habilitar cuando se crea una cuenta de almacenamiento en [Azure Portal](https://portal.azure.com)y para las cuentas de almacenamiento existentes.</span><span class="sxs-lookup"><span data-stu-id="080b6-112">You can enable the "Secure transfer required" setting both when you create a storage account in the [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="080b6-113">Solicitud de transferencia segura al crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="080b6-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="080b6-114">Abra la hoja **Crear cuenta de almacenamiento** en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="080b6-114">Open the **Create storage account** blade in the Azure portal.</span></span>
1. <span data-ttu-id="080b6-115">En **Se requiere transferencia segura**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="080b6-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="080b6-117">Solicitud de transferencia segura en una cuenta de almacenamiento existente</span><span class="sxs-lookup"><span data-stu-id="080b6-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="080b6-118">Seleccione una cuenta de almacenamiento existente en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="080b6-118">Select an existing storage account in the Azure portal.</span></span>
1. <span data-ttu-id="080b6-119">Seleccione **Configuración** en **CONFIGURACIÓN** en la hoja del menú de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="080b6-119">Select **Configuration** under **SETTINGS** in the storage account menu blade.</span></span>
1. <span data-ttu-id="080b6-120">En **Se requiere transferencia segura**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="080b6-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="080b6-122">Habilitación de "Se requiere transferencia segura" mediante programación</span><span class="sxs-lookup"><span data-stu-id="080b6-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="080b6-123">El nombre del valor es _supportsHttpsTrafficOnly_ en las propiedades de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="080b6-123">The setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="080b6-124">Puede habilitar la configuración "Se requiere transferencia segura" con la API de REST, herramientas o bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="080b6-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="080b6-125">**API de REST** (versión: 2016-12-01): [paquete comercial](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="080b6-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="080b6-126">**PowerShell** (versión: 4.1.0): [paquete comercial](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="080b6-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="080b6-127">**CLI** (versión: 2.0.11): [paquete comercial](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="080b6-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="080b6-128">**NodeJS** (versión: 1.1.0): [paquete comercial](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="080b6-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="080b6-129">**SDK de .NET** (versión: 6.3.0): [paquete comercial](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="080b6-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="080b6-130">**SDK de Python** (versión: 1.1.0): [paquete comercial](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="080b6-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="080b6-131">**SDK de Ruby** (versión: 0.11.0): [paquete comercial](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="080b6-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="080b6-132">Habilitación de la configuración "Se requiere transferencia segura" con la API de REST</span><span class="sxs-lookup"><span data-stu-id="080b6-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="080b6-133">Para simplificar las pruebas con la API de REST, puede usar [ArmClient](https://github.com/projectkudu/ARMClient) para llamar desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="080b6-133">To simplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) to call from command line.</span></span>

 <span data-ttu-id="080b6-134">Puede utilizar la línea de comandos siguiente para comprobar la configuración con la API de REST:</span><span class="sxs-lookup"><span data-stu-id="080b6-134">You can use below command line to check the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="080b6-135">En la respuesta, puede encontrar el valor _supportsHttpsTrafficOnly_.</span><span class="sxs-lookup"><span data-stu-id="080b6-135">In the response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="080b6-136">Sample:</span><span class="sxs-lookup"><span data-stu-id="080b6-136">Sample:</span></span>

```Json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}",
  "kind": "Storage",
  ...
  "properties": {
    ...
    "supportsHttpsTrafficOnly": false
  },
  "type": "Microsoft.Storage/storageAccounts"
}
```

<span data-ttu-id="080b6-137">Puede utilizar la línea de comandos siguiente para habilitar la configuración con la API de REST:</span><span class="sxs-lookup"><span data-stu-id="080b6-137">You can use below command line to enable the setting with the REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="080b6-138">Ejemplo de Input.json:</span><span class="sxs-lookup"><span data-stu-id="080b6-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="080b6-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="080b6-139">Next steps</span></span>
<span data-ttu-id="080b6-140">Azure Storage proporciona un completo conjunto de funcionalidades de seguridad que, conjuntamente, permiten a los desarrolladores compilar aplicaciones seguras.</span><span class="sxs-lookup"><span data-stu-id="080b6-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers to build secure applications.</span></span> <span data-ttu-id="080b6-141">Para obtener más detalles, visite la [Guía de seguridad para almacenamiento](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="080b6-141">For more details, visit the [Storage Security Guide](storage-security-guide.md).</span></span>
