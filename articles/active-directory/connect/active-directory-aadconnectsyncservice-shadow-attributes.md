---
title: "Atributos paralelos del servicio de sincronización de Azure AD Connect | Microsoft Docs"
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
ms.openlocfilehash: 0b6a7f22d744480a40a878c979986cdd7667109c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-service-shadow-attributes"></a><span data-ttu-id="9da07-103">Atributos paralelos del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9da07-103">Azure AD Connect sync service shadow attributes</span></span>
<span data-ttu-id="9da07-104">La mayoría de los atributos se representan del mismo modo en Azure AD, ya que se encuentran en el Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="9da07-104">Most attributes are represented the same way in Azure AD as they are in your on-premises Active Directory.</span></span> <span data-ttu-id="9da07-105">Pero algunos atributos tienen algún tratamiento especial y el valor del atributo en Azure AD puede ser distinto de lo que sincroniza Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9da07-105">But some attributes have some special handling and the attribute value in Azure AD might be different than what Azure AD Connect synchronizes.</span></span>

## <a name="introducing-shadow-attributes"></a><span data-ttu-id="9da07-106">Introducción a los atributos paralelos</span><span class="sxs-lookup"><span data-stu-id="9da07-106">Introducing shadow attributes</span></span>
<span data-ttu-id="9da07-107">Algunos atributos tienen dos representaciones en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9da07-107">Some attributes have two representations in Azure AD.</span></span> <span data-ttu-id="9da07-108">Se almacenan el valor local y un valor calculado.</span><span class="sxs-lookup"><span data-stu-id="9da07-108">Both the on-premises value and a calculated value are stored.</span></span> <span data-ttu-id="9da07-109">Estos atributos adicionales se denominan atributos paralelos.</span><span class="sxs-lookup"><span data-stu-id="9da07-109">These extra attributes are called shadow attributes.</span></span> <span data-ttu-id="9da07-110">Los dos atributos más comunes donde verá este comportamiento son **userPrincipalName** y **proxyAddress**.</span><span class="sxs-lookup"><span data-stu-id="9da07-110">The two most common attributes where you see this behavior are **userPrincipalName** and **proxyAddress**.</span></span> <span data-ttu-id="9da07-111">El cambio de los valores de atributo se produce cuando hay valores de estos atributos que representan los dominios no comprobados.</span><span class="sxs-lookup"><span data-stu-id="9da07-111">The change in attribute values happens when there are values in these attributes representing non-verified domains.</span></span> <span data-ttu-id="9da07-112">Pero el motor de sincronización de Connect lee el valor del atributo paralelo, por lo que desde su perspectiva, el atributo se ha confirmado por Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9da07-112">But the sync engine in Connect reads the value in the shadow attribute so from its perspective, the attribute has been confirmed by Azure AD.</span></span>

<span data-ttu-id="9da07-113">No se pueden ver los atributos paralelos mediante Azure Portal o con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9da07-113">You cannot see the shadow attributes using the Azure portal or with PowerShell.</span></span> <span data-ttu-id="9da07-114">Pero entender el concepto le ayudará a solucionar los problemas de determinados escenarios donde el atributo tiene valores diferentes tanto en local como en la nube.</span><span class="sxs-lookup"><span data-stu-id="9da07-114">But understanding the concept helps you to troubleshoot certain scenarios where the attribute has different values on-premises and in the cloud.</span></span>

<span data-ttu-id="9da07-115">Para comprender mejor el comportamiento, vea este ejemplo de Fabrikam:</span><span class="sxs-lookup"><span data-stu-id="9da07-115">To better understand the behavior, look at this example from Fabrikam:</span></span>  
![Dominios](./media/active-directory-aadconnectsyncservice-shadow-attributes/domains.png)  
<span data-ttu-id="9da07-117">Tienen varios sufijos UPN en su instancia de Active Directory local, pero solo se ha comprobado uno.</span><span class="sxs-lookup"><span data-stu-id="9da07-117">They have multiple UPN suffixes in their on-premises Active Directory, but they have only verified one.</span></span>

### <a name="userprincipalname"></a><span data-ttu-id="9da07-118">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="9da07-118">userPrincipalName</span></span>
<span data-ttu-id="9da07-119">Un usuario tiene los siguientes valores de atributo en un dominio no comprobado:</span><span class="sxs-lookup"><span data-stu-id="9da07-119">A user has the following attribute values in a non-verified domain:</span></span>

