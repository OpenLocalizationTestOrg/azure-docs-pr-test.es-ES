---
title: "atributos de la sombra de servicio de sincronización de aaaAzure AD Connect | Documentos de Microsoft"
description: "Describe cómo funcionan los atributos paralelos en el servicio de sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1b8665e7488c6078b655f8a3e35519145bacd898
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="c060a-103">Atributos paralelos del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c060a-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="c060a-104">La mayoría de los atributos se representa Hola de igual manera en Azure AD tal como están en su Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="c060a-104">Most attributes are represented hello same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="c060a-105">Pero algunos atributos tienen algún tratamiento especial y el valor del atributo hello en Azure AD puede ser distinto de lo que se sincroniza en Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c060a-105">But some attributes have some special handling and hello attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="c060a-106">Introducción a los atributos paralelos</span><span class="sxs-lookup"><span data-stu-id="c060a-106">Introducing shadow attributes</span></span>
<span data-ttu-id="c060a-107">Algunos atributos tienen dos representaciones en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c060a-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="c060a-108">Valor de hello local y un valor calculado se almacenan.</span><span class="sxs-lookup"><span data-stu-id="c060a-108">Both hello on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="c060a-109">Estos atributos adicionales se denominan atributos paralelos.</span><span class="sxs-lookup"><span data-stu-id="c060a-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="c060a-110">Hola dos atributos más comunes donde verá este comportamiento son **userPrincipalName** y **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="c060a-110">hello two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="c060a-111">cambio de Hello en valores de atributo ocurre cuando hay valores en estos atributos que representan los dominios no comprobados.</span><span class="sxs-lookup"><span data-stu-id="c060a-111">hello change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="c060a-112">Pero el motor de sincronización de hello en conectar lee valor hello en el atributo de sombra de hello lo desde su perspectiva, atributo Hola se ha confirmado por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c060a-112">But hello sync engine in Connect reads hello value in hello shadow attribute so from its perspective, hello attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="c060a-113">No puede ver los atributos de la sombra de hello mediante Hola portal de Azure o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c060a-113">You cannot see hello shadow attributes using hello Azure portal or with PowerShell.</span></span> <span data-ttu-id="c060a-114">Pero concepto de hello descripción ayuda a tootroubleshoot ciertos escenarios donde el atributo de hello tiene valores diferentes en el servidor local y en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="c060a-114">But understanding hello concept helps you tootroubleshoot certain scenarios where hello attribute has different values on-premises and in hello cloud.</span></span>

