---
title: "Solución de problemas de la implementación de la sincronización de contraseña con la sincronización de Azure AD Connect | Microsoft Docs"
description: "En este artículo se ofrece información sobre cómo solucionar problemas de sincronización de contraseñas."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="49222-103">Solución de problemas de la implementación de la sincronización de contraseña con la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="49222-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="49222-104">En este tema se proporcionan los pasos para solucionar problemas relacionados con la sincronización de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="49222-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="49222-105">Si las contraseñas no se sincronizan como se esperaba, puede ser para un subconjunto de usuarios o para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="49222-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="49222-106">Para la implementación de Azure Active Directory (Azure AD) Connect con la versión 1.1.524.0 o una posterior, ahora hay un cmdlet de diagnóstico que puede usar para solucionar problemas de sincronización de contraseña:</span><span class="sxs-lookup"><span data-stu-id="49222-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="49222-107">Si tiene un problema con contraseñas que no se sincronizan, consulte la sección [No se sincronizan las contraseñas: solución de problemas mediante el cmdlet de diagnóstico](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="49222-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="49222-108">Si tiene un problema con objetos individuales, consulte la sección [Un objeto no sincroniza contraseñas: solución de problemas mediante el cmdlet de diagnóstico](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="49222-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="49222-109">Para versiones anteriores de la implementación de Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="49222-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="49222-110">Si tiene un problema con contraseñas que no se sincronizan, consulte la sección [No se sincronizan las contraseñas: pasos para la solución manual de problemas](#no-passwords-are-synchronized-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="49222-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="49222-111">Si tiene un problema con objetos individuales, consulte la sección [Un objeto no sincroniza contraseñas: pasos para la solución manual de problemas](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="49222-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="49222-112">No se sincronizan las contraseñas: solución de problemas mediante el cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="49222-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="49222-113">Puede usar el cmdlet `Invoke-ADSyncDiagnostics` para averiguar por qué no se sincronizan las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="49222-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="49222-114">El cmdlet `Invoke-ADSyncDiagnostics` solo está disponible para Azure AD Connect versión 1.1.524.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="49222-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="49222-115">Ejecución del cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="49222-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="49222-116">Para solucionar problemas cuando no se sincronizan las contraseñas:</span><span class="sxs-lookup"><span data-stu-id="49222-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="49222-117">Abra una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect mediante la opción **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="49222-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="49222-118">Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="49222-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="49222-119">Ejecute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="49222-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="49222-120">Ejecute `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="49222-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="49222-121">Descripción de los resultados del cmdlet</span><span class="sxs-lookup"><span data-stu-id="49222-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="49222-122">El cmdlet de diagnóstico realiza las siguientes comprobaciones:</span><span class="sxs-lookup"><span data-stu-id="49222-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="49222-123">Valida que la característica de sincronización de contraseña está habilitada para el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="49222-124">Valida que el servidor de Azure AD Connect no está en modo de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="49222-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="49222-125">Para cada conector Active Directory local (que corresponde a un bosque existente de Active Directory):</span><span class="sxs-lookup"><span data-stu-id="49222-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="49222-126">Valida que la característica de sincronización de contraseña está habilitada.</span><span class="sxs-lookup"><span data-stu-id="49222-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="49222-127">Buscas eventos de latido de sincronización de contraseña en los registros de eventos de aplicación Windows.</span><span class="sxs-lookup"><span data-stu-id="49222-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="49222-128">Para cada dominio de Active Directory en el conector Active Directory local:</span><span class="sxs-lookup"><span data-stu-id="49222-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="49222-129">Valida que el dominio sea accesible desde el servidor de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="49222-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="49222-130">Valida que las cuentas de Active Directory Domain Services (AD DS) que usa el conector Active Directory local tienen el nombre de usuario correcto, la contraseña y los permisos necesarios para la sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="49222-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="49222-131">El siguiente diagrama muestra los resultados del cmdlet para una topología de Active Directory local de un solo dominio:</span><span class="sxs-lookup"><span data-stu-id="49222-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Salida de diagnóstico de la sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="49222-133">En el resto de esta sección se describen los resultados concretos que devuelve el cmdlet y los correspondientes problemas.</span><span class="sxs-lookup"><span data-stu-id="49222-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="49222-134">La característica de sincronización de contraseña no está habilitada</span><span class="sxs-lookup"><span data-stu-id="49222-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="49222-135">Si no ha habilitado la sincronización de contraseña mediante el asistente de Azure AD Connect, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![La sincronización de contraseña no está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="49222-137">El servidor de Azure AD Connect está en modo de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="49222-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="49222-138">Si el servidor de Azure AD Connect está en modo de almacenamiento provisional, la sincronización de contraseña está deshabilitada temporalmente y se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![El servidor de Azure AD Connect está en modo de almacenamiento provisional](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="49222-140">No hay eventos de latido de sincronización de contraseña</span><span class="sxs-lookup"><span data-stu-id="49222-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="49222-141">Cada conector Active Directory local tiene su propio canal de sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="49222-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="49222-142">Cuando se establece el canal de sincronización de contraseña y no hay cambios de contraseña que sincronizar, se genera un evento de latido (Id. de evento 654) una vez cada 30 minutos en el registro de eventos de aplicación Windows.</span><span class="sxs-lookup"><span data-stu-id="49222-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="49222-143">Para cada conector Active Directory local, el cmdlet busca los correspondientes eventos de latido de las últimas tres horas.</span><span class="sxs-lookup"><span data-stu-id="49222-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="49222-144">Si no se encuentra ningún evento de latido, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-144">If no heartbeat event is found, the following error is returned:</span></span>

![No hay ningún evento de latido de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="49222-146">La cuenta de AD DS no tiene los permisos correctos</span><span class="sxs-lookup"><span data-stu-id="49222-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="49222-147">Si la cuenta de AD DS que usa el conector Active Directory local para sincronizar los hash de contraseña no tiene los permisos adecuados, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="49222-149">Nombre de usuario o contraseña incorrectos de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="49222-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="49222-150">Si la cuenta de AD DS que usa el conector Active Directory local para sincronizar los hash de contraseña tiene un nombre de usuario o una contraseña incorrectos, se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="49222-152">Un objeto no sincroniza contraseñas: solución de problemas mediante el cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="49222-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="49222-153">Puede usar el cmdlet `Invoke-ADSyncDiagnostics` para determinar por qué un objeto no sincroniza contraseñas.</span><span class="sxs-lookup"><span data-stu-id="49222-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="49222-154">El cmdlet `Invoke-ADSyncDiagnostics` solo está disponible para Azure AD Connect versión 1.1.524.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="49222-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="49222-155">Ejecución del cmdlet de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="49222-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="49222-156">Para solucionar problemas cuando no se sincronizan las contraseñas:</span><span class="sxs-lookup"><span data-stu-id="49222-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="49222-157">Abra una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect mediante la opción **Ejecutar como administrador**.</span><span class="sxs-lookup"><span data-stu-id="49222-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="49222-158">Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="49222-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="49222-159">Ejecute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="49222-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="49222-160">Ejecute el siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="49222-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="49222-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="49222-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="49222-162">Descripción de los resultados del cmdlet</span><span class="sxs-lookup"><span data-stu-id="49222-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="49222-163">El cmdlet de diagnóstico realiza las siguientes comprobaciones:</span><span class="sxs-lookup"><span data-stu-id="49222-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="49222-164">Examina el estado del objeto de Active Directory en el espacio conector Active Directory, el metaverso y el espacio conector Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="49222-165">Valida que hay reglas de sincronización con la sincronización de contraseña habilitada y se aplican al objeto de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49222-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="49222-166">Intenta recuperar y mostrar los resultados del último intento de sincronización de la contraseña del objeto.</span><span class="sxs-lookup"><span data-stu-id="49222-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="49222-167">El diagrama siguiente muestra los resultados del cmdlet al solucionar problemas de sincronización de contraseña de un solo objeto:</span><span class="sxs-lookup"><span data-stu-id="49222-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Salida de diagnóstico de la sincronización de contraseña: un solo objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="49222-169">En el resto de esta sección se describen los resultados concretos que devuelve el cmdlet y los correspondientes problemas.</span><span class="sxs-lookup"><span data-stu-id="49222-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="49222-170">El objeto de Active Directory no se ha exportado a Azure AD</span><span class="sxs-lookup"><span data-stu-id="49222-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="49222-171">La sincronización de contraseña para esta cuenta de Active Directory local no se realiza porque no hay un objeto correspondiente en el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="49222-172">Se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-172">The following error is returned:</span></span>

![Falta objeto de Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="49222-174">El usuario tiene una contraseña incorrecta</span><span class="sxs-lookup"><span data-stu-id="49222-174">User has a temporary password</span></span>
<span data-ttu-id="49222-175">Actualmente, Azure AD Connect no admite la sincronización de contraseñas temporales con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="49222-176">Una contraseña se considera temporal si la opción **Change password at next logon** (Cambiar la contraseña en el siguiente inicio de sesión) se establece como activada en el usuario de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="49222-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="49222-177">Se devuelve el error siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-177">The following error is returned:</span></span>

![La contraseña temporal no se exporta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="49222-179">No hay resultados del último intento de sincronización de contraseña disponibles</span><span class="sxs-lookup"><span data-stu-id="49222-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="49222-180">De manera predeterminada, Azure AD Connect almacena los resultados de los intentos de sincronización de contraseña durante siete días.</span><span class="sxs-lookup"><span data-stu-id="49222-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="49222-181">Si no hay ningún resultado disponible para el objeto de Active Directory seleccionado, se devuelve la advertencia siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Salida de diagnóstico de un solo objeto: no hay historial de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="49222-183">No se sincronizan las contraseñas: pasos para la solución manual de problemas</span><span class="sxs-lookup"><span data-stu-id="49222-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="49222-184">Siga estos pasos para determinar por qué no se sincronizan las contraseñas:</span><span class="sxs-lookup"><span data-stu-id="49222-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="49222-185">¿Está el servidor de Connect en [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="49222-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="49222-186">Un servidor en modo de almacenamiento provisional no sincroniza contraseñas.</span><span class="sxs-lookup"><span data-stu-id="49222-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="49222-187">Ejecute el script de la sección [Obtención del estado de configuración de sincronización de contraseñas](#get-the-status-of-password-sync-settings).</span><span class="sxs-lookup"><span data-stu-id="49222-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="49222-188">Le ofrece una visión general de la configuración de sincronización de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="49222-188">It gives you an overview of the password sync configuration.</span></span>  

    ![Salida del script de PowerShell de la configuración de sincronización de contraseñas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="49222-190">Si la característica no está habilitada en Azure AD o si el estado del canal de sincronización no está habilitado, ejecute el Asistente para instalación de Connect.</span><span class="sxs-lookup"><span data-stu-id="49222-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="49222-191">Seleccione **Personalizar las opciones de sincronización** y anule la selección de sincronización de contraseñas. Este cambio deshabilita temporalmente la característica.</span><span class="sxs-lookup"><span data-stu-id="49222-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="49222-192">Después, vuelva a ejecutar al asistente y habilite de nuevo la sincronización de contraseñas. Vuelva a ejecutar el script para comprobar que la configuración es correcta.</span><span class="sxs-lookup"><span data-stu-id="49222-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="49222-193">Busque errores en el registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="49222-193">Look in the event log for errors.</span></span> <span data-ttu-id="49222-194">Busque los siguientes eventos, que podrían indicar un problema:</span><span class="sxs-lookup"><span data-stu-id="49222-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="49222-195">Origen: "Sincronización de directorios" ID: 0, 611, 652, 655. Si ve estos eventos, significa que hay un problema de conectividad.</span><span class="sxs-lookup"><span data-stu-id="49222-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="49222-196">El mensaje de registro de eventos contiene información de bosques en los que hay un problema.</span><span class="sxs-lookup"><span data-stu-id="49222-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="49222-197">Para más información, vea [Problemas de conectividad](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="49222-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="49222-198">Si no ve ningún latido o si nada funciona, ejecute [Desencadenamiento de una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="49222-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="49222-199">Ejecute el script una sola vez.</span><span class="sxs-lookup"><span data-stu-id="49222-199">Run the script only once.</span></span>

6. <span data-ttu-id="49222-200">Vea la sección [Solución de problemas de un objeto que no sincroniza contraseñas](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="49222-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="49222-201">Problemas de conectividad</span><span class="sxs-lookup"><span data-stu-id="49222-201">Connectivity problems</span></span>

<span data-ttu-id="49222-202">¿Hay conectividad con Azure AD?</span><span class="sxs-lookup"><span data-stu-id="49222-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="49222-203">¿La cuenta tiene los permisos necesarios para leer los valores de hash de contraseña en todos los dominios?</span><span class="sxs-lookup"><span data-stu-id="49222-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="49222-204">Si instaló Connect con la configuración rápida, los permisos deben ser los correctos.</span><span class="sxs-lookup"><span data-stu-id="49222-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="49222-205">Si realizó una instalación personalizada, establezca los permisos manualmente haciendo lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="49222-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="49222-206">Para buscar la cuenta que usa el conector Active Directory, inicie **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="49222-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="49222-207">Vaya a **Conectores** y busque el bosque de Active Directory local cuyos problemas va a solucionar.</span><span class="sxs-lookup"><span data-stu-id="49222-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="49222-208">Seleccione el conector y haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="49222-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="49222-209">Vaya a **Conexión al bosque de Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="49222-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Cuenta que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="49222-211">Apunte el nombre de usuario y el dominio donde está la cuenta.</span><span class="sxs-lookup"><span data-stu-id="49222-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="49222-212">Inicie **Usuarios y equipos de Active Directory** y compruebe que la cuenta encontrada anteriormente tiene los permisos siguientes establecidos en la raíz de todos los dominios del bosque:</span><span class="sxs-lookup"><span data-stu-id="49222-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="49222-213">Replicación de cambios de directorio</span><span class="sxs-lookup"><span data-stu-id="49222-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="49222-214">Replicación de todos los cambios de directorio</span><span class="sxs-lookup"><span data-stu-id="49222-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="49222-215">¿Puede Azure AD Connect acceder a los controladores de dominio?</span><span class="sxs-lookup"><span data-stu-id="49222-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="49222-216">Si el servidor de Connect no puede conectarse a todos los controladores de dominio, configure **Only use preferred domain controller** (Usar solo el controlador de dominio preferido).</span><span class="sxs-lookup"><span data-stu-id="49222-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controlador de dominio que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="49222-218">Vuelva a **Synchronization Service Manager** y **Configure Directory Partition** (Configurar partición de directorio).</span><span class="sxs-lookup"><span data-stu-id="49222-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="49222-219">Seleccione el dominio en **Seleccionar particiones de directorio**, active la casilla **Only use preferred domain controller** (Usar solo el controlador de dominio preferido) y haga clic en **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="49222-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="49222-220">En la lista, escriba los controladores de dominio que Connect debe usar para realizar la sincronización de contraseñas. También se usa la misma lista para los procesos de importación y exportación.</span><span class="sxs-lookup"><span data-stu-id="49222-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="49222-221">Siga estos pasos con todos los dominios.</span><span class="sxs-lookup"><span data-stu-id="49222-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="49222-222">Si el script muestra que no hay ningún latido, ejecute el script de [Desencadenamiento de una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="49222-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="49222-223">Un objeto no sincroniza contraseñas: pasos para la solución manual de problemas</span><span class="sxs-lookup"><span data-stu-id="49222-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="49222-224">Puede solucionar fácilmente los problemas relacionados con la sincronización de contraseñas si revisa el estado actual de un objeto.</span><span class="sxs-lookup"><span data-stu-id="49222-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="49222-225">En **Usuarios y equipos de Active Directory**, busque el usuario y compruebe que la casilla **El usuario debe cambiar la contraseña en el siguiente inicio de sesión** está desactivada.</span><span class="sxs-lookup"><span data-stu-id="49222-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Contraseñas productivas de Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="49222-227">Si la casilla está activada, pida al usuario que inicie sesión y cambie la contraseña.</span><span class="sxs-lookup"><span data-stu-id="49222-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="49222-228">Las contraseñas temporales no se sincronizan con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="49222-229">Si la contraseña parece correcta en Active Directory, siga al usuario en el motor de sincronización.</span><span class="sxs-lookup"><span data-stu-id="49222-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="49222-230">Al seguir al usuario desde Active Directory local hasta Azure AD, puede ver si hay un error descriptivo en el objeto.</span><span class="sxs-lookup"><span data-stu-id="49222-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="49222-231">a.</span><span class="sxs-lookup"><span data-stu-id="49222-231">a.</span></span> <span data-ttu-id="49222-232">Inicie el [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="49222-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="49222-233">b.</span><span class="sxs-lookup"><span data-stu-id="49222-233">b.</span></span> <span data-ttu-id="49222-234">Haga clic en **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="49222-234">Click **Connectors**.</span></span>

    <span data-ttu-id="49222-235">c.</span><span class="sxs-lookup"><span data-stu-id="49222-235">c.</span></span> <span data-ttu-id="49222-236">Seleccione el **conector Active Directory** en el que se encuentra el usuario.</span><span class="sxs-lookup"><span data-stu-id="49222-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="49222-237">d.</span><span class="sxs-lookup"><span data-stu-id="49222-237">d.</span></span> <span data-ttu-id="49222-238">Seleccione **Search Connector Space**(Buscar espacio de conector).</span><span class="sxs-lookup"><span data-stu-id="49222-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="49222-239">e.</span><span class="sxs-lookup"><span data-stu-id="49222-239">e.</span></span> <span data-ttu-id="49222-240">En el cuadro **Ámbito**, seleccione **DN o delimitador** y escriba el DN completo del usuario cuyos problemas va a solucionar.</span><span class="sxs-lookup"><span data-stu-id="49222-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Búsqueda de usuario en el espacio conector con DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="49222-242">f.</span><span class="sxs-lookup"><span data-stu-id="49222-242">f.</span></span> <span data-ttu-id="49222-243">Busque el usuario y haga clic en **Propiedades** para ver todos los atributos.</span><span class="sxs-lookup"><span data-stu-id="49222-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="49222-244">Si el usuario no aparece en el resultado de búsqueda, compruebe las [reglas de filtrado](active-directory-aadconnectsync-configure-filtering.md) y asegúrese de ejecutar [Aplicación y comprobación de los cambios](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para que el usuario se muestre en Connect.</span><span class="sxs-lookup"><span data-stu-id="49222-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="49222-245">g.</span><span class="sxs-lookup"><span data-stu-id="49222-245">g.</span></span> <span data-ttu-id="49222-246">Para ver los detalles de la sincronización de contraseñas del objeto de la semana pasada, haga clic en **Registro**.</span><span class="sxs-lookup"><span data-stu-id="49222-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Detalles del registro de objetos](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="49222-248">Si el registro de objetos está vacío, Azure AD Connect no ha sido capaz de leer el valor de hash de contraseña de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="49222-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="49222-249">Continúe solucionando problemas con [Errores de conectividad](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="49222-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="49222-250">Si ve un valor distinto de **correcto**, consulte la tabla de [Registro de sincronización de contraseñas](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="49222-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="49222-251">h.</span><span class="sxs-lookup"><span data-stu-id="49222-251">h.</span></span> <span data-ttu-id="49222-252">Seleccione la pestaña **Linaje** y asegúrese de que al menos una de las reglas de sincronización de la columna **PasswordSync** está establecida en **True**.</span><span class="sxs-lookup"><span data-stu-id="49222-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="49222-253">En la configuración predeterminada, el nombre de la regla de sincronización es **In from AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="49222-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Información de linaje de un usuario](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="49222-255">i.</span><span class="sxs-lookup"><span data-stu-id="49222-255">i.</span></span> <span data-ttu-id="49222-256">Haga clic en **Metaverse Object Properties** (Propiedades del objeto de metaverso) para mostrar una lista de atributos de usuario.</span><span class="sxs-lookup"><span data-stu-id="49222-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="49222-258">Compruebe que no hay ningún atributo **cloudFiltered**.</span><span class="sxs-lookup"><span data-stu-id="49222-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="49222-259">Asegúrese de que los atributos de dominio (domainFQDN y domainNetBios) tienen los valores esperados.</span><span class="sxs-lookup"><span data-stu-id="49222-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="49222-260">j.</span><span class="sxs-lookup"><span data-stu-id="49222-260">j.</span></span> <span data-ttu-id="49222-261">Haga clic en la pestaña **Conectores**. Asegúrese de que ve conectores para Active Directory local y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="49222-263">k.</span><span class="sxs-lookup"><span data-stu-id="49222-263">k.</span></span> <span data-ttu-id="49222-264">Seleccione la fila que representa Azure AD, haga clic en **Propiedades** y luego, en la pestaña **Linaje**. El objeto del espacio conector debe tener una regla de salida con la columna **PasswordSync** establecida en **True**.</span><span class="sxs-lookup"><span data-stu-id="49222-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="49222-265">En la configuración predeterminada, el nombre de la regla de sincronización es **Out to AAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="49222-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Cuadro de diálogo de propiedades de objeto del espacio conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="49222-267">Registro de sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="49222-267">Password sync log</span></span>
<span data-ttu-id="49222-268">La columna de estado puede presentar los siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="49222-268">The status column can have the following values:</span></span>

| <span data-ttu-id="49222-269">Estado</span><span class="sxs-lookup"><span data-stu-id="49222-269">Status</span></span> | <span data-ttu-id="49222-270">Description</span><span class="sxs-lookup"><span data-stu-id="49222-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49222-271">Correcto</span><span class="sxs-lookup"><span data-stu-id="49222-271">Success</span></span> |<span data-ttu-id="49222-272">La contraseña se sincronizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="49222-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="49222-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="49222-273">FilteredByTarget</span></span> |<span data-ttu-id="49222-274">La contraseña se establece en **El usuario debe cambiar la contraseña en el siguiente inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="49222-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="49222-275">La contraseña no se ha sincronizado.</span><span class="sxs-lookup"><span data-stu-id="49222-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="49222-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="49222-276">NoTargetConnection</span></span> |<span data-ttu-id="49222-277">No hay ningún objeto en el metaverso o en el espacio del conector de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="49222-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="49222-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="49222-279">No se encontró ningún objeto en el espacio del conector de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="49222-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="49222-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="49222-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="49222-281">Aún no se exportó el objeto del espacio del conector de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49222-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="49222-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="49222-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="49222-283">La entrada de registro se creó antes de la versión 1.0.9125.0 y se muestra en su estado heredado.</span><span class="sxs-lookup"><span data-stu-id="49222-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="49222-284">Error</span><span class="sxs-lookup"><span data-stu-id="49222-284">Error</span></span> |<span data-ttu-id="49222-285">El servicio devolvió un error desconocido.</span><span class="sxs-lookup"><span data-stu-id="49222-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="49222-286">Desconocido</span><span class="sxs-lookup"><span data-stu-id="49222-286">Unknown</span></span> |<span data-ttu-id="49222-287">Ha habido un error al intentar procesar un lote de valores hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="49222-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="49222-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="49222-288">MissingAttribute</span></span> |<span data-ttu-id="49222-289">Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="49222-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="49222-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="49222-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="49222-291">Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no estaban disponibles anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49222-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="49222-292">Se intenta volver a sincronizar el valor hash de contraseña del usuario.</span><span class="sxs-lookup"><span data-stu-id="49222-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="49222-293">Scripts para ayudar a solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="49222-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="49222-294">Obtención del estado de configuración de sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="49222-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="49222-295">Desencadenamiento de una sincronización completa de todas las contraseñas</span><span class="sxs-lookup"><span data-stu-id="49222-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="49222-296">Ejecute este script una sola vez.</span><span class="sxs-lookup"><span data-stu-id="49222-296">Run this script only once.</span></span> <span data-ttu-id="49222-297">Si tiene que ejecutarlo varias veces, el problema se debe a otro motivo.</span><span class="sxs-lookup"><span data-stu-id="49222-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="49222-298">Para solucionar el problema, contacte con Soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="49222-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="49222-299">Puede desencadenar una sincronización completa de todas las contraseñas mediante el siguiente script:</span><span class="sxs-lookup"><span data-stu-id="49222-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="49222-300">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="49222-300">Next steps</span></span>
* [<span data-ttu-id="49222-301">Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="49222-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="49222-302">Sincronización de Azure AD Connect: personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="49222-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="49222-303">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49222-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
