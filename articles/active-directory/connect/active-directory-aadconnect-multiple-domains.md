---
title: aaaAzure AD conectar varios dominios
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
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="942c4-103">Compatibilidad con varios dominios para la federación con Azure AD</span><span class="sxs-lookup"><span data-stu-id="942c4-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="942c4-104">Hello siguiente documentación proporciona orientación sobre cómo toouse varios dominios de nivel superior y subdominios al federarse con dominios de Office 365 o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="942c4-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="942c4-105">Compatibilidad con varios dominios de nivel superior</span><span class="sxs-lookup"><span data-stu-id="942c4-105">Multiple top-level domain support</span></span>
<span data-ttu-id="942c4-106">La federación de varios dominios de nivel superior con Azure AD requiere una configuración adicional que no es necesaria al federarse con un dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="942c4-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="942c4-107">Cuando un dominio está federado con Azure AD, se establecen varias propiedades en el dominio de hello en Azure.</span><span class="sxs-lookup"><span data-stu-id="942c4-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="942c4-108">Una propiedad importante es IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="942c4-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="942c4-109">Se trata de un URI que se usa por Azure AD tooidentify dominio de Hola que Hola token está asociado.</span><span class="sxs-lookup"><span data-stu-id="942c4-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="942c4-110">Hola URI no es necesario tooresolve tooanything pero debe ser un URI válido.</span><span class="sxs-lookup"><span data-stu-id="942c4-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="942c4-111">De forma predeterminada, Azure AD establece toohello el valor de identificador de servicio de federación de hello en sus instalaciones en AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="942c4-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="942c4-112">identificador del servicio de federación Hello es un URI que identifica de forma única un servicio de federación.</span><span class="sxs-lookup"><span data-stu-id="942c4-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="942c4-113">servicio de federación de Hello es una instancia de AD FS que funcione como servicio de token de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c4-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="942c4-114">También puede ver IssuerUri mediante comandos de PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="942c4-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="942c4-116">El problema surge si queremos tooadd más de un dominio de nivel superior.</span><span class="sxs-lookup"><span data-stu-id="942c4-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="942c4-117">Por ejemplo, supongamos que ha configurado la federación entre Azure AD y el entorno local.</span><span class="sxs-lookup"><span data-stu-id="942c4-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="942c4-118">Para este documento uso bmcontoso.com.  Ahora he agregado un segundo dominio de nivel superior, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="942c4-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Dominios](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="942c4-120">Cuando intentamos tooconvert nuestro toobe de dominio bmfabrikam.com federado, se recibe un error.</span><span class="sxs-lookup"><span data-stu-id="942c4-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="942c4-121">es el motivo Hello, Azure AD tiene una restricción que no permite Hola Hola de toohave de propiedad IssuerUri mismo valor para más de un dominio.</span><span class="sxs-lookup"><span data-stu-id="942c4-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Error de federación](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="942c4-123">Parámetro SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="942c4-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="942c4-124">tooworkaround esto, debemos tooadd un IssuerUri diferentes que puede realizarse mediante el uso de hello `-SupportMultipleDomain` parámetro.</span><span class="sxs-lookup"><span data-stu-id="942c4-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="942c4-125">Este parámetro se utiliza con hello siguientes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="942c4-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="942c4-126">Este parámetro hace que Azure AD configurar hello IssuerUri para que se basa en el nombre de hello del dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c4-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="942c4-127">Este será único en los directorios de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="942c4-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="942c4-128">Usar el parámetro hello permite toocomplete de comandos de PowerShell de hello correctamente.</span><span class="sxs-lookup"><span data-stu-id="942c4-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Error de federación](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="942c4-130">Examinando configuración Hola de nuestro nuevo dominio bmfabrikam.com puede ver el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="942c4-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Error de federación](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="942c4-132">Tenga en cuenta que `-SupportMultipleDomain` no cambia Hola otros extremos que son todavía configuran el servicio de federación de toopoint tooour en adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="942c4-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="942c4-133">Otra cosa que `-SupportMultipleDomain` does es que garantiza que sistema de hello AD FS incluye valor del emisor correcto hello en tokens emitidos para Azure AD.</span><span class="sxs-lookup"><span data-stu-id="942c4-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="942c4-134">Para ello, tomar parte de dominio de Hola de hello usuarios UPN y si se establece como dominio de Hola Hola IssuerUri, es decir, https://{upn sufijo} / adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="942c4-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="942c4-135">Por lo tanto durante la autenticación tooAzure AD u Office 365, hello IssuerUri elemento token del usuario de hello es dominio de hello toolocate usado en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="942c4-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="942c4-136">Si no se encuentra una coincidencia se producirá un error de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c4-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="942c4-137">Por ejemplo, si un usuario del UPN es bsimon@bmcontoso.com, elemento de IssuerUri hello en problemas de AD FS de token de Hola se establecerá toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="942c4-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="942c4-138">Esto coincidirá con la configuración de Azure AD de Hola y autenticación se realizará correctamente.</span><span class="sxs-lookup"><span data-stu-id="942c4-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="942c4-139">Hola te mostramos regla de notificación personalizada de Hola que implementa esta lógica:</span><span class="sxs-lookup"><span data-stu-id="942c4-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="942c4-140">En orden toouse Hola - SupportMultipleDomain cambiar al intentar tooadd nueva o convertir ya dominios agregados, deberá toohave la instalación de la relación de confianza federada toosupport ellos originalmente.</span><span class="sxs-lookup"><span data-stu-id="942c4-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="942c4-141">¿Cómo tooupdate Hola de confianza entre AD FS y Azure</span><span class="sxs-lookup"><span data-stu-id="942c4-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="942c4-142">Si no se han configurado Hola federado confianza entre AD FS y la instancia de Azure AD, puede que necesite toore-crear esta relación de confianza.</span><span class="sxs-lookup"><span data-stu-id="942c4-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="942c4-143">Esto es porque, cuando es originalmente el programa de instalación sin hello `-SupportMultipleDomain` parámetro, hello IssuerUri se establece con el valor predeterminado de Hola.</span><span class="sxs-lookup"><span data-stu-id="942c4-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="942c4-144">Hola captura de pantalla siguiente se puede ver hello IssuerUri se establece toohttps://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="942c4-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="942c4-145">Ahora, si se ha agregado correctamente un nuevo dominio en el portal de hello Azure AD y, a continuación, intente tooconvert mediante `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtenemos Hola siguiente error.</span><span class="sxs-lookup"><span data-stu-id="942c4-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="942c4-147">Si intentas hello tooadd `-SupportMultipleDomain` conmutador recibimos Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="942c4-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="942c4-149">Simplemente intentar toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` en hello dominio original también producirá un error.</span><span class="sxs-lookup"><span data-stu-id="942c4-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Error de federación](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="942c4-151">Use estos pasos hello tooadd un dominio de nivel superior adicional.</span><span class="sxs-lookup"><span data-stu-id="942c4-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="942c4-152">Si ya se ha agregado un dominio y no usó hello `-SupportMultipleDomain` parámetro Inicio con pasos de Hola para quitar y actualizar su dominio original.</span><span class="sxs-lookup"><span data-stu-id="942c4-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="942c4-153">Si no ha agregado un dominio de nivel superior se puede iniciar con pasos de Hola para agregar un dominio con PowerShell de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="942c4-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="942c4-154">Usar hello después de confianza de Microsoft Online de pasos tooremove hello y actualice su dominio original.</span><span class="sxs-lookup"><span data-stu-id="942c4-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="942c4-155">En el servidor de federación de AD FS, abra **Administración de AD FS.**</span><span class="sxs-lookup"><span data-stu-id="942c4-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="942c4-156">Hola izquierda, expanda **relaciones de confianza** y **usuario autenticado**</span><span class="sxs-lookup"><span data-stu-id="942c4-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="942c4-157">En hello derecha, elimine hello **plataforma de identidad de Microsoft Office 365** entrada.</span><span class="sxs-lookup"><span data-stu-id="942c4-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="942c4-158">![Quitar Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="942c4-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="942c4-159">En un equipo que tenga [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado en el que se ejecute el siguiente hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="942c4-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="942c4-160">Escriba Hola nombre de usuario y la contraseña de administrador global para dominio de Azure AD Hola con que federa</span><span class="sxs-lookup"><span data-stu-id="942c4-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="942c4-161">En PowerShell, escriba `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="942c4-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="942c4-162">En PowerShell, escriba `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="942c4-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="942c4-163">Esto es para dominio original Hola.</span><span class="sxs-lookup"><span data-stu-id="942c4-163">This is for hello original domain.</span></span>  <span data-ttu-id="942c4-164">Por lo que usar Hola anterior dominios sería:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="942c4-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="942c4-165">Usar hello siguiendo los pasos tooadd Hola nuevo dominio de nivel superior con PowerShell</span><span class="sxs-lookup"><span data-stu-id="942c4-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="942c4-166">En un equipo que tenga [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado en el que se ejecute el siguiente hello: `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="942c4-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="942c4-167">Escriba Hola nombre de usuario y la contraseña de administrador global para dominio de Azure AD Hola con que federa</span><span class="sxs-lookup"><span data-stu-id="942c4-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="942c4-168">En PowerShell, escriba `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="942c4-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="942c4-169">En PowerShell, escriba `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="942c4-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="942c4-170">Usar hello siguiendo los pasos tooadd Hola nuevo dominio de nivel superior mediante Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="942c4-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="942c4-171">Iniciar Azure Connect AD desde el escritorio de Hola o del menú Inicio</span><span class="sxs-lookup"><span data-stu-id="942c4-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="942c4-172">Elija "Agregar un dominio de Azure AD adicional" ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="942c4-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="942c4-173">Escriba sus credenciales de Azure AD y Active Directory.</span><span class="sxs-lookup"><span data-stu-id="942c4-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="942c4-174">Seleccione el dominio de segundo de hello desea tooconfigure para la federación.</span><span class="sxs-lookup"><span data-stu-id="942c4-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="942c4-175">![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="942c4-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="942c4-176">Haga clic en Instalar.</span><span class="sxs-lookup"><span data-stu-id="942c4-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="942c4-177">Comprobar el dominio de nivel superior nuevo Hola</span><span class="sxs-lookup"><span data-stu-id="942c4-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="942c4-178">Mediante el uso de comandos de PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`puede ver Hola actualizado IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="942c4-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="942c4-179">Hola de captura de pantalla siguiente muestra la configuración de la federación de Hola se han actualizado en nuestro http://bmcontoso.com/adfs/services/trust dominio original</span><span class="sxs-lookup"><span data-stu-id="942c4-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="942c4-181">Y hello IssuerUri en nuestro nuevo dominio se ha establecido toohttps://bmfabrikam.com/adfs/services/trust</span><span class="sxs-lookup"><span data-stu-id="942c4-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="942c4-183">Compatibilidad con subdominios</span><span class="sxs-lookup"><span data-stu-id="942c4-183">Support for Sub-domains</span></span>
<span data-ttu-id="942c4-184">Cuando se agrega un subdominio, debido a Hola forma Azure AD controla dominios, heredará la configuración de Hola de hello primaria.</span><span class="sxs-lookup"><span data-stu-id="942c4-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="942c4-185">Esto significa que hello IssuerUri tiene a elementos primarios de hello toomatch.</span><span class="sxs-lookup"><span data-stu-id="942c4-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="942c4-186">Supongamos que tengo bmcontoso.com y que agrego corp.bmcontoso.com.  Esto significa que hello IssuerUri para un usuario de corp.bmcontoso.com tendrá toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="942c4-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="942c4-187">Sin embargo, implementan reglas estándar de hello anteriormente para Azure AD, se generará un token con un emisor como **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="942c4-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="942c4-188">Esto no coincidirá con valor requerido del dominio de Hola y se producirá un error de autenticación.</span><span class="sxs-lookup"><span data-stu-id="942c4-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="942c4-189">¿Cómo se admiten tooenable de subdominios</span><span class="sxs-lookup"><span data-stu-id="942c4-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="942c4-190">En orden toowork alrededor de esta Hola ADFS relación de confianza de Microsoft Online debe toobe actualizado.</span><span class="sxs-lookup"><span data-stu-id="942c4-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="942c4-191">toodo esto, debe configurar una regla de notificación personalizada para que quita cualquier subdominios de sufijo UPN del usuario de hello al construir el valor de emisor de hello personalizado.</span><span class="sxs-lookup"><span data-stu-id="942c4-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="942c4-192">Hola después de la notificación hace esto:</span><span class="sxs-lookup"><span data-stu-id="942c4-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="942c4-193">último número de Hello en la expresión regular de hello establece Hola cuántos dominios primarios que hay en el dominio raíz.</span><span class="sxs-lookup"><span data-stu-id="942c4-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="942c4-194">En este caso tenemos bmcontoso.com, por lo que se requieren dos dominios principales.</span><span class="sxs-lookup"><span data-stu-id="942c4-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="942c4-195">Si los tres principales dominios estaban toobe mantiene (es decir,: corp.bmcontoso.com), a continuación, el número de hello habría sido tres.</span><span class="sxs-lookup"><span data-stu-id="942c4-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="942c4-196">Puede indicarse Eventualy un intervalo, coincidencia de hello siempre estará toomatch máximo de Hola de dominios.</span><span class="sxs-lookup"><span data-stu-id="942c4-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="942c4-197">"{2,3}" se corresponderá con dos dominios de toothree (es decir,: bmfabrikam.com y corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="942c4-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="942c4-198">Usar hello siguiendo los pasos tooadd un toosupport de notificación personalizada subdominios.</span><span class="sxs-lookup"><span data-stu-id="942c4-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="942c4-199">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="942c4-199">Open AD FS Management</span></span>
2. <span data-ttu-id="942c4-200">Haga clic en la confianza de Microsoft Online RP hello y elegir reglas de notificación de editar</span><span class="sxs-lookup"><span data-stu-id="942c4-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="942c4-201">Seleccione Hola tercera regla de notificación y reemplace ![Editar notificación](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="942c4-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="942c4-202">Reemplace la notificación actual hello:</span><span class="sxs-lookup"><span data-stu-id="942c4-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Reemplazar notificación](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="942c4-204">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="942c4-204">Click Ok.</span></span>  <span data-ttu-id="942c4-205">Haga clic en Aplicar.</span><span class="sxs-lookup"><span data-stu-id="942c4-205">Click Apply.</span></span>  <span data-ttu-id="942c4-206">Haga clic en Aceptar.</span><span class="sxs-lookup"><span data-stu-id="942c4-206">Click Ok.</span></span>  <span data-ttu-id="942c4-207">Cierre Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="942c4-207">Close AD FS Management.</span></span>

