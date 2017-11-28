---
title: "Volver a ejecutar Asistente de instalación de Connect de hello Azure AD | Documentos de Microsoft"
description: "Explica cómo el Asistente para instalación de hello funciona Hola segunda vez que se ejecuta."
keywords: "Asistente para la instalación de Hello AD Azure Connect permite configurar Hola de configuración de mantenimiento segunda vez que se ejecuta"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="5d975-104">Azure AD Connect sync: ejecutando el Asistente para la instalación de hello otra vez</span><span class="sxs-lookup"><span data-stu-id="5d975-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="5d975-105">Hello primera vez que ejecute el Asistente para la instalación de hello Azure AD Connect, le explicamos cómo tooconfigure la instalación.</span><span class="sxs-lookup"><span data-stu-id="5d975-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="5d975-106">Si ejecuta el Asistente para la instalación de Hola de nuevo, ofrece opciones para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="5d975-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="5d975-107">Puede encontrar el Asistente para la instalación de hello en el menú de inicio de hello denominado **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="5d975-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Menú Inicio](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="5d975-109">Cuando se inicia el Asistente para la instalación de hello, verá una página con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="5d975-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Página con una lista de tareas adicionales](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="5d975-111">Si ha instalado ADFS con Azure AD Connect podrá ver incluso más opciones.</span><span class="sxs-lookup"><span data-stu-id="5d975-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="5d975-112">Hola opciones adicionales que tenga por AD FS se documentan en [administración de ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="5d975-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="5d975-113">Seleccione una de las tareas de Hola y haga clic en **siguiente** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="5d975-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5d975-114">Mientras tiene abierto el Asistente para la instalación de hello, se suspenden todas las operaciones de motor de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d975-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="5d975-115">Asegúrese de que cerrar el Asistente para la instalación de hello tan pronto como haya completado sus cambios de configuración.</span><span class="sxs-lookup"><span data-stu-id="5d975-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="5d975-116">Visualización de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="5d975-116">View current configuration</span></span>
<span data-ttu-id="5d975-117">Esta opción le proporciona una vista rápida de las opciones configuradas en ese momento.</span><span class="sxs-lookup"><span data-stu-id="5d975-117">This option gives you a quick view of your currently configured options.</span></span>

![Página con una lista de todas las opciones y su estado](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="5d975-119">Haga clic en **anterior** toogo back.</span><span class="sxs-lookup"><span data-stu-id="5d975-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="5d975-120">Si selecciona **Exit**, cierre el Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d975-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="5d975-121">Personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="5d975-121">Customize synchronization options</span></span>
<span data-ttu-id="5d975-122">Esta opción es la configuración de sincronización de toohello de cambios de toomake usado.</span><span class="sxs-lookup"><span data-stu-id="5d975-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="5d975-123">Vea un subconjunto de opciones de ruta de acceso de instalación de configuración personalizada de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d975-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="5d975-124">Incluso si ha utilizado la instalación rápida inicialmente verá estas opciones.</span><span class="sxs-lookup"><span data-stu-id="5d975-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="5d975-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Agregar más directorios).</span><span class="sxs-lookup"><span data-stu-id="5d975-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="5d975-126">Para quitar un directorio, consulte la sección sobre cómo [eliminar un conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="5d975-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="5d975-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Cambiar filtrado por dominio y unidad organizativa).</span><span class="sxs-lookup"><span data-stu-id="5d975-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="5d975-128">Remove Group filtering (Quitar filtrado de grupo).</span><span class="sxs-lookup"><span data-stu-id="5d975-128">Remove Group filtering.</span></span>
* <span data-ttu-id="5d975-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Cambiar las características opcionales).</span><span class="sxs-lookup"><span data-stu-id="5d975-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="5d975-130">Hola otras opciones de instalación inicial de hello no se puede cambiar y no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="5d975-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="5d975-131">Estas opciones son:</span><span class="sxs-lookup"><span data-stu-id="5d975-131">These options are:</span></span>

* <span data-ttu-id="5d975-132">Cambiar Hola atributo toouse para userPrincipalName y sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="5d975-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="5d975-133">Cambiar Hola unir método para los objetos de otro bosque.</span><span class="sxs-lookup"><span data-stu-id="5d975-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="5d975-134">Habilitación del filtrado basado en grupo.</span><span class="sxs-lookup"><span data-stu-id="5d975-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="5d975-135">Actualización del esquema de directorio</span><span class="sxs-lookup"><span data-stu-id="5d975-135">Refresh directory schema</span></span>
<span data-ttu-id="5d975-136">Esta opción se utiliza si ha cambiado el esquema de hello en uno de sus instalaciones en bosques de AD DS.</span><span class="sxs-lookup"><span data-stu-id="5d975-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="5d975-137">Por ejemplo, puede que haya instalado Exchange o actualizar el esquema de tooa Windows Server 2012 con objetos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="5d975-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="5d975-138">En este caso, se necesita tooinstruct Azure AD Connect tooread Hola esquema nuevo de AD DS y actualizar su caché.</span><span class="sxs-lookup"><span data-stu-id="5d975-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="5d975-139">Esta acción también vuelve a generar reglas de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d975-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="5d975-140">Si agrega el esquema de Exchange de hello, como ejemplo, reglas de sincronización de hello para el intercambio se agregan toohello configuración.</span><span class="sxs-lookup"><span data-stu-id="5d975-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="5d975-141">Cuando se selecciona esta opción, se muestran todos los directorios de hello en la configuración.</span><span class="sxs-lookup"><span data-stu-id="5d975-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="5d975-142">Puede conservar la configuración predeterminada de Hola y actualizar todos los bosques o anule la selección de algunas de ellas.</span><span class="sxs-lookup"><span data-stu-id="5d975-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Página con una lista de todos los directorios en el entorno de Hola](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="5d975-144">Configurar modo de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="5d975-144">Configure staging mode</span></span>
<span data-ttu-id="5d975-145">Esta opción permite tooenable y deshabilitar el modo de almacenamiento provisional en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="5d975-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="5d975-146">Puede encontrar más información acerca del modo de almacenamiento provisional y cómo se utiliza en [Sincronización de Azure AD Connect: tareas y consideraciones operativas](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="5d975-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="5d975-147">opción de Hello muestra si almacenamiento provisional está habilitado o deshabilitado:</span><span class="sxs-lookup"><span data-stu-id="5d975-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Opción que también se muestra el estado actual de Hola de modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="5d975-149">toochange Hola estado, seleccione esta opción y la casilla de verificación de hello seleccione o anule la selección.</span><span class="sxs-lookup"><span data-stu-id="5d975-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Opción que también se muestra el estado actual de Hola de modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="5d975-151">Cambiar inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="5d975-151">Change user sign-in</span></span>
<span data-ttu-id="5d975-152">Esta opción permite toochange de toofederation de sincronización de contraseña o hello revés.</span><span class="sxs-lookup"><span data-stu-id="5d975-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="5d975-153">No se puede cambiar demasiado**no configure**.</span><span class="sxs-lookup"><span data-stu-id="5d975-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="5d975-154">Para más información sobre esta opción, consulte [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="5d975-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d975-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5d975-155">Next steps</span></span>
* <span data-ttu-id="5d975-156">Obtener más información sobre el modelo de configuración de hello utilizado por la sincronización de Azure AD Connect en [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="5d975-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="5d975-157">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="5d975-157">**Overview topics**</span></span>

* [<span data-ttu-id="5d975-158">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="5d975-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="5d975-159">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5d975-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
