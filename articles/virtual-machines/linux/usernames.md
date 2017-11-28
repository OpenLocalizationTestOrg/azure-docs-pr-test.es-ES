---
title: "Selección de nombres de usuario para Linux | Microsoft Docs"
description: "Aprenda a seleccionar nombres de usuario para una máquina virtual de Linux en Azure."
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
ms.openlocfilehash: 1874d72e5f88816036667932371ff28704d186c8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a><span data-ttu-id="afe20-103">Selección de nombres de usuario para Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="afe20-103">Selecting User Names for Linux on Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="afe20-104">Cuando aprovisiona una máquina virtual con Linux en Azure, debe especificar el nombre de un usuario no raíz que más adelante pueda usar para iniciar sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="afe20-104">When you provision a Linux virtual machine on Azure you must specify the name of a non-root user that you can later use to log into the VM.</span></span> <span data-ttu-id="afe20-105">Puede elegir el nombre del nuevo usuario o, si el aprovisionamiento es a través del Portal de Azure clásico, puede aceptar el nombre predeterminado "azureuser".</span><span class="sxs-lookup"><span data-stu-id="afe20-105">You may choose the name of the new user, or if provisioning via the Azure classic portal you can accept the default name "azureuser".</span></span>

<span data-ttu-id="afe20-106">En la mayoría de los casos, este usuario no existirá en la imagen base y se creará durante el proceso de aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="afe20-106">In most cases this user won't exist on the base image and will be created during the provisioning process.</span></span> <span data-ttu-id="afe20-107">Si el usuario ya existe en la imagen de máquina virtual base, el agente Linux de Azure configura simplemente la contraseña (o la clave SSH) para ese usuario de acuerdo con la información especificada al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="afe20-107">If the user exists on the base VM image, then the Azure Linux agent simply configures the password and/or SSH key for that user based on the information you specified when creating the VM.</span></span>

<span data-ttu-id="afe20-108">**Sin embargo**, Linux define un conjunto de nombres de usuario que no se deben usar al crear usuarios nuevos.</span><span class="sxs-lookup"><span data-stu-id="afe20-108">**However**, Linux defines a set of user names that should not be used.</span></span> <span data-ttu-id="afe20-109">El proceso de aprovisionamiento generará un **error** si trata de aprovisionar una máquina virtual Linux con un usuario del sistema existente, que se define como un usuario con UID 0-99.</span><span class="sxs-lookup"><span data-stu-id="afe20-109">The provisioning process will **fail** if you try to provision a Linux VM using an existing system user, which is defined as a user with UID 0-99.</span></span> <span data-ttu-id="afe20-110">Un ejemplo típico es el usuario `root` , que tiene el UID de 0.</span><span class="sxs-lookup"><span data-stu-id="afe20-110">A typical example is the `root` user, which has UID 0.</span></span>

