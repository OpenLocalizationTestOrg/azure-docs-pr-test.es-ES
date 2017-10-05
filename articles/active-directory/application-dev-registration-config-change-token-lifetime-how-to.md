---
title: "Modificación de los valores predeterminados de vigencia de los tokens en una aplicación personalizada | Microsoft Docs"
description: "Aprenda a actualizar las directivas de vigencia de los tokens para la aplicación que está desarrollando en Azure AD"
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
ms.openlocfilehash: a28eacd820ed28a6470992ce86b060e886c00bcb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-change-the-token-lifetime-defaults-for-a-custom-developed-application"></a><span data-ttu-id="ddc1a-103">Modificación de los valores predeterminados de vigencia de los tokens en una aplicación personalizada</span><span class="sxs-lookup"><span data-stu-id="ddc1a-103">How to change the token lifetime defaults for a custom-developed application</span></span>

<span data-ttu-id="ddc1a-104">Azure AD Premium permite a los desarrolladores de aplicaciones y a los administradores de inquilinos configurar la vigencia de los tokens emitidos para clientes no confidenciales.</span><span class="sxs-lookup"><span data-stu-id="ddc1a-104">Azure AD Premium allows app developers and tenant admins to configure the lifetime of tokens issued for non-confidential clients.</span></span> <span data-ttu-id="ddc1a-105">Las directivas de vigencia de los tokens se establecen para todos los inquilinos o para los recursos a los que se va a acceder.</span><span class="sxs-lookup"><span data-stu-id="ddc1a-105">Token lifetime policies are set on a tenant-wide basis or the resources being accessed.</span></span>

 * <span data-ttu-id="ddc1a-106">Para establecer una directiva de vigencia de tokens, debe descargar el [módulo Azure AD PowerShell](https://www.powershellgallery.com/packages/AzureADPreview).</span><span class="sxs-lookup"><span data-stu-id="ddc1a-106">To set a token lifetime policy, you need to download the [Azure AD PowerShell Module](https://www.powershellgallery.com/packages/AzureADPreview).</span></span>

 * <span data-ttu-id="ddc1a-107">Ejecute el comando **Connect-AzureAD -Confirm**.</span><span class="sxs-lookup"><span data-stu-id="ddc1a-107">Run the **Connect-AzureAD -Confirm** command.</span></span>

 * <span data-ttu-id="ddc1a-108">En esta directiva de ejemplo, se establece la actualización del token con arreglo a un único factor de antigüedad máxima.</span><span class="sxs-lookup"><span data-stu-id="ddc1a-108">Here’s an example policy that sets the max age single factor refresh token.</span></span> <span data-ttu-id="ddc1a-109">Cree la directiva: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span><span class="sxs-lookup"><span data-stu-id="ddc1a-109">Create the policy: ```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```</span></span>

 * <span data-ttu-id="ddc1a-110">Consulte el documento sobre la [configuración de la vigencia de los tokens](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) para aprender a crear una directiva personalizada.</span><span class="sxs-lookup"><span data-stu-id="ddc1a-110">Checkout the [Configuring token lifetime](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)   document to learn how to create other custom.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ddc1a-111">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ddc1a-111">Next steps</span></span>
[<span data-ttu-id="ddc1a-112">Configuración de la vigencia de los tokens</span><span class="sxs-lookup"><span data-stu-id="ddc1a-112">Configuring Token Lifetime</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[<span data-ttu-id="ddc1a-113">Referencia de tokens de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ddc1a-113">Azure AD Token Reference</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

