---
title: "dominios de aaaCustom en el Proxy de aplicación de Azure AD | Documentos de Microsoft"
description: "Administrar dominios personalizados en el Proxy de aplicación de Azure AD para esa dirección URL de hello para la aplicación hello Hola igual independientemente de donde los usuarios obtener acceso a él."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="ee5fd-103">Uso de dominios personalizados en el proxy de la aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="ee5fd-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="ee5fd-104">Al publicar una aplicación a través de Proxy de aplicación de Azure Active Directory, cree una dirección URL externa para su toowhen de toogo de usuarios está trabajando de forma remota.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users toogo toowhen they're working remotely.</span></span> <span data-ttu-id="ee5fd-105">Esta dirección URL Obtiene el dominio predeterminado de hello *yourtenant.msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-105">This URL gets hello default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="ee5fd-106">Por ejemplo, si opta por publicar una aplicación denominada gastos y el inquilino se denomina Contoso, a continuación, dirección URL externa de hello sería https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-106">For example, if you published an app named Expenses and your tenant is named Contoso, then hello external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="ee5fd-107">Si desea toouse su propio nombre de dominio, configure un dominio personalizado para su aplicación.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-107">If you want toouse your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="ee5fd-108">Se recomienda que configure dominios personalizados para las aplicaciones siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="ee5fd-109">Algunas de las ventajas de Hola de dominios personalizados son:</span><span class="sxs-lookup"><span data-stu-id="ee5fd-109">Some of hello benefits of custom domains include:</span></span>

- <span data-ttu-id="ee5fd-110">Los usuarios pueden acceder toohello aplicación Hola la misma dirección URL, si están trabajando dentro o fuera de la red.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-110">Your users can get toohello application with hello same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="ee5fd-111">Si todas las aplicaciones se hello mismas direcciones URL internas y externas, vínculos en una aplicación que señalan tooanother continuar toowork incluso fuera de la red corporativa de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-111">If all of your applications have hello same internal and external URLs, then links in one application that point tooanother continue toowork even outside hello corporate network.</span></span> 
- <span data-ttu-id="ee5fd-112">Para controlar su marca y crear direcciones URL de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-112">You control your branding, and create hello URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="ee5fd-113">Configuración de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="ee5fd-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ee5fd-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="ee5fd-114">Prerequisites</span></span>

