---
title: Servicios de entrega de aaaContinuous para la nube con Visual Studio Online | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooset la entrega continua de Azure en la nube aplicaciones sin guardar archivos de configuración de servicio de almacenamiento toohello clave de diagnóstico"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 148b2959-c5db-4e4a-a7e9-fccb252e7e8a
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: dc87d049e46daf8b8a26ee4450ebd9b7910f287b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-tooazure-using-visual-studio-online"></a><span data-ttu-id="486a1-103">Securely guardar en la nube servicios de almacenamiento de información clave de diagnóstico y tooAzure de integración continua el programa de instalación e implementación mediante Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="486a1-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment tooAzure using Visual Studio Online</span></span>
 <span data-ttu-id="486a1-104">Hoy en día es un proyectos de código fuente de tooopen práctica común.</span><span class="sxs-lookup"><span data-stu-id="486a1-104">It is a common practice tooopen source projects nowadays.</span></span> <span data-ttu-id="486a1-105">Guardar los secretos de aplicación en archivos de configuración ya no es una práctica segura, ya que se producen vulnerabilidades de seguridad procedentes de los secretos que se filtran desde los controles de código fuente públicos.</span><span class="sxs-lookup"><span data-stu-id="486a1-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="486a1-106">Almacenamiento secreto como texto no cifrado en un archivo en una canalización de integración continua no es segura ya sea porque pudieron ser servidores de compilación los recursos compartidos en el entorno de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="486a1-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on hello Cloud environment.</span></span> <span data-ttu-id="486a1-107">Este artículo explica cómo Visual Studio y Visual Studio Online mitiga los riesgos de seguridad de Hola durante el desarrollo y el proceso de integración continua.</span><span class="sxs-lookup"><span data-stu-id="486a1-107">This article explains how Visual Studio and Visual Studio Online mitigates hello security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="486a1-108">Eliminación del secreto de la clave de almacenamiento de la información de diagnóstico del archivo de configuración de proyecto</span><span class="sxs-lookup"><span data-stu-id="486a1-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="486a1-109">La extensión de diagnósticos de Cloud Services requiere Azure Storage para guardar los resultados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="486a1-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="486a1-110">Anteriormente la cadena de conexión de almacenamiento de Hola se especifica en archivos de configuración (.cscfg) de servicios en la nube de Hola y podría activarse en el control de toosource.</span><span class="sxs-lookup"><span data-stu-id="486a1-110">Formerly hello storage connection string is specified in hello Cloud Services configuration (.cscfg) files and could be checked in toosource control.</span></span> <span data-ttu-id="486a1-111">En la versión más reciente de Azure SDK de hello hemos cambiado almacén tooonly Hola comportamiento que una parcial cadena de conexión con la clave de hello reemplazado por un símbolo (token).</span><span class="sxs-lookup"><span data-stu-id="486a1-111">In hello latest Azure SDK release we changed hello behavior tooonly store a partial connection string with hello key replaced by a token.</span></span> <span data-ttu-id="486a1-112">Hola pasos describe el funcionamiento de nuevas herramientas de servicios en la nube hello:</span><span class="sxs-lookup"><span data-stu-id="486a1-112">hello following steps describe how hello new Cloud Services tooling works:</span></span>

### <a name="1-open-hello-role-designer"></a><span data-ttu-id="486a1-113">1. Abra el Diseñador de roles de Hola</span><span class="sxs-lookup"><span data-stu-id="486a1-113">1. Open hello Role designer</span></span>
* <span data-ttu-id="486a1-114">Haga doble clic o haga clic con el botón secundario en un diseñador de roles de tooopen de rol de servicios en la nube</span><span class="sxs-lookup"><span data-stu-id="486a1-114">Double click or right click on a Cloud Services role tooopen Role designer</span></span>

