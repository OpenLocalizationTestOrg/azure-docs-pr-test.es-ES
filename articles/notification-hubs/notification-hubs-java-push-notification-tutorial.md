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
# <a name="how-toouse-notification-hubs-from-java"></a><span data-ttu-id="73652-103">¿Cómo toouse centros de notificaciones desde Java</span><span class="sxs-lookup"><span data-stu-id="73652-103">How toouse Notification Hubs from Java</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

<span data-ttu-id="73652-104">Este tema describe las principales características de Hola de oficial de Hola de nuevo totalmente compatible SDK de Java de concentrador de notificación de Azure.</span><span class="sxs-lookup"><span data-stu-id="73652-104">This topic describes hello key features of hello new fully supported official Azure Notification Hub Java SDK.</span></span> <span data-ttu-id="73652-105">Se trata de un proyecto de código abierto y también puede ver el código de hello completo SDK en [SDK de Java].</span><span class="sxs-lookup"><span data-stu-id="73652-105">This is an open source project and you can view hello entire SDK code at [Java SDK].</span></span> 

<span data-ttu-id="73652-106">En general, se pueden tener acceso a todas las características de los centros de notificaciones de un Java/PHP y Python y Ruby back-end mediante la interfaz de REST de base de datos central de notificaciones de hello tal y como se describe en el tema de MSDN de hello [API de REST de centros de notificación](http://msdn.microsoft.com/library/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="73652-106">In general, you can access all Notification Hubs features from a Java/PHP/Python/Ruby back-end using hello Notification Hub REST interface as described in hello MSDN topic [Notification Hubs REST APIs](http://msdn.microsoft.com/library/dn223264.aspx).</span></span> <span data-ttu-id="73652-107">Este SDK de Java proporciona un contenedor fino de estas interfaces REST en Java.</span><span class="sxs-lookup"><span data-stu-id="73652-107">This Java SDK provides a thin wrapper over these REST interfaces in Java.</span></span> 

<span data-ttu-id="73652-108">Hello SDK admite actualmente:</span><span class="sxs-lookup"><span data-stu-id="73652-108">hello SDK supports currently:</span></span>

* <span data-ttu-id="73652-109">CRUD en los Centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="73652-109">CRUD on Notification Hubs</span></span> 
* <span data-ttu-id="73652-110">CRUD en los registros</span><span class="sxs-lookup"><span data-stu-id="73652-110">CRUD on Registrations</span></span>
* <span data-ttu-id="73652-111">Administración de la instalación</span><span class="sxs-lookup"><span data-stu-id="73652-111">Installation Management</span></span>
* <span data-ttu-id="73652-112">Importación y exportación de registros</span><span class="sxs-lookup"><span data-stu-id="73652-112">Import/Export Registrations</span></span>
* <span data-ttu-id="73652-113">Envíos regulares</span><span class="sxs-lookup"><span data-stu-id="73652-113">Regular Sends</span></span>
* <span data-ttu-id="73652-114">Envíos programados</span><span class="sxs-lookup"><span data-stu-id="73652-114">Scheduled Sends</span></span>
* <span data-ttu-id="73652-115">Operaciones asincrónicas mediante Java NIO</span><span class="sxs-lookup"><span data-stu-id="73652-115">Async operations via Java NIO</span></span>
* <span data-ttu-id="73652-116">Plataformas admitidas: APNS (iOS), GCM (Android), WNS (aplicaciones de la Tienda Windows), MPNS (Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android sin servicios de Google)</span><span class="sxs-lookup"><span data-stu-id="73652-116">Supported platforms: APNS (iOS), GCM (Android), WNS (Windows Store apps), MPNS(Windows Phone), ADM (Amazon Kindle Fire), Baidu (Android without Google services)</span></span> 

## <a name="sdk-usage"></a><span data-ttu-id="73652-117">Uso del SDK</span><span class="sxs-lookup"><span data-stu-id="73652-117">SDK Usage</span></span>
### <a name="compile-and-build"></a><span data-ttu-id="73652-118">Compilación y creación</span><span class="sxs-lookup"><span data-stu-id="73652-118">Compile and build</span></span>
<span data-ttu-id="73652-119">Uso de [Maven]</span><span class="sxs-lookup"><span data-stu-id="73652-119">Use [Maven]</span></span>

<span data-ttu-id="73652-120">toobuild:</span><span class="sxs-lookup"><span data-stu-id="73652-120">toobuild:</span></span>

    mvn package

## <a name="code"></a><span data-ttu-id="73652-121">Código</span><span class="sxs-lookup"><span data-stu-id="73652-121">Code</span></span>
### <a name="notification-hub-cruds"></a><span data-ttu-id="73652-122">Operaciones CRUD de Centros de notificaciones</span><span class="sxs-lookup"><span data-stu-id="73652-122">Notification Hub CRUDs</span></span>
<span data-ttu-id="73652-123">**Creación de un administrador de espacio de nombres:**</span><span class="sxs-lookup"><span data-stu-id="73652-123">**Create a NamespaceManager:**</span></span>

    NamespaceManager namespaceManager = new NamespaceManager("connection string")

<span data-ttu-id="73652-124">**Creación de un Centro de notificaciones:**</span><span class="sxs-lookup"><span data-stu-id="73652-124">**Create Notification Hub:**</span></span>

    NotificationHubDescription hub = new NotificationHubDescription("hubname");
    hub.setWindowsCredential(new WindowsCredential("sid","key"));
    hub = namespaceManager.createNotificationHub(hub);

 <span data-ttu-id="73652-125">OR</span><span class="sxs-lookup"><span data-stu-id="73652-125">OR</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="73652-126">**Obtención del Centro de notificaciones:**</span><span class="sxs-lookup"><span data-stu-id="73652-126">**Get Notification Hub:**</span></span>

    hub = namespaceManager.getNotificationHub("hubname");

<span data-ttu-id="73652-127">**Actualización del Centro de notificaciones:**</span><span class="sxs-lookup"><span data-stu-id="73652-127">**Update Notification Hub:**</span></span>

    hub.setMpnsCredential(new MpnsCredential("mpnscert", "mpnskey"));
    hub = namespaceManager.updateNotificationHub(hub);

<span data-ttu-id="73652-128">**Eliminación del Centro de notificaciones:**</span><span class="sxs-lookup"><span data-stu-id="73652-128">**Delete Notification Hub:**</span></span>

    namespaceManager.deleteNotificationHub("hubname");

### <a name="registration-cruds"></a><span data-ttu-id="73652-129">Operaciones CRUD de registro</span><span class="sxs-lookup"><span data-stu-id="73652-129">Registration CRUDs</span></span>
<span data-ttu-id="73652-130">**Creación de un cliente del Centro de notificaciones:**</span><span class="sxs-lookup"><span data-stu-id="73652-130">**Create a Notification Hub client:**</span></span>

    hub = new NotificationHub("connection string", "hubname");

<span data-ttu-id="73652-131">**Creación de un registro de Windows:**</span><span class="sxs-lookup"><span data-stu-id="73652-131">**Create Windows registration:**</span></span>

    WindowsRegistration reg = new WindowsRegistration(new URI(CHANNELURI));
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");    
    hub.createRegistration(reg);

<span data-ttu-id="73652-132">**Creación de un registro de iOS:**</span><span class="sxs-lookup"><span data-stu-id="73652-132">**Create iOS registration:**</span></span>

    AppleRegistration reg = new AppleRegistration(DEVICETOKEN);
    reg.getTags().add("myTag");
    reg.getTags().add("myOtherTag");
    hub.createRegistration(reg);

<span data-ttu-id="73652-133">Del mismo modo puede crear registros para Android (GCM), Windows Phone (MPNS) y Kindle Fire (ADM).</span><span class="sxs-lookup"><span data-stu-id="73652-133">Similarly you can create registrations for Android (GCM), Windows Phone (MPNS), and Kindle Fire (ADM).</span></span>

<span data-ttu-id="73652-134">**Creación de registros de plantilla:**</span><span class="sxs-lookup"><span data-stu-id="73652-134">**Create template registrations:**</span></span>

    WindowsTemplateRegistration reg = new WindowsTemplateRegistration(new URI(CHANNELURI), WNSBODYTEMPLATE);
    reg.getHeaders().put("X-WNS-Type", "wns/toast");
    hub.createRegistration(reg);

<span data-ttu-id="73652-135">**Creación de registros mediante el patrón create registrationid + upsert**</span><span class="sxs-lookup"><span data-stu-id="73652-135">**Create registrations using create registrationid + upsert pattern**</span></span>

<span data-ttu-id="73652-136">Quita los duplicados debido a las respuestas de tooany perdido si almacenar los Id. de registro en el dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="73652-136">Removes duplicates due tooany lost responses if storing registration ids on hello device:</span></span>

    String id = hub.createRegistrationId();
    WindowsRegistration reg = new WindowsRegistration(id, new URI(CHANNELURI));
    hub.upsertRegistration(reg);

<span data-ttu-id="73652-137">**Actualización de registros:**</span><span class="sxs-lookup"><span data-stu-id="73652-137">**Update registrations:**</span></span>

    hub.updateRegistration(reg);

<span data-ttu-id="73652-138">**Eliminación de registros:**</span><span class="sxs-lookup"><span data-stu-id="73652-138">**Delete registrations:**</span></span>

    hub.deleteRegistration(regid);

<span data-ttu-id="73652-139">**Consulta de registros:**</span><span class="sxs-lookup"><span data-stu-id="73652-139">**Query registrations:**</span></span>

* <span data-ttu-id="73652-140">**Obtención de un único registro:**</span><span class="sxs-lookup"><span data-stu-id="73652-140">**Get single registration:**</span></span>
  
    <span data-ttu-id="73652-141">hub.getRegistration(regid);</span><span class="sxs-lookup"><span data-stu-id="73652-141">hub.getRegistration(regid);</span></span>
* <span data-ttu-id="73652-142">**Obtención de todos los registros en el centro:**</span><span class="sxs-lookup"><span data-stu-id="73652-142">**Get all registrations in hub:**</span></span>
  
    <span data-ttu-id="73652-143">hub.getRegistrations();</span><span class="sxs-lookup"><span data-stu-id="73652-143">hub.getRegistrations();</span></span>
* <span data-ttu-id="73652-144">**Obtención de registros con etiqueta:**</span><span class="sxs-lookup"><span data-stu-id="73652-144">**Get registrations with tag:**</span></span>
  
    <span data-ttu-id="73652-145">hub.getRegistrationsByTag("miEtiqueta");</span><span class="sxs-lookup"><span data-stu-id="73652-145">hub.getRegistrationsByTag("myTag");</span></span>
* <span data-ttu-id="73652-146">**Obtención de registros por canal:**</span><span class="sxs-lookup"><span data-stu-id="73652-146">**Get registrations by channel:**</span></span>
  
    <span data-ttu-id="73652-147">hub.getRegistrationsByChannel("tokenDeDispositivo");</span><span class="sxs-lookup"><span data-stu-id="73652-147">hub.getRegistrationsByChannel("devicetoken");</span></span>

<span data-ttu-id="73652-148">Todas las consultas de la colección admiten los tokens $top y continuation.</span><span class="sxs-lookup"><span data-stu-id="73652-148">All collection queries support $top and continuation tokens.</span></span>

### <a name="installation-api-usage"></a><span data-ttu-id="73652-149">Uso de la API de instalación</span><span class="sxs-lookup"><span data-stu-id="73652-149">Installation API usage</span></span>
<span data-ttu-id="73652-150">La API de instalación es un mecanismo alternativo para la administración de registros.</span><span class="sxs-lookup"><span data-stu-id="73652-150">Installation API is an alternative mechanism for registration management.</span></span> <span data-ttu-id="73652-151">En lugar de mantener varios registros que no es trivial y se puede realizar fácilmente mal o de forma ineficaz, ahora es posible toouse un objeto de una sola instalación.</span><span class="sxs-lookup"><span data-stu-id="73652-151">Instead of maintaining multiple registrations which is not trivial and may be easily done wrongly or inefficiently, it is now possible toouse a SINGLE Installation object.</span></span> <span data-ttu-id="73652-152">La instalación contiene todo lo que necesita: canal de inserción (token del dispositivo), etiquetas, plantillas, iconos secundarios (para WNS y APNS).</span><span class="sxs-lookup"><span data-stu-id="73652-152">Installation contains everything you need: push channel (device token), tags, templates, secondary tiles (for WNS and APNS).</span></span> <span data-ttu-id="73652-153">Ya no necesita toocall Hola servicio tooget Id.: simplemente generar GUID o cualquier otro identificador, mantener en el dispositivo y enviar tooyour back-end junto con el canal de inserción (token del dispositivo).</span><span class="sxs-lookup"><span data-stu-id="73652-153">You don't need toocall hello service tooget Id anymore - just generate GUID or any other identifier, keep it on device and send tooyour backend together with push channel (device token).</span></span> <span data-ttu-id="73652-154">En el back-end de hello solo debería hacer una sola llamada: CreateOrUpdateInstallation, totalmente es idempotente, por lo que se sienta tooretry libre si es necesario.</span><span class="sxs-lookup"><span data-stu-id="73652-154">On hello backend you should only do a single call: CreateOrUpdateInstallation, it is fully idempotent, so feel free tooretry if needed.</span></span>

<span data-ttu-id="73652-155">Un ejemplo para Amazon Kindle Fire es como el siguiente:</span><span class="sxs-lookup"><span data-stu-id="73652-155">As example for Amazon Kindle Fire it looks like this:</span></span>

    Installation installation = new Installation("installation-id", NotificationPlatform.Adm, "adm-push-channel");
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="73652-156">Si desea que tooupdate:</span><span class="sxs-lookup"><span data-stu-id="73652-156">If you want tooupdate it:</span></span> 

    installation.addTag("foo");
    installation.addTemplate("template1", new InstallationTemplate("{\"data\":{\"key1\":\"$(value1)\"}}","tag-for-template1"));
    installation.addTemplate("template2", new InstallationTemplate("{\"data\":{\"key2\":\"$(value2)\"}}","tag-for-template2"));
    hub.createOrUpdateInstallation(installation);

<span data-ttu-id="73652-157">Para escenarios avanzados tenemos la capacidad de actualización parcial que permite toomodify sólo determinadas propiedades del objeto de la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="73652-157">For advanced scenarios we have partial update capability which allows toomodify only particular properties of hello installation object.</span></span> <span data-ttu-id="73652-158">Básicamente la actualización parcial es un subconjunto de las operaciones de revisiones de JSON que se puede ejecutar con el objeto de instalación.</span><span class="sxs-lookup"><span data-stu-id="73652-158">Basically partial update is subset of JSON Patch operations you can run against Installation object.</span></span>

    PartialUpdateOperation addChannel = new PartialUpdateOperation(UpdateOperationType.Add, "/pushChannel", "adm-push-channel2");
    PartialUpdateOperation addTag = new PartialUpdateOperation(UpdateOperationType.Add, "/tags", "bar");
    PartialUpdateOperation replaceTemplate = new PartialUpdateOperation(UpdateOperationType.Replace, "/templates/template1", new InstallationTemplate("{\"data\":{\"key3\":\"$(value3)\"}}","tag-for-template1")).toJson());
    hub.patchInstallation("installation-id", addChannel, addTag, replaceTemplate);

