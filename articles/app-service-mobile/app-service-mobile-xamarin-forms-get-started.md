---
title: "aaaGet a trabajar con aplicaciones móviles mediante el uso de Xamarin.Forms"
description: "Siga este tutorial toostart con aplicaciones móviles para el desarrollo de Xamarin.Forms"
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="c79a0-103">Creación de una aplicación Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="c79a0-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="c79a0-104">Información general</span><span class="sxs-lookup"><span data-stu-id="c79a0-104">Overview</span></span>
<span data-ttu-id="c79a0-105">Este tutorial muestra cómo tooadd una aplicación móvil de servicio de back-end basado en la nube tooa Xamarin.Forms mediante el uso de Hola característica de aplicaciones móviles de servicio de aplicaciones de Azure como back-end de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="c79a0-106">Va a crear tanto un back-end de Mobile Apps nuevo como una aplicación Xamarin.Forms simple de la lista de tareas pendientes que almacene los datos de la aplicación en Azure.</span><span class="sxs-lookup"><span data-stu-id="c79a0-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="c79a0-107">Completar este tutorial es un requisito previo para todos los tutoriales de aplicaciones móviles para aplicaciones Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="c79a0-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c79a0-108">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c79a0-108">Prerequisites</span></span>
<span data-ttu-id="c79a0-109">toocomplete este tutorial, necesita Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c79a0-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c79a0-110">Una cuenta de Azure activa.</span><span class="sxs-lookup"><span data-stu-id="c79a0-110">An active Azure account.</span></span> <span data-ttu-id="c79a0-111">Si no tiene una cuenta, puede registrarse para obtener una evaluación de Azure y desarrollar aplicaciones móviles gratuitas too10 que puede seguir usando incluso después de la prueba finaliza.</span><span class="sxs-lookup"><span data-stu-id="c79a0-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="c79a0-112">Para más información, consulte [Obtener una evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c79a0-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="c79a0-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="c79a0-114">Para obtener información, vea hello [establecer una copia de seguridad e instale Visual Studio y Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="c79a0-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="c79a0-115">Un equipo Mac con Xcode v7.0 o versiones posteriores y Xamarin Studio Community instalados.</span><span class="sxs-lookup"><span data-stu-id="c79a0-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="c79a0-116">Para más información, consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) de Visual Studio y Xamarin, y [Configuración, instalación y comprobaciones para usuarios de Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="c79a0-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="c79a0-117">Creación de un back-end de Mobile Apps</span><span class="sxs-lookup"><span data-stu-id="c79a0-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="c79a0-118">toocreate finalizar volver un nuevas aplicaciones móviles, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c79a0-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="c79a0-119">Ya ha configurado un back-end de Mobile Apps que puede usar con las aplicaciones cliente móviles.</span><span class="sxs-lookup"><span data-stu-id="c79a0-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="c79a0-120">A continuación, descargar un proyecto de servidor para un tarea simple lista back-end y, a continuación, publicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="c79a0-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="c79a0-121">Configurar el proyecto de servidor hello</span><span class="sxs-lookup"><span data-stu-id="c79a0-121">Configure hello server project</span></span>

<span data-ttu-id="c79a0-122">toouse del proyecto de servidor de tooconfigure Hola Hola Node.js o .NET back-end, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c79a0-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="c79a0-123">Descargue y ejecute la solución de Xamarin.Forms Hola</span><span class="sxs-lookup"><span data-stu-id="c79a0-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="c79a0-124">Puede descargar la solución de hello en cualquiera de estas dos maneras.</span><span class="sxs-lookup"><span data-stu-id="c79a0-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="c79a0-125">Descargar tooa Mac y abrirlo en Xamarin Studio, o descargar tooa equipo con Windows y ábralo en Visual Studio mediante el uso de un Mac conectado en red para la creación de la aplicación de iOS de hello.</span><span class="sxs-lookup"><span data-stu-id="c79a0-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="c79a0-126">Para más información, consulte [Configuración e instalación](https://msdn.microsoft.com/library/mt613162.aspx) de Visual Studio y Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="c79a0-127">En un equipo Mac o Windows, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="c79a0-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="c79a0-128">Vaya toohello [portal de Azure].</span><span class="sxs-lookup"><span data-stu-id="c79a0-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="c79a0-129">En hello **configuración** hoja para su aplicación móvil, en **Mobile**, seleccione **Introducción** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="c79a0-130">En el **paso 3**, seleccione **Crear aplicación** y, después, seleccione **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="c79a0-131">Esta acción descarga un proyecto que contenga una aplicación cliente que está conectado tooyour aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="c79a0-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="c79a0-132">Guardar el equipo local del tooyour de archivo comprimido proyectos hello y tome nota donde se guarda.</span><span class="sxs-lookup"><span data-stu-id="c79a0-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="c79a0-133">Extraer el proyecto de Hola que ha descargado y, a continuación, ábralo en Xamarin Studio (Mac) o Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="c79a0-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Proyecto extraído en Xamarin Studio][9]

   ![Proyecto extraído en Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="c79a0-136">(Opcional) Ejecute el proyecto de iOS de Hola</span><span class="sxs-lookup"><span data-stu-id="c79a0-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="c79a0-137">En esta sección, se ejecuta el proyecto de iOS de Xamarin de Hola para dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="c79a0-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="c79a0-138">Puede omitir esta sección si no está trabajando con dispositivos iOS.</span><span class="sxs-lookup"><span data-stu-id="c79a0-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="c79a0-139">En Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="c79a0-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="c79a0-140">Haga clic en proyecto de iOS de hello y, a continuación, seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="c79a0-141">En hello **ejecutar** menú, seleccione **Iniciar depuración** toobuild Hola proyecto e iniciar aplicación hello en el emulador de iPhone Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="c79a0-142">En Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c79a0-142">In Visual Studio</span></span>
1. <span data-ttu-id="c79a0-143">Haga clic en proyecto de iOS de hello y, a continuación, seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="c79a0-144">En hello **generar** menú, seleccione **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="c79a0-145">Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** proyecto de iOS de toohello siguiente de casillas de verificación.</span><span class="sxs-lookup"><span data-stu-id="c79a0-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="c79a0-146">toobuild Hola proyecto e iniciar aplicación hello en emulador de iPhone de hello, seleccione hello **F5** clave.</span><span class="sxs-lookup"><span data-stu-id="c79a0-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c79a0-147">Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="c79a0-148">Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.</span><span class="sxs-lookup"><span data-stu-id="c79a0-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="c79a0-149">En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).</span><span class="sxs-lookup"><span data-stu-id="c79a0-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="c79a0-150">Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure.</span><span class="sxs-lookup"><span data-stu-id="c79a0-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="c79a0-151">Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="c79a0-152">Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c79a0-153">Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.</span><span class="sxs-lookup"><span data-stu-id="c79a0-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="c79a0-154">(Opcional) Ejecute el proyecto de Android Hola</span><span class="sxs-lookup"><span data-stu-id="c79a0-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="c79a0-155">En esta sección, se ejecuta el proyecto de droid de Xamarin de Hola para Android.</span><span class="sxs-lookup"><span data-stu-id="c79a0-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="c79a0-156">Puede omitir esta sección si no está trabajando con dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="c79a0-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="c79a0-157">En Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="c79a0-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="c79a0-158">Haga clic en proyecto de Android de hello y, a continuación, seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="c79a0-159">toobuild Hola proyecto e iniciar aplicación hello en un emulador de Android en hello **ejecutar** menú, seleccione **Iniciar depuración**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="c79a0-160">En Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c79a0-160">In Visual Studio</span></span>

