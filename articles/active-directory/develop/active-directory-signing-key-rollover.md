---
title: "Sustitución de clave en Azure AD aaaSigning | Documentos de Microsoft"
description: "Este artículo describe Hola prácticas recomendadas de sustitución de la clave de firma para Azure Active Directory"
services: active-directory
documentationcenter: .net
author: dstrockis
manager: krassk
editor: 
ms.assetid: ed964056-0723-42fe-bb69-e57323b9407f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ac6ade7f3ba2fbd22ea6d447aa5d07a2d6bdd451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="signing-key-rollover-in-azure-active-directory"></a>Sustitución de claves de firma de Azure Active Directory
Este tema describe lo que necesita tooknow acerca de las claves públicas Hola que se usan en tokens de seguridad de Azure Active Directory (Azure AD) toosign. Es importante toonote que estas claves se sustituyen de forma periódica y, en caso de emergencia, se deben sustituirse inmediatamente. Todas las aplicaciones que usan Azure AD deben ser capaz de tooprogrammatically identificador hello sustitución de claves proceso o establezca un proceso de sustitución manual periódica. Seguir leyendo toounderstand cómo funcionan las claves de hello, cómo tooassess Hola impacto de la aplicación de tooyour de sustitución incremental de hello y cómo tooupdate la aplicación o establecer una sustitución de claves de sustitución manual periódica proceso toohandle si es necesario.

