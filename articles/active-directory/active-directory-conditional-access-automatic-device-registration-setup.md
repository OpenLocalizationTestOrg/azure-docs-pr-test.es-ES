---
title: "aaaHow tooconfigure el registro automático de dispositivos Unidos a un dominio de Windows con Azure Active Directory | Documentos de Microsoft"
description: "Configurar los dispositivos de Windows Unidos a un dominio, tooregister automática y silenciosa con Azure Active Directory."
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
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a>Cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory

toouse [acceso condicional basado en dispositivos de Azure Active Directory](active-directory-conditional-access-azure-portal.md), los equipos deben registrarse con Azure Active Directory (Azure AD). Puede obtener una lista de dispositivos registrados en su organización mediante el uso de hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Hola [módulo de Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0). 

Este artículo proporciona pasos de Hola para configurar el registro automático de dispositivos Unidos a un dominio de Windows hello con Azure AD en su organización.


Para más información acerca de:

- Acceso condicional, consulte [Acceso condicional en Azure Active Directory: versión preliminar](active-directory-conditional-access-azure-portal.md). 
- Dispositivos Windows 10 en un área de trabajo de Hola y experiencias de hello mejorado cuando se registra con Azure AD, consulte [Windows 10 para empresa hello: usar dispositivos para el trabajo](active-directory-azureadjoin-windows10-devices-overview.md).
- Windows 10 Enterprise E3 en CSP, vea hello [Windows 10 Enterprise E3 en información general de CSP](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).


## <a name="before-you-begin"></a>Antes de empezar

Antes de empezar a configurar el registro automático de dispositivos Unidos a un dominio de Windows hello en su entorno, debe familiarizarse con las restricciones de Hola y escenarios de hello compatible.  

mejorar la legibilidad tooimprove Hola de descripciones de hello, en este tema se utiliza Hola después término: 

- **Dispositivos de Windows actuales** -este término hace referencia a los dispositivos Unidos a un toodomain ejecutan Windows 10 o Windows Server 2016.
- **Dispositivos de bajo nivel de Windows** -este término hace referencia tooall **admite** dispositivos Windows Unidos a un dominio que se está ejecutando Windows 10 ni Windows Server 2016.  


### <a name="windows-current-devices"></a>Dispositivos de Windows actuales

- Para dispositivos que ejecutan el sistema operativo de escritorio de Windows de hello, se recomienda usar la actualización de aniversario de Windows 10 (versión 1607) o una versión posterior. 
- Hola registro de dispositivos de Windows actuales **es** admite en entornos de no federadas, como las configuraciones de sincronización de hash de contraseña.  


### <a name="windows-down-level-devices"></a>Dispositivos de Windows de nivel inferior

- se admite Hola después de dispositivos de bajo nivel de Windows:
    - Windows 8.1
    - Windows 7
    - Windows Server 2012 R2
    - Windows Server 2012
    - Windows Server 2008 R2