<span data-ttu-id="73652-159">Eliminación de la instalación:</span><span class="sxs-lookup"><span data-stu-id="73652-159">Delete Installation:</span></span>

    hub.deleteInstallation(installation.getInstallationId());

<span data-ttu-id="73652-160">CreateOrUpdate, Patch y Delete son eventualmente coherentes con Get.</span><span class="sxs-lookup"><span data-stu-id="73652-160">CreateOrUpdate, Patch and Delete are eventually consistent with Get.</span></span> <span data-ttu-id="73652-161">La operación solicitada solo deja de cola del sistema toohello durante la llamada de Hola y se ejecutará en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="73652-161">Your requested operation just goes toohello system queue during hello call and will be executed in background.</span></span> <span data-ttu-id="73652-162">Tenga en cuenta que Get no está diseñado para el escenario principal en tiempo de ejecución, pero solo para depuración y solución de problemas, estrechamente está limitado por el servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="73652-162">Note that Get is not designed for main runtime scenario but just for debug and troubleshooting purposes, it is tightly throttled by hello service.</span></span>

<span data-ttu-id="73652-163">Flujo de envío para las instalaciones se Hola igual que para los registros.</span><span class="sxs-lookup"><span data-stu-id="73652-163">Send flow for Installations is hello same as for Registrations.</span></span> <span data-ttu-id="73652-164">Simplemente hemos introducido un toohello de notificación de opción tootarget instalación particular - etiqueta solo tienes que usar "InstallationId: {deseado-id}".</span><span class="sxs-lookup"><span data-stu-id="73652-164">We've just introduced an option tootarget notification toohello particular Installation - just use tag "InstallationId:{desired-id}".</span></span> <span data-ttu-id="73652-165">Para el caso anterior sería similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="73652-165">For case above it would look like this:</span></span>

    Notification n = Notification.createWindowsNotification("WNS body");
    hub.sendNotification(n, "InstallationId:{installation-id}");

