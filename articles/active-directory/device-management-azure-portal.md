---
title: dispositivos de aaaManaging mediante Hola portal de Azure - vista previa | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola dispositivos toomanage de portal de Azure."
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
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="8cd8c-103">Administrar los dispositivos con Hola portal de Azure: obtener una vista previa</span><span class="sxs-lookup"><span data-stu-id="8cd8c-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="8cd8c-104">Esta funcionalidad se encuentra actualmente en versión preliminar pública.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-104">This capability currently is in public preview.</span></span> <span data-ttu-id="8cd8c-105">Prepararán toorevert o quitar los cambios.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="8cd8c-106">Hola característica está disponible en ninguna suscripción de Azure Active Directory (Azure AD) durante la vista previa pública.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="8cd8c-107">Sin embargo, cuando característica Hola deja de estar disponible con carácter general, algunos aspectos de la característica de hello pueden requerir una suscripción premium a Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="8cd8c-108">Con la administración de dispositivos en Azure Active Directory (Azure AD), puede asegurarse de que los usuarios tienen acceso a los recursos desde dispositivos que cumplen los estándares de seguridad y cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="8cd8c-109">En este tema:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-109">This topic:</span></span>

- <span data-ttu-id="8cd8c-110">Se da por supuesto que está familiarizado con hello [administración toodevice de introducción en Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="8cd8c-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="8cd8c-111">Proporciona información acerca de cómo administrar los dispositivos con Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="8cd8c-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="8cd8c-112">dispositivos de toomanage Hola portal de Azure, necesita tooclick **dispositivos** en hello **administrar** sección de Hola Hola **Azure Active Directory** hoja.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="8cd8c-114">Configuración de dispositivo</span><span class="sxs-lookup"><span data-stu-id="8cd8c-114">Configure device settings</span></span>

<span data-ttu-id="8cd8c-115">toomanage los dispositivos con hello portal de Azure, que necesitan toobe registrado o Unidos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="8cd8c-116">Como administrador, puede ajustar el proceso de Hola de registrar y al unir dispositivos al establecer la configuración de dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="8cd8c-118">hoja de configuración de dispositivo de Hello permite tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="8cd8c-119">**Los usuarios pueden inscribir dispositivos tooAzure AD** : esta configuración permite a los usuarios de tooselect Hola que se pueden unir dispositivos tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="8cd8c-120">valor predeterminado de Hello es **todos los**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-120">hello default is **All**.</span></span>

- <span data-ttu-id="8cd8c-121">**Dispositivos Unidos a los administradores locales adicionales de Azure AD** -puede seleccionar los usuarios de Hola que tienen derechos de administrador local en un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="8cd8c-122">Los usuarios agregados aquí se agregan toohello *administradores de dispositivos* rol en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="8cd8c-123">De forma predeterminada, a los administradores globales de Azure AD y a los propietarios de dispositivos se les conceden derechos de administrador local.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="8cd8c-124">Esta opción es una capacidad de edición premium disponible a través de productos como Azure AD Premium o hello Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="8cd8c-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="8cd8c-125">**Los usuarios pueden registrar sus dispositivos con Azure AD** -necesita tooconfigure esta toobe de dispositivos de tooallow de configuración registrada con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="8cd8c-126">Si selecciona **ninguno**, no se admiten los dispositivos tooregister cuando no estén Unido de Azure AD ni híbrida unido Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="8cd8c-127">La inscripción en Microsoft Intune o Administración de dispositivos móviles (MDM) para Office 365 exige registrarse.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="8cd8c-128">Si ha configurado alguno de estos servicios, se selecciona **TODOS** y **NINGUNO** no está disponible.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="8cd8c-129">**Requiere que los dispositivos de la autenticación multifactor toojoin** -puede elegir si los usuarios son tooprovide necesaria una segunda autenticación factor toojoin su tooAzure dispositivo AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="8cd8c-130">valor predeterminado de Hello es **No**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-130">hello default is **No**.</span></span> <span data-ttu-id="8cd8c-131">Se recomienda exigir Multi-Factor Authentication al registrar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="8cd8c-132">Antes de habilitar la autenticación multifactor para este servicio, debe asegurarse de que la autenticación multifactor está configurada para usuarios de Hola que registren sus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="8cd8c-133">Para más información sobre los distintos servicios de Azure Multi-Factor Authentication, vea [Introducción a Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8cd8c-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="8cd8c-134">**Número máximo de dispositivos** -esta opción le permite el número máximo de hello tooselect de dispositivos que puede tener un usuario en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="8cd8c-135">Si un usuario alcanza esta cuota, que éstos no estén tooadd capaz de más dispositivos hasta que uno o varios de los dispositivos existentes Hola se quitan.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="8cd8c-136">oferta de dispositivo de Hola se cuenta para todos los dispositivos de Azure AD Unido o Azure AD registrado hoy en día.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="8cd8c-137">es el valor predeterminado de Hello **20**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-137">hello default value is **20**.</span></span>

- <span data-ttu-id="8cd8c-138">**Los usuarios pueden sincronizar la configuración y los datos de aplicación en todos los dispositivos** : de forma predeterminada, esta opción se establece demasiado**NONE**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="8cd8c-139">Selección de usuarios específicos o grupos o todos permite configuración del usuario de Hola y toosync de datos de aplicación a través de sus dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="8cd8c-140">Más información sobre cómo funciona la sincronización en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="8cd8c-141">Esta opción es una capacidad de premium disponible a través de productos como Azure AD Premium o hello Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="8cd8c-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Administración de un dispositivo de Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="8cd8c-143">Búsqueda de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8cd8c-143">Locate devices</span></span>

<span data-ttu-id="8cd8c-144">Como administrador, Hola portal de Azure, tienes dos opciones toolocate registró y unió dispositivos:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="8cd8c-145">**Todos los dispositivos** en hello **administrar** sección de hello **dispositivos** hoja</span><span class="sxs-lookup"><span data-stu-id="8cd8c-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Todos los dispositivos](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="8cd8c-147">**Dispositivos** en hello **administrar** sección de un **usuario** hoja</span><span class="sxs-lookup"><span data-stu-id="8cd8c-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Todos los dispositivos](./media/device-management-azure-portal/43.png)



<span data-ttu-id="8cd8c-149">Con ambas opciones, puede obtener vista tooa:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="8cd8c-150">Le permite toosearch para dispositivos con nombre para mostrar hello como filtro.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="8cd8c-151">Proporciona información general detallada de los dispositivos registrados y unidos.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="8cd8c-152">Le permite tooperform tareas comunes de la administración de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8cd8c-152">Enables you tooperform common device management tasks</span></span>
   

![Todos los dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="8cd8c-154">Tareas de administración de dispositivos</span><span class="sxs-lookup"><span data-stu-id="8cd8c-154">Device management tasks</span></span>

<span data-ttu-id="8cd8c-155">Como administrador, puede administrar Hola registrado o dispositivos Unidos a un.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="8cd8c-156">En esta sección se proporciona información sobre las tareas comunes de administración de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="8cd8c-157">**Administrar un dispositivo de Intune**: si es administrador de Intune, puede administrar los dispositivos marcados como **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="8cd8c-158">Un administrador puede ver dispositivos adicionales</span><span class="sxs-lookup"><span data-stu-id="8cd8c-158">An administrator can see additional device</span></span> 

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="8cd8c-160">**Habilitar o deshabilitar un dispositivo de Azure AD**</span><span class="sxs-lookup"><span data-stu-id="8cd8c-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="8cd8c-161">tooenable o deshabilitar un dispositivo, deberá toobe un administrador global en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="8cd8c-162">Al deshabilitar un dispositivo se evita que acceda a los recursos de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="8cd8c-163">dispositivo de hello toodisable, puede hacer clic en *...*</span><span class="sxs-lookup"><span data-stu-id="8cd8c-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="8cd8c-164">Haga clic en el dispositivo de Hola para obtener más detalles.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-164">click hello device for additional details.</span></span>

 
![Administración de un dispositivo de Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="8cd8c-166">Al deshabilitar un dispositivo cambia el estado de Hola Hola **habilitado** columna demasiado**No**.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Deshabilitación de un dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="8cd8c-168">**Eliminar un dispositivo de Azure AD** -toodelete un dispositivo, deberá toobe un administrador global de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="8cd8c-169">La eliminación de un dispositivo:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-169">Deleting a device:</span></span>
 
- <span data-ttu-id="8cd8c-170">Evita que un dispositivo acceda a los recursos de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8cd8c-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="8cd8c-171">Quita todos los detalles que se adjunta toohello dispositivo, por ejemplo, las claves de BitLocker para dispositivos Windows</span><span class="sxs-lookup"><span data-stu-id="8cd8c-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="8cd8c-172">Representa una actividad no recuperable y no se recomienda a menos que sea necesaria</span><span class="sxs-lookup"><span data-stu-id="8cd8c-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="8cd8c-173">Si un dispositivo está administrado por otra entidad de administración (por ejemplo, Microsoft Intune), asegúrese de que dicho dispositivo Hola se ha borrado / retirado antes de eliminar el dispositivo de hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="8cd8c-174">Puede seleccionar "..."</span><span class="sxs-lookup"><span data-stu-id="8cd8c-174">You can either select “…”</span></span> <span data-ttu-id="8cd8c-175">dispositivo de hello toodelete o haga clic en el dispositivo de Hola para obtener más detalles</span><span class="sxs-lookup"><span data-stu-id="8cd8c-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Eliminar un dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="8cd8c-177">**Ver o copiar el Id. de dispositivo** : puede usar un detalles del Id. de dispositivo de dispositivo ID tooverify Hola de dispositivo de Hola o con PowerShell durante la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="8cd8c-178">tooaccess Hola copia opción, haga clic en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-178">tooaccess hello copy option, click hello device.</span></span>

![Visualización de identificador de dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="8cd8c-180">**Ver o copiar las claves de BitLocker** -si eres un administrador, puede ver y Hola copia BitLocker claves toohelp toorecover de los usuarios de su unidad cifrada.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="8cd8c-181">Estas claves solo están disponibles para dispositivos Windows cifrados y con las claves almacenadas en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="8cd8c-182">Puede copiar estas claves al tener acceso a los detalles del dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Visualización de claves de BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="8cd8c-184">Registros de auditoría</span><span class="sxs-lookup"><span data-stu-id="8cd8c-184">Audit logs</span></span>


<span data-ttu-id="8cd8c-185">Hola dispositivo actividades están disponibles a través de los registros de actividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="8cd8c-186">Esto incluye actividades desencadenadas por el servicio de registro de dispositivo de Hola o por el usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="8cd8c-187">Creación de dispositivos y agregar propietarios o los usuarios en el dispositivo de Hola</span><span class="sxs-lookup"><span data-stu-id="8cd8c-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="8cd8c-188">Cambia la configuración de toodevice</span><span class="sxs-lookup"><span data-stu-id="8cd8c-188">Changes toodevice settings</span></span>

- <span data-ttu-id="8cd8c-189">Operaciones de dispositivo como eliminar o actualizar un dispositivo</span><span class="sxs-lookup"><span data-stu-id="8cd8c-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="8cd8c-190">Es el toohello de punto de entrada, datos de auditoría **registros de auditoría** en hello **actividad** sección de hello **dispositivos* hoja.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Registros de auditoría](./media/device-management-azure-portal/61.png)


<span data-ttu-id="8cd8c-192">Un registro de auditoría tiene una vista de lista predeterminada que muestra:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="8cd8c-193">Hola fecha y hora de aparición de Hola</span><span class="sxs-lookup"><span data-stu-id="8cd8c-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="8cd8c-194">destinos de Hola</span><span class="sxs-lookup"><span data-stu-id="8cd8c-194">hello targets</span></span>

- <span data-ttu-id="8cd8c-195">Hola iniciador / actor (que) de una actividad</span><span class="sxs-lookup"><span data-stu-id="8cd8c-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="8cd8c-196">actividad de Hello (¿qué)</span><span class="sxs-lookup"><span data-stu-id="8cd8c-196">hello activity (what)</span></span>

![Registros de auditoría](./media/device-management-azure-portal/63.png)

<span data-ttu-id="8cd8c-198">Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Registros de auditoría](./media/device-management-azure-portal/64.png)


<span data-ttu-id="8cd8c-200">toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de auditoría de hello mediante Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="8cd8c-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="8cd8c-201">Categoría</span><span class="sxs-lookup"><span data-stu-id="8cd8c-201">Catergory</span></span>
- <span data-ttu-id="8cd8c-202">Tipo de recurso de actividad</span><span class="sxs-lookup"><span data-stu-id="8cd8c-202">Activity resource type</span></span>
- <span data-ttu-id="8cd8c-203">Actividad</span><span class="sxs-lookup"><span data-stu-id="8cd8c-203">Activity</span></span>
- <span data-ttu-id="8cd8c-204">Intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="8cd8c-204">Date range</span></span>
- <span data-ttu-id="8cd8c-205">Destino</span><span class="sxs-lookup"><span data-stu-id="8cd8c-205">Target</span></span>
- <span data-ttu-id="8cd8c-206">Iniciado por (actor)</span><span class="sxs-lookup"><span data-stu-id="8cd8c-206">Initiated By (Actor)</span></span>

<span data-ttu-id="8cd8c-207">Además toohello filtros, puede buscar entradas específicas.</span><span class="sxs-lookup"><span data-stu-id="8cd8c-207">In addition toohello filters, you can search for specific entries.</span></span>

![Registros de auditoría](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="8cd8c-209">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8cd8c-209">Next steps</span></span>

* [<span data-ttu-id="8cd8c-210">Administración de toodevice de introducción en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8cd8c-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



