---
title: "Guía de inicio rápido de Azure Cloud Shell (versión preliminar) | Microsoft Docs"
description: "Guía de inicio rápido de Azure Cloud Shell"
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
ms.openlocfilehash: 75676eb0ab784e2adbfd27b170c1dee5599b74ac
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-for-using-the-azure-cloud-shell"></a><span data-ttu-id="52af6-103">Guía de inicio rápido de Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="52af6-103">Quickstart for using the Azure Cloud Shell</span></span>

<span data-ttu-id="52af6-104">En este documento se detalla cómo usar Azure Cloud Shell en [Azure Portal](https://ms.portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="52af6-104">This document details how to use the Azure Cloud Shell in the [Azure portal](https://ms.portal.azure.com/).</span></span>

## <a name="start-cloud-shell"></a><span data-ttu-id="52af6-105">Inicio de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="52af6-105">Start Cloud Shell</span></span>
1. <span data-ttu-id="52af6-106">Inicie **Cloud Shell** en la navegación superior de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="52af6-106">Launch **Cloud Shell** from the top navigation of the Azure portal</span></span> <br>
![](media/shell-icon.png)
2. <span data-ttu-id="52af6-107">Seleccione una suscripción para crear una cuenta de almacenamiento y un recurso compartido de archivos de Azure</span><span class="sxs-lookup"><span data-stu-id="52af6-107">Select a subscription to create a storage account and Azure file share</span></span>
3. <span data-ttu-id="52af6-108">Seleccione "Create storage" (Creación de almacenamiento)</span><span class="sxs-lookup"><span data-stu-id="52af6-108">Select "Create storage"</span></span>

> [!TIP]
> <span data-ttu-id="52af6-109">Usted se autentica automáticamente para la CLI de Azure 2.0 en todas las sesiones.</span><span class="sxs-lookup"><span data-stu-id="52af6-109">You are automatically authenticated for Azure CLI 2.0 in every sesssion.</span></span>

### <a name="set-your-subscription"></a><span data-ttu-id="52af6-110">Establecimiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="52af6-110">Set your subscription</span></span>
1. <span data-ttu-id="52af6-111">Enumere las suscripciones a las que tiene acceso:</span><span class="sxs-lookup"><span data-stu-id="52af6-111">List subscriptions you have access to:</span></span> <br>
`az account list`
2. <span data-ttu-id="52af6-112">Establezca su suscripción preferida:</span><span class="sxs-lookup"><span data-stu-id="52af6-112">Set your preferred subscription:</span></span> <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> <span data-ttu-id="52af6-113">La suscripción se recordará para sesiones futuras mediante `/home/<user>/.azure/azureProfile.json`.</span><span class="sxs-lookup"><span data-stu-id="52af6-113">Your subscription will be remembered for future sessions using `/home/<user>/.azure/azureProfile.json`.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="52af6-114">Crear un grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="52af6-114">Create a resource group</span></span>
<span data-ttu-id="52af6-115">Cree un nuevo grupo de recursos en la región oeste de EE. UU. llamado "MyRG":</span><span class="sxs-lookup"><span data-stu-id="52af6-115">Create a new resource group in WestUS named "MyRG":</span></span> <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a><span data-ttu-id="52af6-116">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="52af6-116">Create a Linux VM</span></span>
<span data-ttu-id="52af6-117">Cree una máquina virtual con Ubuntu en su nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="52af6-117">Create an Ubuntu VM in your new resource group.</span></span> <span data-ttu-id="52af6-118">La CLI de Azure 2.0 creará claves SSH y configurará la máquina virtual con ellas.</span><span class="sxs-lookup"><span data-stu-id="52af6-118">The Azure CLI 2.0 will create SSH keys and setup the VM with them.</span></span> <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> <span data-ttu-id="52af6-119">La CLI de Azure 2.0 coloca las claves públicas y privadas usadas para autenticar la máquina virtual en `/User/.ssh/id_rsa` y `/User/.ssh/id_rsa.pub` de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="52af6-119">The public and private keys used to authenticate your VM are placed in `/User/.ssh/id_rsa` and `/User/.ssh/id_rsa.pub` by Azure CLI 2.0 by default.</span></span> <span data-ttu-id="52af6-120">La carpeta .ssh se conserva en la imagen de 5 GB adjunta del recurso compartido de archivos de Azure.</span><span class="sxs-lookup"><span data-stu-id="52af6-120">Your .ssh folder is persisted in your attached Azure file share's 5-GB image.</span></span>

<span data-ttu-id="52af6-121">Su nombre de usuario en esta máquina virtual será el nombre de usuario utilizado en Cloud Shell ($User@Azure:).</span><span class="sxs-lookup"><span data-stu-id="52af6-121">Your username on this VM will be your username used in Cloud Shell ($User@Azure:).</span></span>

### <a name="ssh-into-your-linux-vm"></a><span data-ttu-id="52af6-122">Conexión SSH con la máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="52af6-122">SSH into your Linux VM</span></span>
1. <span data-ttu-id="52af6-123">Busque el nombre de la máquina virtual en la barra de búsqueda de Azure Portal</span><span class="sxs-lookup"><span data-stu-id="52af6-123">Search for your VM name in the Azure portal search bar</span></span>
2. <span data-ttu-id="52af6-124">Haga clic en "Conectar" y ejecute: `ssh username@ipaddress`</span><span class="sxs-lookup"><span data-stu-id="52af6-124">Click "Connect" and run: `ssh username@ipaddress`</span></span>

![](media/sshcmd-copy.png)

<span data-ttu-id="52af6-125">Al establecer la conexión SSH, debería ver el aviso de bienvenida de Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="52af6-125">Upon establishing the SSH connection, you should see the Ubuntu welcome prompt.</span></span>
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a><span data-ttu-id="52af6-126">Limpiar</span><span class="sxs-lookup"><span data-stu-id="52af6-126">Cleaning up</span></span> 
<span data-ttu-id="52af6-127">Elimine el grupo de recursos y cualquier recurso dentro del mismo:</span><span class="sxs-lookup"><span data-stu-id="52af6-127">Delete your resource group and any resources within it:</span></span> <br>
<span data-ttu-id="52af6-128">Ejecute `az group delete -n MyRG`</span><span class="sxs-lookup"><span data-stu-id="52af6-128">Run `az group delete -n MyRG`</span></span>

## <a name="next-steps"></a><span data-ttu-id="52af6-129">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="52af6-129">Next Steps</span></span>
[<span data-ttu-id="52af6-130">Obtenga información sobre la persistencia del almacenamiento en Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="52af6-130">Learn about persisting storage on Cloud Shell</span></span>](persisting-shell-storage.md) <br><span data-ttu-id="52af6-131">
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/)</span><span class="sxs-lookup"><span data-stu-id="52af6-131">
[Learn about Azure CLI 2.0](https://docs.microsoft.com/cli/azure/)</span></span> <br><span data-ttu-id="52af6-132">
[Información sobre Azure File Storage](../storage/files/storage-files-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="52af6-132">
[Learn about Azure File storage](../storage/files/storage-files-introduction.md)</span></span> <br>