---
title: "aaaFederating varios Azure AD con ADFS único | Documentos de Microsoft"
description: "En este documento, aprenderá cómo toofederate varios Azure AD con un único AD FS."
keywords: "federar, ADFS, AD FS, varios inquilinos, AD FS único, un ADFS, federación de varios inquilinos, adfs de varios bosques, aad connect, federación, federación entre inquilinos"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Federación de varias instancias de Azure AD con una instancia única de AD FS

Una sola granja de AD FS de alta disponibilidad puede federar varios bosques si existe confianza bidireccional entre ellos. Estos varios bosques pueden o no se corresponde necesariamente toohello mismo Azure Active Directory. Este artículo proporciona instrucciones sobre cómo tooconfigure federación entre una sola implementación de AD FS y más de uno bosques que toodifferent sincronización Azure AD.

![Federación de varios inquilinos con una sola instancia de AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> No se admiten la escritura diferida de dispositivos ni la unión automática de dispositivos en este escenario.

> [!NOTE]
> Azure AD Connect no puede ser federación tooconfigure usado en este escenario porque Azure AD Connect puede configurar la federación para dominios en un único Azure AD.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Pasos para la federación de AD FS con varias instancias de Azure AD

Considere la posibilidad de que un dominio contoso.com en Azure Active Directory contoso.onmicrosoft.com ya está federado con instalado en el entorno de Active Directory de contoso.com local a local de hello AD FS. Fabrikam.com es un dominio en la instancia de Azure Active Directory fabrikam.onmicrosoft.com.

##<a name="step-1-establish-a-two-way-trust"></a>Paso 1: Establecimiento de una confianza bidireccional
 
En AD FS en contoso.com toobe tooauthenticate capaz de usuarios en fabrikam.com, es necesaria una confianza bidireccional entre contoso.com y fabrikam.com. Siga las instrucciones de hello en este [artículo](https://technet.microsoft.com/library/cc816590.aspx) toocreate Hola confianza bidireccional.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Paso 2: Modificación de la configuración de federación de contoso.com 
 
emisor de Hello predeterminado establecido para un tooAD único dominio federado FS es "http://ADFSServiceFQDN/adfs/services/trust", por ejemplo, "http://fs.contoso.com/adfs/services/trust". Azure Active Directory requiere un emisor único para cada dominio federado. Puesto que Hola misma instancia de AD FS va toofederate dos dominios, el valor del emisor de hello debe toobe modificado para que sea único para cada dominio de AD FS que se federa con Azure Active Directory. 
 
En el servidor de AD FS hello, abra PowerShell de Azure AD y realice Hola pasos:
 
Conectarse a Azure Active Directory que contiene la configuración de federación de hello Connect-MsolService actualización contoso.com de dominio Hola para contoso.com Update-MsolFederatedDomain - DomainName contoso.com toohello SupportMultipleDomain:
 
Se cambiará el emisor en configuración de federación del dominio de hello demasiado "http://contoso.com/adfs/services/trust" una emisión de notificaciones y reglas se agregarán para hello Azure AD relación de confianza tooissue Hola correcto issuerId valor basada en el sufijo UPN de Hola.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Paso 3: Federación de fabrikam.com con AD FS
 
En Azure AD powershell sesión realizar pasos de hello: conectar tooAzure Active Directory que contenga Hola dominio fabrikam.com

    Connect-MsolService
Convertir Hola fabrikam.com administrados dominio toofederated:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Hola por encima de la operación va a federar Hola dominio fabrikam.com con hello misma instancia de AD FS. Puede comprobar la configuración del dominio hello mediante el uso de Get-MsolDomainFederationSettings para ambos dominios.

## <a name="next-steps"></a>Pasos siguientes
[Conexión de Active Directory con Azure Active Directory](active-directory-aadconnect.md)
