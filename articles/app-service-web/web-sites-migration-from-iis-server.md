---
title: "aaaMigrate una tooAzure de aplicación de web servicio de aplicaciones de empresa"
description: "Muestra cómo toouse el Asistente para la migración de aplicaciones Web tooquickly migrar tooAzure de sitios Web IIS existente aplicación del servicio de aplicaciones Web"
services: app-service
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: 
ms.assetid: 2e846fc0-37cc-42e6-ac57-ff442ef16e85
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 7d66c5b799f0eefe85cbd9ba596ee0a05167f295
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-enterprise-web-app-tooazure-app-service"></a>Migrar una aplicación de web enterprise tooAzure servicio de aplicaciones
Puede migrar fácilmente sus sitios Web existentes que se ejecutan en Internet Information Service (IIS) 6 o posterior demasiado[aplicación del servicio de aplicaciones Web](http://go.microsoft.com/fwlink/?LinkId=529714). 

> [!IMPORTANT]
> El 14 de julio de 2015 Windows Server 2003 llegó al final de su soporte técnico. Si se hospeda actualmente sus sitios Web en un servidor IIS que sea Windows Server 2003, las aplicaciones Web es una manera de bajo riesgo, bajo costo y poco fricción tookeep los sitios Web en línea y el Asistente para la migración de aplicaciones Web pueden ayudar a automatizar el proceso de migración de Hola para usted. 
> 
> 

[El Asistente de migración de aplicaciones de Web](https://www.movemetothecloud.net/) puede analizar la instalación del servidor IIS, identificar qué sitios pueden ser migrado tooApp servicio, resalte cualquier elemento que no se puede migrar o no es compatibles en la plataforma de hello y, a continuación, migrar los sitios Web y tooAzure de bases de datos asociadas.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="elements-verified-during-compatibility-analysis"></a>Elementos comprobados durante el análisis de compatibilidad
Hola Migration Assistant crea un tooidentify de informe de preparación hace que cualquier posible problema o los problemas de bloqueo que pueden impedir que una migración correcta de tooAzure IIS local las aplicaciones de servicio Web de aplicación. Algunos de hello elementos clave toobe en cuenta son:

* Enlaces de puerto: Aplicaciones web solo admite el puerto 80 para el tráfico HTTP y el puerto 443 para el tráfico HTTPS. Se pasará por alto las configuraciones de puerto diferente y será tráfico enrutado too80 o 443. 
* Autenticación: Aplicaciones web admite la autenticación anónima de forma predeterminada y la autenticación de formularios cuando una aplicación lo especifique. Puede utilizarse la autenticación de Windows solo mediante la integración con Azure Active Directory y ADFS. Todos las demás formas de autenticación, por ejemplo la autenticación básica, no se admiten actualmente. 
* Caché global de ensamblados (GAC): Hola GAC no se admite en aplicaciones Web. Si la aplicación hace referencia a ensamblados que suele implementar toohello GAC, necesitará carpeta bin de la aplicación de la toohello toodeploy en aplicaciones Web. 
* Modo de compatibilidad con IIS5: no admitido en Aplicaciones web. 
* Grupos de aplicaciones: en las aplicaciones Web, cada sitio y sus aplicaciones secundarios se ejecutan en hello mismo grupo de aplicaciones. Si el sitio tiene varios secundarios las aplicaciones que utilizan varios grupos de aplicaciones, consolidarlas tooa único grupo de aplicaciones con la misma configuración o migrar cada aplicación web independiente de tooa de aplicación.
* Componentes COM, aplicaciones Web no permitir el registro de hello de componentes COM en la plataforma de Hola. Si las aplicaciones o sitios Web que use de todos los componentes COM, debe volver a escribir en código administrado e implementarlas con el sitio Web de Hola o aplicación.
* Extensiones ISAPI: aplicaciones Web puede admitir el uso de Hola de extensiones ISAPI. Necesita toodo Hola siguiente:
  
  * implementar archivos DLL de Hola a su aplicación web 
  * registrar archivos DLL de hello mediante [Web.config](http://www.iis.net/configreference/system.webserver/isapifilters)
  * Coloque un archivo applicationHost.xdt en la raíz del sitio Hola con contenido de Hola que se describen en "Permitir que toobe de extensiones ISAPI arbitrart cargado" [sección de este artículo](https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples) 
    
  
    
    Para obtener más ejemplos de cómo toouse transformación de un documento XML con el sitio Web, consulte [transformar su sitio Web de Microsoft Azure](http://blogs.msdn.com/b/waws/archive/2014/06/17/transform-your-microsoft-azure-web-site.aspx).
* Otros componentes, como SharePoint, extensiones de servidor de FrontPage (FPSE), FTP o certificados SSL, no se migrarán.

## <a name="how-toouse-hello-web-apps-migration-assistant"></a>¿Cómo toouse Hola el Asistente para la migración de aplicaciones Web
En esta sección los pasos a través de un ejemplo tootoomigrate algunos sitios Web que utilizan una base de datos de SQL Server y ejecuta en una máquina de Windows Server 2003 R2 (IIS 6.0) local:

1. En hello IIS server o el equipo cliente vaya demasiado[https://www.movemetothecloud.net/](https://www.movemetothecloud.net/) 
   
   ![](./media/web-sites-migration-from-iis-server/migration-tool-homepage.png)
2. Instalar el Asistente para la migración de aplicaciones Web, haga clic en hello **dedicado IIS Server** botón. Más opciones serán opciones Hola futuro próximo. 
3. Haga clic en hello **Install Tool** botón tooinstall el Asistente para la migración de aplicaciones Web en su equipo.
   
   ![](./media/web-sites-migration-from-iis-server/install-page.png)
   
   > [!NOTE]
   > También puede hacer clic en **descargar para instalación sin conexión** toodownload un archivo ZIP de archivos de instalación en servidores no está conectado toohello internet. O bien, puede hacer clic en **cargar un informe de preparación para la migración existente**, que es un toowork opción avanzada con un migración preparación informe existente generado previamente (se explica más adelante).
   > 
   > 
4. Hola **instalar aplicación** pantalla, haga clic en **instalar** tooinstall en su equipo. También instalará las dependencias correspondientes como Web Deploy, DacFX e IIS, si es necesario. 
   
   ![](./media/web-sites-migration-from-iis-server/install-progress.png)
   
   Una vez instalado, el Asistente para migración de Aplicaciones web se inicia automáticamente.
5. Elija **migrar sitios y bases de datos de un servidor remoto tooAzure**. Escriba las credenciales administrativas de hello para el servidor remoto de Hola y haga clic en **continuar**. 
   
   ![](./media/web-sites-migration-from-iis-server/migrate-from-remote.png)
   
   Por supuesto, puede elegir toomigrate desde el servidor local de Hola. opción remoto Hello es útil cuando desea toomigrate de sitios Web desde un servidor de IIS de producción.
   
   En este momento inspeccionará la herramienta de migración de Hola Hola configuración de su servidor IIS, como sitios, aplicaciones, grupos de aplicaciones, dependencias tooidentify candidato sitios Web y para la migración. 
6. Hola de captura de pantalla siguiente muestra tres de sitios Web: **sitio Web predeterminado**, **TimeTracker**, y **CommerceNet4**. Todos ellos tengan una base de datos asociado que deseamos toomigrate. Seleccione todos los sitios de hello sería como tooassess y, a continuación, haga clic en **siguiente**.
   
   ![](./media/web-sites-migration-from-iis-server/select-migration-candidates.png)
7. Haga clic en **cargar** informe de disponibilidad de tooupload Hola. Si hace clic en **guardar el archivo localmente**, puede ejecutar la herramienta de migración de Hola de nuevo más tarde y carga Hola guardado informe disponibilidad tal y como se ha indicado anteriormente.
   
   ![](./media/web-sites-migration-from-iis-server/upload-readiness-report.png)
   
   Una vez que cargue el informe de disponibilidad de hello, Azure realiza el análisis de preparación y muestra Hola resultados. Leer los detalles de la evaluación de Hola para cada sitio Web y asegúrese de que se comprendan o que se han resuelto todos los problemas antes de continuar. 
   
   ![](./media/web-sites-migration-from-iis-server/readiness-assessment.png)
8. Haga clic en **Iniciar migración** migración de hello toostart. Ahora será redirigido tooAzure toolog en su cuenta. Es importante que inicie sesión con una cuenta que tenga una suscripción activa de Azure. Si no tiene una cuenta de Azure, puede registrarse [aquí](https://azure.microsoft.com/pricing/free-trial/?WT.srch=1&WT.mc_ID=SEM_) para obtener una evaluación gratuita. 
9. Seleccione la cuenta de inquilino de hello, suscripción de Azure y región toouse para sus aplicaciones web de Azure migrados y las bases de datos y, a continuación, haga clic en **Iniciar migración**. Puede seleccionar toomigrate de sitios Web de hello más tarde.
   
   ![](./media/web-sites-migration-from-iis-server/choose-tenant-account.png)
10. En la pantalla de bienvenida siguiente puede realizar cambios toohello configuración de migración de manera predeterminada, como:
    
    * utilizar una Base de datos SQL de Azure existente o crear una nueva Base de datos SQL de Azure y configurar sus credenciales
    * Seleccione hello toomigrate de sitios Web
    * definir nombres para aplicaciones web de Azure de Hola y sus bases de datos SQL vinculados
    * personalizar la configuración de nivel de sitio y la configuración global de Hola
    
    Hola de captura de pantalla siguiente muestra todos los sitios Web de hello seleccionados para la migración con la configuración predeterminada de Hola.
    
    ![](./media/web-sites-migration-from-iis-server/migration-settings.png)
    
    > [!NOTE]
    > Hola **habilitar Azure Active Directory** checkbox en una configuración personalizada integra la aplicación web de Azure de hello con [Azure Active Directory](../active-directory/active-directory-whatis.md) (hello **directorio predeterminado**). Para más información sobre la sincronización de Azure Active Directory con su Active Directory local, consulte [Integración de directorios](http://msdn.microsoft.com/library/jj573653).
    > 
    > 
11. Cuando haya realizado todos los cambios de hello deseado, haga clic en **crear** proceso de migración de toostart Hola. herramienta de migración de Hola creará aplicación web de la base de datos SQL Azure y Azure de hello y, a continuación, publicar bases de datos y el contenido del sitio Web de Hola. progreso de la migración de Hello claramente se muestra en la herramienta de migración de Hola y verá una pantalla de resumen al final de hello, qué sitios de hello detalles migran, si lo lograron, aplicaciones web de Azure recién creada de vínculos toohello. 
    
    Si cualquier error se produce durante la migración, Hola eliminará de la herramienta de migración claramente indicar cambios de Hola de error y reversión de Hola. También será capaz de toosend informe de errores de hello directamente toohello ingeniería de equipo, haga clic en hello **Enviar informe de errores** botón con pila de llamadas de error capturados de Hola y generar el cuerpo del mensaje. 
    
    ![](./media/web-sites-migration-from-iis-server/migration-error-report.png)
    
    Si migra se realiza correctamente sin errores, también puede hacer clic en hello **enviar comentarios** botón tooprovide cualquier comentario directamente. 
12. Haga clic en aplicaciones web de Azure de hello vínculos toohello y compruebe que se ha realizado correctamente la migración de Hola.
13. Ahora puede administrar Hola migra las aplicaciones web en el servicio de aplicación de Azure. toodo, inicie sesión en hello [Portal de Azure](https://portal.azure.com).
14. Hola Portal de Azure, abra toosee de hoja de aplicaciones Web de hello sus sitios Web migrados (se muestra como aplicaciones web), a continuación, haga clic en uno de ellos toostart administración de aplicación web de hello, como cuando se configura la publicación continua, crear copias de seguridad, de escalado automático y supervisar el uso de o rendimiento.
    
    ![](./media/web-sites-migration-from-iis-server/TimeTrackerMigrated.png)

> [!NOTE]
> Si desea tooget iniciado con el servicio de aplicación de Azure antes de registrarse para una cuenta de Azure, vaya demasiado[pruebe el servicio de aplicaciones](https://azure.microsoft.com/try/app-service/), donde puede crear inmediatamente una aplicación web de inicio de corta duración en el servicio de aplicaciones. No es necesario proporcionar ninguna tarjeta de crédito ni asumir ningún compromiso.
> 
> 

## <a name="whats-changed"></a>Lo que ha cambiado
* Para una toohello guía consulte cambio con respecto a sitios Web tooApp servicio: [servicio de aplicaciones de Azure y su impacto en los servicios de Azure existente](http://go.microsoft.com/fwlink/?LinkId=529714)

