---
title: recursos de nube aaaSecure con MFA de Azure y AD FS | Documentos de Microsoft
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con MFA de Azure y AD FS en la nube de Hola."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="0021d-103">Protección de recursos en la nube con Azure Multi-Factor Authentication y AD FS</span><span class="sxs-lookup"><span data-stu-id="0021d-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="0021d-104">Si su organización está federada con Azure Active Directory, utilice la autenticación multifactor Azure o recursos de toosecure de servicios de federación de Active Directory (AD FS) que se obtiene acceso a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0021d-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="0021d-105">Usar hello después de recursos de Active Directory de toosecure procedimientos con la autenticación multifactor Azure o los servicios de federación de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0021d-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="0021d-106">Protección de los recursos de Azure AD mediante AD FS</span><span class="sxs-lookup"><span data-stu-id="0021d-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="0021d-107">toosecure el recurso en la nube, configure una regla de notificaciones para que los servicios de federación de Active Directory emite hello multipleauthn notificación cuando un usuario realiza la verificación en dos pasos correctamente.</span><span class="sxs-lookup"><span data-stu-id="0021d-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="0021d-108">Esta notificación se pasa en tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="0021d-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="0021d-109">Siga este toowalk procedimiento a través de los pasos de hello:</span><span class="sxs-lookup"><span data-stu-id="0021d-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="0021d-110">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="0021d-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="0021d-111">Hola izquierda, seleccione **Veracidades**.</span><span class="sxs-lookup"><span data-stu-id="0021d-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0021d-112">Haga clic con el botón derecho en **Plataforma de identidad de Microsoft Office 365** y seleccione **Editar reglas de notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="0021d-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="0021d-114">En Reglas de transformación de emisión, haga clic en **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="0021d-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="0021d-116">En Hola transformar notificaciones Asistente para agregar reglas, seleccione **paso a través o filtrar una notificación entrante** de Hola lista desplegable y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0021d-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="0021d-118">Asigne un nombre a la regla.</span><span class="sxs-lookup"><span data-stu-id="0021d-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="0021d-119">Seleccione **referencias de métodos de autenticación** tipo de notificación de Hola entrantes.</span><span class="sxs-lookup"><span data-stu-id="0021d-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="0021d-120">Seleccione **Pasar a través todos los valores de notificaciones**.</span><span class="sxs-lookup"><span data-stu-id="0021d-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="0021d-121">![Asistente para agregar regla de notificación de transformación](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="0021d-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="0021d-122">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="0021d-122">Click **Finish**.</span></span> <span data-ttu-id="0021d-123">Cierre la consola de administración FS Hola AD.</span><span class="sxs-lookup"><span data-stu-id="0021d-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="0021d-124">Direcciones IP de confianza para usuarios federados</span><span class="sxs-lookup"><span data-stu-id="0021d-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="0021d-125">IP de confianza permiten a los administradores verificacion de paso de tooby para direcciones IP concretas o para usuarios federados que tienen las solicitudes que se originan dentro de su propia intranet.</span><span class="sxs-lookup"><span data-stu-id="0021d-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="0021d-126">Hello las secciones siguientes describen cómo tooconfigure la autenticación multifactor Azure confianza direcciones IP con los usuarios federados y verificacion de eludir cuando una solicitud se origina desde dentro de una intranet de los usuarios federados.</span><span class="sxs-lookup"><span data-stu-id="0021d-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="0021d-127">Esto se logra mediante la configuración de AD FS toouse un acceso directo o filtrar una plantilla de notificación entrante con hello el tipo de notificación dentro de la red corporativa.</span><span class="sxs-lookup"><span data-stu-id="0021d-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="0021d-128">En este ejemplo se utiliza Office 365 para las relaciones de confianza para usuario autenticado .</span><span class="sxs-lookup"><span data-stu-id="0021d-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="0021d-129">Configurar reglas de notificaciones de AD FS Hola</span><span class="sxs-lookup"><span data-stu-id="0021d-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="0021d-130">Hola primera cosa que necesitamos toodo es tooconfigure Hola AD FS notificaciones.</span><span class="sxs-lookup"><span data-stu-id="0021d-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="0021d-131">Creará dos reglas de notificaciones, uno para hello dentro de la red corporativa de notificación de tipo y otra adicional para mantener a nuestros usuarios que han iniciado.</span><span class="sxs-lookup"><span data-stu-id="0021d-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="0021d-132">Abra Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="0021d-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="0021d-133">Hola izquierda, seleccione **Veracidades**.</span><span class="sxs-lookup"><span data-stu-id="0021d-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="0021d-134">Haga clic con el botón derecho en **Plataforma de identidad de Microsoft Office 365** y seleccione **Editar reglas de notificaciones…**
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="0021d-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="0021d-135">En Reglas de transformación de emisión, haga clic en **Agregar regla**.
   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="0021d-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="0021d-136">En Hola transformar notificaciones Asistente para agregar reglas, seleccione **paso a través o filtrar una notificación entrante** de Hola lista desplegable y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0021d-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="0021d-137">![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="0021d-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="0021d-138">En nombre de regla de tooClaim siguiente de hello cuadro, asigne la regla un nombre.</span><span class="sxs-lookup"><span data-stu-id="0021d-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="0021d-139">Por ejemplo: InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="0021d-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="0021d-140">Desde la lista desplegable de hello, tooIncoming siguiente tipo de notificación, seleccione **dentro de la red corporativa**.</span><span class="sxs-lookup"><span data-stu-id="0021d-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="0021d-141">![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="0021d-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="0021d-142">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="0021d-142">Click **Finish**.</span></span>
9. <span data-ttu-id="0021d-143">En Reglas de transformación de emisión, haga clic en **Agregar regla**.</span><span class="sxs-lookup"><span data-stu-id="0021d-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="0021d-144">En Hola transformar notificaciones Asistente para agregar reglas, seleccione **enviar notificaciones mediante una regla personalizada** de Hola lista desplegable y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="0021d-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="0021d-145">En el cuadro de hello en nombre de la regla de notificación: escriba *mantener a los usuarios firmado en*.</span><span class="sxs-lookup"><span data-stu-id="0021d-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="0021d-146">En el cuadro de regla personalizada de hello, escriba:</span><span class="sxs-lookup"><span data-stu-id="0021d-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="0021d-148">Haga clic en **Finalizar**</span><span class="sxs-lookup"><span data-stu-id="0021d-148">Click **Finish**.</span></span>
14. <span data-ttu-id="0021d-149">Haga clic en **Apply**.</span><span class="sxs-lookup"><span data-stu-id="0021d-149">Click **Apply**.</span></span>
15. <span data-ttu-id="0021d-150">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0021d-150">Click **Ok**.</span></span>
16. <span data-ttu-id="0021d-151">Cierre Administración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="0021d-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="0021d-152">Configuración de las IP de confianza de Azure Multi-Factor Authentication con usuarios federados</span><span class="sxs-lookup"><span data-stu-id="0021d-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="0021d-153">Ahora que las notificaciones de hello están en su lugar, podemos configurar IP de confianza.</span><span class="sxs-lookup"><span data-stu-id="0021d-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="0021d-154">Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0021d-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0021d-155">Hola izquierda, haga clic en **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0021d-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="0021d-156">En el directorio, seleccione el directorio de Hola donde desea tooset una IP de confianza.</span><span class="sxs-lookup"><span data-stu-id="0021d-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="0021d-157">En hello directorio que ha seleccionado, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="0021d-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="0021d-158">En la sección de la autenticación multifactor de hello, haga clic en **administrar la configuración del servicio**.</span><span class="sxs-lookup"><span data-stu-id="0021d-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="0021d-159">En la página de configuración del servicio de hello en IP de confianza, seleccione **omitir varios-factor de autenticación para solicitudes de usuarios federados en mi intranet**.</span><span class="sxs-lookup"><span data-stu-id="0021d-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Nube](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="0021d-161">Haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="0021d-161">Click **save**.</span></span>
8. <span data-ttu-id="0021d-162">Una vez que se han aplicado las actualizaciones de hello, haga clic en **cerrar**.</span><span class="sxs-lookup"><span data-stu-id="0021d-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="0021d-163">¡Ya está!</span><span class="sxs-lookup"><span data-stu-id="0021d-163">That’s it!</span></span> <span data-ttu-id="0021d-164">En este momento, los usuarios federados de Office 365 solamente deben tener toouse MFA cuando una notificación se origina en la intranet corporativa de hello exterior.</span><span class="sxs-lookup"><span data-stu-id="0021d-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