| <span data-ttu-id="9da07-120">Atributo</span><span class="sxs-lookup"><span data-stu-id="9da07-120">Attribute</span></span> | <span data-ttu-id="9da07-121">Valor</span><span class="sxs-lookup"><span data-stu-id="9da07-121">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9da07-122">userPrincipalName local</span><span class="sxs-lookup"><span data-stu-id="9da07-122">on-premises userPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="9da07-123">shadowUserPrincipalName de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9da07-123">Azure AD shadowUserPrincipalName</span></span> | lee.sperry@fabrikam.com |
| <span data-ttu-id="9da07-124">userPrincipalName de Azure AD</span><span class="sxs-lookup"><span data-stu-id="9da07-124">Azure AD userPrincipalName</span></span> | lee.sperry@fabrikam.onmicrosoft.com |

<span data-ttu-id="9da07-125">El atributo userPrincipalName es el valor que aparece cuando se usa PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9da07-125">The userPrincipalName attribute is the value you see when using PowerShell.</span></span>

<span data-ttu-id="9da07-126">Puesto que el valor del atributo local real se almacena en Azure AD, al comprobar el dominio fabrikam.com, Azure AD actualiza el atributo userPrincipalName con el valor de shadowUserPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="9da07-126">Since the real on-premises attribute value is stored in Azure AD, when you verify the fabrikam.com domain, Azure AD updates the userPrincipalName attribute with the value from the shadowUserPrincipalName.</span></span> <span data-ttu-id="9da07-127">No es necesario sincronizar los cambios de Azure AD Connect para que se actualicen estos valores.</span><span class="sxs-lookup"><span data-stu-id="9da07-127">You do not have to synchronize any changes from Azure AD Connect for these values to be updated.</span></span>

### <a name="proxyaddresses"></a><span data-ttu-id="9da07-128">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="9da07-128">proxyAddresses</span></span>
<span data-ttu-id="9da07-129">El mismo proceso para incluir solo dominios comprobados también se produce para proxyAddresses, pero con alguna lógica adicional.</span><span class="sxs-lookup"><span data-stu-id="9da07-129">The same process for only including verified domains also occurs for proxyAddresses, but with some additional logic.</span></span> <span data-ttu-id="9da07-130">La comprobación de dominios comprobados solo se produce para los usuarios de buzón.</span><span class="sxs-lookup"><span data-stu-id="9da07-130">The check for verified domains only happens for mailbox users.</span></span> <span data-ttu-id="9da07-131">Un usuario habilitado para correo o un contacto representa un usuario de otra organización de Exchange y puede agregar los valores de proxyAddresses en estos objetos.</span><span class="sxs-lookup"><span data-stu-id="9da07-131">A mail-enabled user or contact represent a user in another Exchange organization and you can add any values in proxyAddresses to these objects.</span></span>

<span data-ttu-id="9da07-132">Para un usuario del buzón, de forma local o en Exchange Online, aparecen únicamente los valores para los dominios comprobados.</span><span class="sxs-lookup"><span data-stu-id="9da07-132">For a mailbox user, either on-premises or in Exchange Online, only values for verified domains appear.</span></span> <span data-ttu-id="9da07-133">Debería ser parecido a esto:</span><span class="sxs-lookup"><span data-stu-id="9da07-133">It could look like this:</span></span>

| <span data-ttu-id="9da07-134">Atributo</span><span class="sxs-lookup"><span data-stu-id="9da07-134">Attribute</span></span> | <span data-ttu-id="9da07-135">Valor</span><span class="sxs-lookup"><span data-stu-id="9da07-135">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9da07-136">proxyAddresses local</span><span class="sxs-lookup"><span data-stu-id="9da07-136">on-premises proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie.spencer@fabrikam.com</br>smtp:abbie@fabrikamonline.com |
| <span data-ttu-id="9da07-137">ProxyAddresses de Exchange Online</span><span class="sxs-lookup"><span data-stu-id="9da07-137">Exchange Online proxyAddresses</span></span> | SMTP:abbie.spencer@fabrikamonline.com</br>smtp:abbie@fabrikamonline.com</br>SIP:abbie.spencer@fabrikamonline.com |

