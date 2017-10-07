---
title: "aaaMigrate de servicios móviles tooan aplicación móvil de servicio de aplicación"
description: "Obtenga información acerca de cómo tooeasily migrar su tooan de aplicación de servicios móviles aplicación móvil de servicio de aplicación"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Migrar su tooAzure de servicios móviles de Azure existente servicio de aplicaciones
Con hello [disponibilidad general del servicio de aplicaciones de Azure], servicios móviles de Azure los sitios pueden ser fácilmente migrar in situ tootake aprovechar todas las características del programa Hola a servicio de aplicaciones de Azure.  Este documento explica qué tooexpect al migrar el sitio de servicios móviles de Azure tooAzure servicio de aplicaciones.

## <a name="what-does-migration-do"></a>¿Qué hace migración tooyour sitio
Migración del servicio móvil Azure activa su servicio móvil en un [servicio de aplicaciones de Azure] aplicación sin alterar el código de hello.  Las instancias de Notification Hubs, la conexión de datos SQL, la configuración de la autenticación, los trabajos programados y el nombre de dominio permanecen sin cambios.  Los clientes móviles mediante el servicio móvil de Azure continúan toooperate con normalidad.  Migración reinicia el servicio una vez se haya transferido tooAzure servicio de aplicaciones.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Por qué debe migrar el sitio
Microsoft recomienda que migre su servicio móvil de Azure tootake aprovechar Hola características del servicio de aplicación de Azure, incluidos:

* Nuevas características de host, como [WebJobs] y [nombres de dominio personalizados].
* Tooyour de conectividad con los recursos locales [VNet] además demasiado[conexiones híbridas].
* Supervisión y solución de problemas con New Relic o [Application Insights].
* Herramientas integradas de DevOps, entre las que se incluyen [ranuras de ensayo], reversión y pruebas en producción.
* [Escalado automático], equilibrio de carga y [supervisión del rendimiento].

Para obtener más información sobre las ventajas de Hola de servicio de aplicaciones de Azure, vea hello [frente a servicios móviles. Servicio de aplicaciones].

## <a name="before-you-begin"></a>Antes de empezar
Antes de empezar cualquier trabajo importante en su sitio, debe hacer una copia de seguridad de los scripts y la base de datos SQL de Mobile Service.

## <a name="migrating-site"></a>Migración de los sitios
proceso de migración de Hello migra todos los sitios en una única región de Azure.

toomigrate su sitio:

1. Inicie sesión en toohello [Portal clásico de Azure].
2. Seleccione un servicio móvil en la región de hello desea toomigrate.
3. Haga clic en hello **migrar tooApp servicio** botón.

   ![Hola botón migrar][0]
4. Lea el cuadro de diálogo de hello migrar tooApp servicio.
5. Escriba el nombre de Hola de su servicio móvil en cuadro Hola proporcionado.  Por ejemplo, si el nombre de dominio es contoso.azure-Mobile.NET, a continuación, escriba *contoso* en cuadro Hola proporcionado.
6. Haga clic en el botón de TIC Hola.

Supervisar estado de Hola de migración de hello en el monitor de actividad de Hola. El sitio se muestra como *migrar* Hola Portal clásico de Azure.

  ![Monitor de actividad de migración][1]

Cada migración puede tardar en cualquier lugar de 3 minutos too15 por servicio móvil que se está migrando.  El sitio permanece disponible durante la migración de Hola.
El sitio se reinicia al final de Hola Hola del proceso de migración.  Hola sitio no está disponible durante el proceso de reinicio de hello, que puede durar unos segundos.

## <a name="finalizing-migration"></a>Hola finalizando la migración
Planee tootest su sitio desde un cliente móvil al concluir Hola Hola del proceso de migración.  Asegúrese de que puede realizar todas las acciones comunes de cliente sin cambios toohello cliente móvil.  

