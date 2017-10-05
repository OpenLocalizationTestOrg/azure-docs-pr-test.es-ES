---
title: "Configuración de LDAP seguro (LDAPS) en Azure AD Domain Services | Microsoft Docs"
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
ms.openlocfilehash: 3aafe209aad7383cd0610d147b5fdba673023c93
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="629d7-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="629d7-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="629d7-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="629d7-104">Before you begin</span></span>
<span data-ttu-id="629d7-105">Asegúrese de que ha completado la [Tarea 2: Exportación del certificado LDAP seguro a un archivo .PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="629d7-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="629d7-106">Elija si usar la experiencia de Azure Portal (versión preliminar) o el portal de Azure clásico para completar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="629d7-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="629d7-107">**Azure Portal (versión preliminar)**: [habilite LDAP seguro con Azure Portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="629d7-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="629d7-108">**Portal de Azure clásico**: [habilitación de LDAP seguro con el portal de Azure clásico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="629d7-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal"></a><span data-ttu-id="629d7-109">Tarea 3: Habilitación de LDAP seguro para el dominio administrado mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="629d7-109">Task 3 - enable secure LDAP for the managed domain using the classic Azure portal</span></span>
<span data-ttu-id="629d7-110">Realice los siguientes pasos de configuración para habilitar LDAP seguro:</span><span class="sxs-lookup"><span data-stu-id="629d7-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="629d7-111">Vaya al **[Portal de Azure clásico](https://manage.windowsazure.com)**.</span><span class="sxs-lookup"><span data-stu-id="629d7-111">Navigate to the **[Azure classic portal](https://manage.windowsazure.com)**.</span></span>
2. <span data-ttu-id="629d7-112">En el panel izquierdo, seleccione **Active Directory** .</span><span class="sxs-lookup"><span data-stu-id="629d7-112">Select the **Active Directory** node on the left pane.</span></span>
3. <span data-ttu-id="629d7-113">Seleccione el directorio de Azure AD (también denominado "inquilino"), para el que se ha habilitado Servicios de dominio de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629d7-113">Select the Azure AD directory (also referred to as 'tenant'), for which you have enabled Azure AD Domain Services.</span></span>

    ![Selección de un directorio de Azure AD](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. <span data-ttu-id="629d7-115">Haga clic en la pestaña **Configure** .</span><span class="sxs-lookup"><span data-stu-id="629d7-115">Click the **Configure** tab.</span></span>

    ![Pestaña Configurar del directorio](./media/active-directory-domain-services-getting-started/configure-tab.png)
5. <span data-ttu-id="629d7-117">Desplácese hacia abajo hasta la sección **Servicios de dominio**.</span><span class="sxs-lookup"><span data-stu-id="629d7-117">Scroll down to the section titled **domain services**.</span></span> <span data-ttu-id="629d7-118">Verá una opción denominada **LDAP seguro (LDAPS)** como se muestra en la captura de pantalla siguiente:</span><span class="sxs-lookup"><span data-stu-id="629d7-118">You should see an option titled **Secure LDAP (LDAPS)** as shown in the following screenshot:</span></span>

    ![Sección de configuración de los Servicios de dominio](./media/active-directory-domain-services-admin-guide/secure-ldap-start.png)
6. <span data-ttu-id="629d7-120">Haga clic en el botón **Configurar certificado** para abrir el cuadro de diálogo **Configurar certificado para LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="629d7-120">Click the **Configure certificate ...** button to bring up the **Configure Certificate for Secure LDAP** dialog.</span></span>

    ![Configurar certificado para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-configure-cert-page.png)
7. <span data-ttu-id="629d7-122">Haga clic en el siguiente icono de carpeta que encontrará bajo **ARCHIVO PFX CON CERTIFICADO** para especificar el archivo PFX, que contiene el certificado que desea usar para el acceso LDAP seguro al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="629d7-122">Click the folder icon following **PFX FILE WITH CERTIFICATE** to specify the PFX file, which contains the certificate you wish to use for secure LDAP access to the managed domain.</span></span> <span data-ttu-id="629d7-123">Escriba también la contraseña especificada al exportar el certificado al archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="629d7-123">Also enter the password you specified when exporting the certificate to the PFX file.</span></span> <span data-ttu-id="629d7-124">A continuación, haga clic en el botón Listo de la parte inferior.</span><span class="sxs-lookup"><span data-stu-id="629d7-124">Then, click the done button on the bottom.</span></span>

    ![Especificar la contraseña y archivos PFX para LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-specify-pfx.png)
8. <span data-ttu-id="629d7-126">La sección **Servicios de dominio** de la pestaña **Configurar** debería aparecer en gris y con el estado **Pendiente...** unos minutos.</span><span class="sxs-lookup"><span data-stu-id="629d7-126">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="629d7-127">Durante este período, se verifica la precisión del certificado LDAPS y se configura LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="629d7-127">During this period, the LDAPS certificate is verified for accuracy and secure LDAP is configured for your managed domain.</span></span>

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="629d7-129">Se tardará entre unos 10 y 15 minutos en habilitar LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="629d7-129">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="629d7-130">Si el certificado LDAP seguro proporcionado no coincide con los criterios necesarios, no se habilitará LDAP seguro para el directorio y aparecerá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="629d7-130">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="629d7-131">Por ejemplo, se indicará que el nombre de dominio es incorrecto, que el certificado ha expirado o que lo hará pronto.</span><span class="sxs-lookup"><span data-stu-id="629d7-131">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span>
   >
   >

9. <span data-ttu-id="629d7-132">Cuando LDAP seguro se haya habilitado correctamente para su dominio administrado, el mensaje **Pendiente** debería desaparecer.</span><span class="sxs-lookup"><span data-stu-id="629d7-132">When secure LDAP is successfully enabled for your managed domain, the **Pending...** message should disappear.</span></span> <span data-ttu-id="629d7-133">Debería ver la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="629d7-133">You should see the thumbprint of the certificate displayed.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled.png)

<br>

## <a name="task-4---enable-secure-ldap-access-over-the-internet"></a><span data-ttu-id="629d7-135">Tarea 4: Habilitación del acceso LDAP seguro a través de Internet</span><span class="sxs-lookup"><span data-stu-id="629d7-135">Task 4 - enable secure LDAP access over the internet</span></span>
<span data-ttu-id="629d7-136">**Tarea opcional** : omita esta tarea de configuración si no piensa acceder al dominio administrado con LDAPS a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="629d7-136">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="629d7-137">Antes de comenzar esta tarea, asegúrese de haber completado los pasos que se describen en la [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="629d7-137">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-classic-azure-portal).</span></span>

1. <span data-ttu-id="629d7-138">Debería ver la opción **HABILITAR EL ACCESO LDAP SEGURO A TRAVÉS DE INTERNET** en la sección **Servicios de dominio** de la página **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="629d7-138">You should see an option to **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** in the **domain services** section of the **Configure** page.</span></span> <span data-ttu-id="629d7-139">Dicha opción tendrá el valor **NO** de forma predeterminada, ya que el acceso por Internet al dominio administrado a través de LDAP seguro está deshabilitado de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="629d7-139">This option is set to **NO** by default since internet access to the managed domain over secure LDAP is disabled by default.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enabled2.png)
2. <span data-ttu-id="629d7-141">Cambie **HABILITAR EL ACCESO LDAP SEGURO A TRAVÉS DE INTERNET** a **SÍ**.</span><span class="sxs-lookup"><span data-stu-id="629d7-141">Toggle **ENABLE SECURE LDAP ACCESS OVER THE INTERNET** to **YES**.</span></span> <span data-ttu-id="629d7-142">Haga clic en el botón **GUARDAR** del panel inferior.</span><span class="sxs-lookup"><span data-stu-id="629d7-142">Click the **SAVE** button on the bottom panel.</span></span>
    <span data-ttu-id="629d7-143">![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span><span class="sxs-lookup"><span data-stu-id="629d7-143">![Secure LDAP enabled](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access.png)</span></span>
3. <span data-ttu-id="629d7-144">La sección **Servicios de dominio** de la pestaña **Configurar** debería aparecer en gris y con el estado **Pendiente...** unos minutos.</span><span class="sxs-lookup"><span data-stu-id="629d7-144">The **domain services** section of the **Configure** tab should get grayed out and is in the **Pending...** state for a few minutes.</span></span> <span data-ttu-id="629d7-145">Pasado unos instantes, se habilitará el acceso por Internet al dominio administrado mediante LDAP seguro.</span><span class="sxs-lookup"><span data-stu-id="629d7-145">After some time, internet access to your managed domain over secure LDAP is enabled.</span></span>

    ![LDAP seguro: estado pendiente](./media/active-directory-domain-services-admin-guide/secure-ldap-enable-internet-access-pending-state.png)

   > [!NOTE]
   > <span data-ttu-id="629d7-147">Habilitar el acceso por Internet mediante LDAP seguro para el dominio administrado llevará unos 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="629d7-147">It takes about 10 minutes to enable internet access over secure LDAP for your managed domain.</span></span>
   >
   >
4. <span data-ttu-id="629d7-148">Si el acceso mediante LDAP seguro a su dominio administrado a través de Internet se habilita correctamente, el mensaje **Pendiente** debería desaparecer.</span><span class="sxs-lookup"><span data-stu-id="629d7-148">When secure LDAP access to your managed domain over the internet is successfully enabled, the **Pending...** message should disappear.</span></span> <span data-ttu-id="629d7-149">Debería ver la dirección IP externa que puede utilizarse para acceder a su directorio mediante LDAPS en el campo **DIRECCIÓN IP EXTERNA PARA EL ACCESO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="629d7-149">You should see the external IP address that can be used to access your directory over LDAPS in the field **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

    ![LDAP seguro habilitado](./media/active-directory-domain-services-admin-guide/secure-ldap-internet-access-enabled.png)

<br>

## <a name="task-5---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="629d7-151">Tarea 5: Configuración de DNS para acceder al dominio administrado desde Internet</span><span class="sxs-lookup"><span data-stu-id="629d7-151">Task 5 - configure DNS to access the managed domain from the internet</span></span>
<span data-ttu-id="629d7-152">**Tarea opcional** : omita esta tarea de configuración si no piensa acceder al dominio administrado con LDAPS a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="629d7-152">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>

<span data-ttu-id="629d7-153">Antes de comenzar esta tarea, asegúrese de haber completado los pasos que se describen en la [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="629d7-153">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="629d7-154">Una vez habilitado el acceso LDAP seguro a través de Internet para el dominio administrado, debe actualizar el DNS para que los equipos cliente puedan encontrar este dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="629d7-154">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="629d7-155">Al final de la tarea 4, aparece una dirección IP externa en la pestaña **Configurar**, en **DIRECCIÓN IP EXTERNA PARA EL ACCESO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="629d7-155">At the end of task 4, an external IP address is displayed on the **Configure** tab in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="629d7-156">Configure el proveedor de DNS externo para que el nombre DNS del dominio administrado (p. ej., ldaps.contoso100.com) señale a esta dirección IP externa.</span><span class="sxs-lookup"><span data-stu-id="629d7-156">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="629d7-157">En este ejemplo, es necesario crear la entrada DNS siguiente:</span><span class="sxs-lookup"><span data-stu-id="629d7-157">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="629d7-158">Eso es todo: ya está listo para conectarse al dominio administrado mediante LDAP seguro a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="629d7-158">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="629d7-159">Recuerde que los equipos cliente deben confiar en el emisor del certificado LDAPS para poder conectarse correctamente al dominio administrado mediante LDAPS.</span><span class="sxs-lookup"><span data-stu-id="629d7-159">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="629d7-160">Si usa una entidad de certificación empresarial o una entidad de certificación de confianza pública, no tendrá que realizar ninguna acción, ya que los equipos cliente confiarán en los emisores de certificados.</span><span class="sxs-lookup"><span data-stu-id="629d7-160">If you are using an enterprise certification authority or a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="629d7-161">Si utiliza un certificado autofirmado, tendrá que instalar la parte pública del certificado autofirmado en el almacén de certificados de confianza del equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="629d7-161">If you are using a self-signed certificate, you need to install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="629d7-162">Bloqueo del acceso LDAPS en el dominio administrado a través de Internet</span><span class="sxs-lookup"><span data-stu-id="629d7-162">Lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="629d7-163">**Tarea opcional**: si no ha habilitado el acceso LDAPS en el dominio administrado a través de Internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="629d7-163">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="629d7-164">Antes de comenzar esta tarea, asegúrese de haber completado los pasos que se describen en la [tarea 4](#task-4---enable-secure-ldap-access-over-the-internet).</span><span class="sxs-lookup"><span data-stu-id="629d7-164">Before you begin this task, ensure you have completed the steps outlined in [Task 4](#task-4---enable-secure-ldap-access-over-the-internet).</span></span>

<span data-ttu-id="629d7-165">La exposición del dominio administrado para el acceso LDAPS a través de Internet representa una amenaza de seguridad.</span><span class="sxs-lookup"><span data-stu-id="629d7-165">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="629d7-166">Se puede alcanzar el dominio administrado desde Internet en el puerto usado para LDAP seguro (es decir, el puerto 636).</span><span class="sxs-lookup"><span data-stu-id="629d7-166">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="629d7-167">Por lo tanto, puede elegir restringir el acceso al dominio administrado a direcciones IP conocidas específicas.</span><span class="sxs-lookup"><span data-stu-id="629d7-167">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="629d7-168">Para mejorar la seguridad, cree un grupo de seguridad de red (NSG) y asócielo a la subred en la que habilitó Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="629d7-168">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="629d7-169">En la siguiente tabla se muestra un NSG de ejemplo que puede configurar para bloquear el acceso LDAP seguro a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="629d7-169">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="629d7-170">NSG contiene un conjunto de reglas que permiten el acceso LDAPS de entrada a través del puerto TCP 636 solo desde un conjunto especificado de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="629d7-170">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="629d7-171">La regla predeterminada 'DenyAll' se aplica a todo el tráfico de entrada de Internet.</span><span class="sxs-lookup"><span data-stu-id="629d7-171">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="629d7-172">La regla NSG para permitir el acceso LDAPS a través de Internet desde direcciones IP especificadas tiene una prioridad mayor que la regla NSG DenyAll.</span><span class="sxs-lookup"><span data-stu-id="629d7-172">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![NSG de muestra para el acceso LDAPS seguro a través de Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="629d7-174">**Más información** - [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="629d7-174">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="629d7-175">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="629d7-175">Related content</span></span>
* [<span data-ttu-id="629d7-176">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="629d7-176">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="629d7-177">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="629d7-177">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="629d7-178">Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="629d7-178">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="629d7-179">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="629d7-179">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="629d7-180">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="629d7-180">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
