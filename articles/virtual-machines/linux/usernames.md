---
title: aaaSelecting nombres de usuario de Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooselect usuario asigna un nombre para una máquina virtual de Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="e11e9-103">Selección de nombres de usuario para Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="e11e9-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="e11e9-104">Cuando aprovisiona una máquina virtual de Linux en Azure debe especificar nombre de Hola de un usuario no es de raíz que posteriormente, puede usar toolog en hello VM.</span><span class="sxs-lookup"><span data-stu-id="e11e9-104">When you provision a Linux virtual machine on Azure you must specify hello name of a non-root user that you can later use toolog into hello VM.</span></span> <span data-ttu-id="e11e9-105">Puede elegir nombre Hola de nuevo usuario de hello, o si el aprovisionamiento a través de Hola portal de Azure clásico puede aceptar predeterminado Hola nombre "azureuser".</span><span class="sxs-lookup"><span data-stu-id="e11e9-105">You may choose hello name of hello new user, or if provisioning via hello Azure classic portal you can accept hello default name "azureuser".</span></span>

<span data-ttu-id="e11e9-106">En la mayoría de los casos, este usuario no existe en la imagen base hello y se creará durante el proceso de aprovisionamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e11e9-106">In most cases this user won't exist on hello base image and will be created during hello provisioning process.</span></span> <span data-ttu-id="e11e9-107">Si el usuario Hola existe en la imagen de máquina virtual base hello, a continuación, Hola Linux de Azure agente simplemente configura contraseña Hola o clave SSH para ese usuario basándose en información de Hola que especificó al crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e11e9-107">If hello user exists on hello base VM image, then hello Azure Linux agent simply configures hello password and/or SSH key for that user based on hello information you specified when creating hello VM.</span></span>

<span data-ttu-id="e11e9-108">**Sin embargo**, Linux define un conjunto de nombres de usuario que no se deben usar al crear usuarios nuevos.</span><span class="sxs-lookup"><span data-stu-id="e11e9-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="e11e9-109">Hola will del proceso de aprovisionamiento **producirá un error** si intentas tooprovision una VM de Linux con un usuario de sistema existente, que se define como un usuario con UID 0 y 99.</span><span class="sxs-lookup"><span data-stu-id="e11e9-109">hello provisioning process will **fail** if you try tooprovision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="e11e9-110">Un ejemplo típico es hello `root` usuario, que tiene el UID 0.</span><span class="sxs-lookup"><span data-stu-id="e11e9-110">A typical example is hello `root` user, which has UID 0.</span></span>

