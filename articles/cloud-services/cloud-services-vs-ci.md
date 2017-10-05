---
title: Entrega continua para Cloud Services con Visual Studio Online | Microsoft Docs
description: "Obtenga información acerca de cómo configurar la entrega continua para aplicaciones en la nube de Azure sin guardar la clave de almacenamiento de la información de diagnóstico en los archivos de configuración de servicio"
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
ms.openlocfilehash: 7e70f92d4d1333ca6cbac5876e5ccbc763bd915c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="securely-save-cloud-services-diagnostics-storage-key-and-setup-continuous-integration-and-deployment-to-azure-using-visual-studio-online"></a><span data-ttu-id="88e9c-103">Guarde de forma segura la clave de almacenamiento de la información de diagnóstico de Cloud Services y configure la integración e implementación continua en Azure mediante Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="88e9c-103">Securely Save Cloud Services Diagnostics Storage Key and Setup Continuous Integration and Deployment to Azure using Visual Studio Online</span></span>
 <span data-ttu-id="88e9c-104">Es una práctica común para abrir proyectos de código fuente hoy en día.</span><span class="sxs-lookup"><span data-stu-id="88e9c-104">It is a common practice to open source projects nowadays.</span></span> <span data-ttu-id="88e9c-105">Guardar los secretos de aplicación en archivos de configuración ya no es una práctica segura, ya que se producen vulnerabilidades de seguridad procedentes de los secretos que se filtran desde los controles de código fuente públicos.</span><span class="sxs-lookup"><span data-stu-id="88e9c-105">Saving application secrets in configuration files is no longer safe practice as security vulnerabilities are exposed from secrets being leaked from public source controls.</span></span> <span data-ttu-id="88e9c-106">Almacenar el secreto como texto no cifrado en un archivo de una canalización de integración continua no es seguro ya que los servidores de compilación podrían convertirse en recursos compartidos en el entorno en la nube.</span><span class="sxs-lookup"><span data-stu-id="88e9c-106">Storing secret as plaintext in a file in a Continuous Integration pipeline is not secure either since build servers could be shared resources on the Cloud environment.</span></span> <span data-ttu-id="88e9c-107">Este artículo explica cómo Visual Studio y Visual Studio Online mitiga los problemas de seguridad durante el desarrollo y el proceso de integración continua.</span><span class="sxs-lookup"><span data-stu-id="88e9c-107">This article explains how Visual Studio and Visual Studio Online mitigates the security concerns during development and Continuous Integration process.</span></span>

## <a name="remove-diagnostics-storage-key-secret-in-project-configuration-file"></a><span data-ttu-id="88e9c-108">Eliminación del secreto de la clave de almacenamiento de la información de diagnóstico del archivo de configuración de proyecto</span><span class="sxs-lookup"><span data-stu-id="88e9c-108">Remove Diagnostics Storage Key Secret in Project Configuration File</span></span>
<span data-ttu-id="88e9c-109">La extensión de diagnósticos de Cloud Services requiere Azure Storage para guardar los resultados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="88e9c-109">Cloud Services diagnostics extension requires Azure storage for saving diagnostics results.</span></span> <span data-ttu-id="88e9c-110">Anteriormente, la cadena de conexión de almacenamiento se especificaba en los archivos de configuración (.cscfg) de Cloud Services y podría incorporarse al control de código fuente.</span><span class="sxs-lookup"><span data-stu-id="88e9c-110">Formerly the storage connection string is specified in the Cloud Services configuration (.cscfg) files and could be checked in to source control.</span></span> <span data-ttu-id="88e9c-111">En la versión más reciente de Azure SDK se ha cambiado el comportamiento de forma que solo se almacena una cadena de conexión parcial y la clave se sustituye por un token.</span><span class="sxs-lookup"><span data-stu-id="88e9c-111">In the latest Azure SDK release we changed the behavior to only store a partial connection string with the key replaced by a token.</span></span> <span data-ttu-id="88e9c-112">Los siguientes pasos describen el funcionamiento de las nuevas herramientas de Cloud Services:</span><span class="sxs-lookup"><span data-stu-id="88e9c-112">The following steps describe how the new Cloud Services tooling works:</span></span>

