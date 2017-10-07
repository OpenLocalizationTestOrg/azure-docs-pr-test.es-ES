---
title: la entrega aaaContinuous con Visual Studio Team Services en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooconfigure su Visual Studio Team Services proyectos de equipo de tooautomatically compilar e implementar la característica de la aplicación Web de toohello en los servicios en la nube o de servicio de aplicaciones de Azure."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>TooAzure la entrega continua con Visual Studio Team Services
Puede configurar la compilación de tooautomatically de proyectos de equipo de Visual Studio Team Services e implementar tooAzure las aplicaciones web o servicios en la nube.  (Para obtener información acerca de cómo tooset una copia de seguridad continuada de compilación e implementar el sistema mediante un *local* Team Foundation Server, vea [la entrega continua de los servicios de nube de Azure](cloud-services-dotnet-continuous-delivery.md).)

Este tutorial se supone que Visual Studio 2013 y hello Azure SDK instalado. Si ya no tiene Visual Studio 2013, descárguelo eligiendo hello **empiece de forma gratuita** vincular en [www.visualstudio.com](http://www.visualstudio.com). Instalación hello Azure SDK desde [aquí](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Necesita un toocomplete de cuenta de Visual Studio Team Services este tutorial: puede [abrir una cuenta de Visual Studio Team Services gratis](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset seguridad un tooautomatically de servicio de nube compilar e implementar tooAzure mediante el uso de Visual Studio Team Services, siga estos pasos.

## <a name="1-create-a-team-project"></a>1: Creación de un proyecto de equipo
Siga las instrucciones de hello [aquí](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate su equipo de proyecto y vincúlela tooVisual Studio. En este tutorial se supone que usa Team Foundation Version Control (TFVC) como solución de control de código fuente. Si desea toouse Git para el control de versiones, vea [versión de Git Hola de este tutorial](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2: comprobar en un control de toosource de proyecto
1. En Visual Studio, abra solución de hello desea toodeploy, o cree uno nuevo.
   Puede implementar una aplicación web o un servicio de nube (aplicación de Azure) por hello siguiente los pasos de este tutorial.
   Si desea toocreate una nueva solución, cree un nuevo proyecto de servicio de nube de Azure o un nuevo proyecto de MVC de ASP.NET. Asegúrese de que Hola proyecto tiene como destino .NET Framework 4 o 4.5 y si va a crear un proyecto de servicio de nube, agregue un rol web de ASP.NET MVC y un rol de trabajo y elija la aplicación de Internet para el rol web de Hola. Cuando se le solicite, elija **Aplicación de Internet**.
   Si desea toocreate una aplicación web, elija la plantilla de proyecto de aplicación Web ASP.NET de hello y, a continuación, elija MVC. Consulte [Crear una aplicación web de ASP.NET en Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Actualmente, Visual Studio Team Services solo admite las implementaciones de integración continua de las aplicaciones web de Visual Studio. Los proyectos de sitio web están fuera del alcance.
   > 
   > 
2. Abra el menú contextual de hello para la solución de Hola y elija **Agregar solución tooSource Control**.
   
    ![][5]
3. Aceptar o cambiar los valores predeterminados de Hola y elija hello **Aceptar** botón. Una vez completado el proceso de hello, iconos de control de código fuente aparecen en **el Explorador de soluciones**.
   
    ![][6]
4. Abra el acceso directo de hello para la solución de Hola y elija **proteger**.
   
    ![][7]
5. Hola **cambios pendientes** área no cliente de **Team Explorer**, escriba un comentario para en el repositorio de Hola y elija hello **proteger** botón.
   
    ![][8]
   
    Tenga en cuenta tooinclude de opciones de Hola o excluir cambios específicos cuando protegen. Si se desea se excluyen los cambios, elija hello **incluir todo** vínculo.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3: conectar Hola proyecto tooAzure
1. Ahora que tiene un proyecto de equipo de VS Team Services con algún código de origen en él, está listo tooconnect tooAzure del proyecto de su equipo.  Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), seleccione la aplicación web o servicio de nube, o cree uno nuevo eligiendo hello  **+**  situado en la inferior izquierda de Hola y elegir **deserviciodenube** o **aplicación Web** y, a continuación, **creación rápida**. Elija hello **configurar la publicación con Visual Studio Team Services** vínculo.
   
    ![][10]
2. En el Asistente de hello, escriba el nombre de saludo de la cuenta de Visual Studio Team Services en el cuadro de texto de Hola y haga clic en hello **autorizar ahora** vínculo. Toosign en que se le pida.
   
    ![][11]
3. Hola **solicitud de conexión** cuadro de diálogo emergente, elija hello **Accept** botón tooauthorize Azure tooconfigure su equipo de proyecto de VS Team Services.
   
    ![][12]
4. Si la autorización se realiza correctamente, verá una lista desplegable que contiene los proyectos de equipo de Visual Studio Team Services. Elegir nombre de hello del proyecto de equipo que creó en los pasos anteriores de hello y, a continuación, elija el botón de marca de verificación del Asistente de Hola.
   
    ![][13]
5. Después de su proyecto está vinculado, verá algunas instrucciones para comprobar en el proyecto de equipo de Visual Studio Team Services tooyour de cambios.  En la siguiente comprobación, Visual Studio Team Services compilará e implementará el proyecto tooAzure.  Pruebe esto ahora haciendo clic en hello **insertar en el repositorio de Visual Studio** vincular y, a continuación, Hola **iniciar Visual Studio** vínculo (o hello equivalente **Visual Studio** situado en la parte inferior de Hola de pantalla de bienvenida portal).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4: Desencadenamiento de una recompilación y nueva implementación del proyecto
1. En Visual Studio **Team Explorer**, elija hello **Explorador de Control de código fuente** vínculo.
   
    ![][15]
2. Navegar por el archivo de solución tooyour y ábralo.
   
    ![][16]
3. En el **Explorador de soluciones**, abra un archivo y cámbielo. Por ejemplo, cambie el archivo hello `_Layout.cshtml` en vistas de hello\\carpeta compartida en un rol web MVC.
   
    ![][17]
4. Editar logotipo de hello para el sitio de Hola y elija **CTRL+s** archivo de hello toosave.
   
    ![][18]
5. En **Team Explorer**, elija hello **cambios pendientes** vínculo.
   
    ![][19]
6. Escriba un comentario y, a continuación, elija hello **proteger** botón.
   
    ![][20]
7. Elija hello **principal** botón tooreturn toohello **Team Explorer** página principal.
   
    ![][21]
8. Elija hello **compilaciones** hello tooview de vínculo se basa en curso.
   
    ![][22]
   
    **Team Explorer** indica que se ha desencadenado una compilación para su protección.
   
    ![][23]
9. A medida que progresa de compilación de hello, haga doble clic en el nombre de Hola de compilación de hello en curso tooview un registro detallado.
   
    ![][24]
10. Mientras compilación Hola está en curso, eche un vistazo en la definición de compilación de Hola que se creó si vincula TFS tooAzure mediante el Asistente de Hola.  Abra el menú contextual de Hola de definición de compilación de Hola y elija **Editar definición de compilación**.
    
     ![][25]
    
     Hola **desencadenador** pestaña, verá que definición de compilación de hello está activada toobuild de cada protección de forma predeterminada.
    
     ![][26]
    
     Hola **proceso** ficha, puede ver el entorno de implementación de Hola se establece toohello nombre de la aplicación web o servicio de nube. Si está trabajando con las aplicaciones web, propiedades de hello que verá será diferentes de los mostrados aquí.
    
     ![][27]
11. Si quiere que los valores diferentes a los valores predeterminados de hello, especifique valores para propiedades de Hola. Hello propiedades para la publicación de Azure están en hello **implementación** sección.
    
     Hello tabla siguiente muestran las propiedades disponibles Hola Hola **implementación** sección:
    
    | Propiedad | Valor predeterminado |
    | --- | --- |
    | Permitir certificados que no son de confianza |Si el valor es false, los certificados SSL deben estar firmados por una entidad de certificación raíz. |
    | Permitir actualización |Permite Hola implementación tooupdate una implementación existente en lugar de crear uno nuevo. Conserva la dirección IP de Hola. |
    | No eliminar |Si el valor es true, no sobrescriba una implementación no relacionada existente (la actualización está permitida). |
    | Ruta de acceso tooDeployment configuración |Hola ruta tooyour .pubxml archivo para una aplicación web, toohello relativa de carpeta de raíz del repositorio de Hola. Se ignora para los servicios en la nube. |
    | Entorno de implementación de SharePoint |Hola igual que el nombre del servicio de Hola. |
    | Entorno de implementación de Azure |Hola aplicación o en la nube nombre de servicio web. |
12. Si utiliza varias configuraciones del servicio (archivos .cscfg), puede especificar configuración de servicios deseada de hello en hello **argumentos de compilación, opciones avanzadas, MSBuild** configuración. Por ejemplo, toouse ServiceConfiguration.Test.cscfg, establezca los argumentos de MSBuild opción de línea de `/p:TargetProfile=Test`.
    
     ![][38]
    
     Llegados a este punto, la compilación debería haber finalizado correctamente.
    
     ![][28]
13. Si hace doble clic en nombre de la compilación de hello, Visual Studio muestra un **resumen de la compilación**, incluidos los resultados de pruebas de asociados proyectos de prueba unitaria.
    
     ![][29]
14. Hola [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885), puede ver implementación Hola asociado en hello **implementaciones** pestaña cuando se selecciona Hola entorno de ensayo.
    
     ![][30]
15. Examinar dirección URL del sitio tooyour. Para una aplicación web, simplemente haga clic en hello **examinar** botón de barra de comandos de Hola. Para un servicio de nube, elija dirección URL de Hola Hola **vista rápida** sección de hello **panel** página que muestra el entorno de ensayo de Hola para un servicio de nube. Las implementaciones de integración continua para servicios en la nube están publicados toohello el entorno de ensayo de forma predeterminada. Puede cambiar esta configuración hello **entorno del servicio de nube alternativo** propiedad demasiado**producción**. Esta captura de pantalla muestra dónde hello que dirección URL del sitio se encuentra en la página del panel del servicio de hello en la nube.
    
    ![][31]
    
    Una nueva pestaña de explorador abrirá el sitio de la ejecución de tooreveal.
    
    ![][32]
    
    Para los servicios de nube, si realiza otro proyecto de tooyour de cambios, el desencadenador se más genera y se acumularán varias implementaciones. Hello más reciente marca como activo.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5: Nueva implementación de una compilación anterior
Este paso es opcional y aplica a los servicios de toocloud. En Hola portal de Azure clásico, elija una implementación anterior y, a continuación, elija hello **volver a implementar** botón toorewind su tooan de sitio anteriormente en el repositorio.  Tenga en cuenta que esto desencadenará una nueva compilación en TFS y creará una nueva entrada en el historial de implementaciones.

![][34]

## <a name="6-change-hello-production-deployment"></a>6: cambiar la implementación de producción de hello
Este paso aplica solo toocloud servicios, no a las aplicaciones web. Cuando esté listo, puede promover Hola ensayo toohello entorno de producción eligiendo hello **intercambiar** botón Hola portal de Azure clásico. entorno de ensayo de Hello recién implementado es tooProduction promocionada y entorno de producción de hello anterior, si existe, se convierte en un entorno de ensayo. Hola implementación activa puede ser diferente para entornos de ensayo y producción de hello, pero el historial de implementación de Hola de compilaciones recientes es Hola igual independientemente del entorno.

![][35]

## <a name="7-run-unit-tests"></a>7: Ejecución de pruebas unitarias
Este paso aplica solo las aplicaciones de tooweb, no los servicios en la nube. tooput calidad es satisfactoria de su implementación, puede ejecutar pruebas unitarias y si produce un error, puede detener la implementación de Hola.

1. En Visual Studio, agregue un proyecto de prueba unitaria.
   
   ![][39]
2. Agregar proyecto de toohello de referencias de proyecto que desee tootest.
   
   ![][40]
3. Agregue algunas pruebas unitarias. tooget iniciado, intente una prueba ficticia que pasará siempre.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Editar definición de compilación de hello, elija hello **proceso** pestaña y expanda hello **prueba** nodo.
5. Conjunto hello **producirá un error compilación en caso de error de prueba** tooTrue. Esto significa que no produjo la implementación de Hola a menos que superan las pruebas Hola.
   
   ![][41]
6. Ponga en cola una nueva compilación.
   
   ![][42]
   
   ![][43]
7. Mientras se desarrolla la compilación de hello, comprobar su progreso.
   
    ![][44]
   
    ![][45]
8. Cuando se realiza la compilación de hello, compruebe los resultados de pruebas de Hola.
   
    ![][46]
   
    ![][47]
9. Pruebe a crear una prueba que provoque un error. Agregar una nueva prueba copiando Hola primero, cámbiele el nombre y comente la línea de saludo de código que indica que NotImplementedException es una excepción esperada.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Comprobación de hello cambiar tooqueue una nueva compilación.
    
     ![][48]
11. Ver detalles de toosee de resultados de pruebas de hello sobre los errores de Hola.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre las pruebas unitarias en Visual Studio Team Services, consulte [Ejecución de pruebas unitarias en una compilación](http://go.microsoft.com/fwlink/p/?LinkId=510474). Si usa Git, vea [compartir su código de Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) y [tooAzure servicio de aplicaciones de la implementación continua](../app-service-web/app-service-continuous-deployment.md).  Para obtener más información sobre Visual Studio Team Services, consulte [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
