---
title: "Ejemplo de IoT de Azure MyDriving: compilación | Microsoft Docs"
description: "Compilar una aplicación que es una demostración completa de cómo tooarchitect un sistema IoT mediante Microsoft Azure, incluido el análisis de transmisiones, aprendizaje automático y concentradores de eventos."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Compilar e implementar el entorno de hello MyDriving solución tooyour
MyDriving es una solución de Internet de las cosas (IoT) que recopila datos de su automóvil, los procesa mediante el aprendizaje automático y los presenta en el teléfono móvil. back-end de Hello consta de una serie de servicios proporcionados por Microsoft Azure. los clientes de Hello pueden estar teléfonos Android, iOS o Windows 10.

Hemos creado hello MyDriving solución toogive que un punto de partida para crear su propio sistema de IoT. De hello [MyDriving repositorio en GitHub](https://github.com/Azure-Samples/MyDriving), puede obtener scripts de Azure Resource Manager arquitectura de back-end de hello toodeploy en su propia cuenta de Azure. Desde ese punto, puede volver a configurar diferentes servicios de hello, modificar Hola consultas toosuit sus propios datos y así sucesivamente. Puede encontrar estas secuencias de comandos, junto con el código de aplicación móvil de hello, el proyecto de API del servicio de aplicación de Azure hello y mucho más, en el repositorio de MyDriving Hola.

Si todavía no ha probado aplicación hello aún, mirar hello [Guía de introducción de Get](iot-solution-get-started.md).

Hay una cuenta detallada de la arquitectura de Hola Hola de [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs). En resumen, hay varios elementos que configuramos toocreate un proyecto similar:

* Una **aplicación cliente** funciona en teléfonos Android, iOS y Windows 10. Usamos hello Xamarin plataforma tooshare gran parte del código de hello, que se almacena en GitHub en `src/MobileApp`. aplicación Hello realmente realiza dos funciones distintas:
  * Retransmite telemetría de dispositivo de diagnóstico a bordo (DAB) de Hola y de back-end de nube de su propia ubicación servicio toohello sistema.
  * Es una interfaz de usuario en la que los usuarios pueden consultar sus desplazamientos registrados.
* A **servicio en la nube** recopila datos de viaje hello en tiempo real y lo procesa. el trabajo principal de Hola de creación de este servicio se toochoose, parametrizar y conecte una variedad de servicios de Azure. Algunas partes de hello requieren scripts toofilter y proceso Hola los datos entrantes. Utilizamos un tooconfigure de plantilla de Azure Resource Manager todas las partes de Hola.
* A **aplicación de servicio móvil** es hello web servicio detrás de la parte de interfaz de usuario de Hola de aplicación para dispositivos Hola. Su trabajo principal es la base de datos de Hola de tooquery de datos almacenados, que se procesa. Su código se encuentra en GitHub en `src/MobileAppService`.
* **Visual Studio con Xamarin** es nuestro entorno de desarrollo. Xamarin, que existe como un componente de Visual Studio y como un entorno independiente de desarrollo integrado (IDE), se usa código de toobuild Hola dispositivos multiplataforma. código de iOS de toobuild hello, es necesario toohave una instancia de Xamarin que se ejecuta en una máquina de OS X. Si es necesario, se puede ejecutar como un agente administrado desde Visual Studio.
* **Pruebas unitarias** del dispositivo de hello aplicaciones se realiza en la nube de la prueba de Xamarin.
* **GitHub** es donde se almacenan todas las secuencias de comandos, plantillas y código de hello de repositorio de Hola.
* **Visual Studio Team Services** es un servicio de nube que ha utilizado toomanage continuada de compilación de Hola y prueba de aplicaciones de servicio y el dispositivo de hello web.
* **HockeyApp** es toodistribute usa las versiones de código de hello de dispositivos. También recopila comentarios de usuario y los informes de uso y bloqueo.
* **Visual Studio Application Insights** monitores Hola servicio web móvil.

Ahora veamos cómo se configura todo esto. 

> [!NOTE] 
> Muchas de hello pasos son opcionales.
>
>

## <a name="sign-up-for-accounts"></a>Registro de cuentas
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Es un programa gratuito proporciona herramientas de desarrollo de toomany de fácil acceso y servicios, incluidos Visual Studio, Visual Studio Team Services y Azure. Proporciona un crédito mensual de 25 dólares al mes en Azure durante 12 meses. También incluye suscripciones tooPluralsight entrenamiento y la Universidad de Xamarin. También puede registrarse por separado en los niveles gratuitos de [Azure](https://azure.com) y [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx), pero en este caso no se proporcionan créditos de Azure.
* [HockeyApp](https://rink.hockeyapp.net/) : (opcional) para administrar la distribución de las pruebas de aplicaciones móviles y recopilar datos de telemetría.
* [Xamarin](https://xamarin.com/) (obligatorio), para la creación de aplicaciones móviles de Hola y ejecuta ejecuciones de depuración y pruebas [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (opcional), toocreate de repositorios públicos disponible para su propio código (se pagan repositorios privados). Como alternativa, puede usar el plan básico de Hola en Visual Studio Team Services para repositorios privados.
* [Power BI](https://powerbi.microsoft.com/) (opcional), visualizaciones enriquecidas toocreate de datos en todo sistema de Hola.

> [!NOTE]
> No es necesario un GitHub tooaccess cuenta Hola código MyDriving en [Hola repositorio de GitHub MyDriving](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Instalación de herramientas de desarrollo
Hello siguiente el programa de instalación está diseñado para desarrollar la solución completa de hello: un iOS, Android y Windows 10 Mobile aplicación multiplataforma, con un Azure back-end.

Como alternativa, puede usar Xamarin Studio en Mac o Windows aplicaciones móviles de Hola de toodevelop si ya no está trabajando en hello Azure vuelve a finalizar.

[Aquí](https://msdn.microsoft.com/library/mt613162.aspx)puede consultar una descripción más detallada.

### <a name="windows-development-machine"></a>Máquina de desarrollo Windows
herramienta central de Hello en Windows es Visual Studio para trabajar con hello MyDriving app para Android y Windows, proyecto de API de servicio de aplicación hello y extensiones de microservicio.

Visual Studio incluye Xamarin, Git, emuladores y otros componentes útiles.

Instalación:

* [Visual Studio con Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (cualquier edición – Community es gratuita).
* [SQLite para Plataforma universal de Windows](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Requiere código de Windows 10 Mobile hello toobuild.
* [Azure SDK para Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Encontrará hello SDK para aplicaciones en ejecución en Azure, junto con herramientas de línea de comandos para la administración de Azure.
* [SDK de Azure Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Hola toobuild requiere [microservicio](../service-fabric/service-fabric-get-started.md) extensión.

Asegúrese de que dispone de extensiones de Visual Studio derecho Hola. Compruebe que en **Herramientas**, aparece **Android, iOS, Xamarin....**. Si no es así, abra Visual Studio, busque Xamarin y siguen tooinstall de mensajes de Hola. También debe comprobar si **Git para Windows** está instalado. Si no es así, en Visual Studio, búsquelo y siga tooinstall de mensajes de Hola. 

### <a name="mac-development-machine"></a>Máquina de desarrollo Mac
Hola Mac (Yosemite o posterior) es necesario si desea toodevelop para iOS. Aunque se use Visual Studio con Xamarin en toodevelop de Windows y administra todo el código de hello, Xamarin utiliza a un agente instalado en un equipo Mac en orden toobuild y código de iOS de Hola de inicio de sesión.

![Desarrollo en Windows y compilación en Mac](./media/iot-solution-build-system/image1.png)

(Como alternativa, puede usar Xamarin Studio directamente en aplicaciones multiplataforma de hello Mac toodevelop.)

Hola Mac no es necesario si no desea iOS tooinclude como una plataforma de destino.

Instalación:

* [Xamarin Studio para iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). También puede configurar Visual Studio y Xamarin en un equipo Mac que ejecute una máquina virtual de Windows. Consulte [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) en MSDN.
* [Herramientas de desarrollo de Azure](https://azure.microsoft.com/downloads/) (opcional).

Habilitar inicio de sesión remoto en hello Mac. Abra **Preferencias del sistema** > **Compartir** y seleccione **Inicio de sesión remoto**.

Al abrir un proyecto de iOS en Visual Studio en Windows, hello Xamarin complemento le solicitará que para el Id. de Hola de hello Mac.

## <a name="fetch-hello-github-repository"></a>Capturar el repositorio de GitHub de Hola
Capturar una copia local de [Hola repositorio de GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) mediante el uso de hello **Download ZIP** botón en GitHub, Visual Studio u otro cliente de Git.

Descomprima el archivo tooa carpeta de hello con un nombre de ruta de acceso corta, por ejemplo, C:\\código.

O bien, si desea tookeep una toodate con o contribuir en el código de tooour, clone el repositorio de hello como sigue:

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Obtención de la clave de API de mapas de Bing
[Regístrese para obtener una clave de API de Mapas de Bing](https://msdn.microsoft.com/library/ff428642.aspx).

Necesita tooreplace en esta línea 22 en `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Compilar la aplicación de demostración de hello
Abra estas soluciones en Visual Studio:

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Se le pedirá lo siguiente:

* Confiar en algunos proyectos potencialmente no confiables. Elija tooopen ellos si desea toogo con antelación.
* Establecer el modo de programador si está trabajando en una nueva máquina de Windows 10.
* Proporcionar sus credenciales de Xamarin.
* Conectar toohello Xamarin Mac. Si no tiene un equipo Mac, iOS Hola de menú contextual del proyecto en Visual Studio y, a continuación, seleccione **descargar el proyecto**.

Volver a generar solución Hola.

Si tienes que crear problemas, intente Hola soluciones tooquirks que hemos encontrado:

* *No se carga el proyecto de VINLookupApplication*: asegúrese de que ha instalado hello [Azure SDK para Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *No se compila el proyecto de Service Fabric*: compilar proyectos de la interfaz de hello en primer lugar y asegúrese de que ha instalado Hola SDK del servicio de Fabric.
* *La aplicación Android no se compila*:
  
  * Abra **Herramientas** > **Android** > **Android SDK Manager** (Administrador de SDK de Android) y asegúrese de que está instalada la plataforma Android 6 (API 23)/SDK.
  * Elimine este directorio y luego recompile:<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Obtener el código de hello tooknow
En soluciones de hello, encontrará:

* Extensiones de Azure: Service Fabric.
* HDInsight de Azure: scripts para procesar los datos de los traslados en Azure.
* Aplicaciones móviles: Hola aplicaciones para dispositivos.
* MobileAppsService/MyDrivingService: nuevo web de hello Finalizar.
* Power BI: definición de informe Hola.
* Scripts:
  
  * El Administrador de recursos: plantillas toobuild Hola recursos de Azure.
  * PowerShell: Plantillas de administrador de recursos Scripts toorun Hola.
  * Base de datos SQL de Azure: depuración de bases de datos.
* Base de datos SQL: CreateTables: definiciones de esquema.
* Análisis de transmisiones de Azure: Consulta ese flujo de datos de transformación Hola entrantes.

## <a name="run-hello-apps-in-development-mode"></a>Ejecutar aplicaciones de hello en modo de desarrollo
Realizar acción toorun aplicaciones hello, en función de dispositivo de Hola que esté usando:

* Back-end: MyDrivingService conjunto como proyecto de inicio de Hola y pulse servicio back-end web de F5 toorun Hola. Se abrirá una vista del explorador de anuncio Hola API.
* Los clientes móviles: Hola [se desarrollan aplicaciones móviles en Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android: para obtener más información, consulte [Debugging Android in Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/)(Depuración de Android en Xamarin).
  * iOS: para obtener más información, consulte [Debugging in iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/)(Depuración en iOS).
  * Windows Phone: para obtener más información, consulte [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Cargar hello tooHockeyApp de aplicaciones móviles
HockeyApp administra la distribución de Hola de los usuarios de tootest aplicación de Android, iOS o Windows, informar a los usuarios de nuevas versiones. También recopila útiles informes de errores, comentarios de usuarios con capturas de pantalla y métricas de uso.

[Empiece cargando](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) la aplicación compilada. A continuación, inicie sesión en demasiado[HockeyApp](https://rink.hockeyapp.net) desde el equipo de desarrollo. En el panel del desarrollador hello, haga clic en **nueva aplicación**y a continuación, arrastrar archivos Hola generan ventana hello. (Más adelante, este proceso puede automatizarse la toodo de servicio de compilación.)

Ahora se encuentra en el panel de la aplicación.

![Ficha información general en el panel de la aplicación hello](./media/iot-solution-build-system/image2.png)

Repita el proceso de Hola para cada plataforma que se ejecuta la aplicación. A continuación, puede hacer siguiente hello:

* Hola de uso [identificador de la aplicación](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) de datos de bloqueo de hello panel toosend y los comentarios de la aplicación. En MyDriving, actualice los identificadores de hello en src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Invite a usuarios de prueba](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Obtener una dirección URL toorecruit usuarios de evaluadores. Deberá ser capaz de toosign a su equipo, descargue la aplicación hello y enviar comentarios.
* Si prefiere una versión beta más abierta, establezca hello toopublic de distribución. Haga clic en **Administrar aplicación** > **Distribución** > **Descargar = público**. Ahora cualquier usuario puede descargar la aplicación, enviar comentarios y ver si se publica una nueva versión. También pueden enviarle informes de errores.
  
   ![Equipos en el panel de Hola](./media/iot-solution-build-system/image3.png)
* [Informes de bloqueo de vínculo tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Haga clic en **Administrar aplicación** > **Visual Studio Team Services**. HockeyApp puede crear automáticamente elementos de trabajo en Team Services cuando se generan informes de errores o cuando se reciben comentarios.

Lectura más en hello [HockeyApp sitio](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Probar la aplicación móvil de hello en Xamarin Test Cloud
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatiza las pruebas de IU en dispositivos reales en la nube de Hola. Con el marco de NUnit hello, escribir pruebas que ejecutan la aplicación a través de la interfaz de usuario de Hola.

toouse Xamarin, incorporan hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK en la aplicación, que está disponible como un paquete de NuGet. Encontrará en la aplicación de demostración de hello y se incluye al crear nuevos proyectos de prueba con hello plantillas de Xamarin.

![Donde toofind Hola multiplataforma SDK en la interfaz de Hola](./media/iot-solution-build-system/image4.png)

Un proyecto de prueba de ejemplo se incluye con la aplicación hello en el repositorio de Hola. En [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), mire en [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Si usa una compilación de Visual Studio Team Services, es fácil toowrite unidad Xamarin UI pruebas y ejecutarlas como parte de la compilación.

## <a name="deploy-azure-services"></a>Implementar servicios de Azure
tooperform una implementación automática de los servicios de Azure y servicios de compilación de Team Services, consulte toohello instrucciones en **scripts/README.md**.

Microsoft Azure ofrece una gran variedad de distintos servicios que se pueden usar aplicaciones en la nube toobuild. Aunque muchas se pueden utilizar individualmente (por ejemplo, aplicaciones de servicio Web o la aplicación), están en su mejor rendimiento cuando está interconectados tooform un sistema integrado probable que utilizamos en MyDriving.

Es posible toocreate y servicios de Azure se interconectan manualmente, pero es mucho más rápidas y más confiables plantillas de Azure Resource Manager toouse. [El Administrador de recursos](../azure-resource-manager/resource-group-overview.md) automatiza la implementación de Hola de recursos de una solución y realizar interconexiones Hola entre ellos.

Encontrará plantilla Hola de sistema de MyDriving de hello en el repositorio de GitHub de hello en [secuencias de comandos/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Proporciona una vista concisa y completa de cómo se interconectan los distintos servicios de hello en nuestra arquitectura. Se explican todas estas detalladamente en hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs), pero puede aprender mucho al leer a través de la propia plantilla de Hola.

> [!NOTE]
> Los servicios de Azure más tienen asociado un costo, según el nivel de precios de Hola. Si está tooAzure nueva, puede [Pruébelo GRATIS](https://azure.microsoft.com/free/). Sin embargo, si no tiene pensado toouse ciertos componentes de hello MyDriving system, ser seguro tooremove les tooavoid incurriendo en costes. Hola "Costes operativos estimación" sección más adelante en este artículo proporciona un resumen de los gastos de servicio típico.
> 
> 

### <a name="edit-hello-template"></a>Editar la plantilla de Hola
toocustomize la implementación, quizás tooremove que ya no necesite componentes o tooadd otros, primero realice una copia del escenario de\_complete.params.json y escenario\_complete.json qué cambios toomake.

Puede usar el escenario de hello\_complete.params.json toooverride de archivo predeterminado de varios valores, como Hola SKU o hello storage replicación tipo de servicio, como se describe en hello en la tabla siguiente. valores predeterminados de Hello seleccionar opciones de menor costo de Hola.

| **Parámetro** | **Descripción** | **Valor predeterminado** |
| --- | --- | --- |
| SDK de Centro de IoT |Nivel de servicio de Centro de IoT de Azure |F1 |
| Tipo de cuenta de almacenamiento |Tipo de replicación de almacenamiento |LRS estándar |
| Objetivo del servicio SQL |Consumo de ranuras de simultaneidad |DW100 |
| SKU de plan de hospedaje |Plan del Servicio de aplicaciones |F1 |

En scenario\_complete.json:

* Busque "baseName" y cambiar nombre tooa que prefiera.
* Busque "Create". Cada una de estas secciones crea un recurso.
* Establecer valores de toosuitable de sqlServerAdminLogin y sqlServerAdminPassword.
* Antes de eliminar una sección que crea un recurso, compruebe si tiene elementos dependientes mediante una búsqueda de su nombre en otro lugar en el archivo hello. Observe que cada sección que crea un servicio incluye una sección *dependsOn* en la que se enumeran sus dependencias.

Aquí configura qué plantilla de Hola. Detalles se encuentran en hello [Guía de referencia de](http://aka.ms/mydrivingdocs).

| **Servicio** | **Descripción y detalles** |
| --- | --- |
| Cuentas de almacenamiento |plantilla de Hello crea tres cuentas: |
| -Una base de datos SQL que recibe telemetría agregado de análisis de transmisiones y actúa como almacén de copia de seguridad de Hola para las tablas de servicio de aplicaciones de Azure que exponen estos datos a través de extremos de API. | |
| -Almacenamiento de blobs que acumula los datos históricos de otro trabajo de análisis de transmisiones, toobe procesado por HDInsight. | |
| - Base de datos SQL que recibe los resultados procesados por HDInsight que se usarán con Power BI. | |
| Azure IoT Hub |Establece un dispositivo conectado de tooeach de conexión en ambos sentidos. Hola MyDriving solución, aplicación móvil de hello actúa como un tooAzure de datos de campo puerta de enlace toosend centro de IoT. Centro de IoT de Azure, a continuación, actúa como una entrada tooStream análisis. |
| Azure Event Hubs |Una salida para un trabajo de análisis de transmisiones que pone en cola Hola salida tooextensions que se crean con Azure Service Fabric. |
| Almacenamiento de datos SQL de Azure | |
| Trabajos de Análisis de transmisiones |Conectar entradas y salidas con una consulta, que es usado tooaggregate datos en tiempo real e históricos para hello las API del servicio de aplicación, aprendizaje automático de Azure, extensiones y Power BI. |
| Área de trabajo de Aprendizaje automático |Incluye experimentos, código R y servicio de API. |
| Factoría de datos de Azure |Reciclaje programado de Aprendizaje automático. |
| Plan de hospedaje de Service Fabric |Para extensiones. |
| Servicio de aplicaciones (“Aplicación móvil”) |Proyecto de la API de aplicaciones móviles de hello hosts que proporciona puntos de conexión para aplicaciones móviles de Hola. código de la API de Hello debe ser implementado tooApp servicio desde Visual Studio. |
| Las reglas de alertas |Envía que un correo electrónico si las respuestas de aplicación Hola indican errores. |
| Application Insights |Para supervisar el rendimiento del programa Hola a las API de servicio de aplicaciones. Tiene conexión a hello tooconfigure en Visual Studio. |
| Azure Key Vault |Para guardar el certificado de clúster del servicio de hello web. |

### <a name="run-hello-template"></a>Ejecutar la plantilla de Hola
En **scripts/README.md**, se ofrecen instrucciones detalladas para ejecución plantilla Hola.

tooprovision todos estos servicios en su propia cuenta de Azure mediante script de Hola, realice una de hello siguientes:

* Use PowerShell.
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *ubicación* es hello [ubicación de Azure](https://azure.microsoft.com/regions/), como `North Europe` o `West US`. Use `Get-AzureLocation` toofind una lista de ubicaciones disponibles.
  * *resourceGroupName* es nombre hello que desee toogive toohello grupo que formará parte todos los recursos de Hola. Cuando haya terminado con recursos de hello, puede eliminarlos combina todas estas características mediante la eliminación de este grupo.
* Ejecute DeploymentScripts/Bash/deploy.sh con Bash.
* Abra y compile la solución de Visual Studio hello DeploymentScripts/VS/DeployARM.sln.

Tenga en cuenta que se ejecuta cada plantilla de Hola de tiempo, crea un nuevo conjunto de recursos con los nuevos nombres. recursos de hello toodelete, vaya toohello portal y eliminar el grupo de recursos de Hola.

Si se produce un error en el script de Hola por cualquier motivo, puede volver a ejecutarlo.

proporciona secuencias de comandos de Hola Hola opción de configurar la integración continua en Visual Studio Team Services. Si ha configurado un proyecto Team Services, tendrá una dirección URL: https://suNombredeCuenta.visualstudio.com. Escriba la dirección URL completa de hello cuando se le pregunte. Puede darle un nombre nuevo o uno existente para un proyecto Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Configuración de las definiciones de compilación y pruebas en Visual Studio Team Services
En este proyecto usamos Team Services principalmente por las características de compilación y prueba que ofrece. Además, proporciona una excelente compatibilidad de colaboración, como la administración de tareas con los tableros Kanban, la revisión del código integrada con tareas y control de código fuente y las compilaciones controladas. Se integra bien con otras herramientas como GitHub, Xamarin, HockeyApp y, por supuesto, Visual Studio. Se puede obtener acceso a él a través de la interfaz web de Hola o Visual Studio, lo que sea más conveniente en cualquier momento.

Hola los pasos de compilación de Hola y definiciones de versión utilizar una variedad de servicios de complemento que están disponibles en hello Team Services [Marketplace](https://marketplace.visualstudio.com/VSTS). En líneas de comandos de adición toobasic utilidades toorun o copiar archivos, hay servicios que invocar compilaciones Xamarin, Android y otros proveedores, y que conectan tooHockeyApp.

![Opciones de compilación en Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Definiciones de compilación
Contamos con definiciones de compilación para cada uno de los objetivos principales de Hola. También contamos con variaciones para pruebas de características y regresión. Esto es lo que nos proporciona:

* MyDriving.Services (aplicación de hello web back-end de aplicación móvil de hello)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-Feature
  * MyDriving.Xamarin.Android-Regression
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-Feature
  * MyDriving.Xamarin.iOS-Regression
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-Feature
  * MyDriving.Xamarin.UWP-Regression

Si desea toosee Hola todos los detalles de la configuración, vea la sección 4.7 de hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs), "La compilación y la configuración de versión." Siguen Hola mismo modelo general. script de Hola:

1. Restaura el paquete de NuGet Hola. No mantenemos código compilado en el repositorio de hello, para que hello primeros pasos de cada compilación consisten toorestore Hola necesario paquetes de NuGet.
2. Activa la licencia de Hola. se realiza la compilación de Hello en nube de hello, por lo que donde se necesita una licencia, en particular, por hello Xamarin crear servicio--tenemos tooactivate nuestra licencia en la máquina de compilación actual de Hola. A continuación, se desactivarlo inmediatamente después, tooallow lo toobe utilizado en otro equipo.
3. Compilaciones con servicio adecuado Hola. Utilizamos compilaciones de Xamarin para aplicaciones móviles de Hola y Visual Studio compila para servicio de hello web back-end.
4. Compila pruebas.
5. Ejecuta pruebas. Ejecutar pruebas de aplicación móvil de hello en Xamarin Test Cloud.
6. Publica Hola resultado toohello ubicación de destino.

desencadenador de Hola para las compilaciones de hello principal se establece toocontinuous integración. Es decir, se ejecuta una compilación de hello cada vez que se protege el código en la bifurcación principal toohello.

![La interfaz donde el desencadenador de hello es conjunto toocontinuous integración](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Definiciones de versión
Definiciones de versión se configuran en cantidad Hola igual manera.

Servicio web de hello, establecemos la implementación como una aplicación web de Azure:

![Interfaz para configurar la implementación como una aplicación web de Azure](./media/iot-solution-build-system/image7.png)

Y se configura la implementación de toocontinuous de desencadenador de versión de Hola. Es decir, de cada protección seguido por una compilación correcta da como resultado una aplicación web de toohello de actualización.

![Interfaz para establecer la implementación de toocontinuous de desencadenador de versión de Hola](./media/iot-solution-build-system/image8.png)

Para las aplicaciones móviles, implementamos tooHockeyApp:

![Interfaz para implementar una aplicación móvil tooHockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Exploración de los datos de telemetría mediante Application Insights
[Application Insights](../application-insights/app-insights-overview.md) recopila telemetría sobre el rendimiento de Hola y el uso de los servicios web. Hola Application Insights SDK envía telemetría de hello servicio toohello recursos de Application Insights en Azure.

Examinar toohello recursos de Application Insights esa plantilla Hola configurar. Allí, puede explorar los gráficos de rendimiento de Hola de su [proyecto de servicio de aplicación móvil](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Se muestran las solicitudes del servidor, los tiempos de respuesta, los errores y la cantidad de excepciones. También son gráficos de tiempos de respuesta de dependencia, es decir, base de datos de llamadas toohello y tooREST las API, como el aprendizaje automático. Si no hay ningún problema de rendimiento, podrá toosee capaz de qué parte del sistema está haciendo.

![Gráfico de rendimiento de ejemplo](./media/iot-solution-build-system/image11.png)

Si tiene un servicio web que configure manualmente, es fácil tooget Hola mismo gráficos. En la hoja de servicio web de hello, haga clic en **herramientas** > **extensiones** > **agregar**. Seleccione **Application Insights**.

![Interfaz para seleccionar los gráficos de hello tooget Application Insights](./media/iot-solution-build-system/image12.png)

característica de Hello funciona mediante la instrumentación de la aplicación con hello Application Insights SDK.

Puede agregar telemetría personalizada (o instrumentos de una aplicación que se ejecuta en algún lugar fuera de Azure) [agregar Hola Application Insights SDK](../application-insights/app-insights-asp-net.md) en tiempo de desarrollo. Se trata de métricas de toolog útil que dependen de la aplicación hello, como la longitud promedio de ida y vuelta de los usuarios o Kilometraje total. En Visual Studio, haga clic en proyecto de hello y, a continuación, seleccione **agregar Application Insights**.

![Interfaz para la selección de telemetría de agregar Application Insights tooadd personalizada](./media/iot-solution-build-system/image10.png)

Application Insights enviará correos electrónicos de alerta si detecta números inusuales de respuestas de error. También puede configurar sus propias alertas en varias métricas, como tiempos de respuesta.

Simplemente toobe seguro de que el servicio web estará siempre en activo y en ejecución, puede configurar la [pruebas de disponibilidad](../application-insights/app-insights-monitor-web-app-availability.md). Estas pruebas hacer ping en el sitio desde diversas ubicaciones mundo Hola cada 15 minutos. Una vez más, obtendrá un correo electrónico si parece que hay un problema de toobe.

## <a name="estimate-operational-costs"></a>Estimación de costos operativos
Es muy económica toorun una aplicación como esta a pequeña escala. Muchos de los servicios de hello dispone de niveles de nivel de entrada disponibles, para que el desarrollo y el funcionamiento a pequeña escala costo muy poco. Y por supuesto, sus propias aplicaciones no tienen toouse muestran todas las características de hello en MyDriving.

Esta es una estimación aproximada de nuestros costos al establecer la configuración de desarrollo de Hola para MyDriving. Asimismo, apuntamos algunas alternativas que *no* usamos. Esta información puede resultar útil a la hora de estimar sus propios costos.

Condiciones:

* Equipo no superior a cinco integrantes (+ partes interesadas observadoras).
* Ejecución durante un mes.
* 100 usuarios con cuatro viajes al día.

> [!NOTE]
> Soy nuevo tooAzure, hay un [libre cuenta](https://azure.microsoft.com/free/).
> 
> 

| **Servicio/Componente** | **Notas** | **Costo/Mes** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) con [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Entorno de desarrollo multiplataforma |Visual Studio Community. (Necesita [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) para [Xamarin.Forms](https://xamarin.com/forms), toodesign multiplataforma desde un único código base.) |0 $ |
| [Centro de IoT de Azure](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Toodevices de conexión de datos bidireccional |8000 mensajes + 0,5 KB/mensaje gratis |0 $ |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>   Procesamiento de datos de flujos de gran volumen. |Cargo de 0,031 $ por unidad de streaming por hora mientras esté habilitado. Elija el número de Hola de unidades de streaming que desee; tooscale más seguridad. |23 $ |
| [Aprendizaje automático](https://azure.microsoft.com/documentation/services/machine-learning/)<br/> Respuestas adaptables. |10 $/puesto/mes. <br/>                                                                                                                                                                                 + 3 horas experimento \* 1 $ / hora de experimento. <br/>                                                                                                                                                           + 3,5 horas API CPU \* 2 $ / hora de producción de CPU. <br/>                                                                                                                                                          El tiempo de CPU de la API asume 5 minutos al día de nuevo entrenamiento, aunque esto aumentaría con más datos de entrada.                   <br/>                                                                                                                                                                     + min 2/día puntuación tooprocess 400 viajes/día. |20 $ |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/> Host para el back-end móvil |Nivel B1: aplicaciones web de producción. |56 $ |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/> Compilación, pruebas unitarias y administración de versiones; administración de tareas |Agentes privados, cinco usuarios. |0 $ |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Supervisión de rendimiento y uso de sitios y servicios web |Nivel Gratis. |0 $ |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/> Distribución de aplicaciones beta, más recopilación de comentarios e información de uso y bloqueo |Dos aplicaciones gratuitas para nuevos usuarios.<br/> Después, 30 $/mes. |0 $ |
| [Xamarin](https://store.xamarin.com/)<br/> Código en una plataforma uniforme para varios dispositivos |Evaluación gratuita. <br/>Después, 25 $/mes. |0 $ |
| [Base de datos SQL](https://azure.microsoft.com/pricing/details/sql-database/) para el Servicio de aplicaciones de Azure |Nivel básico; modelo de base de datos única. |5 $ |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (opcional) |Ejecutar un clúster local. |0 $ |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/> Visualizaciones versátiles e investigación de datos transmitidos y estáticos |Nivel gratis: 1 GB, 10.000 filas por hora, la actualización diaria. <br/> 10 USD/usuario/mes para [límites más altos](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), más opciones de conexión y colaboración. |0 $ |
| [Almacenamiento](https://azure.microsoft.com/pricing/details/storage/) |L (con redundancia local) &lt; 100 G 0,024 $/GB. |3 $ |
| [Factoría de datos](https://azure.microsoft.com/pricing/details/data-factory/) |0,60 $ por actividad \* (8 - 5 FOC). |2 $ |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>  Clúster a petición para nuevo entrenamiento diario |Tres nodos de A3 a 0,32 $/hora por 1 hora diaria * 31 días. |30 $ |
| [Centros de eventos](https://azure.microsoft.com/pricing/details/event-hubs/) |Básico con unidad de procesamiento de 11 $/mes + entrada 0,028 $ |11 $ |
| Llave OBD | |12 $ |
| **Total** | |**157 $** |

Para más información, consulte:

* Resumen de [cuotas y límites del servicio de Azure](../azure-subscription-service-limits.md#iot-hub-limits)
* [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Envíenos sus comentarios
Ya hemos creado el punto de partida de MyDriving toohelp sus propios sistemas de IoT, por supuesto, es deseable toohear del usuario acerca de cómo funciona. Queremos saber si:

* Se enfrenta a dificultades y desafíos.
* Hay un punto de extensión que le resulte más conveniente escenario tooyour.
* Buscar un tooaccomplish de manera más eficaz de ciertas necesidades.
* Tiene cualquier sugerencia para mejorar MyDriving o esta documentación.

comentarios de toogive, archivos [problema en GitHub] o deje un comentario a continuación (en-us edition).

¡Esperamos tener toohearing del usuario.

## <a name="next-steps"></a>Pasos siguientes
Se recomienda hello [Guía de referencia de MyDriving](http://aka.ms/mydrivingdocs), que es una descripción completa del diseño de Hola de sistema de Hola y sus componentes.

