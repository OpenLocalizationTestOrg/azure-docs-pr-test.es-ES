---
title: "Integración del centro de datos de Azure Stack: identidad"
description: "Obtenga información sobre cómo integrar AD FS de Azure Stack con AD FS de su centro de datos."
services: azure-stack
author: mattbriggs
ms.service: azure-stack
ms.topic: article
ms.date: 12/12/2017
ms.author: mabrigg
keywords: 
ms.openlocfilehash: 642ed3298eec0bab5515df117c0310786358e417
ms.sourcegitcommit: 922687d91838b77c038c68b415ab87d94729555e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2017
---
# <a name="azure-stack-datacenter-integration---identity"></a>Integración del centro de datos de Azure Stack: identidad

*Se aplica a: sistemas integrados de Azure Stack*

Puede implementar Azure Stack mediante Azure Active Directory (Azure AD) o con los Servicios de federación de Active Directory (AD FS) como proveedores de identidades. Deberá escoger antes de implementar Azure Stack. La implementación mediante AD FS también se conoce como implementación de Azure Stack en modo desconectado.

En la tabla siguiente se muestran las diferencias entre las dos opciones de identidad:

||Físicamente desconectado|Físicamente conectado|
|---------|---------|---------|
|Facturación|Debe ser capacidad<br> Solo Contrato Enterprise (EA)|Capacidad o de pago por uso<br>EA o proveedor de soluciones en la nube (CSP)|
|Identidad|Debe ser AD FS|Azure AD o AD FS|
|Redifusión de Marketplace|No está disponible actualmente|Compatible<br>Licencias BYOL|
|Registro|Recomendado, requiere un medio extraíble<br> y un dispositivo conectado independiente.|Automatizado|
|Revisiones y actualizaciones|Requerido, requiere un medio extraíble<br> y un dispositivo conectado independiente.|El paquete de actualización se puede descargar directamente<br> de Internet a Azure Stack.|

> [!IMPORTANT]
> No se puede cambiar el proveedor de identidades sin volver a implementar la solución completa de Azure Stack.

## <a name="active-directory-federation-services-and-graph"></a>Servicios de federación de Active Directory y Graph

La implementación con AD FS permite autenticar las identidades de un bosque de Active Directory existente con los recursos de Azure Stack. Este bosque de Active Directory existente requiere una implementación de AD FS para permitir la creación de una confianza de federación de AD FS.

La autenticación es parte de la identidad. Para administrar el Control de acceso basado en roles (RBAC) de Azure Stack, se debe configurar el componente de Graph. Cuando se delega el acceso a un recurso, el componente de Graph busca la cuenta de usuario en el bosque de Active Directory existente mediante el protocolo LDAP.

![Arquitectura de AD FS de Azure Stack](media/azure-stack-integrate-identity/Azure-Stack-ADFS-architecture.png)

La instancia existente de AD FS es el servicio de token de seguridad (STS) de la cuenta que envía notificaciones a AD FS de Azure Stack (el STS del recurso). En Azure Stack, la automatización crea la relación de confianza del proveedor de notificaciones con el punto de conexión de metadatos para la instancia de AD FS existente.

En la instancia de AD FS existente, se debe configurar una relación de confianza para usuario autenticado. Este paso no se realiza mediante la automatización y debe estar configurado por el operador. El punto de conexión de metadatos de Azure Stack se documenta en el archivo AzureStackStampDeploymentInfo.JSON, o a través del punto de conexión con privilegios mediante la ejecución del comando `Get-AzureStackInfo`.

La configuración de la relación de confianza para usuario autenticado también requiere que configure las reglas de transformación de notificaciones que proceden de Microsoft.

Para la configuración de Graph, se debe proporcionar una cuenta de servicio que tenga permiso de lectura en la instancia de Active Directory existente. Esta cuenta es necesaria como entrada para que la automatización habilite escenarios RBAC.

Para el último paso, se configura un nuevo propietario para la suscripción del proveedor predeterminado. Esta cuenta tiene acceso completo a todos los recursos cuando se inicia sesión en el portal de administrador de Azure Stack.

Requisitos:


|Componente|Requisito|
|---------|---------|
|Grafo|Microsoft Active Directory 2012/2012 R2/2016|
|AD FS|Windows Server 2012/2012 R2/2016|

## <a name="setting-up-graph-integration"></a>Configuración de la integración de Graph

Se requiere la siguiente información como entrada para los parámetros de automatización:


