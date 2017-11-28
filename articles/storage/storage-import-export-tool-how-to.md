---
title: Uso de la herramienta de Azure Import/Export | Microsoft Docs
description: "Descubra cómo usar la herramienta Import/Export a fin de preparar los discos duros para un trabajo de importación, así como reparar un trabajo de importación o de exportación."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 86073f5d15253d658fcb371e913dd3a543a2b075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="c3568-103">Uso de la herramienta de Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="c3568-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="c3568-104">La herramienta de Azure Import/Export (WAImportExport.exe) se utiliza para crear y administrar trabajos del servicio Azure Import/Export y le permite transferir grandes volúmenes de datos a Azure Blob Storage o desde él.</span><span class="sxs-lookup"><span data-stu-id="c3568-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="c3568-105">Esta documentación está destinada a la versión más reciente de la herramienta de Azure Import/Export.</span><span class="sxs-lookup"><span data-stu-id="c3568-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="c3568-106">Para obtener información sobre cómo usar la versión 1 de la herramienta, consulte [Uso de la herramienta de Azure Import/Export (versión 1)](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="c3568-106">For information about using the v1 tool, please see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="c3568-107">En estos artículos, verá cómo usar la herramienta para realizar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="c3568-107">In these articles, you will see how to use the tool to do the following:</span></span>  

- <span data-ttu-id="c3568-108">Instalar y configurar la herramienta de Import/Export.</span><span class="sxs-lookup"><span data-stu-id="c3568-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="c3568-109">Preparar las unidades de disco duro para un trabajo en el que se importen los datos de las unidades a Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c3568-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="c3568-110">Revisar el estado de un trabajo con archivos de registro de copia.</span><span class="sxs-lookup"><span data-stu-id="c3568-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="c3568-111">Reparar un trabajo de importación.</span><span class="sxs-lookup"><span data-stu-id="c3568-111">Repair an import job.</span></span> 
- <span data-ttu-id="c3568-112">Reparar un trabajo de exportación.</span><span class="sxs-lookup"><span data-stu-id="c3568-112">Repair an export job.</span></span> 
- <span data-ttu-id="c3568-113">Solucionar problemas de la herramienta de Azure Import/Export, en el caso de que le haya surgido algún problema durante el proceso.</span><span class="sxs-lookup"><span data-stu-id="c3568-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c3568-114">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c3568-114">Next steps</span></span>

* [<span data-ttu-id="c3568-115">Configuración de la herramienta WAImportExport</span><span class="sxs-lookup"><span data-stu-id="c3568-115">Setting up the WAImportExport tool</span></span>](storage-import-export-tool-setup.md)