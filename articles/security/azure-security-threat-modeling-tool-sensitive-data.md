---
title: aaaSensitive datos - herramienta de modelado de amenazas de Microsoft - Azure | Documentos de Microsoft
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
ms.openlocfilehash: 8a18f43af439241ba193ccf668971ddc4655355f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-frame-sensitive-data--mitigations"></a>Marco de seguridad: Información confidencial | Mitigaciones 
| Producto o servicio | Artículo |
| --------------- | ------- |
| **Límite de confianza de la máquina** | <ul><li>[Asegúrese de que los archivos binarios estén ofuscados si contienen información confidencial](#binaries-info)</li><li>[Tenga en cuenta el uso de sistema de archivos cifrados (EFS) es tooprotect usado confidencial específica del usuario](#efs-user)</li><li>[Asegúrese de que se cifran los datos confidenciales almacenados por la aplicación hello en el sistema de archivos de Hola](#filesystem)</li></ul> | 
| **Aplicación web** | <ul><li>[Asegúrese de que no se almacena en el explorador Hola de caché de contenido confidencial](#cache-browser)</li><li>[Cifre las secciones de los archivos de configuración de la aplicación web que contengan información confidencial](#encrypt-data)</li><li>[Deshabilitar explícitamente el atributo HTML de Autocompletar hello en los formularios confidenciales y entradas](#autocomplete-input)</li><li>[Asegúrese de que los datos confidenciales que se muestra en pantalla de bienvenida usuario se enmascaran](#data-mask)</li></ul> | 
| **Base de datos** | <ul><li>[Implementar los usuarios de enmascaramiento toolimit exposición de información confidencial no privilegiado de datos dinámicos](#dynamic-users)</li><li>[Asegúrese de que las contraseñas se almacenen en formato de hash con sal](#salted-hash)</li><li>[Asegúrese de que la información confidencial en las columnas de la base de datos esté cifrada](#db-encrypted)</li><li>[Asegúrese de que el cifrado de base de datos (TDE) esté habilitado](#tde-enabled)</li><li>[Asegúrese de que las copias de seguridad de la base de datos estén cifradas](#backup)</li></ul> | 
| **API web** | <ul><li>[Asegúrese de que tooWeb relevante de los datos confidenciales que API no se almacena en el almacenamiento del explorador](#api-browser)</li></ul> | 
| Azure DocumentDB | <ul><li>[Cifre la información confidencial almacenada en DocumentDB](#encrypt-docdb)</li></ul> | 
| **Límites de confianza de VM de IaaS de Azure** | <ul><li>[Utilizar discos de tooencrypt de cifrado del disco de Azure utilizados por máquinas virtuales](#disk-vm)</li></ul> | 
| **Límites de confianza de Service Fabric** | <ul><li>[Cifre los secretos en aplicaciones de Service Fabric](#fabric-apps)</li></ul> | 
| **Dynamics CRM** | <ul><li>[Realice el modelado de seguridad y use unidades de negocio y equipos cuando sea necesario](#modeling-teams)</li><li>[Minimizar la característica de acceso tooshare en entidades críticas](#entities)</li><li>[Entrenamiento de los usuarios en los riesgos de hello asociados con la característica de recurso compartido de Dynamics CRM hello y buenas prácticas de seguridad](#good-practices)</li><li>[Incluya una regla de estándares de desarrollo que prohíba mostrar detalles de configuración en la administración de excepciones](#exception-mgmt)</li></ul> | 
| **Azure Storage** | <ul><li>[Use el cifrado del servicio Azure Storage (SSE) para datos en reposo (versión preliminar)](#sse-preview)</li><li>[Usar datos confidenciales de toostore de cifrado en el cliente en el almacenamiento de Azure](#client-storage)</li></ul> | 
| **Cliente para dispositivos móviles** | <ul><li>[Cifrar confidencial o datos PII escritos toophones de almacenamiento local](#pii-phones)</li><li>[Ofuscar archivos binarios generados antes de distribuir los usuarios tooend](#binaries-end)</li></ul> | 
| **WCF** | <ul><li>[Conjunto clientCredentialType tooCertificate o Windows](#cert)</li><li>[El modo de seguridad de WCF no está habilitado](#security)</li></ul> | 

## <a id="binaries-info"></a>Asegúrese de que los archivos binarios estén ofuscados si contienen información confidencial

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que los archivos binarios estén ofuscados si contienen información confidencial como secretos comerciales o lógica de negocios confidencial que no se deba revelar. Se trata de toostop de ensamblados de ingeniería inversa. Para este fin se pueden usar herramientas como `CryptoObfuscator`. |

## <a id="efs-user"></a>Tenga en cuenta el uso de sistema de archivos cifrados (EFS) es tooprotect usado confidencial específica del usuario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Considere usar el sistema de archivos cifrados (EFS) es específica del usuario confidencial tooprotect usado desde adversarios con el equipo de toohello de acceso física. |

## <a id="filesystem"></a>Asegúrese de que se cifran los datos confidenciales almacenados por la aplicación hello en el sistema de archivos de Hola

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límite de confianza de la máquina | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Asegúrese de que se cifran los datos confidenciales almacenados por la aplicación hello en el sistema de archivos de hello (p. ej., el uso de DPAPI) si no se puede aplicar EFS |

## <a id="cache-browser"></a>Asegúrese de que no se almacena en el explorador Hola de caché de contenido confidencial

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, formularios Web Forms, MVC5, MVC6 |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Los exploradores pueden almacenar información para la memoria caché y el historial. Estos archivos almacenados en caché se almacenan en una carpeta, como la carpeta de archivos temporales de Internet de hello en caso de hello de Internet Explorer. Cuando estas páginas se conocen nuevo, Explorador de hello muestra desde la memoria caché. Si la información confidencial es usuario toohello mostrado (por ejemplo, su dirección, detalles de la tarjeta de crédito, número del seguro Social o nombre de usuario), esta información podría estar almacenado en memoria caché del explorador y, por tanto, puede recuperar a través de examen de la memoria caché del explorador de Hola o simplemente presione botón "Atrás" del explorador de Hola. Establezca el valor de encabezado de respuesta de cache-control demasiado "no-store" para todas las páginas. |

### <a name="example"></a>Ejemplo
```XML
<configuration>
  <system.webServer>
   <httpProtocol>
    <customHeaders>
        <add name="Cache-Control" value="no-cache" />
        <add name="Pragma" value="no-cache" />
        <add name="Expires" value="-1" />
    </customHeaders>
  </httpProtocol>
 </system.webServer>
</configuration>
```

### <a name="example"></a>Ejemplo
Esto se puede implementar por medio de un filtro. Puede usar el siguiente ejemplo: 
```C#
public override void OnActionExecuting(ActionExecutingContext filterContext)
        {
            if (filterContext == null || (filterContext.HttpContext != null && filterContext.HttpContext.Response != null && filterContext.HttpContext.Response.IsRequestBeingRedirected))
            {
                //// Since this is MVC pipeline, this should never be null.
                return;
            }

            var attributes = filterContext.ActionDescriptor.GetCustomAttributes(typeof(System.Web.Mvc.OutputCacheAttribute), false);
            if (attributes == null || **Attributes**.Count() == 0)
            {
                filterContext.HttpContext.Response.Cache.SetNoStore();
                filterContext.HttpContext.Response.Cache.SetCacheability(HttpCacheability.NoCache);
                filterContext.HttpContext.Response.Cache.SetExpires(DateTime.UtcNow.AddHours(-1));
                if (!filterContext.IsChildAction)
                {
                    filterContext.HttpContext.Response.AppendHeader("Pragma", "no-cache");
                }
            }

            base.OnActionExecuting(filterContext);
        }
``` 

## <a id="encrypt-data"></a>Cifre las secciones de los archivos de configuración de la aplicación web que contengan información confidencial

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Cómo: Cifrar secciones de configuración en ASP.NET 2.0 utilizando DPAPI](https://msdn.microsoft.com/library/ff647398.aspx), [especificar un proveedor de configuración protegida](https://msdn.microsoft.com/library/68ze1hb2.aspx), [secretos de aplicación de tooprotect con el almacén de claves de Azure](https://azure.microsoft.com/documentation/articles/guidance-multitenant-identity-keyvault/) |
| **Pasos** | Archivos de configuración como Web.config hello, appSettings.JSON que se suelen usar toohold información confidencial, incluidos los nombres de usuario, contraseñas, las cadenas de conexión de base de datos y las claves de cifrado. Si no protege esta información, la aplicación es vulnerable tooattackers o usuarios malintencionados obtener información confidencial, como nombres de cuenta de usuario y contraseñas, nombres de base de datos y nombres de servidor. Según el tipo de implementación de hello (azure/local), cifrar secciones confidenciales de Hola de archivos de configuración mediante DPAPI o servicios como almacén de claves de Azure. |

## <a id="autocomplete-input"></a>Deshabilitar explícitamente el atributo HTML de Autocompletar hello en los formularios confidenciales y entradas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [MSDN: autocomplete attribute](http://msdn.microsoft.com/library/ms533486(VS.85).aspx) (MSDN: atributo autocomplete), [Using Autocomplete en HTML forms](http://msdn.microsoft.com/library/ms533032.aspx) (Uso de Autocompletar en formularios HTML), [Vulnerabilidad en la comprobación del estado de HTML](http://technet.microsoft.com/security/bulletin/MS10-071), [Autocomplete.,again?!](http://blog.mindedsecurity.com/2011/10/autocompleteagain.html) (Vuelta a Autocompletar) |
| **Pasos** | atributo de Autocompletar Hola especifica si un formulario debe Autocompletar o desactivar. Cuando Autocompletar está activada, valores automáticamente completa del explorador Hola basados en valores ese usuario Hola ha escrito antes. Por ejemplo, cuando se introduce un nuevo nombre y una contraseña en un formulario y se envía el formulario de hello, explorador Hola le pregunta si se debe guardar la contraseña de Hola. A partir de ahí cuando se muestra la forma de hello, Hola nombre y la contraseña se rellenan automáticamente o se completan tal y como se especifica el nombre de Hola. Un atacante con acceso local podría obtener contraseña de texto no cifrado de Hola de caché del explorador de Hola. De forma predeterminada, la función Autocompletar está habilitada y se debe deshabilitar explícitamente. |

### <a name="example"></a>Ejemplo
```C#
<form action="Login.aspx" method="post " autocomplete="off" >
      Social Security Number: <input type="text" name="ssn" />
      <input type="submit" value="Submit" />    
</form>
```

## <a id="data-mask"></a>Asegúrese de que los datos confidenciales que se muestra en pantalla de bienvenida usuario se enmascaran

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Aplicación web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Datos confidenciales, como contraseñas, números de tarjeta de crédito, etc. SSN se deben enmascarar cuando se muestra en la pantalla de bienvenida. Se trata de personal tooprevent no autorizado tengan acceso a datos de hello (p. ej., contraseñas de navegación de hombro, personal de soporte técnico ver números de SSN de usuarios). Asegúrese de que estos elementos de datos no sean visibles sin cifrar y que estén enmascarados correctamente. Esto tiene toobe tenerse en cuenta al aceptarlas como entrada (por ejemplo. tipo de entrada = "contraseña"), así como mostrar en pantalla de bienvenida (p. ej., mostrar sólo Hola últimos 4 dígitos del número de tarjeta de crédito de hello). |

## <a id="dynamic-users"></a>Implementar los usuarios de enmascaramiento toolimit exposición de información confidencial no privilegiado de datos dinámicos

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure, OnPrem |
| **Atributos**              | Versión de SQL: V12, versión de SQL: MsSQL2016 |
| **Referencias**              | [Enmascaramiento de datos dinámicos](https://msdn.microsoft.com/library/mt130841) |
| **Pasos** | Hola de enmascaramiento dinámico de datos sirve toolimit exposición de datos confidenciales, evitar que los usuarios que no deberían poder acceder a los datos toohello vean. Enmascaramiento dinámico de datos no tienen como objetivo tooprevent usuarios de base de datos de base de datos de toohello la conexión directa y ejecuten consultas exhaustivas que expongan de datos confidenciales de Hola. Enmascaramiento dinámico de datos es tooother complementario de la características de seguridad de SQL Server (auditoría, cifrado, seguridad de nivel de fila …) y se recomienda encarecidamente toouse esta característica junto con ellas además en orden toobetter proteger los datos confidenciales de Hola Hola base de datos. Tenga en cuenta que esta característica solo es compatible con SQL Server a partir de 2016 y Azure SQL Database. |

## <a id="salted-hash"></a>Asegúrese de que las contraseñas se almacenen en formato de hash con sal

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Hash de contraseña mediante las API de criptografía de .NET](http://docs.asp.net/en/latest/security/data-protection/consumer-apis/password-hashing.html) |
| **Pasos** | Las contraseñas no se deberían almacenar en bases de datos de almacén de usuarios personalizadas. En su lugar, los hash de contraseña se deben almacenar con valores sal. Asegúrese de que el valor "salt" de hello para el usuario de hello siempre es única y aplicar crypt b, s crypt o PBKDF2 antes de almacenar contraseñas de hello, con un número de iteraciones de factor de trabajo mínimo de 150.000 bucles tooeliminate posibilidad de Hola de fuerza bruta.| 

## <a id="db-encrypted"></a>Asegúrese de que la información confidencial en las columnas de la base de datos esté cifrada

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Versión de SQL: todas |
| **Referencias**              | [Cifrar datos confidenciales en SQL Server](https://technet.microsoft.com/library/ff848751(v=sql.105).aspx), [Cifrar una columna de datos en SQL Server](https://msdn.microsoft.com/library/ms179331), [Cifrado mediante certificados](https://msdn.microsoft.com/library/ms188061) |
| **Pasos** | Los datos confidenciales, como números de tarjeta de crédito tienen toobe cifrado en la base de datos de Hola. Los datos se pueden cifrar mediante el cifrado de nivel de columna o una función de aplicación mediante las funciones de cifrado de Hola. |

## <a id="tde-enabled"></a>Asegúrese de que el cifrado de base de datos (TDE) esté habilitado

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Descripción del Cifrado de datos transparente (TDE) en SQL Server](https://technet.microsoft.com/library/bb934049(v=sql.105).aspx) |
| **Pasos** | Cifrado de datos transparente (TDE) de características de SQL server permite cifrar datos confidenciales en una base de datos y proteger las claves de Hola que son utilizados tooencrypt Hola datos con un certificado. Esto evita que cualquiera que carezca de las claves de hello del uso de datos de Hola. TDE protege los datos "en reposo", lo que significa que los archivos de datos y de registro de hello. Proporciona Hola capacidad toocomply con muchas leyes, normativas y directrices establecidas en diversos sectores. |

## <a id="backup"></a>Asegúrese de que las copias de seguridad de la base de datos estén cifradas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Base de datos | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | SQL Azure, OnPrem |
| **Atributos**              | Versión de SQL: V12, versión de SQL: MsSQL2014 |
| **Referencias**              | [Cifrado de copia de seguridad de bases de datos SQL](https://msdn.microsoft.com/library/dn449489) |
| **Pasos** | SQL Server tiene datos de saludo de hello capacidad tooencrypt al crear una copia de seguridad. Al especificar el algoritmo de cifrado de Hola y sistema de cifrado de hello (un certificado o clave asimétrica) al crear una copia de seguridad, uno puede crear un archivo de copia de seguridad cifrado. |

## <a id="api-browser"></a>Asegúrese de que tooWeb relevante de los datos confidenciales que API no se almacena en el almacenamiento del explorador

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | API Web | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | MVC 5, MVC 6 |
| **Atributos**              | Proveedor de identidades; ADFS, Proveedor de identidades; Azure AD |
| **Referencias**              | N/D  |
| **Pasos** | <p>En algunas implementaciones, tooWeb relevantes de artefactos confidencial de la API de autenticación se almacenan en el almacenamiento local del explorador. Por ejemplo, artefactos de autenticación de Azure AD como adal.idtoken, adal.nonce.idtoken, adal.access.token.key, adal.token.keys, adal.state.login, adal.session.state, adal.expiration.key, etc.</p><p>Todos estos artefactos están disponibles aun después de que se cierren la sesión o el explorador. Si un adversario obtiene acceso a los artefactos de toothese, si puede volver a usarlos recursos de hello protegido tooaccess (API). Asegúrese de que todos los artefactos sensibles a relacionados tooWeb API no se almacena de forma del explorador. En casos donde el almacenamiento del lado cliente es inevitable (p. ej., única página aplicaciones contraseña segura (SPA) que aprovechan implícita OpenIdConnect/OAuth flujos necesario toostore localmente los tokens de acceso), use las opciones de almacenamiento con no tienen persistencia. Por ejemplo, se prefiere SessionStorage tooLocalStorage.</p>| 

### <a name="example"></a>Ejemplo
Hola por debajo de fragmento de código de JavaScript es de una biblioteca de autenticación personalizada que almacena los artefactos de autenticación en el almacenamiento local. Se deben evitar estas implementaciones. 
```javascript
ns.AuthHelper.Authenticate = function () {
window.config = {
instance: 'https://login.microsoftonline.com/',
tenant: ns.Configurations.Tenant,
clientId: ns.Configurations.AADApplicationClientID,
postLogoutRedirectUri: window.location.origin,
cacheLocation: 'localStorage', // enable this for IE, as sessionStorage does not work for localhost.
};
```

## <a id="encrypt-docdb"></a>Cifre la información confidencial almacenada en Cosmos DB

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure DocumentDB | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Cifre la información confidencial en el nivel de aplicación antes de almacenarla en DocumentDB o almacene cualquier información confidencial en otras soluciones de almacenamiento como Azure Storage o SQL de Azure.| 

## <a id="disk-vm"></a>Utilizar discos de tooencrypt de cifrado del disco de Azure utilizados por máquinas virtuales

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de máquinas virtuales de IaaS de Azure | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Mediante el cifrado de disco de Azure usan discos tooencrypt las máquinas virtuales](https://azure.microsoft.com/documentation/articles/storage-security-guide/#_using-azure-disk-encryption-to-encrypt-disks-used-by-your-virtual-machines) |
| **Pasos** | <p>El Cifrado de discos de Azure es una nueva característica que está actualmente en su versión preliminar. Esta característica permite tooencrypt discos de sistemas operativos de Hola y discos de datos usados por una máquina Virtual de IaaS. Para Windows, las unidades de Hola se cifran mediante tecnología de cifrado de BitLocker de estándar del sector. Para Linux, discos de Hola se cifran mediante la tecnología de hello DM Crypt. Esto está integrado con el almacén de claves de Azure tooallow se toocontrol y administrar claves de cifrado de disco de Hola. Hola soluciones de cifrado del disco de Azure admite Hola tres escenarios de cifrado de cliente siguientes:</p><ul><li>Habilitar el cifrado en nuevas máquinas virtuales de IaaS creadas a partir de archivos VHD cifrados por el cliente y claves de cifrado proporcionadas por el cliente, que se almacenan en el Almacén de claves de Azure.</li><li>Habilitar el cifrado en nuevas máquinas virtuales de IaaS creado a partir de hello Azure Marketplace.</li><li>Habilitar el cifrado en máquinas virtuales de IaaS existentes que ya se ejecutan en Azure.</li></ul>| 

## <a id="fabric-apps"></a>Cifre los secretos en aplicaciones de Service Fabric

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Límites de confianza de Service Fabric | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | Entorno: Azure |
| **Referencias**              | [Administración de secretos en aplicaciones de Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-application-secret-management/) |
| **Pasos** | Los secretos pueden ser cualquier información confidencial, como cadenas de conexión de almacenamiento, contraseñas u otros valores que no se deben administrar en texto sin formato. Usar el almacén de claves de Azure toomanage claves y secretos fabric en aplicaciones de servicio. |

## <a id="modeling-teams"></a>Realice el modelado de seguridad y use unidades de negocio y equipos cuando sea necesario

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Realice el modelado de seguridad y use unidades de negocio y equipos cuando sea necesario. |

## <a id="entities"></a>Minimizar la característica de acceso tooshare en entidades críticas

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Minimizar la característica de acceso tooshare en entidades críticas |

## <a id="good-practices"></a>Entrenamiento de los usuarios en los riesgos de hello asociados con la característica de recurso compartido de Dynamics CRM hello y buenas prácticas de seguridad

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Entrenamiento de los usuarios en los riesgos de hello asociados con la característica de recurso compartido de Dynamics CRM hello y buenas prácticas de seguridad |

## <a id="exception-mgmt"></a>Incluya una regla de estándares de desarrollo que prohíba mostrar detalles de configuración en la administración de excepciones

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Dynamics CRM | 
| **Fase de SDL**               | Implementación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | N/D  |
| **Pasos** | Incluya una regla de estándares de desarrollo que prohíba mostrar detalles de configuración en la administración de excepciones fuera del desarrollo. Pruebe esto como parte de las revisiones del código o de la inspección periódica.|

## <a id="sse-preview"></a>Use el cifrado del servicio Azure Storage (SSE) para datos en reposo (versión preliminar)

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | StorageType: blob |
| **Referencias**              | [Cifrado del servicio Azure Storage para datos en reposo (versión preliminar)](https://azure.microsoft.com/documentation/articles/storage-service-encryption/) |
| **Pasos** | <p>Cifrado de servicio de almacenamiento de Azure (SSE) para los datos en reposo le ayuda a proteger y proteger su toomeet de datos de la seguridad de la organización y los compromisos de cumplimiento de normas. Con esta característica, el almacenamiento de Azure cifra su toostorage toopersisting anteriores de datos automáticamente y descifra tooretrieval anterior. Hola cifrado, descifrado y administración de claves es toousers totalmente transparente. SSE se aplica solo tooblock blobs, blobs de página y blobs en anexos. Hello otros tipos de datos, incluidas las tablas, colas y archivos, no se cifrarán.</p><p>Flujo de trabajo de cifrado y descifrado:</p><ul><li>cliente de Hola habilita el cifrado en la cuenta de almacenamiento de Hola</li><li>Cuando el cliente de hello escribe nuevo almacenamiento de datos (PUT Blob, coloque el bloque, PUT Page, etc.) tooBlob; cada escritura se cifra con el cifrado de AES de 256 bits, uno de hello más fuertes cifrados en bloque disponibles</li><li>Al cliente de hello necesita datos de tooaccess (GET Blob, etc.), los datos se descifra automáticamente antes de devolver el usuario toohello</li><li>Si el cifrado está deshabilitado, nuevas escrituras ya no están cifradas y los datos cifrados permanecen cifrados hasta reescrito por usuario de Hola. Mientras está habilitado el cifrado, se cifrará el almacenamiento de información de escrituras tooBlob. estado de Hola de datos no cambia con usuario Hola alternar entre la habilitación o deshabilitación del cifrado para la cuenta de almacenamiento de Hola</li><li>Microsoft almacena, cifra y administra todas las claves de cifrado.</li></ul><p>Tenga en cuenta que en este momento, Microsoft administra las claves de hello usadas para el cifrado de Hola. Microsoft genera claves de hello originalmente y administrar un almacenamiento seguro de claves de hello, así como la rotación normal de Hola Hola tal como se define por la directiva interno de Microsoft. Hola futuras, los clientes obtendrán Hola capacidad toomanage sus propios > claves de cifrado y proporcione una ruta de acceso de migración de claves administrada por Microsoft claves administradas toocustomer.</p>| 

## <a id="client-storage"></a>Usar datos confidenciales de toostore de cifrado en el cliente en el almacenamiento de Azure

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Azure Storage | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Cifrado del lado de cliente y Azure Key Vault para Microsoft Azure Storage](https://azure.microsoft.com/documentation/articles/storage-client-side-encryption/), [Tutorial: Cifrado y descifrado de blobs en Microsoft Azure Storage con Azure Key Vault](https://azure.microsoft.com/documentation/articles/storage-encrypt-decrypt-blobs-key-vault/), [Storing Data Securely in Azure Blob Storage with Azure Encryption Extensions](https://blogs.msdn.microsoft.com/partnercatalystteam/2015/06/17/storing-data-securely-in-azure-blob-storage-with-azure-encryption-extensions/) (Almacenamiento seguro de datos en Azure Blob Storage con Azure Encryption Extensions) |
| **Pasos** | <p>Hola biblioteca de cliente de almacenamiento de Azure para el paquete Nuget de .NET admite el cifrado de datos dentro de las aplicaciones cliente antes de cargar tooAzure almacenamiento y descifrar los datos mientras se descargaba toohello cliente. biblioteca de Hello también admite la integración con el almacén de claves de Azure para administración de claves de cuenta de almacenamiento. Esta es una breve descripción de cómo funciona el cifrado del lado cliente:</p><ul><li>SDK del cliente de almacenamiento de Azure Hola genera una clave de cifrado de contenido (CEK), que es una clave simétrica de un solo uso</li><li>Los datos de usuario se cifran mediante esta CEK.</li><li>Hello CEK se incluye después (cifrada) con clave de cifrado de claves de Hola (de claves KEK). Hola KEK se identifica mediante un identificador de clave y puede ser un par de claves asimétricas o una clave simétrica y se puede administrar de forma local o almacenado en el almacén de claves de Azure. cliente de almacenamiento de Hello propio nunca tiene acceso toohello KEK. Solo se invoca algoritmo de encapsulado de clave de hello proporcionada por el almacén de claves. Los clientes pueden elegir toouse proveedores personalizados para la clave ajuste/desencapsulación si desean</li><li>Hola datos cifrados están, a continuación, cargar el servicio de almacenamiento de Azure toohello. Compruebe los vínculos de hello en la sección de referencias de Hola para obtener detalles de implementación de nivel inferior.</li></ul>|

## <a id="pii-phones"></a>Cifrar confidencial o datos PII escritos toophones de almacenamiento local

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvil | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, Xamarin  |
| **Atributos**              | N/D  |
| **Referencias**              | [Administrar la configuración y las características de los dispositivos con directivas de Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/manage-settings-and-features-on-your-devices-with-microsoft-intune-policies#create-a-configuration-policy), [Keychain Valet](https://components.xamarin.com/view/square.valet) |
| **Pasos** | <p>Si la aplicación hello escribe información confidencial, como PII del usuario (correo electrónico, número de teléfono, nombre, apellido, preferencias etcetera.) -sistema del mobile de archivos, a continuación, se debe cifrar antes de escribir toohello sistema de archivos local. Si la aplicación hello es una aplicación empresarial, a continuación, explore posibilidad de Hola de publicación de aplicación mediante Windows Intune.</p>|

### <a name="example"></a>Ejemplo
Intune puede configurarse con los siguientes datos confidenciales de seguridad directivas toosafeguard: 
```C#
Require encryption on mobile device    
Require encryption on storage cards
Allow screen capture
```

### <a name="example"></a>Ejemplo
Si la aplicación hello no es una aplicación empresarial, a continuación, en plataformas de uso proporcionada el almacén de claves, pueden realizarse las claves de cifrado de toostore llaves, con qué operación criptográfica en sistema de archivos de Hola. Código siguiente fragmento de código muestra cómo tooaccess la clave de cadena de claves con xamarin: 
```C#
        protected static string EncryptionKey
        {
            get
            {
                if (String.IsNullOrEmpty(_Key))
                {
                    var query = new SecRecord(SecKind.GenericPassword);
                    query.Service = NSBundle.MainBundle.BundleIdentifier;
                    query.Account = "UniqueID";

                    NSData uniqueId = SecKeyChain.QueryAsData(query);
                    if (uniqueId == null)
                    {
                        query.ValueData = NSData.FromString(System.Guid.NewGuid().ToString());
                        var err = SecKeyChain.Add(query);
                        _Key = query.ValueData.ToString();
                    }
                    else
                    {
                        _Key = uniqueId.ToString();
                    }
                }

                return _Key;
            }
        }
```

## <a id="binaries-end"></a>Ofuscar archivos binarios generados antes de distribuir los usuarios tooend

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | Cliente móvil | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico |
| **Atributos**              | N/D  |
| **Referencias**              | [Crypto Obfuscator For .Net](http://www.ssware.com/cryptoobfuscator/obfuscator-net.htm) |
| **Pasos** | Archivos binarios generados (ensamblados dentro de apk) deben ser confuso toostop de ensamblados de ingeniería inversa. Herramientas como `CryptoObfuscator` pueden utilizarse para este propósito. |

## <a id="cert"></a>Conjunto clientCredentialType tooCertificate o Windows

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | .NET Framework 3 |
| **Atributos**              | N/D  |
| **Referencias**              | [Fortify](https://vulncat.fortify.com/en/vulncat/index.html) |
| **Pasos** | Usa un UsernameToken con una contraseña de texto simple a través de un canal no cifrado expone hello tooattackers de contraseña que puede examinar mensajes de SOAP de saludo. Los proveedores de servicio que utilizan Hola UsernameToken puede aceptar las contraseñas se envían en texto sin formato. Envío de contraseñas de texto simple a través de un canal no cifrado puede exponer hello tooattackers de credencial que puede rastrear el mensaje de bienvenida de SOAP. | 

### <a name="example"></a>Ejemplo
Hello siguiente configuración del proveedor de servicio WCF usa Hola UsernameToken: 
```
<security mode="Message"> 
<message clientCredentialType="UserName" />
``` 
Establecer clientCredentialType tooCertificate o Windows. 

## <a id="security"></a>El modo de seguridad de WCF no está habilitado

| Título                   | Detalles      |
| ----------------------- | ------------ |
| **Componente**               | WCF | 
| **Fase de SDL**               | Compilación |  
| **Tecnologías aplicables** | Genérico, .NET Framework 3 |
| **Atributos**              | Modo de seguridad: Transport, modo de seguridad: Message |
| **Referencias**              | [MSDN](https://msdn.microsoft.com/library/ff648500.aspx), [Fortify Kingdom](https://vulncat.fortify.com/en/vulncat/index.html), [Fundamentals of WCF Security CoDe Magazine](http://www.codemag.com/article/0611051) (Fundamentos de la seguridad de WCF en CoDe Magazine) |
| **Pasos** | No se ha definido la seguridad de transporte ni de mensajes. Aplicaciones que transmiten mensajes sin transporte o mensaje no puede garantizar la seguridad Hola integridad y confidencialidad de los mensajes de saludo. Cuando un enlace de seguridad WCF se establece tooNone, se deshabilita la seguridad de mensajes y transporte. |

### <a name="example"></a>Ejemplo
Hello siguiente conjuntos de configuración tooNone de modo de seguridad de Hola. 
```
<system.serviceModel> 
  <bindings> 
    <wsHttpBinding> 
      <binding name=""MyBinding""> 
        <security mode=""None""/> 
      </binding> 
  </bindings> 
</system.serviceModel> 
```

### <a name="example"></a>Ejemplo
Modo de seguridad En todos los enlaces de servicio, existen cinco modos de seguridad posibles: 
* Ninguno. Desactiva la seguridad. 
* Transport. Usa la seguridad de transporte para la autenticación mutua y la protección de mensajes. 
* Message. Usa la seguridad de mensajes para la autenticación mutua y la protección de mensajes. 
* Both. Le permite a toosupply configuración de transporte y seguridad de nivel de mensaje (sólo MSMQ es compatible con esto). 
* TransportWithMessageCredential. Las credenciales se pasan con el mensaje de Hola y protección de mensajes y capa de transporte de hello proporciona autenticación del servidor. 
* TransportCredentialOnly. Se pasan las credenciales del cliente con capa de transporte de Hola y no se aplica protección de mensaje. Usar mensajes y transporte integridad de hello tooprotect de seguridad y confidencialidad de los mensajes. configuración Hola siguiente indica la seguridad de transporte de hello servicio toouse con credenciales de mensaje.
```
<system.serviceModel>
  <bindings>
    <wsHttpBinding>
    <binding name=""MyBinding""> 
    <security mode=""TransportWithMessageCredential""/> 
    <message clientCredentialType=""Windows""/> 
    </binding> 
  </bindings> 
</system.serviceModel> 
```
