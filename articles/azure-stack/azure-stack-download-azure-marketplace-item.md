---
title: Descarga de elementos de Marketplace desde Azure | Microsoft Docs
description: "Puedo descargar elementos de Marketplace desde Azure a la implementación de Azure Stack."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: erikje
ms.openlocfilehash: 4d7c335a3c68cc9bb8cb0c823883716a3dd6620a
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="download-marketplace-items-from-azure-to-azure-stack"></a><span data-ttu-id="3f8b3-103">Descarga de elementos de Marketplace desde Azure a Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3f8b3-103">Download marketplace items from Azure to Azure Stack</span></span>

<span data-ttu-id="3f8b3-104">*Se aplica a: Sistemas integrados de Azure Stack y Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="3f8b3-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="3f8b3-105">Puesto que usted decide qué contenido desea incluir en su Marketplace de Azure Stack, debe tener en cuenta el contenido disponible en Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-105">As you decide what content to include in your Azure Stack marketplace, you should consider the content available from the Azure marketplace.</span></span> <span data-ttu-id="3f8b3-106">Puede descargar de una lista protegida de elementos de Azure Marketplace que han sido previamente probados para su ejecución en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-106">You can download from a curated list of Azure marketplace items that have been pre-tested to run on Azure Stack.</span></span> <span data-ttu-id="3f8b3-107">Puesto que se agregan nuevos elementos a esta lista con frecuencia, asegúrese de volver a consultar el nuevo contenido.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-107">New items are frequently added to this list, so make sure check back for new content.</span></span>

<span data-ttu-id="3f8b3-108">Para descargar elementos de Marketplace, primero debe [registrar Azure Stack en Azure](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="3f8b3-108">To download marketplace items, you must first [register Azure Stack with Azure](azure-stack-register.md).</span></span> 

## <a name="download"></a><span data-ttu-id="3f8b3-109">Descargar</span><span class="sxs-lookup"><span data-stu-id="3f8b3-109">Download</span></span>
1. <span data-ttu-id="3f8b3-110">Inicie sesión en el portal de administrador de Azure Stack (https://portal.local.azurestack.external).</span><span class="sxs-lookup"><span data-stu-id="3f8b3-110">Sign in to the Azure Stack administrator portal (https://portal.local.azurestack.external).</span></span>
2. <span data-ttu-id="3f8b3-111">Algunos elementos de Marketplace pueden ser muy grandes.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-111">Some marketplace items can be very large.</span></span>  <span data-ttu-id="3f8b3-112">Para comprobar que dispone de espacio suficiente en el sistema, haga clic en **Proveedores de recursos** > **Storage**.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-112">Check to make sure you have enough space on your system by clicking **Resource Providers** > **Storage**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image01.png)

3. <span data-ttu-id="3f8b3-113">Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace).</span><span class="sxs-lookup"><span data-stu-id="3f8b3-113">Click **More Services** > **Marketplace Management**.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image02.png)

4. <span data-ttu-id="3f8b3-114">Haga clic en **Agregar desde Azure** para ver una lista de elementos disponibles para su descarga.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-114">Click **Add from Azure** to see a list of items available for download.</span></span> <span data-ttu-id="3f8b3-115">Puede hacer clic en cada elemento de la lista para ver su descripción y el tamaño de la descarga.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-115">You can click on each item in the list to view its description and download size.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image03.png)

5. <span data-ttu-id="3f8b3-116">Seleccione el elemento que desee en la lista y, a continuación, haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-116">Select the item you want in the list and then click **Download**.</span></span> <span data-ttu-id="3f8b3-117">Esto inicia la descarga de la imagen de máquina virtual para el elemento seleccionado.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-117">This starts downloading the VM image for the item you selected.</span></span> <span data-ttu-id="3f8b3-118">Los tiempos de descarga varían.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-118">Download times vary.</span></span>

    ![](media/azure-stack-download-azure-marketplace-item/image04.png)

6. <span data-ttu-id="3f8b3-119">Una vez finalizada la descarga, puede implementar el nuevo elemento de Marketplace como un usuario o un operador de Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-119">After the download completes, you can deploy your new marketplace item as either an Azure Stack operator or user.</span></span> <span data-ttu-id="3f8b3-120">Haga clic en **+Nuevo**, busque entre las categorías el nuevo elemento de Marketplace y, a continuación, seleccione el elemento.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-120">Click **+New**, search among the categories for the new marketplace item, and then select the item.</span></span>
7. <span data-ttu-id="3f8b3-121">Haga clic en **Crear** para abrir la experiencia de creación del elemento recién descargado.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-121">Click **Create** to open up the creation experience for the newly downloaded item.</span></span> <span data-ttu-id="3f8b3-122">Siga las instrucciones paso a paso para implementar el elemento.</span><span class="sxs-lookup"><span data-stu-id="3f8b3-122">Follow the step-by-step instructions to deploy your item.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f8b3-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3f8b3-123">Next steps</span></span>

[<span data-ttu-id="3f8b3-124">Creación y publicación de un producto en Marketplace</span><span class="sxs-lookup"><span data-stu-id="3f8b3-124">Create and publish a Marketplace item</span></span>](azure-stack-create-and-publish-marketplace-item.md)
