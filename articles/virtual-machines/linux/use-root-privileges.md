---
title: "Uso de privilegios raíz en máquinas virtuales Linux | Microsoft Docs"
description: "Aprenda a usar privilegios raíz en una máquina virtual de Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="f3f9c-103">Uso de privilegios raíz en máquinas virtuales con Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="f3f9c-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f3f9c-104">De forma predeterminada, el usuario `root` está deshabilitado en las máquinas virtuales Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="f3f9c-105">Los usuarios pueden ejecutar comandos con privilegios elevados mediante el comando `sudo` .</span><span class="sxs-lookup"><span data-stu-id="f3f9c-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="f3f9c-106">Sin embargo, la experiencia puede variar dependiendo de la manera en que se aprovisionó el sistema.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="f3f9c-107">**Clave SSH y contraseña o solo contraseña**: la máquina virtual se aprovisionó con un certificado (archivo `.CER`) o una clave SSH, además de una contraseña, o solo un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="f3f9c-108">En este caso `sudo` solicitará la contraseña del usuario antes de ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="f3f9c-109">**Solo clave SSH**: la máquina virtual se aprovisionó con un certificado (archivo `.cer`, `.pem` o `.pub`) o una clave SSH, pero sin contraseña.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="f3f9c-110">En este caso `sudo` **no** solicitará la contraseña del usuario antes de ejecutar el comando.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="f3f9c-111">Clave SSH y contraseña o solo contraseña</span><span class="sxs-lookup"><span data-stu-id="f3f9c-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="f3f9c-112">Inicie sesión en la máquina virtual Linux usando la autenticación de clave SSH o contraseña y, a continuación, ejecute los comandos usando `sudo`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f3f9c-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="f3f9c-113">En este caso, se le solicitará al usuario una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="f3f9c-114">Después de escribir la contraseña, `sudo` ejecutará el comando con los privilegios `root`.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="f3f9c-115">También puede habilitar sudo sin contraseña, si edita el archivo `/etc/sudoers.d/waagent` , por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f3f9c-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="f3f9c-116">Este cambio permitirá que el usuario "azureuser" use sudo sin contraseña.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="f3f9c-117">Solo clave SSH</span><span class="sxs-lookup"><span data-stu-id="f3f9c-117">SSH Key Only</span></span>
<span data-ttu-id="f3f9c-118">Inicie sesión en la máquina virtual Linux usando la autenticación de clave SSH y, a continuación, ejecute los comandos usando `sudo`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="f3f9c-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="f3f9c-119">En este caso **no** se solicitará la contraseña al usuario.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="f3f9c-120">Después de presionar `<enter>`, `sudo` ejecutará el comando con privilegios `root`.</span><span class="sxs-lookup"><span data-stu-id="f3f9c-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>

