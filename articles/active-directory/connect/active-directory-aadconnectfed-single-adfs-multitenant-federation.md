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
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a><span data-ttu-id="10681-104">Federación de varias instancias de Azure AD con una instancia única de AD FS</span><span class="sxs-lookup"><span data-stu-id="10681-104">Federate multiple instances of Azure AD with single instance of AD FS</span></span>

<span data-ttu-id="10681-105">Una sola granja de AD FS de alta disponibilidad puede federar varios bosques si existe confianza bidireccional entre ellos.</span><span class="sxs-lookup"><span data-stu-id="10681-105">A single high available AD FS farm can federate multiple forests if they have 2-way trust between them.</span></span> <span data-ttu-id="10681-106">Estos varios bosques pueden o no se corresponde necesariamente toohello mismo Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10681-106">These multiple forests may or may not correspond toohello same Azure Active Directory.</span></span> <span data-ttu-id="10681-107">Este artículo proporciona instrucciones sobre cómo tooconfigure federación entre una sola implementación de AD FS y más de uno bosques que toodifferent sincronización Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10681-107">This article provides instructions on how tooconfigure federation between a single AD FS deployment and more than one forests that sync toodifferent Azure AD.</span></span>

![Federación de varios inquilinos con una sola instancia de AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> <span data-ttu-id="10681-109">No se admiten la escritura diferida de dispositivos ni la unión automática de dispositivos en este escenario.</span><span class="sxs-lookup"><span data-stu-id="10681-109">Device writeback and automatic device join are not supported in this scenario.</span></span>

> [!NOTE]
> <span data-ttu-id="10681-110">Azure AD Connect no puede ser federación tooconfigure usado en este escenario porque Azure AD Connect puede configurar la federación para dominios en un único Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10681-110">Azure AD Connect cannot be used tooconfigure federation in this scenario as Azure AD Connect can configure federation for domains in a single Azure AD.</span></span>

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a><span data-ttu-id="10681-111">Pasos para la federación de AD FS con varias instancias de Azure AD</span><span class="sxs-lookup"><span data-stu-id="10681-111">Steps for federating AD FS with multiple Azure AD</span></span>

<span data-ttu-id="10681-112">Considere la posibilidad de que un dominio contoso.com en Azure Active Directory contoso.onmicrosoft.com ya está federado con instalado en el entorno de Active Directory de contoso.com local a local de hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="10681-112">Consider a domain contoso.com in Azure Active Directory contoso.onmicrosoft.com is already federated with hello AD FS on-premises installed in contoso.com on-premises Active Directory environment.</span></span> <span data-ttu-id="10681-113">Fabrikam.com es un dominio en la instancia de Azure Active Directory fabrikam.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="10681-113">Fabrikam.com is a domain in fabrikam.onmicrosoft.com Azure Active Directory.</span></span>

##<a name="step-1-establish-a-two-way-trust"></a><span data-ttu-id="10681-114">Paso 1: Establecimiento de una confianza bidireccional</span><span class="sxs-lookup"><span data-stu-id="10681-114">Step 1: Establish a two-way trust</span></span>
 
<span data-ttu-id="10681-115">En AD FS en contoso.com toobe tooauthenticate capaz de usuarios en fabrikam.com, es necesaria una confianza bidireccional entre contoso.com y fabrikam.com. Siga las instrucciones de hello en este [artículo](https://technet.microsoft.com/library/cc816590.aspx) toocreate Hola confianza bidireccional.</span><span class="sxs-lookup"><span data-stu-id="10681-115">For AD FS in contoso.com toobe able tooauthenticate users in fabrikam.com, a two-way trust is needed between contoso.com and fabrikam.com. Follow hello guideline in this [article](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello two-way trust.</span></span>
 
##<a name="step-2-modify-contosocom-federation-settings"></a><span data-ttu-id="10681-116">Paso 2: Modificación de la configuración de federación de contoso.com</span><span class="sxs-lookup"><span data-stu-id="10681-116">Step 2: Modify contoso.com federation settings</span></span> 
 
<span data-ttu-id="10681-117">emisor de Hello predeterminado establecido para un tooAD único dominio federado FS es "http://ADFSServiceFQDN/adfs/services/trust", por ejemplo, "http://fs.contoso.com/adfs/services/trust".</span><span class="sxs-lookup"><span data-stu-id="10681-117">hello default issuer set for a single domain federated tooAD FS is "http://ADFSServiceFQDN/adfs/services/trust", for example, “http://fs.contoso.com/adfs/services/trust”.</span></span> <span data-ttu-id="10681-118">Azure Active Directory requiere un emisor único para cada dominio federado.</span><span class="sxs-lookup"><span data-stu-id="10681-118">Azure Active Directory requires unique issuer for each federated domain.</span></span> <span data-ttu-id="10681-119">Puesto que Hola misma instancia de AD FS va toofederate dos dominios, el valor del emisor de hello debe toobe modificado para que sea único para cada dominio de AD FS que se federa con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10681-119">Since hello same AD FS is going toofederate two domains, hello issuer value needs toobe modified so that it is unique for each domain AD FS federates with Azure Active Directory.</span></span> 
 
<span data-ttu-id="10681-120">En el servidor de AD FS hello, abra PowerShell de Azure AD y realice Hola pasos:</span><span class="sxs-lookup"><span data-stu-id="10681-120">On hello AD FS server, open Azure AD PowerShell and perform hello following steps:</span></span>
 
<span data-ttu-id="10681-121">Conectarse a Azure Active Directory que contiene la configuración de federación de hello Connect-MsolService actualización contoso.com de dominio Hola para contoso.com Update-MsolFederatedDomain - DomainName contoso.com toohello SupportMultipleDomain:</span><span class="sxs-lookup"><span data-stu-id="10681-121">Connect toohello Azure Active Directory that contains hello domain contoso.com Connect-MsolService Update hello federation settings for contoso.com Update-MsolFederatedDomain -DomainName contoso.com –SupportMultipleDomain</span></span>
 
<span data-ttu-id="10681-122">Se cambiará el emisor en configuración de federación del dominio de hello demasiado "http://contoso.com/adfs/services/trust" una emisión de notificaciones y reglas se agregarán para hello Azure AD relación de confianza tooissue Hola correcto issuerId valor basada en el sufijo UPN de Hola.</span><span class="sxs-lookup"><span data-stu-id="10681-122">Issuer in hello domain federation setting will be changed too"http://contoso.com/adfs/services/trust" and an issuance claim rule will be added for hello Azure AD Relying Party Trust tooissue hello correct issuerId value based on hello UPN suffix.</span></span>
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a><span data-ttu-id="10681-123">Paso 3: Federación de fabrikam.com con AD FS</span><span class="sxs-lookup"><span data-stu-id="10681-123">Step 3: Federate fabrikam.com with AD FS</span></span>
 
<span data-ttu-id="10681-124">En Azure AD powershell sesión realizar pasos de hello: conectar tooAzure Active Directory que contenga Hola dominio fabrikam.com</span><span class="sxs-lookup"><span data-stu-id="10681-124">In Azure AD powershell session perform hello following steps: Connect tooAzure Active Directory that contains hello domain fabrikam.com</span></span>

    Connect-MsolService
<span data-ttu-id="10681-125">Convertir Hola fabrikam.com administrados dominio toofederated:</span><span class="sxs-lookup"><span data-stu-id="10681-125">Convert hello fabrikam.com managed domain toofederated:</span></span>

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
<span data-ttu-id="10681-126">Hola por encima de la operación va a federar Hola dominio fabrikam.com con hello misma instancia de AD FS.</span><span class="sxs-lookup"><span data-stu-id="10681-126">hello above operation will federate hello domain fabrikam.com with hello same AD FS.</span></span> <span data-ttu-id="10681-127">Puede comprobar la configuración del dominio hello mediante el uso de Get-MsolDomainFederationSettings para ambos dominios.</span><span class="sxs-lookup"><span data-stu-id="10681-127">You can verify hello domain settings by using Get-MsolDomainFederationSettings for both domains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="10681-128">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="10681-128">Next steps</span></span>
[<span data-ttu-id="10681-129">Conexión de Active Directory con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10681-129">Connect Active Directory with Azure Active Directory</span></span>](active-directory-aadconnect.md)
