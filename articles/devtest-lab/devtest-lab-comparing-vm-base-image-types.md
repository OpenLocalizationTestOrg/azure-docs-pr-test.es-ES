---
title: "Comparación de imágenes personalizadas y fórmulas en DevTest Labs | Microsoft Docs"
description: "Obtenga más información sobre las diferencias entre las imágenes personalizadas y las fórmulas como bases de máquina virtual para que pueda decidir cuál se adapta mejor a su entorno."
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
ms.openlocfilehash: ff771abc26c08f0adb977c29739d2f5c91924b21
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="comparing-custom-images-and-formulas-in-devtest-labs"></a><span data-ttu-id="9f1a9-103">Comparación de imágenes personalizadas y fórmulas en DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9f1a9-103">Comparing custom images and formulas in DevTest Labs</span></span>
<span data-ttu-id="9f1a9-104">Se pueden usar [imágenes personalizadas](devtest-lab-create-template.md) y [fórmulas](devtest-lab-manage-formulas.md) como base para las [nuevas máquinas virtuales creadas](devtest-lab-add-vm-with-artifacts.md).</span><span class="sxs-lookup"><span data-stu-id="9f1a9-104">Both [custom images](devtest-lab-create-template.md) and [formulas](devtest-lab-manage-formulas.md) can be used as bases for [created new VMs](devtest-lab-add-vm-with-artifacts.md).</span></span> <span data-ttu-id="9f1a9-105">No obstante, la diferencia clave entre las fórmulas y las imágenes personalizadas estriba en que estas últimas son simplemente una imagen basada en un disco duro virtual, mientras que una fórmula es una imagen basada en un disco duro virtual *además de* opciones preconfiguradas, como el tamaño de la máquina virtual, la red virtual, la subred y los artefactos.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-105">However, the key distinction between custom images and formulas is that a custom image is simply an image based on a VHD, while a formula is an image based on a VHD *in addition to* preconfigured settings - such as VM Size, virtual network, subnet, and artifacts.</span></span> <span data-ttu-id="9f1a9-106">Estas opciones preconfiguradas se configuran con valores predeterminados que se pueden reemplazar en el momento de creación de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-106">These preconfigured settings are set up with default values that can be overridden at the time of VM creation.</span></span> <span data-ttu-id="9f1a9-107">En este artículo se explican algunas de las ventajas y desventajas del uso de imágenes personalizadas en comparación con el uso de fórmulas.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-107">This article explains some of the advantages (pros) and disadvantages (cons) to using custom images versus using formulas.</span></span>

## <a name="custom-image-pros-and-cons"></a><span data-ttu-id="9f1a9-108">Ventajas y desventajas de las imágenes personalizadas</span><span class="sxs-lookup"><span data-stu-id="9f1a9-108">Custom image pros and cons</span></span>
<span data-ttu-id="9f1a9-109">Las imágenes personalizadas ofrecen una manera estática e inmutable de crear máquinas virtuales a partir de un entorno deseado.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-109">Custom images provide a static, immutable way to create VMs from a desired environment.</span></span> 

<span data-ttu-id="9f1a9-110">**Ventajas**</span><span class="sxs-lookup"><span data-stu-id="9f1a9-110">**Pros**</span></span>

* <span data-ttu-id="9f1a9-111">El aprovisionamiento de máquinas virtuales a partir de imágenes personalizadas es rápido, ya que nada cambia después de poner en marcha la máquina virtual desde la imagen.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-111">VM provisioning from a custom image is fast as nothing changes after the VM is spun up from the image.</span></span> <span data-ttu-id="9f1a9-112">En otras palabras, no hay ninguna configuración que aplicar, pues la imagen personalizada es tan solo una imagen sin configuración.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-112">In other words, there are no settings to apply as the custom image is just an image without settings.</span></span> 
* <span data-ttu-id="9f1a9-113">Las máquinas virtuales creadas a partir de una sola imagen personalizada son idénticas.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-113">VMs created from a single custom image are identical.</span></span>

