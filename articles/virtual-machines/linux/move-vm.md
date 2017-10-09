---
title: aaaMove una VM de Linux en Azure | Documentos de Microsoft
description: "Mover una VM de Linux tooanother suscripción de Azure o un grupo de recursos en el modelo de implementación del Administrador de recursos de Hola."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d635f0a5-4458-4b95-a5f8-eed4f41eb4d4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 938d04234059111912f03e72d14dabd338bc0678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-a-linux-vm-tooanother-subscription-or-resource-group"></a><span data-ttu-id="0f321-103">Mover un VM de Linux tooanother suscripción o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="0f321-103">Move a Linux VM tooanother subscription or resource group</span></span>
<span data-ttu-id="0f321-104">En este artículo se explica cómo toomove una VM Linux entre grupos de recursos o suscripciones.</span><span class="sxs-lookup"><span data-stu-id="0f321-104">This article walks you through how toomove a Linux VM between resource groups or subscriptions.</span></span> <span data-ttu-id="0f321-105">Mover una máquina virtual entre suscripciones puede resultar útil si ha creado una máquina virtual en una suscripción personal y ahora desea toomove la suscripción de la empresa tooyour.</span><span class="sxs-lookup"><span data-stu-id="0f321-105">Moving a VM between subscriptions can be handy if you created a VM in a personal subscription and now want toomove it tooyour company's subscription.</span></span>

> [!IMPORTANT]
><span data-ttu-id="0f321-106">No se puede mover discos administrados en este momento.</span><span class="sxs-lookup"><span data-stu-id="0f321-106">You cannot move Managed Disks at this time.</span></span> 
>
><span data-ttu-id="0f321-107">Identificadores de recursos nuevos se crean como parte del movimiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="0f321-107">New resource IDs are created as part of hello move.</span></span> <span data-ttu-id="0f321-108">Una vez hello máquina virtual se ha movido, deberá tooupdate los scripts y herramientas toouse Hola nuevos identificadores de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f321-108">Once hello VM has been moved, you need tooupdate your tools and scripts toouse hello new resource IDs.</span></span> 
> 
> 

## <a name="use-hello-azure-cli-toomove-a-vm"></a><span data-ttu-id="0f321-109">Usar hello Azure CLI toomove una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0f321-109">Use hello Azure CLI toomove a VM</span></span>
<span data-ttu-id="0f321-110">toosuccessfully mover una máquina virtual, deberá toomove Hola VM y todos sus recursos de soporte.</span><span class="sxs-lookup"><span data-stu-id="0f321-110">toosuccessfully move a VM, you need toomove hello VM and all its supporting resources.</span></span> <span data-ttu-id="0f321-111">Hola de uso **mostrar grupo azure** comando toolist todos los recursos de hello en un grupo de recursos y sus identificadores.</span><span class="sxs-lookup"><span data-stu-id="0f321-111">Use hello **azure group show** command toolist all hello resources in a resource group and their IDs.</span></span> <span data-ttu-id="0f321-112">Salida de hello toopipe de este archivo de comandos tooa es útil para que pueda copiar y pegar Hola identificadores en los comandos posteriores.</span><span class="sxs-lookup"><span data-stu-id="0f321-112">It helps toopipe hello output of this command tooa file so you can copy and paste hello IDs into later commands.</span></span>

    azure group show <resourceGroupName>

<span data-ttu-id="0f321-113">toomove una máquina virtual y su grupo de recursos tooanother de recursos, utilice hello **mover recursos de azure** comando de CLI.</span><span class="sxs-lookup"><span data-stu-id="0f321-113">toomove a VM and its resources tooanother resource group, use hello **azure resource move** CLI command.</span></span> <span data-ttu-id="0f321-114">Hola de ejemplo siguiente muestra cómo toomove una máquina virtual y los recursos más comunes de hello requiere.</span><span class="sxs-lookup"><span data-stu-id="0f321-114">hello following example shows how toomove a VM and hello most common resources it requires.</span></span> <span data-ttu-id="0f321-115">Usamos hello **-i** parámetro y pase una-lista separados por comas (sin espacios) de identificadores para hello recursos toomove.</span><span class="sxs-lookup"><span data-stu-id="0f321-115">We use hello **-i** parameter and pass in a comma-separated list (without spaces) of IDs for hello resources toomove.</span></span>

    vm=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Compute/virtualMachines/<vmName>
    nic=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkInterfaces/<nicName>
    nsg=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/networkSecurityGroups/<nsgName>
    pip=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/publicIPAddresses/<publicIPName>
    vnet=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Network/virtualNetworks/<vnetName>
    diag=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<diagnosticStorageAccountName>
    storage=/subscriptions/<sourceSubscriptionID>/resourceGroups/<sourceResourceGroup>/providers/Microsoft.Storage/storageAccounts/<storageAcountName>      

    azure resource move --ids $vm,$nic,$nsg,$pip,$vnet,$storage,$diag -d "<destinationResourceGroup>"

<span data-ttu-id="0f321-116">Si desea que toomove Hola VM y su suscripción de recursos de tooa diferente, agregue hello **--destino subscriptionId &#60; destinationSubscriptionID &#62;** suscripción de destino de parámetro toospecify Hola.</span><span class="sxs-lookup"><span data-stu-id="0f321-116">If you want toomove hello VM and its resources tooa different subscription, add hello **--destination-subscriptionId &#60;destinationSubscriptionID&#62;** parameter toospecify hello destination subscription.</span></span>

<span data-ttu-id="0f321-117">Si está trabajando desde Hola símbolo del sistema en un equipo Windows, deberá tooadd un  **$**  delante de los nombres de variable de saludo al declararlas.</span><span class="sxs-lookup"><span data-stu-id="0f321-117">If you are working from hello Command Prompt on a Windows computer, you need tooadd a **$** in front of hello variable names when you declare them.</span></span> <span data-ttu-id="0f321-118">Esto no es necesario en Linux.</span><span class="sxs-lookup"><span data-stu-id="0f321-118">This isn't needed in Linux.</span></span>

<span data-ttu-id="0f321-119">Se le pide tooconfirm que desea toomove Hola el recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="0f321-119">You are asked tooconfirm that you want toomove hello specified resource.</span></span> <span data-ttu-id="0f321-120">Tipo de **Y** tooconfirm que desea que los recursos de hello toomove.</span><span class="sxs-lookup"><span data-stu-id="0f321-120">Type **Y** tooconfirm that you want toomove hello resources.</span></span>

[!INCLUDE [virtual-machines-common-move-vm](../../../includes/virtual-machines-common-move-vm.md)]

## <a name="next-steps"></a><span data-ttu-id="0f321-121">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0f321-121">Next steps</span></span>
<span data-ttu-id="0f321-122">Puede mover muchos tipos diferentes de recursos entre suscripciones y grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f321-122">You can move many different types of resources between resource groups and subscriptions.</span></span> <span data-ttu-id="0f321-123">Para obtener más información, consulte [Mover grupo de recursos de toonew de recursos o suscripción](../../resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0f321-123">For more information, see [Move resources toonew resource group or subscription](../../resource-group-move-resources.md).</span></span>    

