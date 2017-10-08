---
title: aaaAzure AD conectar varios dominios
description: "En este documento se describe cómo instalar y configurar varios dominios de nivel superior con O365 y Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Compatibilidad con varios dominios para la federación con Azure AD
Hello siguiente documentación proporciona orientación sobre cómo toouse varios dominios de nivel superior y subdominios al federarse con dominios de Office 365 o Azure AD.

## <a name="multiple-top-level-domain-support"></a>Compatibilidad con varios dominios de nivel superior
La federación de varios dominios de nivel superior con Azure AD requiere una configuración adicional que no es necesaria al federarse con un dominio de nivel superior.

Cuando un dominio está federado con Azure AD, se establecen varias propiedades en el dominio de hello en Azure.  Una propiedad importante es IssuerUri.  Se trata de un URI que se usa por Azure AD tooidentify dominio de Hola que Hola token está asociado.  Hola URI no es necesario tooresolve tooanything pero debe ser un URI válido.  De forma predeterminada, Azure AD establece toohello el valor de identificador de servicio de federación de hello en sus instalaciones en AD FS configuration.

> [!NOTE]
> identificador del servicio de federación Hello es un URI que identifica de forma única un servicio de federación.  servicio de federación de Hello es una instancia de AD FS que funcione como servicio de token de seguridad de Hola. 
> 
> 

También puede ver IssuerUri mediante comandos de PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

El problema surge si queremos tooadd más de un dominio de nivel superior.  Por ejemplo, supongamos que ha configurado la federación entre Azure AD y el entorno local.  Para este documento uso bmcontoso.com.  Ahora he agregado un segundo dominio de nivel superior, bmfabrikam.com.

![Dominios](./media/active-directory-multiple-domains/domains.png)

Cuando intentamos tooconvert nuestro toobe de dominio bmfabrikam.com federado, se recibe un error.  es el motivo Hello, Azure AD tiene una restricción que no permite Hola Hola de toohave de propiedad IssuerUri mismo valor para más de un dominio.  