### <a name="update-app-service-tier"></a>Selección de un plan de tarifa adecuado del Servicio de aplicaciones
Dispone de más flexibilidad en el precio después de migrar tooAzure servicio de aplicaciones.

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **Plan de servicio de aplicaciones** en el menú de configuración de Hola.
5. Haga clic en hello **tarifa** icono.
6. Haga clic en requisitos de hello mosaico tooyour adecuado, haga clic en **seleccione**.  Puede que necesite tooClick **todas las ver** toosee Hola disponible de los niveles de precios.

Como punto de partida, se recomienda Hola siguientes niveles:

| Plan de tarifa del servicio móvil | Plan de tarifa del Servicio de aplicaciones |
|:--- |:--- |
| Gratuito |F1 Gratis |
| Básica |Básico B1 |
| Standard |S1 Estándar |

Existe una considerable flexibilidad de elegir Hola derecha tarifa para la aplicación.  Consulte demasiado[precios del servicio de aplicación] para obtener detalles completos sobre los precios de Hola de su nuevo servicio de aplicación.

> [!TIP]
> nivel estándar de servicio de aplicación Hello contiene características de toomany de acceso que quizá desee toouse, incluidos los [ranuras de ensayo], copias de seguridad automáticas y la escala automática.  Visite nuevas capacidades de hello mientras estás no existe.
>
>

### <a name="review-migration-scheduler-jobs"></a>Revisar Hola migrar trabajos del programador
Los trabajos del Programador no estarán visibles hasta unos 30 minutos después de la migración.  Los trabajos programados continúan toorun en segundo plano de Hola.
tooview los trabajos programados cuando se encuentran visibles nuevo:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **examinar >**, escriba **programación** en hello *filtro* cuadro y haga clic en **colecciones programador**.

Existe un número limitado de trabajos de Programador gratuitos que están disponibles después de la migración.  Revise su uso y hello [planes de programador de Azure].

### <a name="configure-cors"></a>Configuración de CORS si es necesario
Uso compartido de recursos entre orígenes es un tooallow técnica un tooaccess del sitio Web una API Web en un dominio diferente.  Si usas servicios móviles de Azure con un sitio Web asociado, necesita tooconfigure CORS como parte de la migración de Hola.  Si se obtiene acceso a servicios móviles de Azure exclusivamente a partir de dispositivos móviles, CORS no es necesario toobe configurado excepto en casos poco frecuentes.

La configuración de CORS migrada está disponible como hello **MS_CrossDomainWhitelist** configuración de la aplicación.  toomigrate su toohello sitio instalaciones de CORS del servicio de aplicación:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **CORS** en el menú de hello API.
5. Especifique los orígenes permitidos en hello cuadro proporcionado para ello, al presionar ENTRAR después de cada uno de ellos.
6. Una vez que la lista de orígenes permitidos es correcta, haga clic en el botón Guardar de Hola.