<span data-ttu-id="73652-166">Para una de varias plantillas:</span><span class="sxs-lookup"><span data-stu-id="73652-166">For one of several templates:</span></span>

    Map<String, String> prop =  new HashMap<String, String>();
    prop.put("value3", "some value");
    Notification n = Notification.createTemplateNotification(prop);
    hub.sendNotification(n, "InstallationId:{installation-id} && tag-for-template1");

### <a name="schedule-notifications-available-for-standard-tier"></a><span data-ttu-id="73652-167">Programación de notificaciones (disponibles para el nivel estándar)</span><span class="sxs-lookup"><span data-stu-id="73652-167">Schedule Notifications (available for STANDARD Tier)</span></span>
<span data-ttu-id="73652-168">Hola igual que envío normal, pero con un parámetro adicional - scheduledTime que indica cuándo se debe entregar la notificación.</span><span class="sxs-lookup"><span data-stu-id="73652-168">hello same as regular send but with one additional parameter - scheduledTime which says when notification should be delivered.</span></span> <span data-ttu-id="73652-169">El servicio acepta cualquier punto de tiempo entre ahora + 5 minutos y ahora + 7 días.</span><span class="sxs-lookup"><span data-stu-id="73652-169">Service accepts any point of time between now + 5 minutes and now + 7 days.</span></span>

