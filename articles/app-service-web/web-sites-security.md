---
title: "aaaSecure una aplicación de servicio de aplicaciones de Azure"
description: "Obtenga información acerca de cómo toosecure una aplicación web, el back-end de aplicación móvil o la aplicación de API de servicio de aplicaciones de Azure."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 5ce560b4-42d7-4b20-935c-0445fd539e39
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: fceef7963b29516f33602dcd50591d14309bf188
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="secure-an-app-in-azure-app-service"></a>Protección de una aplicación en el Servicio de aplicaciones de Azure
Este artículo sirve de introducción a la protección de su aplicación web, back-end de aplicación móvil o aplicación de API en el Servicio de aplicaciones de Azure. 

La seguridad en el Servicio de aplicaciones de Azure tiene dos niveles: 

* **Seguridad de infraestructura y plataforma** -confianza hello Azure toohave servicios necesita cosas de tooactually ejecutar con seguridad en nube de Hola.
* **Seguridad de la aplicación** -necesita propia aplicación de hello toodesign de forma segura. Esto incluye cómo integrar con Azure Active Directory, cómo administrar certificados y cómo asegurarse de que puede comunicarse con seguridad toodifferent servicios. 

#### <a name="infrastructure-and-platform-security"></a>Seguridad de la infraestructura y la plataforma
Dado que el servicio de aplicación mantiene máquinas virtuales de Azure de hello, almacenamiento, las conexiones de red, marcos de trabajo web, administración y las características de integración y mucho más, está protegido y protege activamente y lleva a cabo cumplimiento exhaustiva y seguro de que las comprobaciones en un toomake bien continuamente que:

* Las aplicaciones de servicio de aplicaciones están aisladas de ambos Hola Internet y de Hola recursos de Azure de otros clientes.
* La comunicación de secretos (por ejemplo, cadenas de conexión) entre su aplicación del Servicio de aplicaciones y otros recursos de Azure (por ejemplo, Base de datos SQL) en un grupo de recursos permanezca dentro de Azure y no cruce ningún límite de la red. Los secretos siempre están cifrados.
* Toda la comunicación entre su aplicación del Servicio de aplicaciones y los recursos externos, como la administración de PowerShell, la interfaz de la línea de comandos, los SDK de Azure, las API de REST y las conexiones híbridas, se hayan cifrado correctamente.
* La administración ininterrumpida de amenazas proteja los recursos del Servicio de aplicaciones frente a malware, ataques por denegación de servicio distribuido (DDoS), ataques de tipo "Man in the middle" (MITM) y otras amenazas. 

