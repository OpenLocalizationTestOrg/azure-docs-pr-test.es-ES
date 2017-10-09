---
title: "aaaRed infraestructura de actualización de Hat (RHUI) | Documentos de Microsoft"
description: "Obtenga información acerca de Red Hat Update Infrastructure (RHUI) para instancias de Red Hat Enterprise Linux a petición de Microsoft Azure"
services: virtual-machines-linux
documentationcenter: 
author: BorisB2015
manager: timlt
editor: 
ms.assetid: f495f1b4-ae24-46b9-8d26-c617ce3daf3a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/13/2017
ms.author: borisb
ms.openlocfilehash: cc244857104b25e4e61862c518db77e915e137ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="red-hat-update-infrastructure-rhui-for-on-demand-red-hat-enterprise-linux-vms-in-azure"></a><span data-ttu-id="dbdcd-103">Red Hat Update Infrastructure (RHUI) para máquinas virtuales Red Hat Enterprise Linux a petición en Azure</span><span class="sxs-lookup"><span data-stu-id="dbdcd-103">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>
<span data-ttu-id="dbdcd-104">Máquinas virtuales creadas a partir de Hola a petición Red Hat Enterprise Linux (RHEL) imágenes disponible en Azure Marketplace son tooaccess registrados Hola implementado en Azure la infraestructura de actualización de Hat de rojo (RHUI).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-104">Virtual machines created from hello on-demand Red Hat Enterprise Linux (RHEL) images available in Azure Marketplace are registered tooaccess hello Red Hat Update Infrastructure (RHUI) deployed in Azure.</span></span>  <span data-ttu-id="dbdcd-105">instancias RHEL de petición de Hola tienen repositorio de acceso tooa yum regionales y tooreceive capaz de las actualizaciones incrementales.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-105">hello on-demand RHEL instances have access tooa regional yum repository and able tooreceive incremental updates.</span></span>

<span data-ttu-id="dbdcd-106">lista de repositorios de yum Hello, que es administrado por RHUI, se configura en la instancia RHEL durante el aprovisionamiento.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-106">hello yum repository list, which is managed by RHUI, is configured in your RHEL instance during provisioning.</span></span> <span data-ttu-id="dbdcd-107">No necesita ninguna configuración adicional - ejecutar toodo `yum update` después de la instancia RHEL actualizaciones más recientes de hello tooget listo.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-107">You don't need toodo any additional configuration - run `yum update` after your RHEL instance is ready tooget hello latest updates.</span></span>

> [!NOTE]
> <span data-ttu-id="dbdcd-108">En septiembre de 2016 implementamos un RHUI de Azure actualizada y en enero de 2017 comenzamos apagado por fases de hello RHUI anteriores de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-108">In September 2016 we deployed an updated Azure RHUI and in January 2017 we started phased shutdown of hello older Azure RHUI.</span></span> <span data-ttu-id="dbdcd-109">Si ha estado utilizando imágenes RHEL hello (o sus instantáneas) de septiembre de 2016 o posterior - probablemente se requiere ninguna acción.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-109">If you have been using hello RHEL images (or their snapshots) from September 2016 or later - likely no action is required.</span></span> <span data-ttu-id="dbdcd-110">Si, sin embargo, tiene las instantáneas anteriores/VMs, su configuración necesita toobe que se actualizó con un acceso ininterrumpido toohello RHUI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-110">If, however, you have older snapshots/VMs, their configuration needs toobe updated for uninterrupted access toohello Azure RHUI.</span></span>
> 

## <a name="rhui-azure-infrastructure-update"></a><span data-ttu-id="dbdcd-111">Actualización de la infraestructura RHUI en Azure</span><span class="sxs-lookup"><span data-stu-id="dbdcd-111">RHUI Azure Infrastructure Update</span></span>
<span data-ttu-id="dbdcd-112">A partir de septiembre de 2016, Azure tiene un nuevo conjunto de servidores de Red Hat Update Infrastructure (RHUI).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-112">As of September 2016, Azure has a new set of Red Hat Update Infrastructure (RHUI) servers.</span></span> <span data-ttu-id="dbdcd-113">Estos servidores se implementan con [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) para que cualquier máquina virtual, independientemente de la región, pueda usar un único punto de conexión (rhui-1.micrsoft.com).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-113">These servers are deployed with [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) so that a single endpoint (rhui-1.microsoft.com) can be used by any VM regardless of region.</span></span> <span data-ttu-id="dbdcd-114">Hola nuevas imágenes de pago por uso de RHEL (PAYG) en servidores nuevos de Azure RHUI de hello Azure Marketplace (versiones con fecha de septiembre de 2016 o posteriores) toohello de punto y no requieren ninguna acción adicional.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-114">hello new RHEL Pay-As-You-Go (PAYG) images in hello Azure Marketplace (versions dated September 2016 or later) point toohello new Azure RHUI servers and do not require any additional action.</span></span>

