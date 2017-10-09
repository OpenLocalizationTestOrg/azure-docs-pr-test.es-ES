---
title: 'Tutorial: DevOps con hello Portal de Azure | Documentos de Microsoft'
description: "Obtenga información acerca de Hola distintos flujos de trabajo de DevOps Hola Portal de Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Tutorial: DevOps con hello Portal de Azure
Hola plataforma Windows Azure está lleno de flujos de trabajo de DevOps flexibles. En este tutorial, aprenderá cómo las capacidades de hello tooleverage de hello toodevelop del Portal de Azure, probar, implementar, solucionar problemas, supervisar y administrar aplicaciones en ejecución. Este tutorial se centra en los siguientes hello:

1. Creación de una aplicación web y habilitación de la implementación continua
2. Desarrollo y prueba de una aplicación
3. Supervisión y solución de problemas de una aplicación
4. Tareas generales de administración de aplicaciones

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Creación de una aplicación web y habilitación de la implementación continua
Crear una aplicación Web con [servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/), que se usará en el resto de Hola de este tutorial. Inicialmente, deberá habilitar la implementación continua desde el repositorio de código fuente en nuestro entorno de ejecución de Azure.

1. Hola de inicio de sesión en el Portal de Azure
2. Elija **servicios de aplicaciones** &gt; **icono Agregar** y escriba un nombre, elija su suscripción y crear un nuevo tooserve de grupo de recursos como contenedor de hello para el servicio de Hola.
   
   Los grupos de recursos permiten toomanage distintos aspectos de solución de hello como la facturación, implementaciones y supervisión todos como un único grupo a través de [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![imagen1][image1]
3. Transcurridos unos segundos,el Servicio de aplicaciones se ha creado. Tomar Hola de tooexplore de unos minutos diversas opciones de menú para un servicio hello en el portal de Hola.
   
   ![imagen2][image2]    
4. Haga clic en la dirección URL de Hola. Tenga en cuenta diversos Hola opciones disponibles para las herramientas y repositorios. También puede utilizar lenguajes de Hola y marcos de su elección como. NET, Java y Ruby.
   
   ![imagen3][image3]    
5. Hola portal de Azure hace que la implementación continua un proceso sencillo que implica unos pocos pasos sencillos. Hola portal de Azure, elija Configuración en el icono de hello para el servicio de aplicaciones de Hola que acaba de crear.
   
   ![imagen4][image4]
   
   De hoja de Hola que se abre en hello derecho, desplácese toohello sección de la publicación.
   
   ![imagen5][image5]
6. A continuación, configure algunas implementación continua de tooenable de configuración para la aplicación hello. Haga clic en el origen de la implementación y haga clic en Elegir origen. Tenga en cuenta diversos Hola de opciones disponibles para los orígenes del repositorio.
   
   ![imagen6][image6]
7. En este ejemplo, elija GitHub. Opcionalmente, elija repositorio Hola de su elección y configurar las credenciales de autorización de Hola.
   
   ![imagen7][image7]
8. Después de repositorio de tooyour de autorización, a continuación, puede elegir un proyecto y una rama que se va toodeploy. Hay varios ejemplos ficticios que se enumeran a continuación.
   
   ![imagen8][image8]
9. Una vez elegido el proyecto y la rama, haga clic en Aceptar. Debe iniciar las notificaciones de toosee de una implementación.
   
   ![imagen9][image9]
10. Navegue tooGitHub atrás toosee hello webhook al que se ha creado el repositorio de control de código fuente de hello toointegrate con Azure. Hola Portal de Azure habilita la integración con GitHub con solo unos pocos pasos sencillos.
    
    ![imagen10][image10]
11. toodemonstrate implementación continua, agregar rápidamente algunos repositorio toohello contenido. Para obtener un ejemplo simple, agregue un repositorio de GitHub ejemplo tooa de archivo de texto. Son .NET toouse libre, Ruby, Python o algún otro tipo de aplicación con el servicio de aplicaciones. Cree tooadd disponible un archivo de texto, repositorio de toohello de aplicación de MVC de ASP.NET, Java o Ruby de su elección.
    
    ![imagen11][image11]
12. Después de confirmar el repositorio de tooyour de cambios, verá una nueva implementación se inician en el área de notificaciones de portal de Hola. Si no ve rápidamente cambios después de confirmar tooyour repositorio, haga clic en sincronizar.
    
    ![imagen12][image12]
13. En este momento, si intenta cargar página hello para el servicio de aplicaciones de hello, recibirá un error 403. En este ejemplo, es porque no hay ninguna configuración de documento predeterminado para la página de Hola como un archivo como index.htm o default.html. Puede resolverlo rápidamente con hello tooling Hola Portal de Azure.  Hola Portal de Azure, elija configuración &gt; configuración de la aplicación.
    
     ![imagen13][image13]
14. Se abre una hoja de configuración de la aplicación. Escriba el nombre de Hola de página Hola "SamplePage.html" y haga clic en Guardar. Tienen otras configuraciones de Hola de tooexplore de unos minutos.
    
    ![imagen14][image14]
15. Opcionalmente, actualice su tooensure de dirección URL de explorador se verán los cambios de hello espera. En este caso, hay algunos textos ahora rellenar página Hola. Cada repositorio de toohello cambios adicionales se crearán una nueva implementación automática.
    
    ![imagen15][image15]
    
    Habilitar la implementación continua con hello Portal de Azure es una experiencia sencilla. También puede crear canalizaciones de versión más complejas y usar muchas otras técnicas con control de código fuente existente y tooAzure de toodeploy de sistemas de integración continua, como utilizar la compilación automatizada y sistemas de administración de versión.

## <a name="develop-and-test-an-app"></a>Desarrollo y prueba de una aplicación
A continuación, modificar algunos toohello código base e implementar rápidamente los cambios. También configurará el rendimiento de algunas pruebas para la aplicación Web de Hola.

1. Hola Portal de Azure elija Servicios de aplicaciones de panel de navegación de Hola y busque el servicio de aplicaciones.
   
   ![imagen16][image16]
2. Haga clic en Herramientas.
   
   ![imagen17][image17]
3. Tenga en cuenta Hola categoría en herramientas de desarrollo. Hay varias herramientas útiles aquí que nos permiten toowork con aplicaciones sin salir de hello Portal de Azure. Haga clic en Consola.
   
   ![imagen18][image18]
4. En la ventana de la consola de hello, puede emitir comandos en vivo de la aplicación. Comando dir de tipo hello y presione ENTRAR. Observe que los comandos que requieren privilegios elevados no funcionan.
   
   ![imagen19][image19]
5. Retroceder toohello desarrollar categoría y elija Visual Studio Online. Nota: Visual Studio Online ahora se llama Visual Studio Team Services.
   
   ![imagen20][image20]
6. Alternar en la experiencia de edición de hello en el Explorador de la aplicación.
   
   ![imagen21][image21]
7. Se instala una extensión web para la aplicación. Extensiones de forma rápida y sencilla agregan funcionalidad tooapps en Azure. Tenga en cuenta algunas de hello otros tipos de extensiones disponibles en la siguiente captura de pantalla de Hola.
   
   ![imagen22][image22]
8. Una vez que instala Hola extensión de Visual Studio Online, haga clic en Ir.
   
   ![imagen23][image23]
9. Un explorador pestaña abre donde verá un desarrollo IDE directamente en el Explorador de Hola. Experiencia de hello aviso siguiente está en Chrome.
   
   ![imagen24][image24]
10. Puede realizar varias actividades, como editar archivos, agregar archivos y carpetas y descargar el contenido del sitio de hello en vivo. Cree un archivo de SamplePage.html toohello de edición rápida.
    
    ![imagen25][image25]
11. En unos instantes, cambios de Hola se guardan automáticamente. Si navega toohello back-página, puede ver los cambios de Hola. Tenga en cuenta que es muy posible que las modificaciones dinámicas como estas no sean adecuadas para entornos de producción. No obstante, herramientas de Hola hacerla toomake muy fácil cambios rápidos para desarrollo y entornos de prueba.
    
    ![imagen26][image26]
    
    ![imagen27][image27]
12. Retroceder toohello hoja de herramientas y en la categoría de desarrollar hello, haga clic en prueba de rendimiento.
    
    ![imagen28][image28]
13. Debe tooset una cuenta de servicios del equipo. Consulte aquí para ver más detalles: [Create a Team Services Account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. Haga clic en nuevo toocreate una prueba de rendimiento.
    
    ![imagen29][image29]
    
    Configurar Hola distintos valores y haga clic en Ejecutar prueba final Hola de hello diálogo tooinitiate una prueba de rendimiento.
    
    ![imagen30][image30]
    
    ![imagen31][image31]
15. Una vez que la prueba de hello comienza a ejecutarse, puede supervisar el estado de Hola.
    
    ![imagen32][image32]
    
    Una vez finalizada la prueba de hello, al hacer clic en el resultado de hello muestran más detalles.
    
    ![imagen33][image33]
16. En este ejemplo, se creó una prueba pequeña que se ejecutan, por lo que hay datos limitado tooanalyze, pero se pueden ver varias métricas así como volver a ejecutar la prueba desde esta vista. Hola Portal de Azure permite crear, ejecutar y analizar pruebas de rendimiento web en un proceso sencillo. Hola de capturas de pantalla siguientes muestran datos de rendimiento de Hola.
    
    ![imagen34][image34]
    
    ![imagen35][image35]
    
    ![imagen36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Supervisión y solución de problemas de una aplicación
Azure proporciona muchas funcionalidades de supervisión y solución de problemas de las aplicaciones que se ejecutan.

1. Hola Portal de Azure para nuestra aplicación Web, elija Herramientas.
   
   ![imagen37][image37]
2. En la categoría de solución de problemas de hello, fíjese en hello las distintas opciones de uso de posibles problemas de herramientas tootroubleshoot con una aplicación en ejecución. Puede hacer cosas como supervisar el tráfico HTTP dinámico, habilitar la recuperación automática, ver registros, etc.
   
   ![imagen38][image38]
3. Elegir métricas del sitio tooquickly get en una vista de algunos códigos HTTP.
   
   ![imagen39][image39]
4. Elija Diagnóstico como el Servicio. Elija el tipo de aplicación, a continuación, Ejecutar.
   
   ![imagen40][image40]
   
   Comienza una recopilación.
   
   ![imagen41][image41]
5. Puede elegir toodiagnose posibles problemas de registro adecuado de Hola. Necesita tooenable registro toosee todos los datos disponibles de hello opciones, como los registros de HTTP.
   
   ![imagen42][image42]
   
   Haciendo clic en el archivo de volcado de memoria de hello puede descargar y analizar un DebugDiag toohelp de informe de análisis buscar posibles problemas.
   
   ![imagen43][image43]
6. tooview más datos, necesita tooenable inicio de sesión adicional. Hola Portal de Azure, navegue toohello Web app y elija la configuración.
   
   ![imagen44][image44]
7. Desplácese hacia abajo de la categoría de características de toohello y elija registros de diagnóstico.
   
      ![imagen45][image45]
8. Tenga en cuenta Hola varias opciones para el registro. Active el registro del servidor web y haga clic en Guardar.
   
   ![imagen46][image46]
9. Retroceder toohello área de herramientas para la aplicación hello y elija diagnóstico como un servicio y haga clic en la recopilación de datos de ejecución toorerun Hola.
   
   ![imagen47][image47]
10. Con la configuración del registro de hello HTTP está habilitada, verá ahora los datos recopilados para registros de HTTP.
    
    ![imagen48][image48]
11. Haciendo clic en registro de archivos de hello HTML, generar un informe enriquecido basada en explorador para que lo investiguen.
    
    ![imagen49][image49]
12. Retroceder la sección de herramientas de toohello en hello Portal de Azure para la aplicación hello. Desplácese a la sección de herramientas de toohello y elija Process Explorer.
    
    ![imagen50][image50]
13. Al elegir Explorador de procesos, puede ver detalles sobre los procesos en ejecución. Aviso debajo de usted puede profundizar en los procesos e incluso terminar procesos desde Hola Portal de Azure.
    
    ![imagen51][image51]
    
    ![imagen52][image52]
14. Retroceder toohello hoja de configuración de hello izquierda. Haga clic en Nueva solicitud de soporte técnico.
    
    ![imagen53][image53]
15. De hoja Hola Hola derecho, rellene los detalles sobre los problemas de hello, escriba la información de contacto e incluso cargar datos de diagnóstico. Hola Portal de Azure permite trabajar con el soporte técnico de Microsoft una experiencia sin problemas.
    
    ![imagen54][image54]
    
    ![imagen55][image55]
    
    Hola Portal de Azure ayuda a proporcionar eficaz y familiar tooling experiencias toohelp supervisar y solucionar problemas de nuestras aplicaciones en ejecución. También es capaz de tootake acción rápidamente mediante la realización de tareas, como el reciclaje de procesos, habilitar y deshabilitar diversas colecciones de datos e incluso integrar con soporte técnico profesional de Microsoft.

## <a name="general-application-management"></a>Administración general de aplicaciones
Al administrar las aplicaciones, suelen necesitar tooperform una amplia variedad de actividades como la configuración de las estrategias de copia de seguridad, implementar y administrar proveedores de identidades y cómo configurar el control de acceso basado en roles. Como con hello otras experiencias de DevOps, Hola plataforma Windows Azure estas tareas integra directamente en el portal de Hola.

1. tooensure mantiene Hola aplicación Web protegida de la pérdida de datos necesita las copias de seguridad de tooconfigure. Navegue toohello área de configuración de la aplicación Web.
   
   ![imagen56][image56]
2. En la hoja de hello en hello derecho, desplácese hacia abajo toohello categoría de características.
   
    ![imagen57][image57]
3. Elija las copias de seguridad; se abre una hoja en hello derecho.
   
   ![imagen58][image58]
4. Haga clic en configurar, seleccione una cuenta de almacenamiento de hoja Hola Hola derecho.
   
   ![imagen59][image59]
5. Ahora cree y elija un toohold del contenedor de almacenamiento de las copias de seguridad. Haga clic en crear final Hola de hoja de Hola. A continuación, seleccione el contenedor de Hola.
   
   ![imagen60][image60]
6. Una vez que haya elegido el contenedor de hello, puede configurar programaciones, así como las copias de seguridad el programa de instalación para las bases de datos. En este escenario, haga clic en hello guardar icono.
   
    ![imagen61][image61]
7. Después de guardar, desplácese toohello back-hoja de hello izquierda para copias de seguridad. Haga clic en la aplicación de hello tooback copia de seguridad ahora.
   
    ![imagen62][image62]
8. En unos momentos, verá una copia de seguridad creada. Hola aviso Restaurar ahora una opción en hello captura de pantalla siguiente.
   
    ![imagen63][image63]
9. Haga clic en Restaurar ahora y examine la hoja de toohello opciones de hello en hello derecho. Puede elegir que una copia de seguridad adecuada y sencilla restauración tooan anteriormente estado según sea necesario. Hola portal de Azure nos ha ayudado a habilitar fácilmente una estrategia de recuperación ante desastres simple para la aplicación hello.
   
    ![imagen64][image64]
10. Mover hoja de configuración de toohello de hello izquierda y en las funciones y elija autenticación/autorización.
    
     ![imagen65][image65]
11. En la hoja de hello en hello derecha Seleccione autenticación de servicio de la aplicación. Tenga en cuenta diversos Hola de opciones que puede configurar con los proveedores más conocidos.
    
     ![imagen66][image66]
12. Elegir el proveedor de Hola de su elección y observe las opciones de hello para el ámbito de Hola. Puede proporcionar un Id. de aplicación y el secreto de la aplicación y habilitar rápidamente la autenticación de Facebook para la aplicación hello. Hola Portal de Azure habilita la autenticación como una solución integrada para las aplicaciones.
    
     ![imagen67][image67]
13. Retroceder toohello hoja de configuración y elija los usuarios en la categoría de administración de recursos de Hola.
    
     ![imagen68][image68]
14. En la hoja de hello en hello derecho examinar Hola diversas opciones para agregar roles y usuarios. Hola Portal de Azure le permite controlar fácilmente RBAC (control de acceso basado en roles) para la aplicación hello.
    
     ![imagen69][image69]

## <a name="summary"></a>Resumen
Este tutorial muestra algunos de alimentación de hello con hello plataforma Windows Azure rápidamente lo que permite una implementación continua para una aplicación web, realizar distintos del desarrollo y actividades de prueba, supervisión y solución de problemas de una aplicación activa y finalmente administrar clave estrategias como la recuperación ante desastres, identidad y control de acceso basado en roles. Hola plataforma Windows Azure permite una experiencia integrada para estos flujos de trabajo de DevOps, y también puede trabajar eficazmente mantenerse en el contexto para la tarea de hello en cuestión.

## <a name="next-steps"></a>Pasos siguientes
* Administrador de recursos de Azure es importante para habilitar DevOps en hello plataforma Windows Azure.  toolearn más visitar [Introducción a Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
* toolearn más acerca de la implementación de servicio de aplicaciones de Azure, visite [implementar su aplicación de servicio de aplicación tooAzure](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