![Abra el diseñador de roles][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="486a1-116">2. En la sección de diagnósticos, se ha agregado una nueva casilla de verificación "Don’t remove storage key secret from project" (No quitar secreto de la clave de almacenamiento del proyecto)</span><span class="sxs-lookup"><span data-stu-id="486a1-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="486a1-117">Si usas el emulador de almacenamiento local de hello, esta casilla está deshabilitada porque no hay ningún secreto toomanage de cadena de conexión local de hello, que es UseDevelopmentStorage = true.</span><span class="sxs-lookup"><span data-stu-id="486a1-117">If you are using hello local storage emulator, this checkbox is disabled because there is no secret toomanage for hello local connection string, which is UseDevelopmentStorage=true.</span></span>

![La cadena de conexión del emulador de almacenamiento local no es un secreto][1]

* <span data-ttu-id="486a1-119">Si va a crear un nuevo proyecto, esta casilla de verificación estará desactivada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="486a1-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="486a1-120">Esto da como resultado de sección de clave de almacenamiento de Hola de cadena de conexión de almacenamiento de hello seleccionado se reemplazan con un token.</span><span class="sxs-lookup"><span data-stu-id="486a1-120">This results in hello storage key section of hello selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="486a1-121">Hello valor del token de Hola se encontrará en la carpeta AppData móviles del usuario actual de hello, por ejemplo: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="486a1-121">hello value of hello token will be found under hello current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="486a1-122">Tenga en cuenta esa carpeta user\AppData de hello es cuyo acceso esté controlado por inicio de sesión de usuario y se considera un lugar seguro toostore los secretos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="486a1-122">Note that hello user\AppData folder is Access Controlled by user sign-in and is considered a secure place toostore development secrets.</span></span>
> 
> 

![La clave de almacenamiento se guarda en la carpeta del perfil de usuario][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="486a1-124">3. Selección de la cuenta de almacenamiento de información de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="486a1-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="486a1-125">Seleccione una cuenta de almacenamiento del cuadro de diálogo de hello iniciada haciendo clic en "..." hello</span><span class="sxs-lookup"><span data-stu-id="486a1-125">Select a storage account from hello dialog launched by clicking hello “…”</span></span> <span data-ttu-id="486a1-126">.</span><span class="sxs-lookup"><span data-stu-id="486a1-126">button.</span></span> <span data-ttu-id="486a1-127">Tenga en cuenta cómo cadena de conexión de almacenamiento de hello generado no tendrá clave de cuenta de almacenamiento de Hola.</span><span class="sxs-lookup"><span data-stu-id="486a1-127">Notice how hello storage connection string generated will not have hello storage account key.</span></span>
* <span data-ttu-id="486a1-128">Por ejemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="486a1-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-hello-project"></a><span data-ttu-id="486a1-129">4.    Depurar el proyecto de Hola</span><span class="sxs-lookup"><span data-stu-id="486a1-129">4.    Debugging hello project</span></span>
* <span data-ttu-id="486a1-130">F5 toostart de depuración en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="486a1-130">F5 toostart debugging in Visual Studio.</span></span> <span data-ttu-id="486a1-131">Todo lo que debería funcionar en hello igual manera que antes.</span><span class="sxs-lookup"><span data-stu-id="486a1-131">Everything should work in hello same way as before.</span></span>
  <span data-ttu-id="486a1-132">![Inicie la depuración localmente][3]</span><span class="sxs-lookup"><span data-stu-id="486a1-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="486a1-133">5. Publicación del proyecto desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="486a1-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="486a1-134">Hola iniciar cuadro de diálogo Publicar y continúe con las instrucciones de inicio de sesión toopublish hello applicaion tooAzure.</span><span class="sxs-lookup"><span data-stu-id="486a1-134">Launch hello publish dialog and proceed with sign-in instructions toopublish hello applicaion tooAzure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="486a1-135">6. Información adicional</span><span class="sxs-lookup"><span data-stu-id="486a1-135">6. Additional information</span></span>
> <span data-ttu-id="486a1-136">Nota: el panel de configuración de hello en el Diseñador de roles de hello permanecerá tal cual por ahora.</span><span class="sxs-lookup"><span data-stu-id="486a1-136">Note: hello Settings panel in hello role designer will stay as it is for now.</span></span> <span data-ttu-id="486a1-137">Si desea características de administración de secretos de toouse hello para el diagnóstico, vaya toohello configuraciones (pestaña).</span><span class="sxs-lookup"><span data-stu-id="486a1-137">If you want toouse hello secret management feature for diagnostics, go toohello Configurations tab.</span></span>
> 
> 

![Incorporación de la configuración][4]

> <span data-ttu-id="486a1-139">Nota: Si está habilitada, se almacenará Hola Application Insights clave como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="486a1-139">Note: If enabled, hello Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="486a1-140">clave de Hola sólo se utiliza para el contenido de la carga de modo que ningún dato confidencial estarán en riesgo de comprometer.</span><span class="sxs-lookup"><span data-stu-id="486a1-140">hello key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="486a1-141">Compilación y publicación de un proyecto de Cloud Services mediante plantillas de tareas en Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="486a1-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="486a1-142">Hola pasos se muestra cómo usar tareas en línea de Visual Studio de proyectos de toosetup integración continua para servicios en la nube:</span><span class="sxs-lookup"><span data-stu-id="486a1-142">hello following steps illustrates how toosetup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="486a1-143">1.    Obtenga una cuenta de VSO</span><span class="sxs-lookup"><span data-stu-id="486a1-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="486a1-144">[Crear cuenta de Visual Studio Online] [ Create Visual Studio Online account] si aún no tiene uno</span><span class="sxs-lookup"><span data-stu-id="486a1-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="486a1-145">[Crear proyecto de equipo] [ Create team project] en su cuenta en línea de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="486a1-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="486a1-146">2.    Configuración del control de código fuente en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="486a1-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="486a1-147">Conectar el proyecto de equipo de tooa</span><span class="sxs-lookup"><span data-stu-id="486a1-147">Connect tooa team project</span></span>

![Conectar tooteam proyecto][5]

![Seleccione tooconnect de proyecto de equipo a][6]

* <span data-ttu-id="486a1-150">Agregar el control de toosource de proyecto</span><span class="sxs-lookup"><span data-stu-id="486a1-150">Add your project toosource control</span></span>

![Agregar proyecto toosource control][7]

![Carpeta de control de código fuente de mapa proyecto tooa][8]

* <span data-ttu-id="486a1-153">Compruebe el proyecto desde Team Explorer</span><span class="sxs-lookup"><span data-stu-id="486a1-153">Check in your project from Team Explorer</span></span>

![Compruebe en el control de toosource de proyectos][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="486a1-155">3.    Configuración del proceso de compilación</span><span class="sxs-lookup"><span data-stu-id="486a1-155">3.    Configure Build process</span></span>
* <span data-ttu-id="486a1-156">Examinar el proyecto de equipo de tooyour y agregue un nuevo proceso de compilación, plantillas</span><span class="sxs-lookup"><span data-stu-id="486a1-156">Browse tooyour team project and add a new build process Templates</span></span>

![Agregue una nueva compilación][10]

* <span data-ttu-id="486a1-158">Seleccione una tarea de compilación</span><span class="sxs-lookup"><span data-stu-id="486a1-158">Select build task</span></span>

![Agregue una tarea de compilación][11]

![Seleccione la plantilla de tarea de compilación de Visual Studio][12]

* <span data-ttu-id="486a1-161">Edite la entrada de la tarea de compilación.</span><span class="sxs-lookup"><span data-stu-id="486a1-161">Edit build task input.</span></span> <span data-ttu-id="486a1-162">Por favor, personalizar la generación de Hola que tenga parámetros según tooyour</span><span class="sxs-lookup"><span data-stu-id="486a1-162">Please customize hello build parameters according tooyour need</span></span>

![Configure la tarea de compilación][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="486a1-164">Configure las variables de compilación</span><span class="sxs-lookup"><span data-stu-id="486a1-164">Configure build variables</span></span>

![Configure las variables de compilación][14]

* <span data-ttu-id="486a1-166">Agregar una caída de compilación de tooupload de tarea</span><span class="sxs-lookup"><span data-stu-id="486a1-166">Add a task tooupload build drop</span></span>

![Elija publicar tarea de destino de compilación][15]

![Configure la tarea de publicación de destino de compilación][16]

* <span data-ttu-id="486a1-169">Ejecute hello compilación</span><span class="sxs-lookup"><span data-stu-id="486a1-169">Run hello build</span></span>

![Ponga en cola la nueva compilación][17]

![Vea el resumen de compilación][18]

* <span data-ttu-id="486a1-172">Si se realiza correctamente la compilación de hello verá un toobelow similar de resultado</span><span class="sxs-lookup"><span data-stu-id="486a1-172">if hello build is successful you will see a result similar toobelow</span></span>

![Resultado de la compilación][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="486a1-174">4.    Configuración del proceso de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="486a1-174">4.    Configure Release process</span></span>
* <span data-ttu-id="486a1-175">Cree una nueva versión</span><span class="sxs-lookup"><span data-stu-id="486a1-175">Create a new release</span></span>

![Cree una nueva versión][20]

* <span data-ttu-id="486a1-177">Seleccione la tarea de implementación de servicios de nube de Azure de hello</span><span class="sxs-lookup"><span data-stu-id="486a1-177">Select hello Azure Cloud Services Deployment task</span></span>

![Seleccione la tarea de implementación de Azure Cloud Services][21]

* <span data-ttu-id="486a1-179">Como no está activada la clave de cuenta de almacenamiento de hello en control toosource, necesitamos clave secreta de hello toospecify para configurar extensiones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="486a1-179">As hello storage account key is not checked in toosource control, we need toospecify hello secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="486a1-180">Expanda hello **opciones avanzadas para crear un nuevo servicio** sección y editar hello **claves de cuenta de almacenamiento de diagnósticos** proporcionados por el parámetro.</span><span class="sxs-lookup"><span data-stu-id="486a1-180">Expand hello **Advanced Options for Creating New Service** section and edit hello **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="486a1-181">Esta entrada se toma en varias líneas de par clave-valor en formato de Hola de **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="486a1-181">This input takes in multiple lines of key value pair in hello format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="486a1-182">Nota: si su cuenta de almacenamiento está por debajo de diagnóstico hello misma suscripción donde publicará la aplicación de servicios en la nube de hello, no tiene clave de hello tooenter de entrada de tarea de implementación de hello; implementación de Hola obtendrá mediante programación la información de almacenamiento Hola desde su suscripción</span><span class="sxs-lookup"><span data-stu-id="486a1-182">Note: if your diagnostics storage account is under hello same subscription as where you will publish hello Cloud Services application, you don't have tooenter hello key in hello deployment task input; hello deployment will programmatically obtain hello storage information from your subscription</span></span>
> 
> 

![Configuración de la tarea de implementación de Azure Cloud Services][22]

* <span data-ttu-id="486a1-184">Secreto de uso de compilación variables toosave claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="486a1-184">Use secret build variables toosave storage Keys.</span></span> <span data-ttu-id="486a1-185">toomask haga clic en una variable como secreto en el icono de candado de hello en hello derecha de hello las Variables de entrada</span><span class="sxs-lookup"><span data-stu-id="486a1-185">toomask a variable as secret click on hello lock icon on hello right side of hello Variables input</span></span>

![Guardar las claves de almacenamiento en variables de compilación de secreto][23]

* <span data-ttu-id="486a1-187">Crear una versión e implementar su proyecto tooAzure</span><span class="sxs-lookup"><span data-stu-id="486a1-187">Create a release and deploy your project tooAzure</span></span>

![Cree una nueva versión][24]

## <a name="next-steps"></a><span data-ttu-id="486a1-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="486a1-189">Next steps</span></span>
<span data-ttu-id="486a1-190">toolearn más información acerca de la configuración de extensiones de diagnóstico para los servicios de nube de Azure, visite [habilitar diagnósticos en los servicios de nube de Azure con PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="486a1-190">toolearn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

[Create Visual Studio Online account]:https://www.visualstudio.com/team-services/
[Create team project]: https://www.visualstudio.com/it-it/docs/setup-admin/team-services/connect-to-visual-studio-team-services
[Enable diagnostics in Azure Cloud Services using PowerShell]:https://azure.microsoft.com/en-us/documentation/articles/cloud-services-diagnostics-powershell/

[0]: ./media/cloud-services-vs-ci/vs-01.png
[1]: ./media/cloud-services-vs-ci/vs-02.png
[2]: ./media/cloud-services-vs-ci/file-01.png
[3]: ./media/cloud-services-vs-ci/vs-03.png
[4]: ./media/cloud-services-vs-ci/vs-04.png
[5]: ./media/cloud-services-vs-ci/vs-05.png
[6]: ./media/cloud-services-vs-ci/vs-06.png
[7]: ./media/cloud-services-vs-ci/vs-07.png
[8]: ./media/cloud-services-vs-ci/vs-08.png
[9]: ./media/cloud-services-vs-ci/vs-09.png
[10]: ./media/cloud-services-vs-ci/vso-01.png
[11]: ./media/cloud-services-vs-ci/vso-02.png
[12]: ./media/cloud-services-vs-ci/vso-03.png
[13]: ./media/cloud-services-vs-ci/vso-04.png
[14]: ./media/cloud-services-vs-ci/vso-05.png
[15]: ./media/cloud-services-vs-ci/vso-06.png
[16]: ./media/cloud-services-vs-ci/vso-07.png
[17]: ./media/cloud-services-vs-ci/vso-08.png
[18]: ./media/cloud-services-vs-ci/vso-09.png
[19]: ./media/cloud-services-vs-ci/vso-10.png
[20]: ./media/cloud-services-vs-ci/vso-11.png
[21]: ./media/cloud-services-vs-ci/vso-12.png
[22]: ./media/cloud-services-vs-ci/vso-13.png
[23]: ./media/cloud-services-vs-ci/vso-14.png
[24]: ./media/cloud-services-vs-ci/vso-15.png