<span data-ttu-id="73652-170">**Programación de una notificación nativa de Windows:**</span><span class="sxs-lookup"><span data-stu-id="73652-170">**Schedule a Windows native notification:**</span></span>

    Calendar c = Calendar.getInstance();
    c.add(Calendar.DATE, 1);    
    Notification n = Notification.createWindowsNotification("WNS body");
    hub.scheduleNotification(n, c.getTime());

### <a name="importexport-available-for-standard-tier"></a><span data-ttu-id="73652-171">Importación y exportación (disponible para el nivel estándar)</span><span class="sxs-lookup"><span data-stu-id="73652-171">Import/Export (available for STANDARD Tier)</span></span>
<span data-ttu-id="73652-172">A veces es operación masiva de tooperform necesario en los registros.</span><span class="sxs-lookup"><span data-stu-id="73652-172">Sometimes it is required tooperform bulk operation against registrations.</span></span> <span data-ttu-id="73652-173">Normalmente es para la integración con otro sistema o solo una corrección masivos toosay actualización Hola las etiquetas.</span><span class="sxs-lookup"><span data-stu-id="73652-173">Usually it is for integration with another system or just a massive fix toosay update hello tags.</span></span> <span data-ttu-id="73652-174">Se recomienda encarecidamente no toouse flujo de Get/actualización si estamos hablando de miles de registros.</span><span class="sxs-lookup"><span data-stu-id="73652-174">It is strongly not recommended toouse Get/Update flow if we are talking about thousands of registrations.</span></span> <span data-ttu-id="73652-175">Capacidad de importación y exportación es escenario de hello toocover diseñada.</span><span class="sxs-lookup"><span data-stu-id="73652-175">Import/Export capability is designed toocover hello scenario.</span></span> <span data-ttu-id="73652-176">Básicamente proporciona un contenedor de blobs de toosome de acceso en su cuenta de almacenamiento como un origen de datos entrantes y la ubicación de salida.</span><span class="sxs-lookup"><span data-stu-id="73652-176">Basically you provide an access toosome blob container under your storage account as a source of incoming data and location for output.</span></span>