1. <span data-ttu-id="c79a0-161">Haga clic en proyecto de Android (Droid) de hello y, a continuación, seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="c79a0-162">En hello **generar** menú, seleccione **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="c79a0-163">Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** casillas de verificación siguiente toohello proyecto Android.</span><span class="sxs-lookup"><span data-stu-id="c79a0-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="c79a0-164">toobuild Hola proyecto e iniciar aplicación hello en un emulador de Android, seleccione hello **F5** clave.</span><span class="sxs-lookup"><span data-stu-id="c79a0-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c79a0-165">Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="c79a0-166">Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.</span><span class="sxs-lookup"><span data-stu-id="c79a0-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="c79a0-167">En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).</span><span class="sxs-lookup"><span data-stu-id="c79a0-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="c79a0-168">Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure.</span><span class="sxs-lookup"><span data-stu-id="c79a0-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="c79a0-169">Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="c79a0-170">Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c79a0-171">Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.</span><span class="sxs-lookup"><span data-stu-id="c79a0-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="c79a0-172">(Opcional) Ejecute el proyecto de Windows hello</span><span class="sxs-lookup"><span data-stu-id="c79a0-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="c79a0-173">En esta sección, ejecute hello proyecto Xamarin WinApp para dispositivos de Windows.</span><span class="sxs-lookup"><span data-stu-id="c79a0-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="c79a0-174">Puede omitir esta sección si no está trabajando con dispositivos Windows.</span><span class="sxs-lookup"><span data-stu-id="c79a0-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="c79a0-175">En Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c79a0-175">In Visual Studio</span></span>

