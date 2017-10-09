---
title: "aaaAzure cifrado del disco para Windows y las máquinas virtuales de Linux IaaS | Documentos de Microsoft"
description: "En este artículo se ofrece información general de Microsoft Azure Disk Encryption para máquinas virtuales IaaS con Windows y Linux."
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: d3fac8bb-4829-405e-8701-fa7229fb1725
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: kakhan
ms.openlocfilehash: b685abdcc908e66d2352ec5ac2d9996aa75af1b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-for-windows-and-linux-iaas-vms"></a><span data-ttu-id="e14fe-103">Cifrado de disco de Azure para máquinas virtuales IaaS Linux y Windows</span><span class="sxs-lookup"><span data-stu-id="e14fe-103">Azure Disk Encryption for Windows and Linux IaaS VMs</span></span>
<span data-ttu-id="e14fe-104">Microsoft Azure es tooensuring firme compromiso de la privacidad de los datos, soberanía de datos y le permite toocontrol hospedado de Azure datos a través de una gama de tecnologías avanzadas tooencrypt, controlar y administrar claves de cifrado, auditoría y control de acceso de datos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-104">Microsoft Azure is strongly committed tooensuring your data privacy, data sovereignty and enables you toocontrol your Azure hosted data through a range of advanced technologies tooencrypt, control and manage encryption keys, control & audit access of data.</span></span> <span data-ttu-id="e14fe-105">Esto proporciona a los clientes de Azure solución Hola de toochoose de flexibilidad de Hola que mejor se adapte a sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-105">This provides Azure customers hello flexibility toochoose hello solution that best meets their business needs.</span></span> <span data-ttu-id="e14fe-106">En este documento, le presentaremos tooa nueva solución tecnológica "Cifrado de disco de Azure para Windows y de Linux IaaS VM" toohelp proteger y proteger los datos toomeet los compromisos de seguridad y cumplimiento organizativos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-106">In this paper, we will introduce you tooa new technology solution “Azure Disk Encryption for Windows and Linux IaaS VM’s” toohelp protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="e14fe-107">papel de Hello proporciona instrucciones detalladas sobre la compatibilidad de características de cifrado de disco de Azure toouse Hola incluidos Hola escenarios y las experiencias de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-107">hello paper provides detailed guidance on how toouse hello Azure disk encryption features including hello supported scenarios and hello user experiences.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-108">Algunas de las recomendaciones pueden provocar un aumento del uso de datos, de la red o de recursos de proceso, lo que incrementará los costes de las licencias o suscripciones.</span><span class="sxs-lookup"><span data-stu-id="e14fe-108">Certain recommendations might increase data, network, or compute resource usage, resulting in additional license or subscription costs.</span></span>