<span data-ttu-id="73652-177">**Envío del trabajo de exportación:**</span><span class="sxs-lookup"><span data-stu-id="73652-177">**Submit export job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ExportRegistrations);
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);


<span data-ttu-id="73652-178">**Envío del trabajo de importación:**</span><span class="sxs-lookup"><span data-stu-id="73652-178">**Submit import job:**</span></span>

    NotificationHubJob job = new NotificationHubJob();
    job.setJobType(NotificationHubJobType.ImportCreateRegistrations);
    job.setImportFileUri("input file uri with SAS signature");
    job.setOutputContainerUri("container uri with SAS signature");
    job = hub.submitNotificationHubJob(job);

<span data-ttu-id="73652-179">**Espere hasta que se realiza el trabajo:**</span><span class="sxs-lookup"><span data-stu-id="73652-179">**Wait until job is done:**</span></span>

    while(true){
        Thread.sleep(1000);
        job = hub.getNotificationHubJob(job.getJobId());
        if(job.getJobStatus() == NotificationHubJobStatus.Completed)
            break;
    }       

<span data-ttu-id="73652-180">**Obtener todos los trabajos:**</span><span class="sxs-lookup"><span data-stu-id="73652-180">**Get all jobs:**</span></span>

    List<NotificationHubJob> jobs = hub.getAllNotificationHubJobs();

