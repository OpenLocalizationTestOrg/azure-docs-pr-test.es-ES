---
title: "Cómo generar y transferir claves protegidas con HSM para Azure Key Vault | Microsoft Docs"
description: "Use este artículo para ayudarle a planear, generar y, a continuación, transfiera sus propias claves protegidas con HSM para utilizar con el Almacén de clave de Azure. También se denomina BYOK o \"traiga su propia clave\"."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 5dbee1221f64045c64fecb344de1e03b2183dfb1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-generate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="efe19-104">Generación y transferencia de claves protegidas con HSM para el Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-104">How to generate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="efe19-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="efe19-105">Introduction</span></span>
<span data-ttu-id="efe19-106">Para obtener una mayor seguridad, cuando utilice el Almacén de claves de Azure, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no se salen nunca del límite de los HSM.</span><span class="sxs-lookup"><span data-stu-id="efe19-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="efe19-107">Con frecuencia este escenario se conoce también como *Aportar tu propia clave*, o BYOK.</span><span class="sxs-lookup"><span data-stu-id="efe19-107">This scenario is often referred to as *bring your own key*, or BYOK.</span></span> <span data-ttu-id="efe19-108">Los HSM tienen la validación FIPS 140-2 de nivel 2.</span><span class="sxs-lookup"><span data-stu-id="efe19-108">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="efe19-109">El Almacén de claves de Azure usa la familia Thales nShield de HSM para proteger sus claves.</span><span class="sxs-lookup"><span data-stu-id="efe19-109">Azure Key Vault uses Thales nShield family of HSMs to protect your keys.</span></span>

<span data-ttu-id="efe19-110">La información de este tema le ayudará a planear, generar y transferir sus propias claves protegidas con HSM para utilizarlas en Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="efe19-110">Use the information in this topic to help you plan for, generate, and then transfer your own HSM-protected keys to use with Azure Key Vault.</span></span>

<span data-ttu-id="efe19-111">Esta funcionalidad no está disponible para Azure China.</span><span class="sxs-lookup"><span data-stu-id="efe19-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="efe19-112">Para obtener más información sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de claves de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="efe19-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="efe19-113">Para ver tutorial introductorio, que incluye la creación de un almacén de claves para claves protegidas con HSM, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="efe19-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="efe19-114">Obtenga más información acerca de cómo generar y transferir una clave protegida con HSM a través de Internet:</span><span class="sxs-lookup"><span data-stu-id="efe19-114">More information about generating and transferring an HSM-protected key over the Internet:</span></span>