<span data-ttu-id="c060a-115">toobetter entender el comportamiento de hello, examine este ejemplo desde Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="c060a-115">toobetter understand hello behavior, look at this example from Fabrikam:</span></span>  
![Dominios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="c060a-117">Tienen varios sufijos UPN en su instancia de Active Directory local, pero solo se ha comprobado uno.</span><span class="sxs-lookup"><span data-stu-id="c060a-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="c060a-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="c060a-118">userPrincipalName</span></span>
<span data-ttu-id="c060a-119">Un usuario tiene Hola después de valores de atributo en un dominio no comprobado:</span><span class="sxs-lookup"><span data-stu-id="c060a-119">A user has hello following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="c060a-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="c060a-120">Attribute</span></span> | <span data-ttu-id="c060a-121">Valor</span><span class="sxs-lookup"><span data-stu-id="c060a-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c060a-122">userPrincipalName local</span><span class="sxs-lookup"><span data-stu-id="c060a-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="c060a-123">shadowUserPrincipalName de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c060a-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="c060a-124">userPrincipalName de Azure AD</span><span class="sxs-lookup"><span data-stu-id="c060a-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="c060a-125">atributo userPrincipalName de Hello es valor de Hola que aparece cuando se usa PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c060a-125">hello userPrincipalName attribute is hello value you see when using PowerShell.</span></span>

<span data-ttu-id="c060a-126">Puesto que el valor del atributo de hello local real se almacena en Azure AD, al comprobar el dominio fabrikam.com de hello, Azure AD actualiza el atributo userPrincipalName de hello con valor de Hola de hello shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="c060a-126">Since hello real on-premises attribute value is stored in Azure AD, when you verify hello fabrikam.com domain, Azure AD updates hello userPrincipalName attribute with hello value from hello shadowUserPrincipalName.</span></span> <span data-ttu-id="c060a-127">No es necesario toosynchronize los cambios de Azure AD Connect para estos toobe valores actualizados.</span><span class="sxs-lookup"><span data-stu-id="c060a-127">You do not have toosynchronize any changes from Azure AD Connect for these values toobe updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="c060a-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="c060a-128">proxyAddresses</span></span>
<span data-ttu-id="c060a-129">Hola mismo proceso para incluir solo dominios comprobados también se produce para proxyAddresses, pero con alguna lógica adicional.</span><span class="sxs-lookup"><span data-stu-id="c060a-129">hello same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="c060a-130">comprobación de Hola para dominios comprobados solo se produce para los usuarios de buzón.</span><span class="sxs-lookup"><span data-stu-id="c060a-130">hello check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="c060a-131">Un usuario habilitado para correo electrónico o un contacto representan un usuario de otra organización de Exchange y puede agregar los valores en objetos de toothese proxyAddresses.</span><span class="sxs-lookup"><span data-stu-id="c060a-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses toothese objects.</span></span>

<span data-ttu-id="c060a-132">Para un usuario del buzón, de forma local o en Exchange Online, aparecen únicamente los valores para los dominios comprobados.</span><span class="sxs-lookup"><span data-stu-id="c060a-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="c060a-133">Debería ser parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="c060a-133">It could look like this:</span></span>

| <span data-ttu-id="c060a-134">Atributo</span><span class="sxs-lookup"><span data-stu-id="c060a-134">Attribute</span></span> | <span data-ttu-id="c060a-135">Valor</span><span class="sxs-lookup"><span data-stu-id="c060a-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="c060a-136">proxyAddresses local</span><span class="sxs-lookup"><span data-stu-id="c060a-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="c060a-137">ProxyAddresses de Exchange Online</span><span class="sxs-lookup"><span data-stu-id="c060a-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="c060a-138">En este caso ** smtp:abbie.spencer@fabrikam.com ** se quitó porque no se ha comprobado el dominio.</span><span class="sxs-lookup"><span data-stu-id="c060a-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="c060a-139">Pero Exchange también agregó **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam no ha usado Lync o Skype local, pero Azure AD y Exchange Online se preparan para ello.</span><span class="sxs-lookup"><span data-stu-id="c060a-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**. Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="c060a-140">Esta lógica para proxyAddresses es que se hace referencia tooas **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="c060a-140">This logic for proxyAddresses is referred tooas **ProxyCalc**.</span></span> <span data-ttu-id="c060a-141">ProxyCalc se llama con cada cambio en un usuario cuando:</span><span class="sxs-lookup"><span data-stu-id="c060a-141">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="c060a-142">usuario de Hola se ha asignado un plan de servicio que incluya Exchange Online, incluso si no se tiene licencia de usuario de Hola para Exchange.</span><span class="sxs-lookup"><span data-stu-id="c060a-142">hello user has been assigned a service plan that includes Exchange Online even if hello user was not licensed for Exchange.</span></span> <span data-ttu-id="c060a-143">Por ejemplo, si se asigna el usuario de Hola Hola E3 SKU de Office, pero solo se asignó SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="c060a-143">For example, if hello user is assigned hello Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="c060a-144">Esto ocurre incluso si el buzón sigue siendo local.</span><span class="sxs-lookup"><span data-stu-id="c060a-144">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="c060a-145">Hola atributo msExchRecipientTypeDetails tiene un valor.</span><span class="sxs-lookup"><span data-stu-id="c060a-145">hello attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="c060a-146">Realiza un cambio tooproxyAddresses o userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="c060a-146">You make a change tooproxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="c060a-147">ProxyCalc puede tardar algún tiempo tooprocess un cambio en un usuario y no está sincronizado con el proceso de exportación de hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c060a-147">ProxyCalc might take some time tooprocess a change on a user and is not synchronous with hello Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="c060a-148">Hola ProxyCalc lógica tiene algunos comportamientos adicionales para escenarios avanzados que no se documentan en este tema.</span><span class="sxs-lookup"><span data-stu-id="c060a-148">hello ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="c060a-149">Este tema está automáticamente toounderstand Hola comportamiento y documenta toda la lógica interna.</span><span class="sxs-lookup"><span data-stu-id="c060a-149">This topic is provided for you toounderstand hello behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="c060a-150">Valores de atributo en cuarentena</span><span class="sxs-lookup"><span data-stu-id="c060a-150">Quarantined attribute values</span></span>
<span data-ttu-id="c060a-151">Los atributos paralelos también se utilizan cuando hay valores de atributo duplicados.</span><span class="sxs-lookup"><span data-stu-id="c060a-151">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="c060a-152">Para más información, consulte [Resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="c060a-152">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="c060a-153">Consulte también</span><span class="sxs-lookup"><span data-stu-id="c060a-153">See also</span></span>
* [<span data-ttu-id="c060a-154">Sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="c060a-154">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="c060a-155">[Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="c060a-155">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
