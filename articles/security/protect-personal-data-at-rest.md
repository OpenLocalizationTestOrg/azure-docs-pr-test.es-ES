---
title: "aaaAzure protección de datos personales en reposo con el cifrado | Documentos de Microsoft"
description: "Este artículo forma parte de una serie que ayudan a usar datos personales tooprotect de Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 9af182b4897f1d04f5f519e6671f53b85073bae1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="f60b3-103">Tecnologías de cifrado de Azure: protección de datos personales en reposo con cifrado</span><span class="sxs-lookup"><span data-stu-id="f60b3-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="f60b3-104">En este artículo le ayuda a comprender y usar datos de toosecure de tecnologías de Azure cifrado en reposo.</span><span class="sxs-lookup"><span data-stu-id="f60b3-104">This article helps you understand and use Azure encryption technologies toosecure data at rest.</span></span>

<span data-ttu-id="f60b3-105">El cifrado de datos en reposo es esencial como una mejor práctica tooprotect información personal o confidencial de datos y cumplimiento de normas de toomeet y requisitos de privacidad de datos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-105">Encryption of data at rest is essential as a best practice tooprotect sensitive or personal data and toomeet compliance and data privacy requirements.</span></span>
<span data-ttu-id="f60b3-106">El cifrado en reposo es atacante de hello tooprevent diseñada tengan acceso a datos de hello sin cifrar asegurándose de hello datos se cifran en el disco.</span><span class="sxs-lookup"><span data-stu-id="f60b3-106">Encryption at rest is designed tooprevent hello attacker from accessing hello unencrypted data by ensuring hello data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="f60b3-107">Escenario</span><span class="sxs-lookup"><span data-stu-id="f60b3-107">Scenario</span></span> 

<span data-ttu-id="f60b3-108">Una empresa cruise grandes, con sede en Estados Unidos, Hola está ampliando sus itinerarios toooffer de operaciones en hello Mediterráneo y Mar Báltico, así como Hola británicas.</span><span class="sxs-lookup"><span data-stu-id="f60b3-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="f60b3-109">toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas con sede en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="f60b3-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="f60b3-110">la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="f60b3-111">Esto puede incluir empleado o la información de cliente, como:</span><span class="sxs-lookup"><span data-stu-id="f60b3-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="f60b3-112">direcciones</span><span class="sxs-lookup"><span data-stu-id="f60b3-112">addresses</span></span>
- <span data-ttu-id="f60b3-113">números de teléfono</span><span class="sxs-lookup"><span data-stu-id="f60b3-113">phone numbers</span></span>
- <span data-ttu-id="f60b3-114">números de identificación fiscal</span><span class="sxs-lookup"><span data-stu-id="f60b3-114">tax identification numbers</span></span>
- <span data-ttu-id="f60b3-115">Información médica</span><span class="sxs-lookup"><span data-stu-id="f60b3-115">medical information</span></span>
- <span data-ttu-id="f60b3-116">información de tarjeta de crédito</span><span class="sxs-lookup"><span data-stu-id="f60b3-116">credit card information</span></span>

<span data-ttu-id="f60b3-117">empresa Hola debe proteger la privacidad de Hola de datos de clientes y empleados asegurándose de departamentos de toothose accesible de datos que lo necesiten.</span><span class="sxs-lookup"><span data-stu-id="f60b3-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="f60b3-118">(por ejemplo, los departamentos de nóminas y reservas).</span><span class="sxs-lookup"><span data-stu-id="f60b3-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="f60b3-119">línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad que incluye información personal tootrack relaciones con los clientes actuales y pasados.</span><span class="sxs-lookup"><span data-stu-id="f60b3-119">hello cruise line also maintains a large database of reward and loyalty program members that includes personal information tootrack relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="f60b3-120">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="f60b3-120">Problem statement</span></span>

<span data-ttu-id="f60b3-121">empresa Hola debe proteger la privacidad de Hola de datos personales de los empleados y los clientes al hacer que los departamentos de toothose accesible de datos que lo necesitan (por ejemplo, los departamentos de nóminas y reservas).</span><span class="sxs-lookup"><span data-stu-id="f60b3-121">hello company must protect hello privacy of employees’ and customers’ personal data while making data accessible toothose departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="f60b3-122">Estos datos personales se almacenan fuera de centro de datos corporativos controlado de hello y no está bajo control físico de la compañía de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-122">This personal data is stored outside of hello corporate-controlled data center and is not under hello company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="f60b3-123">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="f60b3-123">Company goal</span></span>

