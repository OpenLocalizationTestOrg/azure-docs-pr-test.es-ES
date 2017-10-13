---
title: Varios dominios de Azure AD Connect
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
ms.openlocfilehash: 8e3f496c2868cc3430e0efd47805aec2205168aa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Compatibilidad con varios dominios para la federación con Azure AD
La siguiente documentación proporciona orientación sobre cómo usar varios dominios y subdominios de nivel superior al federarse con Office 365 o con dominios de Azure AD.

## <a name="multiple-top-level-domain-support"></a>Compatibilidad con varios dominios de nivel superior
La federación de varios dominios de nivel superior con Azure AD requiere una configuración adicional que no es necesaria al federarse con un dominio de nivel superior.

Cuando se federa un dominio con Azure AD, se establecen varias propiedades en el dominio de Azure.  Una propiedad importante es IssuerUri.  Se trata de un URI que Azure AD usa para identificar el dominio al que está asociado el token.  El URI no necesita resolver nada, pero debe ser un URI válido.  De forma predeterminada, Azure AD lo establece en el valor del identificador del servicio de federación en la configuración local de AD FS.

> [!NOTE]
> El identificador del servicio de federación es un URI que identifica de forma única un servicio de federación.  El servicio de federación es una instancia de AD FS que funciona como el servicio de token de seguridad. 
> 
> 

Para ver el valor de IssuerUri, use el comando de PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Se produce un problema cuando se quiere agregar más de un dominio de nivel superior.  Por ejemplo, supongamos que ha configurado la federación entre Azure AD y el entorno local.  Para este documento uso bmcontoso.com.  Ahora he agregado un segundo dominio de nivel superior, bmfabrikam.com.

![Dominios](./media/active-directory-multiple-domains/domains.png)

Cuando se intenta convertir el dominio bmfabrikam.com en federado, se recibe un error.  Esto se debe a que Azure AD tiene una restricción que no permite que la propiedad IssuerUri tenga el mismo valor para más de un dominio.  