<span data-ttu-id="9f1a9-114">**Desventajas**</span><span class="sxs-lookup"><span data-stu-id="9f1a9-114">**Cons**</span></span>

* <span data-ttu-id="9f1a9-115">Si necesita actualizar algún aspecto de la imagen personalizada, hay que volver a crear la imagen.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-115">If you need to update some aspect of the custom image, the image must be recreated.</span></span>  

## <a name="formula-pros-and-cons"></a><span data-ttu-id="9f1a9-116">Ventajas y desventajas de las fórmulas</span><span class="sxs-lookup"><span data-stu-id="9f1a9-116">Formula pros and cons</span></span>
<span data-ttu-id="9f1a9-117">Las fórmulas ofrecen una manera dinámica de crear máquinas virtuales a partir de la configuración deseada.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-117">Formulas provide a dynamic way to create VMs from the desired configuration/settings.</span></span>

<span data-ttu-id="9f1a9-118">**Ventajas**</span><span class="sxs-lookup"><span data-stu-id="9f1a9-118">**Pros**</span></span>

* <span data-ttu-id="9f1a9-119">Los cambios de entorno se pueden capturar sobre la marcha mediante artefactos.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-119">Changes in the environment can be captured on the fly via artifacts.</span></span> <span data-ttu-id="9f1a9-120">Por ejemplo, si quiere que una máquina virtual se instale con los bits más recientes de la canalización de entrega de versiones o desea dar de alta el código más reciente del repositorio, basta con especificar un artefacto que implemente los bits más recientes o dé de alta el código más reciente en la fórmula junto con una imagen base de destino.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-120">For example, if you want a VM installed with the latest bits from your release pipeline or enlist the latest code from your repository, you can simply specify an artifact that deploys the latest bits or enlists the latest code in the formula together with a target base image.</span></span> <span data-ttu-id="9f1a9-121">Siempre que se use esta fórmula para crear máquinas virtuales, se implementa o se da de alta el código o los bits más recientes en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-121">Whenever this formula is used to create VMs, the latest bits/code are deployed/enlisted to the VM.</span></span> 
* <span data-ttu-id="9f1a9-122">Las fórmulas pueden definir la configuración predeterminada que las imágenes personalizadas no pueden proporcionar; por ejemplo, tamaños de máquina virtual y configuración de red virtual.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-122">Formulas can define default settings that custom images cannot provide - such as VM sizes and virtual network settings.</span></span> 
* <span data-ttu-id="9f1a9-123">La configuración guardada en una fórmula se muestra como valores predeterminados, pero se puede modificar al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-123">The settings saved in a formula are shown as default values, but can be modified when the VM is created.</span></span> 

<span data-ttu-id="9f1a9-124">**Desventajas**</span><span class="sxs-lookup"><span data-stu-id="9f1a9-124">**Cons**</span></span>

* <span data-ttu-id="9f1a9-125">La creación de una máquina virtual a partir de una fórmula puede tardar más que la creación de una máquina virtual a partir de una imagen personalizada.</span><span class="sxs-lookup"><span data-stu-id="9f1a9-125">Creating a VM from a formula can take more time than creating a VM from a custom image.</span></span>

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="9f1a9-126">Entradas blogs relacionadas</span><span class="sxs-lookup"><span data-stu-id="9f1a9-126">Related blog posts</span></span>
* [<span data-ttu-id="9f1a9-127">Custom images or formulas? (¿Imágenes personalizadas o fórmulas?)</span><span class="sxs-lookup"><span data-stu-id="9f1a9-127">Custom images or formulas?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/06/custom-images-or-formulas/)

## <a name="next-steps"></a><span data-ttu-id="9f1a9-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9f1a9-128">Next steps</span></span>
- [<span data-ttu-id="9f1a9-129">Preguntas frecuentes sobre DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="9f1a9-129">DevTest Labs FAQ</span></span>](devtest-lab-faq.md)