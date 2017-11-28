---
title: "Azure protección de datos personales en reposo con el cifrado | Documentos de Microsoft"
description: "Este artículo forma parte de una serie que ayudan a usar Azure para proteger los datos personales"
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
ms.openlocfilehash: d0ef3ca8d48f5ba11a89c787ff59df39eeaf673b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-encryption-technologies-protect-personal-data-at-rest-with-encryption"></a><span data-ttu-id="25b6e-103">Tecnologías de cifrado de Azure: protección de datos personales en reposo con cifrado</span><span class="sxs-lookup"><span data-stu-id="25b6e-103">Azure encryption technologies: Protect personal data at rest with encryption</span></span>

<span data-ttu-id="25b6e-104">Este artículo le ayudará a entender y usar las tecnologías de cifrado de Azure para proteger datos en reposo.</span><span class="sxs-lookup"><span data-stu-id="25b6e-104">This article helps you understand and use Azure encryption technologies to secure data at rest.</span></span>

<span data-ttu-id="25b6e-105">El cifrado de datos en reposo es un procedimiento recomendado fundamental para proteger datos confidenciales o personales y para cumplir los requisitos de cumplimiento normativo y privacidad de los datos.</span><span class="sxs-lookup"><span data-stu-id="25b6e-105">Encryption of data at rest is essential as a best practice to protect sensitive or personal data and to meet compliance and data privacy requirements.</span></span>
<span data-ttu-id="25b6e-106">El cifrado en reposo está diseñado para evitar que el atacante obtenga acceso a los datos sin cifrar asegurándose de que los datos se cifran en el disco.</span><span class="sxs-lookup"><span data-stu-id="25b6e-106">Encryption at rest is designed to prevent the attacker from accessing the unencrypted data by ensuring the data is encrypted when on disk.</span></span>

## <a name="scenario"></a><span data-ttu-id="25b6e-107">Escenario</span><span class="sxs-lookup"><span data-stu-id="25b6e-107">Scenario</span></span> 

<span data-ttu-id="25b6e-108">Una gran empresa de cruceros, con sede en Estados Unidos, se encuentra en proceso de expansión de sus operaciones para ofrecer itinerarios en los mares Mediterráneo y Báltico, así como en las Islas Británicas.</span><span class="sxs-lookup"><span data-stu-id="25b6e-108">A large cruise company, headquartered in the United States, is expanding its operations to offer itineraries in the Mediterranean, and Baltic seas, as well as the British Isles.</span></span> <span data-ttu-id="25b6e-109">Para apoyar esos esfuerzos, ha adquirido varias líneas de cruceros más pequeñas establecidas en Italia, Alemania, Dinamarca y Reino Unido.</span><span class="sxs-lookup"><span data-stu-id="25b6e-109">To support those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and the U.K.</span></span>

<span data-ttu-id="25b6e-110">La empresa usa Microsoft Azure para almacenar datos corporativos en la nube.</span><span class="sxs-lookup"><span data-stu-id="25b6e-110">The company uses Microsoft Azure to store corporate data in the cloud.</span></span> <span data-ttu-id="25b6e-111">Esto puede incluir empleado o la información de cliente, como:</span><span class="sxs-lookup"><span data-stu-id="25b6e-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="25b6e-112">direcciones</span><span class="sxs-lookup"><span data-stu-id="25b6e-112">addresses</span></span>
- <span data-ttu-id="25b6e-113">números de teléfono</span><span class="sxs-lookup"><span data-stu-id="25b6e-113">phone numbers</span></span>
- <span data-ttu-id="25b6e-114">números de identificación fiscal</span><span class="sxs-lookup"><span data-stu-id="25b6e-114">tax identification numbers</span></span>
- <span data-ttu-id="25b6e-115">Información médica</span><span class="sxs-lookup"><span data-stu-id="25b6e-115">medical information</span></span>
- <span data-ttu-id="25b6e-116">información de tarjeta de crédito</span><span class="sxs-lookup"><span data-stu-id="25b6e-116">credit card information</span></span>

<span data-ttu-id="25b6e-117">La empresa debe proteger la privacidad de los datos de clientes y empleados al hacer que los datos puede tener acceso a los departamentos que lo necesitan.</span><span class="sxs-lookup"><span data-stu-id="25b6e-117">The company must protect the privacy of employee and customer data while making data accessible to those departments that need it.</span></span> <span data-ttu-id="25b6e-118">(por ejemplo, los departamentos de nóminas y reservas).</span><span class="sxs-lookup"><span data-stu-id="25b6e-118">(such as payroll and reservations departments)</span></span>

