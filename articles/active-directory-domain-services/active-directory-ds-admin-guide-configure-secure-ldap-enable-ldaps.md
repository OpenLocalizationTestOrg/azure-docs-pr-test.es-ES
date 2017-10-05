---
title: "Configuración de LDAP seguro (LDAPS) en Azure AD Domain Services | Microsoft Docs"
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
ms.openlocfilehash: 3b19f078b0d6dc3e02d951014056406fd1b099a8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="configure-secure-ldap-ldaps-for-an-azure-ad-domain-services-managed-domain"></a><span data-ttu-id="0557d-103">Configuración de LDAP seguro (LDAPS) para un dominio administrado con Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0557d-103">Configure secure LDAP (LDAPS) for an Azure AD Domain Services managed domain</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0557d-104">Antes de empezar</span><span class="sxs-lookup"><span data-stu-id="0557d-104">Before you begin</span></span>
<span data-ttu-id="0557d-105">Asegúrese de que ha completado la [Tarea 2: Exportación del certificado LDAP seguro a un archivo .PFX](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span><span class="sxs-lookup"><span data-stu-id="0557d-105">Ensure you've completed [Task 2 - export the secure LDAP certificate to a .PFX file](active-directory-ds-admin-guide-configure-secure-ldap-export-pfx.md).</span></span>

<span data-ttu-id="0557d-106">Elija si usar la experiencia de Azure Portal (versión preliminar) o el portal de Azure clásico para completar esta tarea.</span><span class="sxs-lookup"><span data-stu-id="0557d-106">Choose whether to use the preview Azure portal experience or the Azure classic portal to complete this task.</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0557d-107">**Azure Portal (versión preliminar)**: [habilite LDAP seguro con Azure Portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span><span class="sxs-lookup"><span data-stu-id="0557d-107">**Azure portal (Preview)**: [Enable secure LDAP using the Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps.md)</span></span>
> * <span data-ttu-id="0557d-108">**Portal de Azure clásico**: [habilite LDAP seguro con el Portal de Azure clásico](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span><span class="sxs-lookup"><span data-stu-id="0557d-108">**Azure classic portal**: [Enable secure LDAP using the classic Azure portal](active-directory-ds-admin-guide-configure-secure-ldap-enable-ldaps-classic.md)</span></span>
>
>


## <a name="task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview"></a><span data-ttu-id="0557d-109">Tarea 3: Habilitación de LDAP seguro para el dominio administrado mediante Azure Portal (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="0557d-109">Task 3 - enable secure LDAP for the managed domain using the Azure portal (Preview)</span></span>
<span data-ttu-id="0557d-110">Realice los siguientes pasos de configuración para habilitar LDAP seguro:</span><span class="sxs-lookup"><span data-stu-id="0557d-110">To enable secure LDAP, perform the following configuration steps:</span></span>

1. <span data-ttu-id="0557d-111">Vaya a **[Azure Portal](https://portal.azure.com)**.</span><span class="sxs-lookup"><span data-stu-id="0557d-111">Navigate to the **[Azure portal](https://portal.azure.com)**.</span></span>

2. <span data-ttu-id="0557d-112">Busque 'servicios de dominio de' en el cuadro de búsqueda **Buscar recursos**.</span><span class="sxs-lookup"><span data-stu-id="0557d-112">Search for 'domain services' in the **Search resources** search box.</span></span> <span data-ttu-id="0557d-113">En el resultado de la búsqueda, seleccione **Azure AD Domain Services**.</span><span class="sxs-lookup"><span data-stu-id="0557d-113">Select **Azure AD Domain Services** from the search result.</span></span> <span data-ttu-id="0557d-114">La hoja **Azure AD Domain Services** mostrará el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-114">The **Azure AD Domain Services** blade lists your managed domain.</span></span>

    ![Búsqueda del dominio administrado aprovisionado](./media/getting-started/domain-services-provisioning-state-find-resource.png)

2. <span data-ttu-id="0557d-116">Haga clic en el nombre del dominio administrado (por ejemplo, "contoso100.com") para ver más detalles sobre el dominio.</span><span class="sxs-lookup"><span data-stu-id="0557d-116">Click the name of the managed domain (for example, 'contoso100.com') to see more details about the domain.</span></span>

    ![Domain Services: estado de aprovisionamiento](./media/getting-started/domain-services-provisioning-state.png)

3. <span data-ttu-id="0557d-118">Haga clic en **LDAP seguro** en el panel de navegación.</span><span class="sxs-lookup"><span data-stu-id="0557d-118">Click **Secure LDAP** on the navigation pane.</span></span>

    ![Hoja Servicios de dominio: LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade.png)

4. <span data-ttu-id="0557d-120">De forma predeterminada, se deshabilita el acceso de LDAP seguro a su dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-120">By default, secure LDAP access to your managed domain is disabled.</span></span> <span data-ttu-id="0557d-121">Cambie **LDAP seguro** a **Habilitar**.</span><span class="sxs-lookup"><span data-stu-id="0557d-121">Toggle **Secure LDAP** to **Enable**.</span></span>

    ![Habilitación de LDAP seguro](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configure.png)
5. <span data-ttu-id="0557d-123">De forma predeterminada, el acceso de LDAP seguro al dominio administrado sobre Internet está deshabilitado.</span><span class="sxs-lookup"><span data-stu-id="0557d-123">By default, secure LDAP access to your managed domain over the internet is disabled.</span></span> <span data-ttu-id="0557d-124">Cambie **Permitir el acceso mediante LDAP seguro a través de Internet** a **Habilitar**, si lo desea.</span><span class="sxs-lookup"><span data-stu-id="0557d-124">Toggle **Allow secure LDAP access over the internet** to **Enable**, if desired.</span></span> 

6. <span data-ttu-id="0557d-125">Haga clic en el icono de la carpeta que sigue al archivo **.PFX con el certificado LDAP seguro**.</span><span class="sxs-lookup"><span data-stu-id="0557d-125">Click the folder icon following **.PFX file with secure LDAP certificate**.</span></span> <span data-ttu-id="0557d-126">Especifique la ruta de acceso al archivo PFX con el certificado para el acceso de LDAP seguro al dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-126">Specify the path to the PFX file with the certificate for secure LDAP access to the managed domain.</span></span>

7. <span data-ttu-id="0557d-127">Especifique la **contraseña para descifrar el archivo .PFX**.</span><span class="sxs-lookup"><span data-stu-id="0557d-127">Specify the **Password to decrypt .PFX file**.</span></span> <span data-ttu-id="0557d-128">Proporcione la misma contraseña que usó al exportar el certificado al archivo PFX.</span><span class="sxs-lookup"><span data-stu-id="0557d-128">Provide the same password you used when exporting the certificate to the PFX file.</span></span>

8. <span data-ttu-id="0557d-129">Cuando haya terminado, haga clic en el botón **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="0557d-129">When you are done, click the **Save** button.</span></span>

9. <span data-ttu-id="0557d-130">Verá una notificación que le informará de que el LDAP seguro se ha configurado para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-130">You see a notification that informs you secure LDAP is being configured for the managed domain.</span></span> <span data-ttu-id="0557d-131">Hasta que se complete la operación, no podrá modificar otras configuraciones para el dominio.</span><span class="sxs-lookup"><span data-stu-id="0557d-131">Until this operation is complete, you cannot modify other settings for the domain.</span></span>

    ![Configuración del LDAP seguro para el dominio administrado](./media/active-directory-domain-services-admin-guide/secure-ldap-blade-configuring.png)

> [!NOTE]
> <span data-ttu-id="0557d-133">Se tardará entre unos 10 y 15 minutos en habilitar LDAP seguro para el dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-133">It takes about 10 to 15 minutes to enable secure LDAP for your managed domain.</span></span> <span data-ttu-id="0557d-134">Si el certificado LDAP seguro proporcionado no coincide con los criterios necesarios, no se habilitará LDAP seguro para el directorio y aparecerá un mensaje de error.</span><span class="sxs-lookup"><span data-stu-id="0557d-134">If the provided secure LDAP certificate does not match the required criteria, secure LDAP is not enabled for your directory and you see a failure.</span></span> <span data-ttu-id="0557d-135">Por ejemplo, se indicará que el nombre de dominio es incorrecto, que el certificado ha expirado o que lo hará pronto.</span><span class="sxs-lookup"><span data-stu-id="0557d-135">For example, the domain name is incorrect, the certificate has already expired or expires soon.</span></span> <span data-ttu-id="0557d-136">En este caso, vuelva a intentarlo con un certificado válido.</span><span class="sxs-lookup"><span data-stu-id="0557d-136">In this case, retry with a valid certificate.</span></span>
>
>

<br>

## <a name="task-4---configure-dns-to-access-the-managed-domain-from-the-internet"></a><span data-ttu-id="0557d-137">Tarea 4: Configuración de DNS para acceder al dominio administrado desde Internet</span><span class="sxs-lookup"><span data-stu-id="0557d-137">Task 4 - configure DNS to access the managed domain from the internet</span></span>
> [!NOTE]
> <span data-ttu-id="0557d-138">**Tarea opcional** : omita esta tarea de configuración si no piensa acceder al dominio administrado con LDAPS a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="0557d-138">**Optional task** - If you do not plan to access the managed domain using LDAPS over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="0557d-139">Antes de comenzar esta tarea, asegúrese de haber completado los pasos que se describen en la [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="0557d-139">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="0557d-140">Una vez habilitado el acceso LDAP seguro a través de Internet para el dominio administrado, debe actualizar el DNS para que los equipos cliente puedan encontrar este dominio administrado.</span><span class="sxs-lookup"><span data-stu-id="0557d-140">Once you have enabled secure LDAP access over the internet for your managed domain, you need to update DNS so that client computers can find this managed domain.</span></span> <span data-ttu-id="0557d-141">Al final de la tarea 3, aparece una dirección IP externa en la hoja **Configurar**, en **DIRECCIÓN IP EXTERNA PARA EL ACCESO LDAPS**.</span><span class="sxs-lookup"><span data-stu-id="0557d-141">At the end of task 3, an external IP address is displayed on the **Properties** blade in **EXTERNAL IP ADDRESS FOR LDAPS ACCESS**.</span></span>

<span data-ttu-id="0557d-142">Configure el proveedor de DNS externo para que el nombre DNS del dominio administrado (p. ej., ldaps.contoso100.com) señale a esta dirección IP externa.</span><span class="sxs-lookup"><span data-stu-id="0557d-142">Configure your external DNS provider so that the DNS name of the managed domain (for example, 'ldaps.contoso100.com') points to this external IP address.</span></span> <span data-ttu-id="0557d-143">En este ejemplo, es necesario crear la entrada DNS siguiente:</span><span class="sxs-lookup"><span data-stu-id="0557d-143">In our example, we need to create the following DNS entry:</span></span>

    ldaps.contoso100.com  -> 52.165.38.113

<span data-ttu-id="0557d-144">Eso es todo: ya está listo para conectarse al dominio administrado mediante LDAP seguro a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="0557d-144">That's it - you are now ready to connect to the managed domain using secure LDAP over the internet.</span></span>

> [!WARNING]
> <span data-ttu-id="0557d-145">Recuerde que los equipos cliente deben confiar en el emisor del certificado LDAPS para poder conectarse correctamente al dominio administrado mediante LDAPS.</span><span class="sxs-lookup"><span data-stu-id="0557d-145">Remember that client computers must trust the issuer of the LDAPS certificate to be able to connect successfully to the managed domain using LDAPS.</span></span> <span data-ttu-id="0557d-146">Si usa una entidad de certificación de confianza pública, no tendrá que realizar ninguna acción, ya que los equipos cliente confiarán en los emisores de certificados.</span><span class="sxs-lookup"><span data-stu-id="0557d-146">If you are using a publicly trusted certification authority, you do not need to do anything since client computers trust these certificate issuers.</span></span> <span data-ttu-id="0557d-147">Si utiliza un certificado autofirmado, instale la parte pública del certificado autofirmado en el almacén de certificados de confianza del equipo cliente.</span><span class="sxs-lookup"><span data-stu-id="0557d-147">If you are using a self-signed certificate, install the public part of the self-signed certificate into the trusted certificate store on the client computer.</span></span>
>
>


## <a name="task-5---lock-down-ldaps-access-to-your-managed-domain-over-the-internet"></a><span data-ttu-id="0557d-148">Tarea 5: Bloqueo del acceso LDAPS del dominio administrado a través de Internet</span><span class="sxs-lookup"><span data-stu-id="0557d-148">Task 5 - lock-down LDAPS access to your managed domain over the internet</span></span>
> [!NOTE]
> <span data-ttu-id="0557d-149">**Tarea opcional**: si no ha habilitado el acceso LDAPS en el dominio administrado a través de Internet, omita esta tarea de configuración.</span><span class="sxs-lookup"><span data-stu-id="0557d-149">**Optional task** - If you have not enabled LDAPS access to the managed domain over the internet, skip this configuration task.</span></span>
>
>

<span data-ttu-id="0557d-150">Antes de comenzar esta tarea, asegúrese de haber completado los pasos que se describen en la [tarea 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span><span class="sxs-lookup"><span data-stu-id="0557d-150">Before you begin this task, ensure you have completed the steps outlined in [Task 3](#task-3---enable-secure-ldap-for-the-managed-domain-using-the-azure-portal-preview).</span></span>

<span data-ttu-id="0557d-151">La exposición del dominio administrado para el acceso LDAPS a través de Internet representa una amenaza de seguridad.</span><span class="sxs-lookup"><span data-stu-id="0557d-151">Exposing your managed domain for LDAPS access over the internet represents a security threat.</span></span> <span data-ttu-id="0557d-152">Se puede alcanzar el dominio administrado desde Internet en el puerto usado para LDAP seguro (es decir, el puerto 636).</span><span class="sxs-lookup"><span data-stu-id="0557d-152">The managed domain is reachable from the internet at the port used for secure LDAP (that is, port 636).</span></span> <span data-ttu-id="0557d-153">Por lo tanto, puede elegir restringir el acceso al dominio administrado a direcciones IP conocidas específicas.</span><span class="sxs-lookup"><span data-stu-id="0557d-153">Therefore, you can choose to restrict access to the managed domain to specific known IP addresses.</span></span> <span data-ttu-id="0557d-154">Para mejorar la seguridad, cree un grupo de seguridad de red (NSG) y asócielo a la subred en la que habilitó Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="0557d-154">For improved security, create a network security group (NSG) and associate it with the subnet where you have enabled Azure AD Domain Services.</span></span>

<span data-ttu-id="0557d-155">En la siguiente tabla se muestra un NSG de ejemplo que puede configurar para bloquear el acceso LDAP seguro a través de Internet.</span><span class="sxs-lookup"><span data-stu-id="0557d-155">The following table illustrates a sample NSG you can configure, to lock down secure LDAP access over the internet.</span></span> <span data-ttu-id="0557d-156">NSG contiene un conjunto de reglas que permiten el acceso LDAPS de entrada a través del puerto TCP 636 solo desde un conjunto especificado de direcciones IP.</span><span class="sxs-lookup"><span data-stu-id="0557d-156">The NSG contains a set of rules that allow inbound LDAPS access over TCP port 636 only from a specified set of IP addresses.</span></span> <span data-ttu-id="0557d-157">La regla predeterminada 'DenyAll' se aplica a todo el tráfico de entrada de Internet.</span><span class="sxs-lookup"><span data-stu-id="0557d-157">The default 'DenyAll' rule applies to all other inbound traffic from the internet.</span></span> <span data-ttu-id="0557d-158">La regla NSG para permitir el acceso LDAPS a través de Internet desde direcciones IP especificadas tiene una prioridad mayor que la regla NSG DenyAll.</span><span class="sxs-lookup"><span data-stu-id="0557d-158">The NSG rule to allow LDAPS access over the internet from specified IP addresses has a higher priority than the DenyAll NSG rule.</span></span>

![NSG de muestra para el acceso LDAPS seguro a través de Internet](./media/active-directory-domain-services-admin-guide/secure-ldap-sample-nsg.png)

<span data-ttu-id="0557d-160">**Más información** - [Grupos de seguridad de red](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="0557d-160">**More information** - [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="0557d-161">Contenido relacionado</span><span class="sxs-lookup"><span data-stu-id="0557d-161">Related content</span></span>
* [<span data-ttu-id="0557d-162">Introducción a Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0557d-162">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="0557d-163">Administer an Azure AD Domain Services managed domain (Administración de un dominio administrado con Servicios de dominio de Azure AD)</span><span class="sxs-lookup"><span data-stu-id="0557d-163">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="0557d-164">Administración de directiva de grupo en un dominio administrado de Azure AD Domain Services</span><span class="sxs-lookup"><span data-stu-id="0557d-164">Administer Group Policy on an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-group-policy.md)
* [<span data-ttu-id="0557d-165">Grupos de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="0557d-165">Network security groups</span></span>](../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="0557d-166">Creación de un grupo de seguridad de red</span><span class="sxs-lookup"><span data-stu-id="0557d-166">Create a Network Security Group</span></span>](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)
