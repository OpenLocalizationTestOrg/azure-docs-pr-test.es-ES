---
title: aaaRequire transferencia segura en el almacenamiento de Azure | Documentos de Microsoft
description: "Obtenga información acerca de la característica de \"Requerir una transferencia segura\" hello para el almacenamiento de Azure y cómo tooenable lo."
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
ms.openlocfilehash: 27f745c5e771b50213c1dbb39dee081947be1f39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="require-secure-transfer"></a><span data-ttu-id="28f46-103">Requerir transferencia segura</span><span class="sxs-lookup"><span data-stu-id="28f46-103">Require secure transfer</span></span>

<span data-ttu-id="28f46-104">opción de Hola "transferencia segura necesaria" mejora la seguridad de hello de la cuenta de almacenamiento solo tiene que permitir las solicitudes de cuenta de almacenamiento de toohello de conexiones seguras.</span><span class="sxs-lookup"><span data-stu-id="28f46-104">hello "Secure transfer required" option enhances hello security of your storage account by only allowing requests toohello storage account from secure connections.</span></span> <span data-ttu-id="28f46-105">Por ejemplo, al llamar a las API de REST tooaccess su cuenta de almacenamiento, debe conectarse usando HTTPS.</span><span class="sxs-lookup"><span data-stu-id="28f46-105">For example, when calling REST APIs tooaccess your storage account, you must connect using HTTPS.</span></span> <span data-ttu-id="28f46-106">Si "Se requiere transferencia segura" está habilitada, se rechazan todas las solicitudes en que se use HTTP.</span><span class="sxs-lookup"><span data-stu-id="28f46-106">Any requests using HTTP are rejected when "Secure transfer required" is enabled.</span></span>

<span data-ttu-id="28f46-107">Cuando se usa el servicio de archivos de Azure de hello, se produce un error en cualquier conexión sin cifrado cuando "Proteger la transferencia requerida" está habilitada.</span><span class="sxs-lookup"><span data-stu-id="28f46-107">When you are using hello Azure Files service, any connection without encryption fails when "Secure transfer required" is enabled.</span></span> <span data-ttu-id="28f46-108">Esto incluye escenarios con algunos tipos de hello cliente Linux SMB, SMB 2.1 y SMB 3.0 sin cifrado.</span><span class="sxs-lookup"><span data-stu-id="28f46-108">This includes scenarios using SMB 2.1, SMB 3.0 without encryption, and some flavors of hello Linux SMB client.</span></span> 

<span data-ttu-id="28f46-109">De forma predeterminada, la opción de Hola "transferencia segura necesaria" está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="28f46-109">By default, hello "Secure transfer required" option is disabled.</span></span>

> [!NOTE]
> <span data-ttu-id="28f46-110">Dado que Azure Storage no admite HTTPS para los nombres de dominio personalizados, esta opción no se aplica cuando se utiliza un nombre de dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="28f46-110">Because Azure Storage doesn't support HTTPS for custom domain names, this option is not applied when using a custom domain name.</span></span>

## <a name="enable-secure-transfer-required-in-hello-azure-portal"></a><span data-ttu-id="28f46-111">Habilitar a "Transferencia segura necesaria" Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="28f46-111">Enable "Secure transfer required" in hello Azure portal</span></span>

<span data-ttu-id="28f46-112">Puede habilitar Hola "transferencia segura necesario" si se establecen cuando se crea una cuenta de almacenamiento en hello [portal de Azure](https://portal.azure.com)y para las cuentas de almacenamiento existente.</span><span class="sxs-lookup"><span data-stu-id="28f46-112">You can enable hello "Secure transfer required" setting both when you create a storage account in hello [Azure portal](https://portal.azure.com), and for existing storage accounts.</span></span>

### <a name="require-secure-transfer-when-you-create-a-storage-account"></a><span data-ttu-id="28f46-113">Solicitud de transferencia segura al crear una cuenta de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="28f46-113">Require secure transfer when you create a storage account</span></span>

1. <span data-ttu-id="28f46-114">Abra hello **crear cuenta de almacenamiento** hoja Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="28f46-114">Open hello **Create storage account** blade in hello Azure portal.</span></span>
1. <span data-ttu-id="28f46-115">En **Se requiere transferencia segura**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="28f46-115">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_1.png)

### <a name="require-secure-transfer-for-an-existing-storage-account"></a><span data-ttu-id="28f46-117">Solicitud de transferencia segura en una cuenta de almacenamiento existente</span><span class="sxs-lookup"><span data-stu-id="28f46-117">Require secure transfer for an existing storage account</span></span>

1. <span data-ttu-id="28f46-118">Seleccione una cuenta de almacenamiento existente en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="28f46-118">Select an existing storage account in hello Azure portal.</span></span>
1. <span data-ttu-id="28f46-119">Seleccione **configuración** en **configuración** en la hoja de menú de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="28f46-119">Select **Configuration** under **SETTINGS** in hello storage account menu blade.</span></span>
1. <span data-ttu-id="28f46-120">En **Se requiere transferencia segura**, seleccione **Habilitado**.</span><span class="sxs-lookup"><span data-stu-id="28f46-120">Under **Secure transfer required**, select **Enabled**.</span></span>

  ![captura de pantalla](./media/storage-require-secure-transfer/secure_transfer_field_in_portal_en_2.png)

## <a name="enable-secure-transfer-required-programmatically"></a><span data-ttu-id="28f46-122">Habilitación de "Se requiere transferencia segura" mediante programación</span><span class="sxs-lookup"><span data-stu-id="28f46-122">Enable "Secure transfer required" programmatically</span></span>