<span data-ttu-id="25b6e-119">La línea de cruceros también conserva una gran base de datos de miembros del programa de recompensa y lealtad que incluye información personal para hacer un seguimiento de las relaciones con clientes actuales y antiguos.</span><span class="sxs-lookup"><span data-stu-id="25b6e-119">The cruise line also maintains a large database of reward and loyalty program members that includes personal information to track relationships with current and past customers.</span></span>

### <a name="problem-statement"></a><span data-ttu-id="25b6e-120">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="25b6e-120">Problem statement</span></span>

<span data-ttu-id="25b6e-121">La empresa debe proteger la privacidad de los datos personales de los empleados y los clientes al mostrar datos accesibles para los departamentos que lo necesitan (por ejemplo, los departamentos de nóminas y reservas).</span><span class="sxs-lookup"><span data-stu-id="25b6e-121">The company must protect the privacy of employees’ and customers’ personal data while making data accessible to those departments that need it (such as payroll and reservations departments).</span></span> <span data-ttu-id="25b6e-122">Estos datos personales se almacenan fuera del centro de datos controlado por la corporación y no está bajo el control físico de la compañía.</span><span class="sxs-lookup"><span data-stu-id="25b6e-122">This personal data is stored outside of the corporate-controlled data center and is not under the company’s physical control.</span></span>

### <a name="company-goal"></a><span data-ttu-id="25b6e-123">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="25b6e-123">Company goal</span></span>

<span data-ttu-id="25b6e-124">Como parte de una estrategia de seguridad de defensa en profundidad de varias capas, el objetivo de la empresa es garantizar que todos los orígenes de datos que contienen datos personales están cifrados, incluidos aquellos que se encuentran en el almacenamiento en la nube.</span><span class="sxs-lookup"><span data-stu-id="25b6e-124">As part of a multi-layered defense-in-depth security strategy, it is a company goal to ensure that all data sources that contain personal data are encrypted, including those residing in cloud storage.</span></span> <span data-ttu-id="25b6e-125">Si personas no autorizadas logran acceder a los datos personales, estos deben resultar ilegibles.</span><span class="sxs-lookup"><span data-stu-id="25b6e-125">If unauthorized persons gain access to the personal data, it must be in a form that will render it unreadable.</span></span> <span data-ttu-id="25b6e-126">La aplicación del cifrado debería ser fácil y transparente tanto para los usuarios como para los administradores.</span><span class="sxs-lookup"><span data-stu-id="25b6e-126">Applying encryption should be easy, or transparent – for users and administrators.</span></span>

## <a name="solutions"></a><span data-ttu-id="25b6e-127">Soluciones</span><span class="sxs-lookup"><span data-stu-id="25b6e-127">Solutions</span></span>

<span data-ttu-id="25b6e-128">Los servicios de Azure proporcionan varias herramientas y tecnologías para ayudarle a proteger datos personales en reposo mediante el cifrado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-128">Azure services provide multiple tools and technologies to help you protect personal data at rest by encrypting it.</span></span>

### <a name="azure-key-vault"></a><span data-ttu-id="25b6e-129">Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="25b6e-129">Azure Key Vault</span></span>

<span data-ttu-id="25b6e-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) ofrece un almacenamiento seguro para las claves utilizadas para cifrar los datos en reposo de los servicios de Azure y es la solución de almacenamiento y administración de claves recomendada.</span><span class="sxs-lookup"><span data-stu-id="25b6e-130">[Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) provides secure storage for the keys used to encrypt data at rest in Azure services and is the recommended key storage and management solution.</span></span> <span data-ttu-id="25b6e-131">La administración de claves de cifrado es esencial para proteger los datos almacenados.</span><span class="sxs-lookup"><span data-stu-id="25b6e-131">Encryption key management is essential to securing stored data.</span></span>

#### <a name="how-do-i-use-azure-key-vault-to-protect-keys-that-encrypt-personal-data"></a><span data-ttu-id="25b6e-132">¿Cómo se puede usar Azure Key Vault para proteger las claves que cifran los datos personales?</span><span class="sxs-lookup"><span data-stu-id="25b6e-132">How do I use Azure Key Vault to protect keys that encrypt personal data?</span></span>

