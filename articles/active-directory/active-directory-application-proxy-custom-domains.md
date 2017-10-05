---
title: "Dominios personalizados del proxy de aplicación de Azure AD | Microsoft Docs"
description: "Administre los dominios personalizados del proxy de aplicación de Azure AD para que la dirección URL de la aplicación sea la mismo independientemente de dónde accedan los usuarios."
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
ms.openlocfilehash: 1dde300780c8d1f7ea9eee4c92de06bcf70a1f12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a><span data-ttu-id="4d952-103">Uso de dominios personalizados en el proxy de la aplicación de Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d952-103">Working with custom domains in Azure AD Application Proxy</span></span>

<span data-ttu-id="4d952-104">Al publicar una aplicación a través del proxy de la aplicación de Azure Active Directory, se crea una dirección URL externa a la que los usuarios se desplazan cuando trabajan de forma remota.</span><span class="sxs-lookup"><span data-stu-id="4d952-104">When you publish an application through Azure Active Directory Application Proxy, you create an external URL for your users to go to when they're working remotely.</span></span> <span data-ttu-id="4d952-105">Esta dirección URL obtiene el dominio predeterminado *yourtenant-msappproxy.net*.</span><span class="sxs-lookup"><span data-stu-id="4d952-105">This URL gets the default domain *yourtenant.msappproxy.net*.</span></span> <span data-ttu-id="4d952-106">Por ejemplo, si publica una aplicación denominada Expenses y el inquilino se llama Contoso, la dirección URL externa sería https://expenses-contoso.msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="4d952-106">For example, if you published an app named Expenses and your tenant is named Contoso, then the external URL would be https://expenses-contoso.msappproxy.net.</span></span> <span data-ttu-id="4d952-107">Si quiere usar su propio nombre de dominio, configure un dominio personalizado para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d952-107">If you want to use your own domain name, configure a custom domain for your application.</span></span> 

<span data-ttu-id="4d952-108">Se recomienda que configure dominios personalizados para las aplicaciones siempre que sea posible.</span><span class="sxs-lookup"><span data-stu-id="4d952-108">We recommend that you set up custom domains for your applications whenever possible.</span></span> <span data-ttu-id="4d952-109">Algunas de las ventajas de los dominios personalizados son:</span><span class="sxs-lookup"><span data-stu-id="4d952-109">Some of the benefits of custom domains include:</span></span>

- <span data-ttu-id="4d952-110">Los usuarios pueden acceder a la aplicación con la misma dirección URL, ya estén trabajando dentro o fuera de la red.</span><span class="sxs-lookup"><span data-stu-id="4d952-110">Your users can get to the application with the same URL, whether they are working inside or outside of your network.</span></span>
- <span data-ttu-id="4d952-111">Si todas las aplicaciones tienen las mismas direcciones URL internas y externas, los vínculos de una aplicación que señalan a otra seguirán funcionando incluso fuera de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="4d952-111">If all of your applications have the same internal and external URLs, then links in one application that point to another continue to work even outside the corporate network.</span></span> 
- <span data-ttu-id="4d952-112">Puede controlar la personalización de marca y crear las direcciones URL que quiera.</span><span class="sxs-lookup"><span data-stu-id="4d952-112">You control your branding, and create the URLs you want.</span></span> 


## <a name="configure-a-custom-domain"></a><span data-ttu-id="4d952-113">Configuración de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="4d952-113">Configure a custom domain</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4d952-114">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="4d952-114">Prerequisites</span></span>