<span data-ttu-id="28f46-123">es el nombre de la configuración de Hello _supportsHttpsTrafficOnly_ en Propiedades de la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="28f46-123">hello setting name is _supportsHttpsTrafficOnly_ in storage account properties.</span></span> <span data-ttu-id="28f46-124">Puede habilitar la configuración "Se requiere transferencia segura" con la API de REST, herramientas o bibliotecas:</span><span class="sxs-lookup"><span data-stu-id="28f46-124">You can enable "Secure transfer required" setting with REST API, tools or libraries:</span></span>

* <span data-ttu-id="28f46-125">**API de REST** (versión: 2016-12-01): [paquete comercial](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span><span class="sxs-lookup"><span data-stu-id="28f46-125">**REST API** (Version: 2016-12-01): [release package](https://docs.microsoft.com/en-us/rest/api/storagerp/storageaccounts)</span></span>
* <span data-ttu-id="28f46-126">**PowerShell** (versión: 4.1.0): [paquete comercial](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span><span class="sxs-lookup"><span data-stu-id="28f46-126">**PowerShell** (Version: 4.1.0): [release package](https://docs.microsoft.com/en-us/powershell/module/azurerm.storage/set-azurermstorageaccount?view=azurermps-4.1.0)</span></span>
* <span data-ttu-id="28f46-127">**CLI** (versión: 2.0.11): [paquete comercial](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span><span class="sxs-lookup"><span data-stu-id="28f46-127">**CLI** (Version: 2.0.11): [release package](https://pypi.python.org/pypi/azure-cli-storage/2.0.11)</span></span>
* <span data-ttu-id="28f46-128">**NodeJS** (versión: 1.1.0): [paquete comercial](https://www.npmjs.com/package/azure-arm-storage/)</span><span class="sxs-lookup"><span data-stu-id="28f46-128">**NodeJS** (Version: 1.1.0): [release package](https://www.npmjs.com/package/azure-arm-storage/)</span></span>
* <span data-ttu-id="28f46-129">**SDK de .NET** (versión: 6.3.0): [paquete comercial](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span><span class="sxs-lookup"><span data-stu-id="28f46-129">**.NET SDK** (Version: 6.3.0): [release package](https://www.nuget.org/packages/Microsoft.Azure.Management.Storage/6.3.0-preview)</span></span>
* <span data-ttu-id="28f46-130">**SDK de Python** (versión: 1.1.0): [paquete comercial](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span><span class="sxs-lookup"><span data-stu-id="28f46-130">**Python SDK** (Version: 1.1.0): [release package](https://pypi.python.org/pypi/azure-mgmt-storage/1.1.0)</span></span>
* <span data-ttu-id="28f46-131">**SDK de Ruby** (versión: 0.11.0): [paquete comercial](https://rubygems.org/gems/azure_mgmt_storage)</span><span class="sxs-lookup"><span data-stu-id="28f46-131">**Ruby SDK** (Version: 0.11.0): [release package](https://rubygems.org/gems/azure_mgmt_storage)</span></span>

### <a name="enable-secure-transfer-required-setting-with-rest-api"></a><span data-ttu-id="28f46-132">Habilitación de la configuración "Se requiere transferencia segura" con la API de REST</span><span class="sxs-lookup"><span data-stu-id="28f46-132">Enable "Secure transfer required" setting with REST API</span></span>

<span data-ttu-id="28f46-133">toosimplify pruebas con la API de REST, puede usar [ArmClient](https://github.com/projectkudu/ARMClient) toocall desde la línea de comandos.</span><span class="sxs-lookup"><span data-stu-id="28f46-133">toosimplify testing with REST API, you can use [ArmClient](https://github.com/projectkudu/ARMClient) toocall from command line.</span></span>

 <span data-ttu-id="28f46-134">Puede usar por debajo de la opción de línea de comandos toocheck Hola con hello API de REST:</span><span class="sxs-lookup"><span data-stu-id="28f46-134">You can use below command line toocheck hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient GET  /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01
```

<span data-ttu-id="28f46-135">En la respuesta de hello, encontrará _supportsHttpsTrafficOnly_ configuración.</span><span class="sxs-lookup"><span data-stu-id="28f46-135">In hello response, you can find _supportsHttpsTrafficOnly_ setting.</span></span> <span data-ttu-id="28f46-136">Sample:</span><span class="sxs-lookup"><span data-stu-id="28f46-136">Sample:</span></span>

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

<span data-ttu-id="28f46-137">Puede usar por debajo de la opción de línea de comandos tooenable Hola con hello API de REST:</span><span class="sxs-lookup"><span data-stu-id="28f46-137">You can use below command line tooenable hello setting with hello REST API:</span></span>

```
# Login Azure and proceed with your credentials
> armclient login

> armclient PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{accountName}?api-version=2016-12-01 < Input.json
```
<span data-ttu-id="28f46-138">Ejemplo de Input.json:</span><span class="sxs-lookup"><span data-stu-id="28f46-138">Sample of Input.json:</span></span>
```Json
{
  "location": "westus",
  "properties": {
    "supportsHttpsTrafficOnly": true
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="28f46-139">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28f46-139">Next steps</span></span>
<span data-ttu-id="28f46-140">Almacenamiento de Azure proporciona un conjunto completo de capacidades de seguridad, que juntas permiten a los desarrolladores de aplicaciones seguras toobuild.</span><span class="sxs-lookup"><span data-stu-id="28f46-140">Azure Storage provides a comprehensive set of security capabilities, which together enable developers toobuild secure applications.</span></span> <span data-ttu-id="28f46-141">Para obtener más detalles, visite hello [Guía de seguridad de almacenamiento](storage-security-guide.md).</span><span class="sxs-lookup"><span data-stu-id="28f46-141">For more details, visit hello [Storage Security Guide](storage-security-guide.md).</span></span>
