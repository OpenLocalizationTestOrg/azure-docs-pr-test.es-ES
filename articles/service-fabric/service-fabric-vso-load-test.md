---
title: "aaaLoad probar su aplicación mediante Visual Studio Team Services | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toostress probar las aplicaciones de Azure Service Fabric mediante Visual Studio Team Services."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Prueba de carga de la aplicación mediante Visual Studio Team Services
Este artículo muestra cómo toouse Microsoft Visual Studio carga prueba características toostress probar una aplicación. Se usa un back-end de servicio con estado de Azure Service Fabric y un front-end web de servicio sin estado. Hello aplicación de ejemplo utilizado aquí es un simulador de la ubicación de avión. En él se proporciona un identificador de avión, una ubicación de salida y un destino. back-end de la aplicación Hello procesa las solicitudes de Hola y front-end de Hola se muestra en un avión de Hola de mapa que coincide con los criterios de Hola.

Hello siguiente diagrama ilustra aplicación de Service Fabric hello que va a probar.

![Diagrama de la aplicación de ubicación de avión de ejemplo de Hola][0]

## <a name="prerequisites"></a>Requisitos previos
Antes de empezar, necesita toodo Hola siguiente:

* Obtenga una cuenta de Visual Studio Team Services. Puede obtener una de forma gratuita en [Visual Studio Team Services](https://www.visualstudio.com).
* Obtenga e instale Visual Studio 2013 o Visual Studio 2015. Este artículo usa Visual Studio 2015 Enterprise Edition, pero Visual Studio 2013 y otras ediciones deberían funcionar de un modo similar.
* Implemente su tooa aplicación entorno de ensayo. Vea [cómo toodeploy aplicaciones tooa remoto clúster con Visual Studio](service-fabric-publish-app-remote-cluster.md) para obtener información acerca de esto.
* Comprenda el patrón de uso de la aplicación. Esta información es el modelo de carga de hello toosimulate usado.
* Comprender el objetivo de Hola para las pruebas de carga. Esto ayuda a interpretar y analizar los resultados de pruebas de carga de Hola.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Crear y ejecutar el proyecto de prueba de carga y rendimiento Web Hola
### <a name="create-a-web-performance-and-load-test-project"></a>Creación de un proyecto de prueba de carga y rendimiento web.
1. Abra Visual Studio 2015. Elija **archivo** > **New** > **proyecto** en hello tooopen la barra de menús de hello **nuevo proyecto** cuadro de diálogo.
2. Expanda hello **Visual C#** nodo y elija **prueba** > **proyecto de prueba de carga y rendimiento Web**. Asigne un nombre de proyecto de hello y, a continuación, elija hello **Aceptar** botón.

    ![Captura de pantalla del cuadro de diálogo nuevo proyecto de Hola][1]

    Debería ver un nuevo proyecto de prueba de carga y rendimiento web en el Explorador de soluciones.

    ![Captura de pantalla del explorador de soluciones con el nuevo proyecto de Hola][2]

### <a name="record-a-web-performance-test"></a>Grabación de un proyecto de prueba de rendimiento web
1. Proyecto de WebTest Hola abierto.
2. Elija hello **Agregar grabación** icono toostart una sesión de grabación en el explorador.

    ![Captura de pantalla del icono de agregar grabación hello en un explorador][3]

    ![Captura de pantalla del botón de registro de hello en un explorador][4]
3. Busque la aplicación de Service Fabric toohello. panel de grabación de Hello debe mostrar las solicitudes web de Hola.

    ![Captura de pantalla de solicitudes web en hello grabación panel][5]
4. Ejecute una secuencia de acciones que se espera Hola usuarios tooperform. Estas acciones se usan como un patrón toogenerate Hola de carga.
5. Cuando haya terminado, elija hello **detener** grabación de toostop de botón.

    ![Captura de pantalla del botón de detención de Hola][6]

    proyecto de WebTest Hello en Visual Studio debe haber capturado una serie de solicitudes. Los parámetros dinámicos se reemplazan automáticamente. En este momento, puede eliminar las solicitudes de dependencia adicionales repetidas que no forman parte de su escenario de prueba.
6. Guarde el proyecto de hello y, a continuación, elija hello **Ejecutar prueba** comando toorun Hola de rendimiento web una prueba local y asegúrese de que todo funciona correctamente.

    ![Captura de pantalla de hello comando Ejecutar prueba][7]

### <a name="parameterize-hello-web-performance-test"></a>Parametrizar la prueba de rendimiento web Hola
Hola de prueba de rendimiento web se puede parametrizar convirtiéndolo tooa codificada prueba de rendimiento web y, a continuación, editar código de hello. Como alternativa, puede enlazar la lista datos de tooa de prueba de rendimiento de hello web para que hello prueba recorre en iteración los datos de Hola. Vea [generar y ejecutar una prueba de rendimiento web codificada](https://msdn.microsoft.com/library/ms182552.aspx) para obtener más información acerca de cómo tooa de prueba de rendimiento de tooconvert hello web codificadas prueba. Vea [agregar una prueba de rendimiento web de datos origen tooa](https://msdn.microsoft.com/library/ms243142.aspx) para obtener información acerca de cómo toobind datos tooa web rendimiento pruebas.

En este ejemplo, se podrá convertir prueba de tooa codificada de prueba de rendimiento de hello web para que pueda reemplazar Hola avión identificador con un GUID generado y agregar más solicitudes toosend vuelos toodifferent ubicaciones.

### <a name="create-a-load-test-project"></a>Creación de un proyecto de prueba de carga
Un proyecto de prueba de carga se compone de uno o varios de los escenarios descritos por la prueba de rendimiento web de Hola y de prueba unitaria, junto con la configuración de prueba de carga especificado adicional. Hola siguientes pasos muestra cómo toocreate una carga el proyecto de prueba:

1. En el menú contextual de Hola de su proyecto de prueba de carga y rendimiento Web, elija **agregar** > **prueba de carga**. Hola **prueba de carga** asistente, elija hello **siguiente** botón Configuración de pruebas de tooconfigure Hola.
2. Hola **modelo de carga** sección, elija si desea que una carga de usuarios constante o una carga por pasos, que comienza con unos pocos usuarios y aumenta Hola a los usuarios con el tiempo.

    Si tiene una buena estimación de la cantidad de Hola de carga de usuarios y desea toosee cómo realiza el sistema actual de hello, elija **de carga constante**. Si su objetivo es toolearn si sistema Hola se lleva a cabo constantemente con diversas cargas, elija **carga por pasos**.
3. Hola **combinación de pruebas** sección, elija hello **agregar** botón y, a continuación, seleccione Hola de pruebas que desea tooinclude de prueba de carga de Hola. Puede usar hello **distribución** porcentaje de hello toospecify de columna de total se ejecutan para cada prueba de las pruebas.
4. Hola **parámetros de ejecución** sección, especifique la duración de la prueba de carga Hola.

   > [!NOTE]
   > Hola **iteraciones de prueba** opción está disponible solamente cuando ejecuta una prueba de carga localmente mediante Visual Studio.
   >
   >
5. Hola **ubicación** sección de **parámetros de ejecución**, especificar ubicación de Hola donde se generan las solicitudes de prueba de carga. Asistente de Hello puede solicitarle que toolog en tooyour cuenta de Team Services. Inicie sesión y elija una ubicación geográfica. Cuando haya terminado, elija hello **finalizar** botón.
6. Después de crea la prueba de carga de hello, abra Hola LoadTest proyecto y elija actual Hola ejecutar la configuración, como por ejemplo **parámetros de ejecución** > **Run Settings1 [Active]**. Se abre la configuración de hello ejecutar en hello **propiedades** ventana.
7. Hola **resultados** sección de hello **parámetros de ejecución** ventana Propiedades, hello **almacenamiento de detalles de tiempo** configuración debe tener **ninguno** como su valor predeterminado. Cambie este valor demasiado**todos los detalles individuales** tooget obtener más información sobre los resultados de pruebas de carga de Hola. Vea [cargar pruebas](https://www.visualstudio.com/load-testing.aspx) para obtener más información sobre cómo probar tooconnect tooVisual Studio Team Services y ejecutar una carga.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Ejecutar prueba de carga de hello mediante Visual Studio Team Services
Elija hello **ejecutar la prueba de carga** serie de pruebas de comando toostart Hola.

![Captura de pantalla de hello comando Ejecutar prueba de carga][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Ver y analizar los resultados de pruebas de carga de Hola
Como Hola progresa de prueba de carga, se representa gráficamente la información de rendimiento de Hola. Debería ver algo similar toohello después de gráfico.

![Captura de pantalla del gráfico de rendimiento para los resultados de pruebas de carga][9]

1. Elija hello **descargar informe** situado cerca de la parte superior de Hola de página de Hola. Después de descarga informe hello, elija hello **Ver informe** botón.

    En hello **gráfico** ficha puede ver gráficos para diversos contadores de rendimiento. En hello **resumen** ficha hello general resultados de pruebas aparecen. Hola **tablas** pestaña muestra el número total de Hola de pruebas de carga pasado pero no lo consiguió.
2. Elija los vínculos de número de hello en hello **prueba** > **error** hello y **errores** > **recuento** columnas Detalles del error toosee.

    Hola **detalle** ficha muestra información de escenario virtual de prueba y de usuario para solicitudes con error. Estos datos pueden ser útiles si prueba de carga de hello incluye varios escenarios.

Vea [analizar cargar resultados de pruebas en la vista gráficos del analizador de prueba de carga de Hola Hola](https://www.visualstudio.com/load-testing.aspx) para obtener más información acerca de cómo ver la carga de resultados de pruebas.

## <a name="automate-your-load-test"></a>Automatización de la prueba de carga
Visual Studio Team Services carga Test proporciona las API toohelp administrar pruebas de carga y analizar los resultados en una cuenta de Team Services. Consulte [Las API de REST de las pruebas de carga en la nube](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
* [Supervisión y diagnóstico de servicios en una configuración de desarrollo de máquina local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
