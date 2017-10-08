---
title: aplicaciones de aaaHow se agregan tooAzure Active Directory.
description: "Este artículo describe cómo las aplicaciones se agregan tooan instancia de Azure Active Directory."
services: active-directory
documentationcenter: 
author: shoatman
manager: kbrint
editor: 
ms.assetid: 3321d130-f2a8-4e38-b35e-0959693f3576
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2016
ms.author: shoatman
ms.custom: aaddev
ms.openlocfilehash: 3ca710c58a403b52e8b728202ad9010f4873bcea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-and-why-applications-are-added-tooazure-ad"></a>Cómo y por qué aplicaciones se agregan tooAzure AD
Uno de hello inicialmente analizarlo cosas al ver una lista de aplicaciones en la instancia de Azure Active Directory es entender las aplicaciones de hello proceden y por qué son.  Este artículo proporcionará una introducción de alto nivel de cómo las aplicaciones se representan en el directorio de Hola y proporcionan contexto que le ayudarán a entender cómo una aplicación había incluida toobe en el directorio.

## <a name="what-services-does-azure-ad-provide-tooapplications"></a>¿Qué servicios Azure AD proporciona tooapplications?
Las aplicaciones se agregan tooAzure AD tooleverage uno o varios de los servicios de Hola que proporciona.  Los servicios incluyen:

* Autenticación y autorización de aplicaciones
* Autenticación y autorización de usuarios
* Inicio de sesión único (SSO) mediante federación o contraseña
* Aprovisionamiento y sincronización de usuarios
* Control de acceso basado en roles; Use Hola directory toodefine roles tooperform los roles de aplicación en función de las comprobaciones de autorización en una aplicación.
* Servicios de autorización de oAuth (usados Office 365 y otras aplicaciones Microsoft tooauthorize acceso tooAPIs/recursos).
* Publicación de aplicaciones & proxy; Publicar una aplicación desde una red privada toohello internet

## <a name="how-are-applications-represented-in-hello-directory"></a>¿Cómo se representan las aplicaciones en el directorio de hello?
Las aplicaciones se representan en hello Azure AD mediante 2 objetos: un objeto de aplicación y un objeto de entidad de servicio.  Hay un objeto de aplicación, registrado en un "hogar" o "propietario" o "publicar" directorio y uno o varios objetos de entidad que representa la aplicación hello en todos los directorios en el que actúa de servicio.  

Hola aplicación tooAzure AD (servicio de varios inquilinos de Hola) se describen Hello objeto application y puede incluir ninguno de los siguientes hello: (*Nota*: esto no es una lista exhaustiva.)

* Nombre, logotipo y publicador
* Secretos (las claves simétricas o asimétricas usan tooauthenticate Hola aplicación)
* Dependencias de API (oAuth)
* API/recursos/ámbitos publicados (oAuth)
* Roles de aplicación (RBAC)
* Configuración y metadatos SSO (SSO)
* Configuración y metadatos de aprovisionamiento de usuarios
* Configuración y metadatos proxy

entidad de servicio de Hello es un registro de aplicación de hello en cada directorio, donde la aplicación hello actúa incluido su directorio particular.  entidad de servicio de Hello:

* Hacer referencia tooan el objeto de aplicación a través de la propiedad de Id. de aplicación Hola
* Registra las asignaciones de rol de aplicación de grupo y de usuario local
* Registros de usuario y administrador permisos concedidos toohello aplicación local
  * Por ejemplo: permiso para hello aplicación tooaccess un correo electrónico de usuarios concretos
* Registra directivas locales, incluida la directiva de acceso condicional
* Registra la configuración local alternativa para una aplicación
  * Reclama las reglas de transformación
  * Asignaciones de atributos (aprovisionamiento de usuarios)
  * Roles de aplicación específica de los inquilinos (si la aplicación hello es compatible con roles personalizados)
  * Nombre/logotipo

### <a name="a-diagram-of-application-objects-and-service-principals-across-directories"></a>Un diagrama de objetos de aplicación y entidades de seguridad de servicio en directorios
![Un diagrama muestra cómo los objetos de aplicación y entidad de seguridad de servicio existente con las instancias de Azure AD.][apps_service_principals_directory]

Como puede ver en el diagrama de hello anterior.  Microsoft mantiene dos directorios internamente (en la parte izquierda hello) usa toopublish aplicaciones.

* Uno para Microsoft Apps (directorio de servicios de Microsoft)
* Uno para aplicaciones preintegradas de terceros (directorio de Galería de aplicaciones)

