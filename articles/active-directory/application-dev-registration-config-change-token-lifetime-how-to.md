---
title: "duración del token hello aaaHow toochange los valores predeterminados para una aplicación desarrollados de forma personalizada | Documentos de Microsoft"
description: "¿Cómo tooupdate las directivas de duración del Token para la aplicación que se está desarrollando en Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 6e1aa1f2a7c33c1f55c5fb619c618ad43cd96273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="0dc37-103">La duración del token toochange hello tiene como valor predeterminado para una aplicación desarrollados de forma personalizada</span><span class="sxs-lookup"><span data-stu-id="0dc37-103">How toochange hello token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="0dc37-104">Azure AD Premium permite a los desarrolladores de aplicaciones y la duración de Hola de tooconfigure de administradores de inquilinos de tokens emitidos para clientes no son confidenciales.</span><span class="sxs-lookup"><span data-stu-id="0dc37-104">Azure AD Premium allows app developers and tenant admins tooconfigure hello lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="0dc37-105">Las directivas de duración del token se establecen en una base de todos los inquilinos o el acceso a recursos Hola.</span><span class="sxs-lookup"><span data-stu-id="0dc37-105">Token lifetime policies are set on a tenant-wide basis or hello resources being accessed.</span></span>

 * <span data-ttu-id="0dc37-106">tooset una directiva de duración del token, necesita hello toodownload [módulo de PowerShell de Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="0dc37-106">tooset a token lifetime policy, you need toodownload hello [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="0dc37-107">Ejecute hello **organización Connect-confirmar** comando.</span><span class="sxs-lookup"><span data-stu-id="0dc37-107">Run hello **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="0dc37-108">Este es un ejemplo de directiva que establece el token de actualización de factor único de antigüedad máxima de Hola.</span><span class="sxs-lookup"><span data-stu-id="0dc37-108">Here’s an example policy that sets hello max age single factor refresh token.</span></span> <span data-ttu-id="0dc37-109">Crear directiva de hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="0dc37-109">Create hello policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="0dc37-110">Hola de desprotección [duración del token configurar](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento toolearn cómo toocreate otro personalizado.</span><span class="sxs-lookup"><span data-stu-id="0dc37-110">Checkout hello [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document toolearn how toocreate other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0dc37-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="0dc37-111">Next steps</span></span>
[<span data-ttu-id="0dc37-112">Configuración de la vigencia de los tokens</span><span class="sxs-lookup"><span data-stu-id="0dc37-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="0dc37-113">Referencia de tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dc37-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