|Parámetro|Description|Ejemplo|
|---------|---------|---------|
|CustomADGlobalCatalog|FQDN del bosque de Active Directory de destino<br>que desee integrar con|Contoso.com|
|CustomADAdminCredentials|Un usuario con permiso de lectura de LDAP|YOURDOMAIN\graphservice|

### <a name="create-user-account-in-the-existing-active-directory-optional"></a>Creación de una cuenta de usuario en Active Directory existente (opcional)

Si lo desea, puede crear una cuenta para el servicio Graph en la instancia de Active Directory existente. Realice este paso si ya no tiene una cuenta que desea utilizar.

1. En la instancia de Active Directory existente, cree la siguiente cuenta de usuario (recomendación):
   - **Nombre de usuario**: graphservice
   - **Contraseña**: utilice una contraseña segura<br>Configure una contraseña para que no caduque nunca.

   No se necesita ningún permiso especial ni pertenencia.

#### <a name="trigger-automation-to-configure-graph"></a>Automatización de un desencadenador para configurar un grafo

Para este procedimiento, use un equipo de la red del centro de datos que pueda comunicarse con el punto de conexión con privilegios de Azure Stack.

2. Abra una sesión de Windows PowerShell con privilegios elevados (ejecútela como administrador) y conéctese a la dirección IP del punto de conexión con privilegios. Use las credenciales para la autenticación con **CloudAdmin**.

   ```powershell
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

3. Ahora que se ha conectado al punto de conexión con privilegios, ejecute el siguiente comando: 

   ```powershell
   Register-DirectoryService -CustomADGlobalCatalog contoso.com
   ```

   Cuando se le solicite, especifique la credencial para la cuenta de usuario que desea utilizar para el servicio Graph (por ejemplo, graphservice).

   > [!IMPORTANT]
   > Espere las credenciales emergentes (no se admite Get-Credential en el punto de conexión con privilegios) y escriba las credenciales de cuenta del servicio Graph.

#### <a name="graph-protocols-and-ports"></a>Puertos y protocolos de Graph

El servicio Graph en Azure Stack usa los protocolos y puertos siguientes para comunicarse con la instancia de Active Directory de destino:

|Tipo|Port|Protocol|
|---------|---------|---------|
|LDAP|389|TCP y UDP|
|SSL de LDAP|636|TCP|
|GC DE LDAP|3268|TCP|
|SSL de GC de LDAP|3269|TCP|

## <a name="setting-up-ad-fs-integration-by-downloading-federation-metadata"></a>Configuración de la integración de AD FS mediante la descarga de metadatos de federación

Se requiere la siguiente información como entrada para los parámetros de automatización:

|Parámetro|Description|Ejemplo|
|---------|---------|---------|
|CustomAdfsName|Nombre del proveedor de notificaciones. <cr>Aparece de este modo en la página de aterrizaje de AD FS.|Contoso|
|CustomAD<br>FSFederationMetadataEndpointUri|Vínculo de metadatos de federación|https://ad01.contoso.com/federationmetadata/2007-06/federationmetadata.xml|


### <a name="trigger-automation-to-configure-claims-provider-trust-in-azure-stack"></a>Automatización de desencadenador para configurar la relación de confianza de proveedor de notificaciones en Azure Stack

Para este procedimiento, use un equipo de la red del centro de datos que pueda comunicarse con el punto de conexión con privilegios de Azure Stack. Se espera que el certificado utilizado por la instancia de **AD FS del servicio de token de seguridad** de la cuenta sea de confianza para Azure Stack.

1. Abra una sesión de Windows PowerShell con privilegios elevados y conéctese al punto de conexión con privilegios.

   ```powershell
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. Ahora que está conectado al punto de conexión con privilegios, ejecute el comando siguiente con los parámetros adecuados para su entorno:

   ```powershell
   Register-CustomAdfs -CustomAdfsName Contoso -CustomADFSFederationMetadataEndpointUri https://win-SQOOJN70SGL.contoso.com/federationmetadata/2007-06/federationmetadata.xml
   ```

3. Ejecute el siguiente comando para actualizar el propietario de la suscripción del proveedor predeterminado, con los parámetros adecuados para su entorno:

   ```powershell
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "administrator@contoso.com"
   ```

## <a name="setting-up-ad-fs-integration-by-providing-federation-metadata-file"></a>Configuración de la integración de AD FS mediante el archivo de metadatos de federación

Utilice este método si se cumple alguna de las condiciones siguientes:

- La cadena de certificados es diferente para AD FS, en comparación con todos los demás puntos de conexión de Azure Stack.
- No hay ninguna conectividad de red para el servidor de AD FS existente desde la instancia de AD FS de Azure Stack.

