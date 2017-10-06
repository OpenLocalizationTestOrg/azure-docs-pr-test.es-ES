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
# <a name="how-toochange-hello-token-lifetime-defaults-for-a-custom-developed-application"></a>La duración del token toochange hello tiene como valor predeterminado para una aplicación desarrollados de forma personalizada

Azure AD Premium permite a los desarrolladores de aplicaciones y la duración de Hola de tooconfigure de administradores de inquilinos de tokens emitidos para clientes no son confidenciales. Las directivas de duración del token se establecen en una base de todos los inquilinos o el acceso a recursos Hola.

 * tooset una directiva de duración del token, necesita hello toodownload [módulo de PowerShell de Azure AD](https://www.powershellgallery.com/packages/AzureADPreview).

 * Ejecute hello **organización Connect-confirmar** comando.

 * Este es un ejemplo de directiva que establece el token de actualización de factor único de antigüedad máxima de Hola. Crear directiva de hello:```New-AzureADPolicy -Definition @('{"TokenLifetimePolicy":{"Version":1, "MaxAgeSingleFactor":"until-revoked"}}') -DisplayName "OrganizationDefaultPolicyScenario" -IsOrganizationDefault $true -Type "TokenLifetimePolicy"```

 * Hola de desprotección [duración del token configurar](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes) documento toolearn cómo toocreate otro personalizado.

## <a name="next-steps"></a>Pasos siguientes
[Configuración de la vigencia de los tokens](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-configurable-token-lifetimes)<br>

[Referencia de tokens de Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-token-and-claims)

