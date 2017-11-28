---
title: "requisitos previos de aaaTechnical para crear una imagen de máquina virtual para hello Azure Marketplace | Documentos de Microsoft"
description: "Comprender los requisitos de Hola para crear e implementar un toohello de imagen de máquina virtual Azure Marketplace para que otros lo toopurchase."
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
ms.openlocfilehash: fcae4d9e052581e3c1dfe7962e6d50ec31040419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="43990-103">Requisitos previos técnicos para crear una imagen de máquina virtual para hello Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="43990-103">Technical prerequisites for creating a virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="43990-104">Leer proceso Hola exhaustivamente antes de comenzar y comprender dónde y por qué se realiza cada paso.</span><span class="sxs-lookup"><span data-stu-id="43990-104">Read hello process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="43990-105">Tanto como sea posible, debe preparar la información de su empresa y otros datos, descargue las herramientas necesarias, o quiere crear componentes técnicos antes de comenzar el proceso de creación de hello oferta.</span><span class="sxs-lookup"><span data-stu-id="43990-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning hello offer creation process.</span></span> <span data-ttu-id="43990-106">Estos elementos deben estar claros tras la revisión de este artículo.</span><span class="sxs-lookup"><span data-stu-id="43990-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="43990-107">Descargar herramientas y aplicaciones necesarias</span><span class="sxs-lookup"><span data-stu-id="43990-107">Download needed tools & applications</span></span>
<span data-ttu-id="43990-108">Debe tener Hola siguientes elementos listos antes de comenzar el proceso de hello:</span><span class="sxs-lookup"><span data-stu-id="43990-108">You should have hello following items ready before beginning hello process:</span></span>

* <span data-ttu-id="43990-109">Dependiendo del sistema operativo de destino, instale hello [cmdlets de PowerShell de Azure](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) o [herramienta de interfaz de línea de comandos de Linux](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) de hello [descargas de Azure](https://azure.microsoft.com/downloads/) página.</span><span class="sxs-lookup"><span data-stu-id="43990-109">Depending on which operating system you are targeting, install hello [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from hello [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="43990-110">Instale el Explorador de almacenamiento de Azure desde CodePlex.</span><span class="sxs-lookup"><span data-stu-id="43990-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="43990-111">Descargue e instale Hola herramienta Certification Test de Azure Certified:</span><span class="sxs-lookup"><span data-stu-id="43990-111">Download and install hello Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="43990-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="43990-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="43990-113">Necesita una herramienta de certificados de equipo basado en Windows toorun Hola.</span><span class="sxs-lookup"><span data-stu-id="43990-113">You need a Windows-based computer toorun hello certification tool.</span></span> <span data-ttu-id="43990-114">Si no tiene un equipo basado en Windows disponible, puede ejecutar la herramienta de hello en una máquina virtual basada en Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="43990-114">If you do not have a Windows-based computer available, you can run hello tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="43990-115">Plataformas compatibles</span><span class="sxs-lookup"><span data-stu-id="43990-115">Platforms supported</span></span>
<span data-ttu-id="43990-116">Puede desarrollar VM basadas en Azure en Windows o Linux.</span><span class="sxs-lookup"><span data-stu-id="43990-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="43990-117">Algunos elementos del programa Hola proceso, como la creación de un compatible con Azure disco duro virtual (VHD)--Utilice distintas herramientas y pasos dependiendo del sistema operativo que esté usando de publicación:</span><span class="sxs-lookup"><span data-stu-id="43990-117">Some elements of hello publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="43990-118">Si usas Linux, consulte toohello "Crear un disco duro virtual de Azure compatible (basado en Linux)" sección de hello [Guía de publicación de imagen de máquina Virtual](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="43990-118">If you are using Linux, refer toohello “Create an Azure-compatible VHD (Linux-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="43990-119">Si usas Windows, consulte la sección de "Crear un disco duro virtual de Azure compatible (basado en Windows)" de toohello de hello [Guía de publicación de imagen de máquina Virtual](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="43990-119">If you are using Windows, refer toohello “Create an Azure-compatible VHD (Windows-based)” section of hello [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43990-120">Necesita tener acceso a tooa máquina de Windows para:</span><span class="sxs-lookup"><span data-stu-id="43990-120">You need access tooa Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="43990-121">Ejecute la herramienta de validación de certificados de Hola.</span><span class="sxs-lookup"><span data-stu-id="43990-121">Run hello certification validation tool.</span></span>
> * <span data-ttu-id="43990-122">Crear URL de firma de acceso de disco duro virtual compartido de Hola para hello envío de certificación de disco duro virtual.</span><span class="sxs-lookup"><span data-stu-id="43990-122">Create hello VHD shared access signature URL for hello VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="43990-123">Desarrollar el disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="43990-123">Develop your VHD</span></span>
<span data-ttu-id="43990-124">Puede desarrollar discos duros virtuales de Azure en la nube de Hola o de forma local:</span><span class="sxs-lookup"><span data-stu-id="43990-124">You can develop Azure VHDs in hello cloud or on-premises:</span></span>

* <span data-ttu-id="43990-125">El desarrollo basado en la nube significa que todos los pasos de desarrollo se realizan de forma remota en un disco duro virtual residente en Azure.</span><span class="sxs-lookup"><span data-stu-id="43990-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="43990-126">Para el desarrollo local se requiere la descarga de un disco duro virtual y su desarrollo mediante infraestructura local.</span><span class="sxs-lookup"><span data-stu-id="43990-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="43990-127">Aunque esto es posible, no lo recomendamos.</span><span class="sxs-lookup"><span data-stu-id="43990-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="43990-128">Tenga en cuenta que desarrollar para Windows o SQL local requiere toohave Hola local relevante claves de licencia.</span><span class="sxs-lookup"><span data-stu-id="43990-128">Note that developing for Windows or SQL on-premises requires you toohave hello relevant on-premises license keys.</span></span> <span data-ttu-id="43990-129">No puede incluir ni instalar SQL Server tras crear una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="43990-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="43990-130">También deberá basar su oferta en una imagen SQL aprobada de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="43990-130">You must also base your offer on an approved SQL image from hello Azure portal.</span></span> <span data-ttu-id="43990-131">Si decide toodevelop local, debe realizar algunos pasos de manera diferente que si estuviese desarrollando en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="43990-131">If you decide toodevelop on-premises, you must perform some steps differently than if you were developing in hello cloud.</span></span> <span data-ttu-id="43990-132">Encontrará información pertinente en [Creación de una imagen de máquina virtual local](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="43990-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
