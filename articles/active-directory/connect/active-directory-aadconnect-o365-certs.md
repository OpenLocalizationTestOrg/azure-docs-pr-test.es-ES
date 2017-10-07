---
title: "renovación de aaaCertificate para los usuarios de Office 365 y Azure AD | Documentos de Microsoft"
description: "Este artículo explica tooOffice 365 a los usuarios cómo tooresolve problemas con mensajes de correo electrónico que notificarán sobre cómo renovar un certificado."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 543b7dc1-ccc9-407f-85a1-a9944c0ba1be
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b9b309e06949dc5488cd628650be413f366ed347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="renew-federation-certificates-for-office-365-and-azure-active-directory"></a>Renovación de certificados de federación para Office 365 y Azure Active Directory
## <a name="overview"></a>Información general
Para la federación correcta entre Azure Active Directory (Azure AD) y los servicios de federación de Active Directory (AD FS), certificados de hello utilizados por tooAzure de tokens de seguridad de AD FS toosign AD deben coincidir con lo que está configurado en Azure AD. Si hay alguna incoherencia puede provocar toobroken confianza. Azure AD garantiza que esta información se mantiene sincronizada cuando se implementa AD FS y Proxy de aplicación web (para el acceso de extranet).

Este artículo proporciona toomanage de información adicional los certificados de firma de tokens y mantenerlos sincronizados con Azure AD, en hello casos siguientes:

* Va a implementar Hola Proxy de aplicación Web y, por tanto, no están disponible en hello extranet Hola metadatos de federación.
* No se usa la configuración predeterminada de Hola de AD FS para certificados de firma de tokens.
* Utiliza un proveedor de identidades de terceros.

## <a name="default-configuration-of-ad-fs-for-token-signing-certificates"></a>Configuración predeterminada de AD FS para los certificados de firma de tokens
firma de tokens de Hola y el token de descifrado de certificados son normalmente los certificados autofirmados y son buenos para un año. De forma predeterminada, AD FS incluye un proceso de renovación automática llamado **AutoCertificateRollover**. Si utiliza AD FS 2.0 o versiones posteriores, Office 365 y Azure AD actualizan automáticamente el certificado antes de que expire.