<span data-ttu-id="25b6e-133">Para usar Azure Key Vault, necesita una suscripción a una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b6e-133">To use Azure Key Vault, you need a subscription to an Azure account.</span></span> <span data-ttu-id="25b6e-134">También necesita tener Azure Powershell instalado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-134">You also need Azure PowerShell installed.</span></span> <span data-ttu-id="25b6e-135">Los pasos incluyen el uso de cmdlets de PowerShell para hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="25b6e-135">Steps include using PowerShell cmdlets to do the following:</span></span>

1. <span data-ttu-id="25b6e-136">Conectarse a sus suscripciones</span><span class="sxs-lookup"><span data-stu-id="25b6e-136">Connect to your subscriptions</span></span>

2. <span data-ttu-id="25b6e-137">Creación de un Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="25b6e-137">Create a key vault</span></span>

3. <span data-ttu-id="25b6e-138">Adición de una clave o un secreto al Almacén de claves</span><span class="sxs-lookup"><span data-stu-id="25b6e-138">Add a key or secret to the key vault</span></span>

4. <span data-ttu-id="25b6e-139">Registrar las aplicaciones que va a usar el almacén de claves con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="25b6e-139">Register applications that will use the key vault with Azure Active Directory</span></span>

5. <span data-ttu-id="25b6e-140">Autorizar las aplicaciones que van a usar la clave o el secreto</span><span class="sxs-lookup"><span data-stu-id="25b6e-140">Authorize the applications to use the key or secret</span></span>

<span data-ttu-id="25b6e-141">Para crear un almacén de claves, use el cmdlet New-AzureRmKeyVault de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25b6e-141">To create a key vault, use the New-AzureRmKeyVault PowerShell CmDlt.</span></span> <span data-ttu-id="25b6e-142">Asignará un nombre de almacén, un nombre de grupo de recursos y una ubicación geográfica.</span><span class="sxs-lookup"><span data-stu-id="25b6e-142">You will assign a vault name, resource group name, and geographic location.</span></span> <span data-ttu-id="25b6e-143">Deberá usar el nombre de almacén al administrar claves mediante otros cmdlets.</span><span class="sxs-lookup"><span data-stu-id="25b6e-143">You’ll use the vault name when managing keys via other Cmdlets.</span></span> <span data-ttu-id="25b6e-144">Las aplicaciones que usen el almacén a través de la API de REST utilizarán el URI de este.</span><span class="sxs-lookup"><span data-stu-id="25b6e-144">Applications that use the vault through the REST API will use the vault URI.</span></span>

<span data-ttu-id="25b6e-145">Azure Key Vault puede proporcionar una clave protegida mediante software o importar una clave ya existente de un archivo .PFX.</span><span class="sxs-lookup"><span data-stu-id="25b6e-145">Azure Key Vault can provide a software-protected key for you, or you can import an existing key in a .PFX file.</span></span> <span data-ttu-id="25b6e-146">También puede almacenar secretos (contraseñas) en el almacén.</span><span class="sxs-lookup"><span data-stu-id="25b6e-146">You can also store secrets (passwords) in the vault.</span></span>

<span data-ttu-id="25b6e-147">También puede generar una clave en el HSM local y transferirla al HSM del servicio Key Vault, sin que la clave salga del límite del HSM.</span><span class="sxs-lookup"><span data-stu-id="25b6e-147">You can also generate a key in your local HSM and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary.</span></span>

