---
title: "aaaHow toogenerate y transferencia de claves protegidas con HSM para el almacén de claves de Azure | Documentos de Microsoft"
description: "Utilice este toohelp artículo planear, generar y, a continuación, transferir su propios toouse claves protegidas con HSM al almacén de claves de Azure. También se denomina BYOK o \"traiga su propia clave\"."
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
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="b4e55-104">¿Cómo toogenerate y transferencia de claves protegidas con HSM para el almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="b4e55-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="b4e55-105">Introducción</span><span class="sxs-lookup"><span data-stu-id="b4e55-105">Introduction</span></span>
<span data-ttu-id="b4e55-106">Para mayor seguridad, cuando se utiliza el almacén de claves de Azure, puede importar o generar claves en módulos de seguridad de hardware (HSM) que no dejan nunca el límite de HSM Hola.</span><span class="sxs-lookup"><span data-stu-id="b4e55-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="b4e55-107">Este escenario es a menudo denominado tooas *traiga su propia clave*, o BYOK.</span><span class="sxs-lookup"><span data-stu-id="b4e55-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="b4e55-108">Hola HSM son FIPS 140-2 nivel 2 validado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="b4e55-109">Almacén de claves de Azure usa familia Thales nShield de HSM tooprotect sus claves.</span><span class="sxs-lookup"><span data-stu-id="b4e55-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="b4e55-110">Utilice la información de hello en este tema toohelp planear, generar y, a continuación, transferir su propios toouse claves protegidas con HSM al almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="b4e55-111">Esta funcionalidad no está disponible para Azure China.</span><span class="sxs-lookup"><span data-stu-id="b4e55-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="b4e55-112">Para obtener más información sobre el Almacén de claves de Azure, consulte [¿Qué es el Almacén de claves de Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="b4e55-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="b4e55-113">Para ver tutorial introductorio, que incluye la creación de un almacén de claves para claves protegidas con HSM, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b4e55-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="b4e55-114">Obtener más información sobre cómo generar y transferir una clave protegida por HSM a través de Internet de hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="b4e55-115">Generar clave de Hola desde una estación de trabajo sin conexión, lo que reduce la superficie expuesta a ataques Hola.</span><span class="sxs-lookup"><span data-stu-id="b4e55-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="b4e55-116">clave de Hola se cifra con una clave de intercambio de claves (KEK), que permanece cifrada hasta que se transfieren toohello HSM del almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="b4e55-117">Solo Hola versión cifrada de la clave deja de estación de trabajo original Hola.</span><span class="sxs-lookup"><span data-stu-id="b4e55-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="b4e55-118">conjunto de herramientas de Hello establece propiedades en su clave de inquilino que enlaza su clave toohello mundo de seguridad del almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="b4e55-119">Modo que, después de HSM del almacén de claves de hello Azure reciban y descifren su clave, solamente dichos HSM los pueden usarla.</span><span class="sxs-lookup"><span data-stu-id="b4e55-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="b4e55-120">La clave no se puede exportar.</span><span class="sxs-lookup"><span data-stu-id="b4e55-120">Your key cannot be exported.</span></span> <span data-ttu-id="b4e55-121">Este enlace es impuesto por hello HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="b4e55-122">Hola clave de intercambio de claves (KEK) que es tooencrypt usa la clave se genera dentro de HSM del almacén de claves de Azure de hello y no es exportable.</span><span class="sxs-lookup"><span data-stu-id="b4e55-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="b4e55-123">Hola HSM exigen que no puede haber ninguna versión neta de hello KEK fuera Hola HSM.</span><span class="sxs-lookup"><span data-stu-id="b4e55-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="b4e55-124">Además, el conjunto de herramientas de hello incluye la atestación desde Thales ese Hola KEK no es exportable y se generó dentro de un HSM genuino que fabricó Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="b4e55-125">conjunto de herramientas de Hello incluye la atestación desde Thales ese Hola mundo de seguridad también se generó en un HSM genuino fabricado por Thales el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="b4e55-126">Este atestación demuestra tooyou que Microsoft usa hardware genuino.</span><span class="sxs-lookup"><span data-stu-id="b4e55-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="b4e55-127">Microsoft usa KEK independientes y separa los espacios de seguridad de las distintas regiones geográficas.</span><span class="sxs-lookup"><span data-stu-id="b4e55-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="b4e55-128">Esta separación garantiza que su clave pueda usarse solamente en centros de datos en la región de hello en el que se ha cifrado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="b4e55-129">Por ejemplo, una clave de un cliente europeo no se puede utilizar en centros de datos de América del Norte o Asia.</span><span class="sxs-lookup"><span data-stu-id="b4e55-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="b4e55-130">Más información acerca de los HSM de Thales y los servicios de Microsoft</span><span class="sxs-lookup"><span data-stu-id="b4e55-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="b4e55-131">Thales e-Security es una principales proveedores mundiales de cifrado de datos y ciberseguridad seguridad soluciones toohello servicios financieros, tecnología punta, fabricación, gobierno y sectores tecnológicos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="b4e55-132">Con una información de gobierno y 40 años trayectoria de protección corporativa, se utilizan las soluciones de Thales por cuatro de hello cinco empresas más grandes el sector energético y aeroespacial.</span><span class="sxs-lookup"><span data-stu-id="b4e55-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="b4e55-133">También las utilizan 22 países de la OTAN y protegen más del 80 por ciento de las transacciones de pago mundiales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="b4e55-134">Microsoft ha colaborado con el estado de Hola de Thales tooenhance de carátulas de HSM.</span><span class="sxs-lookup"><span data-stu-id="b4e55-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="b4e55-135">Estas mejoras permiten beneficios típico de hello tooget de servicios hospedados sin abandonar control sobre las claves.</span><span class="sxs-lookup"><span data-stu-id="b4e55-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="b4e55-136">En concreto, estas mejoras permiten que Microsoft administre Hola HSM para que no es necesario.</span><span class="sxs-lookup"><span data-stu-id="b4e55-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="b4e55-137">Como una nube de que almacén de claves de servicio, Azure se amplía en muy poco tiempo toomeet picos de uso de su organización.</span><span class="sxs-lookup"><span data-stu-id="b4e55-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="b4e55-138">Hola al mismo tiempo, la clave está protegida dentro de los HSM de Microsoft: mantener el control sobre el ciclo de vida de clave de Hola porque generar clave de Hola y transferir los HSM del tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="b4e55-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="b4e55-139">Implementación del método Aportar tu propia clave (BYOK) en el Almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="b4e55-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="b4e55-140">Hola de uso después de obtener información y procedimientos si va a generar su propia clave protegida por HSM y, a continuación, transferirla tooAzure el almacén de claves: Hola aportar su propia escenario clave (BYOK).</span><span class="sxs-lookup"><span data-stu-id="b4e55-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="b4e55-141">Requisitos previos de BYOK</span><span class="sxs-lookup"><span data-stu-id="b4e55-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="b4e55-142">Vea Hola siguiente tabla para obtener una lista de requisitos previos para aportar su propia clave (BYOK) para el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="b4e55-143">Requisito</span><span class="sxs-lookup"><span data-stu-id="b4e55-143">Requirement</span></span> | <span data-ttu-id="b4e55-144">Más información</span><span class="sxs-lookup"><span data-stu-id="b4e55-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="b4e55-145">Un tooAzure de suscripción</span><span class="sxs-lookup"><span data-stu-id="b4e55-145">A subscription tooAzure</span></span> |<span data-ttu-id="b4e55-146">toocreate un almacén de claves de Azure, se necesita una suscripción a Azure: [suscribirse a la versión de prueba gratuita](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="b4e55-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="b4e55-147">Hola claves protegidas con HSM en el toosupport nivel de servicio Premium de almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="b4e55-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="b4e55-148">Para obtener más información sobre los niveles de servicio de Hola y las capacidades de almacén de claves de Azure, vea hello [precios de Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) sitio Web.</span><span class="sxs-lookup"><span data-stu-id="b4e55-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="b4e55-149">HSM de Thales, tarjetas inteligentes y software compatible</span><span class="sxs-lookup"><span data-stu-id="b4e55-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="b4e55-150">Debe tener acceso a tooa módulo de seguridad de Hardware de Thales y al conocimiento operacional básico de HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="b4e55-151">Vea [módulo de seguridad de Hardware de Thales](https://www.thales-esecurity.com/msrms/buy) de lista de Hola de modelos compatibles o toopurchase un HSM si no tiene uno.</span><span class="sxs-lookup"><span data-stu-id="b4e55-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="b4e55-152">Hola después de hardware y software:</span><span class="sxs-lookup"><span data-stu-id="b4e55-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="b4e55-153">Una estación de trabajo x64 sin conexión con un sistema operativo Windows 7 y software Thales nShield versión 11.50 o superior.</span><span class="sxs-lookup"><span data-stu-id="b4e55-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="b4e55-154">Si esta estación de trabajo ejecuta Windows 7, debe [instalar Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="b4e55-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="b4e55-155">Una estación de trabajo que está conectado toohello Internet y tiene un sistema operativo mínimo de Windows 7 y [Azure PowerShell](/powershell/azure/overview) **versión mínima 1.1.0** instalado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="b4e55-156">Una unidad USB u otro dispositivo de almacenamiento portátil con al menos 16 MB de espacio libre.</span><span class="sxs-lookup"><span data-stu-id="b4e55-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="b4e55-157">Por motivos de seguridad, se recomienda que Hola primera estación de trabajo no está conectado tooa red.</span><span class="sxs-lookup"><span data-stu-id="b4e55-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="b4e55-158">Sin embargo, esta recomendación no es de obligado cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="b4e55-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="b4e55-159">Tenga en cuenta que en las instrucciones de Hola que siguen, esta estación de trabajo es estación de trabajo que se hace referencia tooas Hola desconectado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="b4e55-160">Además, si la clave de inquilino es para una red de producción, se recomienda que realice una segunda estación de trabajo independiente toodownload Hola conjunto de herramientas y la carga Hola clave de inquilino.</span><span class="sxs-lookup"><span data-stu-id="b4e55-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="b4e55-161">Pero con fines de prueba, puede usar Hola misma estación de trabajo como Hola primero.</span><span class="sxs-lookup"><span data-stu-id="b4e55-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="b4e55-162">Tenga en cuenta que en las instrucciones de Hola que siguen, esta segunda estación de trabajo conectada a Internet la estación de trabajo del hello tooas que se hace referencia.</span><span class="sxs-lookup"><span data-stu-id="b4e55-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="b4e55-163">Generar y transferir su clave tooAzure HSM del almacén de claves</span><span class="sxs-lookup"><span data-stu-id="b4e55-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="b4e55-164">Utilizará Hola siguiendo cinco toogenerate de pasos y transferir su clave tooan HSM del almacén de claves de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="b4e55-165">Paso 1: preparación de la estación de trabajo conectada a Internet</span><span class="sxs-lookup"><span data-stu-id="b4e55-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="b4e55-166">Paso 2: preparación de la estación de trabajo desconectada</span><span class="sxs-lookup"><span data-stu-id="b4e55-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="b4e55-167">Paso 3: generación de la clave</span><span class="sxs-lookup"><span data-stu-id="b4e55-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="b4e55-168">Paso 4: preparación de la clave para la transferencia</span><span class="sxs-lookup"><span data-stu-id="b4e55-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="b4e55-169">Paso 5: Transferir su clave tooAzure el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="b4e55-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="b4e55-170">Paso 1: preparación de la estación de trabajo conectada a Internet</span><span class="sxs-lookup"><span data-stu-id="b4e55-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="b4e55-171">Este primer paso, Hola seguir los procedimientos descritos en la estación de trabajo que está conectado toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="b4e55-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="b4e55-172">Paso 1.1: instalación de Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4e55-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="b4e55-173">Hola conectada a Internet estación de trabajo, descargue e instale el módulo de PowerShell de Azure de Hola que incluye cmdlets de hello toomanage el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="b4e55-174">Esto requiere una versión mínima de 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="b4e55-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="b4e55-175">Para obtener instrucciones de instalación, consulte [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4e55-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="b4e55-176">Paso 1.2: especificación del identificador de la suscripción a Azure</span><span class="sxs-lookup"><span data-stu-id="b4e55-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="b4e55-177">Inicie una sesión de PowerShell de Azure e inicie sesión en tooyour cuenta de Azure mediante el siguiente comando de hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="b4e55-178">En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña.</span><span class="sxs-lookup"><span data-stu-id="b4e55-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="b4e55-179">A continuación, usar hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) comando:</span><span class="sxs-lookup"><span data-stu-id="b4e55-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="b4e55-180">De salida de hello, busque el identificador de hello para la suscripción de Hola que se va a utilizar para el almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="b4e55-181">Lo necesitará más adelante.</span><span class="sxs-lookup"><span data-stu-id="b4e55-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="b4e55-182">No cierre la ventana de PowerShell de Azure de hello.</span><span class="sxs-lookup"><span data-stu-id="b4e55-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="b4e55-183">Paso 1.3: Descargar el conjunto de herramientas BYOK de hello para el almacén de claves de Azure</span><span class="sxs-lookup"><span data-stu-id="b4e55-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="b4e55-184">Vaya toohello Microsoft Download Center y [descargar el conjunto de herramientas de BYOK de almacén de claves de Azure de hello](http://www.microsoft.com/download/details.aspx?id=45345) para su región geográfica o la instancia de Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e55-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="b4e55-185">Utilice siguiente hello toodownload de nombre de paquete de información tooidentify hello y su correspondiente SHA-256 hash del paquete:</span><span class="sxs-lookup"><span data-stu-id="b4e55-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="b4e55-186">**Estados Unidos:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-186">**United States:**</span></span>

<span data-ttu-id="b4e55-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="b4e55-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="b4e55-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="b4e55-189">**Europa:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-189">**Europe:**</span></span>

<span data-ttu-id="b4e55-190">KeyVault-BYOK-Tools-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="b4e55-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="b4e55-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="b4e55-192">**Asia:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-192">**Asia:**</span></span>

<span data-ttu-id="b4e55-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="b4e55-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="b4e55-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="b4e55-195">**América Latina:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-195">**Latin America:**</span></span>

<span data-ttu-id="b4e55-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="b4e55-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="b4e55-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="b4e55-198">**Japón:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-198">**Japan:**</span></span>

<span data-ttu-id="b4e55-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="b4e55-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="b4e55-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="b4e55-201">**Corea:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-201">**Korea:**</span></span>

<span data-ttu-id="b4e55-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="b4e55-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="b4e55-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="b4e55-204">**Australia:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-204">**Australia:**</span></span>

<span data-ttu-id="b4e55-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="b4e55-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="b4e55-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="b4e55-207">**Azure Government:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="b4e55-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="b4e55-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="b4e55-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="b4e55-210">**DoD del Gobierno de Estados Unidos:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-210">**US Government DOD:**</span></span>

<span data-ttu-id="b4e55-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="b4e55-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="b4e55-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="b4e55-213">**Canadá:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-213">**Canada:**</span></span>

<span data-ttu-id="b4e55-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="b4e55-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="b4e55-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="b4e55-216">**Alemania:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-216">**Germany:**</span></span>

<span data-ttu-id="b4e55-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="b4e55-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="b4e55-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="b4e55-219">**India:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-219">**India:**</span></span>

<span data-ttu-id="b4e55-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="b4e55-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="b4e55-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="b4e55-222">**Reino Unido:**</span><span class="sxs-lookup"><span data-stu-id="b4e55-222">**United Kingdom:**</span></span>

<span data-ttu-id="b4e55-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="b4e55-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="b4e55-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="b4e55-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="b4e55-225">integridad de hello toovalidate de su conjunto de herramientas BYOK descargado, desde la sesión de PowerShell de Azure, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4e55-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="b4e55-226">conjunto de herramientas de Hello incluye siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="b4e55-227">Un paquete de clave de intercambio de claves (KEK) cuyo nombre comienza por **BYOK-KEK-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="b4e55-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="b4e55-228">Un paquete de espacio de seguridad cuyo nombre comienza por **BYOK-SecurityWorld-pkg-.**</span><span class="sxs-lookup"><span data-stu-id="b4e55-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="b4e55-229">Un script Python denominado **verifykeypackage.py.**</span><span class="sxs-lookup"><span data-stu-id="b4e55-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="b4e55-230">Un archivo ejecutable de línea de comandos denominado **KeyTransferRemote.exe** y asociado a las DLL.</span><span class="sxs-lookup"><span data-stu-id="b4e55-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="b4e55-231">Un paquete redistribuible de Visual C++ denominado **vcredist_x64.exe**.</span><span class="sxs-lookup"><span data-stu-id="b4e55-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="b4e55-232">Unidad USB de tooa de copia Hola paquete u otro almacenamiento portátil.</span><span class="sxs-lookup"><span data-stu-id="b4e55-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="b4e55-233">Paso 2: preparación de la estación de trabajo desconectada</span><span class="sxs-lookup"><span data-stu-id="b4e55-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="b4e55-234">Para este segundo paso: Hola seguir los procedimientos descritos en la estación de trabajo de Hola que no está conectado tooa red (Hola Internet o la red interna).</span><span class="sxs-lookup"><span data-stu-id="b4e55-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="b4e55-235">Paso 2.1: Preparar la estación de trabajo de hello desconectada con HSM de Thales</span><span class="sxs-lookup"><span data-stu-id="b4e55-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="b4e55-236">Instalar software de soporte de hello nCipher (Thales) en un equipo de Windows y, a continuación, adjunte un equipo de toothat HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="b4e55-237">Asegúrese de que Hola herramientas de Thales se encuentran en la ruta de acceso (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="b4e55-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="b4e55-238">Por ejemplo, escriba el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="b4e55-239">Para obtener más información, consulte la Guía de usuario de hello incluida con hello HSM de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="b4e55-240">Paso 2.2: Conjunto de herramientas BYOK de Hola instalación en la estación de trabajo de hello desconectado</span><span class="sxs-lookup"><span data-stu-id="b4e55-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="b4e55-241">Copie el paquete de conjunto de herramientas BYOK de Hola de unidad USB de Hola o de otro almacenamiento portátil y, a continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b4e55-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="b4e55-242">Extraiga los archivos de hello del paquete de descarga de Hola en cualquier carpeta.</span><span class="sxs-lookup"><span data-stu-id="b4e55-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="b4e55-243">En esa carpeta, ejecute vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="b4e55-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="b4e55-244">Siga las instrucciones de hello toohello instalar los componentes de tiempo de ejecución de Visual C++ de Hola para Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="b4e55-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="b4e55-245">Paso 3: generación de la clave</span><span class="sxs-lookup"><span data-stu-id="b4e55-245">Step 3: Generate your key</span></span>
<span data-ttu-id="b4e55-246">Para el tercer paso, Hola seguir los procedimientos descritos en la estación de trabajo de hello desconectado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="b4e55-247">toocomplete este paso HSM debe estar en modo de inicialización.</span><span class="sxs-lookup"><span data-stu-id="b4e55-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="b4e55-248">Paso 3.1: Cambiar Hola HSM modo too'I'</span><span class="sxs-lookup"><span data-stu-id="b4e55-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="b4e55-249">Si usas Thales nShield Edge, modo de Hola toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="b4e55-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="b4e55-250">Utilice Hola modo toohighlight botón Hola modo requerido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="b4e55-251">2.</span><span class="sxs-lookup"><span data-stu-id="b4e55-251">2.</span></span> <span data-ttu-id="b4e55-252">Dentro de unos segundos, mantenga presionada botón Borrar Hola para un par de segundos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="b4e55-253">Si se cambia el modo de hello, Hola nuevo modo se detiene de LED parpadea y permanece encendido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="b4e55-254">Hola el LED de estado podría flash irregular durante unos segundos y, a continuación, parpadeará con regularidad al dispositivo de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="b4e55-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="b4e55-255">En caso contrario, Hola dispositivo permanece en el modo actual hello, con el modo adecuado de hello LED encendido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="b4e55-256">Paso 3.2: creación de un espacio de seguridad</span><span class="sxs-lookup"><span data-stu-id="b4e55-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="b4e55-257">Inicie un símbolo del sistema y ejecute hello programa del nuevo mundo de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="b4e55-258">Este programa crea un **mundo de seguridad** archivos en % NFAST_KMDATA%\local\world, que corresponde a toohello C:\ProgramData\nCipher\Key Management Data\local carpeta.</span><span class="sxs-lookup"><span data-stu-id="b4e55-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="b4e55-259">Puede usar valores diferentes para el quórum de hello pero en nuestro ejemplo, le tooenter solicitadas tres las tarjetas en blanco y PIN de cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="b4e55-260">A continuación, dos tarjetas cualesquiera proporcionarán mundo de seguridad de acceso completo toohello.</span><span class="sxs-lookup"><span data-stu-id="b4e55-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="b4e55-261">Estas tarjetas convierten hello **conjunto de tarjetas de administrador** para Hola mundo de seguridad nuevo.</span><span class="sxs-lookup"><span data-stu-id="b4e55-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="b4e55-262">A continuación, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="b4e55-262">Then do hello following:</span></span>

* <span data-ttu-id="b4e55-263">Realizar una copia de archivo de hello world.</span><span class="sxs-lookup"><span data-stu-id="b4e55-263">Back up hello world file.</span></span> <span data-ttu-id="b4e55-264">Proteger y proteger el archivo de hello world, tarjetas de administrador de Hola y sus anclajes y asegúrese de que ninguna persona tiene acceso toomore que una tarjeta.</span><span class="sxs-lookup"><span data-stu-id="b4e55-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="b4e55-265">Paso 3.3: Cambiar Hola HSM modo too'O'</span><span class="sxs-lookup"><span data-stu-id="b4e55-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="b4e55-266">Si usas Thales nShield Edge, modo de Hola toochange: 1.</span><span class="sxs-lookup"><span data-stu-id="b4e55-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="b4e55-267">Utilice Hola modo toohighlight botón Hola modo requerido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="b4e55-268">2.</span><span class="sxs-lookup"><span data-stu-id="b4e55-268">2.</span></span> <span data-ttu-id="b4e55-269">Dentro de unos segundos, mantenga presionada botón Borrar Hola para un par de segundos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="b4e55-270">Si se cambia el modo de hello, Hola nuevo modo se detiene de LED parpadea y permanece encendido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="b4e55-271">Hola el LED de estado podría flash irregular durante unos segundos y, a continuación, parpadeará con regularidad al dispositivo de hello está listo.</span><span class="sxs-lookup"><span data-stu-id="b4e55-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="b4e55-272">En caso contrario, Hola dispositivo permanece en el modo actual hello, con el modo adecuado de hello LED encendido.</span><span class="sxs-lookup"><span data-stu-id="b4e55-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="b4e55-273">Paso 3.4: Validar el paquete de descarga de Hola</span><span class="sxs-lookup"><span data-stu-id="b4e55-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="b4e55-274">Este paso es opcional pero se recomienda para que pueda validar siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="b4e55-275">Clave de intercambio que se incluye en el conjunto de herramientas de Hola Hola se ha generado desde un HSM de Thales genuino.</span><span class="sxs-lookup"><span data-stu-id="b4e55-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="b4e55-276">hash de Hola Hola mundo de seguridad que se incluye en el conjunto de herramientas de Hola se ha generado desde un HSM de Thales genuino.</span><span class="sxs-lookup"><span data-stu-id="b4e55-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="b4e55-277">Hola clave de intercambio no es exportable.</span><span class="sxs-lookup"><span data-stu-id="b4e55-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="b4e55-278">Hola toovalidate descargó el paquete, hello HSM debe estar conectado, encendida y debe tener un mundo de seguridad en él (por ejemplo, Hola uno que acaba de crear).</span><span class="sxs-lookup"><span data-stu-id="b4e55-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="b4e55-279">paquete de hello descargado toovalidate:</span><span class="sxs-lookup"><span data-stu-id="b4e55-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="b4e55-280">Ejecutar script de Hola verifykeypackage.py escribiendo uno de los siguientes de hello, según la región geográfica o la instancia de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="b4e55-281">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="b4e55-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="b4e55-282">Europa:</span><span class="sxs-lookup"><span data-stu-id="b4e55-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="b4e55-283">Asia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="b4e55-284">América Latina:</span><span class="sxs-lookup"><span data-stu-id="b4e55-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="b4e55-285">Japón:</span><span class="sxs-lookup"><span data-stu-id="b4e55-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="b4e55-286">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="b4e55-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="b4e55-287">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="b4e55-288">Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="b4e55-289">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="b4e55-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="b4e55-290">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="b4e55-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="b4e55-291">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="b4e55-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="b4e55-292">Para India:</span><span class="sxs-lookup"><span data-stu-id="b4e55-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="b4e55-293">Hola software de Thales incluye un script python en %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="b4e55-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="b4e55-294">Confirme que ve a continuación hello, que indica la validación correcta: **resultado: correcto**</span><span class="sxs-lookup"><span data-stu-id="b4e55-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="b4e55-295">Este script valida la cadena del firmante Hola seguridad toohello clave raíz de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="b4e55-296">hash de Hola de esta clave raíz está incrustada en el script de Hola y su valor debe ser **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="b4e55-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="b4e55-297">También puede confirmar este valor independiente visitando hello [sitio Web de Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="b4e55-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="b4e55-298">Ahora está listo toocreate una nueva clave.</span><span class="sxs-lookup"><span data-stu-id="b4e55-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="b4e55-299">Paso 3.5: creación de una nueva clave</span><span class="sxs-lookup"><span data-stu-id="b4e55-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="b4e55-300">Genere una clave mediante hello Thales **generatekey** programa.</span><span class="sxs-lookup"><span data-stu-id="b4e55-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="b4e55-301">Ejecute hello después la tecla de comando toogenerate hello:</span><span class="sxs-lookup"><span data-stu-id="b4e55-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="b4e55-302">Cuando ejecute este comando, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b4e55-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="b4e55-303">Hola parámetro *proteger* se debe establecer el valor de toohello **módulo**, tal y como se muestra.</span><span class="sxs-lookup"><span data-stu-id="b4e55-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="b4e55-304">Esto crea una clave protegida por el módulo.</span><span class="sxs-lookup"><span data-stu-id="b4e55-304">This creates a module-protected key.</span></span> <span data-ttu-id="b4e55-305">conjunto de herramientas BYOK de Hello no admite claves protegidas por OCS.</span><span class="sxs-lookup"><span data-stu-id="b4e55-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="b4e55-306">Reemplazar el valor de Hola de *contosokey* para hello **ident** y **plainname** con cualquier valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="b4e55-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="b4e55-307">toominimize de sobrecargas administrativas y reducir los riesgos de Hola de errores, se recomienda que use Hola mismo valor para ambos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="b4e55-308">Hola **ident** valor debe contener solo números, guiones y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="b4e55-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="b4e55-309">Hola pubexp se deja en blanco (valor predeterminado) en este ejemplo, pero puede especificar valores específicos.</span><span class="sxs-lookup"><span data-stu-id="b4e55-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="b4e55-310">Para obtener más información, vea Hola documentación de Thales.</span><span class="sxs-lookup"><span data-stu-id="b4e55-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="b4e55-311">Este comando crea un archivo de clave acortada en la carpeta %NFAST_KMDATA%\local con un nombre que comienza con **key_simple_**, seguido de hello **ident** que se especificó en el comando de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4e55-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="b4e55-312">Por ejemplo: **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="b4e55-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="b4e55-313">Este archivo contiene una clave cifrada.</span><span class="sxs-lookup"><span data-stu-id="b4e55-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="b4e55-314">Realice una copia del archivo tokenizado en una ubicación segura.</span><span class="sxs-lookup"><span data-stu-id="b4e55-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b4e55-315">Cuando posteriormente transfiera su clave tooAzure el almacén de claves, Microsoft no exportar esta clave tooyou atrás así que tiene mucha importancia que haga una copia el clave y seguridad del mundo de forma segura.</span><span class="sxs-lookup"><span data-stu-id="b4e55-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="b4e55-316">Póngase en contacto con Thales si necesita guía y procedimientos recomendados para realizar copias de seguridad de una clave.</span><span class="sxs-lookup"><span data-stu-id="b4e55-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="b4e55-317">Se está ahora listo tootransfer su clave tooAzure el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b4e55-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="b4e55-318">Paso 4: preparación de la clave para la transferencia</span><span class="sxs-lookup"><span data-stu-id="b4e55-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="b4e55-319">Para este paso cuarto, Hola seguir los procedimientos descritos en la estación de trabajo de hello desconectado.</span><span class="sxs-lookup"><span data-stu-id="b4e55-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="b4e55-320">Paso 4.1: creación de una copia de la clave con menos permisos</span><span class="sxs-lookup"><span data-stu-id="b4e55-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="b4e55-321">Abra un nuevo símbolo y cambie Hola actual toohello ubicación del directorio donde descomprimió el archivo zip de hello BYOK.</span><span class="sxs-lookup"><span data-stu-id="b4e55-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="b4e55-322">permisos de Hola de tooreduce en su clave, desde un símbolo del sistema, ejecutan uno de los siguientes de hello, según la región geográfica o la instancia de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="b4e55-323">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="b4e55-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="b4e55-324">Europa:</span><span class="sxs-lookup"><span data-stu-id="b4e55-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="b4e55-325">Asia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="b4e55-326">América Latina:</span><span class="sxs-lookup"><span data-stu-id="b4e55-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="b4e55-327">Japón:</span><span class="sxs-lookup"><span data-stu-id="b4e55-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="b4e55-328">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="b4e55-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="b4e55-329">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="b4e55-330">Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="b4e55-331">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="b4e55-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="b4e55-332">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="b4e55-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="b4e55-333">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="b4e55-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="b4e55-334">Para India:</span><span class="sxs-lookup"><span data-stu-id="b4e55-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="b4e55-335">Cuando ejecute este comando, reemplace *contosokey* con hello mismo valor que especificó en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.</span><span class="sxs-lookup"><span data-stu-id="b4e55-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="b4e55-336">Se le preguntará tooplug sus tarjetas de administrador del mundo de seguridad.</span><span class="sxs-lookup"><span data-stu-id="b4e55-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="b4e55-337">Cuando se completa el comando de hello, verá **resultado: correcto** y copia de Hola de su clave con permisos reducidos se encuentran en el archivo de hello llamado key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="b4e55-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="b4e55-338">Puede inspecciona Hola ACL con los siguientes comandos mediante Hola utilidades de Thales:</span><span class="sxs-lookup"><span data-stu-id="b4e55-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="b4e55-339">aclprint.py:</span><span class="sxs-lookup"><span data-stu-id="b4e55-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="b4e55-340">kmfile-dump.exe:</span><span class="sxs-lookup"><span data-stu-id="b4e55-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="b4e55-341">Cuando ejecute estos comandos, reemplace contosokey con hello mismo valor que especificó en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.</span><span class="sxs-lookup"><span data-stu-id="b4e55-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="b4e55-342">Paso 4.2: cifrado de la clave mediante la clave de intercambio de claves de Microsoft</span><span class="sxs-lookup"><span data-stu-id="b4e55-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="b4e55-343">Ejecute uno de hello siga los comandos, según la región geográfica o la instancia de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="b4e55-344">Norteamérica:</span><span class="sxs-lookup"><span data-stu-id="b4e55-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-345">Europa:</span><span class="sxs-lookup"><span data-stu-id="b4e55-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-346">Asia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-347">América Latina:</span><span class="sxs-lookup"><span data-stu-id="b4e55-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-348">Japón:</span><span class="sxs-lookup"><span data-stu-id="b4e55-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-349">Para Corea:</span><span class="sxs-lookup"><span data-stu-id="b4e55-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-350">Para Australia:</span><span class="sxs-lookup"><span data-stu-id="b4e55-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-351">Para [Azure Government](https://azure.microsoft.com/features/gov/), que utiliza la instancia de gobierno de hello Estados Unidos de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-352">Para DoD del Gobierno de Estados Unidos:</span><span class="sxs-lookup"><span data-stu-id="b4e55-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-353">Para Canadá:</span><span class="sxs-lookup"><span data-stu-id="b4e55-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-354">Para Alemania:</span><span class="sxs-lookup"><span data-stu-id="b4e55-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="b4e55-355">Para India:</span><span class="sxs-lookup"><span data-stu-id="b4e55-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="b4e55-356">Cuando ejecute este comando, siga estas instrucciones:</span><span class="sxs-lookup"><span data-stu-id="b4e55-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="b4e55-357">Reemplace *contosokey* con el identificador de Hola que usó toogenerate clave de hello en **3.5 paso: crear una nueva clave** de hello [generar su clave de](#step-3-generate-your-key) paso.</span><span class="sxs-lookup"><span data-stu-id="b4e55-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="b4e55-358">Reemplace *SubscriptionID* con el Id. de Hola de hello suscripción de Azure que contiene el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b4e55-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="b4e55-359">Recuperar este valor anteriormente, en **paso 1.2: obtener el identificador de suscripción de Azure** de hello [preparar su estación de trabajo conectada a Internet](#step-1-prepare-your-internet-connected-workstation) paso.</span><span class="sxs-lookup"><span data-stu-id="b4e55-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="b4e55-360">Reemplace *ContosoFirstHSMKey* por una etiqueta que se usará para el nombre del archivo de salida.</span><span class="sxs-lookup"><span data-stu-id="b4e55-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="b4e55-361">Cuando se complete correctamente, muestra **resultado: correcto** y hay un nuevo archivo en la carpeta actual de Hola que tiene Hola después de nombre: KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="b4e55-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="b4e55-362">Paso 4.3: Copie la transferencia de claves paquete toohello conectada a Internet estación de trabajo</span><span class="sxs-lookup"><span data-stu-id="b4e55-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="b4e55-363">Use una unidad USB u otro archivo de salida de almacenamiento portátil toocopy Hola Hola anterior paso (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour conectada a Internet estación de trabajo.</span><span class="sxs-lookup"><span data-stu-id="b4e55-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="b4e55-364">Paso 5: Transferir su clave tooAzure el almacén de claves</span><span class="sxs-lookup"><span data-stu-id="b4e55-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="b4e55-365">Para este último paso, Hola conectada a Internet estación de trabajo, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) paquete de transferencia de clave de Hola de tooupload de cmdlet que copió de hello desconectado toohello de estación de trabajo HSM del almacén de claves de Azure:</span><span class="sxs-lookup"><span data-stu-id="b4e55-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="b4e55-366">Si carga hello es correcta, verá las propiedades de muestra de Hola de clave de Hola que acaba de agregar.</span><span class="sxs-lookup"><span data-stu-id="b4e55-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b4e55-367">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b4e55-367">Next steps</span></span>
<span data-ttu-id="b4e55-368">Ahora puede usar esta clave protegida con HSM en el almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="b4e55-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="b4e55-369">Para obtener más información, vea hello **si desea que un módulo de seguridad de hardware (HSM) de toouse** sección Hola [Introducción al almacén de claves de Azure](key-vault-get-started.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="b4e55-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
