---
title: "Introducción al almacén de claves de Azure Stack | Microsoft Docs"
description: "Aprenda cómo el almacén de claves de Azure Stack administra claves y secretos"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: dc8b5cb299da74c88aa5ae82636dc345ddd45a2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="5ae72-103">Introducción a Key Vault en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5ae72-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="5ae72-104">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="5ae72-104">Before you start</span></span>
<span data-ttu-id="5ae72-105">En este artículo se da por hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="5ae72-105">This article assumes the following:</span></span>

* <span data-ttu-id="5ae72-106">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves.</span><span class="sxs-lookup"><span data-stu-id="5ae72-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="5ae72-107">Los usuarios tienen que [suscribirse a una oferta](azure-stack-subscribe-plan-provision-vm.md) que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5ae72-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="5ae72-108">PowerShell está configurado para su uso con Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5ae72-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="5ae72-109">Conceptos básicos de Key Vault</span><span class="sxs-lookup"><span data-stu-id="5ae72-109">Key Vault basics</span></span>
<span data-ttu-id="5ae72-110">Key Vault en Azure Stack ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="5ae72-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="5ae72-111">Con Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .pfx y contraseñas).</span><span class="sxs-lookup"><span data-stu-id="5ae72-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="5ae72-112">Almacén de claves agiliza el proceso de administración de claves y le permite mantener el control de claves que obtienen acceso a sus datos y los cifran.</span><span class="sxs-lookup"><span data-stu-id="5ae72-112">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="5ae72-113">Los desarrolladores pueden crear claves para desarrollo y prueba en minutos y, a continuación, migrarlas sin problemas a claves de producción.</span><span class="sxs-lookup"><span data-stu-id="5ae72-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="5ae72-114">Los administradores de seguridad pueden conceder (y revocar) permisos a las claves según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="5ae72-114">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="5ae72-115">Cualquiera que tenga una suscripción a Azure Stack puede crear y usar los almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="5ae72-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="5ae72-116">Aunque el almacén de claves se beneficia a los desarrolladores y administradores de seguridad, pueden implementarse y administrado por el Administrador de la nube que administra otros servicios de la pila de Azure para una organización.</span><span class="sxs-lookup"><span data-stu-id="5ae72-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="5ae72-117">Por ejemplo, el Administrador de la nube puede iniciar sesión con una suscripción de la pila de Azure, cree un almacén para la organización en la que se va a almacenar las claves y, a continuación, ser responsable de estas tareas operativas:</span><span class="sxs-lookup"><span data-stu-id="5ae72-117">For example, the cloud administrator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="5ae72-118">Crear o importar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="5ae72-118">Create or import a key or secret</span></span>
* <span data-ttu-id="5ae72-119">Revocar o eliminar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="5ae72-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="5ae72-120">Autorizar usuarios o aplicaciones para acceder al almacén de claves para que puedan administrar o usar sus claves y secretos</span><span class="sxs-lookup"><span data-stu-id="5ae72-120">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="5ae72-121">Configurar el uso de claves (por ejemplo, para firmar o cifrar)</span><span class="sxs-lookup"><span data-stu-id="5ae72-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="5ae72-122">El Administrador de la nube, a continuación, puede proporcionar a los programadores con identificadores URI para llamar desde sus aplicaciones y proporcionar un administrador de seguridad con la información del registro de uso de la clave.</span><span class="sxs-lookup"><span data-stu-id="5ae72-122">The cloud administrator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="5ae72-123">Los desarrolladores también pueden administrar las claves directamente mediante API.</span><span class="sxs-lookup"><span data-stu-id="5ae72-123">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="5ae72-124">Para más información, consulte la guía para desarrolladores de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="5ae72-124">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="5ae72-125">Escenarios</span><span class="sxs-lookup"><span data-stu-id="5ae72-125">Scenarios</span></span>
<span data-ttu-id="5ae72-126">La tabla siguiente muestra algunos de los escenarios en los que Key Vault puede ayudar a satisfacer las necesidades de los desarrolladores y de los administradores de seguridad:</span><span class="sxs-lookup"><span data-stu-id="5ae72-126">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="5ae72-127">Desarrollador para una aplicación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="5ae72-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="5ae72-128">**Problema**: Quiero escribir una aplicación para Azure Stack que use claves para la firma y el cifrado, pero quiero que dichas claves no estén en la propia aplicación, con el fin de que la solución sea adecuada para una aplicación que se distribuya geográficamente.</span><span class="sxs-lookup"><span data-stu-id="5ae72-128">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="5ae72-129">**Instrucción**: Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.</span><span class="sxs-lookup"><span data-stu-id="5ae72-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="5ae72-130">Desarrollador para software como servicio (SaaS)</span><span class="sxs-lookup"><span data-stu-id="5ae72-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="5ae72-131">**Problema**: No quiero asumir la responsabilidad, ni tampoco la posible responsabilidad legal, de las claves y los secretos de mis clientes.</span><span class="sxs-lookup"><span data-stu-id="5ae72-131">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="5ae72-132">**Instrucción**: Los clientes pueden importar sus propias claves a Azure Stack y administrarlas.</span><span class="sxs-lookup"><span data-stu-id="5ae72-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="5ae72-133">Quiero que los clientes sean propietarios y administren sus claves de modo que pueda concentrarme en mi trabajo, que es proporcionar las características de software principales.</span><span class="sxs-lookup"><span data-stu-id="5ae72-133">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="5ae72-134">Responsable principal de la seguridad (CSO)</span><span class="sxs-lookup"><span data-stu-id="5ae72-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="5ae72-135">**Problema**: Deseo asegurarme de que mi organización tiene el control del ciclo de vida de las claves y puedo supervisar el uso de las mismas.</span><span class="sxs-lookup"><span data-stu-id="5ae72-135">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="5ae72-136">**Instrucción**: Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.</span><span class="sxs-lookup"><span data-stu-id="5ae72-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="5ae72-137">Cuando una aplicación necesita realizar operaciones criptográficas utilizando las claves de los clientes, Key Vault lo hace en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="5ae72-137">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="5ae72-138">La aplicación no ve las claves de los clientes.</span><span class="sxs-lookup"><span data-stu-id="5ae72-138">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="5ae72-139">Aunque usamos varios servicios y recursos de Azure Stack, quiero administrar las claves desde una ubicación única en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="5ae72-139">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="5ae72-140">El almacén proporciona una sola interfaz, independientemente del número de almacenes que tenga en Azure Stack, las regiones que admitan y las aplicaciones que los usen.</span><span class="sxs-lookup"><span data-stu-id="5ae72-140">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ae72-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5ae72-141">Next Steps</span></span>

* [<span data-ttu-id="5ae72-142">Administrar Key Vault en Azure Stack mediante el portal</span><span class="sxs-lookup"><span data-stu-id="5ae72-142">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="5ae72-143">Administrar Key Vault en Azure Stack mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="5ae72-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
