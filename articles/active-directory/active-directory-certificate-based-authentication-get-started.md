---
title: "aaaAzure autenticación basada en certificados de Active Directory: Introducción | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooconfigure la autenticación basada en certificados en su entorno"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Introducción a la autenticación basada en certificados de Azure Active Directory

Autenticación basada en certificados le permite toobe autenticado por Azure Active Directory con un certificado de cliente en un dispositivo de Windows, Android o iOS cuando se conecte a su cuenta de Exchange online para: 

- aplicaciones móviles de Office como Microsoft Outlook y Microsoft Word,   

- clientes de Exchange ActiveSync (EAS). 

La configuración de esta característica elimina Hola necesidad tooenter un nombre de usuario y la combinación de contraseña en determinados correo electrónico y aplicaciones de Microsoft Office en su dispositivo móvil. 

En este tema:

- Proporciona hello tooconfigure los pasos y usar la autenticación basada en certificados para los usuarios de inquilinos de Office 365 Enterprise, Business, educación y planes de gobierno de Estados Unidos. Esta característica se encuentra disponible en versión preliminar en los planes Office 365 China, US Government Defense e US Government Federal. 

- Se supone que ya tiene una [infraestructura de clave pública (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) y [AD FS](connect/active-directory-aadconnectfed-whatis.md) configurados.    


## <a name="requirements"></a>Requisitos

autenticación basada en certificados tooconfigure, deben cumplirse Hola siguientes:  

- La autenticación basada en certificados (CBA) solo se admite para entornos federados de aplicaciones del explorador o clientes nativos que usan autenticación moderna (ADAL). Hola única excepción es Exchange Active Sync (EAS) para EXO que se puede usar para las cuentas de ambos, federadas y administradas. 

- entidad de certificación raíz de Hola y las entidades emisoras de certificados intermedios deben configurarse en Azure Active Directory.  

- Cada entidad de certificación debe tener una lista de revocación de certificados (CRL) a la que puede hacerse referencia a través de una dirección URL con conexión a Internet.  

- Debe tener al menos una entidad de certificación configurada en Azure Active Directory. Puede encontrar pasos relacionados en hello [configurar entidades emisoras de certificados de hello](#step-2-configure-the-certificate-authorities) sección.  

- Para los clientes de Exchange ActiveSync, certificado de cliente de hello debe tener enrutables correo electrónico Hola usuarios dirección de Exchange en línea en cualquier nombre de entidad de seguridad de Hola u Hola valor RFC822 nombre del campo de nombre alternativo del sujeto Hola. Azure Active Directory asigna atributo Hola RFC822 value toohello dirección de Proxy en el directorio de Hola.  

- El dispositivo de cliente debe tener acceso tooat lo menos una emisora que emite certificados de cliente.  

- Un certificado de cliente para la autenticación de cliente se debe haber emitido a tooyour cliente.  




## <a name="step-1-select-your-device-platform"></a>Paso 1: Selección de la plataforma de dispositivos

Como primer paso, para la plataforma de dispositivo de Hola que le interesa, necesita tooreview Hola siguiente:

- compatibilidad con aplicaciones móviles de Office de Hola 
- requisitos de implementación específica de Hola  

Hola relacionados existe información para hello después de plataformas de dispositivos:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Paso 2: Configurar entidades emisoras de certificados de Hola 

tooconfigure sus entidades emisoras de certificados en Active Directory de Azure, para cada entidad de certificación, cargar Hola siguientes: 

* Hola parte pública del certificado de hello, en *.cer* formato 
* Hello orientado a las direcciones URL donde hello Internet listas de revocación de certificados (CRL) residen

esquema de Hola para una entidad de certificación tiene el siguiente aspecto: 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

Para la configuración de hello, puede usar hello [Azure Active Directory PowerShell versión 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Inicie Windows PowerShell con privilegios de administrador. 
2. Instale el módulo de hello Azure AD. Necesita tooinstall versión [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) o superior.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Como primer paso de configuración, deberá tooestablish una conexión con su inquilino. Tan pronto como exista un inquilino de tooyour de conexión, puede revisar, agregar, eliminar y modificar las entidades emisoras de certificados de Hola de confianza que se definen en el directorio. 

### <a name="connect"></a>Conectar

una conexión con su inquilino, use hello tooestablish [conectar organización](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Recuperar 

tooretrieve Hola confianza entidades emisoras de certificados que se definen en el directorio, use hello [AzureADTrustedCertificateAuthority Get](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Sumar

toocreate una entidad de certificación de confianza, utilice hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet conjunto hello y **crlDistributionPoint** tooa correcta valor de atributo: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Remove

tooremove una entidad de certificación de confianza, utilice hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modificar

toomodify una entidad de certificación de confianza, utilice hello [AzureADTrustedCertificateAuthority conjunto](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Paso 3: Configuración de revocación

toorevoke un certificado de cliente, Azure Active Directory captura los certificados de hello lista de revocación (CRL) de las direcciones URL de hello cargado como parte de la información de entidad emisora de certificados y lo almacena en caché. Hola publicar última marca de tiempo (**fecha efectiva** propiedad) Hola CRL se utiliza tooensure Hola CRL sigue siendo válida. Hola CRL es toocertificates de acceso de toorevoke periódicamente que se hace referencia que forman parte de la lista de Hola.

Si es necesaria (por ejemplo, si un usuario pierde un dispositivo) una revocación más instantánea, se puede invalidar el token de autorización de saludo del usuario de Hola. tooinvalidate Hola autorización token, establezca Hola **StsRefreshTokenValidFrom** field para este usuario concreto con Windows PowerShell. Debe actualizar hello **StsRefreshTokenValidFrom** field para cada usuario que desea acceso toorevoke para.

tooensure que persiste revocación hello, debe establecer hello **fecha efectiva** de fecha de hello CRL tooa después del valor de hello establecido por **StsRefreshTokenValidFrom** y asegúrese de hello certificado en cuestión está en Hola CRL.

Hola siguiendo pasos esquema Hola proceso de actualización e invalidación token de autorización de Hola por establecer hello **StsRefreshTokenValidFrom** campo. 

**revocación de tooconfigure:** 

1. Conectar con el servicio de administración de credenciales toohello MSOL: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Recuperar el valor de StsRefreshTokensValidFrom actual de Hola de un usuario: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Configurar un nuevo valor de StsRefreshTokensValidFrom de marca de tiempo actual de hello usuario toohello iguales: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

fecha de Hello establecida debe estar en hello futuras. Si Hola fecha no tiene Hola futuras, Hola **StsRefreshTokensValidFrom** propiedad no está establecida. Si es fecha Hola Hola futuras, **StsRefreshTokensValidFrom** se establecen toohello hora actual (no la fecha de hello indicada por el comando Set-MsolUser). 


## <a name="step-4-test-your-configuration"></a>Paso 4: Prueba de la configuración

### <a name="testing-your-certificate"></a>Prueba del certificado

Como una primera prueba de configuración, debe intentar toosign en demasiado[Outlook Web Access](https://outlook.office365.com) o [SharePoint Online](https://microsoft.sharepoint.com) con su **explorador en el dispositivo**.

Si el inicio de sesión se realiza correctamente, sabrá que:

- certificado de usuario de Hello ha sido aprovisionado tooyour dispositivo de prueba
- AD FS está configurado correctamente.  


### <a name="testing-office-mobile-applications"></a>Prueba de aplicaciones móviles de Office

**autenticación basada en certificados tootest en la aplicación de Office mobile:** 

1. En el dispositivo de prueba, instale una aplicación móvil de Office (por ejemplo, OneDrive).
3. Inicie la aplicación hello. 
4. Escriba su nombre de usuario y, a continuación, seleccione el certificado de usuario de Hola que desea toouse. 

Debe haber iniciado sesión correctamente. 

### <a name="testing-exchange-activesync-client-applications"></a>Prueba de aplicaciones cliente de Exchange ActiveSync

tooaccess Exchange ActiveSync (EAS) mediante la autenticación basada en certificados, un perfil EAS que contiene el certificado de cliente de hello debe ser aplicación toohello disponible. 

Hola perfil EAS debe contener Hola siguiente información:

- Hola toobe de certificado de usuario utilizado para la autenticación 

- punto de conexión EAS de Hello (por ejemplo, outlook.office365.com)

Un perfil de EAS se puede configurar y colocar en dispositivo hello mediante la utilización de Hola de administración de dispositivos móviles (MDM) como Intune o colocando manualmente el certificado de Hola Hola perfil EAS en dispositivo Hola.  

### <a name="testing-eas-client-applications-on-android"></a>Prueba de aplicaciones cliente de EAS en Android

**autenticación de certificado de tootest:**  

1. Configurar un perfil EAS en aplicación Hola que satisface los requisitos de hello anteriores.  
2. Abra la aplicación hello y compruebe que está sincronizando el correo electrónico. 