> [!TIP]
> Una de las ventajas de hello del uso de un servicio de aplicaciones de Azure es que puede ejecutar su sitio web y el servicio móvil en hello mismo sitio.  Para obtener más información, vea hello [pasos](#next-steps) sección.
>
>

### <a name="download-publish-profile"></a>Descarga de un nuevo perfil de publicación
perfil de publicación de Hola de su sitio se cambia al migrar tooAzure servicio de aplicaciones.  Si piensa toopublish su sitio desde dentro de Visual Studio, necesita un nuevo perfil de publicación.  toodownload Hola nuevo perfil de publicación:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. Haga clic en **Obtener perfil de publicación**.

archivo de configuración de publicación de Hello es equipo tooyour descargado.  Normalmente se llama *nombre_del_sitio*.PublishSettings.  Hola de importar la configuración en el proyecto existente de publicación:

1. Abra Visual Studio y el proyecto de Servicio móvil de Azure.
2. Haga clic en el proyecto en hello **el Explorador de soluciones** y seleccione **publicar...**
3. Haga clic en **Importar**
4. Haga clic en **Examinar** y seleccione el archivo de configuración de publicación descargado.  Haga clic en **Aceptar**
5. Haga clic en **validar conexión** tooensure Hola publique el trabajo de configuración.
6. Haga clic en **publicar** toopublish su sitio.

## <a name="working-with-your-site"></a>Migración posterior al sitio
Empezar a trabajar con su nuevo servicio de aplicación Hola [portal de Azure] posteriores a la migración.  Hello siguientes son algunas notas en las operaciones concretas que usa tooperform en hello [Portal clásico de Azure], junto con su equivalente de servicio de aplicaciones.

### <a name="publishing-your-site"></a>Descarga y publicación del sitio migrado
El sitio está disponible a través de git o ftp, y se puede volver a publicar con varios mecanismos diferentes, como WebDeploy, TFS, Mercurial, GitHub y FTP.  las credenciales de implementación de Hola se migran con rest Hola de su sitio.  Si no estableció las credenciales de implementación o no las recuerda, puede restablecerlas:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **las credenciales de implementación** Hola menú de publicación.
5. Escriba nuevas credenciales de implementación de hello en los cuadros de hello correspondientes, a continuación, haga clic en el botón Guardar de Hola.

Puede usar estos sitios de hello tooclone credenciales con git o configurar implementaciones automatizadas de GitHub, TFS o Mercurial.  Para obtener más información, vea hello [documentación de implementación de servicio de aplicaciones de Azure].

### <a name="appsettings"></a>Configuración de aplicación
La mayoría de las configuraciones de un servicio móvil migrado están disponible a través de Configuración de aplicación.  Puede obtener una lista de configuración de la aplicación hello de hello [portal de Azure].
tooview o cambiar la configuración de aplicación:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **configuración de la aplicación** menú GENERAL Hola.
5. Desplácese toohello sección de configuración de la aplicación y busque la configuración de la aplicación.
6. Haga clic en valor de Hola de hello aplicación tooedit Hola valor.  Haga clic en **guardar** valor de hello toosave.

Puede actualizar varias opciones de configuración de aplicación en hello mismo tiempo.

> [!TIP]
> Existen dos configuraciones de aplicación con hello mismo valor.  Por ejemplo, puede ver *ApplicationKey* y *MS\_ApplicationKey*.  Actualizar ambas opciones de aplicación en hello mismo tiempo.
>
>

### <a name="authentication"></a>Autenticación
Todas las configuraciones de autenticación están disponibles como configuración de aplicación en su sitio migrado.  tooupdate la configuración de autenticación, debe modificar la configuración de la aplicación adecuada.  Hello tabla siguiente muestra valores de la aplicación adecuada de hello para el proveedor de autenticación:

| Proveedor | Id. de cliente | Secreto del cliente | Otras configuraciones |
|:--- |:--- |:--- |:--- |
| Cuenta Microsoft |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Nota: **MS\_AadTenants** se almacena como una lista separada por comas de dominios del inquilino (campos de Hola "Inquilinos permitida" en el portal de servicios móviles de hello).

> [!WARNING]
> **No use los mecanismos de autenticación de hello en el menú de configuración de Hola**
>
> Servicio de aplicaciones de Azure proporciona un sistema de autenticación y autorización de "sin código" independiente en hello *autenticación / autorización* hello (en desuso) y menú configuración *Mobile autenticación* opción en el menú de configuración de Hola.  Estas opciones no son compatibles con un servicio móvil de Azure migrado.  También puede [actualizar su sitio](app-service-mobile-net-upgrading-from-mobile-services.md) tootake ventaja de autenticación del servicio de aplicación de Azure Hola.
>
>

### <a name="easytables"></a>Datos
Hola *datos* ficha en servicios móviles se ha reemplazado por *tablas fácil* dentro de hello portal de Azure.  tooaccess fácil tablas:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **tablas fácil** en menú móviles Hola.

Puede agregar una tabla haciendo clic en hello **agregar** botón u obtener acceso a las tablas existentes, haga clic en un nombre de tabla.  En esta hoja se pueden realizar varias operaciones, entre las que se incluyen:

* Cambiar los permisos de tabla
* Editar scripts operacionales Hola
* Administrar el esquema de la tabla de Hola
* Eliminar tabla de Hola
* Borrar el contenido de la tabla de Hola
* Eliminar filas de tabla de hello específicas

### <a name="easyapis"></a>API
Hola *API* ficha en servicios móviles se ha reemplazado por *API fácil* dentro de hello portal de Azure.  tooaccess API sencilla:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Haga clic en **API fácil** en menú móviles Hola.

Las API migradas ya se muestran en la hoja de Hola.  También puede agregar una API desde esta hoja.  toomanage una API específica, haga clic en la API de Hola.
Desde la nueva hoja de hello, puede ajustar los permisos de Hola y editar scripts de Hola para hello API.

### <a name="on-demand-jobs"></a>Trabajos del Programador
Todos los trabajos de programador están disponibles a través de hello sección colecciones de trabajos de programador.  tooaccess los trabajos de programador:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **examinar >**, escriba **programación** en hello *filtro* cuadro y haga clic en **colecciones programador**.
3. Seleccione Hola colección de trabajos para el sitio.  Se denomina *nombre_del_sitio*-Jobs.
4. Haga clic en **Configuración**.
5. Haga clic en **Trabajos del Programador** en ADMINISTRAR.

Los trabajos programados se muestran con frecuencia Hola especificados antes de la migración.  Los trabajos a petición se deshabilitan.  toorun un trabajo a petición:

1. Seleccione el trabajo Hola desea toorun.
2. Si es necesario, haga clic en **habilitar** trabajo de hello tooenable.
3. Haga clic en **Configuración** y después en **Programar**.
4. Seleccione **Una vez** como periodicidad y haga clic en **Guardar**

Los trabajos a petición se encuentran en `App_Data/config/scripts/scheduler post-migration`.  Se recomienda convertir todos los trabajos de petición demasiado[WebJobs] o [funciones].  Escriba los nuevos trabajos del programador como [WebJobs] o [funciones].

### <a name="notification-hubs"></a>Centros de notificaciones
Los Servicios móviles usan Centros de notificaciones para las notificaciones push.  Hola después de la configuración de la aplicación es usados toolink Hola centro de notificaciones tooyour servicio móvil después de la migración:

| Configuración de aplicación | Descripción |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Hola Namespace de concentrador de notificación |
| **MS\_NotificationHubName** |Hola, nombre del concentrador de notificación |
| **MS\_NotificationHubConnectionString** |Hola cadena de conexión de concentrador de notificación |
| **MS\_NamespaceName** |Un alias para MS_PushEntityNamespace |

El centro de notificaciones se administra a través de hello [portal de Azure].  Tenga en cuenta el nombre del centro de notificaciones hello (puede encontrar esto mediante la configuración de la aplicación hello):

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **Examinar**> y luego **Notification Hubs**
3. Haga clic en nombre del centro de notificaciones de hello asociado con el servicio móvil de Hola.

> [!NOTE]
> Si el Centro de notificaciones es del tipo "Mixto", no está visible.  Los centros de notificaciones mixtos usan características de Centros de notificaciones y características heredadas de Bus de servicio.  [Convierta los espacios de nombres mixtos] antes de continuar.  Una vez completada la conversión de hello, el centro de notificaciones aparece en hello [portal de Azure].
>
>

Para obtener más información, consulte hello [centros de notificaciones] documentación.

> [!TIP]
> Características de administración de bases de datos centrales de notificación en hello [portal de Azure] están aún en la vista previa.  Hola [Portal clásico de Azure] sigue estando disponible para administrar todos sus centros de notificaciones.
>
>

### <a name="legacy-push"></a>Configuración de inserción heredada
Si configuró la inserción en el servicio móvil antes de introducción de hello en los centros de notificaciones, que usa *inserción heredada*.  Si utiliza Inserción y no ve un Centro de notificaciones en la configuración, es probable que utilice *inserción heredada*.  Esta característica se migra con todas las demás.  Sin embargo, se recomienda actualizar concentradores tooNotification poco después de la migración de hello está completa.

Hola provisional, todos los valores de inserción heredada de hello (con la excepción notable de Hola de certificado de APN Hola) están disponibles en la configuración de la aplicación.  Actualizar certificado de APN Hola reemplazando archivo adecuado de hello en hello filesystem.

### <a name="app-settings"></a>Otra configuración de aplicación
Hola después de la configuración de la aplicación adicional se migran desde su servicio móvil y están disponibles en *configuración* > *configuración de la aplicación*:

| Configuración de aplicación | Descripción |
|:--- |:--- |
| **MS\_MobileServiceName** |nombre de saludo de la aplicación |
| **MS\_MobileServiceDomainSuffix** |prefijo de dominio de Hola. es decir, azure-mobile.net |
| **MS\_ApplicationKey** |La clave de aplicación. |
| **MS\_MasterKey** |La clave maestra de aplicación. |

clave de la aplicación Hello y la clave principal son idéntico toohello claves de aplicación de su servicio móvil original.  En concreto, Hola clave de aplicación se envía por clientes móviles toovalidate su uso de API móviles Hola.

### <a name="cliequivalents"></a>Equivalentes de línea de comandos
Ya puede usar hello *azure móvil* comando toomanage el sitio de servicios móviles de Azure.  En su lugar, muchas funciones han sido reemplazadas por hello *sitio de azure* comando.  Use Hola siguiente tabla se toofind equivalentes para los comandos comunes:

| Comando de *Azure Mobile* | Comando equivalente del *sitio de Azure* |
|:--- |:--- |
| mobile locations |site location list |
| mobile list |site list |
| mobile show *name* |site show *name* |
| mobile restart *name* |site restart *name* |
| mobile redeploy *name* |site deployment redeploy *commitId* *name* |
| mobile key set *name* *type* *value* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile config list *name* |site appsetting list *name* |
| mobile config get *name* *key* |site appsetting show *key* *name* |
| mobile config set *name* *key* |site appsetting delete *key* *name* <br/> site appsetting add *key*=*value* *name* |
| mobile domain list *name* |site domain list *name* |
| mobile domain add *name* *domain* |site domain add *domain* *name* |
| mobile domain delete *name* |site domain delete *domain* *name* |
| mobile scale show *name* |site show *name* |
| mobile scale change *name* |site scale mode *mode* *name* <br /> site scale instances *instances* *name* |
| mobile appsetting list *name* |site appsetting list *name* |
| mobile appsetting add *name* *key* *value* |site appsetting add *key*=*value* *name* |
| mobile appsetting delete *name* *key* |site appsetting delete *key* *name* |
| mobile appsetting show *name* *key* |site appsetting delete *key* *name* |

Actualizar la autenticación o notificación de inserción configuración actualizando Hola configuración adecuada de la aplicación.
Edite los archivos y publique su sitio mediante ftp o git.

### <a name="diagnostics"></a>Diagnósticos y registro
El registro de diagnóstico está normalmente deshabilitado en un Servicio de aplicaciones de Azure.  registro de diagnóstico de tooenable:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. hoja de configuración de Hola se abre de forma predeterminada.
4. Seleccione **registros de diagnóstico** en el menú de características de Hola.
5. Haga clic en **ON** para hello siguientes registros: **(Filesystem) de registro de aplicaciones**, **mensajes de error detallados**, y **seguimiento de solicitudes con error**
6. Haga clic en **Sistema de archivos** en el registro de servidor web.
7. Haga clic en **Guardar**

registros de Hola tooview:

1. Inicie sesión en toohello [portal de Azure].
2. Seleccione **todos los recursos** o **servicios de aplicaciones** , a continuación, haga clic en nombre de hello del servicio móvil migrados.
3. Haga clic en hello **herramientas** botón
4. Seleccione **flujo de registro** en el menú OBSERVE Hola.

Los registros se muestran en la ventana hello tal y como se generan.  También puede descargar los registros de Hola para su análisis posterior mediante sus credenciales de implementación. Para obtener más información, vea hello [registro] documentación.

## <a name="known-issues"></a>Problemas conocidos
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>La eliminación de un clon de aplicaciones móviles migradas provoca una interrupción del sitio
Si se clona el servicio móvil migrado mediante Azure PowerShell y, a continuación, eliminar Hola clon, se quita Hola entrada DNS para el servicio de producción.  Su sitio es ya no estarán accesibles desde Internet Hola.  

Solución: Si desea que tooclone su sitio, hacerlo a través del portal de Hola.

### <a name="changing-webconfig-does-not-work"></a>El cambio de Web.config no funciona
Si tiene un sitio ASP.NET, cambia toohello `Web.config` archivo no se aplica.  Hola servicio de aplicaciones de Azure genera una adecuado `Web.config` archivo en tiempo de ejecución de servicios móviles de inicio toosupport Hola.  Puede reemplazar determinadas configuraciones (como los encabezados personalizados) mediante un archivo de transformación XML.  Cree un archivo denominado en `applicationHost.xdt` -este archivo debe terminar en hello `D:\home\site` directorio Hola servicio de Azure.  Cargue el archivo `applicationHost.xdt` a través de un script de implementación personalizado o directamente mediante Kudu.  Hola continuación, muestra un ejemplo del documento:

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Para obtener más información, vea hello [XDT transformar ejemplos] documentación a GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Servicios móviles migrados no se puede agregar tooTraffic Manager
Cuando se crea un perfil de Traffic Manager, no puede elegir un perfil de servicio móvil migrados toohello directamente.  Use un "punto de conexión externo".  El punto de conexión externo solo puede agregarse a través de PowerShell.  Para más información, consulte el [tutorial de Traffic Manager](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Pasos siguientes
Ahora que la aplicación está tooApp migrado servicio, hay más características que puede usar:

* Implementación [ranuras de ensayo] le permiten sitio tooyour de toostage cambios y realizar un B realizar pruebas.
* [WebJobs] ofrece una sustitución para trabajos programados a petición.
* También puede [implementar continuamente] su sitio mediante la vinculación de su sitio tooGitHub, TFS o Mercurial.
* Puede usar [Application Insights] toomonitor su sitio.
* Serve un sitio Web y una API de Mobile desde Hola mismo código.

### <a name="upgrading-your-site"></a>Actualizar su tooAzure de sitio de servicios móviles SDK de aplicaciones móviles
* Para los proyectos de servidor basado en Node.js, Hola nuevos [SDK de Node.js de aplicaciones móviles] proporciona varias características nuevas. Por ejemplo, ahora puede desarrollar y depurar localmente, usar cualquier versión de Node.js posterior a la 0.10 y personalizar con cualquier middleware de Express.js.
* Para. Proyectos de servidor basada en red, Hola nuevos [paquetes de NuGet de SDK de aplicaciones móviles](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) dispone de más flexibilidad en las dependencias de NuGet.  Estos paquetes admiten la autenticación de servicio de aplicaciones nueva hello y crear con cualquier proyecto de ASP.NET. Para más información acerca de la actualización, consulte [actualizar su tooApp .NET Mobile Service existente servicio](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Precios de Servicio de aplicaciones]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[Escalado automático]: ../app-service-web/web-sites-scale.md
[servicio de aplicaciones de Azure]: ../app-service/app-service-value-prop-what-is.md
[documentación de implementación de servicio de aplicaciones de Azure]: ../app-service-web/web-sites-deploy.md
[Portal clásico de Azure]: https://manage.windowsazure.com
[portal de Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[planes de programador de Azure]: ../scheduler/scheduler-plans-billing.md
[implementar continuamente]: ../app-service-web/app-service-continuous-deployment.md
[Convierta los espacios de nombres mixtos]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[nombres de dominio personalizados]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[disponibilidad general del servicio de aplicaciones de Azure]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[conexiones híbridas]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[registro]: ../app-service-web/web-sites-enable-diagnostic-log.md
[SDK de Node.js de aplicaciones móviles]: https://github.com/azure/azure-mobile-apps-node
[frente a servicios móviles. Servicio de aplicaciones]: app-service-mobile-value-prop-migration-from-mobile-services.md
[centros de notificaciones]: ../notification-hubs/notification-hubs-push-notification-overview.md
[supervisión del rendimiento]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[ranuras de ensayo]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[WebJobs]: ../app-service-web/websites-webjobs-resources.md
[XDT transformar ejemplos]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[funciones]: ../azure-functions/functions-overview.md