## <a name="overview"></a><span data-ttu-id="e14fe-109">Información general</span><span class="sxs-lookup"><span data-stu-id="e14fe-109">Overview</span></span>
<span data-ttu-id="e14fe-110">Azure Disk Encryption es una nueva funcionalidad que permite cifrar los discos de las máquinas virtuales IaaS con Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-110">Azure Disk Encryption is a new capability that helps you encrypt your Windows and Linux IaaS virtual machine disks.</span></span> <span data-ttu-id="e14fe-111">Cifrado del disco Azure aprovecha estándar del sector hello [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) característica de Windows y hello [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) característica de cifrado de volumen de Linux tooprovide para discos de datos de Hola y Hola SO.</span><span class="sxs-lookup"><span data-stu-id="e14fe-111">Azure Disk Encryption leverages hello industry standard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) feature of Windows and hello [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) feature of Linux tooprovide volume encryption for hello OS and hello data disks.</span></span> <span data-ttu-id="e14fe-112">solución de Hola se integra con [el almacén de claves de Azure](https://azure.microsoft.com/documentation/services/key-vault/) toohelp controlar y administrar claves de cifrado del disco de Hola y secretos en su suscripción de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-112">hello solution is integrated with [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp you control and manage hello disk-encryption keys and secrets in your key vault subscription.</span></span> <span data-ttu-id="e14fe-113">solución de Hello también garantiza que todos los datos en discos de máquina virtual de Hola se cifran en reposo en el almacenamiento de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-113">hello solution also ensures that all data on hello virtual machine disks are encrypted at rest in your Azure storage.</span></span>

<span data-ttu-id="e14fe-114">Azure Disk Encryption para máquinas virtuales IaaS de Windows y Linux ahora tiene **disponibilidad general** en todas las regiones públicas de Azure y regiones de AzureGov para VM estándares y VM con Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e14fe-114">Azure disk encryption for Windows and Linux IaaS VMs is now in **General Availability** in all Azure public regions and AzureGov regions for Standard  VMs and VMs with premium storage.</span></span>

### <a name="encryption-scenarios"></a><span data-ttu-id="e14fe-115">Escenarios de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-115">Encryption scenarios</span></span>
<span data-ttu-id="e14fe-116">Hola soluciones de cifrado del disco de Azure admite Hola cliente los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-116">hello Azure Disk Encryption solution supports hello following customer scenarios:</span></span>

* <span data-ttu-id="e14fe-117">Habilitación del cifrado en las nuevas máquinas virtuales IaaS creadas a partir de un VHD precifrado y las claves de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-117">Enable encryption on new IaaS VMs created from pre-encrypted VHD and encryption keys</span></span>
* <span data-ttu-id="e14fe-118">Habilitar el cifrado en nuevas máquinas virtuales de IaaS creado a partir de imágenes de la Galería de Azure de hello compatibles</span><span class="sxs-lookup"><span data-stu-id="e14fe-118">Enable encryption on new IaaS VMs created from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="e14fe-119">Habilitación del cifrado en las máquinas virtuales IaaS existentes que se ejecutan en Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-119">Enable encryption on existing IaaS VMs running in Azure</span></span>
* <span data-ttu-id="e14fe-120">Deshabilitación del cifrado en máquinas virtuales IaaS de Windows</span><span class="sxs-lookup"><span data-stu-id="e14fe-120">Disable encryption on Windows IaaS VMs</span></span>
* <span data-ttu-id="e14fe-121">Deshabilitación del cifrado en unidades de datos para máquinas virtuales IaaS con Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-121">Disable encryption on data drives for Linux IaaS VMs</span></span>
* <span data-ttu-id="e14fe-122">Habilitación del cifrado en máquinas virtuales de discos administrados</span><span class="sxs-lookup"><span data-stu-id="e14fe-122">Enable encryption of managed disk VMs</span></span>
* <span data-ttu-id="e14fe-123">Actualización de la configuración del cifrado de una máquina virtual cifrada de un tipo de almacenamiento que no sea Premium Storage existente</span><span class="sxs-lookup"><span data-stu-id="e14fe-123">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="e14fe-124">Restauración y copia de seguridad de VM cifradas, cifradas con clave de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-124">Backup and restore of encrypted VMs, encrypted with key encryption key</span></span>

<span data-ttu-id="e14fe-125">solución de Hello admite Hola los escenarios siguientes para las máquinas virtuales IaaS cuando están habilitadas en Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="e14fe-125">hello solution supports hello following scenarios for IaaS VMs when they are enabled in Microsoft Azure:</span></span>

* <span data-ttu-id="e14fe-126">Integración con el Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-126">Integration with Azure Key Vault</span></span>
* <span data-ttu-id="e14fe-127">Máquinas virtuales de nivel estándar: [máquinas virtuales IaaS de las series A, D, DS, G, GS, F, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)</span><span class="sxs-lookup"><span data-stu-id="e14fe-127">Standard tier VMs: [A, D, DS, G, GS, F, and so forth series IaaS VMs](https://azure.microsoft.com/pricing/details/virtual-machines/)</span></span>
* <span data-ttu-id="e14fe-128">Habilitar el cifrado en Windows y las máquinas virtuales de IaaS de Linux y las máquinas virtuales de disco administrado de hello admite imágenes de la Galería de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-128">Enable encryption on Windows and Linux IaaS VMs and managed disk VMs from hello supported Azure Gallery images</span></span>
* <span data-ttu-id="e14fe-129">Deshabilitación del cifrado en sistemas operativos y unidades de datos para máquinas virtuales IaaS de Windows y máquinas virtuales de discos administrados</span><span class="sxs-lookup"><span data-stu-id="e14fe-129">Disable encryption on OS and data drives for Windows IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="e14fe-130">Deshabilitación del cifrado en unidades de datos para máquinas virtuales IaaS de Linux y máquinas virtuales de discos administrados</span><span class="sxs-lookup"><span data-stu-id="e14fe-130">Disable encryption on data drives for Linux IaaS VMs and managed disk VMs</span></span>
* <span data-ttu-id="e14fe-131">Habilitación del cifrado en máquinas virtuales IaaS que ejecutan el sistema operativo cliente de Windows</span><span class="sxs-lookup"><span data-stu-id="e14fe-131">Enable encryption on IaaS VMs running Windows Client OS</span></span>
* <span data-ttu-id="e14fe-132">Habilitación del cifrado en volúmenes con rutas de montaje</span><span class="sxs-lookup"><span data-stu-id="e14fe-132">Enable encryption on volumes with mount paths</span></span>
* <span data-ttu-id="e14fe-133">Habilitación del cifrado en máquinas virtuales de Linux configurado con seccionamiento de disco (RAID) mediante el uso de mdadm</span><span class="sxs-lookup"><span data-stu-id="e14fe-133">Enable encryption on Linux VMs configured with disk striping (RAID) using mdadm</span></span>
* <span data-ttu-id="e14fe-134">Habilitación del cifrado en máquinas virtuales de Linux mediante el uso de LVM para discos de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-134">Enable encryption on Linux VMs using LVM for data disks</span></span>
* <span data-ttu-id="e14fe-135">Habilitación del cifrado en máquinas virtuales Windows configurado con espacios de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e14fe-135">Enable encryption on Windows VMs configured with Storage Spaces</span></span>
* <span data-ttu-id="e14fe-136">Actualización de la configuración del cifrado de una máquina virtual cifrada de un tipo de almacenamiento que no sea Premium Storage existente</span><span class="sxs-lookup"><span data-stu-id="e14fe-136">Update encryption settings of an existing encrypted non-premium storage VM</span></span>
* <span data-ttu-id="e14fe-137">Se admiten todas las regiones públicas de Azure y las regiones de AzureGov</span><span class="sxs-lookup"><span data-stu-id="e14fe-137">All Azure Public and AzureGov regions are supported</span></span>

<span data-ttu-id="e14fe-138">solución de Hello no admite Hola siguientes escenarios, características y tecnologías:</span><span class="sxs-lookup"><span data-stu-id="e14fe-138">hello solution does not support hello following scenarios, features, and technology:</span></span>

* <span data-ttu-id="e14fe-139">Máquinas virtuales IaaS de nivel básico</span><span class="sxs-lookup"><span data-stu-id="e14fe-139">Basic tier IaaS VMs</span></span>
* <span data-ttu-id="e14fe-140">Deshabilitación del cifrado en una unidad del sistema operativo para máquinas virtuales IaaS Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-140">Disabling encryption on an OS drive for Linux IaaS VMs</span></span>
* <span data-ttu-id="e14fe-141">Deshabilitar el cifrado en una unidad de datos si se cifra Hola unidad del SO para máquinas virtuales de Iaas de Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-141">Disabling encryption on a data drive if hello OS drive is encrypted for Linux Iaas VMs</span></span>
* <span data-ttu-id="e14fe-142">Máquinas virtuales de IaaS que se crean mediante el método de creación de VM clásica de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-142">IaaS VMs that are created by using hello classic VM creation method</span></span>
* <span data-ttu-id="e14fe-143">NO se admite la habilitación del cifrado en imágenes personalizadas de cliente de máquinas virtuales IaaS Windows y Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-143">Enable encryption on Windows and Linux IaaS VMs customer custom images is NOT supported.</span></span> <span data-ttu-id="e14fe-144">En la actualidad no se admite la habilitación del cifrado en el disco del sistema operativo de LVM Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-144">Enable enccryption on Linux LVM OS disk is not supported currently.</span></span> <span data-ttu-id="e14fe-145">Se admitirá pronto.</span><span class="sxs-lookup"><span data-stu-id="e14fe-145">This support will come soon.</span></span>
* <span data-ttu-id="e14fe-146">Integración con el Servicio de administración de claves local</span><span class="sxs-lookup"><span data-stu-id="e14fe-146">Integration with your on-premises Key Management Service</span></span>
* <span data-ttu-id="e14fe-147">Azure Files (sistema de archivos compartido), Network File System (NFS), volúmenes dinámicos y máquinas virtuales Windows configuradas con sistemas RAID basadas en software</span><span class="sxs-lookup"><span data-stu-id="e14fe-147">Azure Files (shared file system), Network File System (NFS), dynamic volumes, and Windows VMs that are configured with software-based RAID systems</span></span>
* <span data-ttu-id="e14fe-148">Restaure y realice una copia de seguridad de máquinas virtuales cifradas sin clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-148">Backup and restore of encrypted VMs, encrypted without key encryption key.</span></span>
* <span data-ttu-id="e14fe-149">Actualice la configuración del cifrado de una máquina virtual cifrada con Premium Storage existente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-149">Update encryption settings of an existing encrypted premium storage VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-150">Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-150">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e14fe-151">No se admite en máquinas virtuales cifradas sin KEK.</span><span class="sxs-lookup"><span data-stu-id="e14fe-151">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e14fe-152">KEK es un parámetro opcional que habilita el cifrado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-152">KEK is an optional parameter that enables VM encryption.</span></span> <span data-ttu-id="e14fe-153">Próximamente se agregará esta compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="e14fe-153">This support is coming soon.</span></span>
> <span data-ttu-id="e14fe-154">No se admite la actualización de la configuración del cifrado de una máquina virtual cifrada con Premium Storage existente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-154">Update encryption settings of an existing encrypted premium storage VM are not supported.</span></span> <span data-ttu-id="e14fe-155">Próximamente se agregará esta compatibilidad.</span><span class="sxs-lookup"><span data-stu-id="e14fe-155">This support is coming soon.</span></span>

### <a name="encryption-features"></a><span data-ttu-id="e14fe-156">Características de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-156">Encryption features</span></span>
<span data-ttu-id="e14fe-157">Al habilitar e implementar el cifrado del disco de Azure para máquinas virtuales de IaaS de Azure, hello siguientes funcionalidades están habilitadas, dependiendo de la configuración de hello proporcionada:</span><span class="sxs-lookup"><span data-stu-id="e14fe-157">When you enable and deploy Azure Disk Encryption for Azure IaaS VMs, hello following capabilities are enabled, depending on hello configuration provided:</span></span>

* <span data-ttu-id="e14fe-158">Cifrado de volumen de arranque de hello SO volumen tooprotect hello en reposo en el sistema de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e14fe-158">Encryption of hello OS volume tooprotect hello boot volume at rest in your storage</span></span>
* <span data-ttu-id="e14fe-159">Cifrado de datos volúmenes tooprotect Hola los volúmenes de datos en reposo en el sistema de almacenamiento</span><span class="sxs-lookup"><span data-stu-id="e14fe-159">Encryption of data volumes tooprotect hello data volumes at rest in your storage</span></span>
* <span data-ttu-id="e14fe-160">Deshabilitar el cifrado de hello sistema operativo y datos de las unidades para las máquinas virtuales de IaaS de Windows</span><span class="sxs-lookup"><span data-stu-id="e14fe-160">Disabling encryption on hello OS and data drives for Windows IaaS VMs</span></span>
* <span data-ttu-id="e14fe-161">Deshabilitar el cifrado de datos de hello las unidades para las máquinas virtuales de IaaS de Linux (sólo si OS unidad es no cifrado)</span><span class="sxs-lookup"><span data-stu-id="e14fe-161">Disabling encryption on hello data drives for Linux IaaS VMs (only if OS drive IS NOT encrypted)</span></span>
* <span data-ttu-id="e14fe-162">Protección de claves de cifrado de Hola y secretos en su suscripción de almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e14fe-162">Safeguarding hello encryption keys and secrets in your key vault subscription</span></span>
* <span data-ttu-id="e14fe-163">Notificar el estado de cifrado de Hola de hello cifra IaaS VM</span><span class="sxs-lookup"><span data-stu-id="e14fe-163">Reporting hello encryption status of hello encrypted IaaS VM</span></span>
* <span data-ttu-id="e14fe-164">Eliminación de opciones de configuración de cifrado del disco de máquina virtual de IaaS de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-164">Removal of disk-encryption configuration settings from hello IaaS virtual machine</span></span>
* <span data-ttu-id="e14fe-165">Copia de seguridad y restauración de máquinas virtuales cifradas mediante el servicio de copia de seguridad de Azure Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-165">Backup and restore of encrypted VMs by using hello Azure Backup service</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-166">Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-166">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e14fe-167">No se admite en máquinas virtuales cifradas sin KEK.</span><span class="sxs-lookup"><span data-stu-id="e14fe-167">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e14fe-168">KEK es un parámetro opcional que habilita el cifrado de máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-168">KEK is an optional parameter that enables VM encryption.</span></span>

<span data-ttu-id="e14fe-169">La solución Azure Disk Encryption para máquinas virtuales IaaS para Windows y Linux incluye lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-169">Azure Disk Encryption for IaaS VMS for Windows and Linux solution includes:</span></span>

* <span data-ttu-id="e14fe-170">extensión de cifrado del disco de Hola para Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-170">hello disk-encryption extension for Windows.</span></span>
* <span data-ttu-id="e14fe-171">extensión de cifrado del disco de Hola para Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-171">hello disk-encryption extension for Linux.</span></span>
* <span data-ttu-id="e14fe-172">cmdlets de PowerShell de Hello cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="e14fe-172">hello disk-encryption PowerShell cmdlets.</span></span>
* <span data-ttu-id="e14fe-173">Hola cmdlets de Azure interfaz de línea de comandos (CLI) de cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="e14fe-173">hello disk-encryption Azure command-line interface (CLI) cmdlets.</span></span>
* <span data-ttu-id="e14fe-174">Hola plantillas del Administrador de recursos de Azure de cifrado del disco.</span><span class="sxs-lookup"><span data-stu-id="e14fe-174">hello disk-encryption Azure Resource Manager templates.</span></span>

<span data-ttu-id="e14fe-175">Hola soluciones de cifrado del disco de Azure es compatible con las máquinas virtuales de IaaS que ejecutan Windows o el sistema operativo Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-175">hello Azure Disk Encryption solution is supported on IaaS VMs that are running Windows or Linux OS.</span></span> <span data-ttu-id="e14fe-176">Para obtener más información sobre los sistemas operativos compatibles de hello, vea Hola "requisitos previos" sección.</span><span class="sxs-lookup"><span data-stu-id="e14fe-176">For more information about hello supported operating systems, see hello "Prerequisites" section.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-177">No hay cargo adicional por el cifrado de discos de máquinas virtuales con Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="e14fe-177">There is no additional charge for encrypting VM disks with Azure Disk Encryption.</span></span>

### <a name="value-proposition"></a><span data-ttu-id="e14fe-178">Propuesta de valor</span><span class="sxs-lookup"><span data-stu-id="e14fe-178">Value proposition</span></span>
<span data-ttu-id="e14fe-179">Cuando aplique una solución de administración de cifrado de disco de Azure hello, puede cumplir Hola siguiendo las necesidades del negocio:</span><span class="sxs-lookup"><span data-stu-id="e14fe-179">When you apply hello Azure Disk Encryption-management solution, you can satisfy hello following business needs:</span></span>

* <span data-ttu-id="e14fe-180">Las máquinas virtuales IaaS se protegen en reposo, porque se pueden usar cifrado estándar del sector tecnología tooaddress seguridad y cumplimiento de normas requisitos organizativos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-180">IaaS VMs are secured at rest, because you can use industry-standard encryption technology tooaddress organizational security and compliance requirements.</span></span>
* <span data-ttu-id="e14fe-181">Las máquinas virtuales IaaS arrancan bajo directivas y claves controladas por el cliente, y puede auditar su uso en su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-181">IaaS VMs boot under customer-controlled keys and policies, and you can audit their usage in your key vault.</span></span>

### <a name="encryption-workflow"></a><span data-ttu-id="e14fe-182">Flujo de trabajo de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-182">Encryption workflow</span></span>
<span data-ttu-id="e14fe-183">cifrado del disco tooenable para Windows y las máquinas virtuales de Linux, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-183">tooenable disk encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="e14fe-184">Elegir un escenario de cifrado entre Hola anteriores escenarios de cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-184">Choose an encryption scenario from among hello preceding encryption scenarios.</span></span>
2. <span data-ttu-id="e14fe-185">Participar en el cifrado de disco tooenabling a través de la plantilla del Administrador de recursos de cifrado de disco de Azure hello, cmdlets de PowerShell o comando de CLI y especificar la configuración de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-185">Opt in tooenabling disk encryption via hello Azure Disk Encryption Resource Manager template, PowerShell cmdlets, or CLI command, and specify hello encryption configuration.</span></span>

   * <span data-ttu-id="e14fe-186">Para escenario VHD de cifrado de cliente hello, cargue cuenta de almacenamiento de tooyour de disco duro virtual de hello cifrado y almacén de claves de tooyour material clave de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-186">For hello customer-encrypted VHD scenario, upload hello encrypted VHD tooyour storage account and hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="e14fe-187">A continuación, proporciona cifrado de tooenable de configuración de cifrado de hello en una nueva VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-187">Then, provide hello encryption configuration tooenable encryption on a new IaaS VM.</span></span>
   * <span data-ttu-id="e14fe-188">Para nuevas máquinas virtuales que se crean a partir de hello Marketplace y las máquinas virtuales existentes que se están ejecutando en Azure, proporcionan cifrado de tooenable de configuración de cifrado de hello en hello IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="e14fe-188">For new VMs that are created from hello Marketplace and existing VMs that are already running in Azure, provide hello encryption configuration tooenable encryption on hello IaaS VM.</span></span>

3. <span data-ttu-id="e14fe-189">Conceder acceso toohello material de clave de cifrado de hello en tooread plataforma Windows Azure (claves de cifrado de BitLocker para los sistemas Windows) y la frase de contraseña de Linux de cifrado en hello IaaS VM tooenable almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-189">Grant access toohello Azure platform tooread hello encryption-key material (BitLocker encryption keys for Windows systems and Passphrase for Linux) from your key vault tooenable encryption on hello IaaS VM.</span></span>

4. <span data-ttu-id="e14fe-190">Proporcionar hello Azure Active Directory (Azure AD) aplicación identidad toowrite Hola cifrado tooyour material clave almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-190">Provide hello Azure Active Directory (Azure AD) application identity toowrite hello encryption key material tooyour key vault.</span></span> <span data-ttu-id="e14fe-191">Si lo hace, habilita el cifrado en hello IaaS VM para escenarios de hello mencionados en el paso 2.</span><span class="sxs-lookup"><span data-stu-id="e14fe-191">Doing so enables encryption on hello IaaS VM for hello scenarios mentioned in step 2.</span></span>

5. <span data-ttu-id="e14fe-192">Azure actualiza el modelo de servicio VM de hello con cifrado y la configuración de almacén de claves de Hola y configura su VM cifrada.</span><span class="sxs-lookup"><span data-stu-id="e14fe-192">Azure updates hello VM service model with encryption and hello key vault configuration, and sets up your encrypted VM.</span></span>

 ![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig1.png)

### <a name="decryption-workflow"></a><span data-ttu-id="e14fe-194">Flujo de trabajo de descifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-194">Decryption workflow</span></span>
<span data-ttu-id="e14fe-195">toodisable cifrado del disco para máquinas virtuales de IaaS, Hola completa siguiendo los pasos de alto nivel:</span><span class="sxs-lookup"><span data-stu-id="e14fe-195">toodisable disk encryption for IaaS VMs, complete hello following high-level steps:</span></span>

1. <span data-ttu-id="e14fe-196">Elija toodisable cifrado (descifrado) en una VM en ejecución IaaS en Azure a través de la plantilla de administrador de recursos de cifrado de disco de Azure de Hola o los cmdlets de PowerShell y especificar la configuración de descifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-196">Choose toodisable encryption (decryption) on a running IaaS VM in Azure via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets, and specify hello decryption configuration.</span></span>

 <span data-ttu-id="e14fe-197">Este paso deshabilita el cifrado de volumen de datos de sistema operativo u Hola Hola o ambos en hello ejecutando la máquina virtual de IaaS de Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-197">This step disables encryption of hello OS or hello data volume or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="e14fe-198">Sin embargo, como se mencionó en la sección anterior de hello, deshabilitar el cifrado de disco de sistema operativo de Linux no se admite.</span><span class="sxs-lookup"><span data-stu-id="e14fe-198">However, as mentioned in hello previous section, disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="e14fe-199">paso de descifrado de Hello solo se permite para las unidades de datos en máquinas virtuales de Linux siempre y cuando no se cifra el disco del sistema operativo Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-199">hello decryption step is allowed only for data drives on Linux VMs as long as hello OS disk is not encrypted.</span></span>
2. <span data-ttu-id="e14fe-200">Las actualizaciones de Azure Hola modelo de servicio VM y Hola IaaS VM se marca descifrada.</span><span class="sxs-lookup"><span data-stu-id="e14fe-200">Azure updates hello VM service model, and hello IaaS VM is marked decrypted.</span></span> <span data-ttu-id="e14fe-201">contenido de Hola de hello VM ya no se cifra en reposo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-201">hello contents of hello VM are no longer encrypted at rest.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-202">operación de cifrado de la deshabilitación de Hello no elimina la clave hello y el almacén de claves de cifrado (claves de cifrado de BitLocker para los sistemas Windows) o la frase de contraseña de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-202">hello disable-encryption operation does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows systems or Passphrase for Linux).</span></span>
 > <span data-ttu-id="e14fe-203">No se admite la deshabilitación del cifrado de disco del sistema operativo para Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-203">Disabling OS disk encryption for Linux is not supported.</span></span> <span data-ttu-id="e14fe-204">paso de descifrado de Hello solo se permite para las unidades de datos en máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-204">hello decryption step is allowed only for data drives on Linux VMs.</span></span>
<span data-ttu-id="e14fe-205">Deshabilitar el cifrado de disco de datos de Linux no se admite si se cifra Hola unidad del SO.</span><span class="sxs-lookup"><span data-stu-id="e14fe-205">Disabling data disk encryption for Linux is not supported if hello OS drive is encrypted.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e14fe-206">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e14fe-206">Prerequisites</span></span>
<span data-ttu-id="e14fe-207">Antes de habilitar el cifrado de disco de Azure en máquinas virtuales de IaaS de Azure para escenarios de hello admite que se trataron en la sección "Introducción" Hola, vea Hola siguiendo los requisitos previos:</span><span class="sxs-lookup"><span data-stu-id="e14fe-207">Before you enable Azure Disk Encryption on Azure IaaS VMs for hello supported scenarios that were discussed in hello "Overview" section, see hello following prerequisites:</span></span>

* <span data-ttu-id="e14fe-208">Debe tener los recursos de toocreate de una suscripción válida de Azure en Azure en regiones de hello compatible.</span><span class="sxs-lookup"><span data-stu-id="e14fe-208">You must have a valid active Azure subscription toocreate resources in Azure in hello supported regions.</span></span>
* <span data-ttu-id="e14fe-209">Cifrado de disco de Azure es compatible con hello siguientes versiones de Windows Server: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2 y Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="e14fe-209">Azure Disk Encryption is supported on hello following Windows Server versions: Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, and Windows Server 2016.</span></span>
* <span data-ttu-id="e14fe-210">Cifrado de disco de Azure es compatible con Hola después de las versiones de cliente de Windows: Windows 10 y el cliente de Windows 8.</span><span class="sxs-lookup"><span data-stu-id="e14fe-210">Azure Disk Encryption is supported on hello following Windows client versions: Windows 8 client and Windows 10 client.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-211">En el caso de Windows Server 2008 R2, debe tener .NET Framework 4.5 instalado para poder habilitar el cifrado en Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-211">For Windows Server 2008 R2, you must have .NET Framework 4.5 installed before you enable encryption in Azure.</span></span> <span data-ttu-id="e14fe-212">Puede instalarlo desde Windows Update mediante la instalación de actualización opcional Hola Microsoft .NET Framework 4.5.2 para sistemas basados en x64 de Windows Server 2008 R2 ([KB2901983](https://support.microsoft.com/kb/2901983)).</span><span class="sxs-lookup"><span data-stu-id="e14fe-212">You can install it from Windows Update by installing hello optional update Microsoft .NET Framework 4.5.2 for Windows Server 2008 R2 x64-based systems ([KB2901983](https://support.microsoft.com/kb/2901983)).</span></span>

* <span data-ttu-id="e14fe-213">Se admite el cifrado de disco de Azure en hello después de la Galería de Azure según las distribuciones de Linux server y las versiones:</span><span class="sxs-lookup"><span data-stu-id="e14fe-213">Azure Disk Encryption is supported on hello following Azure Gallery based Linux server distributions and versions:</span></span>

| <span data-ttu-id="e14fe-214">Distribución de Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-214">Linux Distribution</span></span> | <span data-ttu-id="e14fe-215">Versión</span><span class="sxs-lookup"><span data-stu-id="e14fe-215">Version</span></span> | <span data-ttu-id="e14fe-216">Tipo de volumen compatible con el cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-216">Volume Type Supported for Encryption</span></span>|
| --- | --- |--- |
| <span data-ttu-id="e14fe-217">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e14fe-217">Ubuntu</span></span> | <span data-ttu-id="e14fe-218">16.04-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="e14fe-218">16.04-DAILY-LTS</span></span> | <span data-ttu-id="e14fe-219">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-219">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-220">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e14fe-220">Ubuntu</span></span> | <span data-ttu-id="e14fe-221">14.04.5-DAILY-LTS</span><span class="sxs-lookup"><span data-stu-id="e14fe-221">14.04.5-DAILY-LTS</span></span> | <span data-ttu-id="e14fe-222">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-222">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-223">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e14fe-223">Ubuntu</span></span> | <span data-ttu-id="e14fe-224">12.10</span><span class="sxs-lookup"><span data-stu-id="e14fe-224">12.10</span></span> | <span data-ttu-id="e14fe-225">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-225">Data disk</span></span> |
| <span data-ttu-id="e14fe-226">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="e14fe-226">Ubuntu</span></span> | <span data-ttu-id="e14fe-227">12.04</span><span class="sxs-lookup"><span data-stu-id="e14fe-227">12.04</span></span> | <span data-ttu-id="e14fe-228">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-228">Data disk</span></span> |
| <span data-ttu-id="e14fe-229">RHEL</span><span class="sxs-lookup"><span data-stu-id="e14fe-229">RHEL</span></span> | <span data-ttu-id="e14fe-230">7.3</span><span class="sxs-lookup"><span data-stu-id="e14fe-230">7.3</span></span> | <span data-ttu-id="e14fe-231">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-231">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-232">RHEL</span><span class="sxs-lookup"><span data-stu-id="e14fe-232">RHEL</span></span> | <span data-ttu-id="e14fe-233">7,2</span><span class="sxs-lookup"><span data-stu-id="e14fe-233">7.2</span></span> | <span data-ttu-id="e14fe-234">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-234">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-235">RHEL</span><span class="sxs-lookup"><span data-stu-id="e14fe-235">RHEL</span></span> | <span data-ttu-id="e14fe-236">6,8</span><span class="sxs-lookup"><span data-stu-id="e14fe-236">6.8</span></span> | <span data-ttu-id="e14fe-237">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-237">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-238">RHEL</span><span class="sxs-lookup"><span data-stu-id="e14fe-238">RHEL</span></span> | <span data-ttu-id="e14fe-239">6.7</span><span class="sxs-lookup"><span data-stu-id="e14fe-239">6.7</span></span> | <span data-ttu-id="e14fe-240">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-240">Data disk</span></span> |
| <span data-ttu-id="e14fe-241">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-241">CentOS</span></span> | <span data-ttu-id="e14fe-242">7.3</span><span class="sxs-lookup"><span data-stu-id="e14fe-242">7.3</span></span> | <span data-ttu-id="e14fe-243">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-243">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-244">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-244">CentOS</span></span> | <span data-ttu-id="e14fe-245">7.2n</span><span class="sxs-lookup"><span data-stu-id="e14fe-245">7.2n</span></span> | <span data-ttu-id="e14fe-246">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-246">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-247">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-247">CentOS</span></span> | <span data-ttu-id="e14fe-248">6,8</span><span class="sxs-lookup"><span data-stu-id="e14fe-248">6.8</span></span> | <span data-ttu-id="e14fe-249">Sistema operativo y disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-249">OS and Data disk</span></span> |
| <span data-ttu-id="e14fe-250">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-250">CentOS</span></span> | <span data-ttu-id="e14fe-251">7.1</span><span class="sxs-lookup"><span data-stu-id="e14fe-251">7.1</span></span> | <span data-ttu-id="e14fe-252">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-252">Data disk</span></span> |
| <span data-ttu-id="e14fe-253">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-253">CentOS</span></span> | <span data-ttu-id="e14fe-254">7.0</span><span class="sxs-lookup"><span data-stu-id="e14fe-254">7.0</span></span> | <span data-ttu-id="e14fe-255">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-255">Data disk</span></span> |
| <span data-ttu-id="e14fe-256">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-256">CentOS</span></span> | <span data-ttu-id="e14fe-257">6.7</span><span class="sxs-lookup"><span data-stu-id="e14fe-257">6.7</span></span> | <span data-ttu-id="e14fe-258">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-258">Data disk</span></span> |
| <span data-ttu-id="e14fe-259">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-259">CentOS</span></span> | <span data-ttu-id="e14fe-260">6.6</span><span class="sxs-lookup"><span data-stu-id="e14fe-260">6.6</span></span> | <span data-ttu-id="e14fe-261">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-261">Data disk</span></span> |
| <span data-ttu-id="e14fe-262">CentOS</span><span class="sxs-lookup"><span data-stu-id="e14fe-262">CentOS</span></span> | <span data-ttu-id="e14fe-263">6.5</span><span class="sxs-lookup"><span data-stu-id="e14fe-263">6.5</span></span> | <span data-ttu-id="e14fe-264">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-264">Data disk</span></span> |
| <span data-ttu-id="e14fe-265">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e14fe-265">openSUSE</span></span> | <span data-ttu-id="e14fe-266">13.2</span><span class="sxs-lookup"><span data-stu-id="e14fe-266">13.2</span></span> | <span data-ttu-id="e14fe-267">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-267">Data disk</span></span> |
| <span data-ttu-id="e14fe-268">SLES</span><span class="sxs-lookup"><span data-stu-id="e14fe-268">SLES</span></span> | <span data-ttu-id="e14fe-269">12 SP1</span><span class="sxs-lookup"><span data-stu-id="e14fe-269">12 SP1</span></span> | <span data-ttu-id="e14fe-270">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-270">Data disk</span></span> |
| <span data-ttu-id="e14fe-271">SLES</span><span class="sxs-lookup"><span data-stu-id="e14fe-271">SLES</span></span> | <span data-ttu-id="e14fe-272">12-SP1 (Premium)</span><span class="sxs-lookup"><span data-stu-id="e14fe-272">12-SP1 (Premium)</span></span> | <span data-ttu-id="e14fe-273">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-273">Data disk</span></span> |
| <span data-ttu-id="e14fe-274">SLES</span><span class="sxs-lookup"><span data-stu-id="e14fe-274">SLES</span></span> | <span data-ttu-id="e14fe-275">HPC 12</span><span class="sxs-lookup"><span data-stu-id="e14fe-275">HPC 12</span></span> | <span data-ttu-id="e14fe-276">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-276">Data disk</span></span> |
| <span data-ttu-id="e14fe-277">SLES</span><span class="sxs-lookup"><span data-stu-id="e14fe-277">SLES</span></span> | <span data-ttu-id="e14fe-278">11-SP4 (Premium)</span><span class="sxs-lookup"><span data-stu-id="e14fe-278">11-SP4 (Premium)</span></span> | <span data-ttu-id="e14fe-279">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-279">Data disk</span></span> |
| <span data-ttu-id="e14fe-280">SLES</span><span class="sxs-lookup"><span data-stu-id="e14fe-280">SLES</span></span> | <span data-ttu-id="e14fe-281">11 SP4</span><span class="sxs-lookup"><span data-stu-id="e14fe-281">11 SP4</span></span> | <span data-ttu-id="e14fe-282">Disco de datos</span><span class="sxs-lookup"><span data-stu-id="e14fe-282">Data disk</span></span> |

* <span data-ttu-id="e14fe-283">Cifrado del disco Azure requiere que el almacén de claves y las máquinas virtuales residan en hello misma región de Azure y la suscripción.</span><span class="sxs-lookup"><span data-stu-id="e14fe-283">Azure Disk Encryption requires that your key vault and VMs reside in hello same Azure region and subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-284">Configuración de recursos de hello en regiones independientes, produce un error en habilitar la característica de cifrado de disco de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-284">Configuring hello resources in separate regions causes a failure in enabling hello Azure Disk Encryption feature.</span></span>

* <span data-ttu-id="e14fe-285">tooset una copia de seguridad y configurar el almacén de claves para el cifrado de disco de Azure, consulte la sección **establecer una copia de seguridad y configurar el almacén de claves de cifrado del disco de Azure** en hello *requisitos previos* sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-285">tooset up and configure your key vault for Azure Disk Encryption, see section **Set up and configure your key vault for Azure Disk Encryption** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e14fe-286">tooset una copia de seguridad y configurar aplicación de Azure AD en Azure Active directory para el cifrado de disco de Azure, consulte la sección **Configurar aplicación hello Azure AD en Azure Active Directory** en hello *requisitos previos* sección de este artículo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-286">tooset up and configure Azure AD application in Azure Active directory for Azure Disk Encryption, see section **Set up hello Azure AD application in Azure Active Directory** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e14fe-287">tooset una copia de seguridad y configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD, consulte la sección **configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD** en hello *requisitos previos* sección de en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-287">tooset up and configure hello key vault access policy for hello Azure AD application, see section **Set up hello key vault access policy for hello Azure AD application** in hello *Prerequisites* section of this article.</span></span>
* <span data-ttu-id="e14fe-288">tooprepare un cifrado previamente VHD de Windows, consulte la sección **preparar un VHD de Windows cifrado previamente** en hello *apéndice*.</span><span class="sxs-lookup"><span data-stu-id="e14fe-288">tooprepare a pre-encrypted Windows VHD, see section **Prepare a pre-encrypted Windows VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="e14fe-289">tooprepare un VHD previamente cifradas de Linux, consulte la sección **preparar un VHD de Linux cifrado previamente** en hello *apéndice*.</span><span class="sxs-lookup"><span data-stu-id="e14fe-289">tooprepare a pre-encrypted Linux VHD, see section **Prepare a pre-encrypted Linux VHD** in hello *Appendix*.</span></span>
* <span data-ttu-id="e14fe-290">Hello plataforma Windows Azure necesita claves de cifrado de acceso toohello o secretos en el almacén de claves toomake su máquina virtual de toohello disponibles cuando inicia y se descifra el volumen de sistema operativo de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-290">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello virtual machine when it boots and decrypts hello virtual machine OS volume.</span></span> <span data-ttu-id="e14fe-291">plataforma de tooAzure toogrant permisos, conjunto hello **EnabledForDiskEncryption** propiedad en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-291">toogrant permissions tooAzure platform, set hello **EnabledForDiskEncryption** property in hello key vault.</span></span> <span data-ttu-id="e14fe-292">Para obtener más información, consulte **establecer una copia de seguridad y configurar el almacén de claves de cifrado del disco de Azure** Hola apéndice.</span><span class="sxs-lookup"><span data-stu-id="e14fe-292">For more information, see **Set up and configure your key vault for Azure Disk Encryption** in hello Appendix.</span></span>
* <span data-ttu-id="e14fe-293">El secreto del almacén de claves y las direcciones URL de KEK deben tener versiones.</span><span class="sxs-lookup"><span data-stu-id="e14fe-293">Your key vault secret and KEK URLs must be versioned.</span></span> <span data-ttu-id="e14fe-294">Azure exige esta restricción del control de versiones.</span><span class="sxs-lookup"><span data-stu-id="e14fe-294">Azure enforces this restriction of versioning.</span></span> <span data-ttu-id="e14fe-295">Para secreta y KEK las direcciones URL, vea hello en los ejemplos siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-295">For valid secret and KEK URLs, see hello following examples:</span></span>

  * <span data-ttu-id="e14fe-296">Ejemplo de dirección URL de secreto válida: *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="e14fe-296">Example of a valid secret URL:   *https://contosovault.vault.azure.net/secrets/BitLockerEncryptionSecretWithKek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="e14fe-297">Ejemplo de dirección URL de KEK válida: *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="e14fe-297">Example of a valid KEK URL:   *https://contosovault.vault.azure.net/keys/diskencryptionkek/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="e14fe-298">Azure Disk Encryption no admite que los números de puerto se especifiquen como parte de los secretos del almacén de claves y las direcciones URL de KEK.</span><span class="sxs-lookup"><span data-stu-id="e14fe-298">Azure Disk Encryption does not support specifying port numbers as part of key vault secrets and KEK URLs.</span></span> <span data-ttu-id="e14fe-299">Para obtener ejemplos de direcciones URL de almacén de claves admitidos y no admitidos, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-299">For examples of non-supported and supported key vault URLs, see hello following:</span></span>

  * <span data-ttu-id="e14fe-300">Dirección URL de almacén de claves no aceptable: *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="e14fe-300">Unacceptable key vault URL  *https://contosovault.vault.azure.net:443/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>
  * <span data-ttu-id="e14fe-301">Dirección URL de almacén de claves aceptable: *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span><span class="sxs-lookup"><span data-stu-id="e14fe-301">Acceptable key vault URL:   *https://contosovault.vault.azure.net/secrets/contososecret/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx*</span></span>

* <span data-ttu-id="e14fe-302">característica de cifrado del disco de Azure de hello tooenable, hello las máquinas virtuales IaaS debe cumplir Hola según los requisitos de configuración de punto de conexión de red:</span><span class="sxs-lookup"><span data-stu-id="e14fe-302">tooenable hello Azure Disk Encryption feature, hello IaaS VMs must meet hello following network endpoint configuration requirements:</span></span>
  * <span data-ttu-id="e14fe-303">tooget un almacén de claves de tooyour tooconnect token, Hola IaaS VM debe ser capaz de tooconnect punto de conexión de Azure Active Directory de tooan, \[login.microsoftonline.com\].</span><span class="sxs-lookup"><span data-stu-id="e14fe-303">tooget a token tooconnect tooyour key vault, hello IaaS VM must be able tooconnect tooan Azure Active Directory endpoint, \[login.microsoftonline.com\].</span></span>
  * <span data-ttu-id="e14fe-304">toowrite Hola cifrado claves tooyour almacén de claves, Hola IaaS VM debe ser el punto de conexión de tooconnect puede toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-304">toowrite hello encryption keys tooyour key vault, hello IaaS VM must be able tooconnect toohello key vault endpoint.</span></span>
  * <span data-ttu-id="e14fe-305">Hola IaaS VM, debe ser capaz de tooconnect tooan almacenamiento de Azure extremo que hosts Hola repositorio de extensión de Azure y una cuenta de almacenamiento de Azure que hosts Hola archivos VHD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-305">hello IaaS VM must be able tooconnect tooan Azure storage endpoint that hosts hello Azure extension repository and an Azure storage account that hosts hello VHD files.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e14fe-306">Si la directiva de seguridad limita el acceso de máquinas virtuales de Azure toohello Internet, puede resolver Hola anterior URI y configurar una toohello de conectividad saliente de tooallow direcciones IP de regla concreta.</span><span class="sxs-lookup"><span data-stu-id="e14fe-306">If your security policy limits access from Azure VMs toohello Internet, you can resolve hello preceding URI and configure a specific rule tooallow outbound connectivity toohello IPs.</span></span>
  >
  ><span data-ttu-id="e14fe-307">tooconfigure y acceso del almacén de claves de Azure detrás de un firewall (https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span><span class="sxs-lookup"><span data-stu-id="e14fe-307">tooconfigure and access Azure Key Vault behind a firewall(https://docs.microsoft.com/en-us/azure/key-vault/key-vault-access-behind-firewall)</span></span>

* <span data-ttu-id="e14fe-308">Use Hola última versión del SDK de Azure PowerShell versión tooconfigure cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-308">Use hello latest version of Azure PowerShell SDK version tooconfigure Azure Disk Encryption.</span></span> <span data-ttu-id="e14fe-309">Descargar la versión más reciente de Hola de [versión de PowerShell de Azure](https://github.com/Azure/azure-powershell/releases)</span><span class="sxs-lookup"><span data-stu-id="e14fe-309">Download hello latest version of [Azure PowerShell release](https://github.com/Azure/azure-powershell/releases)</span></span>

 > [!NOTE]
  > <span data-ttu-id="e14fe-310">En el [SDK de Azure PowerShell (versión 1.1.0)](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016) no se admite Azure Disk Encryption.</span><span class="sxs-lookup"><span data-stu-id="e14fe-310">Azure Disk Encryption is not supported on [Azure PowerShell SDK version 1.1.0](https://github.com/Azure/azure-powershell/releases/tag/v1.1.0-January2016).</span></span> <span data-ttu-id="e14fe-311">Si recibe un error relacionado con toousing Azure PowerShell 1.1.0, consulte [tooAzure relacionados de Error de cifrado de Azure disco PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-311">If you are receiving an error related toousing Azure PowerShell 1.1.0, see [Azure Disk Encryption Error Related tooAzure PowerShell 1.1.0](http://blogs.msdn.com/b/azuresecurity/archive/2016/02/10/azure-disk-encryption-error-related-to-azure-powershell-1-1-0.aspx).</span></span>

* <span data-ttu-id="e14fe-312">toorun cualquier comando de CLI de Azure y asociarlo con su suscripción de Azure, primero debe instalar la CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="e14fe-312">toorun any Azure CLI command and associate it with your Azure subscription, you must first install Azure CLI:</span></span>
  * <span data-ttu-id="e14fe-313">tooinstall CLI de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e14fe-313">tooinstall Azure CLI and associate it with your Azure subscription, see [How tooinstall and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="e14fe-314">toouse CLI de Azure para Mac, Linux y Windows con el Administrador de recursos de Azure, consulte [comandos de CLI de Azure en el modo de administrador de recursos](../virtual-machines/azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="e14fe-314">toouse Azure CLI for Mac, Linux, and Windows with Azure Resource Manager, see [Azure CLI commands in Resource Manager mode](../virtual-machines/azure-cli-arm-commands.md).</span></span>

* <span data-ttu-id="e14fe-315">Cuando se cifra un disco administrado, es obligatorio tootake requisitos previos una instantánea del disco de hello administrada o una copia de seguridad del disco de hello fuera de cifrado de tooenabling anteriores de cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-315">When encrypting a managed disk, it is mandatory prerequisite tootake a snapshot of hello managed disk or a backup of hello disk outside of Azure Disk Encryption prior tooenabling encryption.</span></span>  <span data-ttu-id="e14fe-316">Sin una copia de seguridad en su lugar, cualquier error inesperado durante el cifrado puede presentar disco hello y VM accesible sin una opción de recuperación.</span><span class="sxs-lookup"><span data-stu-id="e14fe-316">Without a backup in place, any unexpected failure during encryption may render hello disk and VM inaccessible without a recovery option.</span></span>  <span data-ttu-id="e14fe-317">AzureRmVMDiskEncryptionExtension de conjunto de copia de seguridad discos administrados actualmente no y se generará un error si se utilizan en un disco administrado a menos que se ha especificado el parámetro - skipVmBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-317">Set-AzureRmVMDiskEncryptionExtension does not currently back up managed disks and will error if used against a managed disk unless hello -skipVmBackup parameter has been specified.</span></span>  <span data-ttu-id="e14fe-318">Este parámetro es toouse unsafe, a menos que ya se hizo una copia de seguridad fuera de cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-318">This parameter is unsafe toouse unless a backup has already been made outside of Azure Disk Encryption.</span></span>   <span data-ttu-id="e14fe-319">Cuando se especifica el parámetro - skipVmBackup de hello, Hola cmdlet no realizará una copia de seguridad de hello administrado disco anterior tooencryption.</span><span class="sxs-lookup"><span data-stu-id="e14fe-319">When hello -skipVmBackup parameter is specified, hello cmdlet will not make a backup of hello managed disk prior tooencryption.</span></span>  <span data-ttu-id="e14fe-320">Por este motivo, se considera un toomake de requisitos previos obligatorio que necesite una copia de seguridad de disco administrado Hola que VM está en la posición anterior tooenabling cifrado del disco de Azure en caso de recuperación es posterior.</span><span class="sxs-lookup"><span data-stu-id="e14fe-320">For this reason, it is considered a mandatory prerequisite toomake sure a backup of hello managed disk VM is in place prior tooenabling Azure Disk Encryption in case recovery is later needed.</span></span>  
> [!NOTE]
 > <span data-ttu-id="e14fe-321">parámetro de Hello - skipVmBackup nunca debe utilizarse a menos que ya ha realizado una copia de seguridad o de instantáneas fuera de cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-321">hello -skipVmBackup parameter should never be used unless a snapshot or backup has already been made outside of Azure Disk Encryption.</span></span> 

* <span data-ttu-id="e14fe-322">Hola soluciones de cifrado del disco de Azure usa el protector de clave externo de hello BitLocker para máquinas virtuales de IaaS de Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-322">hello Azure Disk Encryption solution uses hello BitLocker external key protector for Windows IaaS VMs.</span></span> <span data-ttu-id="e14fe-323">Para las máquinas virtuales unidas en un dominio, NO cree ninguna directiva de grupo que exija protectores de TPM.</span><span class="sxs-lookup"><span data-stu-id="e14fe-323">For domain joined VMs, DO NOT push any group policies that enforce TPM protectors.</span></span> <span data-ttu-id="e14fe-324">Para obtener información acerca de la directiva de grupo de Hola "Permitir BitLocker sin un TPM compatible", consulte [referencia de directiva de grupo de BitLocker](https://technet.microsoft.com/library/ee706521).</span><span class="sxs-lookup"><span data-stu-id="e14fe-324">For information about hello group policy for “Allow BitLocker without a compatible TPM,” see [BitLocker Group Policy Reference](https://technet.microsoft.com/library/ee706521).</span></span>
* <span data-ttu-id="e14fe-325">Directiva de BitLocker en las máquinas virtuales Unidos a un dominio con directiva de grupo personalizado debe incluir Hola después de configuración: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key` cifrado del disco de Azure se producirá un error cuando la configuración de directiva de grupo personalizado para que Bitlocker no es compatibles.</span><span class="sxs-lookup"><span data-stu-id="e14fe-325">Bitlocker policy on domain joined virtual machines with custom group policy must include hello following setting: `Configure user storage of bitlocker recovery information -> Allow 256-bit recovery key`  Azure Disk Encryption will fail when custom group policy settings for Bitlocker are incompatible.</span></span> <span data-ttu-id="e14fe-326">En equipos que no dispongan de hello pueden requerir configuración de directiva correcta, aplicar la nueva directiva de hello, forzar Hola nueva directiva tooupdate (gpupdate.exe /force) y, a continuación, reinicia el sistema.</span><span class="sxs-lookup"><span data-stu-id="e14fe-326">On machines that did not have hello correct policy setting, applying hello new policy, forcing hello new policy tooupdate (gpupdate.exe /force), and then restarting may be required.</span></span>  
* <span data-ttu-id="e14fe-327">toocreate una aplicación de Azure AD, crear un almacén de claves, o configurar un almacén de claves existente y habilitar el cifrado, vea hello [script de PowerShell de requisitos previos de cifrado del disco de Azure](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span><span class="sxs-lookup"><span data-stu-id="e14fe-327">toocreate an Azure AD application, create a key vault, or set up an existing key vault and enable encryption, see hello [Azure Disk Encryption prerequisite PowerShell script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1).</span></span>
* <span data-ttu-id="e14fe-328">requisitos previos de cifrado del disco tooconfigure con hello CLI de Azure, consulte [esta secuencia de comandos de Bash](https://github.com/ejarvi/ade-cli-getting-started).</span><span class="sxs-lookup"><span data-stu-id="e14fe-328">tooconfigure disk-encryption prerequisites using hello Azure CLI, see [this Bash script](https://github.com/ejarvi/ade-cli-getting-started).</span></span>
* <span data-ttu-id="e14fe-329">tooback de servicio de copia de seguridad de Azure toouse Hola seguridad y restauración cifrado las máquinas virtuales, cuando está habilitado el cifrado con el cifrado de disco de Azure, cifran las máquinas virtuales mediante la configuración de clave de cifrado del disco de Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-329">toouse hello Azure Backup service tooback up and restore encrypted VMs, when encryption is enabled with Azure Disk Encryption, encrypt your VMs by using hello Azure Disk Encryption key configuration.</span></span> <span data-ttu-id="e14fe-330">Hola servicio de copia de seguridad es compatible con las máquinas virtuales que se cifran mediante la configuración de la KEK solo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-330">hello Backup service supports VMs that are encrypted using KEK configuration only.</span></span> <span data-ttu-id="e14fe-331">Vea [cómo tooback seguridad y restauración cifran las máquinas virtuales con cifrado de copia de seguridad de Azure](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span><span class="sxs-lookup"><span data-stu-id="e14fe-331">See [How tooback up and restore encrypted virtual machines with Azure Backup  encryption](https://docs.microsoft.com/en-us/azure/backup/backup-azure-vms-encryption).</span></span>

* <span data-ttu-id="e14fe-332">Cuando se cifra un volumen de sistema operativo Linux, tenga en cuenta que un reinicio de máquina virtual actualmente al final de hello del proceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-332">When encrypting a Linux OS volume, note that a VM restart is currently required at hello end of hello process.</span></span> <span data-ttu-id="e14fe-333">Esto puede hacerse a través del portal de hello, powershell o CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-333">This can be done via hello portal, powershell, or CLI.</span></span>   <span data-ttu-id="e14fe-334">progreso de hello tootrack del cifrado, éstos sondeen periódicamente mensajes de estado de hello devuelto por Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span><span class="sxs-lookup"><span data-stu-id="e14fe-334">tootrack hello progress of encryption, periodically poll hello status message returned by Get-AzureRmVMDiskEncryptionStatus https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus.</span></span>  <span data-ttu-id="e14fe-335">Una vez completado el cifrado, el mensaje de estado de Hola Hola devuelta por este comando indicará esto.</span><span class="sxs-lookup"><span data-stu-id="e14fe-335">Once encryption is complete, hello hello status message returned by this command will indicate this.</span></span>  <span data-ttu-id="e14fe-336">Por ejemplo, "ProgressMessage: disco del sistema operativo cifrado correctamente, reinicie Hola máquina virtual" en este Hola de punto de VM se pueden reiniciar y usar.</span><span class="sxs-lookup"><span data-stu-id="e14fe-336">For example, "ProgressMessage: OS disk successfully encrypted, please reboot hello VM"  At this point hello VM can be restarted and used.</span></span>  

* <span data-ttu-id="e14fe-337">Cifrado de disco de Azure para Linux requiere toohave de discos de datos un sistema de archivos montado en tooencryption anterior de Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-337">Azure Disk Encryption for Linux requires data disks toohave a mounted file system in Linux prior tooencryption</span></span>

* <span data-ttu-id="e14fe-338">Hola cifrado del disco de Azure no admite discos de datos montados para Linux de forma recursiva.</span><span class="sxs-lookup"><span data-stu-id="e14fe-338">Recursively mounted data disks are not supported by hello Azure Disk Encryption for Linux.</span></span> <span data-ttu-id="e14fe-339">Por ejemplo, si hello sistema de destino monta un disco en /foo/bar y, a continuación, otro en /foo/bar/baz, cifrado de Hola de /foo/bar/baz se realizará correctamente, pero se producirá un error de cifrado de/foo/barra.</span><span class="sxs-lookup"><span data-stu-id="e14fe-339">For example, if hello target system has mounted a disk on /foo/bar and then another on /foo/bar/baz, hello encryption of /foo/bar/baz will succeed, but encryption of /foo/bar will fail.</span></span> 

* <span data-ttu-id="e14fe-340">Cifrado de disco Azure solo es compatible con imágenes de la Galería de Azure compatible que cumplen los requisitos previos mencionados anteriormente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-340">Azure Disk Encryption is only supported on Azure gallery supported images that meet hello aforementioned prerequisites.</span></span> <span data-ttu-id="e14fe-341">Imágenes personalizadas de cliente no se admiten debido a los esquemas de partición de toocustom y comportamientos de los procesos que puedan existir en estas imágenes.</span><span class="sxs-lookup"><span data-stu-id="e14fe-341">Customer custom images are not supported due toocustom partition schemes and process behaviors that may exist on these images.</span></span> <span data-ttu-id="e14fe-342">Además, incluso pueden no ser compatibles las máquinas virtuales basadas en imágenes de la galería que inicialmente cumplieran los requisitos previos, pero fueran modificadas después de su creación.</span><span class="sxs-lookup"><span data-stu-id="e14fe-342">Further, even gallery image based VM's that initially met prerequisites but have been modified after creation may be incompatible.</span></span>  <span data-ttu-id="e14fe-343">Para que motivo, Hola sugerido procedimiento para cifrar una VM Linux es toostart desde una imagen de galería limpia, cifrar Hola VM y, a continuación, agregar software personalizado o datos toohello VM según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="e14fe-343">For that reason, hello suggested procedure for encrypting a Linux VM is toostart from a clean gallery image, encrypt hello VM, and then add custom software or data toohello VM as needed.</span></span>  

> [!NOTE]
> <span data-ttu-id="e14fe-344">Copia de seguridad y restauración de máquinas virtuales cifradas solo se admite para las máquinas virtuales que se cifran con la configuración de KEK Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-344">Backup and restore of encrypted VMs is supported only for VMs that are encrypted with hello KEK configuration.</span></span> <span data-ttu-id="e14fe-345">No se admite en máquinas virtuales cifradas sin KEK.</span><span class="sxs-lookup"><span data-stu-id="e14fe-345">It is not supported on VMs that are encrypted without KEK.</span></span> <span data-ttu-id="e14fe-346">KEK es un parámetro opcional que habilita las máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-346">KEK is an optional parameter that enables VM.</span></span>

#### <a name="set-up-hello-azure-ad-application-in-azure-active-directory"></a><span data-ttu-id="e14fe-347">Configurar Hola aplicación de Azure AD en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e14fe-347">Set up hello Azure AD application in Azure Active Directory</span></span>
<span data-ttu-id="e14fe-348">Cuando necesite toobe cifrado habilitado en una máquina virtual en ejecución en Azure, el cifrado del disco de Azure genera y escribe el almacén de claves de tooyour de claves de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-348">When you need encryption toobe enabled on a running VM in Azure, Azure Disk Encryption generates and writes hello encryption keys tooyour key vault.</span></span> <span data-ttu-id="e14fe-349">La administración de claves de cifrado en el almacén de claves necesita la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-349">Managing encryption keys in your key vault requires Azure AD authentication.</span></span>

<span data-ttu-id="e14fe-350">Para ello, cree una aplicación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-350">For this purpose, create an Azure AD application.</span></span> <span data-ttu-id="e14fe-351">Encontrará pasos detallados para registrar una aplicación en la sección de "Obtener una identidad para hello aplicación" hello de entrada de blog de hello [almacén de claves de Azure - paso a paso](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-351">You can find detailed steps for registering an application in hello “Get an Identity for hello Application” section of hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="e14fe-352">Esta entrada también contiene varios ejemplos útiles sobre la instalación y la configuración del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-352">This post also contains a number of helpful examples for setting up and configuring your key vault.</span></span> <span data-ttu-id="e14fe-353">Para realizar la autenticación, se pueden usar la autenticación basada en secreto de cliente o la autenticación de Azure AD basada en certificado del cliente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-353">For authentication purposes, you can use either client secret-based authentication or client certificate-based Azure AD authentication.</span></span>

#### <a name="client-secret-based-authentication-for-azure-ad"></a><span data-ttu-id="e14fe-354">Autenticación basada en secreto de cliente para Azure AD</span><span class="sxs-lookup"><span data-stu-id="e14fe-354">Client secret-based authentication for Azure AD</span></span>
<span data-ttu-id="e14fe-355">secciones de Hello siguientes pueden ayudarle a configurar una autenticación basada en el secreto del cliente para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-355">hello sections that follow can help you configure a client secret-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application-by-using-azure-powershell"></a><span data-ttu-id="e14fe-356">Creación de una aplicación de Azure AD mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e14fe-356">Create an Azure AD application by using Azure PowerShell</span></span>
<span data-ttu-id="e14fe-357">Usar hello después toocreate de cmdlet de PowerShell una aplicación de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e14fe-357">Use hello following PowerShell cmdlet toocreate an Azure AD application:</span></span>

    $aadClientSecret = "yourSecret"
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -Password $aadClientSecret
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

> [!NOTE]
> <span data-ttu-id="e14fe-358">$azureAdApplication.ApplicationId es hello Azure AD ClientID y $aadClientSecret es el secreto del cliente de Hola que debe usar tooenable posterior cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-358">$azureAdApplication.ApplicationId is hello Azure AD ClientID and $aadClientSecret is hello client secret that you should use later tooenable Azure Disk Encryption.</span></span> <span data-ttu-id="e14fe-359">Proteger el secreto del cliente hello Azure AD adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-359">Safeguard hello Azure AD client secret appropriately.</span></span>

##### <a name="setting-up-hello-azure-ad-client-id-and-secret-from-hello-azure-classic-portal"></a><span data-ttu-id="e14fe-360">Configurar identificador hello Azure AD y el secreto de hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="e14fe-360">Setting up hello Azure AD client ID and secret from hello Azure classic portal</span></span>
<span data-ttu-id="e14fe-361">También puede configurar el Id. de cliente de Azure AD y el secreto mediante el uso de hello [portal de Azure clásico]( https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e14fe-361">You can also set up your Azure AD client ID and secret by using hello [Azure classic portal]( https://manage.windowsazure.com).</span></span> <span data-ttu-id="e14fe-362">tooperform esta tarea, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-362">tooperform this task, do hello following:</span></span>

1. <span data-ttu-id="e14fe-363">Haga clic en hello **Active Directory** ficha.</span><span class="sxs-lookup"><span data-stu-id="e14fe-363">Click hello **Active Directory** tab.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig3.png)

2. <span data-ttu-id="e14fe-365">Haga clic en **Agregar aplicación**y, a continuación, nombre de aplicación de tipo Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-365">Click **Add Application**, and then type hello application name.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig4.png)

3. <span data-ttu-id="e14fe-367">Haga clic en el botón de flecha de hello y, a continuación, configurar propiedades de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-367">Click hello arrow button, and then configure hello application properties.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig5.png)

4. <span data-ttu-id="e14fe-369">Haga clic en la marca de verificación de hello en hello toofinish de esquina izquierda inferior.</span><span class="sxs-lookup"><span data-stu-id="e14fe-369">Click hello check mark in hello lower left corner toofinish.</span></span> <span data-ttu-id="e14fe-370">Aparecerá la página de configuración de aplicación Hola e Id. de cliente de AD Azure Hola se muestra en parte inferior de Hola de página de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-370">hello application configuration page appears, and hello Azure AD client ID is displayed at hello bottom of hello page.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig6.png)

5. <span data-ttu-id="e14fe-372">Guardar el secreto del cliente hello Azure AD haciendo clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="e14fe-372">Save hello Azure AD client secret by clicking hello **Save** button.</span></span> <span data-ttu-id="e14fe-373">Tenga en cuenta secreta de cliente hello Azure AD en el cuadro de texto de las claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-373">Note hello Azure AD client secret in hello keys text box.</span></span> <span data-ttu-id="e14fe-374">Protéjalo adecuadamente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-374">Safeguard it appropriately.</span></span>

 ![Azure Disk Encryption](./media/azure-security-disk-encryption/disk-encryption-fig7.png)

 > [!NOTE]
 > <span data-ttu-id="e14fe-376">Hola anterior flujo no se admite en hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="e14fe-376">hello preceding flow is not supported on hello Azure classic portal.</span></span>

##### <a name="use-an-existing-application"></a><span data-ttu-id="e14fe-377">Uso de una aplicación existente</span><span class="sxs-lookup"><span data-stu-id="e14fe-377">Use an existing application</span></span>
<span data-ttu-id="e14fe-378">tooexecute Hola siga los comandos, obtener y usar hello [módulo de PowerShell de Azure AD](https://technet.microsoft.com/library/jj151815.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-378">tooexecute hello following commands, obtain and use hello [Azure AD PowerShell module](https://technet.microsoft.com/library/jj151815.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-379">Hello siguientes comandos se deben ejecutar desde una nueva ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e14fe-379">hello following commands must be executed from a new PowerShell window.</span></span> <span data-ttu-id="e14fe-380">No utilice Azure PowerShell o comandos de hello Azure Resource Manager ventana tooexecute Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-380">Do not use Azure PowerShell or hello Azure Resource Manager window tooexecute hello commands.</span></span> <span data-ttu-id="e14fe-381">Se recomienda este enfoque porque estos cmdlets están en el módulo de MSOnline de Hola o PowerShell de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-381">We recommend this approach because these cmdlets are in hello MSOnline module or Azure AD PowerShell.</span></span>

    $clientSecret = ‘<yourAadClientSecret>’
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type password -Value $clientSecret

#### <a name="certificate-based-authentication-for-azure-ad"></a><span data-ttu-id="e14fe-382">Autenticación basada en certificado para Azure AD</span><span class="sxs-lookup"><span data-stu-id="e14fe-382">Certificate-based authentication for Azure AD</span></span>
> [!NOTE]
> <span data-ttu-id="e14fe-383">Actualmente no se admite la autenticación basada en certificado de Azure AD en máquinas virtuales con Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-383">Azure AD certificate-based authentication is currently not supported on Linux VMs.</span></span>

<span data-ttu-id="e14fe-384">Hola secciones siguientes muestran cómo tooconfigure una autenticación basada en certificados para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-384">hello sections that follow show how tooconfigure a certificate-based authentication for Azure AD.</span></span>

##### <a name="create-an-azure-ad-application"></a><span data-ttu-id="e14fe-385">Creación de una aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="e14fe-385">Create an Azure AD application</span></span>
<span data-ttu-id="e14fe-386">toocreate una aplicación de Azure AD, ejecute hello siguientes cmdlets de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e14fe-386">toocreate an Azure AD application, execute hello following PowerShell cmdlets:</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-387">Reemplace Hola siguiente `yourpassword` cadena con su contraseña segura y la contraseña de Hola de medida de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e14fe-387">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $cert = New-Object System.Security.Cryptography.X509Certificates.X509Certificate("C:\certificates\examplecert.pfx", "yourpassword")
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    $azureAdApplication = New-AzureRmADApplication -DisplayName "<Your Application Display Name>" -HomePage "<https://YourApplicationHomePage>" -IdentifierUris "<https://YouApplicationUri>" -KeyValue $keyValue -KeyType AsymmetricX509Cert
    $servicePrincipal = New-AzureRmADServicePrincipal –ApplicationId $azureAdApplication.ApplicationId

<span data-ttu-id="e14fe-388">Una vez finalizado este paso, cargar un almacén de claves de tooyour de archivo PFX y habilitar Hola acceso directiva necesaria toodeploy esa VM tooa de certificado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-388">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy needed toodeploy that certificate tooa VM.</span></span>

##### <a name="use-an-existing-azure-ad-application"></a><span data-ttu-id="e14fe-389">Uso de una aplicación de Azure AD existente</span><span class="sxs-lookup"><span data-stu-id="e14fe-389">Use an existing Azure AD application</span></span>
<span data-ttu-id="e14fe-390">Si va a configurar la autenticación basada en certificados para una aplicación existente, use cmdlets de PowerShell de Hola que se muestra aquí.</span><span class="sxs-lookup"><span data-stu-id="e14fe-390">If you are configuring certificate-based authentication for an existing application, use hello PowerShell cmdlets shown here.</span></span> <span data-ttu-id="e14fe-391">Ser tooexecute seguro de ellas desde una nueva ventana de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e14fe-391">Be sure tooexecute them from a new PowerShell window.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.cer'
    $aadClientID = '<Client ID of your Azure AD application>'
    connect-msolservice
    $cer = New-Object System.Security.Cryptography.X509Certificates.X509Certificate
    $cer.Import($certLocalPath)
    $binCert = $cer.GetRawCertData()
    $credValue = [System.Convert]::ToBase64String($binCert);
    New-MsolServicePrincipalCredential -AppPrincipalId $aadClientID -Type asymmetric -Value $credValue -Usage verify

<span data-ttu-id="e14fe-392">Una vez finalizado este paso, cargar un almacén de claves de tooyour de archivo PFX y habilitar Directiva de acceso de hello requerido toodeploy Hola certificado tooa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-392">After you finish this step, upload a PFX file tooyour key vault and enable hello access policy that's needed toodeploy hello certificate tooa VM.</span></span>

##### <a name="upload-a-pfx-file-tooyour-key-vault"></a><span data-ttu-id="e14fe-393">Cargar un almacén de claves de tooyour de archivo PFX</span><span class="sxs-lookup"><span data-stu-id="e14fe-393">Upload a PFX file tooyour key vault</span></span>
<span data-ttu-id="e14fe-394">Para obtener una explicación detallada de este proceso, consulte [Hola Blog oficial del equipo de almacén de claves de Azure](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-394">For a detailed explanation of this process, see [hello Official Azure Key Vault Team Blog](http://blogs.technet.com/b/kv/archive/2015/07/14/vm_2d00_certificates.aspx).</span></span> <span data-ttu-id="e14fe-395">Sin embargo, Hola siguientes cmdlets de PowerShell es todo lo que necesita para la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-395">However, hello following PowerShell cmdlets are all you need for hello task.</span></span> <span data-ttu-id="e14fe-396">Ser tooexecute seguro desde la consola de PowerShell de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-396">Be sure tooexecute them from Azure PowerShell console.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-397">Reemplace Hola siguiente `yourpassword` cadena con su contraseña segura y la contraseña de Hola de medida de seguridad.</span><span class="sxs-lookup"><span data-stu-id="e14fe-397">Replace hello following `yourpassword` string with your secure password, and safeguard hello password.</span></span>

    $certLocalPath = 'C:\certs\myaadapp.pfx'
    $certPassword = "yourpassword"
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’

    $fileContentBytes = get-content $certLocalPath -Encoding Byte
    $fileContentEncoded = [System.Convert]::ToBase64String($fileContentBytes)

    $jsonObject = @"
    {
    "data": "$filecontentencoded",
    "dataType" :"pfx",
    "password": "$certPassword"
    }
    "@

    $jsonObjectBytes = [System.Text.Encoding]::UTF8.GetBytes($jsonObject)
    $jsonEncoded = [System.Convert]::ToBase64String($jsonObjectBytes)

    Switch-AzureMode -Name AzureResourceManager
    $secret = ConvertTo-SecureString -String $jsonEncoded -AsPlainText -Force
    Set-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName -SecretValue $secret
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ResourceGroupName $resourceGroupName –EnabledForDeployment

##### <a name="deploy-a-certificate-in-your-key-vault-tooan-existing-vm"></a><span data-ttu-id="e14fe-398">Implementar un certificado en su tooan de almacén de claves existente de la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e14fe-398">Deploy a certificate in your key vault tooan existing VM</span></span>
<span data-ttu-id="e14fe-399">Cuando termine de cargar Hola PFX, implemente un certificado en hello tooan de almacén de claves existente VM con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-399">After you finish uploading hello PFX, deploy a certificate in hello key vault tooan existing VM with hello following:</span></span>
 ```
    $resourceGroupName = ‘yourResourceGroup’
    $keyVaultName = ‘yourKeyVaultName’
    $keyVaultSecretName = ‘yourAadCertSecretName’
    $vmName = ‘yourVMName’
    $certUrl = (Get-AzureKeyVaultSecret -VaultName $keyVaultName -Name $keyVaultSecretName).Id
    $sourceVaultId = (Get-AzureRmKeyVault -VaultName $keyVaultName -ResourceGroupName $resourceGroupName).ResourceId
    $vm = Get-AzureRmVM -ResourceGroupName $resourceGroupName -Name $vmName
    $vm = Add-AzureRmVMSecret -VM $vm -SourceVaultId $sourceVaultId -CertificateStore "My" -CertificateUrl $certUrl
    Update-AzureRmVM -VM $vm  -ResourceGroupName $resourceGroupName
 ```

#### <a name="set-up-hello-key-vault-access-policy-for-hello-azure-ad-application"></a><span data-ttu-id="e14fe-400">Configurar la directiva de acceso de almacén de claves de hello para la aplicación hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e14fe-400">Set up hello key vault access policy for hello Azure AD application</span></span>
<span data-ttu-id="e14fe-401">La aplicación de Azure AD necesita claves de derechos tooaccess Hola o secretos en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-401">Your Azure AD application needs rights tooaccess hello keys or secrets in hello vault.</span></span> <span data-ttu-id="e14fe-402">Hola de uso [ `Set-AzureKeyVaultAccessPolicy` ](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permisos toohello de aplicaciones, mediante el identificador de cliente de hello (que se generó cuando se registró la aplicación hello) como hello _– ServicePrincipalName_ valor del parámetro.</span><span class="sxs-lookup"><span data-stu-id="e14fe-402">Use hello [`Set-AzureKeyVaultAccessPolicy`](/powershell/module/azure/set-azurekeyvaultaccesspolicy?view=azuresmps-3.7.0) cmdlet toogrant permissions toohello application, using hello client ID (which was generated when hello application was registered) as hello _–ServicePrincipalName_ parameter value.</span></span> <span data-ttu-id="e14fe-403">toolearn más información, consulte Entrada de blog hello [almacén de claves de Azure - paso a paso](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-403">toolearn more, see hello blog post [Azure Key Vault - Step by Step](http://blogs.technet.com/b/kv/archive/2015/06/02/azure-key-vault-step-by-step.aspx).</span></span> <span data-ttu-id="e14fe-404">Este es un ejemplo de cómo tooperform esta tarea a través de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e14fe-404">Here is an example of how tooperform this task via PowerShell:</span></span>

    $keyVaultName = '<yourKeyVaultName>'
    $aadClientID = '<yourAadAppClientID>'
    $rgname = '<yourResourceGroup>'
    Set-AzureRmKeyVaultAccessPolicy -VaultName $keyVaultName -ServicePrincipalName $aadClientID -PermissionsToKeys 'WrapKey' -PermissionsToSecrets 'Set' -ResourceGroupName $rgname

> [!NOTE]
> <span data-ttu-id="e14fe-405">Cifrado de disco de Azure requiere hello tooconfigure tras la aplicación de cliente de acceso a las directivas tooyour Azure AD: _WrapKey_ y _establecer_ permisos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-405">Azure Disk Encryption requires you tooconfigure hello following access policies tooyour Azure AD client application: _WrapKey_ and _Set_ permissions.</span></span>

## <a name="terminology"></a><span data-ttu-id="e14fe-406">Terminología</span><span class="sxs-lookup"><span data-stu-id="e14fe-406">Terminology</span></span>
<span data-ttu-id="e14fe-407">toounderstand algunos de los términos comunes que Hola utilizan esta tecnología, Hola uso terminología en la tabla siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-407">toounderstand some of hello common terms used by this technology, use hello following terminology table:</span></span>

| <span data-ttu-id="e14fe-408">Terminología</span><span class="sxs-lookup"><span data-stu-id="e14fe-408">Terminology</span></span> | <span data-ttu-id="e14fe-409">Definición</span><span class="sxs-lookup"><span data-stu-id="e14fe-409">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-410">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e14fe-410">Azure AD</span></span> | <span data-ttu-id="e14fe-411">Azure AD es [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-411">Azure AD is [Azure Active Directory](https://azure.microsoft.com/documentation/services/active-directory/).</span></span> <span data-ttu-id="e14fe-412">Una cuenta de Azure AD es un requisito previo para autenticar, almacenar y recuperar secretos del almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-412">An Azure AD account is a prerequisite for authenticating, storing, and retrieving secrets from a key vault.</span></span> |
| <span data-ttu-id="e14fe-413">Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-413">Azure Key Vault</span></span> | <span data-ttu-id="e14fe-414">Key Vault es un servicio de administración de claves criptográficas basado en módulos de seguridad de hardware validados por el Estándar federal de procesamiento de información (FIPS), que ayuda a proteger las claves criptográficas y los secretos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-414">Key Vault is a cryptographic, key management service that's based on Federal Information Processing Standards (FIPS)-validated hardware security modules, which help safeguard your cryptographic keys and sensitive secrets.</span></span> <span data-ttu-id="e14fe-415">Para obtener más información, consulte la documentación de [Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-415">For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="e14fe-416">ARM</span><span class="sxs-lookup"><span data-stu-id="e14fe-416">ARM</span></span> | <span data-ttu-id="e14fe-417">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-417">Azure Resource Manager</span></span> |
| <span data-ttu-id="e14fe-418">BitLocker</span><span class="sxs-lookup"><span data-stu-id="e14fe-418">BitLocker</span></span> |<span data-ttu-id="e14fe-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) es una reconocido del sector volumen cifrado tecnología de Windows que ha utilizado el cifrado del disco tooenable en máquinas virtuales de IaaS de Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-419">[BitLocker](https://technet.microsoft.com/library/hh831713.aspx) is an industry-recognized Windows volume encryption technology that's used tooenable disk encryption on Windows IaaS VMs.</span></span> |
| <span data-ttu-id="e14fe-420">BEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-420">BEK</span></span> | <span data-ttu-id="e14fe-421">Las claves de cifrado de BitLocker son volúmenes de datos y el volumen de arranque de hello OS tooencrypt usado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-421">BitLocker encryption keys are used tooencrypt hello OS boot volume and data volumes.</span></span> <span data-ttu-id="e14fe-422">las claves de BitLocker de Hello están protegidas en un almacén de claves como secretos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-422">hello BitLocker keys are safeguarded in a key vault as secrets.</span></span> |
| <span data-ttu-id="e14fe-423">CLI</span><span class="sxs-lookup"><span data-stu-id="e14fe-423">CLI</span></span> | <span data-ttu-id="e14fe-424">Vea [Instalación de la CLI de Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e14fe-424">See [Azure command-line interface](../cli-install-nodejs.md).</span></span> |
| <span data-ttu-id="e14fe-425">DM-Crypt</span><span class="sxs-lookup"><span data-stu-id="e14fe-425">DM-Crypt</span></span> |<span data-ttu-id="e14fe-426">[DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) es subsistema de cifrado de disco basadas en Linux, transparente de Hola que ha utilizado el cifrado del disco tooenable en máquinas virtuales de IaaS de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-426">[DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) is hello Linux-based, transparent disk-encryption subsystem that's used tooenable disk encryption on Linux IaaS VMs.</span></span> |
| <span data-ttu-id="e14fe-427">KEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-427">KEK</span></span> | <span data-ttu-id="e14fe-428">Clave de cifrado de claves es Hola clave asimétrica (RSA 2048) que puede usar tooprotect o ajustar el secreto de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-428">Key encryption key is hello asymmetric key (RSA 2048) that you can use tooprotect or wrap hello secret.</span></span> <span data-ttu-id="e14fe-429">Se puede proporcionar una clave protegida mediante módulos de seguridad de hardware (HSM) o una clave protegida mediante software.</span><span class="sxs-lookup"><span data-stu-id="e14fe-429">You can provide a hardware security modules (HSM)-protected key or software-protected key.</span></span> <span data-ttu-id="e14fe-430">Para obtener más información, consulte la documentación de [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-430">For more details, see [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) documentation.</span></span> |
| <span data-ttu-id="e14fe-431">cmdlets de PS</span><span class="sxs-lookup"><span data-stu-id="e14fe-431">PS cmdlets</span></span> | <span data-ttu-id="e14fe-432">Consulte [Cmdlets de Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e14fe-432">See [Azure PowerShell cmdlets](/powershell/azure/overview).</span></span> |

### <a name="set-up-and-configure-your-key-vault-for-azure-disk-encryption"></a><span data-ttu-id="e14fe-433">Instalación y configuración del almacén de claves para Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="e14fe-433">Set up and configure your key vault for Azure Disk Encryption</span></span>
<span data-ttu-id="e14fe-434">Cifrado de disco de Azure le ayuda a claves de cifrado del disco de medida de seguridad hello y secretos en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-434">Azure Disk Encryption helps safeguard hello disk-encryption keys and secrets in your key vault.</span></span> <span data-ttu-id="e14fe-435">tooset de su almacén de claves de cifrado del disco de Azure, Hola completa los pasos en cada una de las siguientes secciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-435">tooset up your key vault for Azure Disk Encryption, complete hello steps in each of hello following sections.</span></span>

#### <a name="create-a-key-vault"></a><span data-ttu-id="e14fe-436">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e14fe-436">Create a key vault</span></span>
<span data-ttu-id="e14fe-437">toocreate un almacén de claves, use uno de hello siguientes opciones:</span><span class="sxs-lookup"><span data-stu-id="e14fe-437">toocreate a key vault, use one of hello following options:</span></span>

* [<span data-ttu-id="e14fe-438">Plantilla de Resource Manager llamada "101-Key-Vault-Create"</span><span class="sxs-lookup"><span data-stu-id="e14fe-438">"101-Key-Vault-Create" Resource Manager template</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-key-vault-create)
* [<span data-ttu-id="e14fe-439">Cmdlets de almacén de claves de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e14fe-439">Azure PowerShell key vault cmdlets</span></span>](/powershell/module/azurerm.keyvault/#key_vault)
* <span data-ttu-id="e14fe-440">Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-440">Azure Resource Manager</span></span>
* <span data-ttu-id="e14fe-441">Cómo demasiado[proteger el almacén de claves](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span><span class="sxs-lookup"><span data-stu-id="e14fe-441">How too[Secure your key vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-secure-your-key-vault)</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-442">Si ya ha configurado un almacén de claves de su suscripción, omitir toohello próxima sección.</span><span class="sxs-lookup"><span data-stu-id="e14fe-442">If you have already set up a key vault for your subscription, skip toohello next section.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig1.png)

#### <a name="set-up-a-key-encryption-key-optional"></a><span data-ttu-id="e14fe-444">Configuración de una clave de cifrado de claves (KEK) (opcional)</span><span class="sxs-lookup"><span data-stu-id="e14fe-444">Set up a key encryption key (optional)</span></span>
<span data-ttu-id="e14fe-445">Si desea toouse una KEK para una capa adicional de seguridad para las claves de cifrado de BitLocker de hello, agregar un almacén de claves de tooyour KEK.</span><span class="sxs-lookup"><span data-stu-id="e14fe-445">If you want toouse a KEK for an additional layer of security for hello BitLocker encryption keys, add a KEK tooyour key vault.</span></span> <span data-ttu-id="e14fe-446">Hola de uso [ `Add-AzureKeyVaultKey` ](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) toocreate cmdlet una clave de cifrado de claves en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-446">Use hello [`Add-AzureKeyVaultKey`](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet toocreate a key encryption key in hello key vault.</span></span> <span data-ttu-id="e14fe-447">También puede importar una KEK en el HSM de administración de claves local.</span><span class="sxs-lookup"><span data-stu-id="e14fe-447">You can also import a KEK from your on-premises key management HSM.</span></span> <span data-ttu-id="e14fe-448">Para obtener más información, consulte la [documentación de Key Vault](https://azure.microsoft.com/documentation/services/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-448">For more details, see [Key Vault Documentation](https://azure.microsoft.com/documentation/services/key-vault/).</span></span>

    Add-AzureKeyVaultKey [-VaultName] <string> [-Name] <string> -Destination <string> {HSM | Software}

<span data-ttu-id="e14fe-449">Puede agregar Hola KEK yendo tooAzure el Administrador de recursos o mediante la interfaz de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-449">You can add hello KEK by going tooAzure Resource Manager or by using your key vault interface.</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig2.png)

#### <a name="set-key-vault-permissions"></a><span data-ttu-id="e14fe-451">Configuración de los permisos del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e14fe-451">Set key vault permissions</span></span>
<span data-ttu-id="e14fe-452">Hello plataforma Windows Azure necesita claves de cifrado de acceso toohello o secretos en el almacén de claves toomake les toohello disponible de máquina virtual para arranque y descifrar los volúmenes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-452">hello Azure platform needs access toohello encryption keys or secrets in your key vault toomake them available toohello VM for booting and decrypting hello volumes.</span></span> <span data-ttu-id="e14fe-453">toogrant permisos toohello plataforma Windows Azure, conjunto hello **EnabledForDiskEncryption** del almacén de propiedad de clave de hello mediante cmdlet de PowerShell de almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-453">toogrant permissions toohello Azure platform, set hello **EnabledForDiskEncryption** property in hello key vault by using hello key vault PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName <yourVaultName> -ResourceGroupName <yourResourceGroup> -EnabledForDiskEncryption

<span data-ttu-id="e14fe-454">También puede establecer hello **EnabledForDiskEncryption** propiedad visitando hello [Explorador de recursos de Azure](https://resources.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e14fe-454">You can also set hello **EnabledForDiskEncryption** property by visiting hello [Azure Resource Explorer](https://resources.azure.com).</span></span>

<span data-ttu-id="e14fe-455">Como se mencionó anteriormente, debe establecer hello **EnabledForDiskEncryption** propiedad en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-455">As mentioned earlier, you must set hello **EnabledForDiskEncryption** property on your key vault.</span></span> <span data-ttu-id="e14fe-456">En caso contrario, se producirá un error de implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-456">Otherwise, hello deployment will fail.</span></span>

<span data-ttu-id="e14fe-457">Puede configurar directivas de acceso para la aplicación de Azure AD desde la interfaz del almacén de claves de hello, como se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="e14fe-457">You can set up access policies for your Azure AD application from hello key vault interface, as shown here:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3.png)

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig3b.png)

<span data-ttu-id="e14fe-460">En hello **las directivas de acceso avanzado** ficha, asegúrese de que el almacén de claves está habilitado para el cifrado de disco de Azure:</span><span class="sxs-lookup"><span data-stu-id="e14fe-460">On hello **Advanced access policies** tab, make sure that your key vault is enabled for Azure Disk Encryption:</span></span>

![Azure Key Vault](./media/azure-security-disk-encryption/keyvault-portal-fig4.png)

## <a name="disk-encryption-deployment-scenarios-and-user-experiences"></a><span data-ttu-id="e14fe-462">Escenarios de implementación del cifrado de disco y experiencias de usuario</span><span class="sxs-lookup"><span data-stu-id="e14fe-462">Disk-encryption deployment scenarios and user experiences</span></span>
<span data-ttu-id="e14fe-463">Puede habilitar muchos escenarios de cifrado del disco y pasos de hello pueden variar escenario de toohello correspondiente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-463">You can enable many disk-encryption scenarios, and hello steps may vary according toohello scenario.</span></span> <span data-ttu-id="e14fe-464">Hello las secciones siguientes tratan los escenarios de hello en mayor detalle.</span><span class="sxs-lookup"><span data-stu-id="e14fe-464">hello following sections cover hello scenarios in greater detail.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-hello-marketplace"></a><span data-ttu-id="e14fe-465">Habilitar el cifrado en nuevas máquinas virtuales de IaaS que se crean a partir de hello Marketplace</span><span class="sxs-lookup"><span data-stu-id="e14fe-465">Enable encryption on new IaaS VMs that are created from hello Marketplace</span></span>
<span data-ttu-id="e14fe-466">Puede habilitar el cifrado de disco en la nueva máquina virtual de Windows de IaaS de hello Marketplace en Azure mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span><span class="sxs-lookup"><span data-stu-id="e14fe-466">You can enable disk encryption on new IaaS Windows VM from hello Marketplace in Azure by using hello  [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image).</span></span>

1. <span data-ttu-id="e14fe-467">En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-467">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e14fe-468">Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en una nueva VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-468">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-469">Esta plantilla crea una nueva VM de Windows cifrados que usa la imagen de la Galería de hello Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="e14fe-469">This template creates a new encrypted Windows VM that uses hello Windows Server 2012 gallery image.</span></span>

<span data-ttu-id="e14fe-470">Puede habilitar el cifrado de disco en una nueva máquina virtual IaaS con RedHat Linux 7.2 con una matriz RAID-0 de 200 GB mediante esta [plantilla de Resource Manager](https://aka.ms/fde-rhel).</span><span class="sxs-lookup"><span data-stu-id="e14fe-470">You can enable disk encryption on a new IaaS RedHat Linux 7.2 VM with a 200-GB RAID-0 array by using this [Resource Manager template](https://aka.ms/fde-rhel).</span></span> <span data-ttu-id="e14fe-471">Después de implementar la plantilla de hello, comprobar el estado de cifrado de VM de hello mediante hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, tal y como se describe en [SO cifrado de unidad en una VM de Linux ejecución](#encrypting-os-drive-on-a-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="e14fe-471">After you deploy hello template, verify hello VM encryption status by using hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet, as described in [Encrypting OS drive on a running Linux VM](#encrypting-os-drive-on-a-running-linux-vm).</span></span> <span data-ttu-id="e14fe-472">Cuando la máquina de hello devuelve un estado de _VMRestartPending_, reinicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-472">When hello machine returns a status of _VMRestartPending_, restart hello VM.</span></span>

<span data-ttu-id="e14fe-473">Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos de Hola para nuevas máquinas virtuales de escenario de Marketplace de hello mediante identificador de cliente de Azure AD:</span><span class="sxs-lookup"><span data-stu-id="e14fe-473">hello following table lists hello Resource Manager template parameters for new VMs from hello Marketplace scenario using Azure AD client ID:</span></span>

| <span data-ttu-id="e14fe-474">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e14fe-474">Parameter</span></span> | <span data-ttu-id="e14fe-475">Descripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-475">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-476">adminUserName</span><span class="sxs-lookup"><span data-stu-id="e14fe-476">adminUserName</span></span> | <span data-ttu-id="e14fe-477">Nombre de usuario de administrador de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-477">Admin user name for hello virtual machine.</span></span> |
| <span data-ttu-id="e14fe-478">adminPassword</span><span class="sxs-lookup"><span data-stu-id="e14fe-478">adminPassword</span></span> | <span data-ttu-id="e14fe-479">Contraseña de usuario de administrador de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-479">Admin user password for hello virtual machine.</span></span> |
| <span data-ttu-id="e14fe-480">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e14fe-480">newStorageAccountName</span></span> | <span data-ttu-id="e14fe-481">Nombre de hello almacenamiento cuenta toostore sistema operativo y datos de discos duros virtuales.</span><span class="sxs-lookup"><span data-stu-id="e14fe-481">Name of hello storage account toostore OS and data VHDs.</span></span> |
| <span data-ttu-id="e14fe-482">vmSize</span><span class="sxs-lookup"><span data-stu-id="e14fe-482">vmSize</span></span> | <span data-ttu-id="e14fe-483">Tamaño del programa Hola a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-483">Size of hello VM.</span></span> <span data-ttu-id="e14fe-484">Actualmente, solo se admiten las series A, D y G estándar.</span><span class="sxs-lookup"><span data-stu-id="e14fe-484">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="e14fe-485">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="e14fe-485">virtualNetworkName</span></span> | <span data-ttu-id="e14fe-486">Nombre de red virtual que Hola VM NIC hello debe pertenecer a.</span><span class="sxs-lookup"><span data-stu-id="e14fe-486">Name of hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e14fe-487">subnetName</span><span class="sxs-lookup"><span data-stu-id="e14fe-487">subnetName</span></span> | <span data-ttu-id="e14fe-488">Nombre de subred de Hola Hola ese Hola VM NIC de red virtual debe pertenecer a.</span><span class="sxs-lookup"><span data-stu-id="e14fe-488">Name of hello subnet in hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e14fe-489">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e14fe-489">AADClientID</span></span> | <span data-ttu-id="e14fe-490">Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-490">Client ID of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e14fe-491">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e14fe-491">AADClientSecret</span></span> | <span data-ttu-id="e14fe-492">Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-492">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e14fe-493">keyVaultURL</span><span class="sxs-lookup"><span data-stu-id="e14fe-493">keyVaultURL</span></span> | <span data-ttu-id="e14fe-494">Dirección URL de clave de Hola del almacén que BitLocker se debe cargar la clave en hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-494">URL of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e14fe-495">Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-495">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -VaultName,-ResourceGroupName ).VaultURI`.</span></span> |
| <span data-ttu-id="e14fe-496">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e14fe-496">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e14fe-497">Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera claves de BitLocker (opcional).</span><span class="sxs-lookup"><span data-stu-id="e14fe-497">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key (optional).</span></span> |
| <span data-ttu-id="e14fe-498">keyVaultResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e14fe-498">keyVaultResourceGroup</span></span> | <span data-ttu-id="e14fe-499">Grupo de recursos de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-499">Resource group of hello key vault.</span></span> |
| <span data-ttu-id="e14fe-500">vmName</span><span class="sxs-lookup"><span data-stu-id="e14fe-500">vmName</span></span> | <span data-ttu-id="e14fe-501">Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-501">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="e14fe-502">_KeyEncryptionKeyURL_ es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="e14fe-502">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e14fe-503">Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (frase de contraseña secreta) en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-503">You can bring your own KEK toofurther safeguard hello data encryption key (Passphrase secret) in your key vault.</span></span>

### <a name="enable-encryption-on-new-iaas-vms-that-are-created-from-customer-encrypted-vhd-and-encryption-keys"></a><span data-ttu-id="e14fe-504">Habilitación del cifrado en nuevas máquinas virtuales IaaS creadas a partir del VHD cifrado del cliente y las claves de cifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-504">Enable encryption on new IaaS VMs that are created from customer-encrypted VHD and encryption keys</span></span>
<span data-ttu-id="e14fe-505">En este escenario, puede habilitar cifrado con la plantilla de administrador de recursos de hello, cmdlets de PowerShell o comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-505">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="e14fe-506">Hello las secciones siguientes se explican en la plantilla de administrador de recursos de mayor detalle hello y comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-506">hello following sections explain in greater detail hello Resource Manager template and CLI commands.</span></span>

<span data-ttu-id="e14fe-507">Siga las instrucciones de Hola de una de estas secciones para preparar imágenes previamente cifradas que se pueden usar en Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-507">Follow hello instructions from one of these sections for preparing pre-encrypted images that can be used in Azure.</span></span> <span data-ttu-id="e14fe-508">Después de crea la imagen de hello, puede utilizar pasos hello en la siguiente sección toocreate una VM de Azure cifrados de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-508">After hello image is created, you can use hello steps in hello next section toocreate an encrypted Azure VM.</span></span>

* [<span data-ttu-id="e14fe-509">Preparación de un VHD con Windows precifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-509">Prepare a pre-encrypted Windows VHD</span></span>](#preparing-a-pre-encrypted-windows-vhd)
* [<span data-ttu-id="e14fe-510">Preparación de un VHD con Linux precifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-510">Prepare a pre-encrypted Linux VHD</span></span>](#preparing-a-pre-encrypted-linux-vhd)

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="e14fe-511">Utilizando la plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-511">Using hello Resource Manager template</span></span>
<span data-ttu-id="e14fe-512">Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span><span class="sxs-lookup"><span data-stu-id="e14fe-512">You can enable disk encryption on your encrypted VHD by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-pre-encrypted-vm).</span></span>

1. <span data-ttu-id="e14fe-513">En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-513">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e14fe-514">Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en Hola nueva VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-514">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello new IaaS VM.</span></span>

<span data-ttu-id="e14fe-515">Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos de hello para el disco duro virtual cifrado:</span><span class="sxs-lookup"><span data-stu-id="e14fe-515">hello following table lists hello Resource Manager template parameters for your encrypted VHD:</span></span>

| <span data-ttu-id="e14fe-516">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e14fe-516">Parameter</span></span> | <span data-ttu-id="e14fe-517">Descripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-517">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-518">newStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="e14fe-518">newStorageAccountName</span></span> | <span data-ttu-id="e14fe-519">Nombre del programa Hola toostore de cuenta de almacenamiento de hello cifra VHD de sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-519">Name of hello storage account toostore hello encrypted OS VHD.</span></span> <span data-ttu-id="e14fe-520">Esta cuenta de almacenamiento debe ya se han creado en hello mismo grupo de recursos y la misma ubicación que Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-520">This storage account should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="e14fe-521">osVhdUri</span><span class="sxs-lookup"><span data-stu-id="e14fe-521">osVhdUri</span></span> | <span data-ttu-id="e14fe-522">URI de hello VHD de sistema operativo de la cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-522">URI of hello OS VHD from hello storage account.</span></span> |
| <span data-ttu-id="e14fe-523">osType</span><span class="sxs-lookup"><span data-stu-id="e14fe-523">osType</span></span> | <span data-ttu-id="e14fe-524">Tipo de producto de sistema operativo (Windows o Linux).</span><span class="sxs-lookup"><span data-stu-id="e14fe-524">OS product type (Windows/Linux).</span></span> |
| <span data-ttu-id="e14fe-525">virtualNetworkName</span><span class="sxs-lookup"><span data-stu-id="e14fe-525">virtualNetworkName</span></span> | <span data-ttu-id="e14fe-526">Nombre de red virtual que Hola VM NIC hello debe pertenecer a.</span><span class="sxs-lookup"><span data-stu-id="e14fe-526">Name of hello VNet that hello VM NIC should belong to.</span></span> <span data-ttu-id="e14fe-527">Hello nombre debe ya se han creado en hello mismo grupo de recursos y la misma ubicación que Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-527">hello name should already have been created in hello same resource group and same location as hello VM.</span></span> |
| <span data-ttu-id="e14fe-528">subnetName</span><span class="sxs-lookup"><span data-stu-id="e14fe-528">subnetName</span></span> | <span data-ttu-id="e14fe-529">Nombre de subred de hello en hello ese Hola VM NIC de red virtual debe pertenecer a.</span><span class="sxs-lookup"><span data-stu-id="e14fe-529">Name of hello subnet on hello VNet that hello VM NIC should belong to.</span></span> |
| <span data-ttu-id="e14fe-530">vmSize</span><span class="sxs-lookup"><span data-stu-id="e14fe-530">vmSize</span></span> | <span data-ttu-id="e14fe-531">Tamaño del programa Hola a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-531">Size of hello VM.</span></span> <span data-ttu-id="e14fe-532">Actualmente, solo se admiten las series A, D y G estándar.</span><span class="sxs-lookup"><span data-stu-id="e14fe-532">Currently, only Standard A, D, and G series are supported.</span></span> |
| <span data-ttu-id="e14fe-533">keyVaultResourceID</span><span class="sxs-lookup"><span data-stu-id="e14fe-533">keyVaultResourceID</span></span> | <span data-ttu-id="e14fe-534">Hola ResourceID que identifica el recurso de almacén de claves de hello en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-534">hello ResourceID that identifies hello key vault resource in Azure Resource Manager.</span></span> <span data-ttu-id="e14fe-535">Puede obtenerlo mediante el uso de cmdlet de PowerShell de hello `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-535">You can get it by using hello PowerShell cmdlet `(Get-AzureRmKeyVault -VaultName &lt;yourKeyVaultName&gt; -ResourceGroupName &lt;yourResourceGroupName&gt;).ResourceId`.</span></span> |
| <span data-ttu-id="e14fe-536">keyVaultSecretUrl</span><span class="sxs-lookup"><span data-stu-id="e14fe-536">keyVaultSecretUrl</span></span> | <span data-ttu-id="e14fe-537">Dirección URL de la clave de cifrado del disco de Hola que se puede establecer en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-537">URL of hello disk-encryption key that's set up in hello key vault.</span></span> |
| <span data-ttu-id="e14fe-538">keyVaultKekUrl</span><span class="sxs-lookup"><span data-stu-id="e14fe-538">keyVaultKekUrl</span></span> | <span data-ttu-id="e14fe-539">Dirección URL de la clave de cifrado de claves de Hola para cifrar la clave de cifrado del disco de hello generado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-539">URL of hello key encryption key for encrypting hello generated disk-encryption key.</span></span> |
| <span data-ttu-id="e14fe-540">vmName</span><span class="sxs-lookup"><span data-stu-id="e14fe-540">vmName</span></span> | <span data-ttu-id="e14fe-541">Nombre del programa Hola IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="e14fe-541">Name of hello IaaS VM.</span></span> |

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="e14fe-542">Uso de cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e14fe-542">Using PowerShell cmdlets</span></span>
<span data-ttu-id="e14fe-543">Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante cmdlet de PowerShell de hello [ `Set-AzureRmVMOSDisk` ](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span><span class="sxs-lookup"><span data-stu-id="e14fe-543">You can enable disk encryption on your encrypted VHD by using hello PowerShell cmdlet [`Set-AzureRmVMOSDisk`](/powershell/module/azurerm.compute/set-azurermvmosdisk).</span></span>  

#### <a name="using-cli-commands"></a><span data-ttu-id="e14fe-544">Uso de comandos de la CLI</span><span class="sxs-lookup"><span data-stu-id="e14fe-544">Using CLI commands</span></span>
<span data-ttu-id="e14fe-545">cifrado del disco tooenable para este escenario mediante comandos CLI, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-545">tooenable disk encryption for this scenario by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e14fe-546">Configure las directivas de acceso en el almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e14fe-546">Set access policies in your key vault:</span></span>

   * <span data-ttu-id="e14fe-547">Conjunto hello **EnabledForDiskEncryption** marca:</span><span class="sxs-lookup"><span data-stu-id="e14fe-547">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="e14fe-548">Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e14fe-548">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="e14fe-549">cifrado de tooenable en una máquina virtual existente o se está ejecutando, tipo:</span><span class="sxs-lookup"><span data-stu-id="e14fe-549">tooenable encryption on an existing or running VM, type:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="e14fe-550">Obtenga el estado de cifrado:</span><span class="sxs-lookup"><span data-stu-id="e14fe-550">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="e14fe-551">cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-551">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-existing-or-running-iaas-windows-vm-in-azure"></a><span data-ttu-id="e14fe-552">Habilitación del cifrado en una máquina virtual IaaS con Windows existente o en ejecución en Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-552">Enable encryption on existing or running IaaS Windows VM in Azure</span></span>
<span data-ttu-id="e14fe-553">En este escenario, puede habilitar cifrado con la plantilla de administrador de recursos de hello, cmdlets de PowerShell o comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-553">In this scenario, you can enable encrypting by using hello Resource Manager template, PowerShell cmdlets, or CLI commands.</span></span> <span data-ttu-id="e14fe-554">Hello las secciones siguientes se explican con más detalle cómo tooenable mediante Hola plantilla del Administrador de recursos y comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-554">hello following sections explain in greater detail how tooenable it by using hello Resource Manager template and CLI commands.</span></span>

#### <a name="using-hello-resource-manager-template"></a><span data-ttu-id="e14fe-555">Utilizando la plantilla de administrador de recursos de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-555">Using hello Resource Manager template</span></span>
<span data-ttu-id="e14fe-556">Puede habilitar el cifrado de disco en existente o ejecutar máquinas virtuales de Windows de IaaS en Azure con hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="e14fe-556">You can enable disk encryption on existing or running IaaS Windows VMs in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="e14fe-557">En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-557">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e14fe-558">Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en hello existente o ejecuta VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-558">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="e14fe-559">Hello siguiente tabla enumeran parámetros de plantilla de administrador de recursos de Hola para existente o máquinas virtuales que usan un identificador de cliente de Azure AD en ejecución:</span><span class="sxs-lookup"><span data-stu-id="e14fe-559">hello following table lists hello Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="e14fe-560">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e14fe-560">Parameter</span></span> | <span data-ttu-id="e14fe-561">Descripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-561">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-562">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e14fe-562">AADClientID</span></span> | <span data-ttu-id="e14fe-563">Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-563">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e14fe-564">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e14fe-564">AADClientSecret</span></span> | <span data-ttu-id="e14fe-565">Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-565">Client secret of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e14fe-566">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="e14fe-566">keyVaultName</span></span> | <span data-ttu-id="e14fe-567">Nombre de clave de hello almacén que BitLocker se debe cargar la clave en hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-567">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e14fe-568">Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-568">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="e14fe-569">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e14fe-569">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e14fe-570">Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera la clave de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-570">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="e14fe-571">Este parámetro es opcional si selecciona **nokek** en lista de hello UseExistingKek de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e14fe-571">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="e14fe-572">Si selecciona **kek** en la lista desplegable UseExistingKek hello, debe escribir hello _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="e14fe-572">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="e14fe-573">volumeType</span><span class="sxs-lookup"><span data-stu-id="e14fe-573">volumeType</span></span> | <span data-ttu-id="e14fe-574">Tipo de volumen que se realiza la operación de cifrado de hello en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-574">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="e14fe-575">Los valores válidos son _SO_, _Datos_ y _Todo_.</span><span class="sxs-lookup"><span data-stu-id="e14fe-575">Valid values are _OS_, _Data_, and _All_.</span></span> |
| <span data-ttu-id="e14fe-576">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e14fe-576">sequenceVersion</span></span> | <span data-ttu-id="e14fe-577">Versión de la secuencia de hello operación de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-577">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e14fe-578">Incrementar este número de versión cada vez que se realiza una operación de cifrado del disco en hello misma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-578">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="e14fe-579">vmName</span><span class="sxs-lookup"><span data-stu-id="e14fe-579">vmName</span></span> | <span data-ttu-id="e14fe-580">Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-580">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |

> [!NOTE]
> <span data-ttu-id="e14fe-581">_KeyEncryptionKeyURL_ es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="e14fe-581">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e14fe-582">Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (secreto de cifrado de BitLocker) en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-582">You can bring your own KEK toofurther safeguard hello data encryption key (BitLocker encryption secret) in hello key vault.</span></span>

#### <a name="using-powershell-cmdlets"></a><span data-ttu-id="e14fe-583">Uso de cmdlets de PowerShell</span><span class="sxs-lookup"><span data-stu-id="e14fe-583">Using PowerShell cmdlets</span></span>
<span data-ttu-id="e14fe-584">Para obtener información acerca de cómo habilitar el cifrado con cifrado de disco de Azure mediante el uso de cmdlets de PowerShell, vea las entradas de blog hello [explorar el cifrado del disco de Azure con PowerShell de Azure, parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) y [explorar cifrado del disco de Azure con Azure PowerShell, parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-584">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

#### <a name="using-cli-commands"></a><span data-ttu-id="e14fe-585">Uso de comandos de la CLI</span><span class="sxs-lookup"><span data-stu-id="e14fe-585">Using CLI commands</span></span>
<span data-ttu-id="e14fe-586">cifrado de tooenable en existente o ejecución de máquina virtual de Windows de IaaS de Azure mediante comandos de CLI, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-586">tooenable encryption on existing or running IaaS Windows VM in Azure using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e14fe-587">directivas de acceso de tooset en el almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-587">tooset access policies in hello key vault:</span></span>
   * <span data-ttu-id="e14fe-588">Conjunto hello **EnabledForDiskEncryption** marca:</span><span class="sxs-lookup"><span data-stu-id="e14fe-588">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
   * <span data-ttu-id="e14fe-589">Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e14fe-589">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`
2. <span data-ttu-id="e14fe-590">cifrado de tooenable en una máquina virtual existente o se está ejecutando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-590">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`
3. <span data-ttu-id="e14fe-591">estado de cifrado de tooget:</span><span class="sxs-lookup"><span data-stu-id="e14fe-591">tooget encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`
4. <span data-ttu-id="e14fe-592">cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-592">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>

 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="enable-encryption-on-an-existing-or-running-iaas-linux-vm-in-azure"></a><span data-ttu-id="e14fe-593">Habilitación del cifrado en una máquina virtual IaaS con Linux existente o en ejecución en Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-593">Enable encryption on an existing or running IaaS Linux VM in Azure</span></span>
<span data-ttu-id="e14fe-594">Puede habilitar el cifrado de disco en una VM de Linux IaaS existente o se está ejecutando en Azure mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span><span class="sxs-lookup"><span data-stu-id="e14fe-594">You can enable disk encryption on an existing or running IaaS Linux VM in Azure by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-running-linux-vm).</span></span>

1. <span data-ttu-id="e14fe-595">Haga clic en **implementar tooAzure** en la plantilla de hello inicio rápido de Azure, especifique la configuración de cifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-595">Click **Deploy tooAzure** on hello Azure quick-start template, enter hello encryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e14fe-596">Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en hello existente o ejecuta VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-596">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on hello existing or running IaaS VM.</span></span>

<span data-ttu-id="e14fe-597">Hello en la tabla siguiente enumera los parámetros de plantilla de administrador de recursos existente o máquinas virtuales que usan un identificador de cliente de Azure AD en ejecución:</span><span class="sxs-lookup"><span data-stu-id="e14fe-597">hello following table lists Resource Manager template parameters for existing or running VMs that use an Azure AD client ID:</span></span>

| <span data-ttu-id="e14fe-598">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e14fe-598">Parameter</span></span> | <span data-ttu-id="e14fe-599">Descripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-599">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-600">AADClientID</span><span class="sxs-lookup"><span data-stu-id="e14fe-600">AADClientID</span></span> | <span data-ttu-id="e14fe-601">Id. de cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos toohello el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-601">Client ID of hello Azure AD application that has permissions toowrite secrets toohello key vault.</span></span> |
| <span data-ttu-id="e14fe-602">AADClientSecret</span><span class="sxs-lookup"><span data-stu-id="e14fe-602">AADClientSecret</span></span> | <span data-ttu-id="e14fe-603">Secreto del cliente de aplicación de hello Azure AD que tenga permisos toowrite secretos tooyour el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-603">Client secret of hello Azure AD application that has permissions toowrite secrets tooyour key vault.</span></span> |
| <span data-ttu-id="e14fe-604">keyVaultName</span><span class="sxs-lookup"><span data-stu-id="e14fe-604">keyVaultName</span></span> | <span data-ttu-id="e14fe-605">Nombre de clave de hello almacén que BitLocker se debe cargar la clave en hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-605">Name of hello key vault that hello BitLocker key should be uploaded to.</span></span> <span data-ttu-id="e14fe-606">Puede obtenerlo mediante el cmdlet de hello `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-606">You can get it by using hello cmdlet `(Get-AzureRmKeyVault -ResourceGroupName <yourResourceGroupName>). Vaultname`.</span></span> |
|  <span data-ttu-id="e14fe-607">keyEncryptionKeyURL</span><span class="sxs-lookup"><span data-stu-id="e14fe-607">keyEncryptionKeyURL</span></span> | <span data-ttu-id="e14fe-608">Dirección URL de clave de cifrado de claves de Hola que es usado tooencrypt hello genera la clave de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-608">URL of hello key encryption key that's used tooencrypt hello generated BitLocker key.</span></span> <span data-ttu-id="e14fe-609">Este parámetro es opcional si selecciona **nokek** en lista de hello UseExistingKek de lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e14fe-609">This parameter is optional if you select **nokek** in hello UseExistingKek drop-down list.</span></span> <span data-ttu-id="e14fe-610">Si selecciona **kek** en la lista desplegable UseExistingKek hello, debe escribir hello _keyEncryptionKeyURL_ valor.</span><span class="sxs-lookup"><span data-stu-id="e14fe-610">If you select **kek** in hello UseExistingKek drop-down list, you must enter hello _keyEncryptionKeyURL_ value.</span></span> |
| <span data-ttu-id="e14fe-611">volumeType</span><span class="sxs-lookup"><span data-stu-id="e14fe-611">volumeType</span></span> | <span data-ttu-id="e14fe-612">Tipo de volumen que se realiza la operación de cifrado de hello en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-612">Type of volume that hello encryption operation is performed on.</span></span> <span data-ttu-id="e14fe-613">Los valores válidos admitidos son _SO_ o _All_ (para RHEL 7.2, CentOS 7.2 y Ubuntu 16.04) y _Data_ (para todas las otras distribuciones).</span><span class="sxs-lookup"><span data-stu-id="e14fe-613">Valid supported values are _OS_ or _All_ (for RHEL 7.2, CentOS 7.2, and Ubuntu 16.04), and _Data_ (for all other distributions).</span></span> |
| <span data-ttu-id="e14fe-614">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e14fe-614">sequenceVersion</span></span> | <span data-ttu-id="e14fe-615">Versión de la secuencia de hello operación de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-615">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e14fe-616">Incrementar este número de versión cada vez que se realiza una operación de cifrado del disco en hello misma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-616">Increment this version number every time a disk-encryption operation is performed on hello same VM.</span></span> |
| <span data-ttu-id="e14fe-617">vmName</span><span class="sxs-lookup"><span data-stu-id="e14fe-617">vmName</span></span> | <span data-ttu-id="e14fe-618">Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-618">Name of hello VM that hello encryption operation is toobe performed on.</span></span> |
| <span data-ttu-id="e14fe-619">passPhrase</span><span class="sxs-lookup"><span data-stu-id="e14fe-619">passPhrase</span></span> | <span data-ttu-id="e14fe-620">Escriba una frase de contraseña segura como clave de cifrado de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-620">Type a strong passphrase as hello data encryption key.</span></span> |

> [!NOTE]
> <span data-ttu-id="e14fe-621">_KeyEncryptionKeyURL_ es un parámetro opcional.</span><span class="sxs-lookup"><span data-stu-id="e14fe-621">_KeyEncryptionKeyURL_ is an optional parameter.</span></span> <span data-ttu-id="e14fe-622">Puede aportar tu propia clave de cifrado de KEK toofurther proteger Hola datos (frase de contraseña secreta) en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-622">You can bring your own KEK toofurther safeguard hello data encryption key (passphrase secret) in your key vault.</span></span>

#### <a name="cli-commands"></a><span data-ttu-id="e14fe-623">Comandos de la CLI</span><span class="sxs-lookup"><span data-stu-id="e14fe-623">CLI commands</span></span>
<span data-ttu-id="e14fe-624">Puede habilitar el cifrado de disco en el disco duro virtual cifrado mediante la instalación y uso de hello [comando de CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e14fe-624">You can enable disk encryption on your encrypted VHD by installing and using hello [CLI command](../cli-install-nodejs.md).</span></span> <span data-ttu-id="e14fe-625">cifrado de tooenable ejecutan las máquinas virtuales de Linux de IaaS en Azure mediante comandos CLI, o existente Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-625">tooenable encryption on existing or running IaaS Linux VMs in Azure by using CLI commands, do hello following:</span></span>

1. <span data-ttu-id="e14fe-626">Establecer directivas de acceso en el almacén de claves de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-626">Set access policies in hello key vault:</span></span>

 * <span data-ttu-id="e14fe-627">Conjunto hello **EnabledForDiskEncryption** marca:</span><span class="sxs-lookup"><span data-stu-id="e14fe-627">Set hello **EnabledForDiskEncryption** flag:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --enabled-for-disk-encryption true`
 * <span data-ttu-id="e14fe-628">Conjunto de permisos tooAzure AD aplicación toowrite secretos tooyour almacén de claves:</span><span class="sxs-lookup"><span data-stu-id="e14fe-628">Set permissions tooAzure AD application toowrite secrets tooyour key vault:</span></span>

    `azure keyvault set-policy --vault-name <keyVaultName> --spn <aadClientID> --perms-to-keys '["wrapKey"]' --perms-to-secrets '["set"]'`

2. <span data-ttu-id="e14fe-629">cifrado de tooenable en una máquina virtual existente o se está ejecutando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-629">tooenable encryption on an existing or running VM:</span></span>

 `azure vm enable-disk-encryption --resource-group <resourceGroupName> --name <vmName> --aad-client-id <aadClientId> --aad-client-secret <aadClientSecret> --disk-encryption-key-vault-url <keyVaultURL> --disk-encryption-key-vault-id <keyVaultResourceId> --volume-type [All|OS|Data]`

3. <span data-ttu-id="e14fe-630">Obtenga el estado de cifrado:</span><span class="sxs-lookup"><span data-stu-id="e14fe-630">Get encryption status:</span></span>

 `azure vm show-disk-encryption-status --resource-group <resourceGroupName> --name <vmName> --json`

4. <span data-ttu-id="e14fe-631">cifrado de tooenable en una nueva máquina virtual de un VHD cifrado, Hola utilice parámetros con hello siguientes `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-631">tooenable encryption on a new VM from your encrypted VHD, use hello following parameters with hello `azure vm create` command:</span></span>
 ```
   * disk-encryption-key-vault-id <disk-encryption-key-vault-id>
   * disk-encryption-key-url <disk-encryption-key-url>
   * key-encryption-key-vault-id <key-encryption-key-vault-id>
   * key-encryption-key-url <key-encryption-key-url>
 ```

### <a name="get-hello-encryption-status-of-an-encrypted-iaas-vm"></a><span data-ttu-id="e14fe-632">Obtener el estado de cifrado de Hola de una VM de IaaS cifrados</span><span class="sxs-lookup"><span data-stu-id="e14fe-632">Get hello encryption status of an encrypted IaaS VM</span></span>
<span data-ttu-id="e14fe-633">Puede obtener el estado de cifrado de hello mediante el Administrador de recursos de Azure, [cmdlets de PowerShell](/powershell/azure/overview), o comandos de CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-633">You can get hello encryption status by using Azure Resource Manager, [PowerShell cmdlets](/powershell/azure/overview), or CLI commands.</span></span> <span data-ttu-id="e14fe-634">Hola las secciones siguientes explica cómo toouse Hola portal de Azure clásico y tooget de comandos CLI Hola estado de cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-634">hello following sections explain how toouse hello Azure classic portal and CLI commands tooget hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-an-encrypted-windows-vm-by-using-azure-resource-manager"></a><span data-ttu-id="e14fe-635">Obtener estado de cifrado de Hola de una máquina virtual de Windows cifrados mediante el Administrador de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-635">Get hello encryption status of an encrypted Windows VM by using Azure Resource Manager</span></span>
<span data-ttu-id="e14fe-636">Puede obtener estado de cifrado de Hola de hello IaaS VM de Azure Resource Manager haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-636">You can get hello encryption status of hello IaaS VM from Azure Resource Manager by doing hello following:</span></span>

1. <span data-ttu-id="e14fe-637">Inicie sesión en toohello [portal de Azure clásico](https://portal.azure.com/)y, a continuación, haga clic en **máquinas virtuales** en el panel izquierdo de hello toosee una vista resumida de las máquinas virtuales de hello en su suscripción.</span><span class="sxs-lookup"><span data-stu-id="e14fe-637">Sign in toohello [Azure classic portal](https://portal.azure.com/), and then click **Virtual machines** in hello left pane toosee a summary view of hello virtual machines in your subscription.</span></span> <span data-ttu-id="e14fe-638">Puede filtrar la vista máquinas virtuales Hola seleccionando el nombre de la suscripción de Hola Hola **suscripción** lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="e14fe-638">You can filter hello virtual machines view by selecting hello subscription name in hello **Subscription** drop-down list.</span></span>

2. <span data-ttu-id="e14fe-639">En parte superior de Hola de hello **máquinas virtuales** página, haga clic en **columnas**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-639">At hello top of hello **Virtual machines** page, click **Columns**.</span></span>

3. <span data-ttu-id="e14fe-640">En hello **elegir columna** hoja, seleccione **cifrado del disco**y, a continuación, haga clic en **actualización**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-640">On hello **Choose column** blade, select **Disk Encryption**, and then click **Update**.</span></span> <span data-ttu-id="e14fe-641">Debería ver estado de cifrado de hello cifrado del disco columna mostrando hello _habilitado_ o _no habilitado_ para cada máquina virtual, como se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-641">You should see hello disk-encryption column showing hello encryption state _Enabled_ or _Not Enabled_ for each VM, as shown in hello following figure:</span></span>

 ![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig2.png)

#### <a name="get-hello-encryption-status-of-an-encrypted-windowslinux-iaas-vm-by-using-hello-disk-encryption-powershell-cmdlet"></a><span data-ttu-id="e14fe-643">Obtener el estado de cifrado de Hola de una VM de IaaS (Windows o Linux) cifrada mediante cmdlet de PowerShell de cifrado del disco de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-643">Get hello encryption status of an encrypted (Windows/Linux) IaaS VM by using hello disk-encryption PowerShell cmdlet</span></span>
<span data-ttu-id="e14fe-644">Puede obtener estado de cifrado de Hola de hello IaaS VM del cmdlet de PowerShell de cifrado del disco de hello `Get-AzureRmVMDiskEncryptionStatus`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-644">You can get hello encryption status of hello IaaS VM from hello disk-encryption PowerShell cmdlet `Get-AzureRmVMDiskEncryptionStatus`.</span></span> <span data-ttu-id="e14fe-645">configuración de cifrado de hello tooget para la máquina virtual, escriba la siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-645">tooget hello encryption settings for your VM, enter hello following:</span></span>

    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : NotEncrypted
    DataVolumesEncrypted       : Encrypted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a

<span data-ttu-id="e14fe-646">Puede inspeccionar la salida de hello de _AzureRmVMDiskEncryptionStatus Get_ para el cifrado de clave las direcciones URL.</span><span class="sxs-lookup"><span data-stu-id="e14fe-646">You can inspect hello output of _Get-AzureRmVMDiskEncryptionStatus_ for encryption key URLs.</span></span>

    C:\> $status = Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName
    e $VMName -ExtensionName $ExtensionName
    C:\> $status.OsVolumeEncryptionSettings

    DiskEncryptionKey                                                 KeyEncryptionKey                                               Enabled
    -----------------                                                 ----------------                                               -------
    Microsoft.Azure.Management.Compute.Models.KeyVaultSecretReference Microsoft.Azure.Management.Compute.Models.KeyVaultKeyReference    True


    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey.SecretUrl
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a
    C:\> $status.OsVolumeEncryptionSettings.DiskEncryptionKey

    SecretUrl                                                                                                               SourceVault
    ---------                                                                                                               -----------
    https://rheltest1keyvault.vault.azure.net/secrets/bdb6bfb1-5431-4c28-af46-b18d0025ef2a/abebacb83d864a5fa729508315020f8a Microsoft.Azure.Management....

<span data-ttu-id="e14fe-647">Hola OSVolumeEncrypted y valores de configuración de DataVolumesEncrypted se establecen too_Encrypted_, que muestra que los volúmenes se cifran mediante el cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-647">hello OSVolumeEncrypted and DataVolumesEncrypted settings values are set too_Encrypted_, which shows that both volumes are encrypted using Azure Disk Encryption.</span></span> <span data-ttu-id="e14fe-648">Para obtener información acerca de cómo habilitar el cifrado con cifrado de disco de Azure mediante el uso de cmdlets de PowerShell, vea las entradas de blog hello [explorar el cifrado del disco de Azure con PowerShell de Azure, parte 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) y [explorar cifrado del disco de Azure con Azure PowerShell, parte 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span><span class="sxs-lookup"><span data-stu-id="e14fe-648">For information about enabling encryption with Azure Disk Encryption by using PowerShell cmdlets, see hello blog posts [Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/17/explore-azure-disk-encryption-with-azure-powershell.aspx) and [Explore Azure Disk Encryption with Azure PowerShell - Part 2](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-649">En máquinas virtuales de Linux, toma tres minutos toofour hello `Get-AzureRmVMDiskEncryptionStatus` estado de cifrado de cmdlet tooreport Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-649">On Linux VMs, it takes three toofour minutes for hello `Get-AzureRmVMDiskEncryptionStatus` cmdlet tooreport hello encryption status.</span></span>

#### <a name="get-hello-encryption-status-of-hello-iaas-vm-from-hello-disk-encryption-cli-command"></a><span data-ttu-id="e14fe-650">Obtener el estado de cifrado de Hola de hello IaaS VM de comando de CLI de cifrado del disco de Hola</span><span class="sxs-lookup"><span data-stu-id="e14fe-650">Get hello encryption status of hello IaaS VM from hello disk-encryption CLI command</span></span>
<span data-ttu-id="e14fe-651">Puede obtener estado de cifrado de Hola de hello IaaS VM mediante el uso de comandos CLI de cifrado del disco hello `azure vm show-disk-encryption-status`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-651">You can get hello encryption status of hello IaaS VM by using hello disk-encryption CLI command `azure vm show-disk-encryption-status`.</span></span> <span data-ttu-id="e14fe-652">configuración de cifrado de hello tooget para la máquina virtual, escriba la sesión de CLI de Azure:</span><span class="sxs-lookup"><span data-stu-id="e14fe-652">tooget hello encryption settings for your VM, enter your Azure CLI session:</span></span>

    azure vm show-disk-encryption-status --resource-group <yourResourceGroupName> --name <yourVMName> --json  

#### <a name="disable-encryption-on-running-windows-iaas-vm"></a><span data-ttu-id="e14fe-653">Deshabilitación del cifrado en máquinas virtuales IaaS con Windows en ejecución</span><span class="sxs-lookup"><span data-stu-id="e14fe-653">Disable encryption on running Windows IaaS VM</span></span>
<span data-ttu-id="e14fe-654">Puede deshabilitar el cifrado en una ejecución de Windows o Linux VM de IaaS a través de la plantilla de administrador de recursos de cifrado de disco de Azure de Hola o los cmdlets de PowerShell y especificar la configuración de descifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-654">You can disable encryption on a running Windows or Linux IaaS VM via hello Azure Disk Encryption Resource Manager template or PowerShell cmdlets and specify hello decryption configuration.</span></span>

##### <a name="windows-vm"></a><span data-ttu-id="e14fe-655">Máquina virtual de Windows</span><span class="sxs-lookup"><span data-stu-id="e14fe-655">Windows VM</span></span>
<span data-ttu-id="e14fe-656">paso de deshabilitar cifrado de Hello deshabilita el cifrado de hello SO, volumen de datos de Hola o ambos en hello ejecutando la máquina virtual de IaaS de Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-656">hello disable-encryption step disables encryption of hello OS, hello data volume, or both on hello running Windows IaaS VM.</span></span> <span data-ttu-id="e14fe-657">No se puede deshabilitar el volumen del sistema operativo de Hola y dejar cifradas de volumen de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-657">You cannot disable hello OS volume and leave hello data volume encrypted.</span></span> <span data-ttu-id="e14fe-658">Cuando se realiza el paso de cifrado de la deshabilitación de hello, modelo de implementación clásica Azure Hola actualiza el modelo de servicio VM de Hola y Hola VM de IaaS de Windows se marca descifrada.</span><span class="sxs-lookup"><span data-stu-id="e14fe-658">When hello disable-encryption step is performed, hello Azure classic deployment model updates hello VM service model, and hello Windows IaaS VM is marked decrypted.</span></span> <span data-ttu-id="e14fe-659">contenido de Hola de hello VM ya no se cifra en reposo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-659">hello contents of hello VM are no longer encrypted at rest.</span></span> <span data-ttu-id="e14fe-660">descifrado de Hello no elimina la clave hello y el almacén de claves de cifrado (claves de cifrado de BitLocker para Windows y la frase de contraseña de Linux).</span><span class="sxs-lookup"><span data-stu-id="e14fe-660">hello decryption does not delete your key vault and hello encryption key material (BitLocker encryption keys for Windows and Passphrase for Linux).</span></span>

##### <a name="linux-vm"></a><span data-ttu-id="e14fe-661">Máquina virtual de Linux</span><span class="sxs-lookup"><span data-stu-id="e14fe-661">Linux VM</span></span>
<span data-ttu-id="e14fe-662">paso de deshabilitar cifrado de Hello deshabilita el cifrado del volumen de datos de hello en hello ejecutando la máquina virtual de IaaS de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-662">hello disable-encryption step disables encryption of hello data volume on hello running Linux IaaS VM.</span></span> <span data-ttu-id="e14fe-663">Este paso solo funciona si el disco del sistema operativo de hello no está cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-663">This step only works if hello OS disk is not encrypted.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-664">No se permite deshabilitar el cifrado en el disco del sistema operativo de hello en máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-664">Disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span>

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="e14fe-665">Deshabilitado del cifrado en una máquina virtual IaaS existente o en ejecución</span><span class="sxs-lookup"><span data-stu-id="e14fe-665">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="e14fe-666">Puede deshabilitar el cifrado de disco en la ejecución de máquinas virtuales de IaaS de Windows mediante el uso de hello [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span><span class="sxs-lookup"><span data-stu-id="e14fe-666">You can disable disk encryption on running Windows IaaS VMs by using hello [Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-decrypt-running-windows-vm).</span></span>

1. <span data-ttu-id="e14fe-667">En la plantilla de hello Azure inicio rápido, haga clic en **implementar tooAzure**, escriba configuración de descifrado de hello en hello **parámetros** hoja y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-667">On hello Azure quick-start template, click **Deploy tooAzure**, enter hello decryption configuration on hello **Parameters** blade, and then click **OK**.</span></span>

2. <span data-ttu-id="e14fe-668">Seleccione la suscripción hello, grupo de recursos, ubicación del grupo de recursos, los términos legales y contrato y, a continuación, haga clic en **crear** tooenable cifrado en una nueva VM de IaaS.</span><span class="sxs-lookup"><span data-stu-id="e14fe-668">Select hello subscription, resource group, resource group location, legal terms, and agreement, and then click **Create** tooenable encryption on a new IaaS VM.</span></span>

<span data-ttu-id="e14fe-669">Para máquinas virtuales de Linux, puede deshabilitar el cifrado mediante el uso de hello [deshabilitar el cifrado en una VM de Linux ejecución](https://aka.ms/decrypt-linuxvm) plantilla.</span><span class="sxs-lookup"><span data-stu-id="e14fe-669">For Linux VMs, you can disable encryption by using hello [Disable encryption on a running Linux VM](https://aka.ms/decrypt-linuxvm) template.</span></span>

<span data-ttu-id="e14fe-670">Hello tabla siguiente enumeran los parámetros de plantilla de administrador de recursos para deshabilitar el cifrado en una VM IaaS en ejecución:</span><span class="sxs-lookup"><span data-stu-id="e14fe-670">hello following table lists Resource Manager template parameters for disabling encryption on a running IaaS VM:</span></span>

| <span data-ttu-id="e14fe-671">Parámetro</span><span class="sxs-lookup"><span data-stu-id="e14fe-671">Parameter</span></span> | <span data-ttu-id="e14fe-672">Descripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-672">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e14fe-673">vmName</span><span class="sxs-lookup"><span data-stu-id="e14fe-673">vmName</span></span> | <span data-ttu-id="e14fe-674">Nombre de máquina virtual que Hola operación de cifrado de hello es toobe realizada en.</span><span class="sxs-lookup"><span data-stu-id="e14fe-674">Name of hello VM that hello encryption operation is toobe performed on.</span></span>
| <span data-ttu-id="e14fe-675">volumeType</span><span class="sxs-lookup"><span data-stu-id="e14fe-675">volumeType</span></span> | <span data-ttu-id="e14fe-676">Tipo de volumen en que se realiza la operación de descifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-676">Type of volume that a decryption operation is performed on.</span></span> <span data-ttu-id="e14fe-677">Los valores válidos son _SO_, _Datos_ y _Todo_.</span><span class="sxs-lookup"><span data-stu-id="e14fe-677">Valid values are _OS_, _Data_, and _All_.</span></span> <span data-ttu-id="e14fe-678">No se puede deshabilitar el cifrado en la ejecución de volumen de arranque del SO/máquina virtual de IaaS de Windows sin necesidad de deshabilitar el cifrado en hello _datos_ volumen.</span><span class="sxs-lookup"><span data-stu-id="e14fe-678">You cannot disable encryption on running Windows IaaS VM OS/boot volume without disabling encryption on hello _Data_ volume.</span></span> <span data-ttu-id="e14fe-679">Tenga en cuenta también que la deshabilitación del cifrado en el disco del sistema operativo de hello no se permite en máquinas virtuales de Linux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-679">Also note that disabling encryption on hello OS disk is not allowed on Linux VMs.</span></span> |
| <span data-ttu-id="e14fe-680">sequenceVersion</span><span class="sxs-lookup"><span data-stu-id="e14fe-680">sequenceVersion</span></span> | <span data-ttu-id="e14fe-681">Versión de la secuencia de hello operación de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-681">Sequence version of hello BitLocker operation.</span></span> <span data-ttu-id="e14fe-682">Incrementar este número de versión cada vez que se realiza una operación de descifrado de disco en hello misma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-682">Increment this version number every time a disk decryption operation is performed on hello same VM.</span></span> |

##### <a name="disable-encryption-on-an-existing-or-running-iaas-vm"></a><span data-ttu-id="e14fe-683">Deshabilitado del cifrado en una máquina virtual IaaS existente o en ejecución</span><span class="sxs-lookup"><span data-stu-id="e14fe-683">Disable encryption on an existing or running IaaS VM</span></span>
<span data-ttu-id="e14fe-684">cifrado de toodisable en una VM de IaaS existente o se está ejecutando mediante Hola cmdlet de PowerShell, consulte [ `Disable-AzureRmVMDiskEncryption` ](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span><span class="sxs-lookup"><span data-stu-id="e14fe-684">toodisable encryption on an existing or running IaaS VM by using hello PowerShell cmdlet, see [`Disable-AzureRmVMDiskEncryption`](/powershell/module/azurerm.compute/disable-azurermvmdiskencryption).</span></span> <span data-ttu-id="e14fe-685">Este cmdlet admite máquinas virtuales Linux y Windows.</span><span class="sxs-lookup"><span data-stu-id="e14fe-685">This cmdlet supports both Windows and Linux VMs.</span></span> <span data-ttu-id="e14fe-686">cifrado de toodisable, instala una extensión en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-686">toodisable encryption, it installs an extension on hello virtual machine.</span></span> <span data-ttu-id="e14fe-687">Si hello _nombre_ no se especifica el parámetro, una extensión con el nombre predeterminado de hello _AzureDiskEncryption para máquinas virtuales de Windows_ se crea.</span><span class="sxs-lookup"><span data-stu-id="e14fe-687">If hello _Name_ parameter is not specified, an extension with hello default name _AzureDiskEncryption for Windows VMs_ is created.</span></span>

<span data-ttu-id="e14fe-688">En las máquinas virtuales de Linux, se utiliza hello AzureDiskEncryptionForLinux extensión.</span><span class="sxs-lookup"><span data-stu-id="e14fe-688">On Linux VMs, hello AzureDiskEncryptionForLinux extension is used.</span></span>

> [!NOTE]
> <span data-ttu-id="e14fe-689">Este cmdlet reinicia la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-689">This cmdlet reboots hello virtual machine.</span></span>

### <a name="enable-encryption-on-pre-encrypted-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e14fe-690">Habilitar el cifrado en máquinas virtuales IaaS precifradas con el disco administrado de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-690">Enable encryption on pre-encrypted IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="e14fe-691">Usar hello Azure BRAZO del disco administrado plantilla toocreate una VM cifrada desde un disco duro virtual cifrado previamente con la plantilla de hello ARM se encuentra en</span><span class="sxs-lookup"><span data-stu-id="e14fe-691">Use hello Azure Managed Disk ARM template toocreate a encrypted VM from a pre-encrypted VHD using hello ARM template located at</span></span>   
<span data-ttu-id="e14fe-692">[Crear un nuevo disco administrado cifrado desde un VHD cifrado previamente/blob de almacenamiento] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span><span class="sxs-lookup"><span data-stu-id="e14fe-692">[Create a new encrypted managed disk from a pre-encrypted VHD/storage blob] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-create-encrypted-managed-disk)</span></span>

### <a name="enable-encryption-on-a-new-linux-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e14fe-693">Habilitar el cifrado en máquinas virtuales IaaS nuevas de Linux con el disco administrado de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-693">Enable encryption on a new Linux IaaS VM with Azure Managed Disk</span></span>
<span data-ttu-id="e14fe-694">Usar hello Azure BRAZO del disco administrado plantilla toocreate en que cifra una nueva máquina virtual de IaaS de Linux con plantilla de ARM Hola ubicado</span><span class="sxs-lookup"><span data-stu-id="e14fe-694">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
<span data-ttu-id="e14fe-695">[Implementación de RHEL 7.2 con cifrado de disco completo] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span><span class="sxs-lookup"><span data-stu-id="e14fe-695">[Deployment of RHEL 7.2 with full disk encryption] (https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-full-disk-encrypted-rhel)</span></span>

### <a name="enable-encryption-on-a-new-windows-iaas-vm-with-azure-managed-disk"></a><span data-ttu-id="e14fe-696">Habilitar el cifrado en máquinas virtuales IaaS nuevas de Windows con el disco administrado de Azure</span><span class="sxs-lookup"><span data-stu-id="e14fe-696">Enable encryption on a new Windows IaaS VM with Azure Managed Disk</span></span>
 <span data-ttu-id="e14fe-697">Usar hello Azure BRAZO del disco administrado plantilla toocreate en que cifra una nueva máquina virtual de IaaS de Linux con plantilla de ARM Hola ubicado</span><span class="sxs-lookup"><span data-stu-id="e14fe-697">Use hello Azure Managed Disk ARM template toocreate a new encrypted Linux IaaS VM using hello ARM template located at</span></span>   
 <span data-ttu-id="e14fe-698">[Crear una máquina virtual IaaS de disco administrado cifrado de Windows nueva a partir de una imagen de la galería] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span><span class="sxs-lookup"><span data-stu-id="e14fe-698">[Create a new encrypted Windows IaaS Managed Disk VM from gallery image] (https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image-managed-disks)</span></span>

  > [!NOTE]
  ><span data-ttu-id="e14fe-699">Es obligatorio toosnapshot y/o copia de seguridad un administrado basadas en disco instancia de máquina virtual fuera de y tooenabling anterior cifrado del disco de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-699">It is mandatory toosnapshot and/or backup a managed disk based VM instance outside of and prior tooenabling Azure Disk Encryption.</span></span>  <span data-ttu-id="e14fe-700">Puede tomar una instantánea de disco administrado Hola desde el portal de Hola o copia de seguridad de Azure puede utilizarse.</span><span class="sxs-lookup"><span data-stu-id="e14fe-700">A snapshot of hello managed disk can be taken from hello portal, or Azure Backup can be used.</span></span>  <span data-ttu-id="e14fe-701">Las copias de seguridad Asegúrese de que una opción de recuperación es posible en caso de hello de cualquier error inesperado durante el cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-701">Backups ensure that a recovery option is possible in hello case of any unexpected failure during encryption.</span></span>  <span data-ttu-id="e14fe-702">Una vez que se realiza una copia de seguridad, cmdlet hello AzureRmVMDiskEncryptionExtension conjunto puede ser usado tooencrypt administrado discos especificando el parámetro - skipVmBackup de hello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-702">Once a backup is made, hello Set-AzureRmVMDiskEncryptionExtension cmdlet can be used tooencrypt managed disks by specifying hello -skipVmBackup parameter.</span></span>  <span data-ttu-id="e14fe-703">Este comando producirá un error en las máquinas virtuales basadas en un disco administrado hasta que se realice una copia de seguridad y se especifique este parámetro.</span><span class="sxs-lookup"><span data-stu-id="e14fe-703">This command will fail against managed disk based VM's until a backup has been made and this parameter has been specified.</span></span>    
 
### <a name="update-encryption-settings-of-an-existing-encrypted-non-premium-vm"></a><span data-ttu-id="e14fe-704">Actualización de la configuración del cifrado de una máquina virtual cifrada no premium existente</span><span class="sxs-lookup"><span data-stu-id="e14fe-704">Update encryption settings of an existing encrypted non-premium VM</span></span>
  <span data-ttu-id="e14fe-705">Use Hola disco de Azure admitido el cifrado las interfaces existentes para ejecutar máquinas virtuales [cmdlets de PS, plantillas CLI o ARM] tooupdate configuración de cifrado de hello como cliente AAD/secreto, del identificador de clave de cifrado de clave [KEK], clave de cifrado de BitLocker para la máquina virtual de Windows o la frase de contraseña para Configuración de cifrado de actualización de Linux VM etc. Hola solo se admite para las máquinas virtuales respaldadas por el almacenamiento no son premium.</span><span class="sxs-lookup"><span data-stu-id="e14fe-705">Use hello existing Azure disk encryption supported interfaces for running VM [PS cmdlets, CLI or ARM templates] tooupdate hello encryption settings like AAD client ID/secret, Key encryption key [KEK], BitLocker encryption key for Windows VM or Passphrase for Linux VM etc. hello update encryption setting is supported only for VMs backed by non-premium storage.</span></span> <span data-ttu-id="e14fe-706">NO está admitido para máquinas virtuales respaldadas por Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="e14fe-706">It is NNOT supported for VMs backed by premium storage.</span></span>

## <a name="appendix"></a><span data-ttu-id="e14fe-707">Anexo</span><span class="sxs-lookup"><span data-stu-id="e14fe-707">Appendix</span></span>
### <a name="connect-tooyour-subscription"></a><span data-ttu-id="e14fe-708">Conectar tooyour suscripción</span><span class="sxs-lookup"><span data-stu-id="e14fe-708">Connect tooyour subscription</span></span>
<span data-ttu-id="e14fe-709">Antes de continuar, revise hello *requisitos previos* sección en este artículo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-709">Before you proceed, review hello *Prerequisites* section in this article.</span></span> <span data-ttu-id="e14fe-710">Después de asegurarse de que se cumplen todos los requisitos previos, conecte tooyour suscripción haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-710">After you ensure that all prerequisites have been met, connect tooyour subscription by doing hello following:</span></span>

1. <span data-ttu-id="e14fe-711">Iniciar una sesión de PowerShell de Azure e inicie sesión tooyour cuenta de Azure con hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-711">Start an Azure PowerShell session, and sign in tooyour Azure account with hello following command:</span></span>

    `Login-AzureRmAccount`

2. <span data-ttu-id="e14fe-712">Si tiene varias suscripciones y desea toospecify una toouse, escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:</span><span class="sxs-lookup"><span data-stu-id="e14fe-712">If you have multiple subscriptions and want toospecify one toouse, type hello following toosee hello subscriptions for your account:</span></span>

    `Get-AzureRmSubscription`

3. <span data-ttu-id="e14fe-713">suscripción de hello toospecify desea toouse, tipo:</span><span class="sxs-lookup"><span data-stu-id="e14fe-713">toospecify hello subscription you want toouse, type:</span></span>

    `Select-AzureRmSubscription -SubscriptionName <Yoursubscriptionname>`

4. <span data-ttu-id="e14fe-714">tooverify que suscripción Hola configurada es correcta, escriba:</span><span class="sxs-lookup"><span data-stu-id="e14fe-714">tooverify that hello subscription configured is correct, type:</span></span>

    `Get-AzureRmSubscription`

5. <span data-ttu-id="e14fe-715">Hola tooconfirm cifrado de disco de Azure se instalan cmdlets, tipo:</span><span class="sxs-lookup"><span data-stu-id="e14fe-715">tooconfirm hello Azure Disk Encryption cmdlets are installed, type:</span></span>

    `Get-command *diskencryption*`

6. <span data-ttu-id="e14fe-716">Hola después de salida confirma la instalación de PowerShell de cifrado de disco de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-716">hello following output confirms hello Azure Disk Encryption PowerShell installation:</span></span>

```
    PS C:\Windows\System32\WindowsPowerShell\v1.0> get-command *diskencryption*
    CommandType  Name                                         Source                                                             
    Cmdlet       Get-AzureRmVMDiskEncryptionStatus            AzureRM.Compute                                                    
    Cmdlet       Disable-AzureRmVMDiskEncryption              AzureRM.Compute                                                    
    Cmdlet       Set-AzureRmVMDiskEncryptionExtension         AzureRM.Compute                                                     
```

### <a name="prepare-a-pre-encrypted-windows-vhd"></a><span data-ttu-id="e14fe-717">Preparación de un VHD con Windows precifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-717">Prepare a pre-encrypted Windows VHD</span></span>
<span data-ttu-id="e14fe-718">secciones Hola siguientes son necesario tooprepare un cifrado previamente VHD de Windows para la implementación como un disco duro virtual cifrado en IaaS de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-718">hello sections that follow are necessary tooprepare a pre-encrypted Windows VHD for deployment as an encrypted VHD in Azure IaaS.</span></span> <span data-ttu-id="e14fe-719">Utilice Hola información tooprepare y arrancar una máquina virtual de Windows nueva (VHD) en Azure Site Recovery o Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-719">Use hello information tooprepare and boot a fresh Windows VM (VHD) on Azure Site Recovery or Azure.</span></span>

#### <a name="update-group-policy-tooallow-non-tpm-for-os-protection"></a><span data-ttu-id="e14fe-720">Actualizar grupo Directiva tooallow sin TPM para la protección del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e14fe-720">Update group policy tooallow non-TPM for OS protection</span></span>
<span data-ttu-id="e14fe-721">Configuración de directiva de grupo de BitLocker de hello **cifrado de unidad BitLocker**, que encontrará en **directiva de equipo Local** > **configuración del equipo**  >  **Plantillas administrativas** > **componentes de Windows**.</span><span class="sxs-lookup"><span data-stu-id="e14fe-721">Configure hello BitLocker Group Policy setting **BitLocker Drive Encryption**, which you'll find under **Local Computer Policy** > **Computer Configuration** > **Administrative Templates** > **Windows Components**.</span></span> <span data-ttu-id="e14fe-722">Cambiar esta configuración demasiado**unidades de sistema operativo** > **requerir autenticación adicional al iniciar** > **Permitir BitLocker sin un TPM compatible**, tal y como se muestra en hello figura siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-722">Change this setting too**Operating System Drives** > **Require additional authentication at startup** > **Allow BitLocker without a compatible TPM**, as shown in hello following figure:</span></span>

![Microsoft Antimalware en Azure](./media/azure-security-disk-encryption/disk-encryption-fig8.png)

#### <a name="install-bitlocker-feature-components"></a><span data-ttu-id="e14fe-724">Instalación de componentes de características de BitLocker</span><span class="sxs-lookup"><span data-stu-id="e14fe-724">Install BitLocker feature components</span></span>
<span data-ttu-id="e14fe-725">Para Windows Server 2012 y versiones posteriores, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-725">For Windows Server 2012 and later, use hello following command:</span></span>

    dism /online /Enable-Feature /all /FeatureName:BitLocker /quiet /norestart

<span data-ttu-id="e14fe-726">Para Windows Server 2008 R2, utilice Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="e14fe-726">For Windows Server 2008 R2, use hello following command:</span></span>

    ServerManagerCmd -install BitLockers

#### <a name="prepare-hello-os-volume-for-bitlocker-by-using-bdehdcfg"></a><span data-ttu-id="e14fe-727">Prepare el volumen del sistema operativo de Hola para BitLocker mediante el`bdehdcfg`</span><span class="sxs-lookup"><span data-stu-id="e14fe-727">Prepare hello OS volume for BitLocker by using `bdehdcfg`</span></span>
<span data-ttu-id="e14fe-728">toocompress Hola partición del sistema operativo y preparar la máquina de Hola para BitLocker, ejecute el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="e14fe-728">toocompress hello OS partition and prepare hello machine for BitLocker, execute hello following command:</span></span>

    bdehdcfg -target c: shrink -quiet

#### <a name="protect-hello-os-volume-by-using-bitlocker"></a><span data-ttu-id="e14fe-729">Proteger el volumen del sistema operativo hello mediante el uso de BitLocker</span><span class="sxs-lookup"><span data-stu-id="e14fe-729">Protect hello OS volume by using BitLocker</span></span>
<span data-ttu-id="e14fe-730">Hola de uso [ `manage-bde` ](https://technet.microsoft.com/library/ff829849.aspx) cifrado de tooenable de comando en el volumen de arranque de hello mediante un protector de clave externo.</span><span class="sxs-lookup"><span data-stu-id="e14fe-730">Use hello [`manage-bde`](https://technet.microsoft.com/library/ff829849.aspx) command tooenable encryption on hello boot volume using an external key protector.</span></span> <span data-ttu-id="e14fe-731">Colocar la clave externa de hello (archivo .bek) en unidad externa de Hola o volumen.</span><span class="sxs-lookup"><span data-stu-id="e14fe-731">Also place hello external key (.bek file) on hello external drive or volume.</span></span> <span data-ttu-id="e14fe-732">Cifrado está habilitado en el volumen de arranque o de sistema de hello después del reinicio siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-732">Encryption is enabled on hello system/boot volume after hello next reboot.</span></span>

    manage-bde -on %systemdrive% -sk [ExternalDriveOrVolume]
    reboot

> [!NOTE]
> <span data-ttu-id="e14fe-733">Preparar Hola VM con datos o recursos independientes VHD para obtener la clave externa de hello mediante BitLocker.</span><span class="sxs-lookup"><span data-stu-id="e14fe-733">Prepare hello VM with a separate data/resource VHD for getting hello external key by using BitLocker.</span></span>

#### <a name="encrypting-an-os-drive-on-a-running-linux-vm"></a><span data-ttu-id="e14fe-734">Cifrado de la unidad del sistema operativo en una máquina virtual con Linux en ejecución</span><span class="sxs-lookup"><span data-stu-id="e14fe-734">Encrypting an OS drive on a running Linux VM</span></span>
<span data-ttu-id="e14fe-735">Cifrado de una unidad de sistema operativo en una ejecución VM de Linux es compatible con hello siguientes distribuciones:</span><span class="sxs-lookup"><span data-stu-id="e14fe-735">Encryption of an OS drive on a running Linux VM is supported on hello following distributions:</span></span>

* <span data-ttu-id="e14fe-736">RHEL 7.2</span><span class="sxs-lookup"><span data-stu-id="e14fe-736">RHEL 7.2</span></span>
* <span data-ttu-id="e14fe-737">CentOS 7.2</span><span class="sxs-lookup"><span data-stu-id="e14fe-737">CentOS 7.2</span></span>
* <span data-ttu-id="e14fe-738">Ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e14fe-738">Ubuntu 16.04</span></span>

##### <a name="prerequisites-for-os-disk-encryption"></a><span data-ttu-id="e14fe-739">Requisitos previos para el cifrado de disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e14fe-739">Prerequisites for OS disk encryption</span></span>

* <span data-ttu-id="e14fe-740">Hola VM se debe crear desde una imagen de Marketplace hello en el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-740">hello VM must be created from hello Marketplace image in Azure Resource Manager.</span></span>
* <span data-ttu-id="e14fe-741">La máquina virtual de Azure con al menos 4 GB de RAM (el tamaño recomendado es 7 GB).</span><span class="sxs-lookup"><span data-stu-id="e14fe-741">Azure VM with at least 4 GB of RAM (recommended size is 7 GB).</span></span>
* <span data-ttu-id="e14fe-742">(Para RHEL y CentOS) Deshabilite SELinux.</span><span class="sxs-lookup"><span data-stu-id="e14fe-742">(For RHEL and CentOS) Disable SELinux.</span></span> <span data-ttu-id="e14fe-743">toodisable SELinux, vea "4.4.2.</span><span class="sxs-lookup"><span data-stu-id="e14fe-743">toodisable SELinux, see "4.4.2.</span></span> <span data-ttu-id="e14fe-744">Deshabilitar SELinux"Hola [Guía del administrador y del usuario de SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-744">Disabling SELinux" in hello [SELinux User's and Administrator's Guide](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/sect-Security-Enhanced_Linux-Working_with_SELinux-Changing_SELinux_Modes.html#sect-Security-Enhanced_Linux-Enabling_and_Disabling_SELinux-Disabling_SELinux) on hello VM.</span></span>
* <span data-ttu-id="e14fe-745">Después de deshabilitar SELinux, reinicie Hola VM al menos una vez.</span><span class="sxs-lookup"><span data-stu-id="e14fe-745">After you disable SELinux, reboot hello VM at least once.</span></span>

##### <a name="steps"></a><span data-ttu-id="e14fe-746">Pasos</span><span class="sxs-lookup"><span data-stu-id="e14fe-746">Steps</span></span>
1. <span data-ttu-id="e14fe-747">Crear una máquina virtual mediante una de las distribuciones de hello especificadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-747">Create a VM by using one of hello distributions specified previously.</span></span>

 <span data-ttu-id="e14fe-748">Para CentOS 7.2, se admite el cifrado de disco del sistema operativo a través de una imagen especial.</span><span class="sxs-lookup"><span data-stu-id="e14fe-748">For CentOS 7.2, OS disk encryption is supported via a special image.</span></span> <span data-ttu-id="e14fe-749">toouse esta imagen, especifique "7.2n" como Hola SKU cuando creas Hola VM:</span><span class="sxs-lookup"><span data-stu-id="e14fe-749">toouse this image, specify "7.2n" as hello SKU when you create hello VM:</span></span>
 ```
    Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName "OpenLogic" -Offer "CentOS" -Skus "7.2n" -Version "latest"
 ```
2. <span data-ttu-id="e14fe-750">Configure las necesidades tooyour VM correspondiente Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-750">Configure hello VM according tooyour needs.</span></span> <span data-ttu-id="e14fe-751">Si va a tooencrypt todas las unidades de hello (sistema operativo + datos), las unidades de datos de hello necesitan toobe especificado y pueda montar de/etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="e14fe-751">If you are going tooencrypt all hello (OS + data) drives, hello data drives need toobe specified and mountable from /etc/fstab.</span></span>

 > [!NOTE]
 > <span data-ttu-id="e14fe-752">Usar UUID =... toospecify unidades de datos en/etcetera/fstab en lugar de especificar el nombre de dispositivo de bloque de hello (por ejemplo, / dev/sdb1).</span><span class="sxs-lookup"><span data-stu-id="e14fe-752">Use UUID=... toospecify data drives in /etc/fstab instead of specifying hello block device name (for example, /dev/sdb1).</span></span> <span data-ttu-id="e14fe-753">Durante el cifrado, cambia el orden de Hola de unidades en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-753">During encryption, hello order of drives changes on hello VM.</span></span> <span data-ttu-id="e14fe-754">Si la máquina virtual se basa en un orden específico de dispositivos de bloque, se producirá un error toomount tras su cifrado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-754">If your VM relies on a specific order of block devices, it will fail toomount them after encryption.</span></span>

3. <span data-ttu-id="e14fe-755">Cierre la sesión de las sesiones SSH de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-755">Sign out of hello SSH sessions.</span></span>

4. <span data-ttu-id="e14fe-756">Hola tooencrypt OS, especifique volumeType como **todos los** o **OS** cuando se [habilitar el cifrado](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span><span class="sxs-lookup"><span data-stu-id="e14fe-756">tooencrypt hello OS, specify volumeType as **All** or **OS** when you [enable encryption](#enable-encryption-on-existing-or-running-iaas-linux-vm-in-azure).</span></span>

 > [!NOTE]
 > <span data-ttu-id="e14fe-757">Todos los procesos de espacio de usuario que no se ejecutan como servicios `systemd` deben terminarse con `SIGKILL`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-757">All user-space processes that are not running as `systemd` services should be killed with a `SIGKILL`.</span></span> <span data-ttu-id="e14fe-758">Reinicie Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-758">Reboot hello VM.</span></span> <span data-ttu-id="e14fe-759">Al habilitar el cifrado del disco de sistema operativo en una máquina virtual en ejecución, tenga en cuenta el tiempo de inactividad de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-759">When you enable OS disk encryption on a running VM, plan on VM downtime.</span></span>

5. <span data-ttu-id="e14fe-760">Periódicamente supervisar el progreso de Hola de cifrado mediante el uso de instrucciones de Hola Hola [próxima sección](#monitoring-os-encryption-progress).</span><span class="sxs-lookup"><span data-stu-id="e14fe-760">Periodically monitor hello progress of encryption by using hello instructions in hello [next section](#monitoring-os-encryption-progress).</span></span>

6. <span data-ttu-id="e14fe-761">Después de Get-AzureRmVmDiskEncryptionStatus muestra "VMRestartPending", reinicie la máquina virtual debe iniciar sesión en tooit o mediante el portal de hello, PowerShell o CLI.</span><span class="sxs-lookup"><span data-stu-id="e14fe-761">After Get-AzureRmVmDiskEncryptionStatus shows "VMRestartPending," restart your VM either by signing in tooit or by using hello portal, PowerShell, or CLI.</span></span>
    ```
    C:\> Get-AzureRmVmDiskEncryptionStatus  -ResourceGroupName $ResourceGroupName -VMName $VMName
    -ExtensionName $ExtensionName

    OsVolumeEncrypted          : VMRestartPending
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk successfully encrypted, reboot hello VM
    ```
<span data-ttu-id="e14fe-762">Antes de reiniciar, se recomienda que guarde [diagnósticos de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-762">Before you reboot, we recommend that you save [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/) of hello VM.</span></span>

#### <a name="monitoring-os-encryption-progress"></a><span data-ttu-id="e14fe-763">Supervisión del progreso de cifrado del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e14fe-763">Monitoring OS encryption progress</span></span>
<span data-ttu-id="e14fe-764">Hay tres maneras de supervisar el progreso de cifrado del sistema operativo:</span><span class="sxs-lookup"><span data-stu-id="e14fe-764">You can monitor OS encryption progress in three ways:</span></span>

* <span data-ttu-id="e14fe-765">Hola de uso `Get-AzureRmVmDiskEncryptionStatus` cmdlet e inspeccionar el campo de Hola ProgressMessage:</span><span class="sxs-lookup"><span data-stu-id="e14fe-765">Use hello `Get-AzureRmVmDiskEncryptionStatus` cmdlet and inspect hello ProgressMessage field:</span></span>
    ```
    OsVolumeEncrypted          : EncryptionInProgress
    DataVolumesEncrypted       : NotMounted
    OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
    ProgressMessage            : OS disk encryption started
    ```
 <span data-ttu-id="e14fe-766">Después de hello VM llega "Iniciarlo el cifrado de disco del sistema operativo", que tarda aproximadamente 40 minutos too50 en un almacenamiento Premium copia de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-766">After hello VM reaches "OS disk encryption started," it takes about 40 too50 minutes on a Premium-storage backed VM.</span></span>

 <span data-ttu-id="e14fe-767">Debido al [problema 388](https://github.com/Azure/WALinuxAgent/issues/388) de WALinuxAgent, `OsVolumeEncrypted` y `DataVolumesEncrypted` se muestran como `Unknown` en algunas distribuciones.</span><span class="sxs-lookup"><span data-stu-id="e14fe-767">Because of [issue #388](https://github.com/Azure/WALinuxAgent/issues/388) in WALinuxAgent, `OsVolumeEncrypted` and `DataVolumesEncrypted` show up as `Unknown` in some distributions.</span></span> <span data-ttu-id="e14fe-768">En WALinuxAgent versión 2.1.5 y versiones posteriores, este problema se ha corregido automáticamente.</span><span class="sxs-lookup"><span data-stu-id="e14fe-768">With WALinuxAgent version 2.1.5 and later, this issue is fixed automatically.</span></span> <span data-ttu-id="e14fe-769">Si ve `Unknown` en la salida de hello, puede comprobar el estado de cifrado del disco mediante Hola Explorador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-769">If you see `Unknown` in hello output, you can verify disk-encryption status by using hello Azure Resource Explorer.</span></span>

 <span data-ttu-id="e14fe-770">Vaya demasiado[Explorador de recursos de Azure](https://resources.azure.com/)y, a continuación, expanda esta jerarquía en el panel de selección de Hola a izquierda:</span><span class="sxs-lookup"><span data-stu-id="e14fe-770">Go too[Azure Resource Explorer](https://resources.azure.com/), and then expand this hierarchy in hello selection panel on left:</span></span>

 ~~~~
 |-- subscriptions
     |-- [Your subscription]
          |-- resourceGroups
               |-- [Your resource group]
                    |-- providers
                         |-- Microsoft.Compute
                              |-- virtualMachines
                                   |-- [Your virtual machine]
                                        |-- InstanceView
~~~~                

 <span data-ttu-id="e14fe-771">Hola InstanceView, desplácese hacia abajo de estado de cifrado de hello toosee de las unidades de disco.</span><span class="sxs-lookup"><span data-stu-id="e14fe-771">In hello InstanceView, scroll down toosee hello encryption status of your drives.</span></span>

 ![Vista de instancia de máquina virtual](./media/azure-security-disk-encryption/vm-instanceview.png)

* <span data-ttu-id="e14fe-773">Fíjese en los [diagnósticos de arranque](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-773">Look at [boot diagnostics](https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/).</span></span> <span data-ttu-id="e14fe-774">Mensajes de Hola extensión de fachada deben agregarse como prefijo `[AzureDiskEncryption]`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-774">Messages from hello ADE extension should be prefixed with `[AzureDiskEncryption]`.</span></span>

* <span data-ttu-id="e14fe-775">Inicie sesión en toohello máquina virtual a través de SSH y obtener registros de extensión de Hola desde:</span><span class="sxs-lookup"><span data-stu-id="e14fe-775">Sign in toohello VM via SSH, and get hello extension log from:</span></span>

    <span data-ttu-id="e14fe-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span><span class="sxs-lookup"><span data-stu-id="e14fe-776">/var/log/azure/Microsoft.Azure.Security.AzureDiskEncryptionForLinux</span></span>

 <span data-ttu-id="e14fe-777">Se recomienda no iniciar sesión toohello VM durante el cifrado del sistema operativo en curso.</span><span class="sxs-lookup"><span data-stu-id="e14fe-777">We recommend that you do not sign in toohello VM while OS encryption is in progress.</span></span> <span data-ttu-id="e14fe-778">Copiar registros de hello solo cuando hello otros dos métodos han fallado.</span><span class="sxs-lookup"><span data-stu-id="e14fe-778">Copy hello logs only when hello other two methods have failed.</span></span>

#### <a name="prepare-a-pre-encrypted-linux-vhd"></a><span data-ttu-id="e14fe-779">Preparación de un VHD con Linux precifrado</span><span class="sxs-lookup"><span data-stu-id="e14fe-779">Prepare a pre-encrypted Linux VHD</span></span>
##### <a name="ubuntu-16"></a><span data-ttu-id="e14fe-780">Ubuntu 16</span><span class="sxs-lookup"><span data-stu-id="e14fe-780">Ubuntu 16</span></span>
<span data-ttu-id="e14fe-781">Configurar el cifrado durante la instalación de la distribución de hello haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-781">Configure encryption during hello distribution installation by doing hello following:</span></span>

1. <span data-ttu-id="e14fe-782">Seleccione **configurar los volúmenes cifrados** al realizar particiones de los discos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-782">Select **Configure encrypted volumes** when you partition hello disks.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig1.png)

2. <span data-ttu-id="e14fe-784">Cree una unidad de arranque independiente, que no debe estar cifrada.</span><span class="sxs-lookup"><span data-stu-id="e14fe-784">Create a separate boot drive, which must not be encrypted.</span></span> <span data-ttu-id="e14fe-785">Cifre la unidad raíz.</span><span class="sxs-lookup"><span data-stu-id="e14fe-785">Encrypt your root drive.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig2.png)

3. <span data-ttu-id="e14fe-787">Proporcione una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="e14fe-787">Provide a passphrase.</span></span> <span data-ttu-id="e14fe-788">Se trata de una frase de contraseña de Hola que cargar el almacén de claves toohello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-788">This is hello passphrase that you upload toohello key vault.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig3.png)

4. <span data-ttu-id="e14fe-790">Finalice la partición.</span><span class="sxs-lookup"><span data-stu-id="e14fe-790">Finish partitioning.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig4.png)

5. <span data-ttu-id="e14fe-792">Cuando se arranca Hola VM y se pide una frase de contraseña, utilice Hola frase de contraseña que proporcionó en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="e14fe-792">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig5.png)

6. <span data-ttu-id="e14fe-794">Preparar Hola VM para cargar en Azure mediante [estas instrucciones](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span><span class="sxs-lookup"><span data-stu-id="e14fe-794">Prepare hello VM for uploading into Azure using [these instructions](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-ubuntu/).</span></span> <span data-ttu-id="e14fe-795">Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).</span><span class="sxs-lookup"><span data-stu-id="e14fe-795">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="e14fe-796">Configurar cifrado toowork con Azure haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="e14fe-796">Configure encryption toowork with Azure by doing hello following:</span></span>

1. <span data-ttu-id="e14fe-797">Cree un archivo bajo /usr/local/sbin/azure_crypt_key.sh, con contenido de Hola Hola siguiente secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-797">Create a file under /usr/local/sbin/azure_crypt_key.sh, with hello content in hello following script.</span></span> <span data-ttu-id="e14fe-798">Preste atención toohello KeyFileName, porque es el nombre de archivo de frase de contraseña de hello usa Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-798">Pay attention toohello KeyFileName, because it is hello passphrase file name used by Azure.</span></span>

    ```
    #!/bin/sh
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint
    modprobe vfat >/dev/null 2>&1
    modprobe ntfs >/dev/null 2>&1
    sleep 2
    OPENED=0
    cd /sys/block
    for DEV in sd*; do

        echo "> Trying device: $DEV ..." >&2
        mount -t vfat -r /dev/${DEV}1 $MountPoint >/dev/null||
        mount -t ntfs -r /dev/${DEV}1 $MountPoint >/dev/null
        if [ -f $MountPoint/$KeyFileName ]; then
                cat $MountPoint/$KeyFileName
                umount $MountPoint 2>/dev/null
                OPENED=1
                break
        fi
        umount $MountPoint 2>/dev/null
    done

      if [ $OPENED -eq 0 ]; then
        echo "FAILED toofind suitable passphrase file ..." >&2
        echo -n "Try tooenter your password: " >&2
        read -s -r A </dev/console
        echo -n "$A"
     else
        echo "Success loading keyfile!" >&2
    fi
```

2. <span data-ttu-id="e14fe-799">Cambiar la configuración de cifrado de hello en */etcetera/crypttab*.</span><span class="sxs-lookup"><span data-stu-id="e14fe-799">Change hello crypt config in */etc/crypttab*.</span></span> <span data-ttu-id="e14fe-800">Debería ser parecido a este:</span><span class="sxs-lookup"><span data-stu-id="e14fe-800">It should look like this:</span></span>
 ```
    xxx_crypt uuid=xxxxxxxxxxxxxxxxxxxxx none luks,discard,keyscript=/usr/local/sbin/azure_crypt_key.sh
    ```

3. <span data-ttu-id="e14fe-801">Si está editando *azure_crypt_key.sh* en Windows y se copian tooLinux, ejecute `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-801">If you are editing *azure_crypt_key.sh* in Windows and you copied it tooLinux, run `dos2unix /usr/local/sbin/azure_crypt_key.sh`.</span></span>

4. <span data-ttu-id="e14fe-802">Agregue permisos ejecutable toohello script:</span><span class="sxs-lookup"><span data-stu-id="e14fe-802">Add executable permissions toohello script:</span></span>
 ```
    chmod +x /usr/local/sbin/azure_crypt_key.sh
 ```
5. <span data-ttu-id="e14fe-803">Edite */etc/initramfs-tools/modules* anexando líneas:</span><span class="sxs-lookup"><span data-stu-id="e14fe-803">Edit */etc/initramfs-tools/modules* by appending lines:</span></span>
 ```
    vfat
    ntfs
    nls_cp437
    nls_utf8
    nls_iso8859-1
```
6. <span data-ttu-id="e14fe-804">Ejecutar `update-initramfs -u -k all` tooupdate Hola initramfs toomake Hola `keyscript` surta efecto.</span><span class="sxs-lookup"><span data-stu-id="e14fe-804">Run `update-initramfs -u -k all` tooupdate hello initramfs toomake hello `keyscript` take effect.</span></span>

7. <span data-ttu-id="e14fe-805">Ahora puede cancelar el aprovisionamiento de hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e14fe-805">Now you can deprovision hello VM.</span></span>

 ![Instalación de Ubuntu 16.04](./media/azure-security-disk-encryption/ubuntu-1604-preencrypted-fig6.png)

8. <span data-ttu-id="e14fe-807">Continuar paso siguiente toohello y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-807">Continue toohello next step and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="opensuse-132"></a><span data-ttu-id="e14fe-808">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="e14fe-808">openSUSE 13.2</span></span>
<span data-ttu-id="e14fe-809">cifrado de tooconfigure durante la instalación de la distribución de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-809">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="e14fe-810">Para crear particiones en discos de hello, seleccione **cifrar el grupo de volúmenes**y, a continuación, escriba una contraseña.</span><span class="sxs-lookup"><span data-stu-id="e14fe-810">When you partition hello disks, select **Encrypt Volume Group**, and then enter a password.</span></span> <span data-ttu-id="e14fe-811">Se trata de una contraseña de Hola que va a cargar el almacén de claves tooyour.</span><span class="sxs-lookup"><span data-stu-id="e14fe-811">This is hello password that you will upload tooyour key vault.</span></span>

 ![Instalación de openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig1.png)

2. <span data-ttu-id="e14fe-813">Hola máquina virtual con la contraseña de inicio.</span><span class="sxs-lookup"><span data-stu-id="e14fe-813">Boot hello VM using your password.</span></span>

 ![Instalación de openSUSE 13.2](./media/azure-security-disk-encryption/opensuse-encrypt-fig2.png)

3. <span data-ttu-id="e14fe-815">Preparar Hola VM para cargar tooAzure siguiendo las instrucciones de hello en [preparar una máquina virtual SLES o openSUSE para Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span><span class="sxs-lookup"><span data-stu-id="e14fe-815">Prepare hello VM for uploading tooAzure by following hello instructions in [Prepare a SLES or openSUSE virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-suse-create-upload-vhd/#prepare-opensuse-131).</span></span> <span data-ttu-id="e14fe-816">Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).</span><span class="sxs-lookup"><span data-stu-id="e14fe-816">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

<span data-ttu-id="e14fe-817">tooconfigure toowork de cifrado con Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-817">tooconfigure encryption toowork with Azure, do hello following:</span></span>
1. <span data-ttu-id="e14fe-818">Editar /etc/dracut.conf hello y agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="e14fe-818">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```
2. <span data-ttu-id="e14fe-819">Comenta estas líneas end Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="e14fe-819">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
 ```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
 ```

3. <span data-ttu-id="e14fe-820">Anexar Hola siguiente línea al principio de Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="e14fe-820">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
 ```
    DRACUT_SYSTEMD=0
 ```
<span data-ttu-id="e14fe-821">Y cambie todas las apariciones de:</span><span class="sxs-lookup"><span data-stu-id="e14fe-821">And change all occurrences of:</span></span>
 ```
    if [ -z "$DRACUT_SYSTEMD" ]; then
 ```
<span data-ttu-id="e14fe-822">a:</span><span class="sxs-lookup"><span data-stu-id="e14fe-822">to:</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="e14fe-823">Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh y anexe demasiado "dispositivo de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="e14fe-823">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append it too“# Open LUKS device”:</span></span>

    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```
5. <span data-ttu-id="e14fe-824">Ejecutar `/usr/sbin/dracut -f -v` tooupdate Hola initrd.</span><span class="sxs-lookup"><span data-stu-id="e14fe-824">Run `/usr/sbin/dracut -f -v` tooupdate hello initrd.</span></span>

6. <span data-ttu-id="e14fe-825">Ahora puede cancelar el aprovisionamiento Hola VM y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-825">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

##### <a name="centos-7"></a><span data-ttu-id="e14fe-826">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="e14fe-826">CentOS 7</span></span>
<span data-ttu-id="e14fe-827">cifrado de tooconfigure durante la instalación de la distribución de hello, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-827">tooconfigure encryption during hello distribution installation, do hello following:</span></span>
1. <span data-ttu-id="e14fe-828">Seleccione **Encrypt my data** (Cifrar mis datos) al crear particiones en discos.</span><span class="sxs-lookup"><span data-stu-id="e14fe-828">Select **Encrypt my data** when you partition disks.</span></span>

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig1.png)

2. <span data-ttu-id="e14fe-830">Asegúrese de que **Encrypt** (Cifrar) está seleccionado para la partición raíz.</span><span class="sxs-lookup"><span data-stu-id="e14fe-830">Make sure **Encrypt** is selected for root partition.</span></span>

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig2.png)

3. <span data-ttu-id="e14fe-832">Proporcione una frase de contraseña.</span><span class="sxs-lookup"><span data-stu-id="e14fe-832">Provide a passphrase.</span></span> <span data-ttu-id="e14fe-833">Se trata de una frase de contraseña de Hola que va a cargar el almacén de claves tooyour.</span><span class="sxs-lookup"><span data-stu-id="e14fe-833">This is hello passphrase that you will upload tooyour key vault.</span></span>

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig3.png)

4. <span data-ttu-id="e14fe-835">Cuando se arranca Hola VM y se pide una frase de contraseña, utilice Hola frase de contraseña que proporcionó en el paso 3.</span><span class="sxs-lookup"><span data-stu-id="e14fe-835">When you boot hello VM and are asked for a passphrase, use hello passphrase you provided in step 3.</span></span>

 ![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig4.png)

5. <span data-ttu-id="e14fe-837">Preparar Hola VM para cargar en Azure mediante el uso de instrucciones de "CentOS 7.0 +" hello en [preparar una máquina virtual CentOS para Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span><span class="sxs-lookup"><span data-stu-id="e14fe-837">Prepare hello VM for uploading into Azure by using hello "CentOS 7.0+" instructions in [Prepare a CentOS-based virtual machine for Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-linux-create-upload-centos/#centos-70).</span></span> <span data-ttu-id="e14fe-838">Aún no ejecutado último paso de hello (Hola desaprovisionamiento VM).</span><span class="sxs-lookup"><span data-stu-id="e14fe-838">Do not run hello last step (deprovisioning hello VM) yet.</span></span>

6. <span data-ttu-id="e14fe-839">Ahora puede cancelar el aprovisionamiento Hola VM y [cargar el disco duro virtual](#upload-encrypted-vhd-to-an-azure-storage-account) en Azure.</span><span class="sxs-lookup"><span data-stu-id="e14fe-839">Now you can deprovision hello VM and [upload your VHD](#upload-encrypted-vhd-to-an-azure-storage-account) into Azure.</span></span>

<span data-ttu-id="e14fe-840">tooconfigure toowork de cifrado con Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="e14fe-840">tooconfigure encryption toowork with Azure, do hello following:</span></span>

1. <span data-ttu-id="e14fe-841">Editar /etc/dracut.conf hello y agregue Hola después de línea:</span><span class="sxs-lookup"><span data-stu-id="e14fe-841">Edit hello /etc/dracut.conf, and add hello following line:</span></span>
    ```
    add_drivers+=" vfat ntfs nls_cp437 nls_iso8859-1"
    ```

2. <span data-ttu-id="e14fe-842">Comenta estas líneas end Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span><span class="sxs-lookup"><span data-stu-id="e14fe-842">Comment out these lines by hello end of hello file /usr/lib/dracut/modules.d/90crypt/module-setup.sh:</span></span>
```
    #        inst_multiple -o \
    #        $systemdutildir/system-generators/systemd-cryptsetup-generator \
    #        $systemdutildir/systemd-cryptsetup \
    #        $systemdsystemunitdir/systemd-ask-password-console.path \
    #        $systemdsystemunitdir/systemd-ask-password-console.service \
    #        $systemdsystemunitdir/cryptsetup.target \
    #        $systemdsystemunitdir/sysinit.target.wants/cryptsetup.target \
    #        systemd-ask-password systemd-tty-ask-password-agent
    #        inst_script "$moddir"/crypt-run-generator.sh /sbin/crypt-run-generator
```

3. <span data-ttu-id="e14fe-843">Anexar Hola siguiente línea al principio de Hola de hello archivo /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span><span class="sxs-lookup"><span data-stu-id="e14fe-843">Append hello following line at hello beginning of hello file /usr/lib/dracut/modules.d/90crypt/parse-crypt.sh:</span></span>
```
    DRACUT_SYSTEMD=0
```
<span data-ttu-id="e14fe-844">Y cambie todas las apariciones de:</span><span class="sxs-lookup"><span data-stu-id="e14fe-844">And change all occurrences of:</span></span>
```
    if [ -z "$DRACUT_SYSTEMD" ]; then
```
<span data-ttu-id="e14fe-845">to</span><span class="sxs-lookup"><span data-stu-id="e14fe-845">to</span></span>
```
    if [ 1 ]; then
```
4. <span data-ttu-id="e14fe-846">Editar /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh y anexe esto después de hello "dispositivo de abrir LUKS #":</span><span class="sxs-lookup"><span data-stu-id="e14fe-846">Edit /usr/lib/dracut/modules.d/90crypt/cryptroot-ask.sh and append this after hello “# Open LUKS device”:</span></span>
    ```
    MountPoint=/tmp-keydisk-mount
    KeyFileName=LinuxPassPhraseFileName
    echo "Trying tooget hello key from disks ..." >&2
    mkdir -p $MountPoint >&2
    modprobe vfat >/dev/null >&2
    modprobe ntfs >/dev/null >&2
    for SFS in /dev/sd*; do
    echo "> Trying device:$SFS..." >&2
    mount ${SFS}1 $MountPoint -t vfat -r >&2 ||
    mount ${SFS}1 $MountPoint -t ntfs -r >&2
    if [ -f $MountPoint/$KeyFileName ]; then
        echo "> keyfile got..." >&2
        cp $MountPoint/$KeyFileName /tmp-keyfile >&2
        luksfile=/tmp-keyfile
        umount $MountPoint >&2
        break
    fi
    done
    ```    
5. <span data-ttu-id="e14fe-847">Ejecute hello "/ usr/sbin/dracut - f - v" tooupdate Hola initrd.</span><span class="sxs-lookup"><span data-stu-id="e14fe-847">Run hello “/usr/sbin/dracut -f -v” tooupdate hello initrd.</span></span>

![Instalación de centOS 7](./media/azure-security-disk-encryption/centos-encrypt-fig5.png)

### <a name="upload-encrypted-vhd-tooan-azure-storage-account"></a><span data-ttu-id="e14fe-849">Cargar cifrado cuenta de almacenamiento de Azure de tooan de disco duro virtual</span><span class="sxs-lookup"><span data-stu-id="e14fe-849">Upload encrypted VHD tooan Azure storage account</span></span>
<span data-ttu-id="e14fe-850">Una vez que se habilita el cifrado de BitLocker o Crypt DM, Hola local cifra cuenta de almacenamiento de disco duro virtual necesidades toobe cargado tooyour.</span><span class="sxs-lookup"><span data-stu-id="e14fe-850">After BitLocker encryption or DM-Crypt encryption is enabled, hello local encrypted VHD needs toobe uploaded tooyour storage account.</span></span>

    Add-AzureRmVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo> [[-NumberOfUploaderThreads] <Int32> ] [[-BaseImageUriToPatch] <Uri> ] [[-OverWrite]] [ <CommonParameters>]

### <a name="upload-hello-disk-encryption-secret-for-hello-pre-encrypted-vm-tooyour-key-vault"></a><span data-ttu-id="e14fe-851">Cargar el secreto de cifrado del disco de Hola para hello cifrado previamente VM tooyour almacén de claves</span><span class="sxs-lookup"><span data-stu-id="e14fe-851">Upload hello disk-encryption secret for hello pre-encrypted VM tooyour key vault</span></span>
<span data-ttu-id="e14fe-852">secreto de cifrado del disco de Hola que ha obtenido previamente se debe cargar como un secreto en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-852">hello disk-encryption secret that you obtained previously must be uploaded as a secret in your key vault.</span></span> <span data-ttu-id="e14fe-853">almacén de claves de Hello necesita toohave cifrado del disco y permisos habilitados para el cliente de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e14fe-853">hello key vault needs toohave disk encryption and permissions enabled for your Azure AD client.</span></span>

    $AadClientId = "YourAADClientId"
    $AadClientSecret = "YourAADClientSecret"

    $key vault = New-AzureRmKeyVault -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -Location $Location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -ServicePrincipalName $AadClientId -PermissionsToKeys all -PermissionsToSecrets all
    Set-AzureRmKeyVaultAccessPolicy -VaultName $KeyVaultName -ResourceGroupName $ResourceGroupName -EnabledForDiskEncryption


#### <a name="disk-encryption-secret-not-encrypted-with-a-kek"></a><span data-ttu-id="e14fe-854">Secreto del cifrado de disco no cifrado con una KEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-854">Disk encryption secret not encrypted with a KEK</span></span>
<span data-ttu-id="e14fe-855">tooset copias de seguridad secreto hello en el almacén de claves, use [AzureKeyVaultSecret conjunto](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span><span class="sxs-lookup"><span data-stu-id="e14fe-855">tooset up hello secret in your key vault, use [Set-AzureKeyVaultSecret](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret).</span></span> <span data-ttu-id="e14fe-856">Si tiene una máquina virtual de Windows, archivo de hello bek se codifica como una cadena base64 y, a continuación, cargar el almacén de claves tooyour con hello `Set-AzureKeyVaultSecret` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e14fe-856">If you have a Windows virtual machine, hello bek file is encoded as a base64 string and then uploaded tooyour key vault using hello `Set-AzureKeyVaultSecret` cmdlet.</span></span> <span data-ttu-id="e14fe-857">Para Linux, la frase de contraseña de Hola se codifica como una cadena base64 y, a continuación, carga el almacén de claves toohello.</span><span class="sxs-lookup"><span data-stu-id="e14fe-857">For Linux, hello passphrase is encoded as a base64 string and then uploaded toohello key vault.</span></span> <span data-ttu-id="e14fe-858">Además, asegúrese de que ese Hola después de las etiquetas se establecen cuando se crea el secreto de hello en el almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-858">In addition, make sure that hello following tags are set when you create hello secret in hello key vault.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    $tags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $secretName = [guid]::NewGuid().ToString()
    $secretValue = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($passphrase))
    $secureSecretValue = ConvertTo-SecureString $secretValue -AsPlainText -Force

    $secret = Set-AzureKeyVaultSecret -VaultName $KeyVaultName -Name $secretName -SecretValue $secureSecretValue -tags $tags
    $secretUrl = $secret.Id

<span data-ttu-id="e14fe-859">Hola de uso `$secretUrl` en el paso siguiente de Hola para [adjuntando el disco Hola OS sin usar KEK](#without-using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="e14fe-859">Use hello `$secretUrl` in hello next step for [attaching hello OS disk without using KEK](#without-using-a-kek).</span></span>

#### <a name="disk-encryption-secret-encrypted-with-a-kek"></a><span data-ttu-id="e14fe-860">Secreto del cifrado de disco cifrado con una KEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-860">Disk encryption secret encrypted with a KEK</span></span>
<span data-ttu-id="e14fe-861">Antes de cargar el almacén de claves secretas toohello hello, si lo desea puede cifrar mediante una clave de cifrado de claves.</span><span class="sxs-lookup"><span data-stu-id="e14fe-861">Before you upload hello secret toohello key vault, you can optionally encrypt it by using a key encryption key.</span></span> <span data-ttu-id="e14fe-862">Ajuste de Hola de uso [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst cifrar secreto Hola con clave de cifrado de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-862">Use hello wrap [API](https://msdn.microsoft.com/library/azure/dn878066.aspx) toofirst encrypt hello secret using hello key encryption key.</span></span> <span data-ttu-id="e14fe-863">resultado de esta operación de encapsulado de Hello es una cadena de dirección URL codificada en base64, que, a continuación, puede cargar como un secreto mediante hello [ `Set-AzureKeyVaultSecret` ](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e14fe-863">hello output of this wrap operation is a base64 URL encoded string, which you can then upload as a secret by using hello [`Set-AzureKeyVaultSecret`](/powershell/module/azurerm.keyvault/set-azurekeyvaultsecret) cmdlet.</span></span>

    # This is hello passphrase that was provided for encryption during hello distribution installation
    $passphrase = "contoso-password"

    Add-AzureKeyVaultKey -VaultName $KeyVaultName -Name "keyencryptionkey" -Destination Software
    $KeyEncryptionKey = Get-AzureKeyVaultKey -VaultName $KeyVault.OriginalVault.Name -Name "keyencryptionkey"

    $apiversion = "2015-06-01"

    ##############################
    # Get Auth URI
    ##############################

    $uri = $KeyVault.VaultUri + "/keys"
    $headers = @{}

    $response = try { Invoke-RestMethod -Method GET -Uri $uri -Headers $headers } catch { $_.Exception.Response }

    $authHeader = $response.Headers["www-authenticate"]
    $authUri = [regex]::match($authHeader, 'authorization="(.*?)"').Groups[1].Value

    Write-Host "Got Auth URI successfully"

    ##############################
    # Get Auth Token
    ##############################

    $uri = $authUri + "/oauth2/token"
    $body = "grant_type=client_credentials"
    $body += "&client_id=" + $AadClientId
    $body += "&client_secret=" + [Uri]::EscapeDataString($AadClientSecret)
    $body += "&resource=" + [Uri]::EscapeDataString("https://vault.azure.net")
    $headers = @{}

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $access_token = $response.access_token

    Write-Host "Got Auth Token successfully"

    ##############################
    # Get KEK info
    ##############################

    $uri = $KeyEncryptionKey.Id + "?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token}

    $response = Invoke-RestMethod -Method GET -Uri $uri -Headers $headers

    $keyid = $response.key.kid

    Write-Host "Got KEK info successfully"

    ##############################
    # Encrypt passphrase using KEK
    ##############################

    $passphraseB64 = [Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($Passphrase))
    $uri = $keyid + "/encrypt?api-version=" + $apiversion
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"alg" = "RSA-OAEP"; "value" = $passphraseB64}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method POST -Uri $uri -Headers $headers -Body $body

    $wrappedSecret = $response.value

    Write-Host "Encrypted passphrase successfully"

    ##############################
    # Store secret
    ##############################

    $secretName = [guid]::NewGuid().ToString()
    $uri = $KeyVault.VaultUri + "/secrets/" + $secretName + "?api-version=" + $apiversion
    $secretAttributes = @{"enabled" = $true}
    $secretTags = @{"DiskEncryptionKeyEncryptionAlgorithm" = "RSA-OAEP"; "DiskEncryptionKeyFileName" = "LinuxPassPhraseFileName"}
    $headers = @{"Authorization" = "Bearer " + $access_token; "Content-Type" = "application/json"}
    $bodyObj = @{"value" = $wrappedSecret; "attributes" = $secretAttributes; "tags" = $secretTags}
    $body = $bodyObj | ConvertTo-Json

    $response = Invoke-RestMethod -Method PUT -Uri $uri -Headers $headers -Body $body

    Write-Host "Stored secret successfully"

    $secretUrl = $response.id

<span data-ttu-id="e14fe-864">Use `$KeyEncryptionKey` y `$secretUrl` en el paso siguiente de Hola para [adjuntando el disco Hola SO mediante KEK](#using-a-kek).</span><span class="sxs-lookup"><span data-stu-id="e14fe-864">Use `$KeyEncryptionKey` and `$secretUrl` in hello next step for [attaching hello OS disk using KEK](#using-a-kek).</span></span>

### <a name="specify-a-secret-url-when-you-attach-an-os-disk"></a><span data-ttu-id="e14fe-865">Especificación de una dirección URL de secreto al adjuntar un disco del sistema operativo</span><span class="sxs-lookup"><span data-stu-id="e14fe-865">Specify a secret URL when you attach an OS disk</span></span>
#### <a name="without-using-a-kek"></a><span data-ttu-id="e14fe-866">Sin utilizar una KEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-866">Without using a KEK</span></span>
<span data-ttu-id="e14fe-867">Mientras que va a adjuntar disco de SO hello, necesita toopass `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-867">While you are attaching hello OS disk, you need toopass `$secretUrl`.</span></span> <span data-ttu-id="e14fe-868">dirección URL de Hola se generó en la sección de "secreto de cifrado del disco que no se cifran con una KEK" Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-868">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $VhdUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl

#### <a name="using-a-kek"></a><span data-ttu-id="e14fe-869">Uso de una KEK</span><span class="sxs-lookup"><span data-stu-id="e14fe-869">Using a KEK</span></span>
<span data-ttu-id="e14fe-870">Cuando conecte un disco de SO hello, pasar `$KeyEncryptionKey` y `$secretUrl`.</span><span class="sxs-lookup"><span data-stu-id="e14fe-870">When you attach hello OS disk, pass `$KeyEncryptionKey` and `$secretUrl`.</span></span> <span data-ttu-id="e14fe-871">dirección URL de Hola se generó en la sección de "secreto de cifrado del disco que no se cifran con una KEK" Hola.</span><span class="sxs-lookup"><span data-stu-id="e14fe-871">hello URL was generated in hello "Disk-encryption secret not encrypted with a KEK" section.</span></span>

    Set-AzureRmVMOSDisk `
            -VM $VirtualMachine `
            -Name $OSDiskName `
            -SourceImageUri $CopiedTemplateBlobUri `
            -VhdUri $OSDiskUri `
            -Linux `
            -CreateOption FromImage `
            -DiskEncryptionKeyVaultId $KeyVault.ResourceId `
            -DiskEncryptionKeyUrl $SecretUrl `
            -KeyEncryptionKeyVaultId $KeyVault.ResourceId `
            -KeyEncryptionKeyURL $KeyEncryptionKey.Id

## <a name="download-this-guide"></a><span data-ttu-id="e14fe-872">Descargar esta guía</span><span class="sxs-lookup"><span data-stu-id="e14fe-872">Download this guide</span></span>
<span data-ttu-id="e14fe-873">Puede descargar esta guía de hello [Galería de TechNet](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span><span class="sxs-lookup"><span data-stu-id="e14fe-873">You can download this guide from hello [TechNet Gallery](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0).</span></span>

## <a name="for-more-information"></a><span data-ttu-id="e14fe-874">Para obtener más información</span><span class="sxs-lookup"><span data-stu-id="e14fe-874">For more information</span></span>
<span data-ttu-id="e14fe-875">[Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0) (Exploración de Azure Disk Encryption con Azure PowerShell - Parte 1)</span><span class="sxs-lookup"><span data-stu-id="e14fe-875">[Explore Azure Disk Encryption with Azure PowerShell - Part 1](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/16/explore-azure-disk-encryption-with-azure-powershell.aspx?wa=wsignin1.0)</span></span>  
[<span data-ttu-id="e14fe-876">Exploración de Azure Disk Encryption con Azure PowerShell, parte 2</span><span class="sxs-lookup"><span data-stu-id="e14fe-876">Explore Azure Disk Encryption with Azure PowerShell - Part 2</span></span>](http://blogs.msdn.com/b/azuresecurity/archive/2015/11/21/explore-azure-disk-encryption-with-azure-powershell-part-2.aspx)