Se requiere la siguiente información como entrada para los parámetros de automatización:


|Parámetro|Description|Ejemplo|
|---------|---------|---------|
|CustomAdfsName|Nombre del proveedor de notificaciones. Aparece de este modo en la página de aterrizaje de AD FS.|Contoso|
|CustomADFSFederationMetadataFile|Archivo de metadatos de federación|https://ad01.contoso.com/federationmetadata/2007-06/federationmetadata.xml|

### <a name="create-federation-metadata-file"></a>Creación de un archivo de metadatos de federación

Para el siguiente procedimiento, debe usar un equipo que tenga conectividad de red a la implementación de AD FS existente, que se convierte en el servicio de token de seguridad de la cuenta. Además, deben instalarse los certificados necesarios.

1. Abra una sesión de Windows PowerShell con privilegios elevados y ejecute el comando siguiente con los parámetros adecuados para su entorno:

   ```powershell
   [XML]$Metadata = Invoke-WebRequest -URI https://win-SQOOJN70SGL.contoso.com/federationmetadata/2007-06/federationmetadata.xml -UseBasicParsing

   $Metadata.outerxml|out-file c:\metadata.xml
   ```

2. Copie el archivo de metadatos en un recurso compartido que sea accesible desde el punto de conexión con privilegios.


### <a name="trigger-automation-to-configure-claims-provider-trust-in-azure-stack"></a>Automatización de desencadenador para configurar la relación de confianza de proveedor de notificaciones en Azure Stack

Para este procedimiento, use un equipo de la red del centro de datos que pueda comunicarse con el punto de conexión con privilegios de Azure Stack.