### <a name="1-open-the-role-designer"></a><span data-ttu-id="88e9c-113">1. Apertura del diseñador de roles</span><span class="sxs-lookup"><span data-stu-id="88e9c-113">1. Open the Role designer</span></span>
* <span data-ttu-id="88e9c-114">Haga doble clic o haga clic con el botón secundario en un rol de Cloud Services para abrir el diseñador de roles</span><span class="sxs-lookup"><span data-stu-id="88e9c-114">Double click or right click on a Cloud Services role to open Role designer</span></span>

![Abra el diseñador de roles][0]

### <a name="2-under-diagnostics-section-a-new-check-box-dont-remove-storage-key-secret-from-project-is-added"></a><span data-ttu-id="88e9c-116">2. En la sección de diagnósticos, se ha agregado una nueva casilla de verificación "Don’t remove storage key secret from project" (No quitar secreto de la clave de almacenamiento del proyecto)</span><span class="sxs-lookup"><span data-stu-id="88e9c-116">2. Under diagnostics section, a new check box “Don’t remove storage key secret from project” is added</span></span>
* <span data-ttu-id="88e9c-117">Si está utilizando el emulador de almacenamiento local, esta casilla está deshabilitada porque no hay ningún secreto que administrar para la cadena de conexión local, que es UseDevelopmentStorage=true.</span><span class="sxs-lookup"><span data-stu-id="88e9c-117">If you are using the local storage emulator, this checkbox is disabled because there is no secret to manage for the local connection string, which is UseDevelopmentStorage=true.</span></span>

![La cadena de conexión del emulador de almacenamiento local no es un secreto][1]

* <span data-ttu-id="88e9c-119">Si va a crear un nuevo proyecto, esta casilla de verificación estará desactivada de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="88e9c-119">If you are creating a new project, by default this checkbox is unchecked.</span></span> <span data-ttu-id="88e9c-120">Esto da como resultado que la sección de clave de almacenamiento de la cadena de conexión de almacenamiento seleccionada se sustituye por un token.</span><span class="sxs-lookup"><span data-stu-id="88e9c-120">This results in the storage key section of the selected storage connection string being replaced with a token.</span></span> <span data-ttu-id="88e9c-121">El valor del token se encuentra en la carpeta AppData Roaming actual del usuario, por ejemplo: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span><span class="sxs-lookup"><span data-stu-id="88e9c-121">The value of the token will be found under the current user’s AppData Roaming folder, for example: C:\Users\contosouser\AppData\Roaming\Microsoft\CloudService</span></span>

> <span data-ttu-id="88e9c-122">Tenga en cuenta que la carpeta user\AppData tiene un acceso controlado mediante el inicio de sesión de usuario y se considera un lugar seguro para almacenar secretos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="88e9c-122">Note that the user\AppData folder is Access Controlled by user sign-in and is considered a secure place to store development secrets.</span></span>
> 
> 

![La clave de almacenamiento se guarda en la carpeta del perfil de usuario][2]

### <a name="3-select-a-diagnostics-storage-account"></a><span data-ttu-id="88e9c-124">3. Selección de la cuenta de almacenamiento de información de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="88e9c-124">3. Select a diagnostics storage account</span></span>
* <span data-ttu-id="88e9c-125">Seleccione una cuenta de almacenamiento en el cuadro de diálogo que se inicia haciendo clic en el botón "..."</span><span class="sxs-lookup"><span data-stu-id="88e9c-125">Select a storage account from the dialog launched by clicking the “…”</span></span> <span data-ttu-id="88e9c-126">.</span><span class="sxs-lookup"><span data-stu-id="88e9c-126">button.</span></span> <span data-ttu-id="88e9c-127">Observe cómo la cadena de conexión de almacenamiento generada no tendrá la clave de cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="88e9c-127">Notice how the storage connection string generated will not have the storage account key.</span></span>
* <span data-ttu-id="88e9c-128">Por ejemplo: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span><span class="sxs-lookup"><span data-stu-id="88e9c-128">For example: DefaultEndpointsProtocol=https;AccountName=contosostorage;AccountKey=$(*clouddiagstrg.key*)</span></span>

