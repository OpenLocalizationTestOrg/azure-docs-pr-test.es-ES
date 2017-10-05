---
title: "Requisitos previos técnicos para la creación de una imagen de máquina virtual para Azure Marketplace | Microsoft Docs"
description: "Entienda los requisitos para crear e implementar una imagen de máquina virtual en Azure Marketplace para que otros usuarios la compren."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="51dca-103">Requisitos previos técnicos para la creación de una imagen de máquina virtual para Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="51dca-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="51dca-104">Lea el proceso minuciosamente antes de empezar y comprenda dónde y por qué se realiza cada paso.</span><span class="sxs-lookup"><span data-stu-id="51dca-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="51dca-105">Tanto como sea posible, debe preparar la información de su compañía y otros datos, descargar las herramientas necesarias o crear componentes técnicos antes de comenzar el proceso de creación de la oferta.</span><span class="sxs-lookup"><span data-stu-id="51dca-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="51dca-106">Estos elementos deben estar claros tras la revisión de este artículo.</span><span class="sxs-lookup"><span data-stu-id="51dca-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="51dca-107">Descargar herramientas y aplicaciones necesarias</span><span class="sxs-lookup"><span data-stu-id="51dca-107">Download needed tools & applications</span></span>
<span data-ttu-id="51dca-108">Debe tener listos los elementos siguientes antes de comenzar el proceso:</span><span class="sxs-lookup"><span data-stu-id="51dca-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="51dca-109">Dependiendo de su sistema operativo objetivo, instale los [cmdlets de Azure PowerShell](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) o la [herramienta de la interfaz de la línea de comandos de Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) desde la página de [descargas de Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="51dca-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="51dca-110">Instale el Explorador de almacenamiento de Azure desde CodePlex.</span><span class="sxs-lookup"><span data-stu-id="51dca-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="51dca-111">Descargue e instale la herramienta Certification Test Tool for Azure Certified:</span><span class="sxs-lookup"><span data-stu-id="51dca-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="51dca-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="51dca-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="51dca-113">Necesita un equipo basado en Windows para ejecutar la herramienta de certificación.</span><span class="sxs-lookup"><span data-stu-id="51dca-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="51dca-114">Si no tiene un equipo basado en Windows disponible, puede ejecutar la herramienta con una VM basada en Windows en Azure.</span><span class="sxs-lookup"><span data-stu-id="51dca-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="51dca-115">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="51dca-115">Platforms supported</span></span>
<span data-ttu-id="51dca-116">Puede desarrollar VM basadas en Azure en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="51dca-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="51dca-117">Algunos elementos del proceso de publicación, como la creación de un disco duro virtual compatible con Azure, usan diferentes herramientas y pasos según el sistema operativo que usa:</span><span class="sxs-lookup"><span data-stu-id="51dca-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="51dca-118">Si usa Linux, consulte la sección "Creación de un VHD compatible con Azure (basado en Linux)" de la [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md)(Guía de publicación de imágenes de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="51dca-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="51dca-119">Si usa Windows, consulte la sección "Creación de un VHD compatible con Azure (basado en Windows)" de la [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md)(Guía de publicación de imágenes de máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="51dca-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="51dca-120">Se necesita acceso a una máquina basada en Windows:</span><span class="sxs-lookup"><span data-stu-id="51dca-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="51dca-121">Ejecute la herramienta de validación de certificados.</span><span class="sxs-lookup"><span data-stu-id="51dca-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="51dca-122">Cree la dirección URL de firma de acceso compartido del VHD para la presentación de la certificación de dicho.</span><span class="sxs-lookup"><span data-stu-id="51dca-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="51dca-123">Desarrollar el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="51dca-123">Develop your VHD</span></span>
<span data-ttu-id="51dca-124">Puede desarrollar discos duros virtuales de Azure en la nube o de forma local:</span><span class="sxs-lookup"><span data-stu-id="51dca-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="51dca-125">El desarrollo basado en la nube significa que todos los pasos de desarrollo se realizan de forma remota en un disco duro virtual residente en Azure.</span><span class="sxs-lookup"><span data-stu-id="51dca-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="51dca-126">Para el desarrollo local se requiere la descarga de un disco duro virtual y su desarrollo mediante infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="51dca-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="51dca-127">Aunque esto es posible, no lo recomendamos.</span><span class="sxs-lookup"><span data-stu-id="51dca-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="51dca-128">Tenga en cuenta que para el desarrollo para Windows o SQL de forma local se requiere que tenga las claves de licencia local pertinentes.</span><span class="sxs-lookup"><span data-stu-id="51dca-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="51dca-129">No puede incluir ni instalar SQL Server tras crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="51dca-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="51dca-130">También debe basar su oferta en una imagen SQL aprobada del portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="51dca-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="51dca-131">Si decide desarrollar de forma local, debe realizar algunos pasos de forma diferente a si desarrollara en la nube.</span><span class="sxs-lookup"><span data-stu-id="51dca-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="51dca-132">Encontrará información pertinente en [Creación de una imagen de máquina virtual local](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="51dca-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
