---
title: aaaCommunication seguridad - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
description: mitigaciones en busca de amenazas que se exponen en hello herramienta de modelado de amenazas
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: 667829c75123f4dbe0b383fdaf8cd899802f9b16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-communication-security--mitigations"></a>Marco de seguridad: Seguridad en las comunicaciones | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Centro de eventos de Azure** | <ul><li>[Comunicación segura tooEvent concentrador mediante SSL/TLS](#comm-ssltls)</li></ul> |
| **Dynamics CRM** | <ul><li>[Compruebe la cuenta de servicio privilegios y comprobar que Hola páginas ASP.NET o servicios personalizado respetan la seguridad de CRM](#priv-aspnet)</li></ul> |
| **Factoría de datos de Azure** | <ul><li>[Usar puerta de enlace de administración de datos durante la conexión en el servidor SQL local tooAzure factoría de datos](#sqlserver-factory)</li></ul> |
| **Identity Server** | <ul><li>[Asegúrese de que todos los tooIdentity tráfico servidor es a través de la conexión HTTPS](#identity-https)</li></ul> |
| **Aplicación web** | <ul><li>[Comprobar los certificados X.509 utilizan conexiones SSL, TLS y DTLS de tooauthenticate](#x509-ssltls)</li><li>[Configuración de un certificado SSL para un dominio personalizado en Azure App Service](#ssl-appservice)</li><li>[Forzar tooAzure todo tráfico servicio de aplicaciones a través de la conexión HTTPS](#appservice-https)</li><li>[Habilitación de seguridad de transporte estricto HTTP (HSTS)](#http-hsts)</li></ul> |
| **Base de datos** | <ul><li>[Comprobación de cifrado de la conexión de SQL Server y validación de certificados](#sqlserver-validation)</li><li>[Forzar que el servidor de tooSQL de comunicación cifrada](#encrypted-sqlserver)</li></ul> |
| **Azure Storage** | <ul><li>[Asegúrese de que tooAzure comunicación que almacenamiento es a través de HTTPS](#comm-storage)</li><li>[Validación de hash MD5 después de descargar blob si no se puede habilitar HTTPS](#md5-https)</li><li>[Use SMB 3.0 cliente compatible con tooensure tooAzure de cifrado de datos recursos compartidos de archivos en tránsito](#smb-shares)</li></ul> |
| **Cliente para dispositivos móviles** | <ul><li>[Implementación de asignación de certificados](#cert-pinning)</li></ul> |
| **WCF** | <ul><li>[Habilitación de HTTPS: canal de transporte seguro](#https-transport)</li><li>[WCF: TooEncryptAndSign de nivel de protección mensaje de conjunto de seguridad](#message-protection)</li><li>[WCF: Utilizar una cuenta con privilegios mínimos toorun el servicio WCF](#least-account-wcf)</li></ul> |
| **API web** | <ul><li>[Forzar tooWeb de tráfico todas las API a través de la conexión HTTPS](#webapi-https)</li></ul> |
| **Azure Redis Cache** | <ul><li>[Asegúrese de que tooAzure comunicación que caché en Redis es a través de SSL](#redis-ssl)</li></ul> |
| **Puerta de enlace de campo de IoT** | <ul><li>[Proteger la comunicación de puerta de enlace de dispositivo tooField](#device-field)</li></ul> |
| **Puerta de enlace de nube de IoT** | <ul><li>[Proteger dispositivos tooCloud comunicación de puerta de enlace mediante el uso de SSL/TLS](#device-cloud)</li></ul> |

## <a id="comm-ssltls"></a>Comunicación segura tooEvent concentrador mediante SSL/TLS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Centro de eventos de Azure | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Introducción al modelo de autenticación y seguridad de Event Hubs](https://azure.microsoft.com/documentation/articles/event-hubs-authentication-and-security-model-overview/) |
| **Pasos** | Proteger las conexiones del AMQP o HTTP tooEvent concentrador mediante SSL/TLS |

## <a id="priv-aspnet"></a>Compruebe la cuenta de servicio privilegios y comprobar que Hola páginas ASP.NET o servicios personalizado respetan la seguridad de CRM

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Compruebe la cuenta de servicio privilegios y comprobar que Hola páginas ASP.NET o servicios personalizado respetan la seguridad de CRM |

## <a id="sqlserver-factory"></a>Usar puerta de enlace de administración de datos durante la conexión en el servidor SQL local tooAzure factoría de datos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Data Factory | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Tipos de servicios vinculados: Azure y local |
| **Referencias**              |[Movimiento de datos entre orígenes locales y Azure Data Factory](https://azure.microsoft.com/documentation/articles/data-factory-move-data-between-onprem-and-cloud/#create-gateway), [Data Management Gateway](https://azure.microsoft.com/documentation/articles/data-factory-data-management-gateway/) |
| **Pasos** | <p>herramienta de puerta de enlace de administración de datos (DMG) de Hello es orígenes de toodata de tooconnect requiere que estén protegidos detrás de un firewall o red corporativa.</p><ol><li>Bloquear el equipo de hello aísla herramienta DMG de Hola e impide que los programas que no funciona bien dañar o supervisión de la máquina de origen de datos de Hola. (por ejemplo, deben instalarse las actualizaciones más recientes, habilitar los puertos mínimos necesarios, aprovisionar cuentas controladas, habilitar la auditoría, habilitar el cifrado de disco, etc.).</li><li>Clave de puerta de enlace de datos se debe girar a intervalos frecuentes o cada vez que se renueva la contraseña de la cuenta de servicio de hello DMG</li><li>El tránsito de datos a través del servicio de vínculos debe cifrarse.</li></ol> |

## <a id="identity-https"></a>Asegúrese de que todos los tooIdentity tráfico servidor es a través de la conexión HTTPS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Identity Server | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [IdentityServer3: claves, firmas y criptografía](https://identityserver.github.io/Documentation/docsv2/configuration/crypto.html), [IdentityServer3: implementación](https://identityserver.github.io/Documentation/docsv2/advanced/deployment.html) |
| **Pasos** | De forma predeterminada, IdentityServer requiere que todos los toocome las conexiones entrantes a través de HTTPS. Es absolutamente obligatorio que la comunicación con IdentityServer se realice exclusivamente a través de transportes seguros. En ciertos escenarios de implementación, como la descarga de SSL, este requisito puede ser más flexible. Consulte la página de implementación de servidor de identidades de hello en referencias de Hola para obtener más información. |

## <a id="x509-ssltls"></a>Comprobar los certificados X.509 utilizan conexiones SSL, TLS y DTLS de tooauthenticate

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | <p>Las aplicaciones que utilizan SSL, TLS y DTLS totalmente deben comprobar los certificados X.509 Hola de entidades de Hola que se conectan. Esto incluye la comprobación de certificados de Hola para:</p><ul><li>Nombre de dominio</li><li>Fechas de validez (fechas de inicio y caducidad)</li><li>Estado de revocación</li><li>Uso (por ejemplo, autenticación de servidor para servidores, autenticación de cliente para clientes)</li><li>Cadena de confianza: Certificados deben estar encadenados tooa raíz entidad emisora (CA que es de confianza para la plataforma de Hola o configurado explícitamente por el Administrador de Hola)</li><li>Longitud de la clave pública del certificado > 2048 bits</li><li>Algoritmo hash: SHA256 y versiones posteriores |

## <a id="ssl-appservice"></a>Configuración de un certificado SSL para un dominio personalizado en Azure App Service

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | EnvironmentType: Azure |
| **Referencias**              | [Habilitación de HTTPS para una aplicación en el servicio de aplicaciones de Azure](https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/) |
| **Pasos** | De forma predeterminada, Azure ya habilita HTTPS para todas las aplicaciones con un certificado comodín para Hola *. dominio azurewebsites.net. Sin embargo, al igual que todos los dominios comodín, no es tan seguro como usar un dominio personalizado con su propio certificado. [Más información](https://casecurity.org/2014/02/26/pros-and-cons-of-single-domain-multi-domain-and-wildcard-certificates/). Se recomienda tooenable SSL para qué aplicación Hola implementado se accederá a través de dominio personalizado de Hola|

## <a id="appservice-https"></a>Forzar tooAzure todo tráfico servicio de aplicaciones a través de la conexión HTTPS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | EnvironmentType: Azure |
| **Referencias**              | [Exigencia de HTTPS en Azure App Service]https://azure.microsoft.com/documentation/articles/web-sites-configure-ssl-certificate/#4-enforce-https-on-your-app) |
| **Pasos** | <p>Aunque Azure ya habilita HTTPS para servicios de aplicación de Azure con un certificado comodín para dominio Hola *. azurewebsites.net, no exigen HTTPS. Los visitantes todavía pueden acceder a la aplicación hello utilizando HTTP, que puede comprometer la seguridad de la aplicación hello y, por tanto, HTTPS tiene toobe aplica explícitamente. Las aplicaciones de MVC de ASP.NET deben utilizar hello [RequireHttps filtro](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) que fuerza una toobe de solicitud HTTP no segura que se vuelve a enviar a través de HTTPS.</p><p>O bien, el módulo URL Rewrite de hello, que se incluye con el servicio de aplicación de Azure puede ser tooenforce usa HTTPS. Módulo URL Rewrite permite a los desarrolladores toodefine reglas que se trata de solicitudes de tooincoming aplicados antes de que las solicitudes de Hola se entregan tooyour aplicación. Reglas de reescritura de direcciones URL se definen en un archivo web.config que se almacena en la raíz de Hola de aplicación hello</p>|

### <a name="example"></a>Ejemplo
el ejemplo siguiente se Hello contiene una regla básica de reescritura de direcciones URL que obliga a todas las toouse de tráfico HTTPS
```XML
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```
Esta regla funciona mediante la devolución de un código de estado HTTP de 301 (Redireccionamiento) cuando el usuario de hello solicita una página mediante HTTP. Hola 301 redirecciones Hola solicitud toohello misma dirección URL que visitante Hola solicitado, pero reemplaza Hola HTTP parte de la solicitud de hello con HTTPS. Por ejemplo, HTTP://contoso.com sería tooHTTPS://contoso.com redirigida. 

## <a id="http-hsts"></a>Habilitación de seguridad de transporte estricto HTTP (HSTS)

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Hoja de referencia rápida de seguridad de transporte estricto HTTP del Proyecto de seguridad de aplicación web abierta](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet) |
| **Pasos** | <p>Seguridad de transporte estricta de HTTP (HSTS) es una mejora de seguridad opcional que se especifica mediante una aplicación web mediante el uso de Hola de un encabezado de respuesta especial. Una vez que un explorador compatible recibe este encabezado ese explorador impide que todas las comunicaciones de ser enviados a través del dominio especificado de HTTP toohello y enviará en su lugar, todas las comunicaciones a través de HTTPS. También evita que aparezcan en los exploradores elementos click-through HTTPS.</p><p>tooimplement HSTS, Hola siguiente encabezado de respuesta tiene toobe configurado para un sitio Web globalmente, en el código o en la configuración. Strict-transporte-Security: max-age = 300; includeSubDomains HSTS direcciones Hola después de amenazas:</p><ul><li>Usuario marcadores o manualmente tipos http://example.com y es el atacante de man-in-the-middle tooa asunto: HSTS redirige automáticamente tooHTTPS de las solicitudes HTTP para el dominio de destino de Hola</li><li>Aplicación que está previsto toobe puramente HTTPS sin darse cuenta contiene vínculos HTTP o sirve contenido a través de HTTP Web: HSTS redirige automáticamente tooHTTPS de las solicitudes HTTP para el dominio de destino de Hola</li><li>Un atacante man-in-the-middle intenta toointercept tráfico de un usuario de la víctima utilizando un certificado no válido y espera usuario Hola aceptará certificado incorrecto hello: HSTS no permite que un mensaje de certificado no válido de usuario toooverride Hola</li></ul>|

## <a id="sqlserver-validation"></a>Comprobación de cifrado de la conexión de SQL Server y validación de certificados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure  |
| **Atributos**              | Versión de SQL: V12 |
| **Referencias**              | [Procedimientos recomendados sobre cómo escribir cadenas de conexión seguras para SQL Database](http://social.technet.microsoft.com/wiki/contents/articles/2951.windows-azure-sql-database-connection-security.aspx#best) |
| **Pasos** | <p>Todas las comunicaciones entre SQL Database y una aplicación cliente se cifran mediante capa de sockets seguros (SSL) en todo momento. SQL Database no admite conexiones no cifradas. certificados de toovalidate con código de aplicación o herramientas, solicitar una conexión cifrada y no confiar en certificados de servidor hello explícitamente. Si el código de su aplicación o las herramientas no solicitan una conexión cifrada, seguirán recibiendo conexiones cifradas.</p><p>Sin embargo, no se pueden validar los certificados de servidor hello y por lo tanto son susceptible de sufrir demasiado ataques de "tipo man in intermedio Hola". conjunto de certificados de toovalidate con código de la aplicación de ADO.NET, `Encrypt=True` y `TrustServerCertificate=False` en la cadena de conexión de base de datos de Hola. toovalidate certificados a través de SQL Server Management Studio, Abrir cuadro de diálogo de hello conectar tooServer. Haga clic en conexión de cifrado en la ficha de propiedades de conexión de Hola</p>|

## <a id="encrypted-sqlserver"></a>Forzar que el servidor de tooSQL de comunicación cifrada

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | OnPrem |
| **Atributos**              | Versión de SQL: MsSQL2016, Versión de SQL: MsSQL2012, Versión de SQL: MsSQL2014 |
| **Referencias**              | [Habilitar conexiones cifradas toohello motor de base de datos](https://msdn.microsoft.com/library/ms191192)  |
| **Pasos** | Habilitación de SSL cifrado aumenta la seguridad de Hola de datos que se transmiten a través de redes entre instancias de SQL Server y las aplicaciones. |

## <a id="comm-storage"></a>Asegúrese de que tooAzure comunicación que almacenamiento es a través de HTTPS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Azure Storage: Cifrado de nivel de transporte – Uso de HTTPS](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_encryption-in-transit) |
| **Pasos** | seguridad de hello tooensure de datos de los almacenamiento de Azure en tránsito, utilice siempre protocolo HTTPS de hello al llamar a las API de REST de Hola o tiene acceso a objetos en el almacenamiento. Además, firmas de acceso compartido, que puede ser usado toodelegate tener acceso a objetos de almacenamiento de tooAzure, incluyen una opción toospecify ese Hola solo puede usar el protocolo HTTPS al utilizar firmas de acceso compartido, asegurándose de que cualquier usuario enviar vínculos con tokens SAS será Usar protocolo adecuado Hola.|

## <a id="md5-https"></a>Validación de hash MD5 después de descargar blob si no se puede habilitar HTTPS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | StorageType: blob |
| **Referencias**              | [Información general de MD5 de Windows Azure Blob](https://blogs.msdn.microsoft.com/windowsazurestorage/2011/02/17/windows-azure-blob-md5-overview/) |
| **Pasos** | <p>Servicio de Blob de Windows Azure proporciona mecanismos tooensure integridad de los datos en la aplicación hello y capas de transporte. Si por algún motivo necesita toouse HTTP en lugar de HTTPS y está trabajando con los blobs en bloques, puede usar la comprobación de MD5 toohelp comprobar integridad de Hola de blobs de Hola que se transfieren</p><p>Esto le ayudará con la protección frente a errores de red o de la capa de transporte, pero no necesariamente con ataques de intermediarios. Si puede usar HTTPS, que proporciona seguridad de nivel de transporte, el uso de la comprobación de MD5 es redundante e innecesario.</p>|

## <a id="smb-shares"></a>Usar tooAzure de cifrado de datos en tránsito en tooensure de SMB 3.0 cliente compatible con que recursos compartidos de archivos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvil | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | StorageType: archivo |
| **Referencias**              | [Azure File Storage](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/#comment-2529238931), [Compatibilidad con SMB de Azure File Storage para clientes de Windows](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-files/#_mount-the-file-share) |
| **Pasos** | Almacenamiento de archivos de Azure admite HTTPS cuando se utiliza la API de REST de hello, pero es más comúnmente usado como un recurso compartido de archivos SMB adjunta tooa máquina virtual. SMB 2.1 no admite el cifrado, por lo que las conexiones se permiten únicamente en hello mismo región de Azure. Sin embargo, SMB 3.0 admite el cifrado y se puede utilizar con Windows Server 2012 R2, Windows 8, Windows 8.1 y Windows 10, lo que permite entre regiones accedan e incluso acceso en el escritorio de Hola. |

## <a id="cert-pinning"></a>Implementación de asignación de certificados

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, Windows Phone |
| **Atributos**              | N/D  |
| **Referencias**              | [Asignación de certificados y claves públicas](https://www.owasp.org/index.php/Certificate_and_Public_Key_Pinning#.Net) |
| **Pasos** | <p>La asignación de certificados protege frente a ataques de tipo "man in the middle". Fijar es el proceso de Hola de asociar un host con sus X509 esperado certificado o clave pública. Una vez que se sabe o se ve para un host de un certificado o clave pública, Hola certificado o clave pública es toohello asociados o 'anclados' host. </p><p>Por lo tanto, cuando un adversario intenta toodo ataque MITM SSL, durante la clave de Hola de protocolo de enlace SSL de servidor del atacante serán diferente de hello anclado clave del certificado y se descartará la solicitud de hello, evitando MITM certificado fijar puede lograrse implementación del ServicePointManager `ServerCertificateValidationCallback` delegar.</p>|

### <a name="example"></a>Ejemplo
```C#
using System;
using System.Net;
using System.Net.Security;
using System.Security.Cryptography;

namespace CertificatePinningExample
{
    class CertificatePinningExample
    {
        /* Note: In this example, we're hardcoding a hello certificate's public key and algorithm for 
           demonstration purposes. In a real-world application, this should be stored in a secure
           configuration area that can be updated as needed. */

        private static readonly string PINNED_ALGORITHM = "RSA";

        private static readonly string PINNED_PUBLIC_KEY = "3082010A0282010100B0E75B7CBE56D31658EF79B3A1" +
            "294D506A88DFCDD603F6EF15E7F5BCBDF32291EC50B2B82BA158E905FE6A83EE044A48258B07FAC3D6356AF09B2" +
            "3EDAB15D00507B70DB08DB9A20C7D1201417B3071A346D663A241061C151B6EC5B5B4ECCCDCDBEA24F051962809" +
            "FEC499BF2D093C06E3BDA7D0BB83CDC1C2C6660B8ECB2EA30A685ADE2DC83C88314010FFC7F4F0F895EDDBE5C02" +
            "ABF78E50B708E0A0EB984A9AA536BCE61A0C31DB95425C6FEE5A564B158EE7C4F0693C439AE010EF83CA8155750" +
            "09B17537C29F86071E5DD8CA50EBD8A409494F479B07574D83EDCE6F68A8F7D40447471D05BC3F5EAD7862FA748" +
            "EA3C92A60A128344B1CEF7A0B0D94E50203010001";


        public static void Main(string[] args)
        {
            HttpWebRequest request = (HttpWebRequest)WebRequest.Create("https://azure.microsoft.com");
            request.ServerCertificateValidationCallback = (sender, certificate, chain, sslPolicyErrors) =>
            {
                if (certificate == null || sslPolicyErrors != SslPolicyErrors.None)
                {
                    // Error getting certificate or hello certificate failed basic validation
                    return false;
                }

                var targetKeyAlgorithm = new Oid(certificate.GetKeyAlgorithm()).FriendlyName;
                var targetPublicKey = certificate.GetPublicKeyString();
                
                if (targetKeyAlgorithm == PINNED_ALGORITHM &&
                    targetPublicKey == PINNED_PUBLIC_KEY)
                {
                    // Success, hello certificate matches hello pinned value.
                    return true;
                }
                // Reject, either hello key or hello algorithm does not match hello expected value.
                return false;
            };

            try
            {
                var response = (HttpWebResponse)request.GetResponse();
                Console.WriteLine($"Success, HTTP status code: {response.StatusCode}");
            }
            catch(Exception ex)
            {
                Console.WriteLine($"Failure, {ex.Message}");
            }
            Console.WriteLine("Press any key tooend.");
            Console.ReadKey();
        }
    }
}
```

## <a id="https-transport"></a>Habilitación de HTTPS: canal de transporte seguro

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | configuración de la aplicación Hello debe asegurarse de que se utiliza HTTPS para toda la información de acceso toosensitive.<ul><li>**Explicación:** si una aplicación controla la información confidencial y no usa el cifrado de nivel de mensaje, que solo se debe poder toocommunicate través de un canal de transporte cifrados.</li><li>**RECOMENDACIONES:** asegúrese de que el transporte HTTP está deshabilitado y habilite el transporte HTTPS en su lugar. Por ejemplo, reemplace hello `<httpTransport/>` con `<httpsTransport/>` etiqueta. No se debe confiar en un tooguarantee de configuración (firewall) de red que la aplicación hello solo son accesibles por un canal seguro. Desde un punto de vista filosófica, aplicación hello no debe depender red Hola para su seguridad.</li></ul><p>Desde un punto de vista práctico, personas Hola responsables de proteger la red de Hola no siempre realizar un seguimiento de los requisitos de seguridad de Hola de aplicación hello medida que evolucionan.</p>|

## <a id="message-protection"></a>WCF: TooEncryptAndSign de nivel de protección mensaje de conjunto de seguridad

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff650862.aspx) |
| **Pasos** | <ul><li>**Explicación:** al nivel de protección se establece demasiado "" se deshabilitará la protección de mensajes. La confidencialidad e integridad requieren definir un nivel adecuado.</li><li>**RECOMENDACIONES:**<ul><li>si `Mode=None`: deshabilita la protección del mensaje.</li><li>Cuando `Mode=Sign` -signos pero no cifra los mensajes de bienvenida; debe usarse cuando la integridad de los datos es importante</li><li>Cuando `Mode=EncryptAndSign` -firma y cifra el mensaje de bienvenida</li></ul></li></ul><p>Considere la posibilidad de desactivar el cifrado y firma sólo el mensaje cuando basta con integridad de hello toovalidate de información de hello sin preocuparse de confidencialidad. Esto puede resultar útil para las operaciones o los contratos de servicios en la que necesita el remitente original de toovalidate Hola pero ningún dato confidencial se transmite. Al reducir el nivel de protección de hello, tenga cuidado de que ese mensaje Hola no contiene ninguna información personal identificable (PII).</p>|

### <a name="example"></a>Ejemplo
Configuración de Hola y mensaje de saludo de hello operación tooonly inicio de sesión se muestra en hello en los ejemplos siguientes. Ejemplo de contrato de servicio de `ProtectionLevel.Sign`: Hola siguiente es un ejemplo del uso de ProtectionLevel.Sign en el nivel del contrato de servicio de hello: 
```
[ServiceContract(Protection Level=ProtectionLevel.Sign] 
public interface IService 
  { 
  string GetData(int value); 
  } 
```

### <a name="example"></a>Ejemplo
Ejemplo de contrato de operación de `ProtectionLevel.Sign` (para un Control detallado): Hola siguiente es un ejemplo del uso de `ProtectionLevel.Sign` en hello OperationContract nivel:

```
[OperationContract(ProtectionLevel=ProtectionLevel.Sign] 
string GetData(int value);
``` 

## <a id="least-account-wcf"></a>WCF: Utilizar una cuenta con privilegios mínimos toorun el servicio WCF

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648826.aspx ) |
| **Pasos** | <ul><li>**EXPLICACIÓN:** no ejecute servicios WCF en una cuenta de administrador o con privilegios elevados. Esto tendría una gran incidencia en caso de que los servicios se vieran comprometidos.</li><li>**RECOMENDACIONES:** utilizar un toohost cuenta con menos privilegios su WCF del servicio, porque reduce la superficie expuesta a ataques de su aplicación y reducir los daños potenciales de hello si están atacadas. Si la cuenta de servicio de hello requiere derechos de acceso adicionales en los recursos de infraestructura como MSMQ, hello permisos adecuados de registro de eventos, contadores de rendimiento y sistema de archivos de hello, tendrá recursos toothese para que pueda ejecutar el servicio WCF de Hola se estableció correctamente.</li></ul><p>Si el servicio necesita recursos específicos de tooaccess en nombre del llamador original hello, utilice suplantación y la identidad del llamador de delegación tooflow Hola para una comprobación de autorización de nivel inferior. En un escenario de desarrollo, use la cuenta de servicio de red local de hello, que es una cuenta integrada especial que tiene privilegios reducidos. En un escenario de producción, cree una cuenta de servicio de dominio personalizado con privilegios mínimos.</p>|

## <a id="webapi-https"></a>Forzar tooWeb de tráfico todas las API a través de la conexión HTTPS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | [Aplicación de SSL en un controlador de API web](http://www.asp.net/web-api/overview/security/working-with-ssl-in-web-api) |
| **Pasos** | Si una aplicación tiene un HTTPS y un enlace HTTP, los clientes todavía pueden usar sitio de hello tooaccess HTTP. tooprevent, use un tooensure de filtro de acción que solicita tooprotected API son siempre a través de HTTPS.|

### <a name="example"></a>Ejemplo 
Hello código siguiente muestra un filtro de autenticación de API Web que se comprueba para SSL: 
```C#
public class RequireHttpsAttribute : AuthorizationFilterAttribute
{
    public override void OnAuthorization(HttpActionContext actionContext)
    {
        if (actionContext.Request.RequestUri.Scheme != Uri.UriSchemeHttps)
        {
            actionContext.Response = new HttpResponseMessage(System.Net.HttpStatusCode.Forbidden)
            {
                ReasonPhrase = "HTTPS Required"
            };
        }
        else
        {
            base.OnAuthorization(actionContext);
        }
    }
}
```
Agregue acciones de tooany API Web este filtro que requieran SSL: 
```C#
public class ValuesController : ApiController
{
    [RequireHttps]
    public HttpResponseMessage Get() { ... }
}
```
 
## <a id="redis-ssl"></a>Asegúrese de que tooAzure comunicación que caché en Redis es a través de SSL

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Redis Cache | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Soporte técnico de Azure Redis SSL](https://azure.microsoft.com/documentation/articles/cache-faq/#when-should-i-enable-the-non-ssl-port-for-connecting-to-redis) |
| **Pasos** | Redis server no admite SSL fuera del cuadro de hello, pero hace de caché en Redis de Azure. Si se va a conectar tooAzure caché en Redis y el cliente admite SSL, como StackExchange.Redis, a continuación, debe usar SSL. De forma predeterminada, el puerto no SSL está deshabilitado para las instancias nuevas de Azure Redis Cache. Asegúrese de que no se cambian los valores predeterminados seguros de Hola a menos que haya una dependencia sobre la compatibilidad con SSL para que los clientes de redis. |

Tenga en cuenta que Redis es toobe diseñada tiene acceso a los clientes de confianza dentro de entornos de confianza. Esto significa que normalmente no es una buena idea tooexpose Hola Redis directamente instancia toohello internet o, en general, entorno tooan donde pueden tener acceso directamente los clientes sin confianza Hola el puerto TCP Redis o socket de UNIX. 

## <a id="device-field"></a>Proteger la comunicación de puerta de enlace de dispositivo tooField

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de campo de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Para los dispositivos basados en IP, protocolo de comunicación de hello normalmente se puede encapsular en un datos de tooprotect un canal SSL/TLS en tránsito. Para otros protocolos que no admiten SSL/TLS investigue si hay versiones seguras de protocolo de Hola que proporcionan seguridad en la capa de transporte o de mensaje. |

## <a id="device-cloud"></a>Proteger dispositivos tooCloud comunicación de puerta de enlace mediante el uso de SSL/TLS

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Puerta de enlace de la nube de IoT | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Elección del protocolo de comunicación](https://azure.microsoft.com/documentation/articles/iot-hub-devguide/#messaging) |
| **Pasos** | Proteja los protocolos HTTP/AMQP o MQTT mediante SSL/TLS. |