* <span data-ttu-id="e11e9-111">Consulte también: [Base estándar de Linux - Intervalos de identificadores de usuarios](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="e11e9-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="e11e9-112">Hola aquí te mostramos una lista de usuarios de sistema integradas comunes para CentOS y Ubuntu debe evitar el uso de al aprovisionar una máquina virtual de Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="e11e9-112">hello following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="e11e9-113">Esta lista es sólo un ejemplo, consulte toohello documentación para su distribución tooensure ese nombre de usuario de Hola que elija no entra en conflicto con un usuario del sistema existente.</span><span class="sxs-lookup"><span data-stu-id="e11e9-113">This list is just an example, please refer toohello documentation for your distribution tooensure that hello username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="e11e9-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="e11e9-114">CentOS</span></span>
* <span data-ttu-id="e11e9-115">abrt</span><span class="sxs-lookup"><span data-stu-id="e11e9-115">abrt</span></span>
* <span data-ttu-id="e11e9-116">adm</span><span class="sxs-lookup"><span data-stu-id="e11e9-116">adm</span></span>
* <span data-ttu-id="e11e9-117">audio</span><span class="sxs-lookup"><span data-stu-id="e11e9-117">audio</span></span>
* <span data-ttu-id="e11e9-118">bin</span><span class="sxs-lookup"><span data-stu-id="e11e9-118">bin</span></span>
* <span data-ttu-id="e11e9-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="e11e9-119">cdrom</span></span>
* <span data-ttu-id="e11e9-120">cgred</span><span class="sxs-lookup"><span data-stu-id="e11e9-120">cgred</span></span>
* <span data-ttu-id="e11e9-121">daemon</span><span class="sxs-lookup"><span data-stu-id="e11e9-121">daemon</span></span>
* <span data-ttu-id="e11e9-122">dbus</span><span class="sxs-lookup"><span data-stu-id="e11e9-122">dbus</span></span>
* <span data-ttu-id="e11e9-123">dialout</span><span class="sxs-lookup"><span data-stu-id="e11e9-123">dialout</span></span>
* <span data-ttu-id="e11e9-124">dip</span><span class="sxs-lookup"><span data-stu-id="e11e9-124">dip</span></span>
* <span data-ttu-id="e11e9-125">disk</span><span class="sxs-lookup"><span data-stu-id="e11e9-125">disk</span></span>
* <span data-ttu-id="e11e9-126">floppy</span><span class="sxs-lookup"><span data-stu-id="e11e9-126">floppy</span></span>
* <span data-ttu-id="e11e9-127">ftp</span><span class="sxs-lookup"><span data-stu-id="e11e9-127">ftp</span></span>
* <span data-ttu-id="e11e9-128">ftp</span><span class="sxs-lookup"><span data-stu-id="e11e9-128">ftp</span></span>
* <span data-ttu-id="e11e9-129">games</span><span class="sxs-lookup"><span data-stu-id="e11e9-129">games</span></span>
* <span data-ttu-id="e11e9-130">gopher</span><span class="sxs-lookup"><span data-stu-id="e11e9-130">gopher</span></span>
* <span data-ttu-id="e11e9-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="e11e9-131">haldaemon</span></span>
* <span data-ttu-id="e11e9-132">halt</span><span class="sxs-lookup"><span data-stu-id="e11e9-132">halt</span></span>
* <span data-ttu-id="e11e9-133">kmem</span><span class="sxs-lookup"><span data-stu-id="e11e9-133">kmem</span></span>
* <span data-ttu-id="e11e9-134">lock</span><span class="sxs-lookup"><span data-stu-id="e11e9-134">lock</span></span>
* <span data-ttu-id="e11e9-135">lp</span><span class="sxs-lookup"><span data-stu-id="e11e9-135">lp</span></span>
* <span data-ttu-id="e11e9-136">mail</span><span class="sxs-lookup"><span data-stu-id="e11e9-136">mail</span></span>
* <span data-ttu-id="e11e9-137">man</span><span class="sxs-lookup"><span data-stu-id="e11e9-137">man</span></span>
* <span data-ttu-id="e11e9-138">mem</span><span class="sxs-lookup"><span data-stu-id="e11e9-138">mem</span></span>
* <span data-ttu-id="e11e9-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="e11e9-139">nfsnobody</span></span>
* <span data-ttu-id="e11e9-140">nobody</span><span class="sxs-lookup"><span data-stu-id="e11e9-140">nobody</span></span>
* <span data-ttu-id="e11e9-141">ntp</span><span class="sxs-lookup"><span data-stu-id="e11e9-141">ntp</span></span>
* <span data-ttu-id="e11e9-142">operator</span><span class="sxs-lookup"><span data-stu-id="e11e9-142">operator</span></span>
* <span data-ttu-id="e11e9-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="e11e9-143">oprofile</span></span>
* <span data-ttu-id="e11e9-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="e11e9-144">postdrop</span></span>
* <span data-ttu-id="e11e9-145">postfix</span><span class="sxs-lookup"><span data-stu-id="e11e9-145">postfix</span></span>
* <span data-ttu-id="e11e9-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="e11e9-146">qpidd</span></span>
* <span data-ttu-id="e11e9-147">root</span><span class="sxs-lookup"><span data-stu-id="e11e9-147">root</span></span>
* <span data-ttu-id="e11e9-148">rpc</span><span class="sxs-lookup"><span data-stu-id="e11e9-148">rpc</span></span>
* <span data-ttu-id="e11e9-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="e11e9-149">rpcuser</span></span>
* <span data-ttu-id="e11e9-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="e11e9-150">saslauth</span></span>
* <span data-ttu-id="e11e9-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="e11e9-151">shutdown</span></span>
* <span data-ttu-id="e11e9-152">slocate</span><span class="sxs-lookup"><span data-stu-id="e11e9-152">slocate</span></span>
* <span data-ttu-id="e11e9-153">sshd</span><span class="sxs-lookup"><span data-stu-id="e11e9-153">sshd</span></span>
* <span data-ttu-id="e11e9-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="e11e9-154">stapdev</span></span>
* <span data-ttu-id="e11e9-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="e11e9-155">stapusr</span></span>
* <span data-ttu-id="e11e9-156">sync</span><span class="sxs-lookup"><span data-stu-id="e11e9-156">sync</span></span>
* <span data-ttu-id="e11e9-157">sys</span><span class="sxs-lookup"><span data-stu-id="e11e9-157">sys</span></span>
* <span data-ttu-id="e11e9-158">tape</span><span class="sxs-lookup"><span data-stu-id="e11e9-158">tape</span></span>
* <span data-ttu-id="e11e9-159">test</span><span class="sxs-lookup"><span data-stu-id="e11e9-159">test</span></span>
* <span data-ttu-id="e11e9-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="e11e9-160">tcpdump</span></span>
* <span data-ttu-id="e11e9-161">tty</span><span class="sxs-lookup"><span data-stu-id="e11e9-161">tty</span></span>
* <span data-ttu-id="e11e9-162">users</span><span class="sxs-lookup"><span data-stu-id="e11e9-162">users</span></span>
* <span data-ttu-id="e11e9-163">utempter</span><span class="sxs-lookup"><span data-stu-id="e11e9-163">utempter</span></span>
* <span data-ttu-id="e11e9-164">utmp</span><span class="sxs-lookup"><span data-stu-id="e11e9-164">utmp</span></span>
* <span data-ttu-id="e11e9-165">uucp</span><span class="sxs-lookup"><span data-stu-id="e11e9-165">uucp</span></span>
* <span data-ttu-id="e11e9-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="e11e9-166">vcsa</span></span>
* <span data-ttu-id="e11e9-167">video</span><span class="sxs-lookup"><span data-stu-id="e11e9-167">video</span></span>
* <span data-ttu-id="e11e9-168">wheel</span><span class="sxs-lookup"><span data-stu-id="e11e9-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="e11e9-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e11e9-169">Ubuntu</span></span>
* <span data-ttu-id="e11e9-170">adm</span><span class="sxs-lookup"><span data-stu-id="e11e9-170">adm</span></span>
* <span data-ttu-id="e11e9-171">admin</span><span class="sxs-lookup"><span data-stu-id="e11e9-171">admin</span></span>
* <span data-ttu-id="e11e9-172">audio</span><span class="sxs-lookup"><span data-stu-id="e11e9-172">audio</span></span>
* <span data-ttu-id="e11e9-173">backup</span><span class="sxs-lookup"><span data-stu-id="e11e9-173">backup</span></span>
* <span data-ttu-id="e11e9-174">bin</span><span class="sxs-lookup"><span data-stu-id="e11e9-174">bin</span></span>
* <span data-ttu-id="e11e9-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="e11e9-175">cdrom</span></span>
* <span data-ttu-id="e11e9-176">crontab</span><span class="sxs-lookup"><span data-stu-id="e11e9-176">crontab</span></span>
* <span data-ttu-id="e11e9-177">daemon</span><span class="sxs-lookup"><span data-stu-id="e11e9-177">daemon</span></span>
* <span data-ttu-id="e11e9-178">dialout</span><span class="sxs-lookup"><span data-stu-id="e11e9-178">dialout</span></span>
* <span data-ttu-id="e11e9-179">dip</span><span class="sxs-lookup"><span data-stu-id="e11e9-179">dip</span></span>
* <span data-ttu-id="e11e9-180">disk</span><span class="sxs-lookup"><span data-stu-id="e11e9-180">disk</span></span>
* <span data-ttu-id="e11e9-181">fax</span><span class="sxs-lookup"><span data-stu-id="e11e9-181">fax</span></span>
* <span data-ttu-id="e11e9-182">floppy</span><span class="sxs-lookup"><span data-stu-id="e11e9-182">floppy</span></span>
* <span data-ttu-id="e11e9-183">fuse</span><span class="sxs-lookup"><span data-stu-id="e11e9-183">fuse</span></span>
* <span data-ttu-id="e11e9-184">games</span><span class="sxs-lookup"><span data-stu-id="e11e9-184">games</span></span>
* <span data-ttu-id="e11e9-185">gnats</span><span class="sxs-lookup"><span data-stu-id="e11e9-185">gnats</span></span>
* <span data-ttu-id="e11e9-186">irc</span><span class="sxs-lookup"><span data-stu-id="e11e9-186">irc</span></span>
* <span data-ttu-id="e11e9-187">kmem</span><span class="sxs-lookup"><span data-stu-id="e11e9-187">kmem</span></span>
* <span data-ttu-id="e11e9-188">landscape</span><span class="sxs-lookup"><span data-stu-id="e11e9-188">landscape</span></span>
* <span data-ttu-id="e11e9-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="e11e9-189">libuuid</span></span>
* <span data-ttu-id="e11e9-190">list</span><span class="sxs-lookup"><span data-stu-id="e11e9-190">list</span></span>
* <span data-ttu-id="e11e9-191">lp</span><span class="sxs-lookup"><span data-stu-id="e11e9-191">lp</span></span>
* <span data-ttu-id="e11e9-192">mail</span><span class="sxs-lookup"><span data-stu-id="e11e9-192">mail</span></span>
* <span data-ttu-id="e11e9-193">man</span><span class="sxs-lookup"><span data-stu-id="e11e9-193">man</span></span>
* <span data-ttu-id="e11e9-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="e11e9-194">messagebus</span></span>
* <span data-ttu-id="e11e9-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="e11e9-195">mlocate</span></span>
* <span data-ttu-id="e11e9-196">netdev</span><span class="sxs-lookup"><span data-stu-id="e11e9-196">netdev</span></span>
* <span data-ttu-id="e11e9-197">news</span><span class="sxs-lookup"><span data-stu-id="e11e9-197">news</span></span>
* <span data-ttu-id="e11e9-198">nobody</span><span class="sxs-lookup"><span data-stu-id="e11e9-198">nobody</span></span>
* <span data-ttu-id="e11e9-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="e11e9-199">nogroup</span></span>
* <span data-ttu-id="e11e9-200">operator</span><span class="sxs-lookup"><span data-stu-id="e11e9-200">operator</span></span>
* <span data-ttu-id="e11e9-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="e11e9-201">plugdev</span></span>
* <span data-ttu-id="e11e9-202">proxy</span><span class="sxs-lookup"><span data-stu-id="e11e9-202">proxy</span></span>
* <span data-ttu-id="e11e9-203">root</span><span class="sxs-lookup"><span data-stu-id="e11e9-203">root</span></span>
* <span data-ttu-id="e11e9-204">sasl</span><span class="sxs-lookup"><span data-stu-id="e11e9-204">sasl</span></span>
* <span data-ttu-id="e11e9-205">shadow</span><span class="sxs-lookup"><span data-stu-id="e11e9-205">shadow</span></span>
* <span data-ttu-id="e11e9-206">src</span><span class="sxs-lookup"><span data-stu-id="e11e9-206">src</span></span>
* <span data-ttu-id="e11e9-207">ssh</span><span class="sxs-lookup"><span data-stu-id="e11e9-207">ssh</span></span>
* <span data-ttu-id="e11e9-208">sshd</span><span class="sxs-lookup"><span data-stu-id="e11e9-208">sshd</span></span>
* <span data-ttu-id="e11e9-209">staff</span><span class="sxs-lookup"><span data-stu-id="e11e9-209">staff</span></span>
* <span data-ttu-id="e11e9-210">sudo</span><span class="sxs-lookup"><span data-stu-id="e11e9-210">sudo</span></span>
* <span data-ttu-id="e11e9-211">sync</span><span class="sxs-lookup"><span data-stu-id="e11e9-211">sync</span></span>
* <span data-ttu-id="e11e9-212">sys</span><span class="sxs-lookup"><span data-stu-id="e11e9-212">sys</span></span>
* <span data-ttu-id="e11e9-213">syslog</span><span class="sxs-lookup"><span data-stu-id="e11e9-213">syslog</span></span>
* <span data-ttu-id="e11e9-214">tape</span><span class="sxs-lookup"><span data-stu-id="e11e9-214">tape</span></span>
* <span data-ttu-id="e11e9-215">tty</span><span class="sxs-lookup"><span data-stu-id="e11e9-215">tty</span></span>
* <span data-ttu-id="e11e9-216">users</span><span class="sxs-lookup"><span data-stu-id="e11e9-216">users</span></span>
* <span data-ttu-id="e11e9-217">utmp</span><span class="sxs-lookup"><span data-stu-id="e11e9-217">utmp</span></span>
* <span data-ttu-id="e11e9-218">uucp</span><span class="sxs-lookup"><span data-stu-id="e11e9-218">uucp</span></span>
* <span data-ttu-id="e11e9-219">video</span><span class="sxs-lookup"><span data-stu-id="e11e9-219">video</span></span>
* <span data-ttu-id="e11e9-220">voice</span><span class="sxs-lookup"><span data-stu-id="e11e9-220">voice</span></span>
* <span data-ttu-id="e11e9-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="e11e9-221">whoopsie</span></span>
* <span data-ttu-id="e11e9-222">www-data</span><span class="sxs-lookup"><span data-stu-id="e11e9-222">www-data</span></span>