<span data-ttu-id="73652-181">**URI con firma de SAS:** se trata de dirección URL de Hola de algunos archivos de blob o contenedor de blob además de conjunto de parámetros, como los permisos y la hora de expiración más firma de todas estas cosas realizadas mediante la clave SAS de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="73652-181">**URI with SAS signature:** This is hello URL of some blob file or blob container plus set of parameters like permissions and expiration time plus signature of all these things made using account's SAS key.</span></span> <span data-ttu-id="73652-182">El SDK de Java de almacenamiento de Azure tiene amplias capacidades, incluida la creación de ese tipo de URI.</span><span class="sxs-lookup"><span data-stu-id="73652-182">Azure Storage Java SDK has rich capabilities including creation of such kind of URIs.</span></span> <span data-ttu-id="73652-183">Como alternativa simple puede tomar un vistazo a la clase de prueba de ImportExportE2E (desde la ubicación de github de Hola) que tiene una implementación muy básica y compacta de algoritmo de firma.</span><span class="sxs-lookup"><span data-stu-id="73652-183">As simple alternative you can take a look at ImportExportE2E test class (from hello github location) which has very basic and compact implementation of signing algorithm.</span></span>

### <a name="send-notifications"></a><span data-ttu-id="73652-184">Envío de notificaciones</span><span class="sxs-lookup"><span data-stu-id="73652-184">Send Notifications</span></span>
<span data-ttu-id="73652-185">objeto de notificación de Hello es simplemente un cuerpo con encabezados, algunos métodos de utilidad ayuda en la creación de objetos de hello nativo y plantilla de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="73652-185">hello Notification object is simply a body with headers, some utility methods help in building hello native and template notifications objects.</span></span>

* <span data-ttu-id="73652-186">**Tienda Windows y Windows Phone 8.1 (no Silverlight)**</span><span class="sxs-lookup"><span data-stu-id="73652-186">**Windows Store and Windows Phone 8.1 (non-Silverlight)**</span></span>
  
        String toast = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">Hello from Java!</text></binding></visual></toast>";
        Notification n = Notification.createWindowsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="73652-187">**iOS**</span><span class="sxs-lookup"><span data-stu-id="73652-187">**iOS**</span></span>
  
        String alert = "{\"aps\":{\"alert\":\"Hello from Java!\"}}";
        Notification n = Notification.createAppleNotification(alert);
        hub.sendNotification(n);
* <span data-ttu-id="73652-188">**Android**</span><span class="sxs-lookup"><span data-stu-id="73652-188">**Android**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createGcmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="73652-189">**Silverlight para Windows Phone 8.0 y 8.1**</span><span class="sxs-lookup"><span data-stu-id="73652-189">**Windows Phone 8.0 and 8.1 Silverlight**</span></span>
  
        String toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>Hello from Java!</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
        Notification n = Notification.createMpnsNotification(toast);
        hub.sendNotification(n);
