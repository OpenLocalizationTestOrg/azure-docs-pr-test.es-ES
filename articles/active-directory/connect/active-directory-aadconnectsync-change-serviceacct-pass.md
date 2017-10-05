---
title: "Sincronización de Azure AD Connect: cambio de la cuenta del servicio de sincronización de Azure AD Connect | Microsoft Docs"
description: "En este documento del tema se describe la clave de cifrado y cómo abandonarla una vez cambiada la contraseña."
services: active-directory
keywords: "Cuenta del servicio Sincronización de Azure AD, contraseña"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: bf6234d0810f870909957ee1c1e33c225a4922b9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="changing-the-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="891c4-104">Cambio de la contraseña de la cuenta del servicio de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="891c4-104">Changing the Azure AD Connect sync service account password</span></span>
<span data-ttu-id="891c4-105">Si cambia la contraseña de la cuenta del servicio de sincronización de Azure AD Connect, el servicio de sincronización no podrá iniciarse correctamente hasta que haya abandonado la clave de cifrado y reinicializado la contraseña de la cuenta del servicio de sincronización de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="891c4-105">If you change the  Azure AD Connect sync service account password, the Synchronization Service will not be able start correctly until you have abandoned the encryption key and reinitialized the Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="891c4-106">Azure AD Connect, como parte de los servicios de sincronización usa una clave de cifrado para almacenar las contraseñas de las cuentas de los servicios AD DS y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="891c4-106">Azure AD Connect, as part of the Synchronization Services uses an encryption key to store the passwords of the AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="891c4-107">Estas cuentas se cifran antes de almacenarse en la base de datos.</span><span class="sxs-lookup"><span data-stu-id="891c4-107">These accounts are encrypted before they are stored in the database.</span></span> 

<span data-ttu-id="891c4-108">La clave de cifrado usada se protege mediante la [API de protección de datos de Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="891c4-108">The encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="891c4-109">Para proteger la clave de cifrado, DPAPI usa la **contraseña de la cuenta del servicio de sincronización de Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="891c4-109">DPAPI protects the encryption key using the **password of the Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="891c4-110">Si tiene que cambiar la contraseña de la cuenta del servicio, puede seguir para ello los procedimientos descritos en [Abandonar la clave de cifrado de sincronización de Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key).</span><span class="sxs-lookup"><span data-stu-id="891c4-110">If you need to change the service account password you can use the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) to accomplish this.</span></span>  <span data-ttu-id="891c4-111">También debe seguir estos procedimientos si por algún motivo tiene que abandonar la clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="891c4-111">These procedures should also be used if you need to abandon the encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-the-password"></a><span data-ttu-id="891c4-112">Problemas que surgen al cambiar la contraseña</span><span class="sxs-lookup"><span data-stu-id="891c4-112">Issues that arise from changing the password</span></span>
<span data-ttu-id="891c4-113">Es preciso hacer dos cosas al cambiar la contraseña de la cuenta del servicio.</span><span class="sxs-lookup"><span data-stu-id="891c4-113">There are two things that need to be done when you change the service account password.</span></span>

<span data-ttu-id="891c4-114">En primer lugar, tiene que cambiar la contraseña en el Administrador de control de servicios de Windows.</span><span class="sxs-lookup"><span data-stu-id="891c4-114">First, you need to change the password under the Windows Service Control Manager.</span></span>  <span data-ttu-id="891c4-115">Hasta que se solucione el problema, verá los siguientes errores:</span><span class="sxs-lookup"><span data-stu-id="891c4-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="891c4-116">Si intenta iniciar el servicio de sincronización en el Administrador de control de servicios de Windows, recibirá el error "**Windows no pudo iniciar el servicio Sincronización de Microsoft Azure AD en el equipo local**".</span><span class="sxs-lookup"><span data-stu-id="891c4-116">If you try to start the Synchronization Service in Windows Service Control Manager, you receive the error "**Windows could not start the Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="891c4-117">**Error 1069: No se puede iniciar el servicio debido a un error en el inicio de sesión.**"</span><span class="sxs-lookup"><span data-stu-id="891c4-117">**Error 1069: The service did not start due to a logon failure.**"</span></span>
- <span data-ttu-id="891c4-118">En el Visor de eventos de Windows, el registro de eventos del sistema contiene un error con **Id. de evento 7038** y el mensaje "**The ADSync service was unable to log on as with the currently configured password due to the following error (El servicio ADSync no puede iniciar sesión con la contraseña configurada actualmente debido al siguiente error): El nombre de usuario o la contraseña es incorrecto.**"</span><span class="sxs-lookup"><span data-stu-id="891c4-118">Under Windows Event Viewer, the system event log contains an error with **Event ID 7038** and message “**The ADSync service was unable to log on as with the currently configured password due to the following error: The user name or password is incorrect.**"</span></span>