<span data-ttu-id="f60b3-124">Como parte de una estrategia de varias capas de defensa en profundidad de seguridad, es un tooensure de objetivo de la empresa que se cifren todos los orígenes de datos que contienen datos personales, los que residen en el almacenamiento en nube incluidos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal tooensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="f60b3-125">Si no está autorizado personas ganancia acceso toohello los datos personales, debe ser en un formulario que se representará ilegible.</span><span class="sxs-lookup"><span data-stu-id="f60b3-125">If unauthorized persons gain access toohello personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="f60b3-126">La aplicación del cifrado debería ser fácil y transparente tanto para los usuarios como para los administradores.</span><span class="sxs-lookup"><span data-stu-id="f60b3-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="f60b3-127">Soluciones</span><span class="sxs-lookup"><span data-stu-id="f60b3-127">Solutions</span></span>

<span data-ttu-id="f60b3-128">Los servicios de Azure proporcionan varios toohelp herramientas y tecnologías de proteger los datos personales en reposo cifrándolos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-128">Azure services provide multiple tools and technologies toohelp you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="f60b3-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f60b3-129">Azure Key Vault</span></span>

<span data-ttu-id="f60b3-130">[Almacén de claves de Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) ofrece un almacenamiento seguro para las claves de hello utilizan tooencrypt datos en reposo en los servicios de Azure y se recomienda Hola soluciones de almacenamiento y administración de claves.</span><span class="sxs-lookup"><span data-stu-id="f60b3-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for hello keys used tooencrypt data at rest in Azure services and is hello recommended key storage and management solution.</span></span> <span data-ttu-id="f60b3-131">Administración de claves de cifrado es esencial toosecuring almacena datos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-131">Encryption key management is essential toosecuring stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-tooprotect-keys-that-encrypt-personal-data"></a><span data-ttu-id="f60b3-132">¿Cómo se puede usar las claves de tooprotect del almacén de claves de Azure que cifran los datos personales?</span><span class="sxs-lookup"><span data-stu-id="f60b3-132">How do I use Azure Key Vault tooprotect keys that encrypt personal data?</span></span>

<span data-ttu-id="f60b3-133">toouse almacén de claves de Azure, necesita una cuenta de Azure tooan de suscripción.</span><span class="sxs-lookup"><span data-stu-id="f60b3-133">toouse Azure Key Vault, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="f60b3-134">También necesita tener Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="f60b3-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="f60b3-135">Los pasos incluyen usando PowerShell cmdlets toodo Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f60b3-135">Steps include using PowerShell cmdlets toodo hello following:</span></span>

1. <span data-ttu-id="f60b3-136">Conectar tooyour suscripciones</span><span class="sxs-lookup"><span data-stu-id="f60b3-136">Connect tooyour subscriptions</span></span>

2. <span data-ttu-id="f60b3-137">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="f60b3-137">Create a key vault</span></span>

3. <span data-ttu-id="f60b3-138">Agregar una clave o un almacén de claves secretas toohello</span><span class="sxs-lookup"><span data-stu-id="f60b3-138">Add a key or secret toohello key vault</span></span>

4. <span data-ttu-id="f60b3-139">Registrar las aplicaciones que va a usar el almacén de claves Hola con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f60b3-139">Register applications that will use hello key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="f60b3-140">Autorizar Hola aplicaciones toouse Hola clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="f60b3-140">Authorize hello applications toouse hello key or secret</span></span>

<span data-ttu-id="f60b3-141">toocreate un almacén de claves, use hello CmDlt de PowerShell New-AzureRmKeyVault.</span><span class="sxs-lookup"><span data-stu-id="f60b3-141">toocreate a key vault, use hello New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="f60b3-142">Asignará un nombre de almacén, un nombre de grupo de recursos y una ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="f60b3-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="f60b3-143">Deberá usar el nombre del almacén de hello al administrar claves a través de otros Cmdlets.</span><span class="sxs-lookup"><span data-stu-id="f60b3-143">You’ll use hello vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="f60b3-144">Las aplicaciones que utilizan el almacén de Hola a través de la API de REST de hello usará el almacén de hello URI.</span><span class="sxs-lookup"><span data-stu-id="f60b3-144">Applications that use hello vault through hello REST API will use hello vault URI.</span></span>

<span data-ttu-id="f60b3-145">Azure Key Vault puede proporcionar una clave protegida mediante software o importar una clave ya existente de un archivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="f60b3-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="f60b3-146">También puede almacenar secretos (contraseñas) en el almacén de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-146">You can also store secrets (passwords) in hello vault.</span></span>