* <span data-ttu-id="73652-190">**Kindle Fire**</span><span class="sxs-lookup"><span data-stu-id="73652-190">**Kindle Fire**</span></span>
  
        String message = "{\"data\":{\"msg\":\"Hello from Java!\"}}";
        Notification n = Notification.createAdmNotification(message);
        hub.sendNotification(n);
* <span data-ttu-id="73652-191">**Enviar tooTags**</span><span class="sxs-lookup"><span data-stu-id="73652-191">**Send tooTags**</span></span>
  
        Set<String> tags = new HashSet<String>();
        tags.add("boo");
        tags.add("foo");
        hub.sendNotification(n, tags);
* <span data-ttu-id="73652-192">**Enviar tootag expresión**</span><span class="sxs-lookup"><span data-stu-id="73652-192">**Send tootag expression**</span></span>       
  
        hub.sendNotification(n, "foo && ! bar");
* <span data-ttu-id="73652-193">**Envío de la notificación de plantilla**</span><span class="sxs-lookup"><span data-stu-id="73652-193">**Send template notification**</span></span>
  
        Map<String, String> prop =  new HashMap<String, String>();
        prop.put("prop1", "v1");
        prop.put("prop2", "v2");
        Notification n = Notification.createTemplateNotification(prop);
        hub.sendNotification(n);

<span data-ttu-id="73652-194">La ejecución del código de Java debe generar ahora una notificación que aparece en el dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="73652-194">Running your Java code should now produce a notification appearing on your target device.</span></span>

## <span data-ttu-id="73652-195"><a name="next-steps"></a>Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="73652-195"><a name="next-steps"></a>Next Steps</span></span>
<span data-ttu-id="73652-196">En este tema se ha explicado cómo toocreate un Java simple de REST cliente centrales de notificaciones.</span><span class="sxs-lookup"><span data-stu-id="73652-196">In this topic we showed how toocreate a simple Java REST client for Notification Hubs.</span></span> <span data-ttu-id="73652-197">Desde aquí puede:</span><span class="sxs-lookup"><span data-stu-id="73652-197">From here you can:</span></span>

* <span data-ttu-id="73652-198">Descargar Hola completa [SDK de Java], que contiene el código de hello todo SDK.</span><span class="sxs-lookup"><span data-stu-id="73652-198">Download hello full [Java SDK], which contains hello entire SDK code.</span></span> 
* <span data-ttu-id="73652-199">Practicar con los ejemplos de hello:</span><span class="sxs-lookup"><span data-stu-id="73652-199">Play with hello samples:</span></span>
  * <span data-ttu-id="73652-200">[Introducción a los Centros de notificaciones]</span><span class="sxs-lookup"><span data-stu-id="73652-200">[Get Started with Notification Hubs]</span></span>
  * <span data-ttu-id="73652-201">[Envío de noticias de última hora]</span><span class="sxs-lookup"><span data-stu-id="73652-201">[Send breaking news]</span></span>
  * <span data-ttu-id="73652-202">[Envío de noticias de última hora localizadas]</span><span class="sxs-lookup"><span data-stu-id="73652-202">[Send localized breaking news]</span></span>
  * <span data-ttu-id="73652-203">[Enviar notificaciones a los usuarios de tooauthenticated]</span><span class="sxs-lookup"><span data-stu-id="73652-203">[Send notifications tooauthenticated users]</span></span>
  * <span data-ttu-id="73652-204">[Enviar notificaciones de multiplataforma tooauthenticated usuarios]</span><span class="sxs-lookup"><span data-stu-id="73652-204">[Send cross-platform notifications tooauthenticated users]</span></span>

[SDK de Java]: https://github.com/Azure/azure-notificationhubs-java-backend
[Get started tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-ios-get-started/
[Introducción a los Centros de notificaciones]: http://www.windowsazure.com/manage/services/notification-hubs/getting-started-windows-dotnet/
[Envío de noticias de última hora]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-dotnet/
[Envío de noticias de última hora localizadas]: http://www.windowsazure.com/manage/services/notification-hubs/breaking-news-localized-dotnet/
[Enviar notificaciones a los usuarios de tooauthenticated]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users/
[Enviar notificaciones de multiplataforma tooauthenticated usuarios]: http://www.windowsazure.com/manage/services/notification-hubs/notify-users-xplat-mobile-services/
[Maven]: http://maven.apache.org/

