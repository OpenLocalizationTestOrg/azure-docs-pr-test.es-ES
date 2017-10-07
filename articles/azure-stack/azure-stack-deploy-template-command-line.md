---
title: "plantillas de aaaDeploy con la línea de comandos de hello en la pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola tooAzure de plantillas de interfaz de línea de comandos (CLI) de multiplataforma toodeploy pila."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a><span data-ttu-id="6b3a0-103">Implementación de plantillas en la pila de Azure mediante la línea de comandos de Hola</span><span class="sxs-lookup"><span data-stu-id="6b3a0-103">Deploy templates in Azure Stack using hello command line</span></span>
<span data-ttu-id="6b3a0-104">Utilice Hola línea de comandos toodeploy Azure Resource Manager plantillas toohello Kit de desarrollo de pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="6b3a0-104">Use hello command line toodeploy Azure Resource Manager templates toohello Azure Stack Development Kit.</span></span> <span data-ttu-id="6b3a0-105">Plantillas de administrador de recursos de Azure implementación y aprovisionar todos los recursos de Hola para su aplicación en una única operación coordinada.</span><span class="sxs-lookup"><span data-stu-id="6b3a0-105">Azure Resource Manager templates deploy and provision all hello resources for your application in a single, coordinated operation.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="6b3a0-106">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="6b3a0-106">Before you begin</span></span>
 - <span data-ttu-id="6b3a0-107">[Instalar y conectar](azure-stack-connect-cli.md) tooAzure pila con CLI de Azure</span><span class="sxs-lookup"><span data-stu-id="6b3a0-107">[Install and connect](azure-stack-connect-cli.md) tooAzure Stack with Azure CLI</span></span>
 - <span data-ttu-id="6b3a0-108">Descargar archivos de hello *azuredeploy.json* y *azuredeploy.parameters.json* de hello [crear plantilla de ejemplo de cuenta de almacenamiento](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="6b3a0-108">Download hello files *azuredeploy.json* and *azuredeploy.parameters.json* from hello [create storage account example template](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account).</span></span>
 
## <a name="deploy-template"></a><span data-ttu-id="6b3a0-109">Implementar plantilla</span><span class="sxs-lookup"><span data-stu-id="6b3a0-109">Deploy template</span></span>
<span data-ttu-id="6b3a0-110">Desplazarse por las carpetas de toohello que estos archivos se han descargado y ejecute hello después de la plantilla del comando toodeploy hello:</span><span class="sxs-lookup"><span data-stu-id="6b3a0-110">Navigate toohello folder where these files were downloaded and run hello following command toodeploy hello template:</span></span>

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

<span data-ttu-id="6b3a0-111">Este comando implementa el grupo de recursos de hello plantilla toohello **cliRG** en la ubicación predeterminada de hello Azure pila prueba de concepto.</span><span class="sxs-lookup"><span data-stu-id="6b3a0-111">This command deploys hello template toohello resource group **cliRG** in hello Azure Stack POC’s default location.</span></span>

## <a name="validate-template-deployment"></a><span data-ttu-id="6b3a0-112">Validar la implementación de la plantilla</span><span class="sxs-lookup"><span data-stu-id="6b3a0-112">Validate template deployment</span></span>
<span data-ttu-id="6b3a0-113">comandos de este grupo y almacenamiento cuenta de recursos, Hola de uso después de toosee:</span><span class="sxs-lookup"><span data-stu-id="6b3a0-113">toosee this resource group and storage account, use hello following commands:</span></span>

    azure group list

    azure storage account list

## <a name="next-steps"></a><span data-ttu-id="6b3a0-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6b3a0-114">Next steps</span></span>
[<span data-ttu-id="6b3a0-115">Administración de permisos de usuario</span><span class="sxs-lookup"><span data-stu-id="6b3a0-115">Manage user permissions</span></span>](azure-stack-manage-permissions.md)

