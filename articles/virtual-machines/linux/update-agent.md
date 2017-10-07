---
title: Hola aaaUpdate agente Linux de Azure desde GitHub | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooupdate agente Linux de Azure para la VM de Linux en la versión más reciente de Azure toohello desde GitHub"
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: f1f19300-987d-4f29-9393-9aba866f049c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: mingzhan
ms.openlocfilehash: 4ce7c56efc1e6563e6415f7687573f9fb9e7b4c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooupdate-hello-azure-linux-agent-on-a-vm"></a><span data-ttu-id="1857f-103">¿Cómo tooupdate Hola agente Linux de Azure en una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="1857f-103">How tooupdate hello Azure Linux Agent on a VM</span></span>

<span data-ttu-id="1857f-104">tooupdate su [agente Linux de Azure](https://github.com/Azure/WALinuxAgent) en una VM de Linux en Azure, ya debe tener:</span><span class="sxs-lookup"><span data-stu-id="1857f-104">tooupdate your [Azure Linux Agent](https://github.com/Azure/WALinuxAgent) on a Linux VM in Azure, you must already have:</span></span>

- <span data-ttu-id="1857f-105">Tener en Azure una VM que ejecuta Linux.</span><span class="sxs-lookup"><span data-stu-id="1857f-105">A running Linux VM in Azure.</span></span>
- <span data-ttu-id="1857f-106">Una VM de Linux de conexión toothat mediante SSH.</span><span class="sxs-lookup"><span data-stu-id="1857f-106">A connection toothat Linux VM using SSH.</span></span>

<span data-ttu-id="1857f-107">Siempre debe comprobar para un paquete en el repositorio de distribución de Linux de hello en primer lugar.</span><span class="sxs-lookup"><span data-stu-id="1857f-107">You should always check for a package in hello Linux distro repository first.</span></span> <span data-ttu-id="1857f-108">Es posible paquete Hola disponible no puede ser versión más reciente de hello, sin embargo, al habilitar actualización automática se asegurará Hola agente Linux siempre obtendrá la actualización más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1857f-108">It is possible hello package available may not be hello latest version, however, enabling autoupdate will ensure hello Linux Agent will always get hello latest update.</span></span> <span data-ttu-id="1857f-109">Si tiene problemas de instalación de los administradores de paquetes de saludo, debe buscar soporte técnico del proveedor de distribución de Hola.</span><span class="sxs-lookup"><span data-stu-id="1857f-109">Should you have issues installing from hello package managers, you should seek support from hello distro vendor.</span></span>

## <a name="updating-hello-azure-linux-agent"></a><span data-ttu-id="1857f-110">Actualizar Hola agente Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="1857f-110">Updating hello Azure Linux Agent</span></span>

## <a name="ubuntu"></a><span data-ttu-id="1857f-111">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1857f-111">Ubuntu</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-112">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-112">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="1857f-113">Actualización de la memoria caché del paquete</span><span class="sxs-lookup"><span data-stu-id="1857f-113">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-114">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-114">Install hello latest package version</span></span>

```bash
sudo apt-get install walinuxagent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-115">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-115">Ensure auto update is enabled</span></span>

<span data-ttu-id="1857f-116">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-116">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-117">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-117">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-118">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-118">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-119">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-119">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-120">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-120">Restart hello waagent service</span></span>

#### <a name="restart-agent-for-1404"></a><span data-ttu-id="1857f-121">Reinicio del agente para 14.04</span><span class="sxs-lookup"><span data-stu-id="1857f-121">Restart agent for 14.04</span></span>

```bash
initctl restart walinuxagent
```

#### <a name="restart-agent-for-1604--1704"></a><span data-ttu-id="1857f-122">Reinicio del agente para 16.04/17.04</span><span class="sxs-lookup"><span data-stu-id="1857f-122">Restart agent for 16.04 / 17.04</span></span>

```bash
systemctl restart walinuxagent.service
```

## <a name="debian"></a><span data-ttu-id="1857f-123">Debian</span><span class="sxs-lookup"><span data-stu-id="1857f-123">Debian</span></span>

### <a name="debian-7-wheezy"></a><span data-ttu-id="1857f-124">Debian 7 "Wheezy"</span><span class="sxs-lookup"><span data-stu-id="1857f-124">Debian 7 “Wheezy”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-125">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-125">Check your current package version</span></span>

```bash
dpkg -l | grep waagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="1857f-126">Actualización de la memoria caché del paquete</span><span class="sxs-lookup"><span data-stu-id="1857f-126">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-127">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-127">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```

#### <a name="enable-agent-auto-update"></a><span data-ttu-id="1857f-128">Habilitación de la actualización automática del agente</span><span class="sxs-lookup"><span data-stu-id="1857f-128">Enable agent auto update</span></span>
<span data-ttu-id="1857f-129">Esta versión de Debian no tiene una versión > = 2.0.16, lo que significa que AutoUpdate no está disponible en este caso.</span><span class="sxs-lookup"><span data-stu-id="1857f-129">This version of Debian does not have a version >= 2.0.16, therefore AutoUpdate is not available for it.</span></span> <span data-ttu-id="1857f-130">salida de Hello de hello encima comando le mostrará si se trata de un paquete de hello actualizada.</span><span class="sxs-lookup"><span data-stu-id="1857f-130">hello output from hello above command will show you if hello package is up-to-date.</span></span>

### <a name="debian-8-jessie--debian-9-stretch"></a><span data-ttu-id="1857f-131">Debian 8 "Jessie"/Debian 9 "Stretch"</span><span class="sxs-lookup"><span data-stu-id="1857f-131">Debian 8 “Jessie” / Debian 9 “Stretch”</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-132">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-132">Check your current package version</span></span>

```bash
apt list --installed | grep walinuxagent
```

#### <a name="update-package-cache"></a><span data-ttu-id="1857f-133">Actualización de la memoria caché del paquete</span><span class="sxs-lookup"><span data-stu-id="1857f-133">Update package cache</span></span>

```bash
sudo apt-get -qq update
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-134">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-134">Install hello latest package version</span></span>

```bash
sudo apt-get install waagent
```
#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-135">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-135">Ensure auto update is enabled</span></span> 

<span data-ttu-id="1857f-136">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-136">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-137">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-137">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-138">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-138">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-139">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-139">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-140">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-140">Restart hello waagent service</span></span>

```
sudo systemctl restart walinuxagent.service
```

## <a name="redhat--centos"></a><span data-ttu-id="1857f-141">Red Hat/CentOS</span><span class="sxs-lookup"><span data-stu-id="1857f-141">Redhat / CentOS</span></span>

### <a name="rhelcentos-6"></a><span data-ttu-id="1857f-142">RHEL/CentOS 6</span><span class="sxs-lookup"><span data-stu-id="1857f-142">RHEL/CentOS 6</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-143">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-143">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="1857f-144">Comprobación de las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="1857f-144">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-145">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-145">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-146">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-146">Ensure auto update is enabled</span></span> 

<span data-ttu-id="1857f-147">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-147">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-148">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-148">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-149">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-149">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-150">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-150">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-151">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-151">Restart hello waagent service</span></span>

```
sudo service waagent restart
```

### <a name="rhelcentos-7"></a><span data-ttu-id="1857f-152">RHEL/CentOS 7</span><span class="sxs-lookup"><span data-stu-id="1857f-152">RHEL/CentOS 7</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-153">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-153">Check your current package version</span></span>

```bash
sudo yum list WALinuxAgent
```

#### <a name="check-available-updates"></a><span data-ttu-id="1857f-154">Comprobación de las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="1857f-154">Check available updates</span></span>

```bash
sudo yum check-update WALinuxAgent
```

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-155">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-155">Install hello latest package version</span></span>

```bash
sudo yum install WALinuxAgent  
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-156">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-156">Ensure auto update is enabled</span></span> 

<span data-ttu-id="1857f-157">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-157">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-158">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-158">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-159">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-159">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-160">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-160">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-161">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-161">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="suse-sles"></a><span data-ttu-id="1857f-162">SUSE SLES</span><span class="sxs-lookup"><span data-stu-id="1857f-162">SUSE SLES</span></span>

### <a name="suse-sles-11-sp4"></a><span data-ttu-id="1857f-163">SUSE SLES 11 SP4</span><span class="sxs-lookup"><span data-stu-id="1857f-163">SUSE SLES 11 SP4</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-164">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-164">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="1857f-165">Comprobación de las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="1857f-165">Check available updates</span></span>

<span data-ttu-id="1857f-166">Hola por encima de la salida se mostrará si el paquete de hello está activo toodate.</span><span class="sxs-lookup"><span data-stu-id="1857f-166">hello above output will show you if hello package is up toodate.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-167">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-167">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-168">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-168">Ensure auto update is enabled</span></span> 

<span data-ttu-id="1857f-169">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-169">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-170">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-170">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-171">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-171">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-172">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-172">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-173">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-173">Restart hello waagent service</span></span>

```bash
sudo /etc/init.d/waagent restart
```

### <a name="suse-sles-12-sp2"></a><span data-ttu-id="1857f-174">SUSE SLES 12 SP2</span><span class="sxs-lookup"><span data-stu-id="1857f-174">SUSE SLES 12 SP2</span></span>

#### <a name="check-your-current-package-version"></a><span data-ttu-id="1857f-175">Comprobación de la versión del paquete actual</span><span class="sxs-lookup"><span data-stu-id="1857f-175">Check your current package version</span></span>

```bash
zypper info python-azure-agent
```

#### <a name="check-available-updates"></a><span data-ttu-id="1857f-176">Comprobación de las actualizaciones disponibles</span><span class="sxs-lookup"><span data-stu-id="1857f-176">Check available updates</span></span>

<span data-ttu-id="1857f-177">En la salida de hello de hello anterior, esto le mostrará si el paquete de hello está actualizada.</span><span class="sxs-lookup"><span data-stu-id="1857f-177">In hello output from hello above, this will show you if hello package is upto date.</span></span>

#### <a name="install-hello-latest-package-version"></a><span data-ttu-id="1857f-178">Instalar la versión más reciente de paquete de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-178">Install hello latest package version</span></span>

```bash
sudo zypper install python-azure-agent
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-179">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-179">Ensure auto update is enabled</span></span> 

<span data-ttu-id="1857f-180">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-180">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-181">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-181">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-182">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-182">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-183">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-183">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="restart-hello-waagent-service"></a><span data-ttu-id="1857f-184">Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-184">Restart hello waagent service</span></span>

```bash
sudo systemctl restart waagent.service
```

## <a name="oracle-6-and-7"></a><span data-ttu-id="1857f-185">Oracle 6 y 7</span><span class="sxs-lookup"><span data-stu-id="1857f-185">Oracle 6 and 7</span></span>

<span data-ttu-id="1857f-186">Para Oracle Linux, asegúrese de que ese hello `Addons` repositorio está habilitado.</span><span class="sxs-lookup"><span data-stu-id="1857f-186">For Oracle Linux, make sure that hello `Addons` repository is enabled.</span></span> <span data-ttu-id="1857f-187">Elija el archivo de hello tooedit `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) o `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux) y cambie la línea hello `enabled=0` demasiado`enabled=1` en **[ol6_addons]** o **[ol7_addons]** en este archivo.</span><span class="sxs-lookup"><span data-stu-id="1857f-187">Choose tooedit hello file `/etc/yum.repos.d/public-yum-ol6.repo`(Oracle Linux 6) or `/etc/yum.repos.d/public-yum-ol7.repo`(Oracle Linux), and change hello line `enabled=0` too`enabled=1` under **[ol6_addons]** or **[ol7_addons]** in this file.</span></span>