Publicadores/proveedores de aplicaciones que integran con Azure AD son toohave requiere un directorio de publicación.  (Algunos directorios SAAS).

Las aplicaciones que agrega usted mismo incluyen:

* Aplicaciones que ha desarrollado (integradas con AAD)
* Aplicaciones conectadas para el inicio de sesión único
* Hola a aplicaciones publicadas mediante el proxy de aplicación de Azure AD.

### <a name="a-couple-of-notes-and-exceptions"></a>Un par de notas y excepciones
* No todas las entidades de servicio punto objetos tooapplication atrás.  ¿Verdad? Cuando Azure AD se generó originalmente Hola ofrecen tooapplications mucho más limitada y la entidad de servicio de hello era suficiente para establecer una identidad de aplicación.  entidad de servicio Hola original era más de cerca en forma toohello cuenta de servicio de Windows Server Active Directory.  Para ello, es posible toocreate entidades de servicio mediante Hola PowerShell de Azure AD sin crear primero un objeto de aplicación.  Hola API Graph requiere un objeto de aplicación antes de crear un servicio principal.
* Actualmente no toda información de Hola se ha descrito anteriormente se expone mediante programación.  siguiente Hola solo está disponibles en hello interfaz de usuario:
  * Reclama las reglas de transformación
  * Asignaciones de atributos (aprovisionamiento de usuarios)