### <a name="4----debugging-the-project"></a><span data-ttu-id="88e9c-129">4.    Depuración del proyecto</span><span class="sxs-lookup"><span data-stu-id="88e9c-129">4.    Debugging the project</span></span>
* <span data-ttu-id="88e9c-130">Presione F5 para empezar la depuración en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="88e9c-130">F5 to start debugging in Visual Studio.</span></span> <span data-ttu-id="88e9c-131">Todo debería funcionar de la misma manera que antes.</span><span class="sxs-lookup"><span data-stu-id="88e9c-131">Everything should work in the same way as before.</span></span>
  <span data-ttu-id="88e9c-132">![Inicie la depuración localmente][3]</span><span class="sxs-lookup"><span data-stu-id="88e9c-132">![Start debugging locally][3]</span></span>

### <a name="5-publish-project-from-visual-studio"></a><span data-ttu-id="88e9c-133">5. Publicación del proyecto desde Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88e9c-133">5. Publish project from Visual Studio</span></span>
* <span data-ttu-id="88e9c-134">Inicie el cuadro de diálogo Publicar y continúe con las instrucciones de inicio de sesión para publicar la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="88e9c-134">Launch the publish dialog and proceed with sign-in instructions to publish the applicaion to Azure.</span></span>

### <a name="6-additional-information"></a><span data-ttu-id="88e9c-135">6. Información adicional</span><span class="sxs-lookup"><span data-stu-id="88e9c-135">6. Additional information</span></span>
> <span data-ttu-id="88e9c-136">Nota: El panel de configuración del diseñador de roles permanecerá igual que está ahora.</span><span class="sxs-lookup"><span data-stu-id="88e9c-136">Note: The Settings panel in the role designer will stay as it is for now.</span></span> <span data-ttu-id="88e9c-137">Si desea utilizar la característica de administración de secretos para diagnósticos, vaya a la pestaña de configuraciones.</span><span class="sxs-lookup"><span data-stu-id="88e9c-137">If you want to use the secret management feature for diagnostics, go to the Configurations tab.</span></span>
> 
> 

![Incorporación de la configuración][4]

> <span data-ttu-id="88e9c-139">Nota: Si está habilitada, se almacenará la clave de Application Insights como texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="88e9c-139">Note: If enabled, the Application Insights key will be stored as plain text.</span></span> <span data-ttu-id="88e9c-140">La clave solo se utiliza para los contenidos de carga, de modo que no se ve comprometida la seguridad de ningún dato confidencial.</span><span class="sxs-lookup"><span data-stu-id="88e9c-140">The key is only used for upload contents so no sensitive data will be at risk being compromised.</span></span>
> 
> 

## <a name="build-and-publish-a-cloud-services-project-using-visual-studio-online-task-templates"></a><span data-ttu-id="88e9c-141">Compilación y publicación de un proyecto de Cloud Services mediante plantillas de tareas en Visual Studio Online</span><span class="sxs-lookup"><span data-stu-id="88e9c-141">Build and Publish a Cloud Services Project using Visual Studio online Task Templates</span></span>
* <span data-ttu-id="88e9c-142">Los pasos siguientes muestran cómo configurar la integración continua para proyectos de Cloud Services con tareas de Visual Studio Online:</span><span class="sxs-lookup"><span data-stu-id="88e9c-142">The following steps illustrates how to setup Continuous Integration for Cloud Services project using Visual Studio online tasks:</span></span>
  ### <a name="1----obtain-a-vso-account"></a><span data-ttu-id="88e9c-143">1.    Obtenga una cuenta de VSO</span><span class="sxs-lookup"><span data-stu-id="88e9c-143">1.    Obtain a VSO account</span></span>
