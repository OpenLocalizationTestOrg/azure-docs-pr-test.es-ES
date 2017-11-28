---
title: aaaConfigure seguro (LDAPS) de LDAP en servicios de dominio de AD de Azure | Documentos de Microsoft
description: "Configuración de LDAP seguro (LDAPS) para un dominio administrado con Servicios de dominio de Azure AD"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9d563c45-9578-410d-96c8-355af64feae8
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: maheshu
ms.openlocfilehash: a0d6e2faf474b1f0cbe157fb4ae2754b1d521ef9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0de67-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0de67-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0de67-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0de67-104">Before you begin</span></span>
<span data-ttu-id="0de67-105">Asegúrese de que ha completado [tarea 2: exportar Hola segura LDAP certificado tooa. Archivo PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="0de67-105">Ensure you've completed [Task 2 - export hello secure LDAP certificate tooa .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="0de67-106">Elegir entre toouse hello Azure experiencia del portal de vista previa o hello Azure toocomplete portal clásico esta tarea.</span><span class="sxs-lookup"><span data-stu-id="0de67-106">Choose whether toouse hello preview Azure portal experience or hello Azure classic portal toocomplete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0de67-107">**Portal de Azure (vista previa)**: [Enable secure LDAP mediante Hola portal de Azure](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="0de67-107">**Azure portal (Preview)**: [Enable secure LDAP using hello Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="0de67-108">**Portal de Azure clásico**: [Enable secure LDAP mediante el portal de Azure clásico Hola](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="0de67-108">**Azure classic portal**: [Enable secure LDAP using hello classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-hello-managed-domain-using-hello-classic-azure-portal"></a><span data-ttu-id="0de67-109">Tarea 3: habilitar LDAP seguro para hello dominio administrado mediante el portal de Azure clásico Hola</span><span class="sxs-lookup"><span data-stu-id="0de67-109">Task 3 - enable secure LDAP for hello managed domain using hello classic Azure portal</span></span>
<span data-ttu-id="0de67-110">tooenable LDAP seguro, realizar Hola siguiendo los pasos de configuración:</span><span class="sxs-lookup"><span data-stu-id="0de67-110">tooenable secure LDAP, perform hello following configuration steps:</span></span>

1. <span data-ttu-id="0de67-111">Navegue toohello  **[portal de Azure clásico](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="0de67-111">Navigate toohello **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="0de67-112">Seleccione hello **Active Directory** nodo en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de67-112">Select hello **Active Directory** node on hello left pane.</span></span>
3. <span data-ttu-id="0de67-113">Seleccione el directorio de hello Azure AD (también denominado tooas 'tenant'), que se han habilitado los servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="0de67-113">Select hello Azure AD directory (also referred tooas 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="0de67-115">Haga clic en hello **configurar** ficha.</span><span class="sxs-lookup"><span data-stu-id="0de67-115">Click hello **Configure** tab.</span></span>

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="0de67-117">Desplácese hacia abajo de la sección de toohello **servicios de dominio de**.</span><span class="sxs-lookup"><span data-stu-id="0de67-117">Scroll down toohello section titled **domain services**.</span></span> <span data-ttu-id="0de67-118">Debería ver una opción titulada **LDAP seguro (LDAPS)** tal y como se muestra en la siguiente captura de pantalla de hello:</span><span class="sxs-lookup"><span data-stu-id="0de67-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in hello following screenshot:</span></span>

    ![Sección de configuración de los Servicios de dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="0de67-120">Haga clic en hello **configurar certificado...**  toobring botón seguridad hello **Configure un certificado para LDAP seguro** cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="0de67-120">Click hello **Configure certificate ...** button toobring up hello **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurar certificado para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="0de67-122">Haga clic en siguiente de icono de carpeta de hello **archivo PFX con certificado** archivo PFX de hello de toospecify, que contiene el certificado de hello desea toouse para toohello de acceso LDAP seguro administrado dominio.</span><span class="sxs-lookup"><span data-stu-id="0de67-122">Click hello folder icon following **PFX FILE WITH CERTIFICATE** toospecify hello PFX file, which contains hello certificate you wish toouse for secure LDAP access toohello managed domain.</span></span> <span data-ttu-id="0de67-123">Especificar contraseña Hola especificado al exportar el archivo PFX de hello certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="0de67-123">Also enter hello password you specified when exporting hello certificate toohello PFX file.</span></span> <span data-ttu-id="0de67-124">A continuación, haga clic en hello realiza botón en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de67-124">Then, click hello done button on hello bottom.</span></span>

    ![Especificar la contraseña y archivos PFX para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="0de67-126">Hola **los servicios de dominio** sección de hello **configurar** ficha debe obtener en gris y se encuentra en hello **pendientes...**  estado durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0de67-126">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="0de67-127">Durante este período, se comprueba el certificado LDAPS Hola para precisión y LDAP seguro está configurada para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0de67-127">During this period, hello LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="0de67-129">Se tarda unos 10 minutos de too15 tooenable LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0de67-129">It takes about 10 too15 minutes tooenable secure LDAP for your managed domain.</span></span> <span data-ttu-id="0de67-130">Si Hola proporcionado no coincide con el certificado LDAP seguro Hola necesario criterios, LDAP seguro no está habilitada para el directorio y verá un error.</span><span class="sxs-lookup"><span data-stu-id="0de67-130">If hello provided secure LDAP certificate does not match hello required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="0de67-131">Por ejemplo, nombre de dominio de hello es incorrecto, el certificado de Hola ya ha expirado o va a expirar pronto.</span><span class="sxs-lookup"><span data-stu-id="0de67-131">For example, hello domain name is incorrect, hello certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="0de67-132">Cuando LDAP seguro está habilitado correctamente para el dominio administrado, Hola **pendientes...**  mensaje debería desaparecer.</span><span class="sxs-lookup"><span data-stu-id="0de67-132">When secure LDAP is successfully enabled for your managed domain, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="0de67-133">Debería ver la huella digital de Hola de hello certificados que se muestran.</span><span class="sxs-lookup"><span data-stu-id="0de67-133">You should see hello thumbprint of hello certificate displayed.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-hello-internet"></a><span data-ttu-id="0de67-135">Tarea 4: habilitar el acceso LDAP seguro a través de hello internet</span><span class="sxs-lookup"><span data-stu-id="0de67-135">Task 4 - enable secure LDAP access over hello internet</span></span>
<span data-ttu-id="0de67-136">**Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="0de67-136">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="0de67-137">Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0de67-137">Before you begin this task, ensure you have completed hello steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="0de67-138">Debería ver una opción demasiado**Hola habilitar SECURE LDAP acceso a través de INTERNET** en hello **los servicios de dominio** sección de hello **configurar** página.</span><span class="sxs-lookup"><span data-stu-id="0de67-138">You should see an option too**ENABLE SECURE LDAP ACCESS OVER hello INTERNET** in hello **domain services** section of hello **Configure** page.</span></span> <span data-ttu-id="0de67-139">Esta opción se establece demasiado**NO** de forma predeterminada porque internet access toohello administrada dominio a través de LDAP seguro está deshabilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="0de67-139">This option is set too**NO** by default since internet access toohello managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="0de67-141">Alternar **Hola habilitar SECURE LDAP acceso a través de INTERNET** demasiado**Sí**.</span><span class="sxs-lookup"><span data-stu-id="0de67-141">Toggle **ENABLE SECURE LDAP ACCESS OVER hello INTERNET** too**YES**.</span></span> <span data-ttu-id="0de67-142">Haga clic en hello **guardar** botón en el panel inferior Hola.</span><span class="sxs-lookup"><span data-stu-id="0de67-142">Click hello **SAVE** button on hello bottom panel.</span></span>
    <span data-ttu-id="0de67-143">![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="0de67-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="0de67-144">Hola **los servicios de dominio** sección de hello **configurar** ficha debe obtener en gris y se encuentra en hello **pendientes...**  estado durante unos minutos.</span><span class="sxs-lookup"><span data-stu-id="0de67-144">hello **domain services** section of hello **Configure** tab should get grayed out and is in hello **Pending...** state for a few minutes.</span></span> <span data-ttu-id="0de67-145">Más tarde, está habilitado el acceso a internet tooyour dominio administrado a través de LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="0de67-145">After some time, internet access tooyour managed domain over secure LDAP is enabled.</span></span>

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="0de67-147">Tarda aproximadamente 10 minutos tooenable acceso a internet a través de LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0de67-147">It takes about 10 minutes tooenable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="0de67-148">Si tooyour de acceso LDAP seguro administra dominio a través Hola internet se habilitó correctamente, Hola **pendientes...**  mensaje debería desaparecer.</span><span class="sxs-lookup"><span data-stu-id="0de67-148">When secure LDAP access tooyour managed domain over hello internet is successfully enabled, hello **Pending...** message should disappear.</span></span> <span data-ttu-id="0de67-149">Debería ver direcciones IP externas de Hola de direcciones que pueden ser utilizados tooaccess su directorio sobre LDAPS en campo hello **dirección de IP externas para acceso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="0de67-149">You should see hello external IP address that can be used tooaccess your directory over LDAPS in hello field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-tooaccess-hello-managed-domain-from-hello-internet"></a><span data-ttu-id="0de67-151">Tarea 5: configurar DNS tooaccess Hola dominio administrado de hello internet</span><span class="sxs-lookup"><span data-stu-id="0de67-151">Task 5 - configure DNS tooaccess hello managed domain from hello internet</span></span>
<span data-ttu-id="0de67-152">**Tareas opcionales** : si no tiene previsto tooaccess Hola dominio administrado usa LDAPS más Hola a internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="0de67-152">**Optional task** - If you do not plan tooaccess hello managed domain using LDAPS over hello internet, skip this configuration task.</span></span>

<span data-ttu-id="0de67-153">Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="0de67-153">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="0de67-154">Después de habilitar el acceso LDAP seguro a través de internet de hello para el dominio administrado, deberá tooupdate DNS para que los equipos cliente puedan encontrar este dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0de67-154">Once you have enabled secure LDAP access over hello internet for your managed domain, you need tooupdate DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="0de67-155">Al final de saludo de la tarea 4, se muestra una dirección IP externa en hello **configurar** ficha **dirección de IP externas para acceso de LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="0de67-155">At hello end of task 4, an external IP address is displayed on hello **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="0de67-156">Configurar el proveedor de DNS externo para que ese nombre DNS de Hola de hello administrados direcciones IP externas de dominio (por ejemplo, ' ldaps.contoso100.com') toothis puntos.</span><span class="sxs-lookup"><span data-stu-id="0de67-156">Configure your external DNS provider so that hello DNS name of hello managed domain (for example, 'ldaps.contoso100.com') points toothis external IP address.</span></span> <span data-ttu-id="0de67-157">En nuestro ejemplo, necesitamos hello toocreate siguiente entrada DNS:</span><span class="sxs-lookup"><span data-stu-id="0de67-157">In our example, we need toocreate hello following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="0de67-158">¡Eso es todo: ya estás toohello tooconnect listo administrado Hola de dominio mediante LDAP seguro en internet.</span><span class="sxs-lookup"><span data-stu-id="0de67-158">That's it - you are now ready tooconnect toohello managed domain using secure LDAP over hello internet.</span></span>

> [!WARNING]
> <span data-ttu-id="0de67-159">Recuerde que los equipos cliente deben confiar emisor Hola de hello LDAPS certificado toobe pueda tooconnect correctamente toohello administrado dominio usa LDAPS.</span><span class="sxs-lookup"><span data-stu-id="0de67-159">Remember that client computers must trust hello issuer of hello LDAPS certificate toobe able tooconnect successfully toohello managed domain using LDAPS.</span></span> <span data-ttu-id="0de67-160">Si utilizas una entidad de certificación empresarial o una entidad de certificación de confianza pública, que no necesite toodo nada ya que estos emisores de certificados de confianza de los equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="0de67-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need toodo anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="0de67-161">Si está utilizando un certificado autofirmado, debe parte pública de hello tooinstall del certificado autofirmado de hello en el almacén de certificados de confianza de hello en el equipo cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="0de67-161">If you are using a self-signed certificate, you need tooinstall hello public part of hello self-signed certificate into hello trusted certificate store on hello client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-tooyour-managed-domain-over-hello-internet"></a><span data-ttu-id="0de67-162">Bloquear LDAPS tener acceso a dominio administrado tooyour sobre Hola internet</span><span class="sxs-lookup"><span data-stu-id="0de67-162">Lock-down LDAPS access tooyour managed domain over hello internet</span></span>
> [!NOTE]
> <span data-ttu-id="0de67-163">**Tareas opcionales** : si no se ha habilitado LDAPS dominio administrado de acceso toohello en Hola internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="0de67-163">**Optional task** - If you have not enabled LDAPS access toohello managed domain over hello internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="0de67-164">Antes de comenzar esta tarea, asegúrese de haber completado los pasos de Hola que se describen en [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="0de67-164">Before you begin this task, ensure you have completed hello steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="0de67-165">Exposición de su dominio administrado para el acceso LDAPS sobre Hola internet representa una amenaza para la seguridad.</span><span class="sxs-lookup"><span data-stu-id="0de67-165">Exposing your managed domain for LDAPS access over hello internet represents a security threat.</span></span> <span data-ttu-id="0de67-166">Hello dominio administrado sea accesible desde Hola internet en el puerto de hello usado para LDAP seguro (es decir, el puerto 636).</span><span class="sxs-lookup"><span data-stu-id="0de67-166">hello managed domain is reachable from hello internet at hello port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="0de67-167">Por lo tanto, puede elegir toorestrict acceso toohello administrado dominio toospecific conocida direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="0de67-167">Therefore, you can choose toorestrict access toohello managed domain toospecific known IP addresses.</span></span> <span data-ttu-id="0de67-168">Para mejorar la seguridad, cree un grupo de seguridad de red (NSG) y asociarla a la subred de Hola donde ha habilitado los servicios de dominio de AD de Azure.</span><span class="sxs-lookup"><span data-stu-id="0de67-168">For improved security, create a network security group (NSG) and associate it with hello subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="0de67-169">Hello siguiente tabla muestra un ejemplo de NSG puede configurar, toolock hacia abajo el acceso LDAP seguro a través de hello internet.</span><span class="sxs-lookup"><span data-stu-id="0de67-169">hello following table illustrates a sample NSG you can configure, toolock down secure LDAP access over hello internet.</span></span> <span data-ttu-id="0de67-170">Hola NSG contiene un conjunto de reglas que permitan el acceso de entrada LDAPS a través del puerto TCP 636 solo de un conjunto especificado de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="0de67-170">hello NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="0de67-171">Hello 'DenyAll' reglas predeterminadas aplican tooall otro tráfico entrante de hello internet.</span><span class="sxs-lookup"><span data-stu-id="0de67-171">hello default 'DenyAll' rule applies tooall other inbound traffic from hello internet.</span></span> <span data-ttu-id="0de67-172">regla de acceso LDAPS NSG tooallow sobre Hola Hola internet desde direcciones IP especificadas tiene una prioridad más alta que Hola regla DenyAll NSG.</span><span class="sxs-lookup"><span data-stu-id="0de67-172">hello NSG rule tooallow LDAPS access over hello internet from specified IP addresses has a higher priority than hello DenyAll NSG rule.</span></span>

![Acceso de ejemplo NSG toosecure LDAPS sobre Hola internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="0de67-174">**Más información** - [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="0de67-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="0de67-175">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="0de67-175">Related content</span></span>
* [<span data-ttu-id="0de67-176">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0de67-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="0de67-177">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="0de67-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="0de67-178">Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0de67-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="0de67-179">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="0de67-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="0de67-180">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="0de67-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