<span data-ttu-id="ee5fd-115">Antes de configurar un dominio personalizado, asegúrese de que dispone de hello según los requisitos preparados:</span><span class="sxs-lookup"><span data-stu-id="ee5fd-115">Before you configure a custom domain, make sure that you have hello following requirements prepared:</span></span> 
- <span data-ttu-id="ee5fd-116">A [tooAzure Active Directory de agregado de dominio comprobado](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee5fd-116">A [verified domain added tooAzure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="ee5fd-117">Un certificado personalizado para dominio hello, en forma de Hola de un archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-117">A custom certificate for hello domain, in hello form of a PFX file.</span></span> 
- <span data-ttu-id="ee5fd-118">Una aplicación local [publicada a través del proxy de la aplicación](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee5fd-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="ee5fd-119">Configuración de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="ee5fd-119">Configure your custom domain</span></span>

<span data-ttu-id="ee5fd-120">Cuando haya que esos tres requisitos listo, siga estas tooset pasos su dominio personalizado:</span><span class="sxs-lookup"><span data-stu-id="ee5fd-120">When you have those three requirements ready, follow these steps tooset up your custom domain:</span></span>

1. <span data-ttu-id="ee5fd-121">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee5fd-121">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ee5fd-122">Navegue demasiado**Azure Active Directory** > **aplicaciones empresariales** > **todas las aplicaciones** y elija aplicación hello desea toomanage.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-122">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications** and choose hello app you want toomanage.</span></span>
3. <span data-ttu-id="ee5fd-123">Seleccione **Proxy de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="ee5fd-124">En el campo de dirección URL externa de hello, utilice tooselect de lista desplegable de hello su dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-124">In hello External URL field, use hello dropdown list tooselect your custom domain.</span></span> <span data-ttu-id="ee5fd-125">Si no ve su dominio en la lista de hello, a continuación, que no haya comprobado todavía.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-125">If you don't see your domain in hello list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="ee5fd-126">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-126">Select **Save**</span></span>
5. <span data-ttu-id="ee5fd-127">Hola **certificado** se habilita el campo que se ha deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-127">hello **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="ee5fd-128">Seleccione este campo.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-128">Select this field.</span></span> 

   ![Haga clic en tooupload un certificado](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="ee5fd-130">Si ha cargado un certificado para este dominio, el campo de certificado hello muestra información del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-130">If you already uploaded a certificate for this domain, hello Certificate field displays hello certificate information.</span></span> 

6. <span data-ttu-id="ee5fd-131">Cargar certificados PFX de Hola y escriba la contraseña de hello para el certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-131">Upload hello PFX certificate and enter hello password for hello certificate.</span></span> 
7. <span data-ttu-id="ee5fd-132">Seleccione **guardar** toosave los cambios.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-132">Select **Save** toosave your changes.</span></span> 
8. <span data-ttu-id="ee5fd-133">Agregar un [registro DNS](../dns/dns-operations-recordsets-portal.md) que redirige Hola nuevo dominio externo de msappproxy.net de toohello de dirección URL.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects hello new external URL toohello msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="ee5fd-134">Solo necesita un certificado de tooupload por dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-134">You only need tooupload one certificate per custom domain.</span></span> <span data-ttu-id="ee5fd-135">Una vez que cargue un certificado, puede elegir el dominio personalizado de hello al publicar una aplicación nueva y no tiene una configuración adicional toodo excepto para el registro DNS de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-135">Once you upload a certificate, you can choose hello custom domain when you publish a new app and not have toodo additional configuration except for hello DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="ee5fd-136">Administración de certificados</span><span class="sxs-lookup"><span data-stu-id="ee5fd-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="ee5fd-137">Formato del certificado</span><span class="sxs-lookup"><span data-stu-id="ee5fd-137">Certificate format</span></span>
<span data-ttu-id="ee5fd-138">No hay ninguna restricción sobre métodos de firma de certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-138">There is no restriction on hello certificate signature methods.</span></span> <span data-ttu-id="ee5fd-139">Se admiten todos los tipos de certificado habituales como, por ejemplo, la criptografía de curva elíptica (ECC) y el nombre alternativo del firmante (SAN).</span><span class="sxs-lookup"><span data-stu-id="ee5fd-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="ee5fd-140">Puede usar un certificado comodín como comodín Hola coincide con la dirección URL externa de hello deseado.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-140">You can use a wildcard certificate as long as hello wildcard matches hello desired external URL.</span></span> 

<span data-ttu-id="ee5fd-141">También puede usar certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="ee5fd-142">Si está utilizando una entidad de certificación privada, hello CDP (punto de distribución de punto de revocación de certificados) para el certificado de hello debe ser público.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-142">If you’re using a private certificate authority, hello CDP (certificate revocation point distribution point) for hello certificate should be public.</span></span>

### <a name="changing-hello-domain"></a><span data-ttu-id="ee5fd-143">Cambiar dominio Hola</span><span class="sxs-lookup"><span data-stu-id="ee5fd-143">Changing hello domain</span></span>
<span data-ttu-id="ee5fd-144">Todos los dominios comprobados aparecen en la lista de desplegable de dirección URL externa de hello para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-144">All verified domains appear in hello External URL dropdown list for your application.</span></span> <span data-ttu-id="ee5fd-145">dominio de hello toochange, simplemente actualizar este campo para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-145">toochange hello domain, just update that field for hello application.</span></span> <span data-ttu-id="ee5fd-146">Si dominio Hola desea no está en la lista de hello, [agregarlo como un dominio comprobado](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ee5fd-146">If hello domain you want isn't in hello list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="ee5fd-147">Si selecciona un dominio que aún no tiene un certificado asociado, siga el certificado de hello tooadd pasos 5 a 7.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 tooadd hello certificate.</span></span> <span data-ttu-id="ee5fd-148">A continuación, asegúrese de que actualizar tooredirect de registro de DNS de Hola de dirección URL externa nueva Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-148">Then, make sure you update hello DNS record tooredirect from hello new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="ee5fd-149">Administración de certificados</span><span class="sxs-lookup"><span data-stu-id="ee5fd-149">Certificate management</span></span>
<span data-ttu-id="ee5fd-150">Puede usar el mismo certificado para varias aplicaciones a menos que las aplicaciones de hello compartir un host externo de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-150">You can use hello same certificate for multiple applications unless hello applications share an external host.</span></span> 

<span data-ttu-id="ee5fd-151">Obtendrá una advertencia cuando un certificado expira, indicando tooupload otro certificado a través del portal de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-151">You get a warning when a certificate expires, telling you tooupload another certificate through hello portal.</span></span> <span data-ttu-id="ee5fd-152">Si se revoca el certificado de hello, los usuarios pueden ver una advertencia de seguridad al obtener acceso a la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-152">If hello certificate is revoked, your users may see a security warning when accessing hello application.</span></span> <span data-ttu-id="ee5fd-153">No se realizan comprobaciones de revocación de los certificados.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="ee5fd-154">certificado de Hola de tooupdate para una determinada aplicación, navegar por la aplicación toohello y siga los pasos 5 a 7 para configurar dominios personalizados en tooupload un nuevo certificado de las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-154">tooupdate hello certificate for a given application, navigate toohello application and follow steps 5-7 for configuring custom domains on published applications tooupload a new certificate.</span></span> <span data-ttu-id="ee5fd-155">Si no se utiliza los certificados antiguos de Hola por otras aplicaciones, se elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-155">If hello old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="ee5fd-156">Actualmente toda la administración de certificados es a través de páginas de aplicación individuales por lo que necesita certificados toomanage en contexto de Hola de aplicaciones relevantes de Hola.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-156">Currently all certificate management is through individual application pages so you need toomanage certificates in hello context of hello relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ee5fd-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ee5fd-157">Next steps</span></span>
* <span data-ttu-id="ee5fd-158">[Habilitar inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md) tooyour publicar aplicaciones con autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) tooyour published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="ee5fd-159">[Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md) tooyour las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="ee5fd-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) tooyour published apps.</span></span>
* [<span data-ttu-id="ee5fd-160">Agregue su tooAzure de nombre de dominio personalizado AD</span><span class="sxs-lookup"><span data-stu-id="ee5fd-160">Add your custom domain name tooAzure AD</span></span>](active-directory-domains-add-azure-portal.md)


