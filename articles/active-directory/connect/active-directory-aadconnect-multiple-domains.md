---
title: Varios dominios de Azure AD Connect
description: "En este documento se describe cómo instalar y configurar varios dominios de nivel superior con O365 y Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="4484e-103">Compatibilidad con varios dominios para la federación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="4484e-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="4484e-104">La siguiente documentación proporciona orientación sobre cómo usar varios dominios y subdominios de nivel superior al federarse con Office 365 o con dominios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4484e-104">The following documentation provides guidance on how to use multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="4484e-105">Compatibilidad con varios dominios de nivel superior</span><span class="sxs-lookup"><span data-stu-id="4484e-105">Multiple top-level domain support</span></span>
<span data-ttu-id="4484e-106">La federación de varios dominios de nivel superior con Azure AD requiere una configuración adicional que no es necesaria al federarse con un dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="4484e-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="4484e-107">Cuando se federa un dominio con Azure AD, se establecen varias propiedades en el dominio de Azure.</span><span class="sxs-lookup"><span data-stu-id="4484e-107">When a domain is federated with Azure AD, several properties are set on the domain in Azure.</span></span>  <span data-ttu-id="4484e-108">Una propiedad importante es IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="4484e-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="4484e-109">Se trata de un URI que Azure AD usa para identificar el dominio al que está asociado el token.</span><span class="sxs-lookup"><span data-stu-id="4484e-109">This is a URI that is used by Azure AD to identify the domain that the token is associated with.</span></span>  <span data-ttu-id="4484e-110">El URI no necesita resolver nada, pero debe ser un URI válido.</span><span class="sxs-lookup"><span data-stu-id="4484e-110">The URI doesn’t need to resolve to anything but it must be a valid URI.</span></span>  <span data-ttu-id="4484e-111">De forma predeterminada, Azure AD lo establece en el valor del identificador del servicio de federación en la configuración local de AD FS.</span><span class="sxs-lookup"><span data-stu-id="4484e-111">By default, Azure AD sets this to the value of the federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="4484e-112">El identificador del servicio de federación es un URI que identifica de forma única un servicio de federación.</span><span class="sxs-lookup"><span data-stu-id="4484e-112">The federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="4484e-113">El servicio de federación es una instancia de AD FS que funciona como el servicio de token de seguridad.</span><span class="sxs-lookup"><span data-stu-id="4484e-113">The federation service is an instance of AD FS that functions as the security token service.</span></span> 
> 
> 

<span data-ttu-id="4484e-114">Para ver el valor de IssuerUri, use el comando de PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="4484e-114">You can vew IssuerUri by using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="4484e-116">Se produce un problema cuando se quiere agregar más de un dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="4484e-116">A problem arises when we want to add more than one top-level domain.</span></span>  <span data-ttu-id="4484e-117">Por ejemplo, supongamos que ha configurado la federación entre Azure AD y el entorno local.</span><span class="sxs-lookup"><span data-stu-id="4484e-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="4484e-118">Para este documento uso bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="4484e-118">For this document I am using bmcontoso.com.</span></span>  <span data-ttu-id="4484e-119">Ahora he agregado un segundo dominio de nivel superior, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="4484e-119">Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Dominios](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="4484e-121">Cuando se intenta convertir el dominio bmfabrikam.com en federado, se recibe un error.</span><span class="sxs-lookup"><span data-stu-id="4484e-121">When we attempt to convert our bmfabrikam.com domain to be federated, we receive an error.</span></span>  <span data-ttu-id="4484e-122">Esto se debe a que Azure AD tiene una restricción que no permite que la propiedad IssuerUri tenga el mismo valor para más de un dominio.</span><span class="sxs-lookup"><span data-stu-id="4484e-122">The reason for this is, Azure AD has a constraint that does not allow the IssuerUri property to have the same value for more than one domain.</span></span>  

