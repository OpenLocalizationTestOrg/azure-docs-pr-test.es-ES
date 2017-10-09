---
title: "privilegios de raíz de aaaUse en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los privilegios de toouse raíz en una máquina virtual de Linux en Azure."
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
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="06bee-103">Uso de privilegios raíz en máquinas virtuales con Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="06bee-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="06bee-104">De forma predeterminada, Hola `root` usuario está deshabilitado en las máquinas virtuales de Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="06bee-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="06bee-105">Los usuarios pueden ejecutar comandos con privilegios elevados mediante el uso de hello `sudo` comando.</span><span class="sxs-lookup"><span data-stu-id="06bee-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="06bee-106">Sin embargo, la experiencia de Hola puede variar dependiendo de cómo se haya proporcionado el sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="06bee-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="06bee-107">**Clave SSH y contraseña OR solo** -máquina virtual de Hola se haya proporcionado con un certificado (`.CER` archivo) o clave SSH, así como una contraseña, o simplemente un nombre de usuario y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="06bee-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="06bee-108">En este caso `sudo` solicitará contraseña del usuario de hello antes de ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bee-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="06bee-109">**La clave SSH** -máquina virtual de Hola se haya proporcionado con un certificado (`.cer`, `.pem`, o `.pub` archivo) o clave SSH, pero no hay ninguna contraseña.</span><span class="sxs-lookup"><span data-stu-id="06bee-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="06bee-110">En este caso `sudo` **no** solicitar una contraseña de usuario de hello antes de ejecutar el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="06bee-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="06bee-111">Clave SSH y contraseña o solo contraseña</span><span class="sxs-lookup"><span data-stu-id="06bee-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="06bee-112">Inicie sesión en la máquina virtual de Linux de hello mediante la autenticación de clave o contraseña SSH, a continuación, ejecutar comandos mediante `sudo`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="06bee-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="06bee-113">En este caso usuario Hola le pedirá una contraseña.</span><span class="sxs-lookup"><span data-stu-id="06bee-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="06bee-114">Después de escribir la contraseña de hello `sudo` se ejecutará el comando hello con `root` privilegios.</span><span class="sxs-lookup"><span data-stu-id="06bee-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="06bee-115">También puede habilitar sudo passwordless mediante la edición de hello `/etc/sudoers.d/waagent` de archivos, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="06bee-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="06bee-116">Este cambio permitirá passwordless sudo usuario Hola "azureuser".</span><span class="sxs-lookup"><span data-stu-id="06bee-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="06bee-117">Solo clave SSH</span><span class="sxs-lookup"><span data-stu-id="06bee-117">SSH Key Only</span></span>
<span data-ttu-id="06bee-118">Inicie sesión en la máquina virtual de Linux de hello mediante la autenticación de clave SSH y vuelva a ejecutar comandos mediante `sudo`, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="06bee-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="06bee-119">En este caso le usuario hello **no** se le solicite una contraseña.</span><span class="sxs-lookup"><span data-stu-id="06bee-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="06bee-120">Después de presionar `<enter>`, `sudo` se ejecutará el comando hello con `root` privilegios.</span><span class="sxs-lookup"><span data-stu-id="06bee-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>

