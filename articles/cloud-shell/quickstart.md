---
title: "Inicio rápido de nube Shell (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Inicio rápido para hello Shell en la nube de Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a><span data-ttu-id="6ce0e-103">Inicio rápido para usar Hola Shell en la nube de Azure</span><span class="sxs-lookup"><span data-stu-id="6ce0e-103">Quickstart for using hello Azure Cloud Shell</span></span>

<span data-ttu-id="6ce0e-104">Este documento detalla cómo toouse Hola Shell en la nube de Azure en hello [portal de Azure](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6ce0e-104">This document details how toouse hello Azure Cloud Shell in hello [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="6ce0e-105">Inicio de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="6ce0e-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="6ce0e-106">Iniciar **Shell en la nube** de navegación superior de Hola de hello portal de Azure</span><span class="sxs-lookup"><span data-stu-id="6ce0e-106">Launch **Cloud Shell** from hello top navigation of hello Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="6ce0e-107">Seleccione una suscripción toocreate una cuenta de almacenamiento y el recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="6ce0e-107">Select a subscription toocreate a storage account and Azure file share</span></span>
3. <span data-ttu-id="6ce0e-108">Seleccione "Create storage" (Creación de almacenamiento)</span><span class="sxs-lookup"><span data-stu-id="6ce0e-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="6ce0e-109">Usted se autentica automáticamente para la CLI de Azure 2.0 en todas las sesiones.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="6ce0e-110">Establecimiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="6ce0e-110">Set your subscription</span></span>
1. <span data-ttu-id="6ce0e-111">Enumere las suscripciones a las que tiene acceso:</span><span class="sxs-lookup"><span data-stu-id="6ce0e-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="6ce0e-112">Establezca su suscripción preferida:</span><span class="sxs-lookup"><span data-stu-id="6ce0e-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="6ce0e-113">La suscripción se recordará para sesiones futuras mediante `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="6ce0e-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6ce0e-114">Create a resource group</span></span>
<span data-ttu-id="6ce0e-115">Cree un nuevo grupo de recursos en la región oeste de EE. UU. llamado "MyRG":</span><span class="sxs-lookup"><span data-stu-id="6ce0e-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="6ce0e-116">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="6ce0e-116">Create a Linux VM</span></span>
<span data-ttu-id="6ce0e-117">Cree una máquina virtual con Ubuntu en su nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="6ce0e-118">Hola 2.0 de CLI de Azure creará las claves de SSH y el programa de instalación Hola VM con ellos.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-118">hello Azure CLI 2.0 will create SSH keys and setup hello VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="6ce0e-119">Hola tooauthenticate de claves pública y privada que usa la máquina virtual se colocan en `/User/.ssh/id_rsa` y `/User/.ssh/id_rsa.pub` 2.0 de CLI de Azure de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-119">hello public and private keys used tooauthenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="6ce0e-120">La carpeta .ssh se conserva en la imagen de 5 GB adjunta del recurso compartido de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="6ce0e-121">Su nombre de usuario en esta máquina virtual será el nombre de usuario utilizado en Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="6ce0e-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="6ce0e-122">Conexión SSH con la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="6ce0e-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="6ce0e-123">Buscar el nombre de máquina virtual en la barra de búsqueda del portal Azure de Hola</span><span class="sxs-lookup"><span data-stu-id="6ce0e-123">Search for your VM name in hello Azure portal search bar</span></span>
2. <span data-ttu-id="6ce0e-124">Haga clic en "Conectar" y ejecute: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="6ce0e-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="6ce0e-125">Al establecer la conexión de SSH de hello, debería ver mensaje bienvenida de hello Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="6ce0e-125">Upon establishing hello SSH connection, you should see hello Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="6ce0e-126">Limpiar</span><span class="sxs-lookup"><span data-stu-id="6ce0e-126">Cleaning up</span></span> 
<span data-ttu-id="6ce0e-127">Elimine el grupo de recursos y cualquier recurso dentro del mismo:</span><span class="sxs-lookup"><span data-stu-id="6ce0e-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="6ce0e-128">Ejecute `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="6ce0e-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ce0e-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="6ce0e-129">Next Steps</span></span>
[<span data-ttu-id="6ce0e-130">Obtenga información sobre la persistencia del almacenamiento en Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="6ce0e-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="6ce0e-131">
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="6ce0e-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="6ce0e-132">
[Información sobre Azure File Storage](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="6ce0e-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>