* Para obtener más información detallada sobre la entidad de servicio de Hola y objetos de la aplicación, consulte la documentación de referencia de API de REST de Azure AD Graph toohello.  *Sugerencia*: Hola documentación de la API de Azure AD Graph es referencia de esquema de lo más cercano de hello tooa para Azure AD que está disponible actualmente.  
  * [Aplicación](https://msdn.microsoft.com/library/azure/dn151677.aspx)
  * [Entidad de seguridad de servicio](https://msdn.microsoft.com/library/azure/dn194452.aspx)

## <a name="how-are-apps-added-toomy-azure-ad-instance"></a>¿Cómo se agregan aplicaciones de la instancia de Azure AD toomy?
Hay muchas maneras de que una aplicación puede agregarse tooAzure AD:

* Agregar una aplicación de hello [Galería de aplicaciones de Azure Active Directory](https://azure.microsoft.com/updates/azure-active-directory-over-1000-apps/)
* Registro/inicio de sesión en una aplicación de terceros integrada con Azure Active Directory (por ejemplo: [Smartsheet](https://app.smartsheet.com/b/home) o [DocuSign](https://www.docusign.net/member/MemberLogin.aspx)).
  * Durante el inicio de sesión o los usuarios son más frecuentes toogive permiso toohello aplicación tooaccess su perfil y otros permisos.  Hola primera persona toogive consentimiento causas de una entidad de servicio que representa Hola aplicación toobe toohello agregado directorio.
* Registro/inicio de sesión en servicios en línea de Microsoft, como [Office 365](http://products.office.com/)
  * Cuando se suscribe tooOffice 365 comenzar una prueba o más entidades de servicio se crean en directorio de Hola que representa el saludo diversos servicios que son utilizado toodeliver toda la funcionalidad de hello asociado con Office 365.
  * Algunos servicios de Office 365 como SharePoint crean a entidades de servicio en una base en curso tooallow una comunicación segura entre los componentes, incluidos los flujos de trabajo.
* Agregar una aplicación que está desarrollando en hello, consulte el Portal de administración de Azure: https://msdn.microsoft.com/library/azure/dn132599.aspx
* Para agregar una aplicación que se va a desarrollar con Visual Studio, consulte:
  * [Métodos de autenticación de ASP.Net](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauthoptions)
  * [Servicios conectados](http://blogs.msdn.com/b/visualstudio/archive/2014/11/19/connecting-to-cloud-services.aspx)
* Agregar un saludo de aplicación toouse toouse [el Proxy de aplicación de Azure AD](https://msdn.microsoft.com/library/azure/dn768219.aspx)
* Conexión de una aplicación para inicio de sesión único utilizando SAML o SSO de contraseña
* Muchas más, incluidas varias experiencias de desarrollador en Azure y experiencias del explorador de API en centros de desarrollador.

## <a name="who-has-permission-tooadd-applications-toomy-azure-ad-instance"></a>¿Quién tiene instancia de Azure AD de permiso tooadd aplicaciones toomy?
Solo los administradores globales pueden:

* Agregar las aplicaciones de la Galería de aplicaciones de hello Azure AD (aplicaciones de terceros 3rd previamente integradas)
* Publicar una aplicación mediante Hola Proxy de aplicación de Azure AD

Todos los usuarios del directorio tienen las aplicaciones de tooadd de derechos que están desarrollando y discreción sobre qué aplicaciones recurso compartido o se produce acceso tootheir datos de la organización.  *Recordar el usuario de inicio de sesión arriba/aplicación tooan y conceda permisos podrán resultar en un servicio principal que se está creando.*

Este podría inicialmente sonido relativas a, pero Hola mantener después de la cuenta:

* Aplicaciones han sido capaz de tooleverage Windows Server Active Directory para la autenticación de usuario desde hace muchos años sin necesidad de hello aplicación toobe registrado/se registran en el directorio de Hola.  Ahora organización Hola habrá mejorado visibilidad tooexactly cuántas aplicaciones usan directory hello y qué for.
* No es necesario para el proceso de registro/publicación de la aplicación controlada por el administrador.  Con los servicios de federación de Active Directory es probable que un administrador tenía tooadd una aplicación como un usuario de confianza en nombre de los desarrolladores.  Ahora los desarrolladores pueden hacer uso del autoservicio.
* Usuarios que inician y seguridad tooapps con sus cuentas de organización para fines empresariales es bueno.  Si posteriormente abandonan la organización de Hola que perderá la cuenta de acceso de tootheir en la aplicación hello que ocupaban.
* Disponer de un registro sobre qué datos se compartieron con qué aplicación es algo positivo.  Los datos son más transportables que nunca y tener un registro claro de quién compartió que datos con qué aplicaciones resulta útil.
* Aplicaciones que usan Azure AD para oAuth decidir exactamente los permisos que los usuarios son toogrant capaz de tooapplications y los permisos que requieren un tooagree de administración a.  Debería ir sin tener que decir que sólo los administradores pueden dar su consentimiento toolarger ámbitos y los permisos más importantes.
* Los usuarios agregar y permitir tooaccess aplicaciones que sus datos son los sucesos auditados para que pueda ver informes de auditoría de hello en hello Azure Management portal toodetermine cómo una aplicación se haya agregado toohello directory.

**Nota:** *Microsoft ha estado funcionando usando la configuración predeterminada de Hola durante varios meses ahora.*

Con todo esto dice que es posible tooprevent usuarios del directorio de adición de aplicaciones y de llevar a cabo discreción sobre qué información que se comparten con aplicaciones mediante la modificación de la configuración del directorio en el portal de administración de Azure de Hola.  Hello configuración siguiente son accesibles en el portal de administración de Azure de hello en la ficha "Configuración" del su directorio.

![Una captura de pantalla de hello interfaz de usuario para configurar las opciones de la aplicación integrada][app_settings]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
Más información acerca de cómo tooadd tooAzure aplicaciones AD y cómo tooconfigure services para las aplicaciones.

* Los desarrolladores: [aprender cómo toointegrate una aplicación con AAD](https://msdn.microsoft.com/library/azure/dn151122.aspx)
* Desarrolladores: [Revisión de ejemplo de código para aplicaciones integradas con Azure Active Directory en GitHub](https://github.com/AzureADSamples)
* Los desarrolladores y profesionales de TI: [revisar la documentación de la API de REST de Hola para hello API Graph de Azure Active Directory](https://msdn.microsoft.com/library/azure/hh974478.aspx)
* Los profesionales de TI: [Obtenga información acerca de cómo toouse Azure Active Directory integrado previamente las aplicaciones de hello Galería de aplicaciones](https://msdn.microsoft.com/library/azure/dn308590.aspx)
* Profesionales de TI: [Búsqueda de tutoriales para la configuración de aplicaciones específicas integradas previamente](https://msdn.microsoft.com/library/azure/dn893637.aspx)
* Los profesionales de TI: [Obtenga información acerca de cómo toopublish una aplicación con Hola Proxy de aplicación de Azure Active Directory](https://msdn.microsoft.com/library/azure/dn768219.aspx)

## <a name="see-also"></a>Otras referencias
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](../active-directory-apps-index.md)

<!--Image references-->
[apps_service_principals_directory]:../media/active-directory-how-applications-are-added/HowAppsAreAddedToAAD.jpg
[app_settings]:../media/active-directory-how-applications-are-added/IntegratedAppSettings.jpg