<span data-ttu-id="4d952-115">Antes de configurar un dominio personalizado, asegúrese de que tener preparados los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="4d952-115">Before you configure a custom domain, make sure that you have the following requirements prepared:</span></span> 
- <span data-ttu-id="4d952-116">Un [dominio comprobado agregado a Azure Active Directory](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d952-116">A [verified domain added to Azure Active Directory](active-directory-domains-add-azure-portal.md).</span></span>
- <span data-ttu-id="4d952-117">Un certificado personalizado para el dominio, en forma de un archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="4d952-117">A custom certificate for the domain, in the form of a PFX file.</span></span> 
- <span data-ttu-id="4d952-118">Una aplicación local [publicada a través del proxy de la aplicación](application-proxy-publish-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d952-118">An on-premises app [published through Application Proxy](application-proxy-publish-azure-portal.md).</span></span>

### <a name="configure-your-custom-domain"></a><span data-ttu-id="4d952-119">Configuración de un dominio personalizado</span><span class="sxs-lookup"><span data-stu-id="4d952-119">Configure your custom domain</span></span>

<span data-ttu-id="4d952-120">Cuando tenga listos estos tres requisitos, siga estos pasos para configurar el dominio personalizado:</span><span class="sxs-lookup"><span data-stu-id="4d952-120">When you have those three requirements ready, follow these steps to set up your custom domain:</span></span>

1. <span data-ttu-id="4d952-121">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4d952-121">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4d952-122">Vaya a **Azure Active Directory** > **Aplicaciones empresariales** > **Todas las aplicaciones** y elija la aplicación que quiere administrar.</span><span class="sxs-lookup"><span data-stu-id="4d952-122">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications** and choose the app you want to manage.</span></span>
3. <span data-ttu-id="4d952-123">Seleccione **Proxy de la aplicación**.</span><span class="sxs-lookup"><span data-stu-id="4d952-123">Select **Application Proxy**.</span></span> 
4. <span data-ttu-id="4d952-124">En el campo de dirección URL externa, use la lista desplegable para seleccionar el dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4d952-124">In the External URL field, use the dropdown list to select your custom domain.</span></span> <span data-ttu-id="4d952-125">Si no ve su dominio en la lista, es que no se ha comprobado todavía.</span><span class="sxs-lookup"><span data-stu-id="4d952-125">If you don't see your domain in the list, then it hasn't been verified yet.</span></span> 
5. <span data-ttu-id="4d952-126">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="4d952-126">Select **Save**</span></span>
5. <span data-ttu-id="4d952-127">El campo **Certificado** que se deshabilitó se habilita.</span><span class="sxs-lookup"><span data-stu-id="4d952-127">The **Certificate** field that was disabled becomes enabled.</span></span> <span data-ttu-id="4d952-128">Seleccione este campo.</span><span class="sxs-lookup"><span data-stu-id="4d952-128">Select this field.</span></span> 

   ![Haga clic para cargar un certificado.](./media/active-directory-application-proxy-custom-domains/certificate.png)

   <span data-ttu-id="4d952-130">Si ya ha cargado un certificado para este dominio, el campo Certificado mostrará la información de este.</span><span class="sxs-lookup"><span data-stu-id="4d952-130">If you already uploaded a certificate for this domain, the Certificate field displays the certificate information.</span></span> 

6. <span data-ttu-id="4d952-131">Cargue el certificados PFX y escriba su contraseña.</span><span class="sxs-lookup"><span data-stu-id="4d952-131">Upload the PFX certificate and enter the password for the certificate.</span></span> 
7. <span data-ttu-id="4d952-132">Haga clic en **Guardar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="4d952-132">Select **Save** to save your changes.</span></span> 
8. <span data-ttu-id="4d952-133">Agregue un [registro DNS](../dns/dns-operations-recordsets-portal.md) que redirija la nueva dirección URL externa al dominio msappproxy.net.</span><span class="sxs-lookup"><span data-stu-id="4d952-133">Add a [DNS record](../dns/dns-operations-recordsets-portal.md) that redirects the new external URL to the msappproxy.net domain.</span></span> 

>[!TIP] 
><span data-ttu-id="4d952-134">Solo es necesario cargar un certificado por dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="4d952-134">You only need to upload one certificate per custom domain.</span></span> <span data-ttu-id="4d952-135">Después de cargar un certificado, puede elegir el dominio personalizado cuando publique una nueva aplicación y no tiene que configurar nada más excepto el registro DNS.</span><span class="sxs-lookup"><span data-stu-id="4d952-135">Once you upload a certificate, you can choose the custom domain when you publish a new app and not have to do additional configuration except for the DNS record.</span></span> 

## <a name="manage-certificates"></a><span data-ttu-id="4d952-136">Administración de certificados</span><span class="sxs-lookup"><span data-stu-id="4d952-136">Manage certificates</span></span>

### <a name="certificate-format"></a><span data-ttu-id="4d952-137">Formato del certificado</span><span class="sxs-lookup"><span data-stu-id="4d952-137">Certificate format</span></span>
<span data-ttu-id="4d952-138">No hay ninguna restricción sobre los métodos de firma del certificado.</span><span class="sxs-lookup"><span data-stu-id="4d952-138">There is no restriction on the certificate signature methods.</span></span> <span data-ttu-id="4d952-139">Se admiten todos los tipos de certificado habituales como, por ejemplo, la criptografía de curva elíptica (ECC) y el nombre alternativo del firmante (SAN).</span><span class="sxs-lookup"><span data-stu-id="4d952-139">Elliptic Curve Cryptography (ECC), Subject Alternative Name (SAN), and other common certificate types are all supported.</span></span> 

<span data-ttu-id="4d952-140">Puede usar un certificado comodín siempre y cuando este coincida con la dirección URL externa deseada.</span><span class="sxs-lookup"><span data-stu-id="4d952-140">You can use a wildcard certificate as long as the wildcard matches the desired external URL.</span></span> 

<span data-ttu-id="4d952-141">También puede usar certificados autofirmados.</span><span class="sxs-lookup"><span data-stu-id="4d952-141">You can use self-signed certificates, as well.</span></span> <span data-ttu-id="4d952-142">Si usa una entidad de certificación privada, el CDP (punto de distribución de lista de revocación de certificados) del certificado debe ser público.</span><span class="sxs-lookup"><span data-stu-id="4d952-142">If you’re using a private certificate authority, the CDP (certificate revocation point distribution point) for the certificate should be public.</span></span>

### <a name="changing-the-domain"></a><span data-ttu-id="4d952-143">Cambio del dominio</span><span class="sxs-lookup"><span data-stu-id="4d952-143">Changing the domain</span></span>
<span data-ttu-id="4d952-144">Todos los dominios comprobados aparecen en la lista desplegable de direcciones URL externas de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d952-144">All verified domains appear in the External URL dropdown list for your application.</span></span> <span data-ttu-id="4d952-145">Para cambiar el dominio, actualice ese campo de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d952-145">To change the domain, just update that field for the application.</span></span> <span data-ttu-id="4d952-146">Si el dominio que desea no está en la lista, [agréguelo como dominio comprobado](active-directory-domains-add-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4d952-146">If the domain you want isn't in the list, [add it as a verified domain](active-directory-domains-add-azure-portal.md).</span></span> <span data-ttu-id="4d952-147">Si selecciona un dominio que no tiene aún un certificado asociado, siga los pasos del 5 al 7 para agregarlo.</span><span class="sxs-lookup"><span data-stu-id="4d952-147">If you select a domain that doesn't have an associated certificate yet, follow steps 5-7 to add the certificate.</span></span> <span data-ttu-id="4d952-148">A continuación, asegúrese de actualizar el registro DNS para redirigirlo desde la nueva dirección URL externa.</span><span class="sxs-lookup"><span data-stu-id="4d952-148">Then, make sure you update the DNS record to redirect from the new external URL.</span></span> 

### <a name="certificate-management"></a><span data-ttu-id="4d952-149">Administración de certificados</span><span class="sxs-lookup"><span data-stu-id="4d952-149">Certificate management</span></span>
<span data-ttu-id="4d952-150">Puede usar el mismo certificado para varias aplicaciones a menos que las aplicaciones compartan un host externo.</span><span class="sxs-lookup"><span data-stu-id="4d952-150">You can use the same certificate for multiple applications unless the applications share an external host.</span></span> 

<span data-ttu-id="4d952-151">Cuando un certificado expira, recibirá una advertencia que le indica que cargue otro certificado mediante el portal.</span><span class="sxs-lookup"><span data-stu-id="4d952-151">You get a warning when a certificate expires, telling you to upload another certificate through the portal.</span></span> <span data-ttu-id="4d952-152">Si se revoca el certificado, los usuarios pueden ver una advertencia de seguridad al acceder a la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4d952-152">If the certificate is revoked, your users may see a security warning when accessing the application.</span></span> <span data-ttu-id="4d952-153">No se realizan comprobaciones de revocación de los certificados.</span><span class="sxs-lookup"><span data-stu-id="4d952-153">We don’t perform revocation checks for certificates.</span></span>  <span data-ttu-id="4d952-154">Para actualizar el certificado en una aplicación dada, vaya a la aplicación y siga los pasos del 5 al 7 para configurar dominios personalizados en aplicaciones publicadas y cargar un nuevo certificado.</span><span class="sxs-lookup"><span data-stu-id="4d952-154">To update the certificate for a given application, navigate to the application and follow steps 5-7 for configuring custom domains on published applications to upload a new certificate.</span></span> <span data-ttu-id="4d952-155">Si no se usa un certificado antiguo con otras aplicaciones, se elimina automáticamente.</span><span class="sxs-lookup"><span data-stu-id="4d952-155">If the old certificate is not being used by other applications, it is deleted automatically.</span></span> 

<span data-ttu-id="4d952-156">Actualmente, toda la administración de certificados es a través de páginas de aplicación individuales, por lo que deberá administrar los certificados en el contexto de las aplicaciones pertinentes.</span><span class="sxs-lookup"><span data-stu-id="4d952-156">Currently all certificate management is through individual application pages so you need to manage certificates in the context of the relevant applications.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4d952-157">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4d952-157">Next steps</span></span>
* <span data-ttu-id="4d952-158">[Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md) en las aplicaciones publicadas con la autenticación de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4d952-158">[Enable single sign-on](active-directory-application-proxy-sso-using-kcd.md) to your published apps with Azure AD authentication.</span></span>
* <span data-ttu-id="4d952-159">[Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md) a las aplicaciones publicadas.</span><span class="sxs-lookup"><span data-stu-id="4d952-159">[Enable conditional access](active-directory-application-proxy-conditional-access.md) to your published apps.</span></span>
* [<span data-ttu-id="4d952-160">Incorporación de su nombre de dominio personalizado a Azure AD</span><span class="sxs-lookup"><span data-stu-id="4d952-160">Add your custom domain name to Azure AD</span></span>](active-directory-domains-add-azure-portal.md)