### <a name="renewal-notification-from-hello-office-365-portal-or-an-email"></a>Notificaciones de renovación de portal de Office 365 Hola o un correo electrónico
> [!NOTE]
> Si ha recibido un correo electrónico o una notificación de portal que le pide que toorenew el certificado para Office, consulte [cambia de administrar certificados de firma de tootoken](#managecerts) toocheck si necesita tootake ninguna acción. Microsoft es consciente de un posible problema que puede provocar toonotifications para la renovación de certificados que se envió, incluso cuando no se requiere ninguna acción.
>
>

Azure AD intentos de metadatos de federación de hello toomonitor y símbolo (token) de Hola de actualización de certificados de firma, como se indica en estos metadatos. 30 días antes de que caduque Hola de certificados de firma de tokens de hello Azure AD comprueba si nuevos certificados están disponibles por sondeo en los metadatos de federación de Hola.

* Si puede sondear los metadatos de federación de Hola y recuperar nuevos certificados de hello correctamente, ninguna notificación por correo electrónico o una advertencia en el portal de Office 365 Hola se emite toohello usuario.
* Si no se puede recuperar los certificados de firma de token nuevo de Hola, ya sea porque los metadatos de federación de hello no están accesible o no está habilitada la sustitución automática de certificados, Azure AD emite una notificación por correo electrónico y una advertencia en el portal de Office 365 Hola.

![Notificación del portal de Office 365](./media/active-directory-aadconnect-o365-certs/notification.png)

> [!IMPORTANT]
> Si utilizas AD FS, continuidad del negocio tooensure, compruebe que los servidores tienen Hola después de las actualizaciones de modo que no se producen errores de autenticación para los problemas conocidos. Esta acción mitiga los problemas conocidos del servidor de proxy de AD FS para esta renovación y períodos de renovación futuros:
>
> Server 2012 R2: [paquete acumulativo de mayo de 2014 de Windows Server](http://support.microsoft.com/kb/2955164)
>
> Server 2008 R2 y 2012: [Se produce un error en la autenticación a través de proxy en Windows Server 2012 o Windows Server 2008 R2 SP1](http://support.microsoft.com/kb/3094446)
>
>

## Comprobar si los certificados de hello necesitan toobe actualizado<a name="managecerts"></a>
### <a name="step-1-check-hello-autocertificaterollover-state"></a>Paso 1: Comprobar el estado de AutoCertificateRollover Hola
En el servidor de AD FS, abra Powershell. Compruebe que el valor de AutoCertificateRollover de hello está establecido tooTrue.

    Get-Adfsproperties

![AutoCertificateRollover](./media/active-directory-aadconnect-o365-certs/autocertrollover.png)

>[!NOTE] 
>Si usa AD FS 2.0, ejecute primero Add-Pssnapin Microsoft.Adfs.Powershell.

### <a name="step-2-confirm-that-ad-fs-and-azure-ad-are-in-sync"></a>Paso 2: Confirmar que AD FS y Azure AD están sincronizados
En el servidor de AD FS, abra el símbolo del sistema de hello Azure AD PowerShell y conectar tooAzure AD.

> [!NOTE]
> Puede descargar Azure AD PowerShell [aquí](https://technet.microsoft.com/library/jj151815.aspx).
>
>

    Connect-MsolService

Comprobar certificados Hola configuran en AD FS y especifica las propiedades de confianza de Azure AD para hello dominio.

    Get-MsolFederationProperty -DomainName <domain.name> | FL Source, TokenSigningCertificate

![Get-MsolFederationProperty](./media/active-directory-aadconnect-o365-certs/certsync.png)

Si las huellas digitales de hello en ambas Hola salidas coincidencia, los certificados estén sincronizados con Azure AD.

### <a name="step-3-check-if-your-certificate-is-about-tooexpire"></a>Paso 3: Comprobar si el certificado es sobre tooexpire
En la salida de hello de Get-MsolFederationProperty o Get-AdfsCertificate, busque la fecha de hello en "No After". Si la fecha de hello es inferior a 30 días, que debería adoptar medidas.

| AutoCertificateRollover | Certificados sincronizados con Azure AD | Los metadatos de federación están disponibles públicamente | Validez | Acción |
|:---:|:---:|:---:|:---:|:---:|
| Sí |Sí |Sí |- |No se requiere ninguna acción. Consulte [Renovación automática de certificados de firma de tokens](#autorenew). |
| Sí |No |- |Menos de 15 días |Renovar inmediatamente. Consulte [Renovación manual de certificados de firma de tokens](#manualrenew). |
| No |- |- |Menos de 30 días |Renovar inmediatamente. Consulte [Renovación manual de certificados de firma de tokens](#manualrenew). |

\[-] No importa

## Renovar automáticamente los certificados de firma de tokens de hello (recomendado)<a name="autorenew"></a>
No es necesario tooperform ningún paso manual si se cumplen los siguientes hello:

* Ha implementado el Proxy de aplicación Web, lo que hace posible el acceso a metadatos de federación toohello de hello extranet.
* Usa la configuración predeterminada de hello AD FS (AutoCertificateRollover está habilitado).

Hola de comprobación siguientes tooconfirm que Hola certificado puede actualizarse automáticamente.

**1. Hola propiedad AutoCertificateRollover de AD FS se debe establecer tooTrue.** Esto indica que AD FS generará automáticamente nuevos certificados de firma y descifrado de tokens, antes de hello antiguo los punto de expirar.

**2. metadatos de federación de Hola AD FS están accesible públicamente.** Compruebe que los metadatos de federación están accesible públicamente desplazándose toohello siguiente dirección URL desde un equipo de Hola internet pública (fuera de la red corporativa de hello):

https://(your_FS_name)/federationmetadata/2007-06/federationmetadata.xml

donde `(your_FS_name) `se sustituye por el nombre de host del servicio de federación de hello usa su organización, por ejemplo, fs.contoso.com.  Si es capaz de tooverify ambos de estos valores correctamente, no tiene toodo cualquier otra cosa.  

Ejemplo: https://fs.contoso.com/federationmetadata/2007-06/federationmetadata.xml

## Renovar manualmente los certificados de firma de tokens de Hola<a name="manualrenew"></a>
Puede elegir toorenew certificados de firma de tokens de hello manualmente. Por ejemplo, hello escenarios siguientes podrían funcionar mejor para la renovación manual:

* Los certificados de firma de tokens no son certificados autofirmados. Hola más comunes motivo es que su organización administra los certificados de AD FS inscritos desde una entidad de certificación de organización.
* Seguridad de red no permite toobe de metadatos de federación de hello disponible públicamente.

En estos casos, cada vez que actualice los certificados de firma de tokens de hello también debe actualizar el dominio de Office 365 mediante el uso de comandos de PowerShell de hello, Update-MsolFederatedDomain.

### <a name="step-1-ensure-that-ad-fs-has-new-token-signing-certificates"></a>Paso 1: Asegurarse de que AD FS tiene nuevos certificados de firma de tokens
**Configuración no predeterminada**

Si está utilizando una configuración no predeterminada de AD FS (donde **AutoCertificateRollover** se establece demasiado**False**), probablemente esté utilizando certificados personalizados (no autofirmados). Para obtener más información acerca de cómo toorenew Hola AD FS firma de tokens de certificados, consulte [certificados autofirmados de orientación para los clientes que no usan AD FS](https://msdn.microsoft.com/library/azure/JJ933264.aspx#BKMK_NotADFSCert).

**Los metadatos de federación no están disponibles públicamente**

Hola en otra parte, si **AutoCertificateRollover** se establece demasiado**True**, pero los metadatos de federación no están accesible públicamente, asegúrese de que los certificados de firma de token nuevo que haya generado en AD FS. Confirme que tiene nuevo token de firma de certificados por hello realizar pasos:

1. Compruebe que se registran en el servidor de toohello principal de AD FS.
2. Comprobar los certificados de firma actual de hello en AD FS, abra una ventana de comandos de PowerShell y ejecutando el siguiente comando de Hola:

    PS C:\>Get-ADFSCertificate –CertificateType token-signing

   > [!NOTE]
   > Si usa AD FS 2.0, tendrá que ejecutar Add-Pssnapin Microsoft.Adfs.Powershell primero.
   >
   >
3. Mire el resultado del comando hello en los certificados que se muestran. Si AD FS ha generado un nuevo certificado, debería ver dos certificados en la salida de hello: uno para qué hello **IsPrimary** valor es **True** hello y **NotAfter** fecha es dentro de 5 días y uno para el que **IsPrimary** es **False** y **NotAfter** es aproximadamente un año en hello futuras.
4. Si solo ve un certificado y Hola **NotAfter** fecha está dentro de 5 días, deberá toogenerate un nuevo certificado.
5. toogenerate un nuevo certificado, ejecutar el siguiente comando en un símbolo del sistema de PowerShell de hello: `PS C:\>Update-ADFSCertificate –CertificateType token-signing`.
6. Comprobar Hola actualización ejecutando Hola siguiente nuevo comando: PS C:\>firma de tokens de Get-ADFSCertificate – CertificateType

Ahora deben aparecer dos certificados, uno de los cuales tiene un **NotAfter** fecha de aproximadamente un año en hello futura y para qué hello **IsPrimary** valor es **False**.

### <a name="step-2-update-hello-new-token-signing-certificates-for-hello-office-365-trust"></a>Paso 2: Actualizar el token nuevo de hello firmar los certificados de confianza de hello Office 365
Actualizar Office 365 con hello nuevo token firma certificados toobe destinada confianza hello, como se indica a continuación.

1. Abra Hola Microsoft Azure módulo Active Directory para Windows PowerShell.
2. Ejecute $cred=Get-Credential. Cuando este cmdlet le solicite las credenciales, escriba sus credenciales de cuenta de administrador de servicios en la nube.
3. Ejecute Connect-MsolService –Credential $cred. Este cmdlet conecta toohello servicio en la nube. Crear un contexto que le conecta toohello servicio en la nube es necesario antes de ejecutar cualquiera de hello cmdlets adicionales instalados por la herramienta de Hola.
4. Si se ejecutan estos comandos en un equipo que no sea servidor de federación principal de hello AD FS, ejecute Set-MSOLAdfscontext-equipo <AD FS primary server>, donde <AD FS primary server> es Hola de nombre de dominio completo interno del servidor de hello principal de AD FS. Este cmdlet crea un contexto que le conecta tooAD FS.
5. Ejecute Update-MSOLFederatedDomain –DomainName <domain>. Este cmdlet actualiza la configuración de Hola de AD FS en servicio de nube de Hola y configura la relación de confianza de hello entre Hola dos.

> [!NOTE]
> Si necesita toosupport varios dominios de nivel superior, como contoso.com y fabrikam.com, debe usar hello **SupportMultipleDomain** cambiar con cualquier cmdlet. Para más información, consulte [Support for Multiple Top Level Domains](active-directory-aadconnect-multiple-domains.md)(Compatibilidad con varios dominios de nivel superior).
>
>

## Reparar la relación de confianza de Azure AD con Azure AD Connect <a name="connectrenew"></a>
Si configuró la granja de servidores de AD FS y la confianza de Azure AD mediante el uso de Azure AD Connect, puede usar Azure AD Connect toodetect si necesita tootake ninguna acción para los certificados de firma de tokens. Si necesita certificados de hello toorenew, puede usar por lo que toodo de Azure AD Connect.

Para obtener más información, consulte [reparar confianza hello](active-directory-aadconnect-federation-management.md).