<span data-ttu-id="1857f-188">A continuación, la versión de más reciente de hello tooinstall de hello agente Linux de Azure, tipo:</span><span class="sxs-lookup"><span data-stu-id="1857f-188">Then, tooinstall hello latest version of hello Azure Linux Agent, type:</span></span>

```bash
sudo yum install WALinuxAgent
```

<span data-ttu-id="1857f-189">Si no encuentra el repositorio de complemento de hello simplemente puede agregar estas líneas al final de hello del archivo .repo según la versión de Oracle Linux tooyour:</span><span class="sxs-lookup"><span data-stu-id="1857f-189">If you don't find hello add-on repository you can simply add these lines at hello end of your .repo file according tooyour Oracle Linux release:</span></span>

<span data-ttu-id="1857f-190">Para las máquinas virtuales Oracle Linux 6:</span><span class="sxs-lookup"><span data-stu-id="1857f-190">For Oracle Linux 6 virtual machines:</span></span>

```sh
[ol6_addons]
name=Add-Ons for Oracle Linux $releasever ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL6/addons/x86_64
gpgkey=http://public-yum.oracle.com/RPM-GPG-KEY-oracle-ol6
gpgcheck=1
enabled=1
```

<span data-ttu-id="1857f-191">Para las máquinas virtuales Oracle Linux 7:</span><span class="sxs-lookup"><span data-stu-id="1857f-191">For Oracle Linux 7 virtual machines:</span></span>

