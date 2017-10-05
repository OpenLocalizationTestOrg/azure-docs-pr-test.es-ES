---
title: "Administración de dispositivos con Azure Portal (versión preliminar) | Microsoft Docs"
description: Aprenda a usar Azure Portal para administrar dispositivos.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="3fba1-103">Administración de dispositivos con Azure Portal (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="3fba1-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="3fba1-104">Esta funcionalidad se encuentra actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="3fba1-104">This capability currently is in public preview.</span></span> <span data-ttu-id="3fba1-105">Debe estar preparado para deshacer o eliminar los cambios.</span><span class="sxs-lookup"><span data-stu-id="3fba1-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="3fba1-106">La característica está disponible en cualquier suscripción de Azure Active Directory (Azure AD) durante el período de versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="3fba1-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="3fba1-107">Pero cuando ya esté disponible con carácter general, algunos aspectos de ella podrían requerir una suscripción Premium de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3fba1-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="3fba1-108">Con la administración de dispositivos en Azure Active Directory (Azure AD), puede asegurarse de que los usuarios tienen acceso a los recursos desde dispositivos que cumplen los estándares de seguridad y cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="3fba1-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="3fba1-109">En este tema:</span><span class="sxs-lookup"><span data-stu-id="3fba1-109">This topic:</span></span>

- <span data-ttu-id="3fba1-110">Se da por hecho que está familiarizado con la [introducción a la administración de dispositivos en Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="3fba1-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="3fba1-111">Se proporciona información sobre la administración de dispositivos mediante Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3fba1-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="3fba1-112">Para administrar dispositivos en Azure Portal, debe hacer clic en **Dispositivos** en la sección **Administrar** de la hoja **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="3fba1-114">Configuración de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3fba1-114">Configure device settings</span></span>

<span data-ttu-id="3fba1-115">Para administrar los dispositivos mediante Azure Portal, estos deben estar registrados o unidos a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="3fba1-116">Como administrador, puede ajustar el proceso de registro y unión de dispositivos al configurar los valores del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fba1-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="3fba1-118">La hoja de configuración de dispositivo permite configurar:</span><span class="sxs-lookup"><span data-stu-id="3fba1-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="3fba1-119">**Los usuarios pueden inscribir dispositivos en Azure AD**: esta opción permite seleccionar los usuarios que pueden unir dispositivos a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="3fba1-120">El valor predeterminado es **Todos**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-120">The default is **All**.</span></span>

- <span data-ttu-id="3fba1-121">**Administradores locales adicionales en dispositivos unidos a Azure AD**: puede seleccionar a qué usuarios se conceden derechos de administrador local en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fba1-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="3fba1-122">Los usuarios agregados aquí se agregan al rol *Administradores de dispositivos* de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="3fba1-123">De forma predeterminada, a los administradores globales de Azure AD y a los propietarios de dispositivos se les conceden derechos de administrador local.</span><span class="sxs-lookup"><span data-stu-id="3fba1-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="3fba1-124">Esta opción es una capacidad de la edición Premium disponible en productos como Azure AD Premium o Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="3fba1-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="3fba1-125">**Los usuarios pueden registrar sus dispositivos con Azure AD**: debe configurar esta opción para permitir que los dispositivos se registren en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="3fba1-126">Si selecciona **Ninguno**, no se permite a los dispositivos registrarse si no están unidos a Azure AD o a Azure AD híbrido.</span><span class="sxs-lookup"><span data-stu-id="3fba1-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="3fba1-127">La inscripción en Microsoft Intune o Administración de dispositivos móviles (MDM) para Office 365 exige registrarse.</span><span class="sxs-lookup"><span data-stu-id="3fba1-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="3fba1-128">Si ha configurado alguno de estos servicios, se selecciona **TODOS** y **NINGUNO** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="3fba1-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="3fba1-129">**Requerir Multi-factor Auth para conectar dispositivos**: puede decidir si se exige a los usuarios proporcionar un segundo factor de autenticación para unir su dispositivo a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="3fba1-130">El valor predeterminado es **No**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-130">The default is **No**.</span></span> <span data-ttu-id="3fba1-131">Se recomienda exigir Multi-Factor Authentication al registrar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fba1-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="3fba1-132">Antes de habilitar Multi-Factor Authentication para este servicio, debe asegurarse de que está configurado para los usuarios que registran sus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3fba1-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="3fba1-133">Para más información sobre los distintos servicios de Azure Multi-Factor Authentication, vea [Introducción a Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3fba1-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="3fba1-134">**Número máximo de dispositivos**: esta opción permite seleccionar el número máximo de dispositivos que puede tener un usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="3fba1-135">Si un usuario alcanza esta cuota, no puede agregar dispositivos adicionales hasta que se quitan uno o varios de los dispositivos existentes.</span><span class="sxs-lookup"><span data-stu-id="3fba1-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="3fba1-136">La cuota de dispositivos cuenta todos los dispositivos unidos a Azure AD o registrados en Azure AD hoy.</span><span class="sxs-lookup"><span data-stu-id="3fba1-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="3fba1-137">El valor predeterminado es **20**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-137">The default value is **20**.</span></span>

- <span data-ttu-id="3fba1-138">**Los usuarios pueden sincronizar la configuración y los datos de aplicaciones en distintos dispositivos**: de forma predeterminada, esta opción se establece en **NINGUNO**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="3fba1-139">La selección de usuarios o grupos concretos o de TODOS permite sincronizar la configuración y los datos de aplicación del usuario en sus dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3fba1-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="3fba1-140">Más información sobre cómo funciona la sincronización en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="3fba1-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="3fba1-141">Esta opción es una capacidad Premium disponible en productos como Azure AD Premium o Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="3fba1-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Administración de un dispositivo de Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="3fba1-143">Búsqueda de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3fba1-143">Locate devices</span></span>

<span data-ttu-id="3fba1-144">Como administrador, en Azure Portal tiene dos opciones para buscar dispositivos registrados y unidos:</span><span class="sxs-lookup"><span data-stu-id="3fba1-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="3fba1-145">**Todos los dispositivos** en la sección **Administrar** de la hoja **Dispositivos**</span><span class="sxs-lookup"><span data-stu-id="3fba1-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Todos los dispositivos](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="3fba1-147">**Dispositivos** en la sección **Administrar** de la hoja **Usuarios**</span><span class="sxs-lookup"><span data-stu-id="3fba1-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Todos los dispositivos](./media/device-management-azure-portal/43.png)



<span data-ttu-id="3fba1-149">Con ambas opciones, puede ir a una vista que:</span><span class="sxs-lookup"><span data-stu-id="3fba1-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="3fba1-150">Permite buscar dispositivos si se usa el nombre para mostrar como filtro.</span><span class="sxs-lookup"><span data-stu-id="3fba1-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="3fba1-151">Proporciona información general detallada de los dispositivos registrados y unidos.</span><span class="sxs-lookup"><span data-stu-id="3fba1-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="3fba1-152">Permite realizar tareas comunes de administración de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3fba1-152">Enables you to perform common device management tasks</span></span>
   

![Todos los dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="3fba1-154">Tareas de administración de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3fba1-154">Device management tasks</span></span>

<span data-ttu-id="3fba1-155">Como administrador, puede administrar los dispositivos registrados o unidos.</span><span class="sxs-lookup"><span data-stu-id="3fba1-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="3fba1-156">En esta sección se proporciona información sobre las tareas comunes de administración de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3fba1-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="3fba1-157">**Administrar un dispositivo de Intune**: si es administrador de Intune, puede administrar los dispositivos marcados como **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="3fba1-158">Un administrador puede ver dispositivos adicionales</span><span class="sxs-lookup"><span data-stu-id="3fba1-158">An administrator can see additional device</span></span> 

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="3fba1-160">**Habilitar o deshabilitar un dispositivo de Azure AD**</span><span class="sxs-lookup"><span data-stu-id="3fba1-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="3fba1-161">Para habilitar o deshabilitar un dispositivo, debe ser administrador global en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="3fba1-162">Al deshabilitar un dispositivo se evita que acceda a los recursos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="3fba1-163">Para deshabilitar el dispositivo, puede hacer clic en *...*</span><span class="sxs-lookup"><span data-stu-id="3fba1-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="3fba1-164">o hacer clic en el dispositivo para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="3fba1-164">click the device for additional details.</span></span>

 
![Administración de un dispositivo de Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="3fba1-166">Al deshabilitar un dispositivo, el estado de la columna **HABILITADO** cambia a **No**.</span><span class="sxs-lookup"><span data-stu-id="3fba1-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Deshabilitación de un dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="3fba1-168">**Eliminar un dispositivo de Azure AD**: para eliminar un dispositivo, debe ser administrador global en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="3fba1-169">La eliminación de un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3fba1-169">Deleting a device:</span></span>
 
- <span data-ttu-id="3fba1-170">Evita que un dispositivo acceda a los recursos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="3fba1-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="3fba1-171">Quita todos los detalles asociados al dispositivo, por ejemplo, las claves de BitLocker de dispositivos Windows</span><span class="sxs-lookup"><span data-stu-id="3fba1-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="3fba1-172">Representa una actividad no recuperable y no se recomienda a menos que sea necesaria</span><span class="sxs-lookup"><span data-stu-id="3fba1-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="3fba1-173">Si un dispositivo está administrado por otra entidad de administración (por ejemplo, Microsoft Intune), asegúrese de que el dispositivo se haya borrado o retirado antes de eliminarlo de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="3fba1-174">Puede seleccionar "..."</span><span class="sxs-lookup"><span data-stu-id="3fba1-174">You can either select “…”</span></span> <span data-ttu-id="3fba1-175">para eliminar el dispositivo o hacer clic en él para obtener más detalles</span><span class="sxs-lookup"><span data-stu-id="3fba1-175">to delete the device or click on the device for additional details</span></span>
 
![Eliminar un dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="3fba1-177">**Ver o copiar el identificador de dispositivo**: puede usar un identificador de dispositivo para comprobar los detalles del identificador de dispositivo en el dispositivo o usar PowerShell durante la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="3fba1-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="3fba1-178">Para acceder a la opción de copia, haga clic en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fba1-178">To access the copy option, click the device.</span></span>

![Visualización de identificador de dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="3fba1-180">**Ver o copiar las claves de BitLocker**: si es administrador, puede ver y copiar las claves de BitLocker para ayudar a los usuarios a recuperar su unidad cifrada.</span><span class="sxs-lookup"><span data-stu-id="3fba1-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="3fba1-181">Estas claves solo están disponibles para dispositivos Windows cifrados y con las claves almacenadas en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3fba1-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="3fba1-182">Puede copiar estas claves al acceder a los detalles del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3fba1-182">You can copy these keys when accessing details of the device.</span></span>
 
![Visualización de claves de BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="3fba1-184">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="3fba1-184">Audit logs</span></span>


<span data-ttu-id="3fba1-185">Las actividades de un dispositivo están disponibles a través de los registros de actividad.</span><span class="sxs-lookup"><span data-stu-id="3fba1-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="3fba1-186">Esto incluye actividades desencadenadas por el servicio de registro de dispositivos o por el usuario:</span><span class="sxs-lookup"><span data-stu-id="3fba1-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="3fba1-187">Creación de dispositivos e incorporación de propietarios o usuarios al dispositivo</span><span class="sxs-lookup"><span data-stu-id="3fba1-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="3fba1-188">Cambios en la configuración de un dispositivo</span><span class="sxs-lookup"><span data-stu-id="3fba1-188">Changes to device settings</span></span>

- <span data-ttu-id="3fba1-189">Operaciones de dispositivo como eliminar o actualizar un dispositivo</span><span class="sxs-lookup"><span data-stu-id="3fba1-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="3fba1-190">El punto de entrada a los datos de auditoría es **Registros de auditoría**, en la sección **Actividad** de la hoja **Dispositivos*.</span><span class="sxs-lookup"><span data-stu-id="3fba1-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Registros de auditoría](./media/device-management-azure-portal/61.png)


<span data-ttu-id="3fba1-192">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="3fba1-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="3fba1-193">la fecha y hora de la repetición</span><span class="sxs-lookup"><span data-stu-id="3fba1-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="3fba1-194">los destinos</span><span class="sxs-lookup"><span data-stu-id="3fba1-194">the targets</span></span>

- <span data-ttu-id="3fba1-195">el iniciador o actor (quién) de una actividad</span><span class="sxs-lookup"><span data-stu-id="3fba1-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="3fba1-196">la actividad (qué)</span><span class="sxs-lookup"><span data-stu-id="3fba1-196">the activity (what)</span></span>

![Registros de auditoría](./media/device-management-azure-portal/63.png)

<span data-ttu-id="3fba1-198">Puede personalizar la vista de lista, haga clic en **Columnas** en la barra de herramientas.</span><span class="sxs-lookup"><span data-stu-id="3fba1-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Registros de auditoría](./media/device-management-azure-portal/64.png)


<span data-ttu-id="3fba1-200">Para restringir los datos del informe a un nivel que se adapte a sus necesidades, puede filtrar los datos de auditoría con los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="3fba1-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="3fba1-201">Categoría</span><span class="sxs-lookup"><span data-stu-id="3fba1-201">Catergory</span></span>
- <span data-ttu-id="3fba1-202">Tipo de recurso de actividad</span><span class="sxs-lookup"><span data-stu-id="3fba1-202">Activity resource type</span></span>
- <span data-ttu-id="3fba1-203">Actividad</span><span class="sxs-lookup"><span data-stu-id="3fba1-203">Activity</span></span>
- <span data-ttu-id="3fba1-204">Intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="3fba1-204">Date range</span></span>
- <span data-ttu-id="3fba1-205">Destino</span><span class="sxs-lookup"><span data-stu-id="3fba1-205">Target</span></span>
- <span data-ttu-id="3fba1-206">Iniciado por (actor)</span><span class="sxs-lookup"><span data-stu-id="3fba1-206">Initiated By (Actor)</span></span>

<span data-ttu-id="3fba1-207">Además de los filtros, puede buscar entradas concretas.</span><span class="sxs-lookup"><span data-stu-id="3fba1-207">In addition to the filters, you can search for specific entries.</span></span>

![Registros de auditoría](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="3fba1-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3fba1-209">Next steps</span></span>

* [<span data-ttu-id="3fba1-210">Introducción a la administración de dispositivos en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3fba1-210">Introduction to device management in Azure Active Directory</span></span>](device-management-introduction.md)



