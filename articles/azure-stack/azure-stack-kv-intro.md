---
title: "Introducción de almacén de claves de pila aaaAzure | Documentos de Microsoft"
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
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a><span data-ttu-id="74df2-103">Introducción tooKey almacén en la pila de Azure</span><span class="sxs-lookup"><span data-stu-id="74df2-103">Introduction tooKey Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="74df2-104">Antes de comenzar</span><span class="sxs-lookup"><span data-stu-id="74df2-104">Before you start</span></span>
<span data-ttu-id="74df2-105">En este artículo se da por supuesto siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="74df2-105">This article assumes hello following:</span></span>

* <span data-ttu-id="74df2-106">Deben tener los administradores de la nube de Azure pila [crea una oferta](azure-stack-create-offer.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="74df2-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="74df2-107">Los usuarios deben [suscribirse tooan oferta](azure-stack-subscribe-plan-provision-vm.md) que incluye el servicio de almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="74df2-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="74df2-108">PowerShell está configurado para su uso con Azure Stack</span><span class="sxs-lookup"><span data-stu-id="74df2-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="74df2-109">Conceptos básicos de Key Vault</span><span class="sxs-lookup"><span data-stu-id="74df2-109">Key Vault basics</span></span>
<span data-ttu-id="74df2-110">Key Vault en Azure Stack ayuda a proteger claves criptográficas y secretos usados por servicios y aplicaciones en la nube.</span><span class="sxs-lookup"><span data-stu-id="74df2-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="74df2-111">Con Key Vault, puede cifrar claves y secretos (por ejemplo claves de autenticación, claves de cuenta de almacenamiento, claves de cifrado de datos, archivos .pfx y contraseñas).</span><span class="sxs-lookup"><span data-stu-id="74df2-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="74df2-112">El almacén de claves agiliza el proceso de administración de claves de Hola y permite toomaintain control de claves que tienen acceso y cifrar los datos.</span><span class="sxs-lookup"><span data-stu-id="74df2-112">Key Vault streamlines hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="74df2-113">Los programadores pueden crear claves para desarrollo y pruebas en minutos y, a continuación, perfectamente migrarlos tooproduction claves.</span><span class="sxs-lookup"><span data-stu-id="74df2-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them tooproduction keys.</span></span> <span data-ttu-id="74df2-114">Los administradores de seguridad pueden conceder (y revocar) tookeys de permiso, según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="74df2-114">Security administrators can grant (and revoke) permission tookeys, as needed.</span></span>

<span data-ttu-id="74df2-115">Cualquiera que tenga una suscripción a Azure Stack puede crear y usar los almacenes de claves.</span><span class="sxs-lookup"><span data-stu-id="74df2-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="74df2-116">Aunque el almacén de claves se beneficia a los desarrolladores y administradores de seguridad, pueden implementarse y administrado por el Administrador de la nube de Hola que administra otros servicios de la pila de Azure para una organización.</span><span class="sxs-lookup"><span data-stu-id="74df2-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by hello cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="74df2-117">Por ejemplo, Administrador de la nube de hello puede iniciar sesión con una suscripción de la pila de Azure, cree un almacén para la organización de hello en qué claves toostore y, a continuación, ser responsable de estas tareas operativas:</span><span class="sxs-lookup"><span data-stu-id="74df2-117">For example, hello cloud administrator can sign in with an Azure Stack subscription, create a vault for hello organization in which toostore keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="74df2-118">Crear o importar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="74df2-118">Create or import a key or secret</span></span>
* <span data-ttu-id="74df2-119">Revocar o eliminar una clave o un secreto</span><span class="sxs-lookup"><span data-stu-id="74df2-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="74df2-120">Autorizar a los usuarios o aplicaciones tooaccess Hola almacén de claves, por lo que, a continuación, pueden administrar o usar sus claves y secretos</span><span class="sxs-lookup"><span data-stu-id="74df2-120">Authorize users or applications tooaccess hello key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="74df2-121">Configurar el uso de claves (por ejemplo, para firmar o cifrar)</span><span class="sxs-lookup"><span data-stu-id="74df2-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="74df2-122">Administrador de la nube de Hello, a continuación, puede ofrecer a los desarrolladores con URI toocall desde sus aplicaciones y proporcionar un administrador de seguridad con la información del registro de uso de claves.</span><span class="sxs-lookup"><span data-stu-id="74df2-122">hello cloud administrator can then provide developers with URIs toocall from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="74df2-123">Los desarrolladores también pueden administrar las claves de hello directamente, mediante las API.</span><span class="sxs-lookup"><span data-stu-id="74df2-123">Developers can also manage hello keys directly, by using APIs.</span></span> <span data-ttu-id="74df2-124">Para obtener más información, consulte la Guía del desarrollador del almacén de claves de Hola.</span><span class="sxs-lookup"><span data-stu-id="74df2-124">For more information, see hello Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="74df2-125">Escenarios</span><span class="sxs-lookup"><span data-stu-id="74df2-125">Scenarios</span></span>
<span data-ttu-id="74df2-126">Hello tabla siguiente detallan algunos de los escenarios de hello en el almacén de claves puede ayudar a satisfacer las necesidades de Hola de desarrolladores y administradores de seguridad:</span><span class="sxs-lookup"><span data-stu-id="74df2-126">hello following table depicts some of hello scenarios where Key Vault can help meet hello needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="74df2-127">Desarrollador para una aplicación de Azure Stack</span><span class="sxs-lookup"><span data-stu-id="74df2-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="74df2-128">**Problema**: deseo toowrite una aplicación para la pila de Azure que utiliza claves de firma y cifrado, pero desea que estos toobe externo de mi aplicación para que sea adecuada para una aplicación que se distribuye geográficamente solución Hola.</span><span class="sxs-lookup"><span data-stu-id="74df2-128">**Problem**: I want toowrite an application for Azure Stack that uses keys for signing and encryption, but I want these toobe external from my application so that hello solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="74df2-129">**Instrucción**: Las claves se almacenan en un almacén y las invoca un identificador URI cuando se necesitan.</span><span class="sxs-lookup"><span data-stu-id="74df2-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="74df2-130">Desarrollador para software como servicio (SaaS)</span><span class="sxs-lookup"><span data-stu-id="74df2-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="74df2-131">**Problema:** no deseo responsabilidad de responsabilidad o potencial de hello Mi cliente las claves y secretos.</span><span class="sxs-lookup"><span data-stu-id="74df2-131">**Problem:** I don’t want hello responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="74df2-132">**Instrucción**: Los clientes pueden importar sus propias claves a Azure Stack y administrarlas.</span><span class="sxs-lookup"><span data-stu-id="74df2-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="74df2-133">Desea tooown de los clientes y administrar sus claves de modo que puedo concentrarse en hacer ¿qué hacer mejor, que proporciona características de software de hello principales.</span><span class="sxs-lookup"><span data-stu-id="74df2-133">I want customers tooown and manage their keys so that I can concentrate on doing what I do best, which is providing hello core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="74df2-134">Responsable principal de la seguridad (CSO)</span><span class="sxs-lookup"><span data-stu-id="74df2-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="74df2-135">**Problema:** desea toomake seguro de que mi organización en el control del ciclo de vida de clave de Hola y puede supervisar el uso de claves.</span><span class="sxs-lookup"><span data-stu-id="74df2-135">**Problem:** I want toomake sure that my organization is in control of hello key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="74df2-136">**Instrucción**: Key Vault está diseñado de modo que Microsoft no pueda ver ni extraer sus claves.</span><span class="sxs-lookup"><span data-stu-id="74df2-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="74df2-137">Cuando una aplicación necesita operaciones criptográficas tooperform mediante el uso de claves de los clientes, el almacén de claves se consigue en nombre de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="74df2-137">When an application needs tooperform cryptographic operations by using customers’ keys, Key Vault does this on behalf of hello application.</span></span> <span data-ttu-id="74df2-138">aplicación Hello no ve las claves de los clientes de Hola.</span><span class="sxs-lookup"><span data-stu-id="74df2-138">hello application does not see hello customers’ keys.</span></span>  <span data-ttu-id="74df2-139">Aunque se usan varios servicios de la pila de Azure y recursos, deseo que las claves de hello toomanage desde una sola ubicación en la pila de Azure.</span><span class="sxs-lookup"><span data-stu-id="74df2-139">Although we use multiple Azure Stack services and resources, I want toomanage hello keys from a single location in Azure Stack.</span></span> <span data-ttu-id="74df2-140">almacén de Hello proporciona una única interfaz, independientemente de cuántos almacenes tiene en pila de Azure, qué regiones soporte técnico y usarlos en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="74df2-140">hello vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74df2-141">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="74df2-141">Next Steps</span></span>

* [<span data-ttu-id="74df2-142">Administrar el almacén de claves en la pila de Azure mediante el portal de Hola</span><span class="sxs-lookup"><span data-stu-id="74df2-142">Manage Key Vault in Azure Stack using hello portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="74df2-143">Administrar Key Vault en Azure Stack mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="74df2-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