```sh
[ol7_addons]
name=Oracle Linux $releasever Add ons ($basearch)
baseurl=http://public-yum.oracle.com/repo/OracleLinux/OL7/addons/$basearch/
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-oracle
gpgcheck=1
enabled=0
```

<span data-ttu-id="1857f-192">A continuación, escriba:</span><span class="sxs-lookup"><span data-stu-id="1857f-192">Then type:</span></span>

```bash
sudo yum update WALinuxAgent
```

<span data-ttu-id="1857f-193">Normalmente esto es todo lo que necesita, pero si por algún motivo que necesita tooinstall desde https://github.com directamente, Hola uso siguiendo los pasos.</span><span class="sxs-lookup"><span data-stu-id="1857f-193">Typically this is all you need, but if for some reason you need tooinstall it from https://github.com directly, use hello following steps.</span></span>


## <a name="update-hello-linux-agent-when-no-agent-package-exists-for-distribution"></a><span data-ttu-id="1857f-194">Actualizar agente Linux de hello cuando no existe ningún paquete de agente de distribución</span><span class="sxs-lookup"><span data-stu-id="1857f-194">Update hello Linux Agent when no agent package exists for distribution</span></span>

<span data-ttu-id="1857f-195">Instalar wget (no hay algunos distribuciones que no se instalan de forma predeterminada, como las versiones 6.4 y 6.5 Redhat, CentOS y Oracle Linux) escribiendo `sudo yum install wget` en línea de comandos de Hola.</span><span class="sxs-lookup"><span data-stu-id="1857f-195">Install wget (there are some distros that don't install it by default, such as Redhat, CentOS, and Oracle Linux versions 6.4 and 6.5) by typing `sudo yum install wget` on hello command line.</span></span>

### <a name="1-download-hello-latest-version"></a><span data-ttu-id="1857f-196">1. Descargar la versión más reciente de Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-196">1. Download hello latest version</span></span>
<span data-ttu-id="1857f-197">Abra [Hola versión del agente de Linux de Azure en GitHub](https://github.com/Azure/WALinuxAgent/releases) en una página web y obtenga más información sobre número de versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="1857f-197">Open [hello release of Azure Linux Agent in GitHub](https://github.com/Azure/WALinuxAgent/releases) in a web page, and find out hello latest version number.</span></span> <span data-ttu-id="1857f-198">(Puede buscar la versión actual escribiendo `waagent --version`).</span><span class="sxs-lookup"><span data-stu-id="1857f-198">(You can locate your current version by typing `waagent --version`.)</span></span>

#### <a name="for-version-22x-or-later-type"></a><span data-ttu-id="1857f-199">Para la versión 2.2.x o posteriores, escriba:</span><span class="sxs-lookup"><span data-stu-id="1857f-199">For version 2.2.x or later, type:</span></span>
```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.x.zip
unzip v2.2.x.zip.zip
cd WALinuxAgent-2.2.x
```

<span data-ttu-id="1857f-200">Hello línea siguiente usa versión 2.2.0 como ejemplo:</span><span class="sxs-lookup"><span data-stu-id="1857f-200">hello following line uses version 2.2.0 as an example:</span></span>

```bash
wget https://github.com/Azure/WALinuxAgent/archive/v2.2.14.zip
unzip v2.2.14.zip  
cd WALinuxAgent-2.2.14
```

### <a name="2-install-hello-azure-linux-agent"></a><span data-ttu-id="1857f-201">2. Instalar Hola agente Linux de Azure</span><span class="sxs-lookup"><span data-stu-id="1857f-201">2. Install hello Azure Linux Agent</span></span>

#### <a name="for-version-22x-use"></a><span data-ttu-id="1857f-202">Para la versión 2.2.x, use:</span><span class="sxs-lookup"><span data-stu-id="1857f-202">For version 2.2.x, use:</span></span>
<span data-ttu-id="1857f-203">Puede que necesite paquete de hello tooinstall `setuptools` en primer lugar, consulte [aquí](https://pypi.python.org/pypi/setuptools).</span><span class="sxs-lookup"><span data-stu-id="1857f-203">You may need tooinstall hello package `setuptools` first--see [here](https://pypi.python.org/pypi/setuptools).</span></span> <span data-ttu-id="1857f-204">A continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="1857f-204">Then run:</span></span>

```bash
sudo python setup.py install
```

#### <a name="ensure-auto-update-is-enabled"></a><span data-ttu-id="1857f-205">Comprobación de que la actualización automática está habilitada</span><span class="sxs-lookup"><span data-stu-id="1857f-205">Ensure auto update is enabled</span></span>

<span data-ttu-id="1857f-206">En primer lugar, compruebe toosee si está habilitado:</span><span class="sxs-lookup"><span data-stu-id="1857f-206">First, check toosee if it is enabled:</span></span>

```bash
cat /etc/waagent.conf
```

<span data-ttu-id="1857f-207">Busque "AutoUpdate.Enabled".</span><span class="sxs-lookup"><span data-stu-id="1857f-207">Find 'AutoUpdate.Enabled'.</span></span> <span data-ttu-id="1857f-208">Si ve esta salida, significa que la característica está habilitada:</span><span class="sxs-lookup"><span data-stu-id="1857f-208">If you see this output, it is enabled:</span></span>

```bash
# AutoUpdate.Enabled=y
AutoUpdate.Enabled=y
```

<span data-ttu-id="1857f-209">tooenable ejecutar:</span><span class="sxs-lookup"><span data-stu-id="1857f-209">tooenable run:</span></span>

```bash
sudo sed -i 's/AutoUpdate.Enabled=n/AutoUpdate.Enabled=y/g' /etc/waagent.conf
```

### <a name="3-restart-hello-waagent-service"></a><span data-ttu-id="1857f-210">3. Reinicie el servicio de hello waagent</span><span class="sxs-lookup"><span data-stu-id="1857f-210">3. Restart hello waagent service</span></span>
<span data-ttu-id="1857f-211">Para la mayoría de las distribuciones de Linux:</span><span class="sxs-lookup"><span data-stu-id="1857f-211">For most of Linux distros:</span></span>

```bash
sudo service waagent restart
```

<span data-ttu-id="1857f-212">Para Ubuntu, use:</span><span class="sxs-lookup"><span data-stu-id="1857f-212">For Ubuntu, use:</span></span>

```bash
sudo service walinuxagent restart
```

<span data-ttu-id="1857f-213">Para CoreOS, use:</span><span class="sxs-lookup"><span data-stu-id="1857f-213">For CoreOS, use:</span></span>

```bash
sudo systemctl restart waagent
```

### <a name="4-confirm-hello-azure-linux-agent-version"></a><span data-ttu-id="1857f-214">4. Confirme la versión del agente de Linux de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="1857f-214">4. Confirm hello Azure Linux Agent version</span></span>
    
```bash
waagent -version
```

<span data-ttu-id="1857f-215">CoreOS, Hola por encima del comando puede no funcione.</span><span class="sxs-lookup"><span data-stu-id="1857f-215">For CoreOS, hello above command may not work.</span></span>

<span data-ttu-id="1857f-216">Verá que Hola agente Linux de Azure versión ha sido actualizado a la versión nueva de toohello.</span><span class="sxs-lookup"><span data-stu-id="1857f-216">You will see that hello Azure Linux Agent version has been updated toohello new version.</span></span>

<span data-ttu-id="1857f-217">Para obtener más información sobre Hola agente Linux de Azure, consulte [archivo Léame de agente de Linux de Azure](https://github.com/Azure/WALinuxAgent).</span><span class="sxs-lookup"><span data-stu-id="1857f-217">For more information regarding hello Azure Linux Agent, see [Azure Linux Agent README](https://github.com/Azure/WALinuxAgent).</span></span>