<span data-ttu-id="f60b3-147">También puede generar una clave de HSM local y transferir tooHSMs Hola servicio de almacén de claves, sin clave Hola dejando límite de HSM Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-147">You can also generate a key in your local HSM and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary.</span></span>

<span data-ttu-id="f60b3-148">Para obtener instrucciones detalladas sobre cómo usar el almacén de claves de Azure, siga los pasos de hello [empezar a trabajar con el almacén de claves de Azure.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="f60b3-148">For detailed instructions on using Azure Key Vault, follow hello steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="f60b3-149">Para obtener una lista de cmdlets de PowerShell que se usan con Azure Key Vault, consulte [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="f60b3-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="f60b3-150">Azure Disk Encryption para Windows</span><span class="sxs-lookup"><span data-stu-id="f60b3-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="f60b3-151">[Azure Disk Encryption para máquinas virtuales de IaaS de Windows y Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protege los datos personales en reposo en las máquinas virtuales de Azure y se integra con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f60b3-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="f60b3-152">Cifrado de disco de Azure usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) en Windows y [DM Crypt](https://en.wikipedia.org/wiki/Dm-crypt) en Linux tooencrypt ambos Hola hello y sistema operativo de los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux tooencrypt both hello OS and hello data disks.</span></span> <span data-ttu-id="f60b3-153">Azure Disk Encryption es compatible con Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, y con clientes de Windows 8 y Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f60b3-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-tooprotect-personal-data"></a><span data-ttu-id="f60b3-154">¿Cómo se puede usar datos personales de tooprotect de cifrado del disco de Azure?</span><span class="sxs-lookup"><span data-stu-id="f60b3-154">How do I use Azure Disk Encryption tooprotect personal data?</span></span>

<span data-ttu-id="f60b3-155">toouse cifrado del disco de Azure, necesita una cuenta de Azure tooan de suscripción.</span><span class="sxs-lookup"><span data-stu-id="f60b3-155">toouse Azure Disk Encryption, you need a subscription tooan Azure account.</span></span> <span data-ttu-id="f60b3-156">Cifrado de disco de Azure tooenable para Windows y las máquinas virtuales de Linux, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f60b3-156">tooenable Azure Disk Encryption for Windows and Linux VMs, do hello following:</span></span>

1. <span data-ttu-id="f60b3-157">Use la plantilla del Administrador de recursos de cifrado de disco de Azure hello, PowerShell o cifrado de disco de tooenable de interfaz de línea de comandos (CLI) de Hola y especifique la configuración de cifrado.</span><span class="sxs-lookup"><span data-stu-id="f60b3-157">Use hello Azure Disk Encryption Resource Manager template, PowerShell, or hello command line interface (CLI) tooenable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="f60b3-158">Conceder acceso toohello material de cifrado de la plataforma Azure tooread Hola desde el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f60b3-158">Grant access toohello Azure platform tooread hello encryption material from your key vault.</span></span>

3. <span data-ttu-id="f60b3-159">Proporcione un Azure Active Directory (AAD) aplicación identidad toowrite Hola cifrado tooyour material clave almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="f60b3-159">Provide an Azure Active Directory (AAD) application identity toowrite hello encryption key material tooyour key vault.</span></span>

<span data-ttu-id="f60b3-160">Azure actualizará Hola VM y la configuración de almacén de claves de Hola y configurar la máquina virtual cifrada.</span><span class="sxs-lookup"><span data-stu-id="f60b3-160">Azure will update hello VM and hello key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="f60b3-161">Al configurar su toosupport de almacén de claves cifrado del disco de Azure, puede agregar una clave de cifrado de claves (KEK) para lograr una mayor seguridad y copia de seguridad de toosupport de máquinas virtuales cifradas.</span><span class="sxs-lookup"><span data-stu-id="f60b3-161">When you set up your key vault toosupport Azure Disk Encryption, you can add a key encryption key (KEK) for added security and toosupport backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="f60b3-162">En [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) puede encontrar instrucciones detalladas sobre escenarios de implementación y experiencias de usuario específicas.</span><span class="sxs-lookup"><span data-stu-id="f60b3-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="f60b3-163">Cifrado del servicio Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f60b3-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="f60b3-164">[Cifrado de servicio de almacenamiento de Azure (SSE) para los datos en reposo](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) le ayuda a proteger y proteger los datos toomeet los compromisos de seguridad y cumplimiento organizativos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data toomeet your organizational security and compliance commitments.</span></span> <span data-ttu-id="f60b3-165">Almacenamiento de Azure automáticamente cifra los datos mediante toostorage de toopersisting anteriores de cifrado de AES de 256 bits y los descifra tooretrieval anterior.</span><span class="sxs-lookup"><span data-stu-id="f60b3-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior toopersisting toostorage, and decrypts it prior tooretrieval.</span></span> <span data-ttu-id="f60b3-166">Este servicio está disponible para los archivos y blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60b3-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-tooprotect-personal-data"></a><span data-ttu-id="f60b3-167">¿Cómo se puede usar datos personales de cifrado del servicio de almacenamiento tooprotect?</span><span class="sxs-lookup"><span data-stu-id="f60b3-167">How do I use Storage Service Encryption tooprotect personal data?</span></span>

<span data-ttu-id="f60b3-168">tooenable cifrado del servicio de almacenamiento, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="f60b3-168">tooenable Storage Service Encryption, do hello following:</span></span>

1. <span data-ttu-id="f60b3-169">Inicie sesión en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60b3-169">Log into hello Azure portal.</span></span>

2. <span data-ttu-id="f60b3-170">Seleccione una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f60b3-170">Select a storage account.</span></span>

3. <span data-ttu-id="f60b3-171">En configuración, en la sección de servicio Blob de hello, seleccione cifrado.</span><span class="sxs-lookup"><span data-stu-id="f60b3-171">In Settings, under hello Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="f60b3-172">En hello sección de servicio de archivos, seleccione el cifrado.</span><span class="sxs-lookup"><span data-stu-id="f60b3-172">Under hello File Service section, select Encryption.</span></span>

<span data-ttu-id="f60b3-173">Tras hacer clic en configuración de cifrado de hello, puede habilitar o deshabilitar el cifrado del servicio de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="f60b3-173">After you click hello Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="f60b3-174">Los datos nuevos se cifrarán.</span><span class="sxs-lookup"><span data-stu-id="f60b3-174">New data will be encrypted.</span></span> <span data-ttu-id="f60b3-175">Los datos en los archivos ya existentes de esta cuenta de almacenamiento permanecerán sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="f60b3-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="f60b3-176">Después de habilitar el cifrado, copie la cuenta de almacenamiento de datos toohello mediante uno de los siguientes métodos de hello:</span><span class="sxs-lookup"><span data-stu-id="f60b3-176">After enabling encryption, copy data toohello storage account using one of hello following methods:</span></span>

1. <span data-ttu-id="f60b3-177">Copiar blobs o archivos con hello [utilidad de línea de comandos de AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="f60b3-177">Copy blobs or files with hello [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="f60b3-178">[Montar un recurso compartido de archivos mediante SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) por lo que puede usar una utilidad como Robocopy toocopy archivos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy toocopy files.</span></span>

3. <span data-ttu-id="f60b3-179">Copiar blob o archivo de datos tooand del almacenamiento de blobs o entre cuentas de almacenamiento mediante [bibliotecas de cliente de almacenamiento, como .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="f60b3-179">Copy blob or file data tooand from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="f60b3-180">Use un [Explorador de almacenamiento](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload tooyour cuenta de almacenamiento de blobs con el cifrado habilitado.</span><span class="sxs-lookup"><span data-stu-id="f60b3-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) tooupload blobs tooyour storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="f60b3-181">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="f60b3-181">Transparent Data Encryption</span></span>

<span data-ttu-id="f60b3-182">Cifrado de datos transparente (TDE) es una característica de SQL Azure mediante el cual se puede cifrar los datos en ambos niveles de base de datos y el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both hello database and server levels.</span></span> <span data-ttu-id="f60b3-183">TDE ahora está habilitado de forma predeterminada en todas las bases de datos recién creadas.</span><span class="sxs-lookup"><span data-stu-id="f60b3-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="f60b3-184">TDE realiza el cifrado de E/S y descifrado de los archivos de datos y de registro de hello en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="f60b3-184">TDE performs real-time I/O encryption and decryption of hello data and log files.</span></span>

#### <a name="how-do-i-use-tde-tooprotect-personal-data"></a><span data-ttu-id="f60b3-185">¿Cómo se puede usar datos personales de TDE tooprotect?</span><span class="sxs-lookup"><span data-stu-id="f60b3-185">How do I use TDE tooprotect personal data?</span></span>

<span data-ttu-id="f60b3-186">Puede configurar TDE a través de hello portal de Azure, mediante el uso de API de REST de hello, o mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f60b3-186">You can configure TDE through hello Azure portal, by using hello REST API, or by using PowerShell.</span></span> <span data-ttu-id="f60b3-187">Hola tooenable TDE en una base de datos existente mediante Hola Portal de Azure, después de:</span><span class="sxs-lookup"><span data-stu-id="f60b3-187">tooenable TDE on an existing database using hello Azure Portal, do hello following:</span></span>

1. <span data-ttu-id="f60b3-188">Visite hello Azure portal en <https://portal.azure.com> e inicie sesión con su cuenta de administrador de Azure o colaborador.</span><span class="sxs-lookup"><span data-stu-id="f60b3-188">Visit hello Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="f60b3-189">En el encabezado de la izquierda hello, haga clic en tooBROWSE y, a continuación, haga clic en bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f60b3-189">On hello left banner, click tooBROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="f60b3-190">Con las bases de datos SQL seleccionadas en el panel izquierdo de hello, haga clic en la base de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="f60b3-190">With SQL databases selected in hello left pane, click your user database.</span></span>

4. <span data-ttu-id="f60b3-191">En la hoja de la base de datos de hello, haga clic en todas las configuraciones.</span><span class="sxs-lookup"><span data-stu-id="f60b3-191">In hello database blade, click All settings.</span></span>

5. <span data-ttu-id="f60b3-192">En la hoja de configuración de hello, haga clic en las hoja de cifrado de datos transparente cifrado parte tooopen Hola transparente de los datos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-192">In hello Settings blade, click Transparent data encryption part tooopen hello Transparent data encryption blade.</span></span>

6. <span data-ttu-id="f60b3-193">En la hoja de cifrado de datos de hello, mover tooOn de botón de cifrado de datos de hello y, a continuación, haga clic en Guardar (al principio de Hola de página de hello) configuración de hello tooapply.</span><span class="sxs-lookup"><span data-stu-id="f60b3-193">In hello Data encryption blade, move hello Data encryption button tooOn, and then click Save (at hello top of hello page) tooapply hello setting.</span></span> <span data-ttu-id="f60b3-194">estado de cifrado de Hello aproximará el progreso de Hola de cifrado de datos transparente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f60b3-194">hello Encryption status will approximate hello progress of hello transparent data encryption.</span></span>

![Habilitar el cifrado de datos](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="f60b3-196">Obtener instrucciones sobre cómo tooenable TDE y obtener información acerca de cómo descifrar las bases de datos protegida por TDE etc. pueden encontrarse en el artículo de Hola [cifrado de datos transparente con base de datos de SQL Azure.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="f60b3-196">Instructions on how tooenable TDE and information on decrypting TDE-protected databases and more can be found in hello article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="f60b3-197">Resumen</span><span class="sxs-lookup"><span data-stu-id="f60b3-197">Summary</span></span>

<span data-ttu-id="f60b3-198">empresa Hola puede lograr su objetivo de cifrar datos personales guardados en hello nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60b3-198">hello company can accomplish its goal of encrypting personal data stored in hello Azure cloud.</span></span> <span data-ttu-id="f60b3-199">Puede hacerlo mediante el cifrado de disco de Azure demasiado proteger volúmenes completos.</span><span class="sxs-lookup"><span data-stu-id="f60b3-199">They can do this by using Azure Disk Encryption too protect entire volumes.</span></span> <span data-ttu-id="f60b3-200">Esto puede incluir archivos de sistema operativo de Hola y archivos de datos que contienen información de identificación personal y otros datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="f60b3-200">This may include both hello operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="f60b3-201">Cifrado de servicio de almacenamiento de Azure puede ser usado tooprotect datos personales que se almacenan en archivos y de blobs.</span><span class="sxs-lookup"><span data-stu-id="f60b3-201">Azure Storage Service encryption can be used tooprotect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="f60b3-202">Para los datos que se almacenan en instancias de Azure SQL Database, el cifrado de datos transparente ofrece protección frente a una exposición no autorizada de información personal.</span><span class="sxs-lookup"><span data-stu-id="f60b3-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="f60b3-203">tooprotect hello las claves usadas tooencrypt datos en Azure, la empresa de hello puede usar el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="f60b3-203">tooprotect hello keys that are used tooencrypt data in Azure, hello company can use Azure Key Vault.</span></span> <span data-ttu-id="f60b3-204">Esto simplifica el proceso de administración de claves de Hola y habilita Hola control toomaintain de empresa de claves que tienen acceso y cifrar los datos personales.</span><span class="sxs-lookup"><span data-stu-id="f60b3-204">This streamlines hello key management process and enables hello company toomaintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f60b3-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f60b3-205">Next steps</span></span>

- [<span data-ttu-id="f60b3-206">Guía de solución de problemas de Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="f60b3-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="f60b3-207">Cifrado de una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="f60b3-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="f60b3-208">Cifrado de datos en Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f60b3-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="f60b3-209">Cifrado de base de datos en reposo en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f60b3-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
