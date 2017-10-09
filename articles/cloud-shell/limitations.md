---
title: "limitaciones de Shell en la nube (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Introducción a las limitaciones de Azure Cloud Shell"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="be301-103">Limitaciones de Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be301-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="be301-104">Shell de nube de Azure tiene los siguientes de hello limitaciones conocidas:</span><span class="sxs-lookup"><span data-stu-id="be301-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="be301-105">Persistencia y estado del sistema</span><span class="sxs-lookup"><span data-stu-id="be301-105">System state and persistence</span></span>
<span data-ttu-id="be301-106">máquina de Hola que proporciona la sesión de Shell en la nube es temporal y se recicla después de la sesión está inactiva durante 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="be301-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="be301-107">En la nube Shell requiere un toobe del recurso compartido de archivos montado.</span><span class="sxs-lookup"><span data-stu-id="be301-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="be301-108">Como resultado, la suscripción debe ser capaz de tooset una tooaccess de recursos de almacenamiento en la nube Shell.</span><span class="sxs-lookup"><span data-stu-id="be301-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="be301-109">Otras consideraciones:</span><span class="sxs-lookup"><span data-stu-id="be301-109">Other considerations include:</span></span>
* <span data-ttu-id="be301-110">Con el almacenamiento montado, solo se conservan las modificaciones de los directorios `$Home` o `clouddrive`.</span><span class="sxs-lookup"><span data-stu-id="be301-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="be301-111">Solo se pueden montar recursos compartidos de archivos desde la [región asignada](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="be301-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="be301-112">Azure Files solo admite cuentas de almacenamiento con redundancia local o de almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="be301-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="be301-113">Permisos de usuario</span><span class="sxs-lookup"><span data-stu-id="be301-113">User permissions</span></span>
<span data-ttu-id="be301-114">Los permisos se establecen como usuarios normales sin acceso a sudo.</span><span class="sxs-lookup"><span data-stu-id="be301-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="be301-115">No se conservará cualquier instalación fuera del directorio `$Home`.</span><span class="sxs-lookup"><span data-stu-id="be301-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="be301-116">Aunque ciertos comandos dentro de Hola `clouddrive` directorio, como `git clone`, no tiene los permisos adecuados, su `$Home` directorio tiene permisos.</span><span class="sxs-lookup"><span data-stu-id="be301-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="be301-117">Compatibilidad con exploradores</span><span class="sxs-lookup"><span data-stu-id="be301-117">Browser support</span></span>
<span data-ttu-id="be301-118">Shell de nube es compatible con versiones más recientes de Hola de Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox y Safari de Apple.</span><span class="sxs-lookup"><span data-stu-id="be301-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="be301-119">Safari en modo privado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="be301-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="be301-120">Copiar y pegar</span><span class="sxs-lookup"><span data-stu-id="be301-120">Copy and paste</span></span>
<span data-ttu-id="be301-121">CTRL+c y CTRL+v no funcionan como copiar y pegar accesos directos en el Shell de nube en máquinas con Windows, utilice Ctrl + Insert y MAYÚS+INS toocopy y pegue respectivamente.</span><span class="sxs-lookup"><span data-stu-id="be301-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="be301-122">Opciones de copiar y pegar del menú contextual también están disponibles, pero contextual función acceso de Portapapeles toobrowser específico de asunto.</span><span class="sxs-lookup"><span data-stu-id="be301-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="be301-123">Editar .bashrc</span><span class="sxs-lookup"><span data-stu-id="be301-123">Editing .bashrc</span></span>
<span data-ttu-id="be301-124">Tenga cuidado al editar .bashrc, ya que puede producir errores inesperados en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="be301-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="be301-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="be301-125">.bash_history</span></span>
<span data-ttu-id="be301-126">El historial de comandos de Bash puede ser incoherente debido a una interrupción de la sesión de Cloud Shell o a sesiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="be301-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="be301-127">Límites de uso</span><span class="sxs-lookup"><span data-stu-id="be301-127">Usage limits</span></span>
<span data-ttu-id="be301-128">Cloud Shell está pensado para casos de uso interactivos.</span><span class="sxs-lookup"><span data-stu-id="be301-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="be301-129">Por tanto, todas las sesiones que no sean de este tipo y que se prolonguen durante mucho tiempo se finalizarán sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="be301-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="be301-130">Conectividad de red</span><span class="sxs-lookup"><span data-stu-id="be301-130">Network connectivity</span></span>
<span data-ttu-id="be301-131">Tiempos de espera en el Shell de nube es conectividad a internet toolocal asunto, Shell de nube continúa tooattempt toocarry espera las instrucciones que se envíen.</span><span class="sxs-lookup"><span data-stu-id="be301-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be301-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be301-132">Next steps</span></span>
[<span data-ttu-id="be301-133">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="be301-133">Cloud Shell Quickstart</span></span>](quickstart.md)
