---
title: "Ejemplo de script de Azure PowerShell: agregar certificado de aplicación a un clúster | Microsoft Docs"
description: "Ejemplo de script de Azure PowerShell: agregar un certificado de aplicación a un clúster de Service Fabric."
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
ms.openlocfilehash: 9ccd6bb0458bc03e52103fa70cad26bd6bf98bd5
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/29/2017
---
# <a name="add-an-application-certificate-to-a-service-fabric-cluster"></a><span data-ttu-id="fe284-103">Incorporación de un certificado de aplicación a un clúster de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="fe284-103">Add an application certificate to a Service Fabric cluster</span></span>

<span data-ttu-id="fe284-104">Este script de ejemplo crea un certificado autofirmado en el almacén de claves de Azure especificado y lo instala en todos los nodos del clúster de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="fe284-104">This sample script creates a self-signed certificate in the specified Azure key vault and installs it to all nodes of the Service Fabric cluster.</span></span> <span data-ttu-id="fe284-105">El certificado también se descarga en una carpeta local.</span><span class="sxs-lookup"><span data-stu-id="fe284-105">The certificate also downloads to a local folder.</span></span> <span data-ttu-id="fe284-106">El nombre del certificado descargado es el mismo que el nombre del certificado del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="fe284-106">The name of the downloaded certificate is the same as the name of the certificate in the key vault.</span></span> <span data-ttu-id="fe284-107">Personalice los parámetros según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="fe284-107">Customize the parameters as needed.</span></span>

<span data-ttu-id="fe284-108">Si es necesario, instale Azure PowerShell con la instrucción que se encuentra en la [guía de Azure PowerShell](/powershell/azure/overview) y luego ejecute `Login-AzureRmAccount` para crear una conexión con Azure.</span><span class="sxs-lookup"><span data-stu-id="fe284-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview) and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> 

## <a name="sample-script"></a><span data-ttu-id="fe284-109">Script de ejemplo</span><span class="sxs-lookup"><span data-stu-id="fe284-109">Sample script</span></span>

<span data-ttu-id="fe284-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Incorporación de un certificado de aplicación a un clúster")]</span><span class="sxs-lookup"><span data-stu-id="fe284-110">[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate to a cluster")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="fe284-111">Explicación del script</span><span class="sxs-lookup"><span data-stu-id="fe284-111">Script explanation</span></span>

<span data-ttu-id="fe284-112">Cada script utiliza los comandos siguientes: cada comando de la tabla crea un vínculo a documentación específica del comando.</span><span class="sxs-lookup"><span data-stu-id="fe284-112">This script uses the following commands: Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fe284-113">Comando</span><span class="sxs-lookup"><span data-stu-id="fe284-113">Command</span></span> | <span data-ttu-id="fe284-114">Notas</span><span class="sxs-lookup"><span data-stu-id="fe284-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fe284-115">Add-AzureRmServiceFabricApplicationCertificate</span><span class="sxs-lookup"><span data-stu-id="fe284-115">Add-AzureRmServiceFabricApplicationCertificate</span></span>](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | <span data-ttu-id="fe284-116">Agregue un nuevo certificado de aplicación al conjunto de escalado de máquinas virtuales que componen el clúster.</span><span class="sxs-lookup"><span data-stu-id="fe284-116">Add a new application certificate to the virtual machine scale set that make up the cluster.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="fe284-117">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fe284-117">Next steps</span></span>

<span data-ttu-id="fe284-118">Para obtener más información sobre el módulo de Azure PowerShell, consulte la [documentación de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe284-118">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fe284-119">Puede encontrar ejemplos de Azure PowerShell para Azure Service Fabric en los [ejemplos de PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fe284-119">Additional Azure Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