<span data-ttu-id="891c4-119">En segundo lugar, en determinadas condiciones, si la contraseña se actualiza, el servicio de sincronización ya no podrá recuperar la clave de cifrado a través de DPAPI.</span><span class="sxs-lookup"><span data-stu-id="891c4-119">Second, under specific conditions, if the password is updated, the Synchronization Service can no longer retrieve the encryption key via DPAPI.</span></span> <span data-ttu-id="891c4-120">Sin la clave de cifrado, el servicio de sincronización no puede descifrar la contraseña necesaria para sincronizar con o desde AD y Azure AD locales.</span><span class="sxs-lookup"><span data-stu-id="891c4-120">Without the encryption key, the Synchronization Service cannot decrypt the passwords required to synchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="891c4-121">Verá errores como los siguientes:</span><span class="sxs-lookup"><span data-stu-id="891c4-121">You will see errors such as:</span></span>

- <span data-ttu-id="891c4-122">En el Administrador de control de servicios de Windows, si intenta iniciar el servicio de sincronización y este no puede recuperar la clave de cifrado, se produce el error “**Windows no pudo iniciar el servicio Sincronización de Microsoft Azure AD en el equipo local.</span><span class="sxs-lookup"><span data-stu-id="891c4-122">Under Windows Service Control Manager, if you try to start the Synchronization Service and it cannot retrieve the encryption key, it fails with error “**Windows could not start the Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="891c4-123">Para más información, revise el registro de eventos del sistema.</span><span class="sxs-lookup"><span data-stu-id="891c4-123">For more information, review the System Event log.</span></span> <span data-ttu-id="891c4-124">Si este no es un servicio de Microsoft, póngase en contacto con el proveedor del servicio y haga referencia al código de error específico del servicio **-21451857952****.”</span><span class="sxs-lookup"><span data-stu-id="891c4-124">If this is a non-Microsoft service, contact the service vendor, and refer to service-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="891c4-125">En el Visor de eventos de Windows, el registro de eventos de la aplicación contiene un error con **Id. de evento 6028** y el mensaje de error *“**The server encryption key cannot be accessed.* *(No se puede acceder a la clave de cifrado del servidor.)”*</span><span class="sxs-lookup"><span data-stu-id="891c4-125">Under Windows Event Viewer, the application event log contains an error with **Event ID 6028** and error message *“**The server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="891c4-126">Para asegurarse de que no recibe estos errores, siga los procedimientos descritos en [Abandonar la clave de cifrado de sincronización de Azure AD Connect](#abandoning-the-azure-ad-connect-sync-encryption-key) al cambiar la contraseña.</span><span class="sxs-lookup"><span data-stu-id="891c4-126">To ensure that you do not receive these errors, follow the procedures in [Abandoning the Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing the password.</span></span>
 
## <a name="abandoning-the-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="891c4-127">Abandonar la clave de cifrado de sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="891c4-127">Abandoning the Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="891c4-128">Los procedimientos siguientes solo se aplican a Azure AD Connect compilación 1.1.443.0 o anterior.</span><span class="sxs-lookup"><span data-stu-id="891c4-128">The following procedures only apply to Azure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="891c4-129">Use los procedimientos siguientes para abandonar la clave de cifrado.</span><span class="sxs-lookup"><span data-stu-id="891c4-129">Use the following procedures to abandon the encryption key.</span></span>

### <a name="what-to-do-if-you-need-to-abandon-the-encryption-key"></a><span data-ttu-id="891c4-130">Qué hacer si tiene que abandonar la clave de cifrado</span><span class="sxs-lookup"><span data-stu-id="891c4-130">What to do if you need to abandon the encryption key</span></span>

<span data-ttu-id="891c4-131">Si tiene que abandonar la clave de cifrado, use para ello los procedimientos siguientes.</span><span class="sxs-lookup"><span data-stu-id="891c4-131">If you need to abandon the encryption key, use the following procedures to accomplish this.</span></span>

1. [<span data-ttu-id="891c4-132">Abandonar la clave de cifrado existente</span><span class="sxs-lookup"><span data-stu-id="891c4-132">Abandon the existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="891c4-133">Especificar la contraseña de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="891c4-133">Provide the password of the AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="891c4-134">Reinicializar la contraseña de la cuenta de Sincronización de Azure AD</span><span class="sxs-lookup"><span data-stu-id="891c4-134">Reinitialize the password of the Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="891c4-135">Iniciar el servicio de sincronización</span><span class="sxs-lookup"><span data-stu-id="891c4-135">Start the Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-the-existing-encryption-key"></a><span data-ttu-id="891c4-136">Abandonar la clave de cifrado existente</span><span class="sxs-lookup"><span data-stu-id="891c4-136">Abandon the existing encryption key</span></span>
<span data-ttu-id="891c4-137">Abandone la clave de cifrado existente para poder crear otra clave de cifrado:</span><span class="sxs-lookup"><span data-stu-id="891c4-137">Abandon the existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="891c4-138">Inicie sesión como administrador en el servidor de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="891c4-138">Log in to your Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="891c4-139">Inicie una nueva sesión de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="891c4-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="891c4-140">Acceda a la carpeta: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="891c4-140">Navigate to folder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="891c4-141">Ejecute el comando: `./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="891c4-141">Run the command: `./miiskmu.exe /a`</span></span>

![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-the-password-of-the-ad-ds-account"></a><span data-ttu-id="891c4-143">Especificar la contraseña de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="891c4-143">Provide the password of the AD DS account</span></span>
<span data-ttu-id="891c4-144">Cuando las contraseñas existentes almacenadas en la base de datos ya no se pueden descifrar, tiene que proporcionar el servicio de sincronización con la contraseña de la cuenta de AD DS.</span><span class="sxs-lookup"><span data-stu-id="891c4-144">As the existing passwords stored inside the database can no longer be decrypted, you need to provide the Synchronization Service with the password of the AD DS account.</span></span> <span data-ttu-id="891c4-145">El servicio de sincronización cifra las contraseñas con la nueva clave de cifrado:</span><span class="sxs-lookup"><span data-stu-id="891c4-145">The Synchronization Service encrypts the passwords using the new encryption key:</span></span>

1. <span data-ttu-id="891c4-146">Inicie el Synchronization Service Manager (INICIO → Servicio de sincronización).</span><span class="sxs-lookup"><span data-stu-id="891c4-146">Start the Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="891c4-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="891c4-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="891c4-148">Vaya a la pestaña **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="891c4-148">Go to the **Connectors** tab.</span></span>
3. <span data-ttu-id="891c4-149">Seleccione el **AD Connector** (conector de AD) que corresponda a su AD local.</span><span class="sxs-lookup"><span data-stu-id="891c4-149">Select the **AD Connector** that corresponds to your on-premises AD.</span></span> <span data-ttu-id="891c4-150">Si tiene más de un conector de AD, repita los pasos siguientes para cada uno de ellos.</span><span class="sxs-lookup"><span data-stu-id="891c4-150">If you have more than one AD connector, repeat the following steps for each of them.</span></span>
4. <span data-ttu-id="891c4-151">En **Acciones**, seleccione **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="891c4-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="891c4-152">En el cuadro de diálogo emergente, seleccione **Connect to Active Directory Forest** (Conectarse al bosque de Active Directory):</span><span class="sxs-lookup"><span data-stu-id="891c4-152">In the pop-up dialog, select **Connect to Active Directory Forest**:</span></span>
6. <span data-ttu-id="891c4-153">Escriba la contraseña de la cuenta de AD DS en el cuadro de texto **Contraseña**.</span><span class="sxs-lookup"><span data-stu-id="891c4-153">Enter the password of the AD DS account in the **Password** textbox.</span></span> <span data-ttu-id="891c4-154">Si no conoce la contraseña, debe establecerla en un valor conocido antes de realizar este paso.</span><span class="sxs-lookup"><span data-stu-id="891c4-154">If you do not know its password, you must set it to a known value before performing this step.</span></span>
7. <span data-ttu-id="891c4-155">Haga en **Aceptar** para guardar la nueva contraseña y cerrar el cuadro de diálogo emergente.</span><span class="sxs-lookup"><span data-stu-id="891c4-155">Click **OK** to save the new password and close the pop-up dialog.</span></span>
<span data-ttu-id="891c4-156">![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="891c4-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-the-password-of-the-azure-ad-sync-account"></a><span data-ttu-id="891c4-157">Reinicializar la contraseña de la cuenta de Sincronización de Azure AD</span><span class="sxs-lookup"><span data-stu-id="891c4-157">Reinitialize the password of the Azure AD sync account</span></span>
<span data-ttu-id="891c4-158">No se puede especificar directamente la contraseña de la cuenta del servicio Azure AD en el servicio de sincronización.</span><span class="sxs-lookup"><span data-stu-id="891c4-158">You cannot directly provide the password of the Azure AD service account to the Synchronization Service.</span></span> <span data-ttu-id="891c4-159">En su lugar, tendrá que usar el cmdlet **Add-ADSyncAADServiceAccount** para reinicializar la cuenta del servicio Azure AD.</span><span class="sxs-lookup"><span data-stu-id="891c4-159">Instead, you need to use the cmdlet **Add-ADSyncAADServiceAccount** to reinitialize the Azure AD service account.</span></span> <span data-ttu-id="891c4-160">El cmdlet restablece la contraseña de la cuenta y la pone a disposición de servicio de sincronización:</span><span class="sxs-lookup"><span data-stu-id="891c4-160">The cmdlet resets the account password and makes it available to the Synchronization Service:</span></span>

1. <span data-ttu-id="891c4-161">Inicie una nueva sesión de PowerShell en el servidor de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="891c4-161">Start a new PowerShell session on the Azure AD Connect server.</span></span>
2. <span data-ttu-id="891c4-162">Ejecute el cmdlet `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="891c4-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="891c4-163">En el cuadro de diálogo emergente, especifique las credenciales de administrador global de Azure AD para el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="891c4-163">In the pop-up dialog, provide the Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="891c4-164">![Utilidad de clave de cifrado de sincronización de Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="891c4-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="891c4-165">Si se realiza correctamente, verá el símbolo del sistema de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="891c4-165">If it is successful, you will see the PowerShell command prompt.</span></span>

#### <a name="start-the-synchronization-service"></a><span data-ttu-id="891c4-166">Iniciar el servicio de sincronización</span><span class="sxs-lookup"><span data-stu-id="891c4-166">Start the Synchronization Service</span></span>
<span data-ttu-id="891c4-167">Ahora que el servicio de sincronización tiene acceso a la clave de cifrado y a todas las contraseñas que necesita, puede reiniciar el servicio en el Administrador de control de servicios de Windows:</span><span class="sxs-lookup"><span data-stu-id="891c4-167">Now that the Synchronization Service has access to the encryption key and all the passwords it needs, you can restart the service in the Windows Service Control Manager:</span></span>


1. <span data-ttu-id="891c4-168">Vaya a Administrador de control de servicios de Windows (INICIO → Servicios).</span><span class="sxs-lookup"><span data-stu-id="891c4-168">Go to Windows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="891c4-169">Seleccione **Sincronización de Microsoft Azure AD** y haga clic en Reiniciar.</span><span class="sxs-lookup"><span data-stu-id="891c4-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="891c4-170">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="891c4-170">Next steps</span></span>
<span data-ttu-id="891c4-171">**Temas de introducción**</span><span class="sxs-lookup"><span data-stu-id="891c4-171">**Overview topics**</span></span>

* [<span data-ttu-id="891c4-172">Sincronización de Azure AD Connect: comprender y personalizar la sincronización</span><span class="sxs-lookup"><span data-stu-id="891c4-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="891c4-173">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="891c4-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