* <span data-ttu-id="88e9c-144">[Crear cuenta de Visual Studio Online] [ Create Visual Studio Online account] si aún no tiene uno</span><span class="sxs-lookup"><span data-stu-id="88e9c-144">[Create Visual Studio Online account][Create Visual Studio Online account] if you don’t have one already</span></span>
* <span data-ttu-id="88e9c-145">[Crear proyecto de equipo] [ Create team project] en su cuenta en línea de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88e9c-145">[Create team project][Create team project] in your Visual Studio online account</span></span>

### <a name="2----setup-source-control-in-visual-studio"></a><span data-ttu-id="88e9c-146">2.    Configuración del control de código fuente en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="88e9c-146">2.    Setup source control in Visual Studio</span></span>
* <span data-ttu-id="88e9c-147">Conéctese a un proyecto de equipo</span><span class="sxs-lookup"><span data-stu-id="88e9c-147">Connect to a team project</span></span>

![Conéctese a un proyecto de equipo][5]

![Seleccione el proyecto de equipo al que conectarse][6]

* <span data-ttu-id="88e9c-150">Agregue el proyecto al control de código fuente</span><span class="sxs-lookup"><span data-stu-id="88e9c-150">Add your project to source control</span></span>

![Agregue el proyecto al control de código fuente][7]

![Asigne el proyecto a una carpeta de control de código fuente][8]

* <span data-ttu-id="88e9c-153">Compruebe el proyecto desde Team Explorer</span><span class="sxs-lookup"><span data-stu-id="88e9c-153">Check in your project from Team Explorer</span></span>

![Proteja un proyecto en el control de código fuente][9]

### <a name="3----configure-build-process"></a><span data-ttu-id="88e9c-155">3.    Configuración del proceso de compilación</span><span class="sxs-lookup"><span data-stu-id="88e9c-155">3.    Configure Build process</span></span>
* <span data-ttu-id="88e9c-156">Vaya al proyecto de equipo y agregue un nuevo proceso de compilación, Templates</span><span class="sxs-lookup"><span data-stu-id="88e9c-156">Browse to your team project and add a new build process Templates</span></span>

![Agregue una nueva compilación][10]

* <span data-ttu-id="88e9c-158">Seleccione una tarea de compilación</span><span class="sxs-lookup"><span data-stu-id="88e9c-158">Select build task</span></span>

![Agregue una tarea de compilación][11]

![Seleccione la plantilla de tarea de compilación de Visual Studio][12]

* <span data-ttu-id="88e9c-161">Edite la entrada de la tarea de compilación.</span><span class="sxs-lookup"><span data-stu-id="88e9c-161">Edit build task input.</span></span> <span data-ttu-id="88e9c-162">Personalice los parámetros de compilación según sus necesidades</span><span class="sxs-lookup"><span data-stu-id="88e9c-162">Please customize the build parameters according to your need</span></span>

![Configure la tarea de compilación][13]

`/t:Publish /p:TargetProfile=$(targetProfile) /p:DebugType=None /p:SkipInvalidConfigurations=true /p:OutputPath=bin\ /p:PublishDir="$(build.artifactstagingdirectory)\\"`

* <span data-ttu-id="88e9c-164">Configure las variables de compilación</span><span class="sxs-lookup"><span data-stu-id="88e9c-164">Configure build variables</span></span>

![Configure las variables de compilación][14]

* <span data-ttu-id="88e9c-166">Agregue una tarea para cargar el destino de compilación</span><span class="sxs-lookup"><span data-stu-id="88e9c-166">Add a task to upload build drop</span></span>

![Elija publicar tarea de destino de compilación][15]

![Configure la tarea de publicación de destino de compilación][16]

* <span data-ttu-id="88e9c-169">Ejecute la compilación</span><span class="sxs-lookup"><span data-stu-id="88e9c-169">Run the build</span></span>

![Ponga en cola la nueva compilación][17]

![Vea el resumen de compilación][18]

* <span data-ttu-id="88e9c-172">Si la compilación se ha realizado correctamente, verá un resultado parecido al siguiente</span><span class="sxs-lookup"><span data-stu-id="88e9c-172">if the build is successful you will see a result similar to below</span></span>