1. Abra una sesión de Windows PowerShell con privilegios elevados y conéctese al punto de conexión con privilegios.

   ```powershell
   $creds=Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. Ahora que está conectado al punto de conexión con privilegios, ejecute el comando siguiente con los parámetros adecuados para su entorno:

   ```powershell
   Register-CustomAdfs -CustomAdfsName Contoso – CustomADFSFederationMetadataFile \\share\metadataexample.xml
   ```

3. Ejecute el siguiente comando para actualizar el propietario de la suscripción del proveedor predeterminado, con los parámetros adecuados para su entorno:

   ```powershell
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "administrator@contoso.com"
   ```

## <a name="configure-relying-party-on-existing-ad-fs-deployment-account-sts"></a>Configuración del usuario de confianza en la implementación de AD FS existente (STS de cuenta)

Microsoft proporciona un script que configura la relación de confianza para usuario autenticado, incluidas las reglas de transformación de notificaciones. El uso del script es opcional, ya que se pueden ejecutar los comandos manualmente.

Puede descargar el script de la aplicación auxiliar desde las [herramientas de Azure Stack](https://github.com/Azure/AzureStack-Tools/tree/vnext/DatacenterIntegration/Identity) en Github.

Si decide ejecutar manualmente los comandos, siga estos pasos:

1. Copie el siguiente contenido en un archivo .txt (por ejemplo, guardado como c:\ClaimRules.txt) en la instancia de AD FS o como miembro de la granja de servidores del centro de datos:

   ```text
   @RuleTemplate = "LdapClaims"
   @RuleName = "Name claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"), query = ";userPrincipalName;{0}", param = c.Value);

   @RuleTemplate = "LdapClaims"
   @RuleName = "UPN claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn"), query = ";userPrincipalName;{0}", param = c.Value);

   @RuleTemplate = "LdapClaims"
   @RuleName = "ObjectID claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid"]
   => issue(Type = "http://schemas.microsoft.com/identity/claims/objectidentifier", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, Value = c.Value, ValueType = c.ValueType);

   @RuleName = "Family Name and Given claim"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]
   => issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname", "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"), query = ";sn,givenName;{0}", param = c.Value);

   @RuleTemplate = "PassThroughClaims"
   @RuleName = "Pass through all Group SID claims"
   c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"]
   => issue(claim = c);

   @RuleTemplate = "PassThroughClaims"
   @RuleName = "Pass through all windows account name claims"
   c:[Type == http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname]
   => issue(claim = c);
   ```

2. Para habilitar la autenticación basada en formularios Windows Forms, abra una sesión de Windows PowerShell como usuario con privilegios elevados y ejecute el siguiente comando:

   ```powershell
   Set-AdfsProperties -WIASupportedUserAgents @("MSAuthHost/1.0/In-Domain","MSIPC","Windows Rights Management Client","Kloud")
   ```

3. Para agregar la relación de confianza para usuario autenticado, ejecute el siguiente comando de Windows PowerShell en la instancia de AD FS o un miembro de la granja de servidores. Asegúrese de actualizar el punto de conexión de AD FS y seleccione el archivo creado en el paso 1.

   **Para AD FS 2016**

   ```powershell
   Add-ADFSRelyingPartyTrust -Name AzureStack -MetadataUrl "https://YourAzureStackADFSEndpoint/FederationMetadata/2007-06/FederationMetadata.xml" -IssuanceTransformRulesFile "C:\ClaimIssuanceRules.txt" -AutoUpdateEnabled:$true -MonitoringEnabled:$true -enabled:$true -AccessControlPolicyName "Permit everyone"
   ```

   **Para AD FS 2012/2012 R2**

   ```powershell
   Add-ADFSRelyingPartyTrust -Name AzureStack -MetadataUrl "https://YourAzureStackADFSEndpoint/FederationMetadata/2007-06/FederationMetadata.xml" -IssuanceTransformRulesFile "C:\ClaimIssuanceRules.txt" -AutoUpdateEnabled:$true -MonitoringEnabled:$true -enabled:$true
   ```

   > [!IMPORTANT]
   > Debe usar el complemento MMC de AD FS para configurar las reglas de autorización de emisión cuando se usa AD FS de Windows Server 2012 o 2012 R2.

4. Cuando se utiliza el explorador Internet Explorer o Edge para tener acceso a Azure Stack, debe omitir los enlaces de token. En caso contrario, se producirá un error al intentar iniciar sesión. En la instancia de AD FS o en un miembro de la granja de servidores, ejecute el siguiente comando:

   ```powershell
   Set-AdfsProperties -IgnoreTokenBinding $true
   ```

5. Para habilitar la actualización de tokens, abra una sesión de Windows PowerShell con privilegios elevados y ejecute el siguiente comando:

   ```powershell
   Set-ADFSRelyingPartyTrust -TargetName AzureStack -TokenLifeTime 1440
   ```

## <a name="spn-creation"></a>Creación de SPN

Hay muchos escenarios que requieren el uso de un nombre de entidad de seguridad de servicio (SPN) para la autenticación. A continuación se muestran algunos ejemplos.

- Uso de la CLI con la implementación de AD FS de Azure Stack
- Módulo de administración de System Center para Azure Stack cuando se implementa con AD FS
- Proveedores de recursos de Azure Stack cuando se implementan con AD FS
- Diversas aplicaciones
- Se requiere un inicio de sesión no interactivo.

Para más información sobre cómo crear un nombre de entidad de seguridad de servicio, consulte la sección [Crear una entidad de servicio para AD FS](https://docs.microsoft.com/azure/azure-stack/azure-stack-create-service-principals#create-service-principal-for-ad-fs).


## <a name="troubleshooting"></a>Solución de problemas

### <a name="configuration-rollback"></a>Reversión de la configuración

Si se produce un error que deja el entorno en un estado donde ya no se puede realizar la autenticación, está disponible una opción de reversión.

1. Abra una sesión de Windows PowerShell con privilegios elevados y ejecute el siguiente comando:

   ```powershell
   $creds = Get-Credential
   Enter-PSSession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. Después, ejecute el siguiente cmdlet:

   ```powershell
   Reset-DatacenterIntegationConfiguration
   ```

   Tras ejecutar la acción de reversión, todos los cambios de configuración se revierten. Solo es posible la autenticación con el usuario **CloudAdmin** integrado.

   > [!IMPORTANT]
   > Debe configurar el propietario original de la suscripción del proveedor predeterminado.

   ```powershell
   Set-ServiceAdminOwner -ServiceAdminOwnerUpn "azurestackadmin@[Internal Domain]"
   ```

### <a name="collecting-additional-logs"></a>Recopilación de registros adicionales

Si se produce un error en cualquiera de los cmdlets, puede recopilar registros adicionales mediante el cmdlet `Get-Azurestacklogs`.

1. Abra una sesión de Windows PowerShell con privilegios elevados y ejecute el siguiente comando:

   ```powershell
   $creds = Get-Credential
   Enter-pssession -ComputerName <IP Address of ERCS> -ConfigurationName PrivilegedEndpoint -Credential $creds
   ```

2. Después, ejecute el cmdlet siguiente:

   ```powershell
   Get-AzureStackLog -OutputPath \\myworstation\AzureStackLogs -FilterByRole ECE
   ```


## <a name="next-steps"></a>Pasos siguientes

[Integración del centro de datos de Azure Stack: publicar puntos de conexión](azure-stack-integrate-endpoints.md)