* <span data-ttu-id="efe19-115">Genere la clave desde una estación de trabajo sin conexión, lo que reduce la superficie de ataque.</span><span class="sxs-lookup"><span data-stu-id="efe19-115">You generate the key from an offline workstation, which reduces the attack surface.</span></span>
* <span data-ttu-id="efe19-116">La clave se cifra con una clave de intercambio de claves (KEK), que permanece cifrada hasta que se transfiere a los HSM del Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-116">The key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred to the Azure Key Vault HSMs.</span></span> <span data-ttu-id="efe19-117">Solo la versión cifrada de la clave deja la estación de trabajo original.</span><span class="sxs-lookup"><span data-stu-id="efe19-117">Only the encrypted version of your key leaves the original workstation.</span></span>
* <span data-ttu-id="efe19-118">El conjunto de herramientas establece las propiedades en su clave de inquilino que enlaza la clave con el espacio de seguridad del Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-118">The toolset sets properties on your tenant key that binds your key to the Azure Key Vault security world.</span></span> <span data-ttu-id="efe19-119">Por consiguiente, después de que los HSM del Almacén de claves de Azure reciban y descifren la clave, dichos HSM son los únicos los que puedan usarla.</span><span class="sxs-lookup"><span data-stu-id="efe19-119">So after the Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="efe19-120">La clave no se puede exportar.</span><span class="sxs-lookup"><span data-stu-id="efe19-120">Your key cannot be exported.</span></span> <span data-ttu-id="efe19-121">Este enlace lo exigen los HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-121">This binding is enforced by the Thales HSMs.</span></span>
* <span data-ttu-id="efe19-122">La clave de intercambio de claves (KEK) que se utiliza para cifrar la clave se genera dentro de los HSM del Almacén de clave de Azure y no es exportable.</span><span class="sxs-lookup"><span data-stu-id="efe19-122">The Key Exchange Key (KEK) that is used to encrypt your key is generated inside the Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="efe19-123">Los HSM exigen que no pueda haber una versión sin cifrar de la KEK fuera de los HSM.</span><span class="sxs-lookup"><span data-stu-id="efe19-123">The HSMs enforce that there can be no clear version of the KEK outside the HSMs.</span></span> <span data-ttu-id="efe19-124">Además, el conjunto de herramientas incluye la atestación desde Thales de que la KEK no es exportable y se generó dentro de un HSM genuino que fabricó Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-124">In addition, the toolset includes attestation from Thales that the KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="efe19-125">El conjunto de herramientas incluye la atestación desde Thales de que el espacio de seguridad del Almacén de claves de Azure también se generó en un HSM genuino que fabricó Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-125">The toolset includes attestation from Thales that the Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="efe19-126">Esta certificación demuestra que Microsoft usa hardware original.</span><span class="sxs-lookup"><span data-stu-id="efe19-126">This attestation proves to you that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="efe19-127">Microsoft usa KEK independientes y separa los espacios de seguridad de las distintas regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="efe19-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="efe19-128">Esta separación garantiza que la clave puede utilizarse únicamente en centros de datos de la región en la que se ha cifrado.</span><span class="sxs-lookup"><span data-stu-id="efe19-128">This separation ensures that your key can be used only in data centers in the region in which you encrypted it.</span></span> <span data-ttu-id="efe19-129">Por ejemplo, una clave de un cliente europeo no se puede utilizar en centros de datos de América del Norte o Asia.</span><span class="sxs-lookup"><span data-stu-id="efe19-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="efe19-130">Más información acerca de los HSM de Thales y los servicios de Microsoft</span><span class="sxs-lookup"><span data-stu-id="efe19-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="efe19-131">Thales e-Security es uno de los principales proveedores mundiales de soluciones de cifrado de datos y ciberseguridad para servicios financieros, tecnología punta, industria manufacturera, gobierno y sectores tecnológicos.</span><span class="sxs-lookup"><span data-stu-id="efe19-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions to the financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="efe19-132">Las soluciones de Thales cuentan con una trayectoria de 40 años en la protección de información corporativa y gubernamental, y las usan cuatro de las cinco mayores compañías de los sectores energético y aeroespacial.</span><span class="sxs-lookup"><span data-stu-id="efe19-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of the five largest energy and aerospace companies.</span></span> <span data-ttu-id="efe19-133">También las utilizan 22 países de la OTAN y protegen más del 80 por ciento de las transacciones de pago mundiales.</span><span class="sxs-lookup"><span data-stu-id="efe19-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="efe19-134">Microsoft ha colaborado con Thales para mejorar la tecnología de vanguardia de los HSM.</span><span class="sxs-lookup"><span data-stu-id="efe19-134">Microsoft has collaborated with Thales to enhance the state of art for HSMs.</span></span> <span data-ttu-id="efe19-135">Estas mejoras te permiten obtener los beneficios típicos de los servicios hospedados sin tener que renunciar al control de las claves.</span><span class="sxs-lookup"><span data-stu-id="efe19-135">These enhancements enable you to get the typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="efe19-136">En concreto, estas mejoras permiten que Microsoft administre los HSM para que no lo tengan que hacer sus usuarios.</span><span class="sxs-lookup"><span data-stu-id="efe19-136">Specifically, these enhancements let Microsoft manage the HSMs so that you do not have to.</span></span> <span data-ttu-id="efe19-137">Al ser un servicio en la nube, el Almacén de claves de Azure se escala verticalmente en muy poco tiempo para cubrir los picos de uso de cualquier organización.</span><span class="sxs-lookup"><span data-stu-id="efe19-137">As a cloud service, Azure Key Vault scales up at short notice to meet your organization’s usage spikes.</span></span> <span data-ttu-id="efe19-138">Al mismo tiempo, la clave está protegida dentro de los HSM de Microsoft y se conserva el control sobre su ciclo de vida, ya que es el usuario el que genera la clave y la transfiere a los HSM de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="efe19-138">At the same time, your key is protected inside Microsoft’s HSMs: You retain control over the key lifecycle because you generate the key and transfer it to Microsoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="efe19-139">Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="efe19-140">Utilice la siguiente información y procedimientos si va a generar su propia clave protegida con HSM y, a continuación, va a transferirla al Almacén de claves de Azure, el escenario de Aportar tu propia clave (BYOK).</span><span class="sxs-lookup"><span data-stu-id="efe19-140">Use the following information and procedures if you will generate your own HSM-protected key and then transfer it to Azure Key Vault—the bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="efe19-141">Requisitos previos de BYOK</span><span class="sxs-lookup"><span data-stu-id="efe19-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="efe19-142">En la tabla siguiente puede ver una lista de los requisitos previos del método Aportar tu propia clave (BYOK) para el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-142">See the following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="efe19-143">Requisito</span><span class="sxs-lookup"><span data-stu-id="efe19-143">Requirement</span></span> | <span data-ttu-id="efe19-144">Más información</span><span class="sxs-lookup"><span data-stu-id="efe19-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="efe19-145">Una suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-145">A subscription to Azure</span></span> |<span data-ttu-id="efe19-146">Para crear un Almacén de claves de Azure, se necesita una suscripción a Azure: [Regístrese para obtener la versión de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="efe19-146">To create an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="efe19-147">Nivel de servicio Premium de Azure Key Vault, que admita claves protegidas con HSM</span><span class="sxs-lookup"><span data-stu-id="efe19-147">The Azure Key Vault Premium service tier to support HSM-protected keys</span></span> |<span data-ttu-id="efe19-148">Para obtener más información sobre los niveles de servicio y las capacidades del Almacén de claves de Azure, consulte el sitio web [Precios de Almacén de claves](https://azure.microsoft.com/pricing/details/key-vault/) .</span><span class="sxs-lookup"><span data-stu-id="efe19-148">For more information about the service tiers and capabilities for Azure Key Vault, see the [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="efe19-149">HSM de Thales, tarjetas inteligentes y software compatible</span><span class="sxs-lookup"><span data-stu-id="efe19-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="efe19-150">Debe tener acceso al módulo de seguridad de hardware de Thales y al conocimiento operacional básico de los HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-150">You must have access to a Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="efe19-151">Para ver la lista de modelos compatibles o comprar un HSM, consulte [Módulo de seguridad de hardware de Thales](https://www.thales-esecurity.com/msrms/buy) .</span><span class="sxs-lookup"><span data-stu-id="efe19-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for the list of compatible models, or to purchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="efe19-152">El siguiente hardware y software:</span><span class="sxs-lookup"><span data-stu-id="efe19-152">The following hardware and software:</span></span><ol><li><span data-ttu-id="efe19-153">Una estación de trabajo x64 sin conexión con un sistema operativo Windows 7 y software Thales nShield versión 11.50 o superior.</span><span class="sxs-lookup"><span data-stu-id="efe19-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="efe19-154">Si esta estación de trabajo ejecuta Windows 7, debe [instalar Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="efe19-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="efe19-155">Una estación de trabajo conectada a Internet y con un sistema operativo Windows 7 como mínimo y [Azure PowerShell](/powershell/azure/overview)  **con al menos la versión 1.1.0**  instalada.</span><span class="sxs-lookup"><span data-stu-id="efe19-155">A workstation that is connected to the Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="efe19-156">Una unidad USB u otro dispositivo de almacenamiento portátil con al menos 16 MB de espacio libre.</span><span class="sxs-lookup"><span data-stu-id="efe19-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="efe19-157">Por seguridad, se recomienda que la primera estación de trabajo no esté conectada a una red.</span><span class="sxs-lookup"><span data-stu-id="efe19-157">For security reasons, we recommend that the first workstation is not connected to a network.</span></span> <span data-ttu-id="efe19-158">Sin embargo, esta recomendación no es de obligado cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="efe19-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="efe19-159">Tenga en cuenta que en las instrucciones siguientes, esta estación de trabajo se conoce como la desconectada.</span><span class="sxs-lookup"><span data-stu-id="efe19-159">Note that in the instructions that follow, this workstation is referred to as the disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="efe19-160">Además, si la clave de inquilino es para una red de producción, se recomienda usar una segunda estación de trabajo independiente para descargar el conjunto de herramientas y cargar la clave de inquilino.</span><span class="sxs-lookup"><span data-stu-id="efe19-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation to download the toolset and upload the tenant key.</span></span> <span data-ttu-id="efe19-161">Sin embargo, para la prueba puede usar la misma estación de trabajo que la primera.</span><span class="sxs-lookup"><span data-stu-id="efe19-161">But for testing purposes, you can use the same workstation as the first one.</span></span><br/><br/><span data-ttu-id="efe19-162">Tenga en cuenta que en las instrucciones siguientes, la segunda estación de trabajo se conoce como la que está conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="efe19-162">Note that in the instructions that follow, this second workstation is referred to as the Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-to-azure-key-vault-hsm"></a><span data-ttu-id="efe19-163">Generación y transferencia de una clave a un HSM del Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-163">Generate and transfer your key to Azure Key Vault HSM</span></span>
<span data-ttu-id="efe19-164">Los cinco pasos siguientes sirven para generar y transferir la clave a un HSM de Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="efe19-164">You will use the following five steps to generate and transfer your key to an Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="efe19-165">Paso 1: preparación de la estación de trabajo conectada a Internet</span><span class="sxs-lookup"><span data-stu-id="efe19-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="efe19-166">Paso 2: preparación de la estación de trabajo desconectada</span><span class="sxs-lookup"><span data-stu-id="efe19-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="efe19-167">Paso 3: generación de la clave</span><span class="sxs-lookup"><span data-stu-id="efe19-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="efe19-168">Paso 4: preparación de la clave para la transferencia</span><span class="sxs-lookup"><span data-stu-id="efe19-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="efe19-169">Paso 5: transferencia de la clave al Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-169">Step 5: Transfer your key to Azure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="efe19-170">Paso 1: preparación de la estación de trabajo conectada a Internet</span><span class="sxs-lookup"><span data-stu-id="efe19-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="efe19-171">En este primer paso, realice los siguientes procedimientos en la estación de trabajo conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="efe19-171">For this first step, do the following procedures on your workstation that is connected to the Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="efe19-172">Paso 1.1: instalación de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="efe19-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="efe19-173">Desde la estación de trabajo conectada a Internet, descargue e instale el módulo de Azure PowerShell que incluye los cmdlets para administrar el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-173">From the Internet-connected workstation, download and install the Azure PowerShell module that includes the cmdlets to manage Azure Key Vault.</span></span> <span data-ttu-id="efe19-174">Esto requiere una versión mínima de 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="efe19-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="efe19-175">Para ver las instrucciones de instalación, consulte [Cómo instalar y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="efe19-175">For installation instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="efe19-176">Paso 1.2: especificación del identificador de la suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="efe19-177">Inicie una sesión de Azure PowerShell e inicie sesión en su cuenta de Azure con el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="efe19-177">Start an Azure PowerShell session and sign in to your Azure account by using the following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="efe19-178">En la ventana emergente del explorador, escriba el nombre de usuario y la contraseña de su cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-178">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="efe19-179">A continuación, utilice el comando [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) :</span><span class="sxs-lookup"><span data-stu-id="efe19-179">Then, use the [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="efe19-180">En la salida, busque el identificador de la suscripción que va a utilizar para el Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-180">From the output, locate the ID for the subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="efe19-181">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="efe19-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="efe19-182">No cierre la ventana de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efe19-182">Do not close the Azure PowerShell window.</span></span>

### <a name="step-13-download-the-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="efe19-183">Paso 1.3: descarga del conjunto de herramientas BYOK para el Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-183">Step 1.3: Download the BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="efe19-184">Vaya al Centro de descarga de Microsoft y [descargue el conjunto de herramientas de BYOK para el Almacén de claves de Azure](http://www.microsoft.com/download/details.aspx?id=45345) de su región geográfica o instancia de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-184">Go to the Microsoft Download Center and [download the Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="efe19-185">Utilice la siguiente información para identificar el nombre del paquete para descargar y su hash de paquete SHA-256 correspondiente:</span><span class="sxs-lookup"><span data-stu-id="efe19-185">Use the following information to identify the package name to download and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="efe19-186">**Estados Unidos:**</span><span class="sxs-lookup"><span data-stu-id="efe19-186">**United States:**</span></span>

<span data-ttu-id="efe19-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="efe19-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="efe19-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="efe19-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="efe19-189">**Europe:**</span></span>

<span data-ttu-id="efe19-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="efe19-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="efe19-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="efe19-192">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="efe19-192">**Asia:**</span></span>

<span data-ttu-id="efe19-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="efe19-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="efe19-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="efe19-195">**América Latina:**</span><span class="sxs-lookup"><span data-stu-id="efe19-195">**Latin America:**</span></span>

<span data-ttu-id="efe19-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="efe19-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="efe19-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="efe19-198">**Japón:**</span><span class="sxs-lookup"><span data-stu-id="efe19-198">**Japan:**</span></span>

<span data-ttu-id="efe19-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="efe19-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="efe19-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="efe19-201">**Corea:**</span><span class="sxs-lookup"><span data-stu-id="efe19-201">**Korea:**</span></span>

<span data-ttu-id="efe19-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="efe19-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="efe19-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="efe19-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="efe19-204">**Australia:**</span></span>

<span data-ttu-id="efe19-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="efe19-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="efe19-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="efe19-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="efe19-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="efe19-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="efe19-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="efe19-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="efe19-210">**DoD del Gobierno de Estados Unidos:**</span><span class="sxs-lookup"><span data-stu-id="efe19-210">**US Government DOD:**</span></span>

<span data-ttu-id="efe19-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="efe19-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="efe19-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="efe19-213">**Canadá:**</span><span class="sxs-lookup"><span data-stu-id="efe19-213">**Canada:**</span></span>

<span data-ttu-id="efe19-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="efe19-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="efe19-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="efe19-216">**Alemania:**</span><span class="sxs-lookup"><span data-stu-id="efe19-216">**Germany:**</span></span>

<span data-ttu-id="efe19-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="efe19-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="efe19-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="efe19-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="efe19-219">**India:**</span></span>

<span data-ttu-id="efe19-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="efe19-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="efe19-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="efe19-222">**Reino Unido:**</span><span class="sxs-lookup"><span data-stu-id="efe19-222">**United Kingdom:**</span></span>

<span data-ttu-id="efe19-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="efe19-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="efe19-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="efe19-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="efe19-225">Para validar la integridad del conjunto de herramientas BYOK que descargó, use el cmdlet [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) en la sesión de Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="efe19-225">To validate the integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use the [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="efe19-226">El conjunto de herramientas incluye:</span><span class="sxs-lookup"><span data-stu-id="efe19-226">The toolset includes the following:</span></span>

* <span data-ttu-id="efe19-227">Un paquete de clave de intercambio de claves (KEK) cuyo nombre comienza por **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="efe19-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="efe19-228">Un paquete de espacio de seguridad cuyo nombre comienza por **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="efe19-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="efe19-229">Un script Python denominado **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="efe19-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="efe19-230">Un archivo ejecutable de línea de comandos denominado **KeyTransferRemote.exe** y asociado a las DLL.</span><span class="sxs-lookup"><span data-stu-id="efe19-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="efe19-231">Un paquete redistribuible de Visual C++ denominado **vcredist_x64.exe**.</span><span class="sxs-lookup"><span data-stu-id="efe19-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="efe19-232">Copie el paquete en una unidad USB u otro dispositivo de almacenamiento portátil.</span><span class="sxs-lookup"><span data-stu-id="efe19-232">Copy the package to a USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="efe19-233">Paso 2: preparación de la estación de trabajo desconectada</span><span class="sxs-lookup"><span data-stu-id="efe19-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="efe19-234">En este segundo paso, realice los siguientes procedimientos en la estación de trabajo que no está conectada a una red (Internet o la red interna).</span><span class="sxs-lookup"><span data-stu-id="efe19-234">For this second step, do the following procedures on the workstation that is not connected to a network (either the Internet or your internal network).</span></span>

### <a name="step-21-prepare-the-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="efe19-235">Paso 2.1: preparación de la estación de trabajo desconectada con HSM de Thales</span><span class="sxs-lookup"><span data-stu-id="efe19-235">Step 2.1: Prepare the disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="efe19-236">Instale el software nCipher (Thales) en un equipo de Windows y, a continuación, adjunte un HSM de Thales a dicho equipo.</span><span class="sxs-lookup"><span data-stu-id="efe19-236">Install the nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM to that computer.</span></span>

<span data-ttu-id="efe19-237">Asegúrese de que las herramientas de Thales estén en su ruta de acceso (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="efe19-237">Ensure that the Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="efe19-238">Por ejemplo, escriba lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="efe19-238">For example, type the following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="efe19-239">Para obtener más información, consulte el Manual del usuario que se incluye en el HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-239">For more information, see the user guide included with the Thales HSM.</span></span>

### <a name="step-22-install-the-byok-toolset-on-the-disconnected-workstation"></a><span data-ttu-id="efe19-240">Paso 2.2: instalación del conjunto de herramientas BYOK en la estación de trabajo desconectada</span><span class="sxs-lookup"><span data-stu-id="efe19-240">Step 2.2: Install the BYOK toolset on the disconnected workstation</span></span>
<span data-ttu-id="efe19-241">Copie el paquete del conjunto de herramientas BYOK de la unidad USB, u otro dispositivo de almacenamiento portátil, y, a continuación, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="efe19-241">Copy the BYOK toolset package from the USB drive or other portable storage, and then do the following:</span></span>

1. <span data-ttu-id="efe19-242">Extraiga los archivos del paquete descargado en cualquier carpeta.</span><span class="sxs-lookup"><span data-stu-id="efe19-242">Extract the files from the downloaded package into any folder.</span></span>
2. <span data-ttu-id="efe19-243">En esa carpeta, ejecute vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="efe19-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="efe19-244">Siga las instrucciones para instalar los componentes de tiempo de ejecución de Visual C++ para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="efe19-244">Follow the instructions to the install the Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="efe19-245">Paso 3: generación de la clave</span><span class="sxs-lookup"><span data-stu-id="efe19-245">Step 3: Generate your key</span></span>
<span data-ttu-id="efe19-246">En el tercer paso, realice los siguientes procedimientos en la estación de trabajo desconectada.</span><span class="sxs-lookup"><span data-stu-id="efe19-246">For this third step, do the following procedures on the disconnected workstation.</span></span> <span data-ttu-id="efe19-247">Para completar este paso, HSM debe estar en modo de inicialización.</span><span class="sxs-lookup"><span data-stu-id="efe19-247">To complete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-the-hsm-mode-to-i"></a><span data-ttu-id="efe19-248">Paso 3.1: cambio del modo HSM a "I"</span><span class="sxs-lookup"><span data-stu-id="efe19-248">Step 3.1: Change the HSM mode to 'I'</span></span>
<span data-ttu-id="efe19-249">Si está usando Thales nShield Edge, para cambiar el modo: 1.</span><span class="sxs-lookup"><span data-stu-id="efe19-249">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="efe19-250">Use el botón de modo para resaltar el modo requerido.</span><span class="sxs-lookup"><span data-stu-id="efe19-250">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="efe19-251">2.</span><span class="sxs-lookup"><span data-stu-id="efe19-251">2.</span></span> <span data-ttu-id="efe19-252">Después de un momento, mantenga presionado el botón Borrar durante un par de segundos.</span><span class="sxs-lookup"><span data-stu-id="efe19-252">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="efe19-253">Si el modo cambia, el LED del nuevo modo deja de parpadear y permanece encendido.</span><span class="sxs-lookup"><span data-stu-id="efe19-253">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="efe19-254">El LED del estado puede parpadear irregularmente durante algunos segundos y, luego, parpadea regularmente cuando el dispositivo está listo.</span><span class="sxs-lookup"><span data-stu-id="efe19-254">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="efe19-255">En caso contrario, el dispositivo permanece en el modo actual, con el modo correspondiente de LED encendido.</span><span class="sxs-lookup"><span data-stu-id="efe19-255">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="efe19-256">Paso 3.2: creación de un espacio de seguridad</span><span class="sxs-lookup"><span data-stu-id="efe19-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="efe19-257">Inicie un símbolo del sistema y ejecute el programa new-world de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-257">Start a command prompt and run the Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="efe19-258">Este programa crea un archivo de **espacio de seguridad** en %NFAST_KMDATA%\local\world, que corresponde a la carpeta C:\ProgramData\nCipher\Key Management Data\local.</span><span class="sxs-lookup"><span data-stu-id="efe19-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds to the C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="efe19-259">Puede usar valores diferentes para el quórum, pero en nuestro ejemplo, se le pedirá que escriba tres tarjetas en blanco y PIN para cada una de ellos.</span><span class="sxs-lookup"><span data-stu-id="efe19-259">You can use different values for the quorum but in our example, you’re prompted to enter three blank cards and pins for each one.</span></span> <span data-ttu-id="efe19-260">A continuación, dos tarjetas cualesquiera le proporcionarán acceso total al espacio de seguridad.</span><span class="sxs-lookup"><span data-stu-id="efe19-260">Then, any two cards give full access to the security world.</span></span> <span data-ttu-id="efe19-261">Estas tarjetas pasan a ser el **Conjunto de tarjetas de administrador** del nuevo espacio de seguridad.</span><span class="sxs-lookup"><span data-stu-id="efe19-261">These cards become the **Administrator Card Set** for the new security world.</span></span>

<span data-ttu-id="efe19-262">A continuación, haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="efe19-262">Then do the following:</span></span>

* <span data-ttu-id="efe19-263">Realice una copia de seguridad del archivo del espacio.</span><span class="sxs-lookup"><span data-stu-id="efe19-263">Back up the world file.</span></span> <span data-ttu-id="efe19-264">Proteja dicho archivo, las tarjetas de administrador y sus PIN, y asegúrese de que nadie tiene acceso a más de una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="efe19-264">Secure and protect the world file, the Administrator Cards, and their pins, and make sure that no single person has access to more than one card.</span></span>

### <a name="step-33-change-the-hsm-mode-to-o"></a><span data-ttu-id="efe19-265">Paso 3.3: cambio del modo HSM a "O"</span><span class="sxs-lookup"><span data-stu-id="efe19-265">Step 3.3: Change the HSM mode to 'O'</span></span>
<span data-ttu-id="efe19-266">Si está usando Thales nShield Edge, para cambiar el modo: 1.</span><span class="sxs-lookup"><span data-stu-id="efe19-266">If you are using Thales nShield Edge, to change the mode: 1.</span></span> <span data-ttu-id="efe19-267">Use el botón de modo para resaltar el modo requerido.</span><span class="sxs-lookup"><span data-stu-id="efe19-267">Use the Mode button to highlight the required mode.</span></span> <span data-ttu-id="efe19-268">2.</span><span class="sxs-lookup"><span data-stu-id="efe19-268">2.</span></span> <span data-ttu-id="efe19-269">Después de un momento, mantenga presionado el botón Borrar durante un par de segundos.</span><span class="sxs-lookup"><span data-stu-id="efe19-269">Within a few seconds, press and hold the Clear button for a couple of seconds.</span></span> <span data-ttu-id="efe19-270">Si el modo cambia, el LED del nuevo modo deja de parpadear y permanece encendido.</span><span class="sxs-lookup"><span data-stu-id="efe19-270">If the mode changes, the new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="efe19-271">El LED del estado puede parpadear irregularmente durante algunos segundos y, luego, parpadea regularmente cuando el dispositivo está listo.</span><span class="sxs-lookup"><span data-stu-id="efe19-271">The Status LED might flash irregularly for a few seconds and then flashes regularly when the device is ready.</span></span> <span data-ttu-id="efe19-272">En caso contrario, el dispositivo permanece en el modo actual, con el modo correspondiente de LED encendido.</span><span class="sxs-lookup"><span data-stu-id="efe19-272">Otherwise, the device remains in the current mode, with the appropriate mode LED lit.</span></span>


### <a name="step-34-validate-the-downloaded-package"></a><span data-ttu-id="efe19-273">Paso 3.4: validación del paquete descargado</span><span class="sxs-lookup"><span data-stu-id="efe19-273">Step 3.4: Validate the downloaded package</span></span>
<span data-ttu-id="efe19-274">Este paso es opcional, pero se recomienda realizarlo para poder validar estos elementos:</span><span class="sxs-lookup"><span data-stu-id="efe19-274">This step is optional but recommended so that you can validate the following:</span></span>

* <span data-ttu-id="efe19-275">La clave de intercambio de claves que se incluye en el conjunto de herramientas se ha generado desde un HSM de Thales original.</span><span class="sxs-lookup"><span data-stu-id="efe19-275">The Key Exchange Key that is included in the toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="efe19-276">El hash del espacio de seguridad que se incluye en el conjunto de herramientas se ha generado en un HSM de Thales original.</span><span class="sxs-lookup"><span data-stu-id="efe19-276">The hash of the Security World that is included in the toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="efe19-277">La clave de intercambio de claves no es exportable.</span><span class="sxs-lookup"><span data-stu-id="efe19-277">The Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="efe19-278">Para validar el paquete descargado, el HSM debe estar conectado, encendido y debe tener un espacio de seguridad (como el que acaba de crear).</span><span class="sxs-lookup"><span data-stu-id="efe19-278">To validate the downloaded package, the HSM must be connected, powered on, and must have a security world on it (such as the one you’ve just created).</span></span>
>
>

<span data-ttu-id="efe19-279">Para validar el paquete descargado:</span><span class="sxs-lookup"><span data-stu-id="efe19-279">To validate the downloaded package:</span></span>

1. <span data-ttu-id="efe19-280">Ejecute el script verifykeypackage.py, para lo que, en función de su región geográfica o instancia de Azure, debe escribir lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="efe19-280">Run the verifykeypackage.py script by typing one of the following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="efe19-281">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="efe19-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="efe19-282">Europa:</span><span class="sxs-lookup"><span data-stu-id="efe19-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="efe19-283">Asia:</span><span class="sxs-lookup"><span data-stu-id="efe19-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="efe19-284">América Latina:</span><span class="sxs-lookup"><span data-stu-id="efe19-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="efe19-285">Japón:</span><span class="sxs-lookup"><span data-stu-id="efe19-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="efe19-286">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="efe19-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="efe19-287">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="efe19-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="efe19-288">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa la instancia del gobierno de Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="efe19-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="efe19-289">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="efe19-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="efe19-290">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="efe19-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="efe19-291">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="efe19-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="efe19-292">Para India:</span><span class="sxs-lookup"><span data-stu-id="efe19-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="efe19-293">El software de Thales incluye Python en %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="efe19-293">The Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="efe19-294">Confirme que ve lo siguiente, que indica que el resultado de la validación ha sido satisfactorio: **Result: SUCCESS**</span><span class="sxs-lookup"><span data-stu-id="efe19-294">Confirm that you see the following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="efe19-295">Este script valida la cadena del firmante hasta la clave raíz de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-295">This script validates the signer chain up to the Thales root key.</span></span> <span data-ttu-id="efe19-296">El hash de esta clave raíz está insertado en el script y su valor debe ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="efe19-296">The hash of this root key is embedded in the script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="efe19-297">Este valor también se puede confirmar por separado en el [sitio web de Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="efe19-297">You can also confirm this value separately by visiting the [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="efe19-298">Ya está listo para crear una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="efe19-298">You’re now ready to create a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="efe19-299">Paso 3.5: creación de una nueva clave</span><span class="sxs-lookup"><span data-stu-id="efe19-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="efe19-300">Genere una clave con el programa **generatekey** de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-300">Generate a key by using the Thales **generatekey** program.</span></span>

<span data-ttu-id="efe19-301">Ejecute el comando siguiente para generar la clave:</span><span class="sxs-lookup"><span data-stu-id="efe19-301">Run the following command to generate the key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="efe19-302">Cuando ejecute este comando, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="efe19-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="efe19-303">El parámetro *protect* debe establecerse en el valor **module**, como se muestra.</span><span class="sxs-lookup"><span data-stu-id="efe19-303">The parameter *protect* must be set to the value **module**, as shown.</span></span> <span data-ttu-id="efe19-304">Esto crea una clave protegida por el módulo.</span><span class="sxs-lookup"><span data-stu-id="efe19-304">This creates a module-protected key.</span></span> <span data-ttu-id="efe19-305">El conjunto de herramientas BYOK no es compatible con claves protegidas con OCS.</span><span class="sxs-lookup"><span data-stu-id="efe19-305">The BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="efe19-306">Reemplace el valor de *contosokey* en **ident** y **plainname** por cualquier valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="efe19-306">Replace the value of *contosokey* for the **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="efe19-307">Para minimizar gastos administrativos y reducir el riesgo de errores, se recomienda utilizar el mismo valor en ambos.</span><span class="sxs-lookup"><span data-stu-id="efe19-307">To minimize administrative overheads and reduce the risk of errors, we recommend that you use the same value for both.</span></span> <span data-ttu-id="efe19-308">El valor **ident** debe contener solo números, guiones y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="efe19-308">The **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="efe19-309">En este ejemplo, pubexp se deja en blanco (valor predeterminado), pero puede especificar valores concretos.</span><span class="sxs-lookup"><span data-stu-id="efe19-309">The pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="efe19-310">Para obtener más información, consulte la documentación de Thales.</span><span class="sxs-lookup"><span data-stu-id="efe19-310">For more information, see the Thales documentation.</span></span>

<span data-ttu-id="efe19-311">Este comando crea un archivo de clave con tokens en la carpeta %NFAST_KMDATA%\local cuyo nombre comienza por **key_simple_**, seguido del valor **ident** que se especificó en el comando.</span><span class="sxs-lookup"><span data-stu-id="efe19-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by the **ident** that was specified in the command.</span></span> <span data-ttu-id="efe19-312">Por ejemplo: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="efe19-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="efe19-313">Este archivo contiene una clave cifrada.</span><span class="sxs-lookup"><span data-stu-id="efe19-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="efe19-314">Realice una copia del archivo tokenizado en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="efe19-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efe19-315">Cuando posteriormente transfiera la clave al Almacén de claves de Azure, Microsoft no podrá exportar esta clave, por lo que resulta extremadamente importante que realice una copia de seguridad de la misma y del espacio de seguridad.</span><span class="sxs-lookup"><span data-stu-id="efe19-315">When you later transfer your key to Azure Key Vault, Microsoft cannot export this key back to you so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="efe19-316">Póngase en contacto con Thales si necesita guía y procedimientos recomendados para realizar copias de seguridad de una clave.</span><span class="sxs-lookup"><span data-stu-id="efe19-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="efe19-317">Ya está listo para transferir la clave al Almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="efe19-317">You are now ready to transfer your key to Azure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="efe19-318">Paso 4: preparación de la clave para la transferencia</span><span class="sxs-lookup"><span data-stu-id="efe19-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="efe19-319">En este paso, realice los siguientes procedimientos en la estación de trabajo desconectada.</span><span class="sxs-lookup"><span data-stu-id="efe19-319">For this fourth step, do the following procedures on the disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="efe19-320">Paso 4.1: creación de una copia de la clave con menos permisos</span><span class="sxs-lookup"><span data-stu-id="efe19-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="efe19-321">Abra un nuevo símbolo del sistema y cambie el directorio actual a la ubicación en la que descomprimió el archivo zip de BYOK.</span><span class="sxs-lookup"><span data-stu-id="efe19-321">Open a new command prompt and change the current directory to the location where you unzipped the BYOK zip file.</span></span> <span data-ttu-id="efe19-322">Para reducir los permisos en su clave, desde un símbolo del sistema, ejecute uno de los siguientes comandos, en función de su región geográfica o instancia de Azure:</span><span class="sxs-lookup"><span data-stu-id="efe19-322">To reduce the permissions on your key, from a command prompt, run one of the following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="efe19-323">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="efe19-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="efe19-324">Europa:</span><span class="sxs-lookup"><span data-stu-id="efe19-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="efe19-325">Asia:</span><span class="sxs-lookup"><span data-stu-id="efe19-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="efe19-326">América Latina:</span><span class="sxs-lookup"><span data-stu-id="efe19-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="efe19-327">Japón:</span><span class="sxs-lookup"><span data-stu-id="efe19-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="efe19-328">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="efe19-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="efe19-329">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="efe19-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="efe19-330">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa la instancia del gobierno de Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="efe19-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="efe19-331">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="efe19-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="efe19-332">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="efe19-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="efe19-333">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="efe19-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="efe19-334">Para India:</span><span class="sxs-lookup"><span data-stu-id="efe19-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="efe19-335">Cuando ejecute este comando, reemplace *contosokey* por el valor que especificó en el **Paso 3.5: creación de una nueva clave** del paso [Generación de la clave](#step-3-generate-your-key).</span><span class="sxs-lookup"><span data-stu-id="efe19-335">When you run this command, replace *contosokey* with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="efe19-336">Se le pedirá que conecte sus tarjetas de administrador del espacio de seguridad.</span><span class="sxs-lookup"><span data-stu-id="efe19-336">You are asked to plug in your security world admin cards.</span></span>

<span data-ttu-id="efe19-337">Cuando se complete el comando, verá **Result: SUCCESS** y la copia de la clave con menos permisos estará en el archivo denominado key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="efe19-337">When the command completes, you see **Result: SUCCESS** and the copy of your key with reduced permissions are in the file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="efe19-338">Puede inspeccionar ACLS mediante los comandos siguientes utilizando las herramientas de Thales:</span><span class="sxs-lookup"><span data-stu-id="efe19-338">You may inspects the ACLS using following commands using the Thales utilities:</span></span>

* <span data-ttu-id="efe19-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="efe19-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="efe19-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="efe19-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="efe19-341">Cuando ejecute estos comandos, reemplace contosokey por el mismo valor que especificó en el **Paso 3.5: creación de una nueva clave** del paso [Generación de la clave](#step-3-generate-your-key) .</span><span class="sxs-lookup"><span data-stu-id="efe19-341">When you run these commands, replace contosokey with the same value you specified in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="efe19-342">Paso 4.2: cifrado de la clave mediante la clave de intercambio de claves de Microsoft</span><span class="sxs-lookup"><span data-stu-id="efe19-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="efe19-343">Ejecute uno de los comandos siguientes, dependiendo de su región geográfica o la instancia de Azure:</span><span class="sxs-lookup"><span data-stu-id="efe19-343">Run one of the following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="efe19-344">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="efe19-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-345">Europa:</span><span class="sxs-lookup"><span data-stu-id="efe19-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-346">Asia:</span><span class="sxs-lookup"><span data-stu-id="efe19-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-347">América Latina:</span><span class="sxs-lookup"><span data-stu-id="efe19-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-348">Japón:</span><span class="sxs-lookup"><span data-stu-id="efe19-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-349">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="efe19-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-350">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="efe19-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-351">Para [Azure Government](https://azure.microsoft.com/features/gov/), que usa la instancia del gobierno de Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="efe19-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses the US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-352">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="efe19-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-353">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="efe19-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-354">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="efe19-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="efe19-355">Para India:</span><span class="sxs-lookup"><span data-stu-id="efe19-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="efe19-356">Cuando ejecute este comando, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="efe19-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="efe19-357">Reemplace *contosokey* por el identificador que usó para generar la clave en el **Paso 3.5: creación de una nueva clave** del paso [Generación de la clave](#step-3-generate-your-key) .</span><span class="sxs-lookup"><span data-stu-id="efe19-357">Replace *contosokey* with the identifier that you used to generate the key in **Step 3.5: Create a new key** from the [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="efe19-358">Reemplace *SubscriptionID* por el identificador de la suscripción de Azure con Key Vault.</span><span class="sxs-lookup"><span data-stu-id="efe19-358">Replace *SubscriptionID* with the ID of the Azure subscription that contains your key vault.</span></span> <span data-ttu-id="efe19-359">Este valor lo recuperó anteriormente, en el **paso 1.2: especificación del identificador de la suscripción de Azure** del paso de [preparación de la estación de trabajo conectada a Internet](#step-1-prepare-your-internet-connected-workstation).</span><span class="sxs-lookup"><span data-stu-id="efe19-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from the [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="efe19-360">Reemplace *ContosoFirstHSMKey* por una etiqueta que se usará para el nombre del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="efe19-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="efe19-361">Cuando la operación se complete correctamente, se mostrará **Result: SUCCESS** y habrá un nuevo archivo en la carpeta actual que tendrá el siguiente nombre: KeyTransferPackage-*ContosoFirstHSMkey*.byok.</span><span class="sxs-lookup"><span data-stu-id="efe19-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in the current folder that has the following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-to-the-internet-connected-workstation"></a><span data-ttu-id="efe19-362">Paso 4.3: copia del paquete de transferencia de claves a la estación de trabajo conectada a Internet</span><span class="sxs-lookup"><span data-stu-id="efe19-362">Step 4.3: Copy your key transfer package to the Internet-connected workstation</span></span>
<span data-ttu-id="efe19-363">Utilice una unidad USB u otro dispositivo de almacenamiento portátil para copiar el archivo de salida del paso anterior (KeyTransferPackage-ContosoFirstHSMkey.byok) a la estación de trabajo conectada a Internet.</span><span class="sxs-lookup"><span data-stu-id="efe19-363">Use a USB drive or other portable storage to copy the output file from the previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) to your Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-to-azure-key-vault"></a><span data-ttu-id="efe19-364">Paso 5: transferencia de la clave al Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="efe19-364">Step 5: Transfer your key to Azure Key Vault</span></span>
<span data-ttu-id="efe19-365">En este paso final, en la estación de trabajo conectada a Internet, use el cmdlet [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) para cargar el paquete de transferencia de claves que copió de la estación de trabajo desconectada en el HSM de Azure Key Vault:</span><span class="sxs-lookup"><span data-stu-id="efe19-365">For this final step, on the Internet-connected workstation, use the [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet to upload the key transfer package that you copied from the disconnected workstation to the Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="efe19-366">Si la carga se realiza correctamente, verá que se muestran las propiedades de la clave que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="efe19-366">If the upload is successful, you see displayed the properties of the key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="efe19-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="efe19-367">Next steps</span></span>
<span data-ttu-id="efe19-368">Ahora puede usar esta clave protegida con HSM en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="efe19-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="efe19-369">Para obtener más información, consulte la sección **Si desea usar un módulo de seguridad de hardware (HSM)** del tutorial [Introducción al Almacén de claves de Azure](key-vault-get-started.md) .</span><span class="sxs-lookup"><span data-stu-id="efe19-369">For more information, see the **If you want to use a hardware security module (HSM)** section in the [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
