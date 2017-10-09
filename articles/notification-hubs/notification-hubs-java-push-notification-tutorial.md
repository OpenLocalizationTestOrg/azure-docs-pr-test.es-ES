---
title: aaaHow toouse centros de notificaciones con Java
description: "Obtenga información acerca de cómo toouse centros de notificaciones de Azure de un back-end de Java."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 4c3f966d-0158-4a48-b949-9fa3666cb7e4
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: java
ms.devlang: java
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: afcf305b1acd9ee28ee4889040ece59d9399d29d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-notification-hubs-from-java"></a>¿Cómo toouse centros de notificaciones desde Java
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

Este tema describe las principales características de Hola de oficial de Hola de nuevo totalmente compatible SDK de Java de concentrador de notificación de Azure. Se trata de un proyecto de código abierto y también puede ver el código de hello completo SDK en [SDK de Java]. 

En general, se pueden tener acceso a todas las características de los centros de notificaciones de un Java/PHP y Python y Ruby back-end mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx). Este SDK de Java proporciona un contenedor fino de estas interfaces REST en Java. 

Hello SDK admite actualmente:

* CRUD en los Centros de notificaciones 
* CRUD en los registros
* Administración de la instalación
* Importación y exportación de registros
* Envíos regulares
* Envíos programados
* Operaciones asincrónicas mediante Java NIO
* Plataformas admitidas: APNS (iOS), GCM (Android), WNS (aplicaciones de la Tienda Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sin servicios de Google) 

## <a name="sdk-usage"></a>Uso del SDK
### <a name="compile-and-build"></a>Compilación y creación
Uso de [Maven]

toobuild:

    mvn package

## <a name="code"></a>Código
### <a name="notification-hub-cruds"></a>Operaciones CRUD de Centros de notificaciones
**Creación de un administrador de espacio de nombres:**

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

**Creación de un Centro de notificaciones:**

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 OR

    hub = new NotificationHub("connection string", "hubname");

**Obtención del Centro de notificaciones:**

    hub = namespaceManager.getNotificationHub("hubname");

**Actualización del Centro de notificaciones:**

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

**Eliminación del Centro de notificaciones:**

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a>Operaciones CRUD de registro
**Creación de un cliente del Centro de notificaciones:**

    hub = new NotificationHub("connection string", "hubname");

**Creación de un registro de Windows:**

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

**Creación de un registro de iOS:**

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

Del mismo modo puede crear registros para Android (GCM), Windows Phone (MPNS) y Kindle Fire (ADM).

**Creación de registros de plantilla:**

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

**Creación de registros mediante el patrón create registrationid + upsert**

Quita los duplicados debido a las respuestas de tooany perdido si almacenar los Id. de registro en el dispositivo de hello:

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

**Actualización de registros:**

    hub.updateRegistration(reg);

**Eliminación de registros:**

    hub.deleteRegistration(regid);

**Consulta de registros:**

* **Obtención de un único registro:**
  
    hub.getRegistration(regid);
* **Obtención de todos los registros en el centro:**
  
    hub.getRegistrations();
* **Obtención de registros con etiqueta:**
  
    hub.getRegistrationsByTag("miEtiqueta");
* **Obtención de registros por canal:**
  
    hub.getRegistrationsByChannel("tokenDeDispositivo");

Todas las consultas de la colección admiten los tokens $top y continuation.

### <a name="installation-api-usage"></a>Uso de la API de instalación
La API de instalación es un mecanismo alternativo para la administración de registros. En lugar de mantener varios registros que no es trivial y se puede realizar fácilmente mal o de forma ineficaz, ahora es posible toouse un objeto de una sola instalación. La instalación contiene todo lo que necesita: canal de inserción (token del dispositivo), etiquetas, plantillas, iconos secundarios (para WNS y APNS). Ya no necesita toocall Hola servicio tooget Id.: simplemente generar GUID o cualquier otro identificador, mantener en el dispositivo y enviar tooyour back-end junto con el canal de inserción (token del dispositivo). En el back-end de hello solo debería hacer una sola llamada: CreateOrUpdateInstallation, totalmente es idempotente, por lo que se sienta tooretry libre si es necesario.

Un ejemplo para Amazon Kindle Fire es como el siguiente:

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

Si desea que tooupdate: 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

