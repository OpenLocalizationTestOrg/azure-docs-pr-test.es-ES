---
title: "sincronización de contraseña de aaaTroubleshoot con sincronización de Azure AD Connect | Documentos de Microsoft"
description: "Este artículo proporciona información acerca de cómo los problemas de sincronización de contraseña tootroubleshoot."
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="9af62-103">Solución de problemas de la implementación de la sincronización de contraseña con la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9af62-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="9af62-104">Este tema proporciona los pasos para cómo tootroubleshoot problemas con la sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9af62-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="9af62-105">Si las contraseñas no se sincronizan como se esperaba, puede ser para un subconjunto de usuarios o para todos los usuarios.</span><span class="sxs-lookup"><span data-stu-id="9af62-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="9af62-106">Para Azure Active Directory (Azure AD) conectar la implementación con la versión 1.1.524.0 o una versión posterior, ahora hay un cmdlet de diagnóstico que puede usar tootroubleshoot problemas de sincronización de contraseña:</span><span class="sxs-lookup"><span data-stu-id="9af62-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="9af62-107">Si tiene un problema que no se sincroniza ninguna contraseña, consulte toohello [contraseñas no están sincronizadas: solución de problemas mediante el cmdlet de diagnóstico de hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="9af62-108">Si tiene un problema con los objetos individuales, consulte toohello [un objeto no se han sincronizado las contraseñas: solución de problemas mediante el cmdlet de diagnóstico de hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="9af62-109">Para versiones anteriores de la implementación de Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="9af62-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="9af62-110">Si tiene un problema que no se sincroniza ninguna contraseña, consulte toohello [contraseñas no están sincronizadas: pasos para solucionar problemas de manual](#no-passwords-are-synchronized-manual-troubleshooting-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="9af62-111">Si tiene un problema con los objetos individuales, consulte toohello [un objeto no se han sincronizado las contraseñas: pasos para solucionar problemas de manual](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="9af62-112">No las contraseñas se sincronizan: solución de problemas mediante el cmdlet de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="9af62-113">Puede usar hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out ¿por qué no contraseñas están sincronizadas.</span><span class="sxs-lookup"><span data-stu-id="9af62-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="9af62-114">Hola `Invoke-ADSyncDiagnostics` cmdlet está disponible sólo para Azure AD Connect versión 1.1.524.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9af62-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="9af62-115">Ejecute el cmdlet de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="9af62-116">problemas de tootroubleshoot donde no se sincroniza ninguna contraseña:</span><span class="sxs-lookup"><span data-stu-id="9af62-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="9af62-117">Abrir una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect con hello **ejecutar como administrador** opción.</span><span class="sxs-lookup"><span data-stu-id="9af62-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="9af62-118">Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="9af62-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="9af62-119">Ejecute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="9af62-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="9af62-120">Ejecute `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="9af62-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="9af62-121">Entender los resultados de hello del cmdlet Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="9af62-122">cmdlet de diagnóstico de Hello realiza Hola siguientes comprobaciones:</span><span class="sxs-lookup"><span data-stu-id="9af62-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="9af62-123">Valida que Hola está habilitada la característica de sincronización de contraseña para el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="9af62-124">Valida que hello Azure Connect AD server no está en modo de almacenamiento provisional.</span><span class="sxs-lookup"><span data-stu-id="9af62-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="9af62-125">Para cada locales existentes conector de Active Directory (que se corresponde el bosque de Active Directory existente tooan):</span><span class="sxs-lookup"><span data-stu-id="9af62-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="9af62-126">Valida que Hola está habilitada la característica de sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9af62-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="9af62-127">Registros de eventos de aplicación de Windows busca eventos de latido de sincronización de contraseña en Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="9af62-128">Para cada dominio de Active Directory en Conector de Active Directory de hello local:</span><span class="sxs-lookup"><span data-stu-id="9af62-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="9af62-129">Valida que Hola dominio sea accesible desde el servidor de hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9af62-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="9af62-130">Valida que las cuentas de servicios de dominio de Active Directory (AD DS) de hello utilizadas por el conector de Active Directory local de hello tiene Hola correcta nombre de usuario, contraseña y permisos necesarios para la sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9af62-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="9af62-131">Hola siguiente diagrama muestra resultados de hello del cmdlet de Hola para una topología de Active Directory local de dominio único:</span><span class="sxs-lookup"><span data-stu-id="9af62-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Salida de diagnóstico de la sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="9af62-133">resto de Hola de esta sección describen los resultados específicos que se devuelven mediante el cmdlet hello y problemas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="9af62-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="9af62-134">La característica de sincronización de contraseña no está habilitada</span><span class="sxs-lookup"><span data-stu-id="9af62-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="9af62-135">Si no ha habilitado la sincronización de contraseña mediante el uso de Asistente de hello Azure AD Connect, se devuelve Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="9af62-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![La sincronización de contraseña no está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="9af62-137">El servidor de Azure AD Connect está en modo de almacenamiento provisional</span><span class="sxs-lookup"><span data-stu-id="9af62-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="9af62-138">Si el servidor de Azure AD Connect Hola está en modo de almacenamiento provisional, sincronización de contraseñas está deshabilitada temporalmente y hello siguiente se devuelve el error:</span><span class="sxs-lookup"><span data-stu-id="9af62-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![El servidor de Azure AD Connect está en modo de almacenamiento provisional](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="9af62-140">No hay eventos de latido de sincronización de contraseña</span><span class="sxs-lookup"><span data-stu-id="9af62-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="9af62-141">Cada conector Active Directory local tiene su propio canal de sincronización de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9af62-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="9af62-142">Cuando se establece el canal de sincronización de contraseña de hello y no hay ningún toobe de cambios de contraseña sincronizada, un evento de latido (Id. de evento 654) se genera una vez cada 30 minutos en el registro de eventos de aplicación de Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9af62-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="9af62-143">Para cada conector de Active Directory local, Hola cmdlet busca eventos de latido correspondientes en hello las últimas tres horas.</span><span class="sxs-lookup"><span data-stu-id="9af62-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="9af62-144">Si no se encuentra ningún evento de latido, hello siguiente error se devuelve:</span><span class="sxs-lookup"><span data-stu-id="9af62-144">If no heartbeat event is found, hello following error is returned:</span></span>

![No hay ningún evento de latido de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="9af62-146">La cuenta de AD DS no tiene los permisos correctos</span><span class="sxs-lookup"><span data-stu-id="9af62-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="9af62-147">Si la cuenta de hello AD DS que se usa por hello local hashes de contraseña de toosynchronize de conector de Active Directory no tiene los permisos adecuados de hello, hello siguiente error se devuelve:</span><span class="sxs-lookup"><span data-stu-id="9af62-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="9af62-149">Nombre de usuario o contraseña incorrectos de la cuenta de AD DS</span><span class="sxs-lookup"><span data-stu-id="9af62-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="9af62-150">Si hello cuenta AD DS usa hello hashes de contraseña de toosynchronize de conector de Active Directory de local tiene una contraseña o nombre de usuario incorrecto, hello siguiente se devuelve el error:</span><span class="sxs-lookup"><span data-stu-id="9af62-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="9af62-152">Un objeto no se han sincronizado las contraseñas: solución de problemas mediante el cmdlet de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="9af62-153">Puede usar hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet ¿por qué un objeto no sincroniza las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="9af62-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="9af62-154">Hola `Invoke-ADSyncDiagnostics` cmdlet está disponible sólo para Azure AD Connect versión 1.1.524.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="9af62-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="9af62-155">Ejecute el cmdlet de diagnóstico de Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="9af62-156">problemas de tootroubleshoot donde no se sincroniza ninguna contraseña:</span><span class="sxs-lookup"><span data-stu-id="9af62-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="9af62-157">Abrir una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect con hello **ejecutar como administrador** opción.</span><span class="sxs-lookup"><span data-stu-id="9af62-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="9af62-158">Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="9af62-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="9af62-159">Ejecute `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="9af62-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="9af62-160">Ejecute hello siguiente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9af62-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="9af62-161">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9af62-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="9af62-162">Entender los resultados de hello del cmdlet Hola</span><span class="sxs-lookup"><span data-stu-id="9af62-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="9af62-163">cmdlet de diagnóstico de Hello realiza Hola siguientes comprobaciones:</span><span class="sxs-lookup"><span data-stu-id="9af62-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="9af62-164">Examina el estado de saludo del objeto de Active Directory de hello en el espacio de conector de Active Directory de Hola y metaverso, Azure espacio de conector de AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="9af62-165">Comprueba que haya reglas de sincronización con la sincronización de contraseña habilitada y aplican toohello objeto de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9af62-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="9af62-166">Intentos de tooretrieve y mostrar los resultados de Hola Hola último intento toosynchronize hello de la contraseña del objeto de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="9af62-167">Hola siguiente diagrama muestra resultados de hello del cmdlet de hello cuando solucione problemas de sincronización de contraseña para un único objeto:</span><span class="sxs-lookup"><span data-stu-id="9af62-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Salida de diagnóstico de la sincronización de contraseña: un solo objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="9af62-169">resto Hola de esta sección describe los resultados específicos devueltos por el cmdlet de Hola y problemas correspondientes.</span><span class="sxs-lookup"><span data-stu-id="9af62-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="9af62-170">objeto de Active Directory de Hello no exportado tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="9af62-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="9af62-171">Se produce un error en la sincronización de contraseña para esta cuenta de Active Directory local porque no hay ningún objeto correspondiente en el inquilino de Azure AD Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="9af62-172">se devuelve Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="9af62-172">hello following error is returned:</span></span>

![Falta objeto de Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="9af62-174">El usuario tiene una contraseña incorrecta</span><span class="sxs-lookup"><span data-stu-id="9af62-174">User has a temporary password</span></span>
<span data-ttu-id="9af62-175">Actualmente, Azure AD Connect no admite la sincronización de contraseñas temporales con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="9af62-176">Una contraseña se considera toobe temporal si hello **cambiar la contraseña en el siguiente inicio de sesión** opción está establecida en el usuario de Active Directory local de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="9af62-177">se devuelve Hola siguiente error:</span><span class="sxs-lookup"><span data-stu-id="9af62-177">hello following error is returned:</span></span>

![La contraseña temporal no se exporta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="9af62-179">Resultados del último intento de toosynchronize contraseña no están disponibles</span><span class="sxs-lookup"><span data-stu-id="9af62-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="9af62-180">De forma predeterminada, Azure AD Connect almacena los resultados de Hola de intentos de sincronización de contraseña durante siete días.</span><span class="sxs-lookup"><span data-stu-id="9af62-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="9af62-181">Si no hay ningún resultado disponible para el objeto de Active Directory de hello seleccionado, se devuelve Hola siguiente advertencia:</span><span class="sxs-lookup"><span data-stu-id="9af62-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Salida de diagnóstico de un solo objeto: no hay historial de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="9af62-183">No se sincronizan las contraseñas: pasos para la solución manual de problemas</span><span class="sxs-lookup"><span data-stu-id="9af62-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="9af62-184">Siga estos toodetermine pasos ¿por qué no se sincroniza ninguna contraseña:</span><span class="sxs-lookup"><span data-stu-id="9af62-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="9af62-185">¿Es servidor de Connect de hello en [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="9af62-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="9af62-186">Un servidor en modo de almacenamiento provisional no sincroniza contraseñas.</span><span class="sxs-lookup"><span data-stu-id="9af62-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="9af62-187">Ejecutar script de Hola Hola [obtener estado de Hola de configuración de sincronización de contraseña](#get-the-status-of-password-sync-settings) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="9af62-188">Proporciona información general sobre la configuración de sincronización de contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Salida del script de PowerShell de la configuración de sincronización de contraseñas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="9af62-190">Si no está habilitada la característica de hello en Azure AD o si no está habilitado el estado de sincronización del canal hello, ejecutar a Asistente de instalación de Connect de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="9af62-191">Seleccione **Personalizar las opciones de sincronización** y anule la selección de sincronización de contraseñas. Este cambio deshabilita temporalmente la característica de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="9af62-192">A continuación, vuelva a ejecutar al Asistente de Hola y volver a habilitar la sincronización de contraseñas. Ejecutar script de Hola de nuevo tooverify que Hola configuración es correcta.</span><span class="sxs-lookup"><span data-stu-id="9af62-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="9af62-193">Busque en registro de eventos de Hola para los errores.</span><span class="sxs-lookup"><span data-stu-id="9af62-193">Look in hello event log for errors.</span></span> <span data-ttu-id="9af62-194">Busque Hola después de eventos, lo que podría indicar un problema:</span><span class="sxs-lookup"><span data-stu-id="9af62-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="9af62-195">Origen: "Sincronización de directorios" ID: 0, 611, 652, 655. Si ve estos eventos, significa que hay un problema de conectividad.</span><span class="sxs-lookup"><span data-stu-id="9af62-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="9af62-196">mensaje de registro de eventos de Hello contiene información del bosque donde haya un problema.</span><span class="sxs-lookup"><span data-stu-id="9af62-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="9af62-197">Para más información, vea [Problemas de conectividad](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="9af62-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="9af62-198">Si no ve ningún latido o si nada funciona, ejecute [Desencadenamiento de una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="9af62-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="9af62-199">Ejecutar script de Hola solo una vez.</span><span class="sxs-lookup"><span data-stu-id="9af62-199">Run hello script only once.</span></span>

6. <span data-ttu-id="9af62-200">Vea hello [solucionar problemas de un objeto que no se está sincronizando las contraseñas](#one-object-is-not-synchronizing-passwords) sección.</span><span class="sxs-lookup"><span data-stu-id="9af62-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="9af62-201">Problemas de conectividad</span><span class="sxs-lookup"><span data-stu-id="9af62-201">Connectivity problems</span></span>

<span data-ttu-id="9af62-202">¿Hay conectividad con Azure AD?</span><span class="sxs-lookup"><span data-stu-id="9af62-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="9af62-203">¿Hola se requiere cuenta hashes de contraseña de permisos tooread hello en todos los dominios?</span><span class="sxs-lookup"><span data-stu-id="9af62-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="9af62-204">Si ha instalado conectar con la configuración rápida, permisos de hello deberían ser correctos.</span><span class="sxs-lookup"><span data-stu-id="9af62-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="9af62-205">Si realizó una instalación personalizada, establecer permisos de hello manualmente haciendo Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="9af62-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="9af62-206">cuenta de hello toofind utilizado por el conector de Active Directory de hello, inicio **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="9af62-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="9af62-207">Vaya demasiado**conectores**y, a continuación, busque el bosque de Active Directory local Hola está solucionando.</span><span class="sxs-lookup"><span data-stu-id="9af62-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="9af62-208">Seleccione el conector de hello y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="9af62-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="9af62-209">Vaya demasiado**conectar tooActive Directory bosque**.</span><span class="sxs-lookup"><span data-stu-id="9af62-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Cuenta que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="9af62-211">Tenga en cuenta el nombre de usuario de Hola y el dominio de Hola donde se encuentra la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="9af62-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="9af62-212">Iniciar **equipos y usuarios de Active Directory**y, a continuación, compruebe que el que se encuentra antes de la cuenta de hello tiene permisos de seguimiento de hello establecidos en raíz de Hola de todos los dominios del bosque:</span><span class="sxs-lookup"><span data-stu-id="9af62-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="9af62-213">Replicación de cambios de directorio</span><span class="sxs-lookup"><span data-stu-id="9af62-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="9af62-214">Replicación de todos los cambios de directorio</span><span class="sxs-lookup"><span data-stu-id="9af62-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="9af62-215">¿Es Hola controladores de dominio accesible, Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="9af62-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="9af62-216">Si el servidor de Connect de hello no puede conectarse a controladores de dominio de tooall, configurar **usar solo controlador de dominio preferido**.</span><span class="sxs-lookup"><span data-stu-id="9af62-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controlador de dominio que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="9af62-218">Vuelva demasiado**Synchronization Service Manager** y **configurar la partición del directorio**.</span><span class="sxs-lookup"><span data-stu-id="9af62-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="9af62-219">Seleccione el dominio en **seleccionar particiones de directorio**, seleccione hello **sólo utilizará los controladores de dominio preferidos** casilla de verificación y, a continuación, haga clic en **configurar**.</span><span class="sxs-lookup"><span data-stu-id="9af62-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="9af62-220">En la lista de hello, escriba los controladores de dominio de Hola que conectar debe usar para la sincronización de contraseñas. Hola misma lista se utiliza para importar y exportar también.</span><span class="sxs-lookup"><span data-stu-id="9af62-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="9af62-221">Siga estos pasos con todos los dominios.</span><span class="sxs-lookup"><span data-stu-id="9af62-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="9af62-222">Si el script de Hola muestra que no ha habido latidos, ejecute el script de Hola en [desencadenar una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="9af62-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="9af62-223">Un objeto no sincroniza contraseñas: pasos para la solución manual de problemas</span><span class="sxs-lookup"><span data-stu-id="9af62-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="9af62-224">Fácilmente puede solucionar problemas de sincronización de contraseña, revise el estado de saludo de un objeto.</span><span class="sxs-lookup"><span data-stu-id="9af62-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="9af62-225">En **equipos y usuarios de Active Directory**, Buscar usuario hello y, a continuación, compruebe que hello **usuario debe cambiar la contraseña en el siguiente inicio de sesión** casilla de verificación está desactivada.</span><span class="sxs-lookup"><span data-stu-id="9af62-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Contraseñas productivas de Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="9af62-227">Si está activada la casilla de verificación de hello, formule Hola usuario toosign en y cambiar la contraseña de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="9af62-228">Las contraseñas temporales no se sincronizan con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="9af62-229">Si la contraseña de hello parece correcto en Active Directory, siga usuario hello en el motor de sincronización de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="9af62-230">Por usuario de hello siguientes desde tooAzure de Active Directory local AD, puede ver si hay un error descriptivo en objeto Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="9af62-231">a.</span><span class="sxs-lookup"><span data-stu-id="9af62-231">a.</span></span> <span data-ttu-id="9af62-232">Iniciar hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="9af62-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="9af62-233">b.</span><span class="sxs-lookup"><span data-stu-id="9af62-233">b.</span></span> <span data-ttu-id="9af62-234">Haga clic en **Conectores**.</span><span class="sxs-lookup"><span data-stu-id="9af62-234">Click **Connectors**.</span></span>

    <span data-ttu-id="9af62-235">c.</span><span class="sxs-lookup"><span data-stu-id="9af62-235">c.</span></span> <span data-ttu-id="9af62-236">Seleccione hello **conector de Active Directory** donde se encuentra el usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="9af62-237">d.</span><span class="sxs-lookup"><span data-stu-id="9af62-237">d.</span></span> <span data-ttu-id="9af62-238">Seleccione **Search Connector Space**(Buscar espacio de conector).</span><span class="sxs-lookup"><span data-stu-id="9af62-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="9af62-239">e.</span><span class="sxs-lookup"><span data-stu-id="9af62-239">e.</span></span> <span data-ttu-id="9af62-240">Hola **ámbito** cuadro, seleccione **DN o delimitador**y, a continuación, escriba Hola DN completo del usuario de hello está solucionando.</span><span class="sxs-lookup"><span data-stu-id="9af62-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Búsqueda de usuario en el espacio conector con DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="9af62-242">f.</span><span class="sxs-lookup"><span data-stu-id="9af62-242">f.</span></span> <span data-ttu-id="9af62-243">Buscar usuario de Hola que está buscando y, a continuación, haga clic en **propiedades** toosee Hola a todos los atributos.</span><span class="sxs-lookup"><span data-stu-id="9af62-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="9af62-244">Si no es usuario hello en el resultado de la búsqueda de hello, compruebe su [las reglas de filtrado](active-directory-aadconnectsync-configure-filtering.md) y asegúrese de que ejecuta [aplicar y comprobar los cambios](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para tooappear de usuario de hello en conectar.</span><span class="sxs-lookup"><span data-stu-id="9af62-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="9af62-245">g.</span><span class="sxs-lookup"><span data-stu-id="9af62-245">g.</span></span> <span data-ttu-id="9af62-246">Haga clic en la semana pasada, detalles de sincronización de contraseña de toosee Hola del objeto de Hola para hello **registro**.</span><span class="sxs-lookup"><span data-stu-id="9af62-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Detalles del registro de objetos](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="9af62-248">Si el registro de hello objeto está vacío, Azure AD Connect ha sido hash de contraseña de hello no se puede tooread de Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9af62-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="9af62-249">Continúe solucionando problemas con [Errores de conectividad](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="9af62-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="9af62-250">Si ve un valor distinto de **correcto**, consulte la tabla de toohello en [registro de sincronización de contraseña](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="9af62-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="9af62-251">h.</span><span class="sxs-lookup"><span data-stu-id="9af62-251">h.</span></span> <span data-ttu-id="9af62-252">Seleccione hello **linaje** pestaña y asegúrese de que esa regla al menos una sincronización en hello **PasswordSync** columna es **True**.</span><span class="sxs-lookup"><span data-stu-id="9af62-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="9af62-253">En la configuración predeterminada de hello, nombre de hello de la regla de sincronización hello es **en desde AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="9af62-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Información de linaje de un usuario](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="9af62-255">i.</span><span class="sxs-lookup"><span data-stu-id="9af62-255">i.</span></span> <span data-ttu-id="9af62-256">Haga clic en **propiedades del objeto de metaverso** toodisplay una lista de atributos de usuario.</span><span class="sxs-lookup"><span data-stu-id="9af62-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="9af62-258">Compruebe que no hay ningún atributo **cloudFiltered**.</span><span class="sxs-lookup"><span data-stu-id="9af62-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="9af62-259">Asegúrese de que los atributos de dominio de hello (domainFQDN y domainNetBios) tienen valores de hello esperados.</span><span class="sxs-lookup"><span data-stu-id="9af62-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="9af62-260">j.</span><span class="sxs-lookup"><span data-stu-id="9af62-260">j.</span></span> <span data-ttu-id="9af62-261">Haga clic en hello **conectores** ficha. Asegúrese de que ve conectores tooboth Active Directory local y Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="9af62-263">k.</span><span class="sxs-lookup"><span data-stu-id="9af62-263">k.</span></span> <span data-ttu-id="9af62-264">Seleccione Hola fila que representa AD de Azure, haga clic en **propiedades**y, a continuación, haga clic en hello **linaje** objeto de espacio de conector de Hola de ficha debe tener una regla de salida en hello **PasswordSync** columna se establece demasiado**True**.</span><span class="sxs-lookup"><span data-stu-id="9af62-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="9af62-265">En la configuración predeterminada de hello, nombre de hello de la regla de sincronización hello es **Out tooAAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="9af62-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Cuadro de diálogo de propiedades de objeto del espacio conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="9af62-267">Registro de sincronización de contraseñas</span><span class="sxs-lookup"><span data-stu-id="9af62-267">Password sync log</span></span>
<span data-ttu-id="9af62-268">columna de estado de Hello puede tener Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="9af62-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="9af62-269">Estado</span><span class="sxs-lookup"><span data-stu-id="9af62-269">Status</span></span> | <span data-ttu-id="9af62-270">Description</span><span class="sxs-lookup"><span data-stu-id="9af62-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9af62-271">Correcto</span><span class="sxs-lookup"><span data-stu-id="9af62-271">Success</span></span> |<span data-ttu-id="9af62-272">La contraseña se sincronizó correctamente.</span><span class="sxs-lookup"><span data-stu-id="9af62-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="9af62-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="9af62-273">FilteredByTarget</span></span> |<span data-ttu-id="9af62-274">Contraseña se establece demasiado**usuario debe cambiar la contraseña en el siguiente inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="9af62-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="9af62-275">La contraseña no se ha sincronizado.</span><span class="sxs-lookup"><span data-stu-id="9af62-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="9af62-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="9af62-276">NoTargetConnection</span></span> |<span data-ttu-id="9af62-277">Ningún objeto de metaverso de Hola o en el espacio del conector de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9af62-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="9af62-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="9af62-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="9af62-279">No se encuentran en el espacio del conector de Active Directory de hello local de objetos.</span><span class="sxs-lookup"><span data-stu-id="9af62-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="9af62-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="9af62-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="9af62-281">objeto de Hola Hola espacio de conector de Azure AD aún no se ha exportado.</span><span class="sxs-lookup"><span data-stu-id="9af62-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="9af62-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="9af62-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="9af62-283">La entrada de registro se creó antes de la versión 1.0.9125.0 y se muestra en su estado heredado.</span><span class="sxs-lookup"><span data-stu-id="9af62-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="9af62-284">Error</span><span class="sxs-lookup"><span data-stu-id="9af62-284">Error</span></span> |<span data-ttu-id="9af62-285">El servicio devolvió un error desconocido.</span><span class="sxs-lookup"><span data-stu-id="9af62-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="9af62-286">Desconocido</span><span class="sxs-lookup"><span data-stu-id="9af62-286">Unknown</span></span> |<span data-ttu-id="9af62-287">Se produjo un error al tratar de tooprocess un lote de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="9af62-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="9af62-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="9af62-288">MissingAttribute</span></span> |<span data-ttu-id="9af62-289">Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no están disponibles.</span><span class="sxs-lookup"><span data-stu-id="9af62-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="9af62-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="9af62-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="9af62-291">Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no estaban disponibles anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9af62-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="9af62-292">Hash de contraseña de un intento de tooresynchronize Hola usuario se ha realizado.</span><span class="sxs-lookup"><span data-stu-id="9af62-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="9af62-293">Solución de problemas de las secuencias de comandos toohelp</span><span class="sxs-lookup"><span data-stu-id="9af62-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="9af62-294">Obtener estado de Hola de configuración de sincronización de contraseña</span><span class="sxs-lookup"><span data-stu-id="9af62-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="9af62-295">Desencadenamiento de una sincronización completa de todas las contraseñas</span><span class="sxs-lookup"><span data-stu-id="9af62-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="9af62-296">Ejecute este script una sola vez.</span><span class="sxs-lookup"><span data-stu-id="9af62-296">Run this script only once.</span></span> <span data-ttu-id="9af62-297">Si necesita toorun más de una vez, algo es problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9af62-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="9af62-298">problema de hello tootroubleshoot, póngase en contacto con soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9af62-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="9af62-299">Puede desencadenar una sincronización completa de todas las contraseñas mediante Hola siguiente secuencia de comandos:</span><span class="sxs-lookup"><span data-stu-id="9af62-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9af62-300">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9af62-300">Next steps</span></span>
* [<span data-ttu-id="9af62-301">Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9af62-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="9af62-302">Sincronización de Azure AD Connect: personalización de las opciones de sincronización</span><span class="sxs-lookup"><span data-stu-id="9af62-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="9af62-303">Integración de las identidades locales con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9af62-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