![Resultado de la compilación][19]

### <a name="4----configure-release-process"></a><span data-ttu-id="88e9c-174">4.    Configuración del proceso de lanzamiento</span><span class="sxs-lookup"><span data-stu-id="88e9c-174">4.    Configure Release process</span></span>
* <span data-ttu-id="88e9c-175">Cree una nueva versión</span><span class="sxs-lookup"><span data-stu-id="88e9c-175">Create a new release</span></span>

![Cree una nueva versión][20]

* <span data-ttu-id="88e9c-177">Seleccione la tarea de implementación de Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="88e9c-177">Select the Azure Cloud Services Deployment task</span></span>

![Seleccione la tarea de implementación de Azure Cloud Services][21]

* <span data-ttu-id="88e9c-179">Como la clave de la cuenta de almacenamiento no está activada en el control de código fuente, es preciso especificar la clave secreta para establecer las extensiones de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="88e9c-179">As the storage account key is not checked in to source control, we need to specify the secret key for setting diagnostics extensions.</span></span> <span data-ttu-id="88e9c-180">Expanda la sección **Opciones avanzadas para Creación de un nuevo servicio** y edite la entrada de parámetro de **claves de cuenta de almacenamiento de información de diagnósticos**.</span><span class="sxs-lookup"><span data-stu-id="88e9c-180">Expand the **Advanced Options for Creating New Service** section and edit the **Diagnostics Storage Account Keys** parameter input.</span></span> <span data-ttu-id="88e9c-181">Esta entrada ocupa varias líneas de par clave-valor con el formato **[RoleName]:$(StorageAccountKey)**</span><span class="sxs-lookup"><span data-stu-id="88e9c-181">This input takes in multiple lines of key value pair in the format of **[RoleName]:$(StorageAccountKey)**</span></span>

> <span data-ttu-id="88e9c-182">Nota: Si la cuenta de almacenamiento de información de diagnóstico pertenece a la misma suscripción en la que publicará la aplicación de Cloud Services, no es necesario que introduzca la clave de la entrada de la tarea de implementación. La implementación obtendrá mediante programación la información de almacenamiento de la suscripción</span><span class="sxs-lookup"><span data-stu-id="88e9c-182">Note: if your diagnostics storage account is under the same subscription as where you will publish the Cloud Services application, you don't have to enter the key in the deployment task input; the deployment will programmatically obtain the storage information from your subscription</span></span>
> 
> 

![Configuración de la tarea de implementación de Azure Cloud Services][22]

* <span data-ttu-id="88e9c-184">Use variables de compilación de secretos para guardar las claves de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="88e9c-184">Use secret build variables to save storage Keys.</span></span> <span data-ttu-id="88e9c-185">Para enmascarar una variable como secreto, haga clic en el icono de bloqueo en el lado derecho de la entrada Variables</span><span class="sxs-lookup"><span data-stu-id="88e9c-185">To mask a variable as secret click on the lock icon on the right side of the Variables input</span></span>

![Guardar las claves de almacenamiento en variables de compilación de secreto][23]

* <span data-ttu-id="88e9c-187">Cree una versión e implemente el proyecto en Azure</span><span class="sxs-lookup"><span data-stu-id="88e9c-187">Create a release and deploy your project to Azure</span></span>

![Cree una nueva versión][24]

## <a name="next-steps"></a><span data-ttu-id="88e9c-189">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="88e9c-189">Next steps</span></span>
<span data-ttu-id="88e9c-190">Para más información sobre la configuración de extensiones de diagnóstico para los servicios de nube de Azure, consulte [habilitar diagnósticos en los servicios de nube de Azure con PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span><span class="sxs-lookup"><span data-stu-id="88e9c-190">To learn more about setting diagnostics extensions for Azure Cloud Services, please see [Enable diagnostics in Azure Cloud Services using PowerShell][Enable diagnostics in Azure Cloud Services using PowerShell]</span></span>

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