Para escenarios avanzados tenemos la capacidad de actualización parcial que permite toomodify sólo determinadas propiedades del objeto de la instalación de Hola. Básicamente la actualización parcial es un subconjunto de las operaciones de revisiones de JSON que se puede ejecutar con el objeto de instalación.

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

Eliminación de la instalación:

    hub.deleteInstallation(installation.getInstallationId());

CreateOrUpdate, Patch y Delete son eventualmente coherentes con Get. La operación solicitada solo deja de cola del sistema toohello durante la llamada de Hola y se ejecutará en segundo plano. Tenga en cuenta que Get no está diseñado para el escenario principal en tiempo de ejecución, pero solo para depuración y solución de problemas, estrechamente está limitado por el servicio de Hola.

Flujo de envío para las instalaciones se Hola igual que para los registros. Simplemente hemos introducido un toohello de notificación de opción tootarget instalación particular - etiqueta solo tienes que usar "InstallationId: {deseado-id}". Para el caso anterior sería similar al siguiente:

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

Para una de varias plantillas:

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a>Programación de notificaciones (disponibles para el nivel estándar)
Hola igual que envío normal, pero con un parámetro adicional - scheduledTime que indica cuándo se debe entregar la notificación. El servicio acepta cualquier punto de tiempo entre ahora + 5 minutos y ahora + 7 días.

**Programación de una notificación nativa de Windows:**

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a>Importación y exportación (disponible para el nivel estándar)
A veces es operación masiva de tooperform necesario en los registros. Normalmente es para la integración con otro sistema o solo una corrección masivos toosay actualización Hola las etiquetas. Se recomienda encarecidamente no toouse flujo de Get/actualización si estamos hablando de miles de registros. Capacidad de importación y exportación es escenario de hello toocover diseñada. Básicamente proporciona un contenedor de blobs de toosome de acceso en su cuenta de almacenamiento como un origen de datos entrantes y la ubicación de salida.

**Envío del trabajo de exportación:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


**Envío del trabajo de importación:**

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

**Espere hasta que se realiza el trabajo:**

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

**Obtener todos los trabajos:**

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

**URI con firma de SAS:** se trata de dirección URL de Hola de algunos archivos de blob o contenedor de blob además de conjunto de parámetros, como los permisos y la hora de expiración más firma de todas estas cosas realizadas mediante la clave SAS de la cuenta. El SDK de Java de almacenamiento de Azure tiene amplias capacidades, incluida la creación de ese tipo de URI. Como alternativa simple puede tomar un vistazo a la clase de prueba de ImportExportE2E (desde la ubicación de github de Hola) que tiene una implementación muy básica y compacta de algoritmo de firma.

### <a name="send-notifications"></a>Envío de notificaciones
objeto de notificación de Hello es simplemente un cuerpo con encabezados, algunos métodos de utilidad ayuda en la creación de objetos de hello nativo y plantilla de notificaciones.

* **Tienda Windows y Windows Phone 8.1 (no Silverlight)**
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* **iOS**
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* **Android**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* **Silverlight para Windows Phone 8.0 y 8.1**
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* **Kindle Fire**
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* **Enviar tooTags**
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* **Enviar tootag expresión**       
  
        hub.sendNotification(n, "foo && ! bar");
* **Envío de la notificación de plantilla**
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

La ejecución del código de Java debe generar ahora una notificación que aparece en el dispositivo de destino.

## <a name="next-steps"></a>Pasos siguientes
En este tema se ha explicado cómo toocreate un Java simple de REST cliente centrales de notificaciones. Desde aquí puede:

* Descargar Hola completa [SDK de Java], que contiene el código de hello todo SDK. 
* Practicar con los ejemplos de hello:
  * [Introducción a los Centros de notificaciones]
  * [Envío de noticias de última hora]
  * [Envío de noticias de última hora localizadas]
  * [Enviar notificaciones a los usuarios de tooauthenticated]
  * [Enviar notificaciones de multiplataforma tooauthenticated usuarios]

[SDK de Java]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introducción a los Centros de notificaciones]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Envío de noticias de última hora]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Envío de noticias de última hora localizadas]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Enviar notificaciones a los usuarios de tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Enviar notificaciones de multiplataforma tooauthenticated usuarios]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