1. <span data-ttu-id="c79a0-176">Haga clic en cualquiera de los proyectos de Windows hello y, a continuación, seleccione **establecer como proyecto de inicio**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="c79a0-177">En hello **generar** menú, seleccione **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="c79a0-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="c79a0-178">Hola **Configuration Manager** cuadro de diálogo, seleccione hello **generar** y **implementar** casillas de verificación siguiente toohello proyecto de Windows que eligió.</span><span class="sxs-lookup"><span data-stu-id="c79a0-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="c79a0-179">toobuild Hola proyecto e iniciar aplicación hello en un emulador de Windows, seleccione hello **F5** clave.</span><span class="sxs-lookup"><span data-stu-id="c79a0-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c79a0-180">Si tiene problemas para crear el proyecto de hello, ejecute hello NuGet paquete manager y actualización toohello última versión de los paquetes de soporte técnico de hello Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="c79a0-181">Proyectos de inicio rápido podrían ser lenta tooupdate toohello últimas versiones.</span><span class="sxs-lookup"><span data-stu-id="c79a0-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="c79a0-182">En la aplicación hello, escriba texto significativo, como *Obtenga información acerca de Xamarin*, y, a continuación, seleccione Hola signo (**+**).</span><span class="sxs-lookup"><span data-stu-id="c79a0-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="c79a0-183">Esta acción envía un toohello de solicitud de post que nuevas aplicaciones de Mobile back-end que se hospeda en Azure.</span><span class="sxs-lookup"><span data-stu-id="c79a0-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="c79a0-184">Datos de solicitud de saludo se insertan en la tabla TodoItem de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="c79a0-185">Elementos que se almacenan en la tabla de Hola se devuelven por hello aplicaciones móviles volver finalizar y Hola datos se muestran en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="c79a0-186">Puede encontrar código de hello que tiene acceso a su aplicaciones móviles de back-end en hello TodoItemManager.cs C# archivo de proyecto de biblioteca de clases portables hello de la solución.</span><span class="sxs-lookup"><span data-stu-id="c79a0-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="c79a0-187">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c79a0-187">Next steps</span></span>

* [<span data-ttu-id="c79a0-188">Agregar aplicación de autenticación tooyour</span><span class="sxs-lookup"><span data-stu-id="c79a0-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="c79a0-189">Obtenga información acerca de cómo tooauthenticate a los usuarios de la aplicación con un proveedor de identidades.</span><span class="sxs-lookup"><span data-stu-id="c79a0-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="c79a0-190">Agregar aplicación de tooyour de notificaciones de inserción</span><span class="sxs-lookup"><span data-stu-id="c79a0-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="c79a0-191">Obtenga información acerca de cómo las notificaciones de inserción de tooadd son compatibles con la aplicación tooyour y configurar las notificaciones de inserción de aplicaciones móviles back-end toouse centros de notificaciones de Azure toosend Hola.</span><span class="sxs-lookup"><span data-stu-id="c79a0-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="c79a0-192">Activación de la sincronización sin conexión para la aplicación de Windows</span><span class="sxs-lookup"><span data-stu-id="c79a0-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="c79a0-193">Obtenga información acerca de cómo tooadd compatibilidad sin conexión para la aplicación mediante el uso de aplicaciones móviles de un back-end.</span><span class="sxs-lookup"><span data-stu-id="c79a0-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="c79a0-194">Con la sincronización sin conexión, podrá ver, agregar o modificar los datos en la aplicación móvil, incluso cuando no hay ninguna conexión de red.</span><span class="sxs-lookup"><span data-stu-id="c79a0-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="c79a0-195">Usar el cliente administrado de Hola para aplicaciones móviles</span><span class="sxs-lookup"><span data-stu-id="c79a0-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="c79a0-196">Obtenga información acerca de cómo toowork con hello administra SDK del cliente de la aplicación de Xamarin.</span><span class="sxs-lookup"><span data-stu-id="c79a0-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portal de Azure]: https://portal.azure.com/
