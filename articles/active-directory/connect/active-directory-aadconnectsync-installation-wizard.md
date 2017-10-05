---
title: "Volver a ejecutar el Asistente para instalación de Azure AD Connect | Microsoft Docs"
description: "Explica cómo funciona el Asistente para la instalación la segunda vez que lo ejecute."
keywords: "El Asistente para instalación de Azure AD Connect le permite configurar opciones de mantenimiento la segunda vez que se ejecuta"
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="d136f-104">Sincronización de Azure AD Connect: ejecución por segunda vez del Asistente para la instalación</span><span class="sxs-lookup"><span data-stu-id="d136f-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="d136f-105">La primera vez que ejecute el Asistente para la instalación de Azure AD Connect, este lo guiará a través de la configuración de la instalación.</span><span class="sxs-lookup"><span data-stu-id="d136f-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="d136f-106">Si vuelve a ejecutarlo, le ofrecerá opciones para el mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="d136f-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="d136f-107">Puede encontrar el Asistente para la instalación en el menú de inicio **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="d136f-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Menú Inicio](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="d136f-109">Cuando se inicia el Asistente para la instalación, aparece una página con estas opciones:</span><span class="sxs-lookup"><span data-stu-id="d136f-109">When you start the installation wizard, you see a page with these options:</span></span>

![Página con una lista de tareas adicionales](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="d136f-111">Si ha instalado ADFS con Azure AD Connect podrá ver incluso más opciones.</span><span class="sxs-lookup"><span data-stu-id="d136f-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="d136f-112">Estas opciones adicionales que tenga por ADFS se documentan en [Administración de AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="d136f-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="d136f-113">Seleccione una de las tareas y haga clic en **Siguiente** para continuar.</span><span class="sxs-lookup"><span data-stu-id="d136f-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d136f-114">Mientras tiene abierto el Asistente para la instalación, todas las operaciones en el motor de sincronización se suspenden.</span><span class="sxs-lookup"><span data-stu-id="d136f-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="d136f-115">Asegúrese de cerrar el Asistente para instalación tan pronto como haya terminado los cambios de configuración que desea realizar.</span><span class="sxs-lookup"><span data-stu-id="d136f-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="d136f-116">Visualización de la configuración actual.</span><span class="sxs-lookup"><span data-stu-id="d136f-116">View current configuration</span></span>
<span data-ttu-id="d136f-117">Esta opción le proporciona una vista rápida de las opciones configuradas en ese momento.</span><span class="sxs-lookup"><span data-stu-id="d136f-117">This option gives you a quick view of your currently configured options.</span></span>

![Página con una lista de todas las opciones y su estado](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="d136f-119">Haga clic en **Anterior** para volver atrás.</span><span class="sxs-lookup"><span data-stu-id="d136f-119">Click **Previous** to go back.</span></span> <span data-ttu-id="d136f-120">Si selecciona **Salir**, se cerrará el Asistente para la instalación.</span><span class="sxs-lookup"><span data-stu-id="d136f-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="d136f-121">Personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="d136f-121">Customize synchronization options</span></span>
<span data-ttu-id="d136f-122">Esta opción se utiliza para realizar cambios en la configuración de sincronización.</span><span class="sxs-lookup"><span data-stu-id="d136f-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="d136f-123">Se mostrará un subconjunto de opciones de la ruta de instalación de la configuración personalizada.</span><span class="sxs-lookup"><span data-stu-id="d136f-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="d136f-124">Incluso si ha utilizado la instalación rápida inicialmente verá estas opciones.</span><span class="sxs-lookup"><span data-stu-id="d136f-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="d136f-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Agregar más directorios).</span><span class="sxs-lookup"><span data-stu-id="d136f-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="d136f-126">Para quitar un directorio, consulte la sección sobre cómo [eliminar un conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="d136f-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="d136f-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Cambiar filtrado por dominio y unidad organizativa).</span><span class="sxs-lookup"><span data-stu-id="d136f-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="d136f-128">Remove Group filtering (Quitar filtrado de grupo).</span><span class="sxs-lookup"><span data-stu-id="d136f-128">Remove Group filtering.</span></span>
* <span data-ttu-id="d136f-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Cambiar las características opcionales).</span><span class="sxs-lookup"><span data-stu-id="d136f-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="d136f-130">Las demás opciones de la instalación inicial no se pueden cambiar y no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="d136f-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="d136f-131">Estas opciones son:</span><span class="sxs-lookup"><span data-stu-id="d136f-131">These options are:</span></span>

* <span data-ttu-id="d136f-132">Cambio del atributo que se utiliza para userPrincipalName y sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="d136f-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="d136f-133">Cambio del método de unión para objetos de un bosque diferente.</span><span class="sxs-lookup"><span data-stu-id="d136f-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="d136f-134">Habilitación del filtrado basado en grupo.</span><span class="sxs-lookup"><span data-stu-id="d136f-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="d136f-135">Actualización del esquema de directorio</span><span class="sxs-lookup"><span data-stu-id="d136f-135">Refresh directory schema</span></span>
<span data-ttu-id="d136f-136">Esta opción se utiliza si ha cambiado el esquema de una de sus instalaciones locales de bosques de AD DS.</span><span class="sxs-lookup"><span data-stu-id="d136f-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="d136f-137">Por ejemplo, puede haber instalado Exchange o actualizado a un esquema de Windows Server 2012 con objetos de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d136f-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="d136f-138">En este caso, tiene que indicar a Azure AD Connect que vuelva a leer el esquema de AD DS y actualice su memoria caché.</span><span class="sxs-lookup"><span data-stu-id="d136f-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="d136f-139">Esta acción también vuelve a generar las reglas de sincronización.</span><span class="sxs-lookup"><span data-stu-id="d136f-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="d136f-140">Si agrega el esquema de Exchange, por ejemplo, las reglas de sincronización para Exchange se agregan a la configuración.</span><span class="sxs-lookup"><span data-stu-id="d136f-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="d136f-141">Cuando se selecciona esta opción, se muestran todos los directorios en la configuración.</span><span class="sxs-lookup"><span data-stu-id="d136f-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="d136f-142">Puede mantener la configuración predeterminada y actualizar todos los bosques o anular la selección de algunos de ellos.</span><span class="sxs-lookup"><span data-stu-id="d136f-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Página con una lista de todos los directorios en el entorno](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="d136f-144">Configurar modo de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="d136f-144">Configure staging mode</span></span>
<span data-ttu-id="d136f-145">Esta opción le permite habilitar y deshabilitar el modo de almacenamiento provisional en el servidor.</span><span class="sxs-lookup"><span data-stu-id="d136f-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="d136f-146">Puede encontrar más información acerca del modo de almacenamiento provisional y cómo se utiliza en [Sincronización de Azure AD Connect: tareas y consideraciones operativas](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="d136f-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="d136f-147">La opción mostrará si el almacenamiento provisional está habilitado o deshabilitado: </span><span class="sxs-lookup"><span data-stu-id="d136f-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Opción que también muestra el estado actual del modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="d136f-149">Para cambiar el estado, seleccione esta opción y seleccione o anule la selección de la casilla.</span><span class="sxs-lookup"><span data-stu-id="d136f-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Opción que también muestra el estado actual del modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="d136f-151">Cambiar inicio de sesión de usuario</span><span class="sxs-lookup"><span data-stu-id="d136f-151">Change user sign-in</span></span>
<span data-ttu-id="d136f-152">Esta opción permite cambiar de sincronización de contraseñas a la federación o al revés.</span><span class="sxs-lookup"><span data-stu-id="d136f-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="d136f-153">No se puede cambiar a **No configurar**.</span><span class="sxs-lookup"><span data-stu-id="d136f-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="d136f-154">Para más información sobre esta opción, consulte [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="d136f-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d136f-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d136f-155">Next steps</span></span>
* <span data-ttu-id="d136f-156">Obtenga más información sobre el modelo de configuración que emplea la sincronización de Azure AD Connect en el artículo de información sobre el [aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="d136f-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="d136f-157">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="d136f-157">**Overview topics**</span></span>

* [<span data-ttu-id="d136f-158">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="d136f-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="d136f-159">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d136f-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