![Error de federación](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Parámetro SupportMultipleDomain
Para solucionarlo necesitamos agregar un valor de IssuerUri diferente, lo que puede hacerse mediante el parámetro `-SupportMultipleDomain` .  Este parámetro se usa con los cmdlets siguientes:

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Este parámetro hace que Azure AD configure el valor de IssuerUri para que se base en el nombre del dominio.  Este será único en los directorios de Azure AD.  El uso del parámetro permite que el comando de PowerShell se complete correctamente.

![Error de federación](./media/active-directory-multiple-domains/convert.png)

Si examina la configuración del nuevo dominio bmfabrikam.com, observará lo siguiente:

![Error de federación](./media/active-directory-multiple-domains/settings.png)

Tenga en cuenta que `-SupportMultipleDomain` no cambia los otros puntos de conexión que todavía están configurados para apuntar al servicio de federación de adfs.bmcontoso.com.

Otra cosa que hace `-SupportMultipleDomain` es garantizar que el sistema de AD FS incluya el valor Issuer apropiado en los tokens emitidos para Azure AD. Para ello, toma la parte de dominio del UPN de los usuarios y la establece como dominio en IssuerUri, es decir, https://{upn suffix}/adfs/services/trust. 

Por lo tanto, durante la autenticación en Azure AD u Office 365, el elemento IssuerUri del token del usuario se usa para buscar el dominio en Azure AD.  Si no se encuentra una coincidencia, se producirá un error en la autenticación. 

Por ejemplo, si un usuario del UPN es bsimon@bmcontoso.com, el elemento IssuerUri en los problemas de símbolo (token) de AD FS se establecerá en http://bmcontoso.com/adfs/services/trust. Coincidirá con la configuración de Azure AD y la autenticación se realizará correctamente.

A continuación se muestra la regla de notificaciones personalizada que implementa esta lógica:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> Para poder usar el modificador -SupportMultipleDomain al intentar agregar dominios nuevos o convertir dominios ya agregados, debe tener configurada la confianza federada de modo que los admita originalmente.  
> 
> 

## <a name="how-to-update-the-trust-between-ad-fs-and-azure-ad"></a>Actualización de la confianza entre AD FS y Azure AD
Si no configuró la confianza federada entre AD FS y la instancia de Azure AD, podría tener que volver a crear esta confianza.  Esto se debe a que, cuando se configura originalmente sin el parámetro `-SupportMultipleDomain` , el valor de IssuerUri se establece como predeterminado.  En la captura de pantalla siguiente se puede ver que el elemento IssuerUri se establece en https://adfs.bmcontoso.com/adfs/services/trust.

Ahora, si hemos agregado correctamente un nuevo dominio en el Portal de Azure AD e intentamos convertirlo con `Convert-MsolDomaintoFederated -DomainName <your domain>`, obtendremos el error siguiente.

![Error de federación](./media/active-directory-multiple-domains/trust1.png)

Si intenta agregar el modificador `-SupportMultipleDomain` , aparecerá el error siguiente:

![Error de federación](./media/active-directory-multiple-domains/trust2.png)

El simple hecho de intentar ejecutar `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` en el dominio original también producirá un error.

![Error de federación](./media/active-directory-multiple-domains/trust3.png)

Siga los pasos indicados a continuación para agregar otro dominio de nivel superior.  Si ya ha agregado un dominio y no ha usado el parámetro `-SupportMultipleDomain` , empiece por los pasos para quitar y actualizar el dominio original.  Si todavía no ha agregado un dominio de nivel superior, puede comenzar por los pasos para agregar un dominio con PowerShell de Azure AD Connect.

Siga los pasos indicados a continuación para quitar la confianza de Microsoft Online y actualizar el dominio original.

1. En el servidor de federación de AD FS, abra **Administración de AD FS.** 
2. A la izquierda, expanda **Relaciones de confianza** y **Confianzas de usuario de confianza**.
3. A la derecha, elimine la entrada **Plataforma de identidad de Microsoft Office 365** .
   ![Quitar Microsoft Online](./media/active-directory-multiple-domains/trust4.png)
4. En un equipo que tenga instalado el [Módulo de Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), ejecute lo siguiente: `$cred=Get-Credential`.  
5. Escriba el nombre de usuario y la contraseña de un administrador global del dominio de Azure AD con el que se esté federando.
6. En PowerShell, escriba `Connect-MsolService -Credential $cred`
7. En PowerShell, escriba `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Esto es para el dominio original.  Si se usan los dominios anteriores, sería: `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Siga los pasos que se indican a continuación para agregar el nuevo dominio de nivel superior con PowerShell.

1. En un equipo que tenga instalado el [Módulo de Azure Active Directory para Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx), ejecute lo siguiente: `$cred=Get-Credential`.  
2. Escriba el nombre de usuario y la contraseña de un administrador global del dominio de Azure AD con el que se esté federando.
3. En PowerShell, escriba `Connect-MsolService -Credential $cred`
4. En PowerShell, escriba `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Siga los pasos que se indican a continuación para agregar el nuevo dominio de nivel superior con Azure AD Connect.

1. Inicie Azure AD Connect desde el escritorio o el menú Inicio.
2. Elija "Agregar un dominio de Azure AD adicional" ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add1.png)
3. Escriba sus credenciales de Azure AD y Active Directory.
4. Seleccione el segundo dominio que desea configurar para federación.
   ![Agregar un dominio de Azure AD adicional](./media/active-directory-multiple-domains/add2.png)
5. Haga clic en Instalar.

### <a name="verify-the-new-top-level-domain"></a>Comprobación del nuevo dominio de nivel superior
Con el comando de PowerShell `Get-MsolDomainFederationSettings -DomainName <your domain>`, puede ver el valor de IssuerUri actualizado.  La captura de pantalla siguiente muestra que la configuración de la federación se actualizó en el dominio original http://bmcontoso.com/adfs/services/trust.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Y el elemento IssuerUri de nuestro dominio nuevo se ha establecido en https://bmfabrikam.com/adfs/services/trust.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Compatibilidad con subdominios
Cuando se agrega un subdominio, debido a la manera en que Azure AD controla los dominios, heredará la configuración del elemento primario.  Esto significa que el elemento IssuerUri debe coincidir con los elementos primarios.

Supongamos que tengo bmcontoso.com y que agrego corp.bmcontoso.com.  Esto significa que el elemento IssuerUri de un usuario de corp.bmcontoso.com deberá ser **http://bmcontoso.com/adfs/services/trust.**  A pesar de la regla estándar implementada anteriormente para Azure AD, se generará un token con un emisor como **http://corp.bmcontoso.com/adfs/services/trust.** que no coincidirá con el valor obligatorio del dominio y se producirá un error de autenticación.

### <a name="how-to-enable-support-for-sub-domains"></a>Habilitación de la compatibilidad con subdominios
Para solucionar este problema, es necesario actualizar la confianza de usuario de confianza de AD FS para Microsoft Online.  Para ello, debe configurar una regla de notificaciones personalizada para eliminar cualquier subdominio del sufijo UPN del usuario al construir el valor de emisor personalizado. 

La siguiente notificación hará lo siguiente:

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
El último número de la expresión regular establece la cantidad de dominios primarios que hay en el dominio raíz. En este caso tenemos bmcontoso.com, por lo que se requieren dos dominios principales. Si tuviéramos que mantener tres dominios principales (es decir, corp.bmcontoso.com), el número habría sido tres. Es posible indicar un intervalo; en ese caso, la coincidencia se realizará siempre con el número máximo de dominios. "{2,3}" coincidirá con dos o tres dominios (esto es, bmfabrikam.com y corp.bmcontoso.com).

Siga los pasos indicados a continuación para agregar una notificación personalizada para admitir subdominios.

1. Abra Administración de AD FS.
2. Haga clic con el botón derecho en la confianza de usuario de confianza de Microsoft Online y elija Editar reglas de notificación.
3. Seleccione la tercera regla de notificación y reemplace ![Editar notificación](./media/active-directory-multiple-domains/sub1.png).
4. Reemplace la notificación actual:
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Reemplazar notificación](./media/active-directory-multiple-domains/sub2.png)

5. Haga clic en Aceptar.  Haga clic en Aplicar.  Haga clic en Aceptar.  Cierre Administración de AD FS.