Para más información sobre la seguridad de la infraestructura y la plataforma en Azure, consulte [Centro de confianza de Microsoft Azure](https://azure.microsoft.com/support/trust-center/security/).

#### <a name="application-security"></a>Seguridad de las aplicaciones
Aunque es responsable de proteger la infraestructura de Hola y la plataforma que se ejecuta la aplicación en Azure, es su responsabilidad toosecure su propia aplicación. En otras palabras, necesita toodevelop, implementar y administrar el contenido y el código de la aplicación de una manera segura. Sin esto, el código de aplicación o el contenido todavía puede estar toothreats vulnerables como:

* Inyección de código SQL
* Secuestro de sesión
* Ataque de scripts de sitios
* MITM en el nivel de aplicación
* DDoS en el nivel de aplicación

Una descripción completa de las consideraciones de seguridad para las aplicaciones basadas en web está más allá del ámbito de Hola de este documento. Como punto de partida para obtener más información sobre cómo proteger la aplicación, vea hello [Abrir proyecto de seguridad aplicación de Web (OWASP)](https://www.owasp.org/index.php/Main_Page), específicamente hello [10 principales del proyecto.](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project), qué listas Hola 10 superior actual web crítico aplicación brechas de seguridad, según lo determinado por los miembros OWASP.

## <a name="perform-penetration-testing-on-your-app"></a>Realización de pruebas de penetración en la aplicación
Uno de hello más fácil formas tooget inició con pruebas de vulnerabilidades en la aplicación de servicio de aplicaciones es hello toouse [integración con Tinfoil Security](https://azure.microsoft.com/blog/web-vulnerability-scanning-for-azure-app-service-powered-by-tinfoil-security/) una vulnerabilidad de un solo clic tooperform análisis en la aplicación. Puede ver los resultados de pruebas de hello en un informe fácil de entender y obtenga información acerca de cómo toofix cada vulnerabilidad con instrucciones paso a paso.

Si lo prefiere tooperform su propio penetración pruebas o desea toouse otro conjunto de escáner o proveedor, deberá seguir hello [proceso de aprobación de prueba de penetración Azure](https://security-forms.azure.com/penetration-testing/terms) y obtener la aprobación previa tooperform Hola deseado de penetración pruebas.

## <a name="https"></a> Protección de la comunicación con clientes
Si usas hello  **\*. azurewebsites.net** nombre de dominio creado para la aplicación de servicio de aplicaciones, inmediatamente puede usar HTTPS, tal y como se proporciona un certificado SSL para todos los  **\*. azurewebsites.net** nombres de dominio. Si el sitio utiliza un [nombre de dominio personalizado](app-service-web-tutorial-custom-domain.md), puede cargar un certificado SSL demasiado[Habilitar HTTPS](app-service-web-tutorial-custom-ssl.md) dominio personalizado de Hola.

Habilitar [HTTPS](https://en.wikipedia.org/wiki/HTTPS) puede ayudar a proteger frente a ataques MITM en la comunicación de hello entre la aplicación y sus usuarios.

## <a name="secure-data-tier"></a>Protección de la capa de datos
Servicio de aplicaciones de alta se integra con la base de datos SQL, por ejemplo, que todas las cadenas de conexión de Hola se cifran en el tablero de Hola y sólo se descifran en hello VM esa aplicación Hola se ejecuta en *y* sólo Hola cuando se ejecuta la aplicación. Además, la base de datos de SQL Azure incluye muchos toohelp de características de seguridad que proteja los datos de aplicación frente a amenazas de intrusos, incluidos [cifrado en reposo](https://msdn.microsoft.com/library/dn948096.aspx), [Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx), [ Enmascaramiento dinámico de datos](../sql-database/sql-database-dynamic-data-masking-get-started.md), y [detección de amenazas](../sql-database/sql-database-threat-detection.md). Si tiene datos confidenciales o requisitos de cumplimiento, consulte [proteger la base de datos de SQL](../sql-database/sql-database-security-overview.md) para obtener más información acerca de cómo toosecure los datos.

Si utiliza un proveedor de base de datos de terceros, como ClearDB, debe consultar con la documentación del proveedor de hello directamente en prácticas recomendadas de seguridad.  

## <a name="develop"></a> Desarrollo e implementación seguros
### <a name="publishing-profiles-and-publish-settings"></a>Perfiles de publicación y configuración de publicación
Al desarrollar aplicaciones, realizar tareas de administración y automatización de tareas mediante utilidades como **Visual Studio**, **Web Matrix**, **Azure PowerShell** o hello **Interfaz de línea de comandos de azure (Azure CLI)**, puede utilizar un *configuración de publicación* archivo o un *perfil de publicación*. Ambos tipos de archivo autentican con Azure y deben protegerse acceso tooprevent no autorizado.

* Un archivo de **configuración de publicación** contiene
  
  * El identificador de suscripción a Azure
  * Un certificado de administración que permite tooperform las tareas de administración para su suscripción *sin necesidad de tooprovide un nombre de cuenta o contraseña*.
* Un archivo de **perfil de publicación** contiene
  
  * Información para publicar aplicación de tooyour

Si utiliza una utilidad que usa un archivo de configuración de publicación o el archivo de perfil de publicación, importar archivo de Hola que contenga la configuración de publicación de Hola o generar perfiles en la utilidad de hello y, a continuación, **eliminar** archivo hello. Si debe mantener el archivo hello, tooshare con otros usuarios que trabajen en proyectos de hello, por ejemplo, almacenarla en una ubicación segura como una *cifrados* directorio con permisos restringidos.

Además, debe asegurarse de que se protegen las credenciales de hello importado. Por ejemplo, **Azure PowerShell** hello y **interfaz de línea de comandos de Azure (Azure CLI)** ambos almacenan información importada en su **directorio particular** ( *~*  en sistemas Linux u OS X y */usuarios/suNombreDeUsuario* en sistemas Windows.) Para mayor seguridad, es recomendable demasiado**cifrar** estas ubicaciones utilizan las herramientas de cifrado disponibles para su sistema operativo.

### <a name="configuration-settings-and-connection-strings"></a>Valores de configuración y cadenas de conexión
Es las cadenas de conexión de toostore práctica común, las credenciales de autenticación y otra información confidencial en archivos de configuración. Lamentablemente, estos archivos pueden resultar expuestos en su sitio web o podrían aparecer en búsquedas de un repositorio público, con lo que la información podría quedar al descubierto. Una búsqueda simple en [GitHub](https://github.com), por ejemplo, puede descubrir y archivos de configuración con secretos expuestos en repositorios públicos Hola.

Hola práctica recomendada es tookeep esta información fuera de los archivos de configuración de la aplicación. Servicio de aplicaciones le permite almacenar información de configuración como parte del entorno de tiempo de ejecución de hello como **configuración de la aplicación** y **las cadenas de conexión**. valores de Hello son tooyour expuesta de la aplicación en tiempo de ejecución a través de *variables de entorno* para la mayoría de lenguajes de programación. En el caso de las aplicaciones .NET, estos valores se insertan en la configuración de .NET en el tiempo de ejecución. Además de estas situaciones, estos valores de configuración permanecerán cifrados a menos que se puede ver o configurarlos mediante hello [Portal de Azure](https://portal.azure.com) o utilidades como PowerShell o hello CLI de Azure. 

Almacenar información de configuración de servicio de aplicaciones realiza toolock de administrador de la aplicación hello hacia abajo de la información confidencial para las aplicaciones de producción de hello. Los desarrolladores pueden usar un conjunto independiente de valores de configuración para el desarrollo de aplicaciones y configuración Hola puede se reemplazará automáticamente por la configuración de hello configurado en el servicio de aplicaciones. Los desarrolladores de hello ni siquiera necesitan secretos de hello tooknow configurados para la aplicación de producción de hello. Para más información sobre cómo establecer la configuración de la aplicación y las cadenas de conexión en el Servicio de aplicaciones, consulte [Configuración de aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-configure.md).

### <a name="ftps"></a>FTPS
Servicio de aplicaciones de Azure proporciona el sistema de archivos de toohello de acceso FTP seguro para su aplicación a través de **FTPS**. Esto le permite toosecurely acceso Hola código de la aplicación en aplicación web de hello, así como los diagnósticos de registros. Se recomienda que use siempre FTPS en lugar de FTP. 

Hola FTPS vínculo para la aplicación se encuentra con hello pasos:

1. Abra hello [Portal de Azure](https://portal.azure.com).
2. Seleccione **Examinar todo**.
3. De hello **examinar** hoja, seleccione **servicios de aplicaciones**.
4. De hello **servicios de aplicaciones** hoja, la aplicación deseada de hello Select.
5. En la hoja de la aplicación hello, seleccione **toda la configuración de**.
6. De hello **configuración** hoja, seleccione **propiedades**.
7. Hello FTP y FTPS se proporcionan vínculos en hello **configuración** hoja. 

Para obtener más información acerca de FTPS, consulte [File Transfer Protocol](http://en.wikipedia.org/wiki/File_Transfer_Protocol).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre la seguridad de Hola de hello plataforma Windows Azure, información sobre cómo informar de un **incidente de seguridad o abuso**, o tooinform Microsoft que se va a realizar **las pruebas de penetración** de su de sitio, consulte la sección de seguridad de Hola de hello [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/security/).

Para más información sobre los archivos **web.config** o **applicationhost.config** en aplicaciones de App Service, consulte [ Opciones de configuración desbloqueadas en Azure App Service Web Apps](https://azure.microsoft.com/blog/2014/01/28/more-to-explore-configuration-options-unlocked-in-windows-azure-web-sites/).

Para más datos sobre la información de registro para aplicaciones del Servicio de aplicaciones, que puede resultar útil para detectar de ataques, consulte [Habilitación del registro de diagnóstico para aplicaciones web en el Servicio de aplicaciones de Azure](web-sites-enable-diagnostic-log.md).

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

