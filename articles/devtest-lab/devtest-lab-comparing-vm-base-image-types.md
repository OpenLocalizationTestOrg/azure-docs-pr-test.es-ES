---
title: "aaaComparing imágenes personalizadas y las fórmulas en los laboratorios de desarrollo y pruebas | Documentos de Microsoft"
description: "Obtenga información sobre las diferencias de hello entre imágenes personalizadas y las fórmulas como bases de máquina virtual para que pueda decidir que mejor se adapte a su entorno."
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a3cb259a-7d80-40ec-8ee8-45105704d589
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: tarcher
ms.openlocfilehash: 3c1d88dfe0ff94b8e825bb7a0b4aca3341c9330d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="b4d97-103">Comparación de imágenes personalizadas y fórmulas en DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b4d97-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="b4d97-104">Se pueden usar [imágenes personalizadas](devtest-lab-create-template.md) y [fórmulas](devtest-lab-manage-formulas.md) como base para las [nuevas máquinas virtuales creadas](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="b4d97-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="b4d97-105">Sin embargo, distinción de clave de hello entre imágenes personalizadas y las fórmulas es que una imagen personalizada es simplemente una imagen basada en un disco duro virtual, mientras que una fórmula no es una imagen basada en un disco duro virtual *además* preconfigurado configuración - como el tamaño de máquina virtual, red virtual, subred y artefactos.</span><span class="sxs-lookup"><span data-stu-id="b4d97-105">However, hello key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="b4d97-106">Estos valores preconfigurados se configuran con los valores predeterminados que se pueden invalidar en tiempo de Hola de creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="b4d97-106">These preconfigured settings are set up with default values that can be overridden at hello time of VM creation.</span></span> <span data-ttu-id="b4d97-107">Este artículo explica algunas de las ventajas de hello (los profesionales de TI) y desventajas (cons) toousing imágenes personalizadas frente al uso de las fórmulas.</span><span class="sxs-lookup"><span data-stu-id="b4d97-107">This article explains some of hello advantages (pros) and disadvantages (cons) toousing custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="b4d97-108">Ventajas y desventajas de las imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="b4d97-108">Custom image pros and cons</span></span>
<span data-ttu-id="b4d97-109">Imágenes personalizadas proporcionan una toocreate de manera estática, inmutable máquinas virtuales de un entorno deseado.</span><span class="sxs-lookup"><span data-stu-id="b4d97-109">Custom images provide a static, immutable way toocreate VMs from a desired environment.</span></span> 

<span data-ttu-id="b4d97-110">**Ventajas**</span><span class="sxs-lookup"><span data-stu-id="b4d97-110">**Pros**</span></span>

* <span data-ttu-id="b4d97-111">Aprovisionamiento de una imagen personalizada de VM es rápido cuando no cambie nada después de hello que VM se active de imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d97-111">VM provisioning from a custom image is fast as nothing changes after hello VM is spun up from hello image.</span></span> <span data-ttu-id="b4d97-112">En otras palabras, no hay ningún tooapply de configuración como imagen personalizada hello es simplemente una imagen sin configuración.</span><span class="sxs-lookup"><span data-stu-id="b4d97-112">In other words, there are no settings tooapply as hello custom image is just an image without settings.</span></span> 
* <span data-ttu-id="b4d97-113">Las máquinas virtuales creadas a partir de una sola imagen personalizada son idénticas.</span><span class="sxs-lookup"><span data-stu-id="b4d97-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="b4d97-114">**Desventajas**</span><span class="sxs-lookup"><span data-stu-id="b4d97-114">**Cons**</span></span>

* <span data-ttu-id="b4d97-115">Si necesita tooupdate algún aspecto de la imagen personalizada de hello, se debe recrear la imagen de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d97-115">If you need tooupdate some aspect of hello custom image, hello image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="b4d97-116">Ventajas y desventajas de las fórmulas</span><span class="sxs-lookup"><span data-stu-id="b4d97-116">Formula pros and cons</span></span>
<span data-ttu-id="b4d97-117">Las fórmulas proporcionan un toocreate de manera dinámica las máquinas virtuales de configuración de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="b4d97-117">Formulas provide a dynamic way toocreate VMs from hello desired configuration/settings.</span></span>

<span data-ttu-id="b4d97-118">**Ventajas**</span><span class="sxs-lookup"><span data-stu-id="b4d97-118">**Pros**</span></span>

* <span data-ttu-id="b4d97-119">Se pueden capturar cambios en el entorno de hello en marcha de Hola a través de artefactos.</span><span class="sxs-lookup"><span data-stu-id="b4d97-119">Changes in hello environment can be captured on hello fly via artifacts.</span></span> <span data-ttu-id="b4d97-120">Por ejemplo, si desea que una máquina virtual que se instala con bits más recientes de hello en la canalización de versiones o dar de alta código más reciente de Hola desde el repositorio, puede especificar simplemente un artefacto que implementa los bits más recientes de Hola o se da de alta código más reciente de hello en fórmula Hola junto con un imagen base del destino.</span><span class="sxs-lookup"><span data-stu-id="b4d97-120">For example, if you want a VM installed with hello latest bits from your release pipeline or enlist hello latest code from your repository, you can simply specify an artifact that deploys hello latest bits or enlists hello latest code in hello formula together with a target base image.</span></span> <span data-ttu-id="b4d97-121">Siempre que esta fórmula se usa toocreate las máquinas virtuales, bits/código más reciente de hello son implementado/dado de alta toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b4d97-121">Whenever this formula is used toocreate VMs, hello latest bits/code are deployed/enlisted toohello VM.</span></span> 
* <span data-ttu-id="b4d97-122">Las fórmulas pueden definir la configuración predeterminada que las imágenes personalizadas no pueden proporcionar; por ejemplo, tamaños de máquina virtual y configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="b4d97-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="b4d97-123">configuración de Hello guardada en una fórmula se muestra como valores predeterminados, pero puede modificarse cuando se crea la VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4d97-123">hello settings saved in a formula are shown as default values, but can be modified when hello VM is created.</span></span> 

<span data-ttu-id="b4d97-124">**Desventajas**</span><span class="sxs-lookup"><span data-stu-id="b4d97-124">**Cons**</span></span>

* <span data-ttu-id="b4d97-125">La creación de una máquina virtual a partir de una fórmula puede tardar más que la creación de una máquina virtual a partir de una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="b4d97-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="b4d97-126">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="b4d97-126">Related blog posts</span></span>
* [<span data-ttu-id="b4d97-127">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="b4d97-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="b4d97-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4d97-128">Next steps</span></span>
- [<span data-ttu-id="b4d97-129">Preguntas frecuentes sobre DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="b4d97-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)