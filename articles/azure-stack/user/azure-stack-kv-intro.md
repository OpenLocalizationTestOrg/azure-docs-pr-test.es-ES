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
ms.openlocfilehash: ecb542e967669fc4e4465ae59b3e9c37e4a5c332
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="8b7c6-103">Introducción a Key Vault en Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8b7c6-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8b7c6-104">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="8b7c6-104">Before you start</span></span>
<span data-ttu-id="8b7c6-105">En este artículo se da por hecho lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="8b7c6-105">This article assumes the following:</span></span>

* <span data-ttu-id="8b7c6-106">Debe suscribirse a una oferta que incluya el servicio Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-106">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="8b7c6-107">PowerShell está configurado para su uso con Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8b7c6-107">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="8b7c6-108">Conceptos básicos de Key Vault</span><span class="sxs-lookup"><span data-stu-id="8b7c6-108">Key Vault basics</span></span>
<span data-ttu-id="8b7c6-109">Key Vault en Azure Stack ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-109">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="8b7c6-110">Con Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .pfx y contraseñas).</span><span class="sxs-lookup"><span data-stu-id="8b7c6-110">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="8b7c6-111">Almacén de claves agiliza el proceso de administración de claves y le permite mantener el control de claves que obtienen acceso a sus datos y los cifran.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-111">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="8b7c6-112">Los desarrolladores pueden crear claves para desarrollo y prueba en minutos y, a continuación, migrarlas sin problemas a claves de producción.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-112">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="8b7c6-113">Los administradores de seguridad pueden conceder (y revocar) permisos a las claves según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-113">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="8b7c6-114">Cualquiera que tenga una suscripción a Azure Stack puede crear y usar los almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-114">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="8b7c6-115">Aunque Key Vault beneficia a los desarrolladores y los administradores de seguridad, el operador de una organización que administra otros servicios de Azure Stack puede implementarlo y administrarlo.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-115">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the operator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="8b7c6-116">Por ejemplo, el operador de Azure Stack puede iniciar sesión con una suscripción de Azure Stack, crear un almacén para la organización en el que almacenaría las claves y asumir la responsabilidad de las tareas operativas:</span><span class="sxs-lookup"><span data-stu-id="8b7c6-116">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="8b7c6-117">Crear o importar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="8b7c6-117">Create or import a key or secret</span></span>
* <span data-ttu-id="8b7c6-118">Revocar o eliminar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="8b7c6-118">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="8b7c6-119">Autorizar usuarios o aplicaciones para acceder al almacén de claves para que puedan administrar o usar sus claves y secretos</span><span class="sxs-lookup"><span data-stu-id="8b7c6-119">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="8b7c6-120">Configurar el uso de claves (por ejemplo, para firmar o cifrar)</span><span class="sxs-lookup"><span data-stu-id="8b7c6-120">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="8b7c6-121">El operador puede ofrecer después a los desarrolladores los URI para llamar desde sus aplicaciones y proporcionar al administrador de seguridad la información de registro de uso de claves.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-121">The operator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="8b7c6-122">Los desarrolladores también pueden administrar las claves directamente mediante API.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-122">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="8b7c6-123">Para más información, consulte la guía para desarrolladores de Key Vault.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-123">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="8b7c6-124">Escenarios</span><span class="sxs-lookup"><span data-stu-id="8b7c6-124">Scenarios</span></span>
<span data-ttu-id="8b7c6-125">La tabla siguiente muestra algunos de los escenarios en los que Key Vault puede ayudar a satisfacer las necesidades de los desarrolladores y de los administradores de seguridad:</span><span class="sxs-lookup"><span data-stu-id="8b7c6-125">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="8b7c6-126">Desarrollador para una aplicación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8b7c6-126">Developer for an Azure Stack application</span></span>
<span data-ttu-id="8b7c6-127">**Problema**: Quiero escribir una aplicación para Azure Stack que use claves para la firma y el cifrado, pero quiero que dichas claves no estén en la propia aplicación, con el fin de que la solución sea adecuada para una aplicación que se distribuya geográficamente.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-127">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="8b7c6-128">**Instrucción**: Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-128">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="8b7c6-129">Desarrollador para software como servicio (SaaS)</span><span class="sxs-lookup"><span data-stu-id="8b7c6-129">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="8b7c6-130">**Problema**: No quiero asumir la responsabilidad, ni tampoco la posible responsabilidad legal, de las claves y los secretos de mis clientes.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-130">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="8b7c6-131">**Instrucción**: Los clientes pueden importar sus propias claves a Azure Stack y administrarlas.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-131">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="8b7c6-132">Quiero que los clientes sean propietarios y administren sus claves de modo que pueda concentrarme en mi trabajo, que es proporcionar las características de software principales.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-132">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="8b7c6-133">Responsable principal de la seguridad (CSO)</span><span class="sxs-lookup"><span data-stu-id="8b7c6-133">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="8b7c6-134">**Problema**: Deseo asegurarme de que mi organización tiene el control del ciclo de vida de las claves y puedo supervisar el uso de las mismas.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-134">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="8b7c6-135">**Instrucción**: Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-135">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="8b7c6-136">Cuando una aplicación necesita realizar operaciones criptográficas utilizando las claves de los clientes, Key Vault lo hace en nombre de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-136">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="8b7c6-137">La aplicación no ve las claves de los clientes.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-137">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="8b7c6-138">Aunque usamos varios servicios y recursos de Azure Stack, quiero administrar las claves desde una ubicación única en Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-138">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="8b7c6-139">El almacén proporciona una sola interfaz, independientemente del número de almacenes que tenga en Azure Stack, las regiones que admitan y las aplicaciones que los usen.</span><span class="sxs-lookup"><span data-stu-id="8b7c6-139">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b7c6-140">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8b7c6-140">Next Steps</span></span>

* [<span data-ttu-id="8b7c6-141">Administrar Key Vault en Azure Stack mediante el portal</span><span class="sxs-lookup"><span data-stu-id="8b7c6-141">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="8b7c6-142">Administrar Key Vault en Azure Stack mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b7c6-142">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