- Hola registro de dispositivos de Windows inferiores **es** admite en entornos de no federadas a través de perfecta Single Sign On [Azure Active Directory sin problemas Single Sign-On](https://aka.ms/hybrid/sso).
- Hola registro de dispositivos de Windows inferiores **no es** compatible con dispositivos con perfiles móviles. Si confía en la itinerancia de la configuración o de los perfiles, use Windows 10.



## <a name="prerequisites"></a>Requisitos previos

Antes de empezar a habilitar el registro automático de Hola de dispositivos Unidos a un dominio de su organización, deberá toomake seguro de que está ejecutando una versión actualizada de Azure AD conectarse.

Azure AD Connect:

- Mantiene la asociación de hello entre la cuenta de equipo de hello en el local de Active Directory (AD) y el objeto de dispositivo de hello en Azure AD. 
- Habilita otras características relacionadas del dispositivo como Windows Hello para empresas.



## <a name="configuration-steps"></a>Pasos de configuración

Este tema incluye los pasos de hello necesaria para todos los escenarios de configuración típica.  
Usar hello después de la tabla tooget una visión general de los pasos de Hola que son necesarios para su escenario:  



| Pasos                                      | Dispositivos actuales de Windows y sincronización de hash de contraseña | Dispositivos actuales de Windows y federación | Dispositivos de Windows de nivel inferior |
| :--                                        | :-:                                    | :-:                            | :-:                |
| Paso 1: Configuración del punto de conexión de servicio | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| Paso 2: Configuración de la emisión de notificaciones           |                                        | ![Comprobar][1]                    | ![Comprobar][1]        |
| Paso 3: Habilitación de dispositivos que no tengan Windows 10      |                                        |                                | ![Comprobar][1]        |
| Paso 4: Control de implementación y lanzamiento     | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |
| Paso 5: Comprobación de los dispositivos registrados          | ![Comprobar][1]                            | ![Comprobar][1]                    | ![Comprobar][1]        |



## <a name="step-1-configure-service-connection-point"></a>Paso 1: Configurar el punto de conexión de servicio

objeto de punto de conexión de servicio de Hola se usa por sus dispositivos durante el registro de hello toodiscover información del inquilino de Azure AD. En el local Active Directory (AD), objeto SCP de hello para el registro automático de Hola de dispositivos Unidos a un dominio debe existir en hello nomenclatura contexto partición de configuración bosque del equipo de hello. Hay solo un contexto de nomenclatura de configuración por bosque. En una configuración de Active Directory de bosques múltiples, el punto de conexión de servicio de hello debe existir en todos los bosques que contienen equipos unidos a un dominio.

Puede usar hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve Hola configuración contexto de nomenclatura de su bosque.  

Para un bosque con el nombre de dominio de Active Directory de hello *fabrikam.com*, contexto de nomenclatura de configuración de hello es:

`CN=Configuration,DC=fabrikam,DC=com`

En el bosque, objeto de hello SCP para hello el registro automático de dispositivos Unidos a un dominio se encuentra en:  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

Según cómo ha implementado Azure AD Connect, objeto SCP de hello puede que ya se configuraron.
Puede comprobar la existencia de hello del objeto de Hola y recuperar los valores de detección de hello mediante Hola siguiente secuencia de comandos de Windows PowerShell: 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

Hola **$scp. Palabras clave** salida muestra información del inquilino hello Azure AD, por ejemplo:

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

Si no existe el punto de conexión de servicio de hello, puede crear mediante la ejecución de hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet en el servidor de Azure AD Connect. Credenciales de administrador de empresa es necesario toorun este cmdlet.  
Hola cmdlet:

- Crea el punto de conexión de servicio de hello en el bosque de Active Directory de hello A que Azure AD Connect está conectado. 
- Requiere toospecify hello `AdConnectorAccount` parámetro. Esta es la cuenta de hello que está configurada como cuenta de conector de Azure AD conectarse de Active Directory. 


Hello secuencia de comandos siguiente muestra un ejemplo para usar el cmdlet de Hola. En esta secuencia de comandos, `$aadAdminCred = Get-Credential` requiere tootype un nombre de usuario. Necesita el nombre de usuario de hello tooprovide en formato de nombre principal (UPN) del usuario de hello (`user@example.com`). 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

Hola `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:

- Usa el módulo de Active Directory PowerShell hello, que se basa en los servicios Web de Active Directory ejecutándose en un controlador de dominio. Active Directory Web Services es compatible con los controladores de dominio en los que se ejecuta Windows Server 2008 R2, y las versiones posteriores.
- Solo es compatible con hello **MSOnline PowerShell versión del módulo 1.1.166.0**. toodownload este módulo, utilícelo [vínculo](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).   

Controladores de dominio ejecutan Windows Server 2008 o versiones anteriores, usar script de Hola por debajo del punto de conexión de servicio de toocreate Hola.

En una configuración de varios bosques, debe usar Hola después de la secuencia de comandos toocreate Hola service connection point en cada bosque donde existen equipos:
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a>Paso 2: Configuración de la emisión de notificaciones

De Azure federado utilizan los dispositivos de la configuración de AD, en los servicios de federación de Active Directory (AD FS) o una entidad 3rd tooAzure de tooauthenticate de servicio de federación AD local. Los dispositivos autentican tooget un tooregister de token de acceso con hello Azure Active Directory Device Registration Service (Azure DRS).

Dispositivos actuales autentican mediante autenticación de Windows integrada tooan WS-Trust extremo activo (versiones 1.3 o 2005) hospedada por el servicio de federación de hello local de Windows.

> [!NOTE]
> Si se usa AD FS, es preciso habilitar **adfs/services/trust/13/windowstransport** o **adfs/services/trust/2005/windowstransport**. Si usas hello Web autenticación Proxy, asegurarse de que este extremo se publica a través de proxy de Hola. Puede ver qué extremos están habilitadas a través de la consola de administración de AD FS de hello en **servicio > extremos**.
>
>Si no dispone de AD FS como el servicio de federación local, siga las instrucciones de Hola de su toomake de proveedores que admiten WS-Trust 1.3 o extremos de 2005 y que se publican a través de hello archivo de intercambio de metadatos (MEX).

Hello deben existir siguientes notificaciones en el símbolo (token) de hello recibido por Azure DRS para toocomplete de registro de dispositivo. DRS Azure creará un objeto de dispositivo en Azure AD con parte de esta información que se usa por objeto de dispositivo de Azure AD Connect tooassociate Hola recién creado con hello equipo cuenta local.

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

Si tiene más de un nombre de dominio comprobado, debe hello tooprovide después de la notificación para equipos:

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

Si ya esté emitiendo una notificación de ImmutableID (p. ej., Id. de inicio de sesión alternativo) debe tooprovide una notificación correspondiente para los equipos:

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

En las secciones siguientes de hello, encontrará información sobre:
 
- valores de Hello deben tener todas las notificaciones
- El aspecto de una definición en AD FS

definición de Hello ayuda a tooverify si los valores de hello están presentes, o si necesita toocreate ellos.

> [!NOTE]
> Si no utiliza AD FS para el servidor de federación local, siga tooissue configuración adecuada de su proveedor instrucciones toocreate Hola estas notificaciones.

### <a name="issue-account-type-claim"></a>Emisión de notificación de tipo de cuenta

**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-Esta notificación debe contener un valor de **DJ**, que identifica el dispositivo de Hola como un equipo unido al dominio. En AD FS, puede agregar una regla de transformación de emisión como esta:

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a>Emitir objectGUID de hello equipo cuenta local

**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-Esta notificación debe contener hello **objectGUID** valor de hello cuenta de equipo local. En AD FS, puede agregar una regla de transformación de emisión como esta:

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a>Emitir objectSID de hello equipo cuenta local

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-Esta notificación debe contener Hola Hola **objectSid** valor de hello cuenta de equipo local. En AD FS, puede agregar una regla de transformación de emisión como esta:

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a>Emisión de issuerID para un equipo cuando haty varios nombres de dominio comprobados en Azure AD

**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-Esta notificación debe contener Hola identificador uniforme de recursos (URI) de cualquiera de hello comprobar nombres de dominio que se conectan con hello federation service (AD FS o 3ª parte) emisora Hola símbolo (token) local. En AD FS, puede agregar reglas de transformación que parecen los Hola siguiente en ese orden específico después Hola los anteriores. Tenga en cuenta que una regla tooexplicitly problema Hola regla para los usuarios es necesario. En reglas de Hola a continuación, se agrega una regla primera identificación de usuario frente a la autenticación del equipo.

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


En la notificación de hello anterior,

- `$<domain>`es la dirección URL del servicio de hello AD FS
- `<verified-domain-name>`es un marcador de posición que necesita tooreplace con uno de los nombres de dominio comprobado en Azure AD



Para obtener más información acerca de los nombres de dominio comprobado, consulte [agregar un tooAzure de nombre de dominio personalizado Active Directory](active-directory-add-domain.md).  
tooget una lista de los dominios de la compañía comprobados, puede usar hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet. 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a>Emisión de ImmutableID para un equipo cuando existe uno para los usuarios (por ejemplo, se ha establecido el identificador de inicio de sesión alternativo)

**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**: esta notificación debe contener un valor válido para los equipos. En AD FS, se puede crear una regla de transformación de emisión como se indica a continuación:

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a>Aplicación auxiliar script toocreate Hola AD FS reglas de transformación

Hello siguiente secuencia de comandos le ayuda con la creación de hello de emisión de hello transformar las reglas descritas anteriormente.

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a>Comentarios 

- Este script anexa reglas existentes de hello reglas toohello. Script de Hola no se ejecutan dos veces porque Hola un conjunto de reglas se debe agregar dos veces. Asegúrese de que no existe ninguna regla correspondiente de estas notificaciones (condiciones Hola correspondiente) antes de ejecutar script de Hola de nuevo.

- Si tiene varios nombres de dominio verificado (como se muestra en el portal de hello Azure AD o a través del cmdlet Get-MsolDomains Hola), establecer valor de Hola de **$multipleVerifiedDomainNames** Hola script demasiado**$true**. Además, asegúrese de que quita cualquier notificación issuerid existente que pueda haber creado Azure AD Connect o a través de otros medios. Este es un ejemplo de esta regla:


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- Si ya ha emitido una **ImmutableID** de notificación para las cuentas de usuario, establezca el valor de Hola de **$immutableIDAlreadyIssuedforUsers** Hola script demasiado**$true**.

## <a name="step-3-enable-windows-down-level-devices"></a>Paso 3: Habilitación de dispositivos de Windows de nivel inferior

Si algunos de los dispositivos unidos a un dominio son dispositivos de Windows de nivel inferior, necesitará:

- Establecer una directiva de Azure AD tooenable tooregister dispositivos de los usuarios.
 
- Configurar el toosupport de notificaciones local tooissue de servicio de federación **autenticación de Windows integrada (IWA)** para el registro de dispositivos.
 
- Agregue hello Azure AD dispositivo autenticación extremo toohello local Intranet zonas tooavoid certificado pide al autenticar el dispositivo de Hola.

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a>Establezca la directiva en Azure AD tooenable dispositivos de los usuarios tooregister

dispositivos de nivel inferior de tooregister Windows, debe toomake que ese Hola establecer a tooallow usuarios tooregister dispositivos en Azure AD esté establecido. Hola portal de Azure, puede encontrar esta configuración en:

`Azure Active Directory > Users and groups > Device settings`
    
Hello siguiente directiva debe establecerse demasiado**todos los**: **los usuarios pueden registrar sus dispositivos con Azure AD**

![Registro de dispositivos](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a>Configuración de un servicio de federación local 

El servicio de federación local debe ser compatible con hello emisora **authenticationmehod** y **wiaormultiauthn** notificaciones al recibir una autenticación solicitud de usuario de confianza de Azure AD toohello que contiene un resouce_params parámetro con un valor codificado como se muestra a continuación:

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

Cuando llega una solicitud de este tipo, servicio de federación local Hola debe autenticar usuario hello mediante la autenticación integrada de Windows y cuando se realiza correctamente, debe emitir Hola siguiendo dos notificaciones:

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

En AD FS, debe agregar ese método de autenticación de hello pasa a través de una regla de transformación de emisión.  

**tooadd esta regla:**

1. En la consola de administración de hello AD FS, vaya demasiado`AD FS > Trust Relationships > Relying Party Trusts`.
2. Haga clic en hello plataforma de identidad de Microsoft Office 365 confianza para usuario autenticado y, a continuación, seleccione **editar reglas de notificación**.
3. En hello **reglas de transformación de emisión** ficha, seleccione **Agregar regla**.
4. Hola **regla de notificación** lista de plantillas, seleccione **enviar notificaciones mediante una regla personalizada**.
5. Seleccione **Siguiente**.
6. Hola **nombre de la regla de notificación** , escriba **Auth Method Claim Rule**.
7. Hola **regla de notificación** cuadro, Hola de tipo siguiente regla:

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. En el servidor de federación, escriba el comando de PowerShell de Hola a continuación después de reemplazar ** \<RPObjectName\> ** con nombre de objeto de usuario autenticado de Hola para su Azure AD confianza para usuario autenticado. Normalmente, este objeto se llama **Plataforma de identidad de Microsoft Office 365**.
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a>Agregar zonas de Intranet Local de hello Azure AD dispositivo autenticación extremo toohello

certificado tooavoid pide al autentican a los usuarios de dispositivos de registro tooAzure AD puede insertar un hello tooadd de directiva tooyour dispositivos Unidos a un dominio después de la zona de Intranet Local toohello de dirección URL en Internet Explorer:

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a>Paso 4: Control de implementación y lanzamiento

Cuando se hayan completado los pasos necesario de hello, los dispositivos Unidos a un dominio son register tooautomatically listo con Azure AD. Todos los dispositivos unidos a un dominio en que se ejecuten la Actualización de aniversario de Windows 10 y Windows Server 2016 se registran automáticamente en Azure AD cuando el dispositivo se reinicie o el usuario inicie sesión. Registran nuevos dispositivos con Azure AD al dispositivo de hello reinicia una vez completada la operación de unión de dominio de Hola.

Dispositivos que estaban previamente unido al área de trabajo tooAzure AD (por ejemplo, para Intune) transición demasiado"*Unidos a un dominio, registrado en AAD*"; sin embargo tarda algún tiempo para este proceso toocomplete en todos los dispositivos pendientes toohello normal flujo de actividad de usuario y dominio.

### <a name="remarks"></a>Comentarios

- Puede usar una implementación de Hola de toocontrol de objeto de directiva de grupo de registro automático de Windows 10 y equipos unidos a un dominio de Windows Server 2016.

- Windows 10 de noviembre de 2015 actualización automáticamente registros con Azure AD **sólo** si se establece el objeto de directiva de grupo de implementación de Hola.

- toorollout Hola el registro automático de los equipos de nivel inferior de Windows, puede implementar un [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) toocomputers que seleccione.

- Si se insertan Hola directiva de grupo objeto tooWindows 8.1 dispositivos Unidos a dominio, se volverá a intentar el registro; Sin embargo, se recomienda que utilice hello [paquete de Windows Installer](#windows-installer-packages-for-non-windows-10-computers) tooregister todos los dispositivos de bajo nivel de Windows. 

### <a name="create-a-group-policy-object"></a>Creación de un objeto de directiva de grupo 

implementación de hello toocontrol de inscripción automática de equipos actuales de Windows, debe implementar hello **registrar equipos unidos a un dominio como dispositivos** dispositivos de toohello de objeto de directiva de grupo que desee tooregister. Por ejemplo, puede implementar el grupo de seguridad de tooa o unidad organizativa de hello directiva tooan.

**Directiva de Hola tooset:**

1. Abra **el administrador del servidor**y, a continuación, vaya demasiado`Tools > Group Policy Management`.
2. Vaya toohello nodo del dominio que se corresponde el dominio toohello donde desea que el registro automático de tooactivate de equipos de Windows actuales.
3. Haga clic con el botón derecho en **Objetos de directiva de grupo** y seleccione **Nuevo**.
4. Escriba un nombre para el objeto de directiva de grupo. Por ejemplo, *tooAzure el registro automático AD*. Seleccione **Aceptar**.
5. Haga clic con el botón derecho en el nuevo objeto de directiva de grupo y seleccione **Editar**.
6. Vaya demasiado**configuración del equipo** > **directivas** > **plantillas administrativas** > **Windows Componentes** > **el registro de dispositivos**. Haga clic con el botón derecho en **Registrar los equipos asociados a un dominio como dispositivos** y seleccione **Editar**.
   
   > [!NOTE]
   > Esta plantilla de directiva de grupo se ha cambiado desde las versiones anteriores de la consola de administración de directivas de grupo de Hola. Si está utilizando una versión anterior de la consola de hello, vaya demasiado`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`. 

7. Seleccione **Habilitado** y luego **Aplicar**.
8. Seleccione **Aceptar**.
9. Hola de vínculo tooa ubicación de objeto de directiva de grupo de su elección. Por ejemplo, puede vincular tooa determinada unidad organizativa. También puede vincularlo tooa el grupo de seguridad específico de equipos que se registren automáticamente con Azure AD. tooset esta directiva para todos los equipos de Windows 10 y Windows Server 2016 Unidos a un dominio de su organización, dominio de toohello de objeto de directiva de grupo de Hola de vínculo.

### <a name="windows-installer-packages-for-non-windows-10-computers"></a>Paquetes de Windows Installer para equipos sin Windows 10

equipos unidos a un dominio de nivel inferior de Windows de tooregister en un entorno federado, puede descargar e instalar estos paquetes de Windows Installer (.msi) desde el centro de descarga en hello [área de trabajo de Microsoft para equipos que no sean Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554) página.

Puede implementar el paquete de hello mediante el uso de un sistema de distribución de software como System Center Configuration Manager. paquete Hello admite opciones de instalación silenciosa estándar Hola con hello *silencioso* parámetro. Rama actual de System Center Configuration Manager ofrece ventajas adicionales de versiones anteriores, como registros de hello capacidad tootrack completado. Para más información, consulte [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).

instalador de Hello crea una tarea programada en sistema de Hola que se ejecuta en el contexto del usuario de Hola. tarea Hello se desencadena cuando Hola usuario inicia sesión en tooWindows. tarea Hello registra automáticamente el dispositivo de hello con Azure AD con credenciales de usuario de hello tras la autenticación mediante la autenticación integrada de Windows. toosee tarea programada de hello, en el dispositivo de hello, vaya demasiado**Microsoft** > **unión**, y, a continuación, vaya biblioteca del programador de tareas de toohello.

## <a name="step-5-verify-registered-devices"></a>Paso 5: Comprobación de los dispositivos registrados

Puede comprobar los dispositivos registrados correctamente en su organización mediante hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet Hola [módulo de Azure Active Directory PowerShell](/powershell/azure/install-msonlinev1?view=azureadps-2.0).

salida de Hello de este cmdlet muestra dispositivos registrados en Azure AD. tooget todos los dispositivos, use hello **-todos los** parámetro y, a continuación, filtrar mediante hello **deviceTrustType** propiedad. Los dispositivos unidos a un dominio tienen el valor **Unido a dominio**.

## <a name="next-steps"></a>Pasos siguientes

* [Azure Active Directory automatic device registration FAQ](active-directory-device-registration-faq.md) (Preguntas más frecuentes acerca del registro automático de dispositivos)
* [Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md)
* [Solución de problemas de registro automático de dominio unido equipos tooAzure AD – distinta de Windows 10](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [Acceso condicional de Azure Active Directory](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