### <a name="determine-if-action-is-required"></a><span data-ttu-id="dbdcd-115">Determinar si se requiere alguna acción</span><span class="sxs-lookup"><span data-stu-id="dbdcd-115">Determine if action is required</span></span>
<span data-ttu-id="dbdcd-116">Si experimenta problemas de conexión tooAzure RHUI de la máquina virtual de Azure RHEL PAYG, siga estos pasos</span><span class="sxs-lookup"><span data-stu-id="dbdcd-116">If you are experiencing problems connecting tooAzure RHUI from your Azure RHEL PAYG VM, follow these steps</span></span>
1. <span data-ttu-id="dbdcd-117">Inspeccione la configuración de máquina virtual del punto de conexión de RHUI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-117">Inspect VM configuration for Azure RHUI endpoint</span></span>

    <span data-ttu-id="dbdcd-118">Compruebe si `/etc/yum.repos.d/rh-cloud.repo` archivo también contiene referencia`rhui-[1-3].microsoft.com` en URL base del `[rhui-microsoft-azure-rhel*]` sección del archivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-118">Check if `/etc/yum.repos.d/rh-cloud.repo` file contains reference too`rhui-[1-3].microsoft.com` in baseurl of `[rhui-microsoft-azure-rhel*]` section of hello file.</span></span> <span data-ttu-id="dbdcd-119">Si es - utilizas Hola nueva RHUI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-119">If it is - you are using hello new Azure RHUI.</span></span>

    <span data-ttu-id="dbdcd-120">Si lo que señala tooa ubicación con hello sigue el patrón `mirrorlist.*cds[1-4].cloudapp.net` -actualización de la configuración de hello es necesaria.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-120">If it pointing tooa location with hello following pattern `mirrorlist.*cds[1-4].cloudapp.net` - hello configuration update is required.</span></span>

    <span data-ttu-id="dbdcd-121">Si está usando la nueva configuración de Hola y sigue sin poder conectarse tooAzure RHUI - archivo de un caso de soporte técnico con Microsoft o con Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-121">If you are using hello new configuration and still cannot connect tooAzure RHUI - file a support case with Microsoft or Red Hat.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dbdcd-122">Acceso hospedado tooAzure RHUI es toohello limita las máquinas virtuales de [intervalos de direcciones IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-122">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
    > 

2. <span data-ttu-id="dbdcd-123">Si hello RHUI de Azure anterior sigue estando disponible cuando realice esta comprobación y le gustaría tooautomatically actualizar la configuración de hello, ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-123">If hello old Azure RHUI is still available when you do this check and you would like tooautomatically update hello configuration, execute hello following command:</span></span>

    <span data-ttu-id="dbdcd-124">`sudo yum update RHEL6`o `sudo yum update RHEL7` según la versión de la familia de hello RHEL.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-124">`sudo yum update RHEL6` or `sudo yum update RHEL7` depending on hello RHEL family version.</span></span>

3. <span data-ttu-id="dbdcd-125">Si ya no se puede conectar toohello antiguo RHUI de Azure, siga Hola manual los pasos descritos en la sección siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-125">If you can no longer connect toohello old Azure RHUI, follow hello manual steps described in hello next section.</span></span>

4. <span data-ttu-id="dbdcd-126">Asegúrese de que configuración de hello tooupdate en origen de Hola o instantánea de imagen afectados VM se haya proporcionado de.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-126">Make sure tooupdate hello configuration on hello source image/snapshot affected VM was provisioned from.</span></span>

### <a name="phased-shutdown-of-hello-old-azure-rhui"></a><span data-ttu-id="dbdcd-127">Cierre por fases de Hola antiguo RHUI de Azure</span><span class="sxs-lookup"><span data-stu-id="dbdcd-127">Phased shutdown of hello old Azure RHUI</span></span>
<span data-ttu-id="dbdcd-128">Durante el cierre de Hola de hello antiguo RHUI de Azure, restringimos acceder a tooit como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-128">During hello shutdown of hello old Azure RHUI we restrict access tooit as follows:</span></span>

1. <span data-ttu-id="dbdcd-129">Restringir aún más el tooset de acceso (ACL) de direcciones IP que ya se está conectando tooit.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-129">Further restrict access (ACL) tooset of IP addresses that are already connecting tooit.</span></span> <span data-ttu-id="dbdcd-130">Posibles efectos secundarios: Si continúa utilizando Hola antiguo RHUI de Azure: las máquinas virtuales nuevas pueden no ser capaz de tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-130">Possible side-effects: if you continue using hello old Azure RHUI - your new VMs may not be able tooconnect tooit.</span></span> <span data-ttu-id="dbdcd-131">Máquinas virtuales de RHEL con direcciones IP dinámica que vaya a través de la secuencia de apagado/desasignar/inicio puede recibir IP nueva y, por tanto, también podría empiezan a generar errores tooconnect toohello RHUI de Azure anterior</span><span class="sxs-lookup"><span data-stu-id="dbdcd-131">RHEL VMs with dynamic IPs that go through shutdown/deallocate/start sequence may receive new IP and hence also could start failing tooconnect toohello old Azure RHUI</span></span>

2. <span data-ttu-id="dbdcd-132">Apagado de los servidores de entrega de contenido reflejados.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-132">Shutdown of mirror content delivery servers.</span></span> <span data-ttu-id="dbdcd-133">Posibles efectos secundarios: desconectamos CDSes más puede que vea ya `yum update` tiempo de mantenimiento, seleccione más los tiempos de espera hasta hello cuando ya no se puede conectar toohello antiguo RHUI de Azure.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-133">Possible side-effects: as we shut down more CDSes you may see longer `yum update` servicing time, more timeouts up until hello point when you can no longer connect toohello old Azure RHUI.</span></span>

### <a name="hello-ips-for-hello-new-rhui-content-delivery-servers-are"></a><span data-ttu-id="dbdcd-134">Hola direcciones IP para servidores de entrega de contenido de hello nuevos RHUI son</span><span class="sxs-lookup"><span data-stu-id="dbdcd-134">hello IPs for hello new RHUI content delivery servers are</span></span>
<span data-ttu-id="dbdcd-135">Si usas toofurther de configuración de red restringen el acceso de las máquinas virtuales de RHEL PAYG, asegúrese de que Hola después de direcciones IP se permite para `yum update` toowork según se encuentra en el entorno de Hola.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-135">If you are using network configuration toofurther restrict access from RHEL PAYG VMs, make sure hello following IPs are allowed for `yum update` toowork depending on hello environment you are in.</span></span> 

```
# Azure Global
13.91.47.76
40.85.190.91
52.187.75.218
52.174.163.213

# Azure US Government
13.72.186.193

# Azure Germany
51.5.243.77
51.4.228.145
```

### <a name="manual-update-procedure-toouse-hello-new-azure-rhui-servers"></a><span data-ttu-id="dbdcd-136">Actualización manual procedimiento toouse Hola nuevos Azure RHUI servidores</span><span class="sxs-lookup"><span data-stu-id="dbdcd-136">Manual update procedure toouse hello new Azure RHUI servers</span></span>
<span data-ttu-id="dbdcd-137">Firma de clave pública de descarga (a través de curl) Hola</span><span class="sxs-lookup"><span data-stu-id="dbdcd-137">Download (via curl) hello public key signature</span></span>

```bash
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 
```

<span data-ttu-id="dbdcd-138">Comprobar clave Hola descargado</span><span class="sxs-lookup"><span data-stu-id="dbdcd-138">Verify hello downloaded key</span></span>

```bash
gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="dbdcd-139">Comprobar la salida de hello, comprobar `keyid` y `user ID packet`:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-139">Check hello output, verify `keyid` and `user ID packet`:</span></span>

```bash
Version: GnuPG v1.4.7 (GNU/Linux)
:public key packet:
        version 4, algo 1, created 1446074508, expires 0
        pkey[0]: [2048 bits]
        pkey[1]: [17 bits]
        keyid: EB3E94ADBE1229CF
:user ID packet: "Microsoft (Release signing) <gpgsecurity@microsoft.com>"
:signature packet: algo 1, keyid EB3E94ADBE1229CF
        version 4, created 1446074508, md5len 0, sigclass 0x13
        digest algo 2, begin of digest 1a 9b
        hashed subpkt 2 len 4 (sig created 2015-10-28)
        hashed subpkt 27 len 1 (key flags: 03)
        hashed subpkt 11 len 5 (pref-sym-algos: 9 8 7 3 2)
        hashed subpkt 21 len 3 (pref-hash-algos: 2 8 3)
        hashed subpkt 22 len 2 (pref-zip-algos: 2 1)
        hashed subpkt 30 len 1 (features: 01)
        hashed subpkt 23 len 1 (key server preferences: 80)
        subpkt 16 len 8 (issuer key ID EB3E94ADBE1229CF)
        data: [2047 bits]
```

<span data-ttu-id="dbdcd-140">Instalar la clave pública de Hola</span><span class="sxs-lookup"><span data-stu-id="dbdcd-140">Install hello public key</span></span>

```bash
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release
```

<span data-ttu-id="dbdcd-141">Descargue, compruebe e instale el cliente RPM.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-141">Download, Verify, and Install Client RPM</span></span>

<span data-ttu-id="dbdcd-142">Descargue lo siguiente para RHEL 6:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-142">Download: For RHEL 6</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel6/rhui-azure-rhel6-2.0-2.noarch.rpm 
```

<span data-ttu-id="dbdcd-143">Para RHEL 7:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-143">For RHEL 7</span></span>

```bash
curl -o azureclient.rpm https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel7/rhui-azure-rhel7-2.0-2.noarch.rpm  
```

<span data-ttu-id="dbdcd-144">Compruebe:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-144">Verify:</span></span>

```bash
rpm -Kv azureclient.rpm
```

<span data-ttu-id="dbdcd-145">Compruebe en la salida esa firma de hello paquete es correcto</span><span class="sxs-lookup"><span data-stu-id="dbdcd-145">Check in output that signature of hello package is OK</span></span>

```bash
azureclient.rpm:
    Header V3 RSA/SHA256 Signature, key ID be1229cf: OK
    Header SHA1 digest: OK (927a3b548146c95a3f6c1a5d5ae52258a8859ab3)
    V3 RSA/SHA256 Signature, key ID be1229cf: OK
    MD5 digest: OK (c04ff605f82f4be8c96020bf5c23b86c)
```

<span data-ttu-id="dbdcd-146">Instalar Hola RPM</span><span class="sxs-lookup"><span data-stu-id="dbdcd-146">Install hello RPM</span></span>

```bash
sudo rpm -U azureclient.rpm
```

<span data-ttu-id="dbdcd-147">Tras la finalización, compruebe que puede tener acceso a Hola de formulario RHUI de Azure VM</span><span class="sxs-lookup"><span data-stu-id="dbdcd-147">Upon completion, verify that you can access Azure RHUI form hello VM</span></span>

### <a name="all-in-one-script-for-automating-hello-preceding-task"></a><span data-ttu-id="dbdcd-148">All-in-one script para automatizar Hola delante de la tarea</span><span class="sxs-lookup"><span data-stu-id="dbdcd-148">All-in-one script for automating hello preceding task</span></span>
<span data-ttu-id="dbdcd-149">Usar hello siguiente secuencia de comandos como tarea de hello tooautomate necesarios sobre la actualización de las máquinas virtuales toohello nuevo Azure RHUI los servidores afectados.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-149">Use hello following script as needed tooautomate hello task of updating affected VMs toohello new Azure RHUI servers.</span></span>

```sh
# Download key
curl -o RPM-GPG-KEY-microsoft-azure-release https://download.microsoft.com/download/9/D/9/9d945f05-541d-494f-9977-289b3ce8e774/microsoft-sign-public.asc 

# Validate key
if ! gpg --list-packets --verbose < RPM-GPG-KEY-microsoft-azure-release | grep -q "keyid: EB3E94ADBE1229CF"; then
    echo "Keyfile azure.asc NOT valid. Exiting."
    exit 1
fi

# Install Key
sudo install -o root -g root -m 644 RPM-GPG-KEY-microsoft-azure-release /etc/pki/rpm-gpg
sudo rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-microsoft-azure-release

# Download RPM package
if grep -q "release 7" /etc/redhat-release; then
    ver=7
elif  grep -q "release 6" /etc/redhat-release; then
    ver=6
else
    echo "Version not supported, exiting"
    exit 1
fi

url=https://rhui-1.microsoft.com/pulp/repos/microsoft-azure-rhel$ver/rhui-azure-rhel$ver-2.0-2.noarch.rpm
curl -o azureclient.rpm "$url"

# Verify package
if ! rpm -Kv azureclient.rpm | grep -q "key ID be1229cf: OK"; then
    echo "RPM failed validation ($url)"
    exit 1
fi

# Install package
sudo rpm -U azureclient.rpm
```

## <a name="rhui-overview"></a><span data-ttu-id="dbdcd-150">Introducción sobre RHUI</span><span class="sxs-lookup"><span data-stu-id="dbdcd-150">RHUI overview</span></span>
<span data-ttu-id="dbdcd-151">[Infraestructura de Red Hat actualización](https://access.redhat.com/products/red-hat-update-infrastructure) ofrece un contenido del repositorio de soluciones muy escalables toomanage yum para instancias en la nube de Red Hat Enterprise Linux que están hospedadas por proveedores de nube de certificados de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-151">[Red Hat Update Infrastructure](https://access.redhat.com/products/red-hat-update-infrastructure) offers a highly scalable solution toomanage yum repository content for Red Hat Enterprise Linux cloud instances that are hosted by Red Hat-certified cloud providers.</span></span> <span data-ttu-id="dbdcd-152">Basándonos en proyecto de pasta de nivel superior de hello, RHUI permite que los proveedores de nube toolocally reflejado repositorio hospedados en Red Hat contenido de, crear repositorios personalizados con su propio contenido y poner dichos grupo grande de repositorios tooa disponibles de los usuarios finales a través de un equilibrio de carga sistema de entrega de contenido.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-152">Based on hello upstream Pulp project, RHUI allows cloud providers toolocally mirror Red Hat-hosted repository content, create custom repositories with their own content, and make those repositories available tooa large group of end users through a load-balanced content delivery system.</span></span>

## <a name="regions-where-rhui-is-available"></a><span data-ttu-id="dbdcd-153">Regiones donde se implementa RHUI</span><span class="sxs-lookup"><span data-stu-id="dbdcd-153">Regions where RHUI is available</span></span>
<span data-ttu-id="dbdcd-154">RHUI está disponible en todas las regiones donde estén disponibles las imágenes a petición RHEL.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-154">RHUI is available in all regions where RHEL on-demand images are available.</span></span> <span data-ttu-id="dbdcd-155">Actualmente incluyen públicas todas las regiones incluidas en hello [panel de estado de Azure](https://azure.microsoft.com/status/) página, las regiones de Azure en Alemania y de gobierno de EE.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-155">It currently includes all public regions listed on hello [Azure status dashboard](https://azure.microsoft.com/status/) page, Azure US Government and Azure Germany regions.</span></span> <span data-ttu-id="dbdcd-156">En el precio se incluye el acceso de RHUI a las máquinas virtuales aprovisionadas desde imágenes RHEL a petición.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-156">RHUI access for VMs provisioned from RHEL on-demand images is included in their price.</span></span> <span data-ttu-id="dbdcd-157">Disponibilidad en la nube regionales o nacionales adicionales se actualizarán mientras se expanda disponibilidad de petición RHEL Hola futuras.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-157">Additional regional/national cloud availability will be updated as we expand RHEL on-demand availability in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="dbdcd-158">Acceso hospedado tooAzure RHUI es toohello limita las máquinas virtuales de [intervalos de direcciones IP de centro de datos de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-158">Access tooAzure-hosted RHUI is limited toohello VMs within [Microsoft Azure Datacenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>
> 
> 

## <a name="get-updates-from-another-update-repository"></a><span data-ttu-id="dbdcd-159">Obtención de actualizaciones de otro repositorio de actualización</span><span class="sxs-lookup"><span data-stu-id="dbdcd-159">Get updates from another update repository</span></span>
<span data-ttu-id="dbdcd-160">Si necesita tooget actualizaciones desde un repositorio de actualización diferentes (en lugar de RHUI hospedado de Azure), primero debe toounregister las instancias de RHUI.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-160">If you need tooget updates from a different update repository (instead of Azure-hosted RHUI), first you need toounregister your instances from RHUI.</span></span> <span data-ttu-id="dbdcd-161">Es necesario el registro toore usarlas con la infraestructura de actualización deseado hello (por ejemplo, Red Hat satélite o Red Hat cliente Portal CDN).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-161">Then you need toore-register them with hello desired update infrastructure (such as Red Hat Satellite or Red Hat Customer Portal CDN).</span></span> <span data-ttu-id="dbdcd-162">Necesitará suscripciones apropiadas a Red Hat para estos servicios y registrarse en [Red Hat Cloud Access en Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-162">You will need appropriate Red Hat subscriptions for these services and registration for [Red Hat Cloud Access in Azure](https://access.redhat.com/ecosystem/partners/ccsp/microsoft-azure).</span></span>

<span data-ttu-id="dbdcd-163">toounregister RHUI y vuelva a registrar tooyour actualización infraestructura siguen estos pasos:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-163">toounregister RHUI and reregister tooyour update infrastructure follow these steps:</span></span>

1. <span data-ttu-id="dbdcd-164">Edite /etc/yum.repos.d/rh-cloud.repo y cambie todos `enabled=1` demasiado`enabled=0`.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-164">Edit /etc/yum.repos.d/rh-cloud.repo and change all `enabled=1` too`enabled=0`.</span></span> <span data-ttu-id="dbdcd-165">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="dbdcd-165">For example:</span></span>
   
   ```bash
   sed -i 's/enabled=1/enabled=0/g' /etc/yum.repos.d/rh-cloud.repo
   ```
   
2. <span data-ttu-id="dbdcd-166">Edite /etc/yum/pluginconf.d/rhnplugin.conf y cambie `enabled=0` demasiado`enabled=1`.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-166">Edit /etc/yum/pluginconf.d/rhnplugin.conf and change `enabled=0` too`enabled=1`.</span></span>
3. <span data-ttu-id="dbdcd-167">A continuación, registrar con la infraestructura de hello deseado, como Portal del cliente de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-167">Then register with hello desired infrastructure, such as Red Hat Customer Portal.</span></span> <span data-ttu-id="dbdcd-168">Siga la Guía de solución de Red Hat [cómo tooregister y suscribirse a un Portal del cliente de Red Hat de sistema toohello](https://access.redhat.com/solutions/253273).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-168">Follow Red Hat solution guide on [how tooregister and subscribe a system toohello Red Hat Customer Portal](https://access.redhat.com/solutions/253273).</span></span>

> [!NOTE]
> <span data-ttu-id="dbdcd-169">Acceso toohello RHUI hospedado de Azure se incluye en el precio de imagen de hello RHEL pago por uso (PAYG).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-169">Access toohello Azure-hosted RHUI is included in hello RHEL Pay-As-You-Go (PAYG) image price.</span></span> <span data-ttu-id="dbdcd-170">Al anular el registro de una VM de RHEL PAYG de hello RHUI hospedado de Azure no convierte máquina virtual de hello en VM de tipo de Bring Your-posee-licencia (BYOL).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-170">Unregistering a PAYG RHEL VM from hello Azure-hosted RHUI does not convert hello virtual machine into Bring-Your-Own-License (BYOL) type VM.</span></span> <span data-ttu-id="dbdcd-171">Si registra Hola misma máquina virtual con otro origen de actualizaciones puede acumulando gastos por el dobles: la primera vez para hello y precio del software de Azure RHEL segunda vez para suscripciones de Red Hat.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-171">If you register hello same VM with another source of updates you may be incurring double charges: first time for Azure RHEL software fee, and hello second time for Red Hat subscription(s).</span></span> 
> 
> <span data-ttu-id="dbdcd-172">Si necesita toouse sistemáticamente una infraestructura de actualizaciones que no sea RHUI hospedado de Azure considere la posibilidad de crear e implementar sus propias imágenes (BYOL-type) como se describe en [crear y cargar Red Hat máquina virtual de Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) artículo.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-172">If you consistently need toouse an update infrastructure other than Azure-hosted RHUI consider creating and deploying your own (BYOL-type) images as described in [Create and Upload Red Hat-based virtual machine for Azure](redhat-create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) article.</span></span>
> 

## <a name="next-steps"></a><span data-ttu-id="dbdcd-173">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dbdcd-173">Next steps</span></span>
<span data-ttu-id="dbdcd-174">toocreate una VM de rojo Hat Enterprise Linux de imagen de pago por uso de Azure Marketplace y aproveche RHUI hospedado de Azure vaya demasiado[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span><span class="sxs-lookup"><span data-stu-id="dbdcd-174">toocreate a Red Hat Enterprise Linux VM from Azure Marketplace Pay-As-You-Go image and leverage Azure-hosted RHUI go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/redhat/).</span></span> <span data-ttu-id="dbdcd-175">Será capaz de toouse `yum update` en la instancia RHEL sin ninguna configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="dbdcd-175">You will be able toouse `yum update` in your RHEL instance without any additional setup.</span></span>

