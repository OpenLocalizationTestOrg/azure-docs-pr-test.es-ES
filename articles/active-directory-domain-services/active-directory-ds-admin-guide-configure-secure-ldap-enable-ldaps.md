---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: c6da94b6-4328-4230-801a-4b646055d4d7
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: 8781285cd02d690788056b985b017efd7e4d6b3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="230b6-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="230b6-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="230b6-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="230b6-104">Before you begin</span></span>
<span data-ttu-id="230b6-105">Asegúrese de que ha completado [tarea 2: exportar Hola segura LDAP certificado tooa. Archivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="230b6-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="230b6-106">Elegir entre toouse hello Azure experiencia del portal de vista previa o hello Azure toocomplete portal clásico esta tarea.</span><span class="sxs-lookup"><span data-stu-id="230b6-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="230b6-107">**Portal de Azure (vista previa)**: [Enable secure LDAP mediante Hola portal de Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="230b6-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="230b6-108">**Portal de Azure clásico**: [Enable secure LDAP mediante el portal de Azure clásico Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="230b6-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-azure-portal-preview"></a><span data-ttu-id="230b6-109">Tarea 3: habilitar LDAP seguro de dominio administrados de hello mediante Hola portal de Azure (vista previa)</span><span class="sxs-lookup"><span data-stu-id="230b6-109">Task 3 - enable secure LDAP for hello managed domain using hello Azure portal (Preview)</span></span>
<span data-ttu-id="230b6-110">tooenable LDAP seguro, realizar Hola siguiendo los pasos de configuración:</span><span class="sxs-lookup"><span data-stu-id="230b6-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="230b6-111">Navegue toohello  **[portal de Azure](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="230b6-111">Navigate toohello **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="230b6-112">Busque "servicios de dominio' en hello **buscar recursos** cuadro de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="230b6-112">Search for 'domain services' in hello **Search resources** search box.</span></span> <span data-ttu-id="230b6-113">Seleccione **servicios de dominio de AD de Azure** Hola resultados de búsqueda.</span><span class="sxs-lookup"><span data-stu-id="230b6-113">Select **Azure AD Domain Services** from hello search result.</span></span> <span data-ttu-id="230b6-114">Hola **servicios de dominio de AD de Azure** hoja muestra el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="230b6-114">hello **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Búsqueda del dominio administrado que se va aprovisionar](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="230b6-116">Haga clic en Hola Hola administrado toosee de dominio (por ejemplo, ' contoso100.com') para obtener más detalles sobre el dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="230b6-116">Click hello name of hello managed domain (for example, 'contoso100.com') toosee more details about hello domain.</span></span>

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="230b6-118">Haga clic en **LDAP seguro** en el panel de navegación de Hola.</span><span class="sxs-lookup"><span data-stu-id="230b6-118">Click **Secure LDAP** on hello navigation pane.</span></span>

    ![Hoja Servicios de dominio: LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="230b6-120">De forma predeterminada, LDAP acceso tooyour administrado dominio seguro está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="230b6-120">By default, secure LDAP access tooyour managed domain is disabled.</span></span> <span data-ttu-id="230b6-121">Alternar **LDAP seguro** demasiado**habilitar**.</span><span class="sxs-lookup"><span data-stu-id="230b6-121">Toggle **Secure LDAP** too**Enable**.</span></span>

    ![Habilitación de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="230b6-123">De forma predeterminada, tooyour de acceso LDAP seguro administra dominio a través de hello que Internet está deshabilitada.</span><span class="sxs-lookup"><span data-stu-id="230b6-123">By default, secure LDAP access tooyour managed domain over hello internet is disabled.</span></span> <span data-ttu-id="230b6-124">Alternar **Hola a permitir acceso LDAP seguro a través de internet** demasiado**habilitar**, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="230b6-124">Toggle **Allow secure LDAP access over hello internet** too**Enable**, if desired.</span></span> 

6. <span data-ttu-id="230b6-125">Haga clic en siguiente de icono de carpeta de hello **. Archivo PFX con certificado LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="230b6-125">Click hello folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="230b6-126">Especifique archivo PFX de hello ruta de acceso toohello con certificado de Hola para LDAP acceso toohello administrado dominio seguro.</span><span class="sxs-lookup"><span data-stu-id="230b6-126">Specify hello path toohello PFX file with hello certificate for secure LDAP access toohello managed domain.</span></span>

7. <span data-ttu-id="230b6-127">Especificar hello **toodecrypt de contraseña. Archivo PFX**.</span><span class="sxs-lookup"><span data-stu-id="230b6-127">Specify hello **Password toodecrypt .PFX file**.</span></span> <span data-ttu-id="230b6-128">Proporcionar Hola contraseña que se usa al exportar el archivo PFX de hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="230b6-128">Provide hello same password you used when exporting hello certificate toohello PFX file.</span></span>

8. <span data-ttu-id="230b6-129">Cuando haya terminado, haga clic en hello **guardar** botón.</span><span class="sxs-lookup"><span data-stu-id="230b6-129">When you are done, click hello **Save** button.</span></span>

9. <span data-ttu-id="230b6-130">Verá una notificación que le informa de que LDAP seguro se configura de dominio administrados Hola.</span><span class="sxs-lookup"><span data-stu-id="230b6-130">You see a notification that informs you secure LDAP is being configured for hello managed domain.</span></span> <span data-ttu-id="230b6-131">Hasta que se complete esta operación, no se puede modificar otras configuraciones de dominio de Hola.</span><span class="sxs-lookup"><span data-stu-id="230b6-131">Until this operation is complete, you cannot modify other settings for hello domain.</span></span>

    ![Configuración de LDAP seguro para el dominio administrado Hola](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="230b6-133">Se tarda unos 10 minutos de too15 tooenable LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="230b6-133">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="230b6-134">Si Hola proporcionado no coincide con el certificado LDAP seguro Hola necesario criterios, LDAP seguro no está habilitada para el directorio y verá un error.</span><span class="sxs-lookup"><span data-stu-id="230b6-134">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="230b6-135">Por ejemplo, nombre de dominio de hello es incorrecto, el certificado de Hola ya ha expirado o va a expirar pronto.</span><span class="sxs-lookup"><span data-stu-id="230b6-135">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span> <span data-ttu-id="230b6-136">En este caso, vuelva a intentarlo con un certificado válido.</span><span class="sxs-lookup"><span data-stu-id="230b6-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="230b6-137">Tarea 4: configurar DNS tooaccess Hola dominio administrado de hello internet</span><span class="sxs-lookup"><span data-stu-id="230b6-137">Task 4 - configure DNS tooaccess hello managed domain from hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="230b6-138">**Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="230b6-138">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="230b6-139">Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="230b6-139">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="230b6-140">Después de habilitar el acceso LDAP seguro a través de internet de hello para el dominio administrado, deberá tooupdate DNS para que los equipos cliente puedan encontrar este dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="230b6-140">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="230b6-141">Al final de Hola de tarea 3, se muestra una dirección IP externa en hello **propiedades** hoja en **dirección de IP externas para acceso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="230b6-141">At hello end of task 3, an external IP address is displayed on hello **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="230b6-142">Configurar el proveedor de DNS externo para que ese nombre DNS de Hola de hello administrados direcciones IP externas de dominio (por ejemplo, ' ldaps.contoso100.com') toothis puntos.</span><span class="sxs-lookup"><span data-stu-id="230b6-142">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="230b6-143">En nuestro ejemplo, necesitamos hello toocreate siguiente entrada DNS:</span><span class="sxs-lookup"><span data-stu-id="230b6-143">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="230b6-144">¡Eso es todo: ya estás toohello tooconnect listo administrado Hola de dominio mediante LDAP seguro en internet.</span><span class="sxs-lookup"><span data-stu-id="230b6-144">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="230b6-145">Recuerde que los equipos cliente deben confiar emisor Hola de hello LDAPS certificado toobe pueda tooconnect correctamente toohello administrado dominio usa LDAPS.</span><span class="sxs-lookup"><span data-stu-id="230b6-145">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="230b6-146">Si utilizas una entidad de certificación de confianza pública, que no necesite toodo nada ya que estos emisores de certificados de confianza de los equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="230b6-146">If you are using a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="230b6-147">Si está utilizando un certificado autofirmado, instale parte pública de Hola de certificado autofirmado de hello en el almacén de certificados de confianza de hello en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="230b6-147">If you are using a self-signed certificate, install hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="230b6-148">Tarea 5: bloquear LDAPS acceso tooyour administrado Hola de dominio a través de internet</span><span class="sxs-lookup"><span data-stu-id="230b6-148">Task 5 - lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="230b6-149">**Tareas opcionales** : si no se ha habilitado LDAPS dominio administrado de acceso toohello en Hola internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="230b6-149">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="230b6-150">Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="230b6-150">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="230b6-151">Exposición de su dominio administrado para el acceso LDAPS sobre Hola internet representa una amenaza para la seguridad.</span><span class="sxs-lookup"><span data-stu-id="230b6-151">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="230b6-152">Hello dominio administrado sea accesible desde Hola internet en el puerto de hello usado para LDAP seguro (es decir, el puerto 636).</span><span class="sxs-lookup"><span data-stu-id="230b6-152">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="230b6-153">Por lo tanto, puede elegir toorestrict acceso toohello administrado dominio toospecific conocida direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="230b6-153">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="230b6-154">Para mejorar la seguridad, cree un grupo de seguridad de red (NSG) y asociarla a la subred de Hola donde ha habilitado los servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="230b6-154">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="230b6-155">Hello siguiente tabla muestra un ejemplo de NSG puede configurar, toolock hacia abajo el acceso LDAP seguro a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="230b6-155">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="230b6-156">Hola NSG contiene un conjunto de reglas que permitan el acceso de entrada LDAPS a través del puerto TCP 636 solo de un conjunto especificado de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="230b6-156">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="230b6-157">Hello 'DenyAll' reglas predeterminadas aplican tooall otro tráfico entrante de hello internet.</span><span class="sxs-lookup"><span data-stu-id="230b6-157">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="230b6-158">regla de acceso LDAPS NSG tooallow sobre Hola Hola internet desde direcciones IP especificadas tiene una prioridad más alta que Hola regla DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="230b6-158">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Acceso de ejemplo NSG toosecure LDAPS sobre Hola internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="230b6-160">**Más información** - [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="230b6-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="230b6-161">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="230b6-161">Related content</span></span>
* [<span data-ttu-id="230b6-162">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="230b6-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="230b6-163">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="230b6-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="230b6-164">Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="230b6-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="230b6-165">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="230b6-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="230b6-166">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="230b6-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
