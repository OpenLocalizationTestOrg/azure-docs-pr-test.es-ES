---
title: "Limitaciones de Azure Cloud Shell (versión preliminar) | Microsoft Docs"
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
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="445a5-103">Limitaciones de Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="445a5-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="445a5-104">Azure Cloud Shell tiene las limitaciones conocidas siguientes:</span><span class="sxs-lookup"><span data-stu-id="445a5-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="445a5-105">Persistencia y estado del sistema</span><span class="sxs-lookup"><span data-stu-id="445a5-105">System state and persistence</span></span>
<span data-ttu-id="445a5-106">La máquina que proporciona la sesión de Cloud Shell es temporal y se recicla después de que la sesión esté inactiva durante 20 minutos.</span><span class="sxs-lookup"><span data-stu-id="445a5-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="445a5-107">Cloud Shell requiere montar un recurso compartido de archivos.</span><span class="sxs-lookup"><span data-stu-id="445a5-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="445a5-108">Como resultado, la suscripción debe poder configurar los recursos de almacenamiento para tener acceso a Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="445a5-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="445a5-109">Otras consideraciones:</span><span class="sxs-lookup"><span data-stu-id="445a5-109">Other considerations include:</span></span>
* <span data-ttu-id="445a5-110">Con el almacenamiento montado, solo se conservan las modificaciones de los directorios `$Home` o `clouddrive`.</span><span class="sxs-lookup"><span data-stu-id="445a5-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="445a5-111">Solo se pueden montar recursos compartidos de archivos desde la [región asignada](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="445a5-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="445a5-112">Azure Files solo admite cuentas de almacenamiento con redundancia local o de almacenamiento con redundancia geográfica.</span><span class="sxs-lookup"><span data-stu-id="445a5-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="445a5-113">Permisos de usuario</span><span class="sxs-lookup"><span data-stu-id="445a5-113">User permissions</span></span>
<span data-ttu-id="445a5-114">Los permisos se establecen como usuarios normales sin acceso a sudo.</span><span class="sxs-lookup"><span data-stu-id="445a5-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="445a5-115">No se conservará cualquier instalación fuera del directorio `$Home`.</span><span class="sxs-lookup"><span data-stu-id="445a5-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="445a5-116">Aunque algunos comandos del directorio `clouddrive`, como `git clone`, no tienen los permisos adecuados, el directorio `$Home` sí los tiene.</span><span class="sxs-lookup"><span data-stu-id="445a5-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="445a5-117">Compatibilidad con exploradores</span><span class="sxs-lookup"><span data-stu-id="445a5-117">Browser support</span></span>
<span data-ttu-id="445a5-118">Cloud Shell es compatible con las versiones más recientes de Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox y Safari de Apple.</span><span class="sxs-lookup"><span data-stu-id="445a5-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="445a5-119">Safari en modo privado no es compatible.</span><span class="sxs-lookup"><span data-stu-id="445a5-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="445a5-120">Copiar y pegar</span><span class="sxs-lookup"><span data-stu-id="445a5-120">Copy and paste</span></span>
<span data-ttu-id="445a5-121">Ctrl+C y Ctrl+V no funcionan como métodos abreviados de teclado para copiar y pegar en equipos Windows, use Ctrl+Insert y Mayús+Insert para copiar y pegar respectivamente.</span><span class="sxs-lookup"><span data-stu-id="445a5-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="445a5-122">También se puede hacer clic con el botón derecho para copiar y pegar, pero dependerá del acceso al Portapapeles que tenga cada explorador.</span><span class="sxs-lookup"><span data-stu-id="445a5-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="445a5-123">Editar .bashrc</span><span class="sxs-lookup"><span data-stu-id="445a5-123">Editing .bashrc</span></span>
<span data-ttu-id="445a5-124">Tenga cuidado al editar .bashrc, ya que puede producir errores inesperados en Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="445a5-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="445a5-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="445a5-125">.bash_history</span></span>
<span data-ttu-id="445a5-126">El historial de comandos de Bash puede ser incoherente debido a una interrupción de la sesión de Cloud Shell o a sesiones simultáneas.</span><span class="sxs-lookup"><span data-stu-id="445a5-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="445a5-127">Límites de uso</span><span class="sxs-lookup"><span data-stu-id="445a5-127">Usage limits</span></span>
<span data-ttu-id="445a5-128">Cloud Shell está pensado para casos de uso interactivos.</span><span class="sxs-lookup"><span data-stu-id="445a5-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="445a5-129">Por tanto, todas las sesiones que no sean de este tipo y que se prolonguen durante mucho tiempo se finalizarán sin previo aviso.</span><span class="sxs-lookup"><span data-stu-id="445a5-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="445a5-130">Conectividad de red</span><span class="sxs-lookup"><span data-stu-id="445a5-130">Network connectivity</span></span>
<span data-ttu-id="445a5-131">La latencia de Cloud Shell está sujeta a la conectividad de Internet local, Cloud Shell seguirá tratando de ejecutar las instrucciones enviadas.</span><span class="sxs-lookup"><span data-stu-id="445a5-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="445a5-132">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="445a5-132">Next steps</span></span>
[<span data-ttu-id="445a5-133">Inicio rápido de Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="445a5-133">Cloud Shell Quickstart</span></span>](quickstart.md)
