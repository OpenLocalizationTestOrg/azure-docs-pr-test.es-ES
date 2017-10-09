---
title: "aaaGet a trabajar con búsqueda de Azure en Java | Documentos de Microsoft"
description: "¿Cómo toobuild una nube hospedada Buscar aplicación en Azure con Java como el lenguaje de programación."
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a>Introducción a Búsqueda de Azure en Java
> [!div class="op_single_selector"]
> * [Portal](search-get-started-portal.md)
> * [.NET](search-howto-dotnet-sdk.md)
> 
> 

Obtenga información acerca de cómo buscar los toobuild personalizadas de Java en la aplicación que utiliza la búsqueda de Azure para su experiencia de búsqueda. Este tutorial usa hello [API de REST de servicio de búsqueda de Azure](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hola objetos y operaciones que se usan en este ejercicio.

toorun en este ejemplo, debe tener un servicio de búsqueda de Azure, que pueden suscribirse a Hola [Portal de Azure](https://portal.azure.com). Vea [crear un servicio de búsqueda de Azure en el portal de hello](search-create-service-portal.md) para obtener instrucciones paso a paso.

Se usa Hola después toobuild de software y probar este ejemplo:

* [IDE de Eclipse para desarrolladores de Java EE](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar). Ser seguro toodownload Hola EE versión. Uno de los pasos de comprobación de hello requiere una característica que se encuentra solo en esta edición.
* [JDK 8u40](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [Apache Tomcat 8.0](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a>Acerca de los datos de Hola
Esta aplicación de ejemplo utiliza datos de hello [servicios geológicas de Estados Unidos (USG)](http://geonames.usgs.gov/domestic/download_data.htm)y filtrado en el tamaño de conjunto de datos de hello estado de Rhode Island tooreduce Hola. Usaremos esta toobuild una aplicación de búsqueda que devuelve edificios de punto de referencia como hospitales y varios centros escolares, así como características geológicas como secuencias, lagos y cumbres de datos.

En esta aplicación, Hola **SearchServlet.java** programa genera y cargas Hola índice usando un [indizador](https://msdn.microsoft.com/library/azure/dn798918.aspx) construcción, recuperar Hola filtra USG conjunto de datos de una base de datos de SQL Azure pública. Se proporcionan credenciales predefinidas y origen de datos en línea de toohello de información de conexión en el código de programa Hola. En términos de acceso a datos, no es necesario realizar ninguna otra configuración.

> [!NOTE]
> Se aplica un filtro en este toostay de conjunto de datos en límite del documento 10.000 Hola de hello libre de nivel de precios. Si usas nivel estándar de hello, este límite no se aplica, y puede modificar este toouse código un conjunto de datos más grande. Para obtener más información acerca de la capacidad de cada nivel de precios, consulte [Límites y restricciones](search-limits-quotas-capacity.md).
> 
> 

## <a name="about-hello-program-files"></a>Acerca de los archivos de programa Hola
Hello lista siguiente describen los archivos de Hola que son relevantes toothis muestra.

* Search.jsp: Proporciona la interfaz de usuario de Hola
* SearchServlet.java: Proporciona métodos (controlador de tooa similar en MVC)
* SearchServiceClient.java: controla las solicitudes HTTP
* SearchServiceHelper.java: clase auxiliar que proporciona métodos estáticos
* Document.Java: Proporciona el modelo de datos de Hola
* config.Properties: establece la dirección URL del servicio de búsqueda de Hola y clave de api
* Pom.xml: una dependencia de Maven

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a>Buscar el nombre del servicio de Hola y clave de api del servicio en la búsqueda de Azure
Todas las llamadas de API de REST en búsqueda de Azure requieren que proporcione la dirección URL del servicio de hello y una clave de api. 

1. Inicie sesión en toohello [Portal de Azure](https://portal.azure.com).
2. En la barra de salto de hello, haga clic en **servicio de búsqueda** toolist todos los servicios de búsqueda de Azure Hola aprovisionados para su suscripción.
3. Seleccione servicio de Hola que desee toouse.
4. En el panel de servicio de hello, podrá ver iconos para obtener información esencial, así como icono de llave hello para tener acceso a las claves de administración de Hola.
   
      ![][3]
5. Copiar dirección URL del servicio de hello y una clave de administración. Los necesitará más adelante, cuando se agrega toohello **config.properties** archivo.

## <a name="download-hello-sample-files"></a>Descargar archivos de ejemplo de Hola
1. Vaya demasiado[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) en GitHub.
2. Haga clic en **Download ZIP**, guardar toodisk de archivo .zip de hello y, a continuación, extraer todos los archivos de Hola que contiene. Considere la posibilidad de extraer Hola proyecto de archivos en su toomake de área de trabajo de Java sea más fácil toofind hello más tarde.
3. archivos de ejemplo de Hola son de solo lectura. Haga clic en Propiedades de la carpeta y el atributo de solo lectura de hello desactive.

Todas las modificaciones y las instrucciones de ejecución subsiguientes se realizarán en los archivos de esta carpeta.  

## <a name="import-project"></a>Importación del proyecto
1. En Eclipse, elija **Archivo** > **Importar** > **General** > **Proyectos existentes al área de trabajo**.
   
    ![][4]
2. En **directorio raíz seleccione**, busque la carpeta toohello que contiene los archivos de ejemplo. Seleccione la carpeta de Hola que contiene la carpeta de .project Hola. proyecto de Hello debe aparecer en hello **proyectos** lista como un elemento seleccionado.
   
    ![][12]
3. Haga clic en **Finalizar**
4. Use **el Explorador de proyectos** tooview y editar archivos de Hola. Si no está ya abierto, haga clic en **ventana** > **Mostrar vista** > **el Explorador de proyectos** o usar Hola contextual tooopen lo.

## <a name="configure-hello-service-url-and-api-key"></a>Configurar la dirección URL del servicio de Hola y clave de api
1. En **el Explorador de proyectos**, haga doble clic en **config.properties** tooedit Hola configuración que contiene el nombre del servidor de Hola y clave de api.
2. Consulte los pasos toohello anteriormente en este artículo, donde se encuentra Hola dirección URL del servicio y la clave de api en hello [Portal de Azure](https://portal.azure.com), valores de hello tooget ahora entrará en **config.properties**.
3. En **config.properties**, reemplace "Clave de Api" con la clave de api de hello para el servicio. A continuación, el nombre de servicio (Hola primer componente de hello URL http://servicename.search.windows.net) reemplaza "nombre del servicio" Hola mismo archivo.
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a>Configurar entornos de proyecto de compilación y en tiempo de ejecución de Hola
1. En Eclipse, en el Explorador de proyectos, haga clic en proyecto de hello > **propiedades** > **proyecto facetas**.
2. Seleccione **Dynamic Web Module**, **Java** y **JavaScript**.
   
    ![][6]
3. Haga clic en **Apply**.
4. Seleccione **Ventana** > **Preferencias** > **Servidor** > **Entornos en tiempo de ejecución** > **Agregar...**.
5. Expanda Apache y seleccione la versión de Hola de servidor de Apache Tomcat Hola que instaló anteriormente. En nuestro sistema, se instala la versión 8.
   
    ![][7]
6. En la página siguiente de hello, especifique el directorio de instalación de Tomcat Hola. En un equipo Windows, probablemente será C:\Program Files\Apache Software Foundation\Tomcat *versión*.
7. Haga clic en **Finalizar**
8. Seleccione **Ventana** > **Preferencias** > **Java** > **JRE instalados** > **Agregar**.
9. En **Add JRE** (Agregar JRE), seleccione **Standard VM** (VM estándar).
10. Haga clic en **Siguiente**.
11. En JRE Definition (Definición de JRE), en JRE home (Directorio de JRE), haga clic en **Directory**(Directorio).
12. Navegue demasiado**archivos de programa** > **Java** y seleccione Hola JDK que se instaló anteriormente. Es importante tooselect Hola JDK como Hola JRE.
13. En versiones de JRE instalada, elija hello **JDK**. La configuración debe tener un aspecto similar toohello siguiente captura de pantalla.
    
    ![][9]
14. Si lo desea, seleccione **ventana** > **explorador Web** > **Internet Explorer** tooopen aplicación de hello en una ventana del explorador externo. Utilizar un explorador externo proporciona una mejor experiencia de aplicación web.
    
    ![][8]

Ahora ha completado las tareas de configuración de Hola. A continuación, podrá crear y ejecutar el proyecto de Hola.

## <a name="build-hello-project"></a>Compile el proyecto de Hola
1. En el Explorador de proyectos, haga clic en el nombre del proyecto de Hola y elija **ejecución** > **compilación de Maven...**  tooconfigure proyecto de Hola.
   
    ![][10]
2. En Edit Configuration (Editar configuración), en la sección Goals (Objetivos), escriba "clean install" y, a continuación, haga clic en **Run**(Ejecutar).

Mensajes de estado son la ventana de la consola de salida toohello. Debería ver compilaciones correctas e indica Hola proyecto sin errores.

## <a name="run-hello-app"></a>Ejecutar aplicación hello
En este último paso, ejecutará la aplicación hello en un entorno de tiempo de ejecución del servidor local.

Si aún no ha especificado un entorno de tiempo de ejecución de servidor en Eclipse, necesitará toodo primero este último.

1. En Project Explorer, expanda **WebContent**(Contenido web).
2. Haga clic con el botón secundario en **Search.jsp** > **Ejecutar como** > **Ejecutar en el servidor**. Seleccione el servidor Apache Tomcat de hello y, a continuación, haga clic en **ejecutar**.

> [!TIP]
> Si ha usado un área de trabajo no predeterminado toostore el proyecto, deberá toomodify **configuración de ejecución de** toopoint toohello proyecto ubicación tooavoid un error de inicio del servidor. En el Explorador de proyectos, haga clic en **Search.jsp** > **Ejecutar como** > **Configuraciones de ejecución**. Seleccione el servidor de hello Apache Tomcat. Haga clic en **Arguments**(Argumentos). Haga clic en **área de trabajo** o **sistema de archivos** tooset carpeta de Hola que contiene el proyecto de Hola.
> 
> 

Cuando se ejecuta la aplicación hello, debería ver una ventana del explorador, que proporciona un cuadro de búsqueda para introducir términos.

Espere aproximadamente un minuto antes de hacer clic **búsqueda** toogive Hola servicio tiempo toocreate y carga Hola el índice. Si recibe un error HTTP 404, solo tiene toowait un poco más larga antes de intentarlo de nuevo.

## <a name="search-on-usgs-data"></a>Buscar en los datos de USGS
conjunto de datos de Hello USG incluye registros de estado toohello relevante de Rhode Island. Si hace clic en **búsqueda** en un cuadro de búsqueda vacío, obtendrá entradas de 50 primeras hello, que es el valor predeterminado de Hola.

Escriba un término de búsqueda le dará el motor de búsqueda de hello algo toogo en. Pruebe a escribir un nombre regional. "Roger Williams" era gobernador primera Hola de Rhode Island. Hay numerosos parques, edificios y escuelas que llevan su nombre.

![][11]

También puede probar con alguno de estos términos:

* Pawtucket
* Pembroke
* goose +cape

## <a name="next-steps"></a>Pasos siguientes
Se trata del primer tutorial de búsqueda de Azure hello en función de hello USG dataset y Java. Con el tiempo, ampliaremos esta tutorial toodemonstrate características de búsqueda adicional puede toouse en sus soluciones personalizadas.

Si ya tiene conocimientos básicos en búsqueda de Azure, puede utilizar este ejemplo como un springboard para experimentación adicional, quizás aumentar hello [página de búsqueda](search-pagination-page-layout.md), o implementando [la navegación por facetas](search-faceted-navigation.md). También puede mejorar en la página de resultados de búsqueda de hello agregando los recuentos y procesamiento por lotes de documentos para que los usuarios pueden desplazarse a través de los resultados de Hola.

¿TooAzure nueva búsqueda? Se recomienda intentar otra toodevelop tutoriales una descripción de lo que puede crear. Visite nuestro [página de documentación](https://azure.microsoft.com/documentation/services/search/) toofind más recursos. También puede ver los vínculos de hello en nuestro [lista de vídeo y un Tutorial](search-video-demo-tutorial-list.md) tooaccess obtener más información.

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png