<span data-ttu-id="9da07-138">En este caso  **smtp:abbie.spencer@fabrikam.com**  se quitó porque no se ha comprobado el dominio.</span><span class="sxs-lookup"><span data-stu-id="9da07-138">In this case **smtp:abbie.spencer@fabrikam.com** was removed since that domain has not been verified.</span></span> <span data-ttu-id="9da07-139">Pero Exchange también agregó **SIP:abbie.spencer@fabrikamonline.com**.</span><span class="sxs-lookup"><span data-stu-id="9da07-139">But Exchange also added **SIP:abbie.spencer@fabrikamonline.com**.</span></span> <span data-ttu-id="9da07-140">Fabrikam no ha usado Lync o Skype local, pero Azure AD y Exchange Online se preparan para ello.</span><span class="sxs-lookup"><span data-stu-id="9da07-140">Fabrikam has not used Lync/Skype on-premises, but Azure AD and Exchange Online prepare for it.</span></span>

<span data-ttu-id="9da07-141">Esta lógica para proxyAddresses se conoce como **ProxyCalc**.</span><span class="sxs-lookup"><span data-stu-id="9da07-141">This logic for proxyAddresses is referred to as **ProxyCalc**.</span></span> <span data-ttu-id="9da07-142">ProxyCalc se llama con cada cambio en un usuario cuando:</span><span class="sxs-lookup"><span data-stu-id="9da07-142">ProxyCalc is invoked with every change on a user when:</span></span>

- <span data-ttu-id="9da07-143">Al usuario se ha asignado un plan de servicio que incluye Exchange Online, incluso si el usuario no se tiene licencia para Exchange.</span><span class="sxs-lookup"><span data-stu-id="9da07-143">The user has been assigned a service plan that includes Exchange Online even if the user was not licensed for Exchange.</span></span> <span data-ttu-id="9da07-144">Por ejemplo, si al usuario se le asigna la SKU de Office E3, pero solo se asignó SharePoint Online.</span><span class="sxs-lookup"><span data-stu-id="9da07-144">For example, if the user is assigned the Office E3 SKU, but only was assigned SharePoint Online.</span></span> <span data-ttu-id="9da07-145">Esto ocurre incluso si el buzón sigue siendo local.</span><span class="sxs-lookup"><span data-stu-id="9da07-145">This is true even if your mailbox is still on-premises.</span></span>
- <span data-ttu-id="9da07-146">El atributo msExchRecipientTypeDetails tiene un valor.</span><span class="sxs-lookup"><span data-stu-id="9da07-146">The attribute msExchRecipientTypeDetails has a value.</span></span>
- <span data-ttu-id="9da07-147">Realiza un cambio en proxyAddresses o userPrincipalName.</span><span class="sxs-lookup"><span data-stu-id="9da07-147">You make a change to proxyAddresses or userPrincipalName.</span></span>

<span data-ttu-id="9da07-148">ProxyCalc puede tardar algún tiempo en procesar un cambio en un usuario y no está sincronizado con el proceso de exportación de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9da07-148">ProxyCalc might take some time to process a change on a user and is not synchronous with the Azure AD Connect export process.</span></span>

> [!NOTE]
> <span data-ttu-id="9da07-149">La lógica de ProxyCalc tiene algunos comportamientos adicionales para escenarios avanzados que no se documentan en este tema.</span><span class="sxs-lookup"><span data-stu-id="9da07-149">The ProxyCalc logic has some additional behaviors for advanced scenarios not documented in this topic.</span></span> <span data-ttu-id="9da07-150">Este tema se proporciona para que pueda entender el comportamiento y no tener que documentar toda la lógica interna.</span><span class="sxs-lookup"><span data-stu-id="9da07-150">This topic is provided for you to understand the behavior and not document all internal logic.</span></span>

### <a name="quarantined-attribute-values"></a><span data-ttu-id="9da07-151">Valores de atributo en cuarentena</span><span class="sxs-lookup"><span data-stu-id="9da07-151">Quarantined attribute values</span></span>
<span data-ttu-id="9da07-152">Los atributos paralelos también se utilizan cuando hay valores de atributo duplicados.</span><span class="sxs-lookup"><span data-stu-id="9da07-152">Shadow attributes are also used when there are duplicate attribute values.</span></span> <span data-ttu-id="9da07-153">Para más información, consulte [Resistencia de atributos duplicados](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span><span class="sxs-lookup"><span data-stu-id="9da07-153">For more information, see [duplicate attribute resiliency](active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9da07-154">Consulte también</span><span class="sxs-lookup"><span data-stu-id="9da07-154">See also</span></span>
* [<span data-ttu-id="9da07-155">Sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9da07-155">Azure AD Connect sync</span></span>](active-directory-aadconnectsync-whatis.md)
* <span data-ttu-id="9da07-156">[Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="9da07-156">[Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