<span data-ttu-id="25b6e-148">Para obtener instrucciones detalladas sobre cómo usar Azure Key Vault, siga los pasos descritos en [Introducción a Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span><span class="sxs-lookup"><span data-stu-id="25b6e-148">For detailed instructions on using Azure Key Vault, follow the steps in [Get Started with Azure Key Vault.](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-get-started)</span></span>

<span data-ttu-id="25b6e-149">Para obtener una lista de cmdlets de PowerShell que se usan con Azure Key Vault, consulte [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span><span class="sxs-lookup"><span data-stu-id="25b6e-149">For a list of PowerShell Cmdlets used with Azure Key Vault, see [AzureRM.KeyVault](https://docs.microsoft.com/en-us/powershell/module/azurerm.keyvault/?view=azurermps-4.2.0).</span></span>

### <a name="azure-disk-encryption-for-windows"></a><span data-ttu-id="25b6e-150">Azure Disk Encryption para Windows</span><span class="sxs-lookup"><span data-stu-id="25b6e-150">Azure Disk Encryption for Windows</span></span>

<span data-ttu-id="25b6e-151">[Azure Disk Encryption para máquinas virtuales de IaaS de Windows y Linux](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protege los datos personales en reposo en las máquinas virtuales de Azure y se integra con Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="25b6e-151">[Azure Disk Encryption for Windows and Linux IaaS VMs](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) protects personal data at rest on Azure virtual machines and integrates with Azure Key Vault.</span></span> <span data-ttu-id="25b6e-152">Azure Disk Encryption usa [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) en Windows y [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) en Linux para cifrar tanto el sistema operativo como los discos de datos.</span><span class="sxs-lookup"><span data-stu-id="25b6e-152">Azure Disk Encryption uses [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) in Windows and [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) in Linux to encrypt both the OS and the data disks.</span></span> <span data-ttu-id="25b6e-153">Azure Disk Encryption es compatible con Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, y con clientes de Windows 8 y Windows 10.</span><span class="sxs-lookup"><span data-stu-id="25b6e-153">Azure Disk Encryption is supported on Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, and on Windows 8 and Windows 10 clients.</span></span>

#### <a name="how-do-i-use-azure-disk-encryption-to-protect-personal-data"></a><span data-ttu-id="25b6e-154">¿Cómo se puede usar Azure Disk Encryption para proteger los datos personales?</span><span class="sxs-lookup"><span data-stu-id="25b6e-154">How do I use Azure Disk Encryption to protect personal data?</span></span>

<span data-ttu-id="25b6e-155">Para usar Azure Disk Encryption, necesita una suscripción a una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b6e-155">To use Azure Disk Encryption, you need a subscription to an Azure account.</span></span> <span data-ttu-id="25b6e-156">Para habilitar Azure Disk Encryption para máquinas virtuales con Windows y Linux, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="25b6e-156">To enable Azure Disk Encryption for Windows and Linux VMs, do the following:</span></span>

1. <span data-ttu-id="25b6e-157">Use la plantilla de Resource Manager de Azure Disk Encryption, PowerShell o la interfaz de la línea de comandos (CLI) para habilitar el cifrado de disco y especificar la configuración del cifrado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-157">Use the Azure Disk Encryption Resource Manager template, PowerShell, or the command line interface (CLI) to enable disk encryption and specify the  encryption configuration.</span></span> 

2. <span data-ttu-id="25b6e-158">Conceda acceso a la plataforma de Azure para leer el material de cifrado desde el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="25b6e-158">Grant access to the Azure platform to read the encryption material from your key vault.</span></span>

3. <span data-ttu-id="25b6e-159">Proporcione una identidad de aplicación de Azure Active Directory (AAD) para escribir el material de clave de cifrado en su almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="25b6e-159">Provide an Azure Active Directory (AAD) application identity to write the encryption key material to your key vault.</span></span>

<span data-ttu-id="25b6e-160">Azure actualizará la máquina virtual y la configuración del almacén de claves y configurará la máquina virtual cifrada.</span><span class="sxs-lookup"><span data-stu-id="25b6e-160">Azure will update the VM and the key vault configuration, and set up your encrypted VM.</span></span>

<span data-ttu-id="25b6e-161">Al configurar el almacén de claves para que sea compatible con Azure Disk Encryption, puede agregar una clave de cifrado de claves (KEK) para una mayor seguridad y para que admita la copia de seguridad de máquinas virtuales cifradas.</span><span class="sxs-lookup"><span data-stu-id="25b6e-161">When you set up your key vault to support Azure Disk Encryption, you can add a key encryption key (KEK) for added security and to support backup of encrypted virtual machines.</span></span>

![](media/protect-personal-data-at-rest/create-key.png)

<span data-ttu-id="25b6e-162">En [Azure Disk Encryption para máquinas virtuales IaaS Linux y Windows](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) puede encontrar instrucciones detalladas sobre escenarios de implementación y experiencias de usuario específicas.</span><span class="sxs-lookup"><span data-stu-id="25b6e-162">Detailed instructions for specific deployment scenarios and user experiences are included in [Azure Disk Encryption for Windows and Linux IaaS VMs.](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)</span></span>

### <a name="azure-storage-service-encryption"></a><span data-ttu-id="25b6e-163">Cifrado del servicio Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25b6e-163">Azure Storage Service Encryption</span></span>

<span data-ttu-id="25b6e-164">[Cifrado del servicio Azure Storage (SSE) para datos en reposo](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) le ayuda a asegurar y proteger sus datos con el fin de cumplir con los compromisos de cumplimiento y seguridad de su organización.</span><span class="sxs-lookup"><span data-stu-id="25b6e-164">[Azure Storage Service Encryption (SSE) for Data at Rest](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) helps you protect and safeguard your data to meet your organizational security and compliance commitments.</span></span> <span data-ttu-id="25b6e-165">Azure Storage cifra automáticamente sus datos mediante cifrado AES de 256-bits antes de continuar al almacenamiento y los descifra antes de la recuperación.</span><span class="sxs-lookup"><span data-stu-id="25b6e-165">Azure Storage automatically encrypts your data using 256-bit AES encryption prior to persisting to storage, and decrypts it prior to retrieval.</span></span> <span data-ttu-id="25b6e-166">Este servicio está disponible para los archivos y blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b6e-166">This service is available for Azure Blobs and Files.</span></span>

#### <a name="how-do-i-use-storage-service-encryption-to-protect-personal-data"></a><span data-ttu-id="25b6e-167">¿Cómo se puede usar Cifrado del servicio Azure Storage para proteger los datos personales?</span><span class="sxs-lookup"><span data-stu-id="25b6e-167">How do I use Storage Service Encryption to protect personal data?</span></span>

<span data-ttu-id="25b6e-168">Para habilitar Cifrado del servicio Azure Storage, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="25b6e-168">To enable Storage Service Encryption, do the following:</span></span>

1. <span data-ttu-id="25b6e-169">Inicie sesión en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="25b6e-169">Log into the Azure portal.</span></span>

2. <span data-ttu-id="25b6e-170">Seleccione una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="25b6e-170">Select a storage account.</span></span>

3. <span data-ttu-id="25b6e-171">En Configuración, en la sección Blob service, seleccione Cifrado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-171">In Settings, under the Blob Service section, select Encryption.</span></span>

4. <span data-ttu-id="25b6e-172">En la sección Servicio Archivo, seleccione Cifrado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-172">Under the File Service section, select Encryption.</span></span>

<span data-ttu-id="25b6e-173">Una vez que haga clic en la configuración de cifrado, puede habilitar o deshabilitar Cifrado del servicio de Almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="25b6e-173">After you click the Encryption setting, you can enable or disable Storage Service Encryption.</span></span>

![](media/protect-personal-data-at-rest/storage-service-encryption.png)

<span data-ttu-id="25b6e-174">Los datos nuevos se cifrarán.</span><span class="sxs-lookup"><span data-stu-id="25b6e-174">New data will be encrypted.</span></span> <span data-ttu-id="25b6e-175">Los datos en los archivos ya existentes de esta cuenta de almacenamiento permanecerán sin cifrar.</span><span class="sxs-lookup"><span data-stu-id="25b6e-175">Data in existing files in this storage account will remain unencrypted.</span></span>

<span data-ttu-id="25b6e-176">Después de habilitar el cifrado, copie datos en la cuenta de almacenamiento mediante uno de los métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="25b6e-176">After enabling encryption, copy data to the storage account using one of the following methods:</span></span>

1. <span data-ttu-id="25b6e-177">Copie los blobs o archivos con la [utilidad de línea de comandos AzCopy](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span><span class="sxs-lookup"><span data-stu-id="25b6e-177">Copy blobs or files with the [AzCopy Command Line utility](https://docs.microsoft.com/en-us/azure/storage/storage-use-azcopy).</span></span>

2. <span data-ttu-id="25b6e-178">[Monte un recurso compartido de archivos mediante SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) para que pueda usar una utilidad como Robocopy para copiar archivos.</span><span class="sxs-lookup"><span data-stu-id="25b6e-178">[Mount a file share using SMB](https://docs.microsoft.com/en-us/azure/storage/storage-file-how-to-use-files-windows) so you can use a utility such as Robocopy to copy files.</span></span>

3. <span data-ttu-id="25b6e-179">Copie los datos de blobs o archivos en Blob Storage y desde este, o entre cuentas de almacenamiento mediante las [bibliotecas de cliente de Storage, como .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span><span class="sxs-lookup"><span data-stu-id="25b6e-179">Copy blob or file data to and from blob storage or between storage accounts using [Storage Client Libraries such as .NET](https://docs.microsoft.com/en-us/azure/storage/storage-dotnet-how-to-use-blobs).</span></span>

4.  <span data-ttu-id="25b6e-180">Use un [Explorador de almacenamiento](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) para cargar blobs a su cuenta de almacenamiento con cifrado habilitado.</span><span class="sxs-lookup"><span data-stu-id="25b6e-180">Use a [Storage Explorer](https://docs.microsoft.com/en-us/azure/storage/storage-explorers) to upload blobs to your storage account with encryption enabled.</span></span>

### <a name="transparent-data-encryption"></a><span data-ttu-id="25b6e-181">Cifrado de datos transparente</span><span class="sxs-lookup"><span data-stu-id="25b6e-181">Transparent Data Encryption</span></span>

<span data-ttu-id="25b6e-182">Cifrado de datos transparente (TDE) es una característica de SQL Azure mediante la cual puede cifrar los datos en los niveles de la base de datos y el servidor.</span><span class="sxs-lookup"><span data-stu-id="25b6e-182">Transparent Data Encryption (TDE) is a feature in SQL Azure by which you can encrypt data at both the database and server levels.</span></span> <span data-ttu-id="25b6e-183">TDE ahora está habilitado de forma predeterminada en todas las bases de datos recién creadas.</span><span class="sxs-lookup"><span data-stu-id="25b6e-183">TDE is now enabled by default on all newly created databases.</span></span> <span data-ttu-id="25b6e-184">TDE realiza el cifrado y descifrado de E/S en tiempo real de los archivos de datos y de registro.</span><span class="sxs-lookup"><span data-stu-id="25b6e-184">TDE performs real-time I/O encryption and decryption of the data and log files.</span></span>

#### <a name="how-do-i-use-tde-to-protect-personal-data"></a><span data-ttu-id="25b6e-185">¿Cómo se usa TDE para proteger los datos personales?</span><span class="sxs-lookup"><span data-stu-id="25b6e-185">How do I use TDE to protect personal data?</span></span>

<span data-ttu-id="25b6e-186">Puede configurar TDE a través de Azure Portal, mediante el uso de la API de REST o mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25b6e-186">You can configure TDE through the Azure portal, by using the REST API, or by using PowerShell.</span></span> <span data-ttu-id="25b6e-187">Para habilitar TDE en una base de datos existente mediante Azure Portal, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="25b6e-187">To enable TDE on an existing database using the Azure Portal, do the following:</span></span>

1. <span data-ttu-id="25b6e-188">Visite Azure Portal en <https://portal.azure.com> e inicie sesión con su cuenta de administrador o colaborador de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b6e-188">Visit the Azure portal at <https://portal.azure.com> and sign-in with your Azure Administrator or Contributor account.</span></span>

2. <span data-ttu-id="25b6e-189">En el encabezado de la izquierda, haga clic en EXAMINAR y, a continuación, haga clic en bases de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="25b6e-189">On the left banner, click to BROWSE, and then click SQL databases.</span></span>

3. <span data-ttu-id="25b6e-190">Con las bases de datos SQL seleccionadas en el panel izquierdo, haga clic en la base de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="25b6e-190">With SQL databases selected in the left pane, click your user database.</span></span>

4. <span data-ttu-id="25b6e-191">En la hoja de la base de datos, haga clic en Toda la configuración.</span><span class="sxs-lookup"><span data-stu-id="25b6e-191">In the database blade, click All settings.</span></span>

5. <span data-ttu-id="25b6e-192">En la hoja de configuración, haga clic en la parte de Cifrado de datos transparente para abrir la hoja correspondiente.</span><span class="sxs-lookup"><span data-stu-id="25b6e-192">In the Settings blade, click Transparent data encryption part to open the Transparent data encryption blade.</span></span>

6. <span data-ttu-id="25b6e-193">En la hoja de cifrado de datos, mueva el botón de cifrado de datos a On y, a continuación, haga clic en Guardar (en la parte superior de la página) para aplicar la configuración.</span><span class="sxs-lookup"><span data-stu-id="25b6e-193">In the Data encryption blade, move the Data encryption button to On, and then click Save (at the top of the page) to apply the setting.</span></span> <span data-ttu-id="25b6e-194">El estado de cifrado será aproximadamente el mismo que el progreso del cifrado de datos transparente.</span><span class="sxs-lookup"><span data-stu-id="25b6e-194">The Encryption status will approximate the progress of the transparent data encryption.</span></span>

![Habilitar el cifrado de datos](media/protect-personal-data-at-rest/turn-data-encryption-on.png)

<span data-ttu-id="25b6e-196">Puede encontrar instrucciones sobre cómo habilitar TDE y obtener información acerca de cómo descifrar las bases de datos protegidas por TDE y mucho más en el artículo [Cifrado de datos transparente con Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span><span class="sxs-lookup"><span data-stu-id="25b6e-196">Instructions on how to enable TDE and information on decrypting TDE-protected databases and more can be found in the article [Transparent Data Encryption with Azure SQL Database.](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database)</span></span>

## <a name="summary"></a><span data-ttu-id="25b6e-197">Resumen</span><span class="sxs-lookup"><span data-stu-id="25b6e-197">Summary</span></span>

<span data-ttu-id="25b6e-198">La compañía puede lograr su objetivo de cifrar datos personales almacenados en la nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="25b6e-198">The company can accomplish its goal of encrypting personal data stored in the Azure cloud.</span></span> <span data-ttu-id="25b6e-199">Puede hacerlo mediante Azure Disk Encryption para proteger volúmenes completos.</span><span class="sxs-lookup"><span data-stu-id="25b6e-199">They can do this by using Azure Disk Encryption to  protect entire volumes.</span></span> <span data-ttu-id="25b6e-200">Esto incluye los archivos del sistema operativo y los archivos de datos que contienen información de identificación personal y otros datos confidenciales.</span><span class="sxs-lookup"><span data-stu-id="25b6e-200">This may include both the operating system files and data files that hold personal identifiable information and other sensitive data.</span></span> <span data-ttu-id="25b6e-201">Cifrado del servicio Azure Storage puede utilizarse para proteger los datos personales que se almacenan en archivos y blobs.</span><span class="sxs-lookup"><span data-stu-id="25b6e-201">Azure Storage Service encryption can be used to protect personal data that is stored in blobs and files.</span></span> <span data-ttu-id="25b6e-202">Para los datos que se almacenan en instancias de Azure SQL Database, el cifrado de datos transparente ofrece protección frente a una exposición no autorizada de información personal.</span><span class="sxs-lookup"><span data-stu-id="25b6e-202">For data that is stored in Azure SQL databases, Transparent Data Encryption provides protection from unauthorized exposure of personal information.</span></span>

<span data-ttu-id="25b6e-203">Para proteger las claves que se usan para cifrar los datos de Azure, la empresa puede usar Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="25b6e-203">To protect the keys that are used to encrypt data in Azure, the company can use Azure Key Vault.</span></span> <span data-ttu-id="25b6e-204">Este agiliza el proceso de administración de claves y permite a la empresa mantener el control de claves que obtienen acceso a los datos personales y los cifran.</span><span class="sxs-lookup"><span data-stu-id="25b6e-204">This streamlines the key management process and enables the company to maintain control of keys that access and encrypt personal data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="25b6e-205">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="25b6e-205">Next steps</span></span>

- [<span data-ttu-id="25b6e-206">Guía de solución de problemas de Azure Disk Encryption</span><span class="sxs-lookup"><span data-stu-id="25b6e-206">Azure Disk Encryption Troubleshooting Guide</span></span>](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-tsg)

- [<span data-ttu-id="25b6e-207">Cifrado de una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="25b6e-207">Encrypt an Azure Virtual Machine</span></span>](https://docs.microsoft.com/en-us/azure/security-center/security-center-disk-encryption?toc=%2fazure%2fsecurity%2ftoc.json)

- [<span data-ttu-id="25b6e-208">Cifrado de datos en Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="25b6e-208">Encryption of data in Azure Data Lake Store</span></span>](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption)

- [<span data-ttu-id="25b6e-209">Cifrado de base de datos en reposo en Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="25b6e-209">Azure Cosmos DB database encryption at rest</span></span>](https://docs.microsoft.com/en-us/azure/cosmos-db/database-encryption-at-rest)