* <span data-ttu-id="afe20-111">Consulte también: [Base estándar de Linux - Intervalos de identificadores de usuarios](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span><span class="sxs-lookup"><span data-stu-id="afe20-111">See also: [Linux Standard Base - User ID Ranges](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)</span></span>

<span data-ttu-id="afe20-112">A continuación encontrará una lista de usuarios de sistema integrados comunes para CentOS y Ubuntu que se debe intentar no usar al aprovisionar una máquina virtual Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="afe20-112">The following is a list of common built-in system users for CentOS and Ubuntu that you should avoid using when provisioning a Linux virtual machine on Azure.</span></span> <span data-ttu-id="afe20-113">Esta lista es solo un ejemplo, consulte la documentación de su distribución para asegurarse de que el nombre de usuario que elija no entra en conflicto con un usuario existente del sistema.</span><span class="sxs-lookup"><span data-stu-id="afe20-113">This list is just an example, please refer to the documentation for your distribution to ensure that the username you choose does not conflict with an existing system user.</span></span>

## <a name="centos"></a><span data-ttu-id="afe20-114">CentOS</span><span class="sxs-lookup"><span data-stu-id="afe20-114">CentOS</span></span>
* <span data-ttu-id="afe20-115">abrt</span><span class="sxs-lookup"><span data-stu-id="afe20-115">abrt</span></span>
* <span data-ttu-id="afe20-116">adm</span><span class="sxs-lookup"><span data-stu-id="afe20-116">adm</span></span>
* <span data-ttu-id="afe20-117">audio</span><span class="sxs-lookup"><span data-stu-id="afe20-117">audio</span></span>
* <span data-ttu-id="afe20-118">bin</span><span class="sxs-lookup"><span data-stu-id="afe20-118">bin</span></span>
* <span data-ttu-id="afe20-119">cdrom</span><span class="sxs-lookup"><span data-stu-id="afe20-119">cdrom</span></span>
* <span data-ttu-id="afe20-120">cgred</span><span class="sxs-lookup"><span data-stu-id="afe20-120">cgred</span></span>
* <span data-ttu-id="afe20-121">daemon</span><span class="sxs-lookup"><span data-stu-id="afe20-121">daemon</span></span>
* <span data-ttu-id="afe20-122">dbus</span><span class="sxs-lookup"><span data-stu-id="afe20-122">dbus</span></span>
* <span data-ttu-id="afe20-123">dialout</span><span class="sxs-lookup"><span data-stu-id="afe20-123">dialout</span></span>
* <span data-ttu-id="afe20-124">dip</span><span class="sxs-lookup"><span data-stu-id="afe20-124">dip</span></span>
* <span data-ttu-id="afe20-125">disk</span><span class="sxs-lookup"><span data-stu-id="afe20-125">disk</span></span>
* <span data-ttu-id="afe20-126">floppy</span><span class="sxs-lookup"><span data-stu-id="afe20-126">floppy</span></span>
* <span data-ttu-id="afe20-127">ftp</span><span class="sxs-lookup"><span data-stu-id="afe20-127">ftp</span></span>
* <span data-ttu-id="afe20-128">ftp</span><span class="sxs-lookup"><span data-stu-id="afe20-128">ftp</span></span>
* <span data-ttu-id="afe20-129">games</span><span class="sxs-lookup"><span data-stu-id="afe20-129">games</span></span>
* <span data-ttu-id="afe20-130">gopher</span><span class="sxs-lookup"><span data-stu-id="afe20-130">gopher</span></span>
* <span data-ttu-id="afe20-131">haldaemon</span><span class="sxs-lookup"><span data-stu-id="afe20-131">haldaemon</span></span>
* <span data-ttu-id="afe20-132">halt</span><span class="sxs-lookup"><span data-stu-id="afe20-132">halt</span></span>
* <span data-ttu-id="afe20-133">kmem</span><span class="sxs-lookup"><span data-stu-id="afe20-133">kmem</span></span>
* <span data-ttu-id="afe20-134">lock</span><span class="sxs-lookup"><span data-stu-id="afe20-134">lock</span></span>
* <span data-ttu-id="afe20-135">lp</span><span class="sxs-lookup"><span data-stu-id="afe20-135">lp</span></span>
* <span data-ttu-id="afe20-136">mail</span><span class="sxs-lookup"><span data-stu-id="afe20-136">mail</span></span>
* <span data-ttu-id="afe20-137">man</span><span class="sxs-lookup"><span data-stu-id="afe20-137">man</span></span>
* <span data-ttu-id="afe20-138">mem</span><span class="sxs-lookup"><span data-stu-id="afe20-138">mem</span></span>
* <span data-ttu-id="afe20-139">nfsnobody</span><span class="sxs-lookup"><span data-stu-id="afe20-139">nfsnobody</span></span>
* <span data-ttu-id="afe20-140">nobody</span><span class="sxs-lookup"><span data-stu-id="afe20-140">nobody</span></span>
* <span data-ttu-id="afe20-141">ntp</span><span class="sxs-lookup"><span data-stu-id="afe20-141">ntp</span></span>
* <span data-ttu-id="afe20-142">operator</span><span class="sxs-lookup"><span data-stu-id="afe20-142">operator</span></span>
* <span data-ttu-id="afe20-143">oprofile</span><span class="sxs-lookup"><span data-stu-id="afe20-143">oprofile</span></span>
* <span data-ttu-id="afe20-144">postdrop</span><span class="sxs-lookup"><span data-stu-id="afe20-144">postdrop</span></span>
* <span data-ttu-id="afe20-145">postfix</span><span class="sxs-lookup"><span data-stu-id="afe20-145">postfix</span></span>
* <span data-ttu-id="afe20-146">qpidd</span><span class="sxs-lookup"><span data-stu-id="afe20-146">qpidd</span></span>
* <span data-ttu-id="afe20-147">root</span><span class="sxs-lookup"><span data-stu-id="afe20-147">root</span></span>
* <span data-ttu-id="afe20-148">rpc</span><span class="sxs-lookup"><span data-stu-id="afe20-148">rpc</span></span>
* <span data-ttu-id="afe20-149">rpcuser</span><span class="sxs-lookup"><span data-stu-id="afe20-149">rpcuser</span></span>
* <span data-ttu-id="afe20-150">saslauth</span><span class="sxs-lookup"><span data-stu-id="afe20-150">saslauth</span></span>
* <span data-ttu-id="afe20-151">shutdown</span><span class="sxs-lookup"><span data-stu-id="afe20-151">shutdown</span></span>
* <span data-ttu-id="afe20-152">slocate</span><span class="sxs-lookup"><span data-stu-id="afe20-152">slocate</span></span>
* <span data-ttu-id="afe20-153">sshd</span><span class="sxs-lookup"><span data-stu-id="afe20-153">sshd</span></span>
* <span data-ttu-id="afe20-154">stapdev</span><span class="sxs-lookup"><span data-stu-id="afe20-154">stapdev</span></span>
* <span data-ttu-id="afe20-155">stapusr</span><span class="sxs-lookup"><span data-stu-id="afe20-155">stapusr</span></span>
* <span data-ttu-id="afe20-156">sync</span><span class="sxs-lookup"><span data-stu-id="afe20-156">sync</span></span>
* <span data-ttu-id="afe20-157">sys</span><span class="sxs-lookup"><span data-stu-id="afe20-157">sys</span></span>
* <span data-ttu-id="afe20-158">tape</span><span class="sxs-lookup"><span data-stu-id="afe20-158">tape</span></span>
* <span data-ttu-id="afe20-159">test</span><span class="sxs-lookup"><span data-stu-id="afe20-159">test</span></span>
* <span data-ttu-id="afe20-160">tcpdump</span><span class="sxs-lookup"><span data-stu-id="afe20-160">tcpdump</span></span>
* <span data-ttu-id="afe20-161">tty</span><span class="sxs-lookup"><span data-stu-id="afe20-161">tty</span></span>
* <span data-ttu-id="afe20-162">users</span><span class="sxs-lookup"><span data-stu-id="afe20-162">users</span></span>
* <span data-ttu-id="afe20-163">utempter</span><span class="sxs-lookup"><span data-stu-id="afe20-163">utempter</span></span>
* <span data-ttu-id="afe20-164">utmp</span><span class="sxs-lookup"><span data-stu-id="afe20-164">utmp</span></span>
* <span data-ttu-id="afe20-165">uucp</span><span class="sxs-lookup"><span data-stu-id="afe20-165">uucp</span></span>
* <span data-ttu-id="afe20-166">vcsa</span><span class="sxs-lookup"><span data-stu-id="afe20-166">vcsa</span></span>
* <span data-ttu-id="afe20-167">video</span><span class="sxs-lookup"><span data-stu-id="afe20-167">video</span></span>
* <span data-ttu-id="afe20-168">wheel</span><span class="sxs-lookup"><span data-stu-id="afe20-168">wheel</span></span>

## <a name="ubuntu"></a><span data-ttu-id="afe20-169">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="afe20-169">Ubuntu</span></span>
* <span data-ttu-id="afe20-170">adm</span><span class="sxs-lookup"><span data-stu-id="afe20-170">adm</span></span>
* <span data-ttu-id="afe20-171">admin</span><span class="sxs-lookup"><span data-stu-id="afe20-171">admin</span></span>
* <span data-ttu-id="afe20-172">audio</span><span class="sxs-lookup"><span data-stu-id="afe20-172">audio</span></span>
* <span data-ttu-id="afe20-173">backup</span><span class="sxs-lookup"><span data-stu-id="afe20-173">backup</span></span>
* <span data-ttu-id="afe20-174">bin</span><span class="sxs-lookup"><span data-stu-id="afe20-174">bin</span></span>
* <span data-ttu-id="afe20-175">cdrom</span><span class="sxs-lookup"><span data-stu-id="afe20-175">cdrom</span></span>
* <span data-ttu-id="afe20-176">crontab</span><span class="sxs-lookup"><span data-stu-id="afe20-176">crontab</span></span>
* <span data-ttu-id="afe20-177">daemon</span><span class="sxs-lookup"><span data-stu-id="afe20-177">daemon</span></span>
* <span data-ttu-id="afe20-178">dialout</span><span class="sxs-lookup"><span data-stu-id="afe20-178">dialout</span></span>
* <span data-ttu-id="afe20-179">dip</span><span class="sxs-lookup"><span data-stu-id="afe20-179">dip</span></span>
* <span data-ttu-id="afe20-180">disk</span><span class="sxs-lookup"><span data-stu-id="afe20-180">disk</span></span>
* <span data-ttu-id="afe20-181">fax</span><span class="sxs-lookup"><span data-stu-id="afe20-181">fax</span></span>
* <span data-ttu-id="afe20-182">floppy</span><span class="sxs-lookup"><span data-stu-id="afe20-182">floppy</span></span>
* <span data-ttu-id="afe20-183">fuse</span><span class="sxs-lookup"><span data-stu-id="afe20-183">fuse</span></span>
* <span data-ttu-id="afe20-184">games</span><span class="sxs-lookup"><span data-stu-id="afe20-184">games</span></span>
* <span data-ttu-id="afe20-185">gnats</span><span class="sxs-lookup"><span data-stu-id="afe20-185">gnats</span></span>
* <span data-ttu-id="afe20-186">irc</span><span class="sxs-lookup"><span data-stu-id="afe20-186">irc</span></span>
* <span data-ttu-id="afe20-187">kmem</span><span class="sxs-lookup"><span data-stu-id="afe20-187">kmem</span></span>
* <span data-ttu-id="afe20-188">landscape</span><span class="sxs-lookup"><span data-stu-id="afe20-188">landscape</span></span>
* <span data-ttu-id="afe20-189">libuuid</span><span class="sxs-lookup"><span data-stu-id="afe20-189">libuuid</span></span>
* <span data-ttu-id="afe20-190">list</span><span class="sxs-lookup"><span data-stu-id="afe20-190">list</span></span>
* <span data-ttu-id="afe20-191">lp</span><span class="sxs-lookup"><span data-stu-id="afe20-191">lp</span></span>
* <span data-ttu-id="afe20-192">mail</span><span class="sxs-lookup"><span data-stu-id="afe20-192">mail</span></span>
* <span data-ttu-id="afe20-193">man</span><span class="sxs-lookup"><span data-stu-id="afe20-193">man</span></span>
* <span data-ttu-id="afe20-194">messagebus</span><span class="sxs-lookup"><span data-stu-id="afe20-194">messagebus</span></span>
* <span data-ttu-id="afe20-195">mlocate</span><span class="sxs-lookup"><span data-stu-id="afe20-195">mlocate</span></span>
* <span data-ttu-id="afe20-196">netdev</span><span class="sxs-lookup"><span data-stu-id="afe20-196">netdev</span></span>
* <span data-ttu-id="afe20-197">news</span><span class="sxs-lookup"><span data-stu-id="afe20-197">news</span></span>
* <span data-ttu-id="afe20-198">nobody</span><span class="sxs-lookup"><span data-stu-id="afe20-198">nobody</span></span>
* <span data-ttu-id="afe20-199">nogroup</span><span class="sxs-lookup"><span data-stu-id="afe20-199">nogroup</span></span>
* <span data-ttu-id="afe20-200">operator</span><span class="sxs-lookup"><span data-stu-id="afe20-200">operator</span></span>
* <span data-ttu-id="afe20-201">plugdev</span><span class="sxs-lookup"><span data-stu-id="afe20-201">plugdev</span></span>
* <span data-ttu-id="afe20-202">proxy</span><span class="sxs-lookup"><span data-stu-id="afe20-202">proxy</span></span>
* <span data-ttu-id="afe20-203">root</span><span class="sxs-lookup"><span data-stu-id="afe20-203">root</span></span>
* <span data-ttu-id="afe20-204">sasl</span><span class="sxs-lookup"><span data-stu-id="afe20-204">sasl</span></span>
* <span data-ttu-id="afe20-205">shadow</span><span class="sxs-lookup"><span data-stu-id="afe20-205">shadow</span></span>
* <span data-ttu-id="afe20-206">src</span><span class="sxs-lookup"><span data-stu-id="afe20-206">src</span></span>
* <span data-ttu-id="afe20-207">ssh</span><span class="sxs-lookup"><span data-stu-id="afe20-207">ssh</span></span>
* <span data-ttu-id="afe20-208">sshd</span><span class="sxs-lookup"><span data-stu-id="afe20-208">sshd</span></span>
* <span data-ttu-id="afe20-209">staff</span><span class="sxs-lookup"><span data-stu-id="afe20-209">staff</span></span>
* <span data-ttu-id="afe20-210">sudo</span><span class="sxs-lookup"><span data-stu-id="afe20-210">sudo</span></span>
* <span data-ttu-id="afe20-211">sync</span><span class="sxs-lookup"><span data-stu-id="afe20-211">sync</span></span>
* <span data-ttu-id="afe20-212">sys</span><span class="sxs-lookup"><span data-stu-id="afe20-212">sys</span></span>
* <span data-ttu-id="afe20-213">syslog</span><span class="sxs-lookup"><span data-stu-id="afe20-213">syslog</span></span>
* <span data-ttu-id="afe20-214">tape</span><span class="sxs-lookup"><span data-stu-id="afe20-214">tape</span></span>
* <span data-ttu-id="afe20-215">tty</span><span class="sxs-lookup"><span data-stu-id="afe20-215">tty</span></span>
* <span data-ttu-id="afe20-216">users</span><span class="sxs-lookup"><span data-stu-id="afe20-216">users</span></span>
* <span data-ttu-id="afe20-217">utmp</span><span class="sxs-lookup"><span data-stu-id="afe20-217">utmp</span></span>
* <span data-ttu-id="afe20-218">uucp</span><span class="sxs-lookup"><span data-stu-id="afe20-218">uucp</span></span>
* <span data-ttu-id="afe20-219">video</span><span class="sxs-lookup"><span data-stu-id="afe20-219">video</span></span>
* <span data-ttu-id="afe20-220">voice</span><span class="sxs-lookup"><span data-stu-id="afe20-220">voice</span></span>
* <span data-ttu-id="afe20-221">whoopsie</span><span class="sxs-lookup"><span data-stu-id="afe20-221">whoopsie</span></span>
* <span data-ttu-id="afe20-222">www-data</span><span class="sxs-lookup"><span data-stu-id="afe20-222">www-data</span></span>