## <a name="overview-of-signing-keys-in-azure-ad"></a>Información general sobre las claves de firma de Azure AD
Azure AD usa criptografía de clave pública depende de la industria estándares tooestablish confianza entre él y hello las aplicaciones que lo usan. En la práctica, esto funciona en hello siguiente forma: Azure AD usa una clave de firma que consta de un par de claves público y privado. Cuando un usuario inicia sesión en la aplicación tooan que usa Azure AD para la autenticación, Azure AD crea un token de seguridad que contiene información acerca del usuario de Hola. Este token está firmado por Azure AD utilizando su clave privada antes de enviarlo aplicación toohello atrás. tooverify que Hola token es válido y realmente se ha originado en Azure AD, aplicación hello debe validar la firma del token de hello usando la clave pública de hello expuesta por Azure AD que se encuentra en el inquilino de hello [documento de detección de OpenID Connect](http://openid.net/specs/openid-connect-discovery-1_0.html) o SAML/WS-Fed [documento de metadatos de federación](active-directory-federation-metadata.md).

Por motivos de seguridad de Azure AD firma clave revierte de forma periódica y, en caso de hello de emergencia, se deben sustituirse inmediatamente. Cualquier aplicación que se integra con Azure AD debe estar preparado toohandle un evento de sustitución de claves independientemente de la frecuencia con la que ocurra. Si no es así, y la aplicación trata de toouse una firma de hello expiradas tooverify clave en un símbolo (token), se producirá un error en la solicitud de inicio de sesión Hola.

Siempre hay más de una clave válida disponible en el documento de detección de OpenID Connect de Hola y documento de metadatos de federación de Hola. La aplicación debe estar preparada toouse cualquiera de las claves de hello especificada en el documento de hello, ya que se puede sustituir una clave pronto, otra puede ser su sustituta y así sucesivamente.

## <a name="how-tooassess-if-your-application-will-be-affected-and-what-toodo-about-it"></a>¿Cómo tooassess si su aplicación se verá afectada y qué toodo sobre él
Cómo la aplicación controla la sustitución de claves depende de variables como tipo de Hola de aplicación o qué protocolo de identidad y la biblioteca se usó. Hola las siguientes secciones se evaluación si los tipos más comunes de Hola de aplicaciones se ven afectados por la sustitución de claves de Hola y ofrecen orientación sobre cómo tooupdate Hola sustitución automática de aplicación toosupport o actualizar manualmente la clave de Hola.

* [Aplicaciones de cliente nativas que acceden a recursos](#nativeclient)
* [Aplicaciones y API web que acceden a recursos](#webclient)
* [Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure](#appservices)
* [Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication](#owin)
* [Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication](#owincore)
* [Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad](#passport)
* [Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017](#vs2015)
* [Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013](#vs2013)
* [API web de protección de recursos y creadas con Visual Studio 2013](#vs2013_webapi)
* [Aplicaciones web de protección de recursos y creadas con Visual Studio 2012](#vs2012)
* [Aplicaciones web de protección de recursos y creadas con Visual Studio 2010, 2008 o mediante Windows Identity Foundation](#vs2010)
* [Aplicaciones Web / API de protección de los recursos cualquiera otras bibliotecas o implementar manualmente cualquiera de hello admite el uso de protocolos](#other)

Esta guía **no** es aplicable para:

* Las aplicaciones agregadas desde la Galería de aplicaciones de Azure AD (incluyendo personalizado) tienen instrucciones independientes con lo que respecta toosigning claves. [Más información.](../active-directory-sso-certs.md)
* Las aplicaciones publicadas a través de proxy de aplicación no tienen tooworry sobre claves de firma en local.

### <a name="nativeclient"></a>Aplicaciones de cliente nativas que acceden a recursos
Las aplicaciones que solo acceden a los recursos (es decir, Microsoft Graph, KeyVault, API de Outlook y otras APIs Microsoft) generalmente solo obtienen un token y pasan a toohello propietario del recurso. Dado que no están protegiendo todos los recursos, se inspecciona el token de hello y, por tanto, no es necesario tooensure que está firmado correctamente.

Si escritorio o móvil, las aplicaciones cliente nativas, entran en esta categoría y, por tanto, no se ven afectadas por la sustitución de Hola.

### <a name="webclient"></a>Aplicaciones y API web que acceden a recursos
Las aplicaciones que solo acceden a los recursos (es decir, Microsoft Graph, KeyVault, API de Outlook y otras APIs Microsoft) generalmente solo obtienen un token y pasan a toohello propietario del recurso. Dado que no están protegiendo todos los recursos, se inspecciona el token de hello y, por tanto, no es necesario tooensure que está firmado correctamente.

Las aplicaciones Web y las API que están usando el flujo de hello solo de aplicación web (las credenciales del cliente / certificado de cliente), entran en esta categoría y, por tanto, no se ven afectadas por la sustitución de Hola.

### <a name="appservices"></a>Aplicaciones y API web que protegen recursos y creadas mediante Servicios de aplicaciones de Azure
Autenticación de Azure Servicios de aplicaciones / funcionalidad de autorización (EasyAuth) ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.

### <a name="owin"></a>Aplicaciones y API web que protegen recursos mediante middleware .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication
Si la aplicación está utilizando Hola .NET OWIN OpenID Connect, WS-Fed o WindowsAzureActiveDirectoryBearerAuthentication middleware, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.

Puede confirmar que la aplicación está utilizando cualquiera de estos métodos, debe buscar cualquiera de los siguientes fragmentos de código de la aplicación Startup.cs o Startup.Auth.cs de Hola

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseWsFederationAuthentication(
    new WsFederationAuthenticationOptions
    {
     // ...
     });
```
```
 app.UseWindowsAzureActiveDirectoryBearerAuthentication(
     new WindowsAzureActiveDirectoryBearerAuthenticationOptions
     {
     // ...
     });
```

### <a name="owincore"></a>Aplicaciones y API web que protegen recursos mediante el middleware .NET Core OpenID Connect o JwtBearerAuthentication
Si la aplicación utiliza .NET Core OWIN OpenID Connect de Hola o JwtBearerAuthentication middleware, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.

Puede confirmar que la aplicación está utilizando cualquiera de estos métodos, debe buscar cualquiera de los siguientes fragmentos de código de la aplicación Startup.cs o Startup.Auth.cs de Hola

```
app.UseOpenIdConnectAuthentication(
     new OpenIdConnectAuthenticationOptions
     {
         // ...
     });
```
```
app.UseJwtBearerAuthentication(
    new JwtBearerAuthenticationOptions
    {
     // ...
     });
```

### <a name="passport"></a>Aplicaciones y API web que protegen recursos mediante el módulo Node.js passport-azure-ad
Si la aplicación está utilizando el módulo de passport ad Node.js hello, ya tiene la sustitución de clave toohandle Hola lógica necesaria automáticamente.

Puede confirmar que su aplicación passport-ad mediante la búsqueda de hello siguiente fragmento de código en app.js la aplicación

```
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

passport.use(new OIDCStrategy({
    //...
));
```

### <a name="vs2015"></a>Aplicaciones y API web de protección de recursos y creadas con Visual Studio 2015 o Visual Studio 2017
Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2015 o Visual Studio de 2017 y seleccionó **cuentas de trabajo y educativa** de hello **Cambiar autenticación** menú, que ya se tiene automáticamente la sustitución de clave toohandle Hola lógica necesaria. Esta lógica, incrustada en middleware OWIN OpenID Connect hello, recupera y almacena en caché las claves de Hola de documento de detección de OpenID Connect de Hola y los actualiza periódicamente.

Si agrega manualmente la solución de tooyour de autenticación, la aplicación podría no tener lógica de sustitución de claves necesaria Hola. Necesitará toowrite usted mismo u Hola siga los pasos de [aplicaciones Web API con cualquier otra biblioteca o implementar manualmente cualquiera de hello admite protocolos.](#other).

### <a name="vs2013"></a>Aplicaciones Web de protección de recursos y creadas con Visual Studio 2013
Si la aplicación se compiló mediante una plantilla de aplicación web en Visual Studio 2013 y seleccionó **cuentas organizativas** de hello **Cambiar autenticación** menú, ya tiene Hola necesarios lógica toohandle sustitución de clave automáticamente. Esta lógica almacena hello firma información clave en dos tablas de base de datos asociados con el proyecto de Hola e identificador único de su organización. Puede encontrar la cadena de conexión de Hola para base de datos de Hola en el archivo Web.config del proyecto de Hola.

Si agrega manualmente la solución de tooyour de autenticación, la aplicación podría no tener lógica de sustitución de claves necesaria Hola. Necesitará toowrite usted mismo u Hola siga los pasos de [aplicaciones Web API con cualquier otra biblioteca o implementar manualmente cualquiera de hello admite protocolos.](#other).

Hola pasos le ayudará a comprobar que Hola lógica funciona correctamente en la aplicación.

1. En Visual Studio 2013, abra la solución de hello y, a continuación, haga clic en hello **Explorador de servidores** ficha en la ventana derecha Hola.
2. Expanda **Conexiones de datos**, **DefaultConnection** y **Tablas**. Busque hello **IssuingAuthorityKeys** de tabla, haga clic en él y, a continuación, haga clic en **mostrar datos de tabla**.
3. Hola **IssuingAuthorityKeys** tabla, habrá al menos una fila, que se corresponde el valor de huella digital de toohello para la clave de Hola. Elimine las filas de tabla de Hola.
4. Menú contextual hello **inquilinos** de tabla y, a continuación, haga clic en **mostrar datos de tabla**.
5. Hola **inquilinos** tabla, habrá al menos una fila, que se corresponde el identificador del inquilino de directorio único tooa. Elimine las filas de tabla de Hola. Si no elimina las filas de hello en ambos hello **inquilinos** tabla y **IssuingAuthorityKeys** tabla, obtendrá un error en tiempo de ejecución.
6. Compile y ejecute la aplicación hello. Una vez haya iniciado en tooyour cuenta, puede detener la aplicación hello.
7. Devolver toohello **Explorador de servidores** y examine los valores de hello en hello **IssuingAuthorityKeys** y **inquilinos** tabla. Observará que ha vuelto a llenar automáticamente con información adecuada de Hola de documento de metadatos de federación de Hola.

### <a name="vs2013"></a>API web de protección de recursos y creadas con Visual Studio 2013
Si crea una aplicación API web en Visual Studio 2013 mediante la plantilla de la API Web de hello y, a continuación, selecciona **cuentas organizativas** de hello **Cambiar autenticación** menú, ya haya Hola lógica necesaria en la aplicación.

Si ha configurado manualmente la autenticación, siga instrucciones hello toolearn cómo tooconfigure su tooautomatically API Web actualizar su información de clave.

Hello fragmento de código siguiente muestra cómo tooget Hola claves más recientes de documento de metadatos de federación de hello y, a continuación, usar hello [controlador de Token JWT](https://msdn.microsoft.com/library/dn205065.aspx) símbolo (token) de toovalidate Hola. fragmento de código de Hello se supone que va a usar sus propio mecanismo para conservar Hola clave toovalidate futuras el almacenamiento en caché los tokens de Azure AD, ya sea en una base de datos, archivo de configuración o en otro lugar.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IdentityModel.Tokens;
using System.Configuration;
using System.Security.Cryptography.X509Certificates;
using System.Xml;
using System.IdentityModel.Metadata;
using System.ServiceModel.Security;
using System.Threading;

namespace JWTValidation
{
    public class JWTValidator
    {
        private string MetadataAddress = "[Your Federation Metadata document address goes here]";

        // Validates hello JWT Token that's part of hello Authorization header in an HTTP request.
        public void ValidateJwtToken(string token)
        {
            JwtSecurityTokenHandler tokenHandler = new JwtSecurityTokenHandler()
            {
                // Do not disable for production code
                CertificateValidator = X509CertificateValidator.None
            };

            TokenValidationParameters validationParams = new TokenValidationParameters()
            {
                AllowedAudience = "[Your App ID URI goes here, as registered in hello Azure Classic Portal]",
                ValidIssuer = "[hello issuer for hello token goes here, such as https://sts.windows.net/68b98905-130e-4d7c-b6e1-a158a9ed8449/]",
                SigningTokens = GetSigningCertificates(MetadataAddress)

                // Cache hello signing tokens by your desired mechanism
            };

            Thread.CurrentPrincipal = tokenHandler.ValidateToken(token, validationParams);
        }

        // Returns a list of certificates from hello specified metadata document.
        public List<X509SecurityToken> GetSigningCertificates(string metadataAddress)
        {
            List<X509SecurityToken> tokens = new List<X509SecurityToken>();

            if (metadataAddress == null)
            {
                throw new ArgumentNullException(metadataAddress);
            }

            using (XmlReader metadataReader = XmlReader.Create(metadataAddress))
            {
                MetadataSerializer serializer = new MetadataSerializer()
                {
                    // Do not disable for production code
                    CertificateValidationMode = X509CertificateValidationMode.None
                };

                EntityDescriptor metadata = serializer.ReadMetadata(metadataReader) as EntityDescriptor;

                if (metadata != null)
                {
                    SecurityTokenServiceDescriptor stsd = metadata.RoleDescriptors.OfType<SecurityTokenServiceDescriptor>().First();

                    if (stsd != null)
                    {
                        IEnumerable<X509RawDataKeyIdentifierClause> x509DataClauses = stsd.Keys.Where(key => key.KeyInfo != null && (key.Use == KeyType.Signing || key.Use == KeyType.Unspecified)).
                                                             Select(key => key.KeyInfo.OfType<X509RawDataKeyIdentifierClause>().First());

                        tokens.AddRange(x509DataClauses.Select(token => new X509SecurityToken(new X509Certificate2(token.GetX509RawData()))));
                    }
                    else
                    {
                        throw new InvalidOperationException("There is no RoleDescriptor of type SecurityTokenServiceType in hello metadata");
                    }
                }
                else
                {
                    throw new Exception("Invalid Federation Metadata document");
                }
            }
            return tokens;
        }
    }
}
```

### <a name="vs2012"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2012
Si la aplicación se compiló en Visual Studio 2012, probablemente ha utilizado hello identidad y tooconfigure de la herramienta de acceso a la aplicación. También es probable que esté utilizando hello [del registro de nombre de emisor validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx). Hola VINR es responsable de mantener la información sobre proveedores de identidades confiables (Azure AD) y las claves de hello utilizan tokens toovalidate que han emitido. Hola VINR también facilita la información de claves tooautomatically fácil actualización Hola almacenada en un archivo Web.config descargando Hola último federación documento de metadatos asociada al directorio, comprobando si configuración de hello no está actualizada con hello más reciente documento y actualización hello toouse Hola nueva clave de aplicación según sea necesario.

Si ha creado su aplicación mediante cualquiera de los ejemplos de código de hello o documentación de tutoriales proporcionados por Microsoft, la lógica de sustitución de claves de hello ya está incluido en el proyecto. Observará que código de hello siguiente ya existe en el proyecto. Si la aplicación aún no tiene esta lógica, siga los pasos hello tooadd y tooverify que funciona correctamente.

1. En **el Explorador de soluciones**, agregar una referencia toohello **System.IdentityModel** ensamblado de proyecto adecuada de Hola.
2. Abra hello **Global.asax.cs** de archivos y agregue Hola siguientes directivas using:
   ```
   using System.Configuration;
   using System.IdentityModel.Tokens;
   ```
3. Agregar Hola siguiendo el método toohello **Global.asax.cs** archivo:
   ```
   protected void RefreshValidationSettings()
   {
    string configPath = AppDomain.CurrentDomain.BaseDirectory + "\\" + "Web.config";
    string metadataAddress =
                  ConfigurationManager.AppSettings["ida:FederationMetadataLocation"];
    ValidatingIssuerNameRegistry.WriteToConfig(metadataAddress, configPath);
   }
   ```
4. Invocar hello **RefreshValidationSettings()** método Hola **Application_Start ()** método **Global.asax.cs** tal como se muestra:
   ```
   protected void Application_Start()
   {
    AreaRegistration.RegisterAllAreas();
    ...
    RefreshValidationSettings();
   }
   ```

Una vez que haya seguido estos pasos, se actualizará con la información más reciente de Hola de documento de metadatos de federación Hola, incluidas las claves más recientes de Hola Web.config de su aplicación. Esta actualización se producirá cada vez que se recicla el grupo de aplicaciones en IIS; de forma predeterminada IIS se establece toorecycle aplicaciones cada 29 horas.

Siga los pasos de hello debajo tooverify que funciona la lógica de sustitución de claves de Hola.

1. Después de comprobar que la aplicación está usando código de hello anteriormente, abra hello **Web.config** de archivos y desplácese toohello  **<issuerNameRegistry>**  bloque, buscando específicamente Hola después algunas líneas:
   ```
   <issuerNameRegistry type="System.IdentityModel.Tokens.ValidatingIssuerNameRegistry, System.IdentityModel.Tokens.ValidatingIssuerNameRegistry">
        <authority name="https://sts.windows.net/ec4187af-07da-4f01-b18f-64c2f5abecea/">
          <keys>
            <add thumbprint="3A38FA984E8560F19AADC9F86FE9594BB6AD049B" />
          </keys>
   ```
2. Hola  **<add thumbprint=””>**  configuración, cambie el valor de huella digital de hello reemplazando algún carácter por otra diferente. Guardar hello **Web.config** archivo.
3. Compilar la aplicación hello y, a continuación, ejecútelo. Si puede completar el proceso de inicio de sesión de hello, la aplicación actualiza correctamente clave Hola descargando información de hello necesario de documento de metadatos de federación de su directorio. Si tiene problemas para iniciar sesión, asegúrese de hello cambios en la aplicación son correctos leyendo hello [tooYour agregar inicio de sesión Web aplicaciones con Azure AD](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) tema, o bien descargarlos e inspeccionando el siguiente ejemplo de código de hello: [ Aplicación de nube de varios inquilinos de Azure Active Directory](https://code.msdn.microsoft.com/multi-tenant-cloud-8015b84b).

### <a name="vs2010"></a>Aplicaciones web de protección de recursos y creadas con Visual Studio 2008 o 2010 y Windows Identity Foundation (WIF) v1.0 para .NET 3.5
Si ha creado una aplicación en WIF v1.0, no hay ninguna actualización de tooautomatically mecanismo toouse de configuración de la aplicación una nueva clave.

* *La manera más fácil* usar el utillaje de FedUtil Hola incluido en hello WIF SDK, que puede recuperar el último documento de metadatos de Hola y actualizar la configuración.
* Actualice su too.NET aplicación 4.5, que incluye la versión más reciente de Hola de WIF ubicada en el espacio de nombres de sistema de Hola. A continuación, puede usar hello [del registro de nombre de emisor validación (VINR)](https://msdn.microsoft.com/library/dn205067.aspx) tooperform actualizaciones automáticas de configuración de la aplicación hello.
* Realizar una sustitución manual según las instrucciones de hello final Hola de este documento de instrucciones.

Instrucciones toouse Hola FedUtil tooupdate su configuración:

1. Compruebe que dispone de hello WIF v1.0 SDK instalado en el equipo de desarrollo para Visual Studio 2008 o 2010. También puede [descargarlo desde aquí](https://www.microsoft.com/en-us/download/details.aspx?id=4451) si aún no lo ha instalado.
2. En Visual Studio, abra la solución hello y, a continuación, haga clic en proyecto aplicable de Hola y seleccione **actualizar metadatos de federación**. Si esta opción no está disponible, no se instaló FedUtil y/o Hola WIF v1.0 SDK.
3. En el símbolo del sistema de hello, seleccione **actualización** toobegin actualizar los metadatos de federación. Si tiene un entorno de servidor de acceso a toohello donde se hospeda la aplicación hello, también puede usar FedUtil [programador de actualizaciones de metadatos automática](https://msdn.microsoft.com/library/ee517272.aspx).
4. Haga clic en **finalizar** proceso de actualización de toocomplete Hola.

### <a name="other"></a>Aplicaciones Web / API de protección de los recursos cualquiera otras bibliotecas o implementar manualmente cualquiera de hello admite el uso de protocolos
Si está utilizando alguna otra biblioteca o implementa manualmente cualquiera de los protocolos de hello admitida, necesitará tooreview biblioteca de Hola o se está recuperando el tooensure de implementación que Hola clave de documento de detección de OpenID Connect de Hola o hello documento de metadatos de federación. Toocheck una manera para que esto es toodo una búsqueda en el código o el código de la biblioteca de Hola para las llamadas a cualquier documento de descubrimiento de tooeither Hola OpenID o documento de metadatos de federación de Hola.

Si la clave se almacena en algún lugar o codificado de forma rígida en la aplicación, puede preparar manualmente recuperar clave hello y según corresponda al realizar una sustitución manual según las instrucciones de hello final Hola de este documento de instrucciones de actualización. **Se recomienda encarecidamente que mejora la sustitución automática de toosupport de aplicación** mediante cualquiera de Hola aproxima contorno en interrupciones del artículo tooavoid futuras y la sobrecarga si aumenta su cadencia de sustitución de Azure AD o si tiene un sustitución de emergencia fuera de banda.

## <a name="how-tootest-your-application-toodetermine-if-it-will-be-affected"></a>Cómo tootest su toodetermine de aplicación si se verán afectado
Puede validar si la aplicación admite la sustitución de clave automática, se descargan las secuencias de comandos de Hola y siguiendo las instrucciones de hello en [este repositorio de GitHub.](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey)

## <a name="how-tooperform-a-manual-rollover-if-you-application-does-not-support-automatic-rollover"></a>¿Cómo tooperform una sustitución manual si, su aplicación no admite la sustitución automática
Si la aplicación **no** admite la sustitución automática, deberá tooestablish un proceso que periódicamente de monitores de Azure AD firma de claves y realiza una sustitución manual en consecuencia. [Este repositorio de GitHub](https://github.com/AzureAD/azure-activedirectory-powershell-tokenkey) contiene secuencias de comandos e instrucciones sobre cómo toodo esto.