![Error de federación](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="4484e-124">Parámetro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="4484e-124">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="4484e-125">Para solucionarlo necesitamos agregar un valor de IssuerUri diferente, lo que puede hacerse mediante el parámetro `-SupportMultipleDomain` .</span><span class="sxs-lookup"><span data-stu-id="4484e-125">To workaround this, we need to add a different IssuerUri which can be done by using the `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="4484e-126">Este parámetro se usa con los cmdlets siguientes:</span><span class="sxs-lookup"><span data-stu-id="4484e-126">This parameter is used with the following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="4484e-127">Este parámetro hace que Azure AD configure el valor de IssuerUri para que se base en el nombre del dominio.</span><span class="sxs-lookup"><span data-stu-id="4484e-127">This parameter makes Azure AD configure the IssuerUri so that it is based on the name of the domain.</span></span>  <span data-ttu-id="4484e-128">Este será único en los directorios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4484e-128">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="4484e-129">El uso del parámetro permite que el comando de PowerShell se complete correctamente.</span><span class="sxs-lookup"><span data-stu-id="4484e-129">Using the parameter allows the PowerShell command to complete successfully.</span></span>

![Error de federación](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="4484e-131">Si examina la configuración del nuevo dominio bmfabrikam.com, observará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4484e-131">Looking at the settings of our new bmfabrikam.com domain you can see the following:</span></span>

![Error de federación](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="4484e-133">Tenga en cuenta que `-SupportMultipleDomain` no cambia los otros puntos de conexión que todavía están configurados para apuntar al servicio de federación de adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="4484e-133">Note that `-SupportMultipleDomain` does not change the other endpoints which are still configured to point to our federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="4484e-134">Otra cosa que hace `-SupportMultipleDomain` es garantizar que el sistema de AD FS incluya el valor Issuer apropiado en los tokens emitidos para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4484e-134">Another thing that `-SupportMultipleDomain` does is that it ensures that the AD FS system includes the proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="4484e-135">Para ello, toma la parte de dominio del UPN de los usuarios y la establece como dominio en IssuerUri, es decir, https://{upn suffix}/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="4484e-135">It does this by taking the domain portion of the users UPN and setting this as the domain in the IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="4484e-136">Por lo tanto, durante la autenticación en Azure AD u Office 365, el elemento IssuerUri del token del usuario se usa para buscar el dominio en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4484e-136">Thus during authentication to Azure AD or Office 365, the IssuerUri element in the user’s token is used to locate the domain in Azure AD.</span></span>  <span data-ttu-id="4484e-137">Si no se encuentra una coincidencia, se producirá un error en la autenticación.</span><span class="sxs-lookup"><span data-stu-id="4484e-137">If a match cannot be found the authentication will fail.</span></span> 

<span data-ttu-id="4484e-138">Por ejemplo, si un usuario del UPN es bsimon@bmcontoso.com, el elemento IssuerUri en los problemas de símbolo (token) de AD FS se establecerá en http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="4484e-138">For example, if a user’s UPN is bsimon@bmcontoso.com, the IssuerUri element in the token AD FS issues will be set to http://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="4484e-139">Coincidirá con la configuración de Azure AD y la autenticación se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="4484e-139">This will match the Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="4484e-140">A continuación se muestra la regla de notificaciones personalizada que implementa esta lógica:</span><span class="sxs-lookup"><span data-stu-id="4484e-140">The following is the customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="4484e-141">Para poder usar el modificador -SupportMultipleDomain al intentar agregar dominios nuevos o convertir dominios ya agregados, debe tener configurada la confianza federada de modo que los admita originalmente.</span><span class="sxs-lookup"><span data-stu-id="4484e-141">In order to use the -SupportMultipleDomain switch when attempting to add new or convert already added domains, you need to have setup your federated trust to support them originally.</span></span>  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="4484e-142">Actualización de la confianza entre AD FS y Azure AD</span><span class="sxs-lookup"><span data-stu-id="4484e-142">How to update the trust between AD FS and Azure AD</span></span>
<span data-ttu-id="4484e-143">Si no configuró la confianza federada entre AD FS y la instancia de Azure AD, podría tener que volver a crear esta confianza.</span><span class="sxs-lookup"><span data-stu-id="4484e-143">If you did not setup the federated trust between AD FS and your instance of Azure AD, you may need to re-create this trust.</span></span>  <span data-ttu-id="4484e-144">Esto se debe a que, cuando se configura originalmente sin el parámetro `-SupportMultipleDomain` , el valor de IssuerUri se establece como predeterminado.</span><span class="sxs-lookup"><span data-stu-id="4484e-144">This is because, when it is originally setup without the `-SupportMultipleDomain` parameter, the IssuerUri is set with the default value.</span></span>  <span data-ttu-id="4484e-145">En la captura de pantalla siguiente se puede ver que el elemento IssuerUri se establece en https://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="4484e-145">In the screenshot below you can see the IssuerUri is set to https://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="4484e-146">Ahora, si hemos agregado correctamente un nuevo dominio en el Portal de Azure AD e intentamos convertirlo con `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtendremos el error siguiente.</span><span class="sxs-lookup"><span data-stu-id="4484e-146">So now, if we have successfully added an new domain in the Azure AD portal and then attempt to convert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get the following error.</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="4484e-148">Si intenta agregar el modificador `-SupportMultipleDomain` , aparecerá el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="4484e-148">If you try to add the `-SupportMultipleDomain` switch we will receive the following error:</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="4484e-150">El simple hecho de intentar ejecutar `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` en el dominio original también producirá un error.</span><span class="sxs-lookup"><span data-stu-id="4484e-150">Simply trying to run `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on the original domain will also result in an error.</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="4484e-152">Siga los pasos indicados a continuación para agregar otro dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="4484e-152">Use the steps below to add an additional top-level domain.</span></span>  <span data-ttu-id="4484e-153">Si ya ha agregado un dominio y no ha usado el parámetro `-SupportMultipleDomain` , empiece por los pasos para quitar y actualizar el dominio original.</span><span class="sxs-lookup"><span data-stu-id="4484e-153">If you have already added a domain and did not use the `-SupportMultipleDomain` parameter start with the steps for removing and updating your original domain.</span></span>  <span data-ttu-id="4484e-154">Si todavía no ha agregado un dominio de nivel superior, puede comenzar por los pasos para agregar un dominio con PowerShell de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4484e-154">If you have not added a top-level domain yet you can start with the steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="4484e-155">Siga los pasos indicados a continuación para quitar la confianza de Microsoft Online y actualizar el dominio original.</span><span class="sxs-lookup"><span data-stu-id="4484e-155">Use the following steps to remove the Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="4484e-156">En el servidor de federación de AD FS, abra **Administración de AD FS.**</span><span class="sxs-lookup"><span data-stu-id="4484e-156">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="4484e-157">A la izquierda, expanda **Relaciones de confianza** y **Confianzas de usuario de confianza**.</span><span class="sxs-lookup"><span data-stu-id="4484e-157">On the left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="4484e-158">A la derecha, elimine la entrada **Plataforma de identidad de Microsoft Office 365** .</span><span class="sxs-lookup"><span data-stu-id="4484e-158">On the right, delete the **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="4484e-159">![Quitar Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="4484e-159">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="4484e-160">En un equipo que tenga instalado el [Módulo de Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), ejecute lo siguiente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="4484e-160">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="4484e-161">Escriba el nombre de usuario y la contraseña de un administrador global del dominio de Azure AD con el que se esté federando.</span><span class="sxs-lookup"><span data-stu-id="4484e-161">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="4484e-162">En PowerShell, escriba `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="4484e-162">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="4484e-163">En PowerShell, escriba `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="4484e-163">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="4484e-164">Esto es para el dominio original.</span><span class="sxs-lookup"><span data-stu-id="4484e-164">This is for the original domain.</span></span>  <span data-ttu-id="4484e-165">Si se usan los dominios anteriores, sería: `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="4484e-165">So using the above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="4484e-166">Siga los pasos que se indican a continuación para agregar el nuevo dominio de nivel superior con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4484e-166">Use the following steps to add the new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="4484e-167">En un equipo que tenga instalado el [Módulo de Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), ejecute lo siguiente: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="4484e-167">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run the following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="4484e-168">Escriba el nombre de usuario y la contraseña de un administrador global del dominio de Azure AD con el que se esté federando.</span><span class="sxs-lookup"><span data-stu-id="4484e-168">Enter the username and password of a global administrator for the Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="4484e-169">En PowerShell, escriba `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="4484e-169">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="4484e-170">En PowerShell, escriba `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="4484e-170">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="4484e-171">Siga los pasos que se indican a continuación para agregar el nuevo dominio de nivel superior con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4484e-171">Use the following steps to add the new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="4484e-172">Inicie Azure AD Connect desde el escritorio o el menú Inicio.</span><span class="sxs-lookup"><span data-stu-id="4484e-172">Launch Azure AD Connect from the desktop or start menu</span></span>
2. <span data-ttu-id="4484e-173">Elija "Agregar un dominio de Azure AD adicional" ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="4484e-173">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="4484e-174">Escriba sus credenciales de Azure AD y Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4484e-174">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="4484e-175">Seleccione el segundo dominio que desea configurar para federación.</span><span class="sxs-lookup"><span data-stu-id="4484e-175">Select the second domain you wish to configure for federation.</span></span>
   <span data-ttu-id="4484e-176">![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="4484e-176">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="4484e-177">Haga clic en Instalar.</span><span class="sxs-lookup"><span data-stu-id="4484e-177">Click Install</span></span>

### <a name="verify-the-new-top-level-domain"></a><span data-ttu-id="4484e-178">Comprobación del nuevo dominio de nivel superior</span><span class="sxs-lookup"><span data-stu-id="4484e-178">Verify the new top-level domain</span></span>
<span data-ttu-id="4484e-179">Con el comando de PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`, puede ver el valor de IssuerUri actualizado.</span><span class="sxs-lookup"><span data-stu-id="4484e-179">By using the PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view the updated IssuerUri.</span></span>  <span data-ttu-id="4484e-180">La captura de pantalla siguiente muestra que la configuración de la federación se actualizó en el dominio original http://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="4484e-180">The screenshot below shows the federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="4484e-182">Y el elemento IssuerUri de nuestro dominio nuevo se ha establecido en https://bmfabrikam.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="4484e-182">And the IssuerUri on our new domain has been set to https://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="4484e-184">Compatibilidad con subdominios</span><span class="sxs-lookup"><span data-stu-id="4484e-184">Support for Sub-domains</span></span>
<span data-ttu-id="4484e-185">Cuando se agrega un subdominio, debido a la manera en que Azure AD controla los dominios, heredará la configuración del elemento primario.</span><span class="sxs-lookup"><span data-stu-id="4484e-185">When you add a sub-domain, because of the way Azure AD handled domains, it will inherit the settings of the parent.</span></span>  <span data-ttu-id="4484e-186">Esto significa que el elemento IssuerUri debe coincidir con los elementos primarios.</span><span class="sxs-lookup"><span data-stu-id="4484e-186">This means that the IssuerUri needs to match the parents.</span></span>

<span data-ttu-id="4484e-187">Supongamos que tengo bmcontoso.com y que agrego corp.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="4484e-187">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.</span></span>  <span data-ttu-id="4484e-188">Esto significa que el elemento IssuerUri de un usuario de corp.bmcontoso.com deberá ser **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="4484e-188">This means that the IssuerUri for a user from corp.bmcontoso.com will need to be **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="4484e-189">A pesar de la regla estándar implementada anteriormente para Azure AD, se generará un token con un emisor como **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="4484e-189">However the standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="4484e-190">que no coincidirá con el valor obligatorio del dominio y se producirá un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="4484e-190">which will not match the domain's required value and authentication will fail.</span></span>

### <a name="how-to-enable-support-for-sub-domains"></a><span data-ttu-id="4484e-191">Habilitación de la compatibilidad con subdominios</span><span class="sxs-lookup"><span data-stu-id="4484e-191">How To enable support for sub-domains</span></span>
<span data-ttu-id="4484e-192">Para solucionar este problema, es necesario actualizar la confianza de usuario de confianza de AD FS para Microsoft Online.</span><span class="sxs-lookup"><span data-stu-id="4484e-192">In order to work around this the AD FS relying party trust for Microsoft Online needs to be updated.</span></span>  <span data-ttu-id="4484e-193">Para ello, debe configurar una regla de notificaciones personalizada para eliminar cualquier subdominio del sufijo UPN del usuario al construir el valor de emisor personalizado.</span><span class="sxs-lookup"><span data-stu-id="4484e-193">To do this, you must configure a custom claim rule so that it strips off any sub-domains from the user’s UPN suffix when constructing the custom Issuer value.</span></span> 

<span data-ttu-id="4484e-194">La siguiente notificación hará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="4484e-194">The following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="4484e-195">El último número de la expresión regular establece la cantidad de dominios primarios que hay en el dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="4484e-195">The last number in the regular expression set the how many parent domains there is in your root domain.</span></span> <span data-ttu-id="4484e-196">En este caso tenemos bmcontoso.com, por lo que se requieren dos dominios principales.</span><span class="sxs-lookup"><span data-stu-id="4484e-196">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="4484e-197">Si tuviéramos que mantener tres dominios principales (es decir, corp.bmcontoso.com), el número habría sido tres.</span><span class="sxs-lookup"><span data-stu-id="4484e-197">If three parent domains were to be kept (i.e.: corp.bmcontoso.com), then the number would have been three.</span></span> <span data-ttu-id="4484e-198">Es posible indicar un intervalo; en ese caso, la coincidencia se realizará siempre con el número máximo de dominios.</span><span class="sxs-lookup"><span data-stu-id="4484e-198">Eventualy a range can be indicated, the match will always be made to match the maximum of domains.</span></span> <span data-ttu-id="4484e-199">"{2,3}" coincidirá con dos o tres dominios (esto es, bmfabrikam.com y corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="4484e-199">"{2,3}" will match two to three domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="4484e-200">Siga los pasos indicados a continuación para agregar una notificación personalizada para admitir subdominios.</span><span class="sxs-lookup"><span data-stu-id="4484e-200">Use the following steps to add a custom claim to support sub-domains.</span></span>

1. <span data-ttu-id="4484e-201">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="4484e-201">Open AD FS Management</span></span>
2. <span data-ttu-id="4484e-202">Haga clic con el botón derecho en la confianza de usuario de confianza de Microsoft Online y elija Editar reglas de notificación.</span><span class="sxs-lookup"><span data-stu-id="4484e-202">Right click the Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="4484e-203">Seleccione la tercera regla de notificación y reemplace ![Editar notificación](./media/active-directory-multiple-domains/sub1.png).</span><span class="sxs-lookup"><span data-stu-id="4484e-203">Select the third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="4484e-204">Reemplace la notificación actual:</span><span class="sxs-lookup"><span data-stu-id="4484e-204">Replace the current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Reemplazar notificación](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="4484e-206">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="4484e-206">Click Ok.</span></span>  <span data-ttu-id="4484e-207">Haga clic en Aplicar.</span><span class="sxs-lookup"><span data-stu-id="4484e-207">Click Apply.</span></span>  <span data-ttu-id="4484e-208">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="4484e-208">Click Ok.</span></span>  <span data-ttu-id="4484e-209">Cierre Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="4484e-209">Close AD FS Management.</span></span>

