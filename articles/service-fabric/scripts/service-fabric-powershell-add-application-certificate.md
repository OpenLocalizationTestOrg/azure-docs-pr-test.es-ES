---
title: "Ejemplo de Script de PowerShell - aaaAzure Agregar aplicación cert tooa clúster | Documentos de Microsoft"
description: "Script de Azure PowerShell de ejemplo: agregar un clúster de Service Fabric application certificado tooa."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a><span data-ttu-id="f4615-103">Agregar un clúster de Service Fabric application certificado tooa</span><span class="sxs-lookup"><span data-stu-id="f4615-103">Add an application certificate tooa Service Fabric cluster</span></span>

<span data-ttu-id="f4615-104">Este script de ejemplo crea un certificado autofirmado en el almacén de claves Azure especificado hello y lo instala tooall nodos de clúster de Service Fabric Hola.</span><span class="sxs-lookup"><span data-stu-id="f4615-104">This sample script creates a self-signed certificate in hello specified Azure key vault and installs it tooall nodes of hello Service Fabric cluster.</span></span> <span data-ttu-id="f4615-105">certificado de Hello también descarga tooa de carpeta local.</span><span class="sxs-lookup"><span data-stu-id="f4615-105">hello certificate also downloads tooa local folder.</span></span> <span data-ttu-id="f4615-106">nombre de Hola de hello Descargar certificado es Hola mismo que el nombre del certificado de hello en el almacén de claves de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="f4615-106">hello name of hello downloaded certificate is hello same as hello name of hello certificate in hello key vault.</span></span> <span data-ttu-id="f4615-107">Personalizar los parámetros de hello según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="f4615-107">Customize hello parameters as needed.</span></span>

<span data-ttu-id="f4615-108">Si es necesario, instale hello Azure PowerShell con hello instrucción se encuentra en hello [Guía de Azure PowerShell](/powershell/azure/overview) y, a continuación, ejecute `Login-AzureRmAccount` toocreate una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="f4615-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f4615-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="f4615-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a><span data-ttu-id="f4615-110">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="f4615-110">Script explanation</span></span>

<span data-ttu-id="f4615-111">Este script utiliza Hola siguientes comandos: cada comando en la tabla de hello vincula documentación específica de toocommand.</span><span class="sxs-lookup"><span data-stu-id="f4615-111">This script uses hello following commands: Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f4615-112">Comando</span><span class="sxs-lookup"><span data-stu-id="f4615-112">Command</span></span> | <span data-ttu-id="f4615-113">Notas</span><span class="sxs-lookup"><span data-stu-id="f4615-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f4615-114">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="f4615-114">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="f4615-115">Agregar que una nueva escala de máquinas virtuales de aplicación certificado toohello conjuntos que componen el clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="f4615-115">Add a new application certificate toohello virtual machine scale set that make up hello cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="f4615-116">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f4615-116">Next steps</span></span>

<span data-ttu-id="f4615-117">Para obtener más información sobre el módulo de PowerShell de Azure de hello, consulte [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f4615-117">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f4615-118">Encontrará más ejemplos de Azure Powershell para Azure Service Fabric en hello [ejemplos de PowerShell de Azure](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f4615-118">Additional Azure Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
