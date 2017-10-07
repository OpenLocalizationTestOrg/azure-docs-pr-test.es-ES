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
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a>Solución de problemas de la implementación de la sincronización de contraseña con la sincronización de Azure AD Connect
Este tema proporciona los pasos para cómo tootroubleshoot problemas con la sincronización de contraseña. Si las contraseñas no se sincronizan como se esperaba, puede ser para un subconjunto de usuarios o para todos los usuarios. Para Azure Active Directory (Azure AD) conectar la implementación con la versión 1.1.524.0 o una versión posterior, ahora hay un cmdlet de diagnóstico que puede usar tootroubleshoot problemas de sincronización de contraseña:

* Si tiene un problema que no se sincroniza ninguna contraseña, consulte toohello [contraseñas no están sincronizadas: solución de problemas mediante el cmdlet de diagnóstico de hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sección.

* Si tiene un problema con los objetos individuales, consulte toohello [un objeto no se han sincronizado las contraseñas: solución de problemas mediante el cmdlet de diagnóstico de hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sección.

Para versiones anteriores de la implementación de Azure AD Connect:

* Si tiene un problema que no se sincroniza ninguna contraseña, consulte toohello [contraseñas no están sincronizadas: pasos para solucionar problemas de manual](#no-passwords-are-synchronized-manual-troubleshooting-steps) sección.

* Si tiene un problema con los objetos individuales, consulte toohello [un objeto no se han sincronizado las contraseñas: pasos para solucionar problemas de manual](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sección.

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>No las contraseñas se sincronizan: solución de problemas mediante el cmdlet de diagnóstico de Hola
Puede usar hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out ¿por qué no contraseñas están sincronizadas.

> [!NOTE]
> Hola `Invoke-ADSyncDiagnostics` cmdlet está disponible sólo para Azure AD Connect versión 1.1.524.0 o posterior.

### <a name="run-hello-diagnostics-cmdlet"></a>Ejecute el cmdlet de diagnóstico de Hola
problemas de tootroubleshoot donde no se sincroniza ninguna contraseña:

1. Abrir una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect con hello **ejecutar como administrador** opción.

2. Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.

3. Ejecute `Import-Module ADSyncDiagnostics`.

4. Ejecute `Invoke-ADSyncDiagnostics -PasswordSync`.

### <a name="understand-hello-results-of-hello-cmdlet"></a>Entender los resultados de hello del cmdlet Hola
cmdlet de diagnóstico de Hello realiza Hola siguientes comprobaciones:

* Valida que Hola está habilitada la característica de sincronización de contraseña para el inquilino de Azure AD.

* Valida que hello Azure Connect AD server no está en modo de almacenamiento provisional.

* Para cada locales existentes conector de Active Directory (que se corresponde el bosque de Active Directory existente tooan):

   * Valida que Hola está habilitada la característica de sincronización de contraseña.
   
   * Registros de eventos de aplicación de Windows busca eventos de latido de sincronización de contraseña en Hola.

   * Para cada dominio de Active Directory en Conector de Active Directory de hello local:

      * Valida que Hola dominio sea accesible desde el servidor de hello Azure AD Connect.

      * Valida que las cuentas de servicios de dominio de Active Directory (AD DS) de hello utilizadas por el conector de Active Directory local de hello tiene Hola correcta nombre de usuario, contraseña y permisos necesarios para la sincronización de contraseña.

Hola siguiente diagrama muestra resultados de hello del cmdlet de Hola para una topología de Active Directory local de dominio único:

![Salida de diagnóstico de la sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

resto de Hola de esta sección describen los resultados específicos que se devuelven mediante el cmdlet hello y problemas correspondientes.

#### <a name="password-synchronization-feature-isnt-enabled"></a>La característica de sincronización de contraseña no está habilitada
Si no ha habilitado la sincronización de contraseña mediante el uso de Asistente de hello Azure AD Connect, se devuelve Hola siguiente error:

![La sincronización de contraseña no está habilitada](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a>El servidor de Azure AD Connect está en modo de almacenamiento provisional
Si el servidor de Azure AD Connect Hola está en modo de almacenamiento provisional, sincronización de contraseñas está deshabilitada temporalmente y hello siguiente se devuelve el error:

![El servidor de Azure AD Connect está en modo de almacenamiento provisional](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a>No hay eventos de latido de sincronización de contraseña
Cada conector Active Directory local tiene su propio canal de sincronización de contraseña. Cuando se establece el canal de sincronización de contraseña de hello y no hay ningún toobe de cambios de contraseña sincronizada, un evento de latido (Id. de evento 654) se genera una vez cada 30 minutos en el registro de eventos de aplicación de Windows hello. Para cada conector de Active Directory local, Hola cmdlet busca eventos de latido correspondientes en hello las últimas tres horas. Si no se encuentra ningún evento de latido, hello siguiente error se devuelve:

![No hay ningún evento de latido de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a>La cuenta de AD DS no tiene los permisos correctos
Si la cuenta de hello AD DS que se usa por hello local hashes de contraseña de toosynchronize de conector de Active Directory no tiene los permisos adecuados de hello, hello siguiente error se devuelve:

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a>Nombre de usuario o contraseña incorrectos de la cuenta de AD DS
Si hello cuenta AD DS usa hello hashes de contraseña de toosynchronize de conector de Active Directory de local tiene una contraseña o nombre de usuario incorrecto, hello siguiente se devuelve el error:

![Credencial incorrecta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a>Un objeto no se han sincronizado las contraseñas: solución de problemas mediante el cmdlet de diagnóstico de Hola
Puede usar hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet ¿por qué un objeto no sincroniza las contraseñas.

> [!NOTE]
> Hola `Invoke-ADSyncDiagnostics` cmdlet está disponible sólo para Azure AD Connect versión 1.1.524.0 o posterior.

### <a name="run-hello-diagnostics-cmdlet"></a>Ejecute el cmdlet de diagnóstico de Hola
problemas de tootroubleshoot donde no se sincroniza ninguna contraseña:

1. Abrir una nueva sesión de Windows PowerShell en el servidor de Azure AD Connect con hello **ejecutar como administrador** opción.

2. Ejecute `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.

3. Ejecute `Import-Module ADSyncDiagnostics`.

4. Ejecute hello siguiente cmdlet:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   Por ejemplo:
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a>Entender los resultados de hello del cmdlet Hola
cmdlet de diagnóstico de Hello realiza Hola siguientes comprobaciones:

* Examina el estado de saludo del objeto de Active Directory de hello en el espacio de conector de Active Directory de Hola y metaverso, Azure espacio de conector de AD.

* Comprueba que haya reglas de sincronización con la sincronización de contraseña habilitada y aplican toohello objeto de Active Directory.

* Intentos de tooretrieve y mostrar los resultados de Hola Hola último intento toosynchronize hello de la contraseña del objeto de Hola.

Hola siguiente diagrama muestra resultados de hello del cmdlet de hello cuando solucione problemas de sincronización de contraseña para un único objeto:

![Salida de diagnóstico de la sincronización de contraseña: un solo objeto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

resto Hola de esta sección describe los resultados específicos devueltos por el cmdlet de Hola y problemas correspondientes.

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a>objeto de Active Directory de Hello no exportado tooAzure AD
Se produce un error en la sincronización de contraseña para esta cuenta de Active Directory local porque no hay ningún objeto correspondiente en el inquilino de Azure AD Hola. se devuelve Hola siguiente error:

![Falta objeto de Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a>El usuario tiene una contraseña incorrecta
Actualmente, Azure AD Connect no admite la sincronización de contraseñas temporales con Azure AD. Una contraseña se considera toobe temporal si hello **cambiar la contraseña en el siguiente inicio de sesión** opción está establecida en el usuario de Active Directory local de Hola. se devuelve Hola siguiente error:

![La contraseña temporal no se exporta](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a>Resultados del último intento de toosynchronize contraseña no están disponibles
De forma predeterminada, Azure AD Connect almacena los resultados de Hola de intentos de sincronización de contraseña durante siete días. Si no hay ningún resultado disponible para el objeto de Active Directory de hello seleccionado, se devuelve Hola siguiente advertencia:

![Salida de diagnóstico de un solo objeto: no hay historial de sincronización de contraseña](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a>No se sincronizan las contraseñas: pasos para la solución manual de problemas
Siga estos toodetermine pasos ¿por qué no se sincroniza ninguna contraseña:

1. ¿Es servidor de Connect de hello en [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode)? Un servidor en modo de almacenamiento provisional no sincroniza contraseñas.

2. Ejecutar script de Hola Hola [obtener estado de Hola de configuración de sincronización de contraseña](#get-the-status-of-password-sync-settings) sección. Proporciona información general sobre la configuración de sincronización de contraseña de Hola.  

    ![Salida del script de PowerShell de la configuración de sincronización de contraseñas](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. Si no está habilitada la característica de hello en Azure AD o si no está habilitado el estado de sincronización del canal hello, ejecutar a Asistente de instalación de Connect de Hola. Seleccione **Personalizar las opciones de sincronización** y anule la selección de sincronización de contraseñas. Este cambio deshabilita temporalmente la característica de Hola. A continuación, vuelva a ejecutar al Asistente de Hola y volver a habilitar la sincronización de contraseñas. Ejecutar script de Hola de nuevo tooverify que Hola configuración es correcta.

4. Busque en registro de eventos de Hola para los errores. Busque Hola después de eventos, lo que podría indicar un problema:
    * Origen: "Sincronización de directorios" ID: 0, 611, 652, 655. Si ve estos eventos, significa que hay un problema de conectividad. mensaje de registro de eventos de Hello contiene información del bosque donde haya un problema. Para más información, vea [Problemas de conectividad](#connectivity problem).

5. Si no ve ningún latido o si nada funciona, ejecute [Desencadenamiento de una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords). Ejecutar script de Hola solo una vez.

6. Vea hello [solucionar problemas de un objeto que no se está sincronizando las contraseñas](#one-object-is-not-synchronizing-passwords) sección.

### <a name="connectivity-problems"></a>Problemas de conectividad

¿Hay conectividad con Azure AD?

¿Hola se requiere cuenta hashes de contraseña de permisos tooread hello en todos los dominios? Si ha instalado conectar con la configuración rápida, permisos de hello deberían ser correctos. 

Si realizó una instalación personalizada, establecer permisos de hello manualmente haciendo Hola siguiente:
    
1. cuenta de hello toofind utilizado por el conector de Active Directory de hello, inicio **Synchronization Service Manager**. 
 
2. Vaya demasiado**conectores**y, a continuación, busque el bosque de Active Directory local Hola está solucionando. 
 
3. Seleccione el conector de hello y, a continuación, haga clic en **propiedades**. 
 
4. Vaya demasiado**conectar tooActive Directory bosque**.  
    
    ![Cuenta que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    Tenga en cuenta el nombre de usuario de Hola y el dominio de Hola donde se encuentra la cuenta de hello.
    
5. Iniciar **equipos y usuarios de Active Directory**y, a continuación, compruebe que el que se encuentra antes de la cuenta de hello tiene permisos de seguimiento de hello establecidos en raíz de Hola de todos los dominios del bosque:
    * Replicación de cambios de directorio
    * Replicación de todos los cambios de directorio

6. ¿Es Hola controladores de dominio accesible, Azure AD Connect? Si el servidor de Connect de hello no puede conectarse a controladores de dominio de tooall, configurar **usar solo controlador de dominio preferido**.  
    
    ![Controlador de dominio que usa el conector Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. Vuelva demasiado**Synchronization Service Manager** y **configurar la partición del directorio**. 
 
8. Seleccione el dominio en **seleccionar particiones de directorio**, seleccione hello **sólo utilizará los controladores de dominio preferidos** casilla de verificación y, a continuación, haga clic en **configurar**. 

9. En la lista de hello, escriba los controladores de dominio de Hola que conectar debe usar para la sincronización de contraseñas. Hola misma lista se utiliza para importar y exportar también. Siga estos pasos con todos los dominios.

10. Si el script de Hola muestra que no ha habido latidos, ejecute el script de Hola en [desencadenar una sincronización completa de todas las contraseñas](#trigger-a-full-sync-of-all-passwords).

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a>Un objeto no sincroniza contraseñas: pasos para la solución manual de problemas
Fácilmente puede solucionar problemas de sincronización de contraseña, revise el estado de saludo de un objeto.

1. En **equipos y usuarios de Active Directory**, Buscar usuario hello y, a continuación, compruebe que hello **usuario debe cambiar la contraseña en el siguiente inicio de sesión** casilla de verificación está desactivada.  

    ![Contraseñas productivas de Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    Si está activada la casilla de verificación de hello, formule Hola usuario toosign en y cambiar la contraseña de Hola. Las contraseñas temporales no se sincronizan con Azure AD.

2. Si la contraseña de hello parece correcto en Active Directory, siga usuario hello en el motor de sincronización de Hola. Por usuario de hello siguientes desde tooAzure de Active Directory local AD, puede ver si hay un error descriptivo en objeto Hola.

    a. Iniciar hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).

    b. Haga clic en **Conectores**.

    c. Seleccione hello **conector de Active Directory** donde se encuentra el usuario de Hola.

    d. Seleccione **Search Connector Space**(Buscar espacio de conector).

    e. Hola **ámbito** cuadro, seleccione **DN o delimitador**y, a continuación, escriba Hola DN completo del usuario de hello está solucionando.

    ![Búsqueda de usuario en el espacio conector con DN](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    f. Buscar usuario de Hola que está buscando y, a continuación, haga clic en **propiedades** toosee Hola a todos los atributos. Si no es usuario hello en el resultado de la búsqueda de hello, compruebe su [las reglas de filtrado](active-directory-aadconnectsync-configure-filtering.md) y asegúrese de que ejecuta [aplicar y comprobar los cambios](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) para tooappear de usuario de hello en conectar.

    g. Haga clic en la semana pasada, detalles de sincronización de contraseña de toosee Hola del objeto de Hola para hello **registro**.  

    ![Detalles del registro de objetos](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    Si el registro de hello objeto está vacío, Azure AD Connect ha sido hash de contraseña de hello no se puede tooread de Active Directory. Continúe solucionando problemas con [Errores de conectividad](#connectivity-errors). Si ve un valor distinto de **correcto**, consulte la tabla de toohello en [registro de sincronización de contraseña](#password-sync-log).

    h. Seleccione hello **linaje** pestaña y asegúrese de que esa regla al menos una sincronización en hello **PasswordSync** columna es **True**. En la configuración predeterminada de hello, nombre de hello de la regla de sincronización hello es **en desde AD - User AccountEnabled**.  

    ![Información de linaje de un usuario](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    i. Haga clic en **propiedades del objeto de metaverso** toodisplay una lista de atributos de usuario.  

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    Compruebe que no hay ningún atributo **cloudFiltered**. Asegúrese de que los atributos de dominio de hello (domainFQDN y domainNetBios) tienen valores de hello esperados.

    j. Haga clic en hello **conectores** ficha. Asegúrese de que ve conectores tooboth Active Directory local y Azure AD.

    ![Información de metaverso](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    k. Seleccione Hola fila que representa AD de Azure, haga clic en **propiedades**y, a continuación, haga clic en hello **linaje** objeto de espacio de conector de Hola de ficha debe tener una regla de salida en hello **PasswordSync** columna se establece demasiado**True**. En la configuración predeterminada de hello, nombre de hello de la regla de sincronización hello es **Out tooAAD - User Join**.  

    ![Cuadro de diálogo de propiedades de objeto del espacio conector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a>Registro de sincronización de contraseñas
columna de estado de Hello puede tener Hola siguientes valores:

| Estado | Description |
| --- | --- |
| Correcto |La contraseña se sincronizó correctamente. |
| FilteredByTarget |Contraseña se establece demasiado**usuario debe cambiar la contraseña en el siguiente inicio de sesión**. La contraseña no se ha sincronizado. |
| NoTargetConnection |Ningún objeto de metaverso de Hola o en el espacio del conector de hello Azure AD. |
| SourceConnectorNotPresent |No se encuentran en el espacio del conector de Active Directory de hello local de objetos. |
| TargetNotExportedToDirectory |objeto de Hola Hola espacio de conector de Azure AD aún no se ha exportado. |
| MigratedCheckDetailsForMoreInfo |La entrada de registro se creó antes de la versión 1.0.9125.0 y se muestra en su estado heredado. |
| Error |El servicio devolvió un error desconocido. |
| Desconocido |Se produjo un error al tratar de tooprocess un lote de hash de contraseña.  |
| MissingAttribute |Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no están disponibles. |
| RetryRequestedByTarget |Los atributos específicos (por ejemplo, hash de Kerberos) que requiere Azure AD Domain Services no estaban disponibles anteriormente. Hash de contraseña de un intento de tooresynchronize Hola usuario se ha realizado. |

## <a name="scripts-toohelp-troubleshooting"></a>Solución de problemas de las secuencias de comandos toohelp

### <a name="get-hello-status-of-password-sync-settings"></a>Obtener estado de Hola de configuración de sincronización de contraseña
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a>Desencadenamiento de una sincronización completa de todas las contraseñas
> [!NOTE]
> Ejecute este script una sola vez. Si necesita toorun más de una vez, algo es problema de Hola. problema de hello tootroubleshoot, póngase en contacto con soporte técnico de Microsoft.

Puede desencadenar una sincronización completa de todas las contraseñas mediante Hola siguiente secuencia de comandos:

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

## <a name="next-steps"></a>Pasos siguientes
* [Implementación de la sincronización de contraseña mediante la sincronización de Azure AD Connect](active-directory-aadconnectsync-implement-password-synchronization.md)
* [Sincronización de Azure AD Connect: personalización de las opciones de sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