![Error de federación](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parámetro SupportMultipleDomain
tooworkaround esto, debemos tooadd un IssuerUri diferentes que puede realizarse mediante el uso de hello `-SupportMultipleDomain` parámetro.  Este parámetro se utiliza con hello siguientes cmdlets:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Este parámetro hace que Azure AD configurar hello IssuerUri para que se basa en el nombre de hello del dominio de Hola.  Este será único en los directorios de Azure AD.  Usar el parámetro hello permite toocomplete de comandos de PowerShell de hello correctamente.

![Error de federación](./media/active-directory-multiple-domains/convert.png)

Examinando configuración Hola de nuestro nuevo dominio bmfabrikam.com puede ver el siguiente hello:

![Error de federación](./media/active-directory-multiple-domains/settings.png)

Tenga en cuenta que `-SupportMultipleDomain` no cambia Hola otros extremos que son todavía configuran el servicio de federación de toopoint tooour en adfs.bmcontoso.com.

Otra cosa que `-SupportMultipleDomain` does es que garantiza que sistema de hello AD FS incluye valor del emisor correcto hello en tokens emitidos para Azure AD. Para ello, tomar parte de dominio de Hola de hello usuarios UPN y si se establece como dominio de Hola Hola IssuerUri, es decir, https://{upn sufijo} / adfs/services/trust. 

Por lo tanto durante la autenticación tooAzure AD u Office 365, hello IssuerUri elemento token del usuario de hello es dominio de hello toolocate usado en Azure AD.  Si no se encuentra una coincidencia se producirá un error de autenticación de Hola. 

Por ejemplo, si un usuario del UPN es bsimon@bmcontoso.com, elemento de IssuerUri hello en problemas de AD FS de token de Hola se establecerá toohttp://bmcontoso.com/adfs/services/trust. Esto coincidirá con la configuración de Azure AD de Hola y autenticación se realizará correctamente.

Hola te mostramos regla de notificación personalizada de Hola que implementa esta lógica:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> En orden toouse Hola - SupportMultipleDomain cambiar al intentar tooadd nueva o convertir ya dominios agregados, deberá toohave la instalación de la relación de confianza federada toosupport ellos originalmente.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>¿Cómo tooupdate Hola de confianza entre AD FS y Azure
Si no se han configurado Hola federado confianza entre AD FS y la instancia de Azure AD, puede que necesite toore-crear esta relación de confianza.  Esto es porque, cuando es originalmente el programa de instalación sin hello `-SupportMultipleDomain` parámetro, hello IssuerUri se establece con el valor predeterminado de Hola.  Hola captura de pantalla siguiente se puede ver hello IssuerUri se establece toohttps://adfs.bmcontoso.com/adfs/services/trust.

Ahora, si se ha agregado correctamente un nuevo dominio en el portal de hello Azure AD y, a continuación, intente tooconvert mediante `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtenemos Hola siguiente error.

![Error de federación](./media/active-directory-multiple-domains/trust1.png)

Si intentas hello tooadd `-SupportMultipleDomain` conmutador recibimos Hola siguiente error:

![Error de federación](./media/active-directory-multiple-domains/trust2.png)

Simplemente intentar toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` en hello dominio original también producirá un error.

![Error de federación](./media/active-directory-multiple-domains/trust3.png)

Use estos pasos hello tooadd un dominio de nivel superior adicional.  Si ya se ha agregado un dominio y no usó hello `-SupportMultipleDomain` parámetro Inicio con pasos de Hola para quitar y actualizar su dominio original.  Si no ha agregado un dominio de nivel superior se puede iniciar con pasos de Hola para agregar un dominio con PowerShell de Azure AD Connect.

Usar hello después de confianza de Microsoft Online de pasos tooremove hello y actualice su dominio original.

1. En el servidor de federación de AD FS, abra **Administración de AD FS.** 
2. Hola izquierda, expanda **relaciones de confianza** y **usuario autenticado**
3. En hello derecha, elimine hello **plataforma de identidad de Microsoft Office 365** entrada.
   ![Quitar Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. En un equipo que tenga [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado en el que se ejecute el siguiente hello: `$cred=Get-Credential`.  
5. Escriba Hola nombre de usuario y la contraseña de administrador global para dominio de Azure AD Hola con que federa
6. En PowerShell, escriba `Connect-MsolService -Credential $cred`
7. En PowerShell, escriba `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Esto es para dominio original Hola.  Por lo que usar Hola anterior dominios sería:`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Usar hello siguiendo los pasos tooadd Hola nuevo dominio de nivel superior con PowerShell

1. En un equipo que tenga [Azure módulo Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) instalado en el que se ejecute el siguiente hello: `$cred=Get-Credential`.  
2. Escriba Hola nombre de usuario y la contraseña de administrador global para dominio de Azure AD Hola con que federa
3. En PowerShell, escriba `Connect-MsolService -Credential $cred`
4. En PowerShell, escriba `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Usar hello siguiendo los pasos tooadd Hola nuevo dominio de nivel superior mediante Azure AD Connect.

1. Iniciar Azure Connect AD desde el escritorio de Hola o del menú Inicio
2. Elija "Agregar un dominio de Azure AD adicional" ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add1.png)
3. Escriba sus credenciales de Azure AD y Active Directory.
4. Seleccione el dominio de segundo de hello desea tooconfigure para la federación.
   ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add2.png)
5. Haga clic en Instalar.

### <a name="verify-hello-new-top-level-domain"></a>Comprobar el dominio de nivel superior nuevo Hola
Mediante el uso de comandos de PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`puede ver Hola actualizado IssuerUri.  Hola de captura de pantalla siguiente muestra la configuración de la federación de Hola se han actualizado en nuestro http://bmcontoso.com/adfs/services/trust dominio original

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Y hello IssuerUri en nuestro nuevo dominio se ha establecido toohttps://bmfabrikam.com/adfs/services/trust

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Compatibilidad con subdominios
Cuando se agrega un subdominio, debido a Hola forma Azure AD controla dominios, heredará la configuración de Hola de hello primaria.  Esto significa que hello IssuerUri tiene a elementos primarios de hello toomatch.

Supongamos que tengo bmcontoso.com y que agrego corp.bmcontoso.com.  Esto significa que hello IssuerUri para un usuario de corp.bmcontoso.com tendrá toobe **http://bmcontoso.com/adfs/services/trust.**  Sin embargo, implementan reglas estándar de hello anteriormente para Azure AD, se generará un token con un emisor como **http://corp.bmcontoso.com/adfs/services/trust.** Esto no coincidirá con valor requerido del dominio de Hola y se producirá un error de autenticación.

### <a name="how-tooenable-support-for-sub-domains"></a>¿Cómo se admiten tooenable de subdominios
En orden toowork alrededor de esta Hola ADFS relación de confianza de Microsoft Online debe toobe actualizado.  toodo esto, debe configurar una regla de notificación personalizada para que quita cualquier subdominios de sufijo UPN del usuario de hello al construir el valor de emisor de hello personalizado. 

Hola después de la notificación hace esto:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
último número de Hello en la expresión regular de hello establece Hola cuántos dominios primarios que hay en el dominio raíz. En este caso tenemos bmcontoso.com, por lo que se requieren dos dominios principales. Si los tres principales dominios estaban toobe mantiene (es decir,: corp.bmcontoso.com), a continuación, el número de hello habría sido tres. Puede indicarse Eventualy un intervalo, coincidencia de hello siempre estará toomatch máximo de Hola de dominios. "{2,3}" se corresponderá con dos dominios de toothree (es decir,: bmfabrikam.com y corp.bmcontoso.com).

Usar hello siguiendo los pasos tooadd un toosupport de notificación personalizada subdominios.

1. Abra Administración de AD FS.
2. Haga clic en la confianza de Microsoft Online RP hello y elegir reglas de notificación de editar
3. Seleccione Hola tercera regla de notificación y reemplace ![Editar notificación](./media/active-directory-multiple-domains/sub1.png)
4. Reemplace la notificación actual hello:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Reemplazar notificación](./media/active-directory-multiple-domains/sub2.png)

5. Haga clic en Aceptar.  Haga clic en Aplicar.  Haga clic en Aceptar.  Cierre Administración de AD FS.

