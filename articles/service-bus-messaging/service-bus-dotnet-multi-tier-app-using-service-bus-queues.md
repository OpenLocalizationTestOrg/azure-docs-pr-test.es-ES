---
title: "aplicación de varios niveles de aaa.NET uso del Bus de servicio de Azure | Documentos de Microsoft"
description: "Un tutorial de .NET que ayuda a desarrollar una aplicación de varios nivel en Azure que usa toocommunicate de colas de Bus de servicio entre las capas."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>Aplicación de niveles múltiples .NET con colas del Bus de servicio de Azure
## <a name="introduction"></a>Introducción
Desarrollar para Microsoft Azure es fácil con Visual Studio y Hola libre Azure SDK para. NET. Este tutorial le guía a través de hello pasos toocreate una aplicación que usa varios recursos de Azure ejecutando en su entorno local.

Aprenderá siguiente hello:

* Cómo tooenable el equipo de desarrollo de Azure con una sola descargar e instalar.
* Cómo toouse toodevelop de Visual Studio para Azure.
* ¿Cómo toocreate una aplicación de varios niveles en Azure con roles web y de trabajo.
* Cómo toocommunicate entre niveles de uso de colas de Bus de servicio.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

En este tutorial podrá crear y ejecutar la aplicación de varios niveles de hello en un servicio de nube de Azure. Hola front-end es un rol web de ASP.NET MVC y back-end de hello es un rol de trabajo que utiliza una cola de Bus de servicio. Puede crear Hola la misma aplicación de varios nivel con front-end de Hola como un proyecto web, que está implementado tooan sitio Web de Azure en lugar de un servicio de nube. También puede probar hello [aplicación de .NET en local y la nube híbrida](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.

Hello siguiente captura de pantalla muestra aplicación hello completado.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Información general del escenario: comunicación entre roles
toosubmit un pedido para el procesamiento, el componente interfaz de usuario de hello front-end, ejecuta en rol de hello web, debe interactuar con la lógica de nivel intermedio de hello ejecuta en rol de trabajo de Hola. Este ejemplo utiliza la mensajería de Bus de servicio para la comunicación de hello entre las capas de Hola.

Uso del Bus de servicio de mensajería entre los niveles intermedios y web Hola desacopla los dos componentes. En cambio toodirect mensajería (es decir, TCP o HTTP), Hola nivel web no conecta nivel intermedio toohello directamente; en su lugar inserta unidades de trabajo, como mensajes, en el Bus de servicio, que se mantiene hasta que el nivel intermedio de hello es tooconsume listo y procesarlos de forma confiable.

Bus de servicio proporciona dos entidades toosupport asíncrona mensajería: colas y temas. Con las colas, cada mensaje enviado toohello cola es utilizado por un único receptor. Temas de admiten el patrón de publicación/suscripción de hello en el que cada mensaje publicado se pone tooa disponibles las suscripciones registradas con el tema de Hola. Cada suscripción mantiene lógicamente su propia cola de mensajes. Las suscripciones también pueden configurarse con reglas de filtro que restringen el conjunto de Hola de mensajes que se pasan a toothose de cola de suscripción de Hola que coinciden con el filtro de Hola. Hello en el ejemplo siguiente se utiliza colas de Service Bus.

![][1]

Este mecanismo de comunicación tiene varias ventajas sobre la mensajería directa:

* **Desacoplamiento temporal.** Con el patrón de mensajería asincrónica de hello, los productores y consumidores no necesitan ser en línea en hello mismo tiempo. Bus de servicio almacena de forma confiable los mensajes hasta que esté preparada para recibirlos, parte consumidora Hola. Esto permite a los componentes de Hola de toobe de aplicación Hola distribuido desconectados, ya sea voluntariamente, por ejemplo, para mantenimiento o debido a un bloqueo del componente tooa, sin afectar a todo el sistema. Además, Hola consumiendo aplicación solo necesita toocome en línea durante determinadas horas del día de Hola.
* **Redistribución de la carga.** En muchas aplicaciones, la carga del sistema cambia con el tiempo, mientras el tiempo de procesamiento de hello necesario para cada unidad de trabajo es normalmente constante. Intermediar de mensaje de productores y consumidores con una cola significa que Hola consumiendo toobe de necesidades de aplicación (trabajo hello) solo aprovisionado carga media de tooaccommodate en lugar de carga máxima. profundidad de Hola de cola de hello aumenta y disminuye medida que varía la carga entrante Hola. Esto directamente ahorra dinero en cuanto a la cantidad de Hola de carga de aplicaciones de infraestructura necesario tooservice Hola.
* **Equilibrio de carga.** Conforme aumenta la carga, más procesos de trabajo se pueden agregar tooread de cola de Hola. Cada mensaje se procesa solamente mediante uno de los procesos de trabajo de Hola. Además, este equilibrio de carga basados en extracción permite un uso óptimo de los equipos de trabajo de hello incluso si los equipos de trabajo difieren en cuanto a capacidad de procesamiento, ya que extraerán mensajes a su propia velocidad máxima. Este patrón se denomina a menudo hello *consumidor en competencia* patrón.
  
  ![][2]

Hola las secciones siguientes tratan sobre código de hello que implementa esta arquitectura.

## <a name="set-up-hello-development-environment"></a>Configurar el entorno de desarrollo de Hola
Antes de empezar a desarrollar aplicaciones de Azure, obtener herramientas de Hola y configurar el entorno de desarrollo.

1. Instalar hello Azure SDK para .NET de hello SDK [página de descargas](https://azure.microsoft.com/downloads/).
2. Hola **.NET** columna, haga clic en la versión de Hola de [Visual Studio](http://www.visualstudio.com) que usa. Hola los pasos de este tutorial, use Visual Studio 2015, pero también funcionan con Visual Studio de 2017.
3. Cuando se le pida toorun o guardar el instalador de hello, haga clic en **ejecutar**.
4. Hola **instalador de plataforma Web**, haga clic en **instalar** y continuar con la instalación de Hola.
5. Una vez completada la instalación de hello, tendrá todo lo necesario toostart toodevelop Hola aplicación. Hola SDK incluye herramientas que le permiten desarrollar fácilmente aplicaciones de Azure en Visual Studio.

## <a name="create-a-namespace"></a>Creación de un espacio de nombres
Hola siguiente paso es toocreate un espacio de nombres de servicio y obtener una clave de firma de acceso compartido (SAS). Un espacio de nombres proporciona un límite de aplicación para cada aplicación que se expone a través del Bus de servicio. Cuando se crea un espacio de nombres, se genera una clave SAS sistema Hola. combinación de Hola de espacio de nombres y la clave SAS proporciona credenciales de Hola para aplicación de Bus de servicio tooauthenticate acceso tooan.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Creación de un rol web
En esta sección, creará front-end de saludo de la aplicación. En primer lugar, cree páginas de Hola que muestra la aplicación.
A continuación, agregue código que envía la cola de Bus de servicio tooa los elementos y se muestra información de estado acerca de la cola de Hola.

### <a name="create-hello-project"></a>Crear proyecto de Hola
1. Con privilegios de administrador, inicie Visual Studio: Hola contextual **Visual Studio** icono del programa y, a continuación, haga clic en **ejecutar como administrador**. emulador de proceso de Azure de Hello, descrito más adelante en este artículo, requiere que se puede iniciar Visual Studio con privilegios de administrador.
   
   En Visual Studio, en hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
2. En **Plantillas instaladas**, en **Visual C#**, haga clic en **Nube** y, a continuación, en **Azure Cloud Service**. Proyecto de hello Name **MultiTierApp**. y, a continuación, haga clic en **Aceptar**.
   
   ![][9]
3. En los roles de **.NET Framework 4.5**, haga doble clic en **Rol web de ASP.NET**.
   
   ![][10]
4. Mantenga el mouse sobre **WebRole1** en **solución de servicio de nube de Azure**, haga clic en el icono de lápiz hello y cambiar el nombre de rol web de hello demasiado**FrontendWebRole**. y, a continuación, haga clic en **Aceptar**. (Asegúrese de que escribe "Frontend" con "e" minúscula, no "FrontEnd").
   
   ![][11]
5. De hello **nuevo proyecto ASP.NET** cuadro de diálogo hello **seleccione una plantilla de** lista, haga clic en **MVC**.
   
   ![][12]
6. Aún en hello **nuevo proyecto ASP.NET** diálogo cuadro, haga clic en hello **Cambiar autenticación** botón. Hola **Cambiar autenticación** cuadro de diálogo, haga clic en **sin autenticación**y, a continuación, haga clic en **Aceptar**. En este tutorial, va a implementar una aplicación que no necesita un inicio de sesión de usuario.
   
    ![][16]
7. Nuevo en hello **nuevo proyecto ASP.NET** cuadro de diálogo, haga clic en **Aceptar** proyecto de hello toocreate.
8. En **el Explorador de soluciones**, Hola **FrontendWebRole** proyecto de equipo y haga clic en **referencias**, a continuación, haga clic en **administrar paquetes de NuGet**.
9. Haga clic en hello **examinar** y, después, busque `Microsoft Azure Service Bus`. Seleccione hello **WindowsAzure.ServiceBus** del paquete, haga clic en **instalar**y acepte los términos de Hola de uso.
   
   ![][13]
   
   Tenga en cuenta que Hola ahora ensamblados de cliente al que se hace referencia y se han agregado algunos nuevos archivos de código.
10. En el **Explorador de soluciones**, haga clic con el botón derecho en **Modelos** y, luego, en **Agregar** y, por último, en **Clase**. Hola **nombre** cuadro, escriba un nombre hello **OnlineOrder.cs**. A continuación, haga clic en **Agregar**.

### <a name="write-hello-code-for-your-web-role"></a>Escribir código de hello para el rol web
En esta sección, creará Hola distintas páginas que muestra la aplicación.

1. En el archivo de OnlineOrder.cs hello en Visual Studio, reemplace la definición de espacio de nombres existente con el siguiente código de hello:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**. Agregue Hola siguiente **con** las instrucciones en la parte superior de Hola de hello tooinclude Hola espacios de nombres para el modelo que acaba de crear, así como de Bus de servicio de archivos.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. También en el archivo HomeController.cs de hello en Visual Studio, reemplace la definición de espacio de nombres existente con el siguiente código de hello. Este código contiene métodos para controlar la presentación de Hola de cola de toohello los elementos.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. De hello **generar** menú, haga clic en **generar solución** precisión de hello tootest de su trabajo hasta ahora.
5. Ahora, crear vista de Hola para hello `Submit()` método que creó anteriormente. Haga clic en hello `Submit()` método (sobrecarga Hola de `Submit()` que no toma ningún parámetro) y, a continuación, elija **agregar vista**.
   
   ![][14]
6. Aparece un cuadro de diálogo para crear vista Hola. Hola **plantilla** elija **crear**. Hola **clase modelo** lista, haga clic en hello **OnlineOrder** clase.
   
   ![][15]
7. Haga clic en **Agregar**.
8. Ahora, cambie el nombre hello muestra de la aplicación. En **el Explorador de soluciones**, haga doble clic en el **Views\Shared\\_Layout.cshtml** tooopen de archivos en el editor de Visual Studio Hola.
9. Reemplace todas las apariciones de **My ASP.NET Application** por **Productos de LITWARE**.
10. Quitar hello **inicio**, **sobre**, y **póngase en contacto con** vínculos. Eliminar código de hello resaltado:
    
    ![][28]
11. Por último, modifique Hola envío página tooinclude cierta información acerca de la cola de Hola. En **el Explorador de soluciones**, haga doble clic en el **Views\Home\Submit.cshtml** tooopen de archivos en el editor de Visual Studio Hola. Hola después de línea después de agregar `<h2>Submit</h2>`. Por ahora, Hola `ViewBag.MessageCount` está vacía. Lo rellenará más adelante.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. Acaba de implementar su interfaz de usuario. Puede presionar **F5** toorun la aplicación y confirme que lo haga según lo previsto.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Escribir código de hello para el envío de cola de Bus de servicio tooa los elementos
Ahora, agregue código para el envío de cola de tooa los elementos. En primer lugar, va a crear una clase que contiene la información de conexión a la cola del Bus de servicio. A continuación, inicialice la conexión en Global.aspx.cs. Por último, actualizar código de envío de Hola que creó anteriormente en la cola de Bus de servicio de tooa de HomeController.cs tooactually enviar elementos.

1. En **el Explorador de soluciones**, haga clic en **FrontendWebRole** (proyecto de Hola de menú contextual, no Hola rol). Haga clic en **Agregar** y, a continuación, en **Clase**.
2. Nombre de la clase hello **QueueConnector.cs**. Haga clic en **agregar** clase de hello toocreate.
3. Ahora, agregue código que encapsula la información de conexión de hello e inicializa la cola de Bus de servicio de hello conexión tooa. Reemplace Hola todo contenido de QueueConnector.cs con el siguiente código de hello y especifique los valores de `your Service Bus namespace` (el nombre de espacio de nombres) y `yourKey`, que es hello **clave principal** ha obtenido anteriormente de hello Azure Portal.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Ahora, asegúrese de que se llama al método **Initialize**. En el **Explorador de soluciones**, haga doble clic en **Global.asax\Global.asax.cs**.
5. Agregar Hola después de la línea de código al final de Hola de hello **Application_Start** método.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Por último, actualizar código de hello web que creó anteriormente, para enviar elementos toohello cola. En el **Explorador de soluciones**, haga doble clic en **Controllers\HomeController.cs**.
7. Hola de actualización `Submit()` método (sobrecarga de Hola que no toma ningún parámetro) como se indica a continuación tooget Hola número de mensajes para la cola de Hola.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Hola de actualización `Submit(OnlineOrder order)` método (sobrecarga de Hola que toma un parámetro) como se indica a continuación toosubmit ordenar cola toohello de información.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. Ahora puede ejecutar la aplicación hello nuevo. Cada vez que envíe un pedido, aumenta el número de mensajes de Hola.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Crear rol de trabajo de Hola
Rol de trabajo de Hola que procesa los envíos de orden de hello creará ahora. Este ejemplo utiliza hello **rol de trabajo con cola de Service Bus** plantilla de proyecto de Visual Studio. Ya obtenido credenciales Hola necesario desde el portal de Hola.

1. Asegúrese de que se ha conectado a Visual Studio tooyour cuenta de Azure.
2. En Visual Studio, en **el Explorador de soluciones** haga clic en el **Roles** carpeta bajo hello **MultiTierApp** proyecto.
3. Haga clic en **Agregar** y, a continuación, en **Nuevo proyecto de rol de trabajo**. Hola **Agregar nuevo proyecto de rol** aparece el cuadro de diálogo.
   
   ![][26]
4. Hola **Agregar nuevo proyecto de rol** cuadro de diálogo, haga clic en **rol de trabajo con cola de Service Bus**.
   
   ![][23]
5. Hola **nombre** cuadro, proyecto de hello name **OrderProcessingRole**. A continuación, haga clic en **Agregar**.
6. Copie la cadena de conexión de Hola que obtuvo en el paso 9 del Portapapeles de toohello de sección de Hola "Crear un espacio de nombres de Bus de servicio".
7. En **el Explorador de soluciones**, contextual hello **OrderProcessingRole** que creó en el paso 5 (asegúrese de que haga **OrderProcessingRole** en **Roles**, y no Hola clase). A continuación, haga clic en **Propiedades**.
8. En hello **configuración** ficha de hello **propiedades** cuadro de diálogo, haga clic dentro de hello **valor** cuadro **Microsoft.ServiceBus.ConnectionString**y, a continuación, pegue el valor de punto de conexión de Hola que copió en el paso 6.
   
   ![][25]
9. Crear un **OnlineOrder** clase toorepresent Hola pedidos como procesarlos de cola de Hola. Puede reutilizar una clase que ya ha creado. En **el Explorador de soluciones**, contextual hello **OrderProcessingRole** clase (icono de clase de Hola de menú contextual, no Hola rol). Haga clic en **Agregar** y, a continuación, en **Elemento existente**.
10. Busque la subcarpeta toohello para **FrontendWebRole\Models**y, a continuación, haga doble clic en **OnlineOrder.cs** tooadd se toothis proyecto.
11. En **WorkerRole.cs**, cambiar el valor Hola de hello **QueueName** variables de `"ProcessingQueue"` demasiado`"OrdersQueue"` tal y como se muestra en el siguiente código de hello.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Agregue los siguiente Hola using instrucción Hola principio del archivo WorkerRole.cs de Hola.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. Hola `Run()` función dentro de hello `OnMessage()` llamar a, reemplace el contenido de Hola de hello `try` cláusula con el siguiente código de hello.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. Ha completado la aplicación hello. Puede probar la aplicación completa de hello haciendo clic en proyecto de MultiTierApp hello en el Explorador de soluciones, seleccione **establecer como proyecto de inicio**y, a continuación, presione la tecla F5. Tenga en cuenta que el número de mensajes no se incrementa, porque el rol de trabajo de hello procesa elementos de cola de Hola y las marca como completa. Puede ver los resultados de seguimiento de Hola de su rol de trabajo mediante la visualización Hola IU del emulador de proceso de Azure. Puede hacerlo haciendo clic en el icono del emulador Hola Hola área de notificación de la barra de tareas y seleccionando **Mostrar IU del emulador de proceso**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Pasos siguientes
toolearn más información acerca de Bus de servicio, vea Hola recursos siguientes:  

* [Documentación de Azure Service Bus][sbdocs]  
* [Página de servicio de Service Bus][sbacom]  
* [¿Cómo tooUse colas de Service Bus][sbacomqhowto]  

toolearn más información acerca de los escenarios de varios niveles, vea:  

* [Aplicación de niveles múltiples .NET mediante tablas, colas y blobs de Storage][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36
