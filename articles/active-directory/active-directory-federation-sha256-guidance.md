---
title: algoritmo de hash de firma de aaaChange de confianza para usuario autenticado de Office 365 | Documentos de Microsoft
description: "En esta página se proporcionan instrucciones para cambiar el algoritmo SHA para la confianza de federación con Office 365."
keywords: "SHA1,SHA256,O365,federación,aadconnect,adfs,ad fs,cambiar sha,confianza de federación,relación de confianza para usuario autenticado"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="2b664-104">Cambio del algoritmo hash de firma para usuarios de confianza de Office 365</span><span class="sxs-lookup"><span data-stu-id="2b664-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="2b664-105">Información general</span><span class="sxs-lookup"><span data-stu-id="2b664-105">Overview</span></span>
<span data-ttu-id="2b664-106">Los servicios de federación de Active Directory (AD FS) se inicia su tooensure de Azure Active Directory de tooMicrosoft de tokens no pueden manipularse.</span><span class="sxs-lookup"><span data-stu-id="2b664-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="2b664-107">Esta firma se puede basar en SHA1 o SHA256.</span><span class="sxs-lookup"><span data-stu-id="2b664-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="2b664-108">Azure Active Directory ahora es compatible con tokens firmados con un algoritmo SHA256, y es recomendable establecer tooSHA256 de algoritmo de firma de tokens de Hola de mayor nivel de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="2b664-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="2b664-109">Este artículo describen pasos Hola necesarios toohello de algoritmo de firma de tokens de Hola de tooset más segura nivel SHA256.</span><span class="sxs-lookup"><span data-stu-id="2b664-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="2b664-110">Microsoft recomienda el uso de SHA256 como algoritmo de Hola para firmar los tokens tal y como es más seguro que SHA1 pero SHA1 sigue siendo una opción admitida.</span><span class="sxs-lookup"><span data-stu-id="2b664-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="2b664-111">Cambie el algoritmo de firma de tokens de Hola</span><span class="sxs-lookup"><span data-stu-id="2b664-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="2b664-112">Después de que ha configurado el algoritmo de firma de hello con uno de los siguientes dos procesos Hola, AD FS firma tokens de Hola para Office 365 relación de confianza con SHA-256.</span><span class="sxs-lookup"><span data-stu-id="2b664-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="2b664-113">No es necesario toomake los cambios de configuración adicionales, y este cambio no tiene ningún efecto en su tooaccess capacidad Office 365 u otras aplicaciones de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2b664-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="2b664-114">Consola de administración de AD FS</span><span class="sxs-lookup"><span data-stu-id="2b664-114">AD FS management console</span></span>
1. <span data-ttu-id="2b664-115">Abra la consola de administración de hello AD FS en servidor de hello principal de AD FS.</span><span class="sxs-lookup"><span data-stu-id="2b664-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="2b664-116">Expanda el nodo de hello AD FS y haga clic en **Veracidades**.</span><span class="sxs-lookup"><span data-stu-id="2b664-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="2b664-117">Haga clic con el botón derecho en la relación de confianza para usuario autenticado de Office 365 o Azure y seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="2b664-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="2b664-118">Seleccione hello **avanzadas** pestaña y el algoritmo de hash seguro Hola seleccione SHA256.</span><span class="sxs-lookup"><span data-stu-id="2b664-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="2b664-119">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2b664-119">Click **OK**.</span></span>

![Algoritmo de firma SHA256 - MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="2b664-121">Cmdlets de PowerShell de AD FS</span><span class="sxs-lookup"><span data-stu-id="2b664-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="2b664-122">En cualquier servidor de AD FS, abra PowerShell con privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="2b664-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="2b664-123">Algoritmo de hash seguro conjunto hello mediante el uso de hello **Set-AdfsRelyingPartyTrust** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b664-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="2b664-124">Consulte también</span><span class="sxs-lookup"><span data-stu-id="2b664-124">Also read</span></span>
* [<span data-ttu-id="2b664-125">Reparación de la confianza de Office 365 con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2b664-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

