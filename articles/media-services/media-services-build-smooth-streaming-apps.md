---
title: "Tutorial de aplicación de tienda de Windows de la transmisión por secuencias aaaSmooth | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse servicios multimedia de Azure toocreate una aplicación de tienda de Windows de C# con un elemento XML MediaElement controlar el contenido de transmisión por secuencias suave de tooplayback."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 0fa5d8c5-3d5f-4886-ae55-fb6de4f5256d
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: juliako
ms.openlocfilehash: b02aa2c7f68fe22a23ea846d72fdd23bfba2b19c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a><span data-ttu-id="97269-103">¿Cómo tooBuild una aplicación Smooth Streaming Windows Store</span><span class="sxs-lookup"><span data-stu-id="97269-103">How tooBuild a Smooth Streaming Windows Store Application</span></span>

<span data-ttu-id="97269-104">Hola Smooth Streaming Client SDK para Windows 8 permite que las aplicaciones de tienda Windows de toobuild a los desarrolladores que pueden reproducir contenido de transmisión por secuencias suave a petición y en directo.</span><span class="sxs-lookup"><span data-stu-id="97269-104">hello Smooth Streaming Client SDK for Windows 8 enables developers toobuild Windows Store applications that can play on-demand and live Smooth Streaming content.</span></span> <span data-ttu-id="97269-105">Además toohello básica reproducción de Smooth Streaming de contenido, Hola SDK también proporciona características avanzadas como la protección de Microsoft PlayReady, restricción del nivel de calidad, Live DVR, la secuencia de audio de conmutación, realizar escuchas para las actualizaciones de estado (por ejemplo, los cambios de nivel de calidad ) y eventos de error y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="97269-105">In addition toohello basic playback of Smooth Streaming content, hello SDK also provides rich features like Microsoft PlayReady protection, quality level restriction, Live DVR, audio stream switching, listening for status updates (such as quality level changes) and error events, and so on.</span></span> <span data-ttu-id="97269-106">Para obtener más información de características de hello compatibles, vea hello [notas de la versión](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span><span class="sxs-lookup"><span data-stu-id="97269-106">For more information of hello supported features, see hello [release notes](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes).</span></span> <span data-ttu-id="97269-107">Para más información, vea [Player Framework para Windows 8](http://playerframework.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="97269-107">For more information, see [Player Framework for Windows 8](http://playerframework.codeplex.com/).</span></span> 

<span data-ttu-id="97269-108">Este tutorial contiene cuatro lecciones:</span><span class="sxs-lookup"><span data-stu-id="97269-108">This tutorial contains four lessons:</span></span>

1. <span data-ttu-id="97269-109">Creación de una aplicación básica de Tienda de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-109">Create a Basic Smooth Streaming Store Application</span></span>
2. <span data-ttu-id="97269-110">Agregar un control deslizante barra tooControl Hola progreso de medios</span><span class="sxs-lookup"><span data-stu-id="97269-110">Add a Slider Bar tooControl hello Media Progress</span></span>
3. <span data-ttu-id="97269-111">Selección de secuencias de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-111">Select Smooth Streaming Streams</span></span>
4. <span data-ttu-id="97269-112">Selección de pistas de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-112">Select Smooth Streaming Tracks</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97269-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="97269-113">Prerequisites</span></span>
* <span data-ttu-id="97269-114">Windows 8 de 32 o 64 bits.</span><span class="sxs-lookup"><span data-stu-id="97269-114">Windows 8 32-bit or 64-bit.</span></span> <span data-ttu-id="97269-115">Puede conseguir la [Evaluación de Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) en MSDN.</span><span class="sxs-lookup"><span data-stu-id="97269-115">You can get [Windows 8 Enterprise Evaluation](http://msdn.microsoft.com/evalcenter/jj554510.aspx) from MSDN.</span></span>
* <span data-ttu-id="97269-116">Visual Studio 2012 o Visual Studio Express 2012 (o una versión posterior).</span><span class="sxs-lookup"><span data-stu-id="97269-116">Visual Studio 2012 or Visual Studio Express 2012 (or a later version).</span></span> <span data-ttu-id="97269-117">Puede obtener la versión de prueba de hello [aquí](http://www.microsoft.com/visualstudio/11/downloads).</span><span class="sxs-lookup"><span data-stu-id="97269-117">You can get hello trial version from [here](http://www.microsoft.com/visualstudio/11/downloads).</span></span>
* <span data-ttu-id="97269-118">[SDK de cliente Smooth Streaming de Microsoft para Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span><span class="sxs-lookup"><span data-stu-id="97269-118">[Microsoft Smooth Streaming Client SDK for Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).</span></span>

<span data-ttu-id="97269-119">solución de Hello completado de cada lección puede descargarse de ejemplos de código para desarrolladores de MSDN (Galería de código):</span><span class="sxs-lookup"><span data-stu-id="97269-119">hello completed solution for each lesson can be downloaded from MSDN Developer Code Samples (Code Gallery):</span></span> 

* <span data-ttu-id="97269-120">[Lección 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : Un sencillo reproductor multimedia de Smooth Streaming para Windows 8</span><span class="sxs-lookup"><span data-stu-id="97269-120">[Lesson 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) - A Simple Windows 8 Smooth Streaming Media Player,</span></span> 
* <span data-ttu-id="97269-121">[Lección 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : Un sencillo reproductor multimedia de Smooth Streaming para Windows 8 con un control de barra deslizante</span><span class="sxs-lookup"><span data-stu-id="97269-121">[Lesson 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) - A Simple Windows 8 Smooth Streaming Media Player with a Slider Bar Control,</span></span> 
* <span data-ttu-id="97269-122">[Lección 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : Un reproductor multimedia de Smooth Streaming para Windows 8 con selección de secuencias</span><span class="sxs-lookup"><span data-stu-id="97269-122">[Lesson 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) - A Windows 8 Smooth Streaming Media Player with Stream Selection,</span></span>  
* <span data-ttu-id="97269-123">[Lección 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907): Un reproductor multimedia de Smooth Streaming para Windows 8 con selección de pistas</span><span class="sxs-lookup"><span data-stu-id="97269-123">[Lesson 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907)  - A Windows 8 Smooth Streaming Media Player with Track Selection.</span></span>

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a><span data-ttu-id="97269-124">Lección 1: Creación de una aplicación básica de Tienda de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-124">Lesson 1: Create a Basic Smooth Streaming Store Application</span></span>

<span data-ttu-id="97269-125">En esta lección, creará una aplicación de tienda Windows con un MediaElement control tooplay transmisión por secuencias suave contenido.</span><span class="sxs-lookup"><span data-stu-id="97269-125">In this lesson, you will create a Windows Store application with a MediaElement control tooplay Smooth Stream content.</span></span>  <span data-ttu-id="97269-126">aplicación en ejecución Hello tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="97269-126">hello running application looks like:</span></span>

![Ejemplo de aplicación de Tienda Windows de Smooth Streaming][PlayerApplication]

<span data-ttu-id="97269-128">Para obtener más información acerca del desarrollo de la aplicación de la Tienda Windows, consulte [Desarrollo de magníficas aplicaciones para Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span><span class="sxs-lookup"><span data-stu-id="97269-128">For more information on developing Windows Store application, see [Develop Great Apps for Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx).</span></span> <span data-ttu-id="97269-129">Esta lección contiene Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="97269-129">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="97269-130">Creación de un proyecto de Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="97269-130">Create a Windows Store project</span></span>
2. <span data-ttu-id="97269-131">Diseñar la interfaz de usuario de hello (XAML)</span><span class="sxs-lookup"><span data-stu-id="97269-131">Design hello user interface (XAML)</span></span>
3. <span data-ttu-id="97269-132">Modificar Hola archivo de código subyacente</span><span class="sxs-lookup"><span data-stu-id="97269-132">Modify hello code behind file</span></span>
4. <span data-ttu-id="97269-133">Compilar y probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="97269-133">Compile and test hello application</span></span>

<span data-ttu-id="97269-134">**toocreate un proyecto de la tienda de Windows**</span><span class="sxs-lookup"><span data-stu-id="97269-134">**toocreate a Windows Store project**</span></span>

1. <span data-ttu-id="97269-135">Ejecute Visual Studio 2012 o posterior.</span><span class="sxs-lookup"><span data-stu-id="97269-135">Run Visual Studio 2012 or later.</span></span>
2. <span data-ttu-id="97269-136">De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.</span><span class="sxs-lookup"><span data-stu-id="97269-136">From hello **FILE** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="97269-137">Del cuadro de diálogo nuevo proyecto de hello, tipo o seleccione hello siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="97269-137">From hello New Project dialog, type or select  hello following values:</span></span>

| <span data-ttu-id="97269-138">Nombre</span><span class="sxs-lookup"><span data-stu-id="97269-138">Name</span></span> | <span data-ttu-id="97269-139">Valor</span><span class="sxs-lookup"><span data-stu-id="97269-139">Value</span></span> |
| --- | --- |
| <span data-ttu-id="97269-140">Grupo de plantillas</span><span class="sxs-lookup"><span data-stu-id="97269-140">Template group</span></span> |<span data-ttu-id="97269-141">Instalado/Plantillas/Visual C#/Tienda Windows</span><span class="sxs-lookup"><span data-stu-id="97269-141">Installed/Templates/Visual C#/Windows Store</span></span> |
| <span data-ttu-id="97269-142">Plantilla</span><span class="sxs-lookup"><span data-stu-id="97269-142">Template</span></span> |<span data-ttu-id="97269-143">Aplicación vacía (XAML)</span><span class="sxs-lookup"><span data-stu-id="97269-143">Blank App (XAML)</span></span> |
| <span data-ttu-id="97269-144">Nombre</span><span class="sxs-lookup"><span data-stu-id="97269-144">Name</span></span> |<span data-ttu-id="97269-145">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="97269-145">SSPlayer</span></span> |
| <span data-ttu-id="97269-146">Ubicación</span><span class="sxs-lookup"><span data-stu-id="97269-146">Location</span></span> |<span data-ttu-id="97269-147">C:\SSTutorials</span><span class="sxs-lookup"><span data-stu-id="97269-147">C:\SSTutorials</span></span> |
| <span data-ttu-id="97269-148">Nombre de la solución</span><span class="sxs-lookup"><span data-stu-id="97269-148">Solution Name</span></span> |<span data-ttu-id="97269-149">SSPlayer</span><span class="sxs-lookup"><span data-stu-id="97269-149">SSPlayer</span></span> |
| <span data-ttu-id="97269-150">Crear directorio para la solución</span><span class="sxs-lookup"><span data-stu-id="97269-150">Create directory for solution</span></span> |<span data-ttu-id="97269-151">(seleccionado)</span><span class="sxs-lookup"><span data-stu-id="97269-151">(selected)</span></span> |

1. <span data-ttu-id="97269-152">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="97269-152">Click **OK**.</span></span>

<span data-ttu-id="97269-153">**tooadd un toohello referencia SDK de cliente de transmisión por secuencias suave**</span><span class="sxs-lookup"><span data-stu-id="97269-153">**tooadd a reference toohello Smooth Streaming Client SDK**</span></span>

1. <span data-ttu-id="97269-154">En el Explorador de soluciones, haga clic con el botón derecho en **SSPlayer** y haga clic en **Agregar referencia**.</span><span class="sxs-lookup"><span data-stu-id="97269-154">From Solution Explorer, right-click **SSPlayer**, and then click **Add Reference**.</span></span>
2. <span data-ttu-id="97269-155">Escriba o seleccione Hola siguientes valores:</span><span class="sxs-lookup"><span data-stu-id="97269-155">Type or select hello following values:</span></span>

| <span data-ttu-id="97269-156">Nombre</span><span class="sxs-lookup"><span data-stu-id="97269-156">Name</span></span> | <span data-ttu-id="97269-157">Valor</span><span class="sxs-lookup"><span data-stu-id="97269-157">Value</span></span> |
| --- | --- |
| <span data-ttu-id="97269-158">Grupo de referencia</span><span class="sxs-lookup"><span data-stu-id="97269-158">Reference group</span></span> |<span data-ttu-id="97269-159">Windows/Extensiones</span><span class="sxs-lookup"><span data-stu-id="97269-159">Windows/Extensions</span></span> |
| <span data-ttu-id="97269-160">Referencia</span><span class="sxs-lookup"><span data-stu-id="97269-160">Reference</span></span> |<span data-ttu-id="97269-161">Seleccione el SDK de cliente Smooth Streaming de Microsoft para Windows 8 y el paquete en tiempo de ejecución de Microsoft Visual C++</span><span class="sxs-lookup"><span data-stu-id="97269-161">Select Microsoft Smooth Streaming Client SDK for Windows 8 and Microsoft Visual C++ Runtime Package</span></span> |

1. <span data-ttu-id="97269-162">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="97269-162">Click **OK**.</span></span> 

<span data-ttu-id="97269-163">Después de agregar las referencias de hello, debe seleccionar la plataforma de destino de hello (x64 o x86), agregar referencias no funcionará para la configuración de la plataforma de cualquier CPU.</span><span class="sxs-lookup"><span data-stu-id="97269-163">After adding hello references, you must select hello targeted platform (x64 or x86), adding references will not work for Any CPU platform configuration.</span></span>  <span data-ttu-id="97269-164">En el Explorador de soluciones, verá una marca de advertencia amarilla en estas referencias agregadas.</span><span class="sxs-lookup"><span data-stu-id="97269-164">In solution explorer, you will see yellow warning mark for these added references.</span></span>

<span data-ttu-id="97269-165">**interfaz de usuario de Reproductor de hello toodesign**</span><span class="sxs-lookup"><span data-stu-id="97269-165">**toodesign hello player user interface**</span></span>

1. <span data-ttu-id="97269-166">En el Explorador de soluciones, haga doble clic en **MainPage.xaml** tooopen en diseño de hello ver.</span><span class="sxs-lookup"><span data-stu-id="97269-166">From Solution Explorer, double click **MainPage.xaml** tooopen it in hello design view.</span></span>
2. <span data-ttu-id="97269-167">Busque hello  **&lt;cuadrícula&gt;**  y  **&lt;/Grid&gt;**  etiquetas Hola archivo XAML y pegar Hola siguiente de código entre las etiquetas de hello dos:</span><span class="sxs-lookup"><span data-stu-id="97269-167">Locate hello **&lt;Grid&gt;** and **&lt;/Grid&gt;**  tags hello XAML file, and paste hello following code between hello two tags:</span></span>

         <Grid.RowDefinitions>

            <RowDefinition Height="20"/>    <!-- spacer -->
            <RowDefinition Height="50"/>    <!-- media controls -->
            <RowDefinition Height="100*"/>  <!-- media element -->
            <RowDefinition Height="80*"/>   <!-- media stream and track selection -->
            <RowDefinition Height="50"/>    <!-- status bar -->
         </Grid.RowDefinitions>

         <StackPanel Name="spMediaControl" Grid.Row="1" Orientation="Horizontal">
            <TextBlock x:Name="tbSource" Text="Source :  " FontSize="16" FontWeight="Bold" VerticalAlignment="Center" />
            <TextBox x:Name="txtMediaSource" Text="http://ecn.channel9.msdn.com/o9/content/smf/smoothcontent/elephantsdream/Elephants_Dream_1024-h264-st-aac.ism/manifest" FontSize="10" Width="700" Margin="0,4,0,10" />
            <Button x:Name="btnSetSource" Content="Set Source" Width="111" Height="43" Click="btnSetSource_Click"/>
            <Button x:Name="btnPlay" Content="Play" Width="111" Height="43" Click="btnPlay_Click"/>
            <Button x:Name="btnPause" Content="Pause"  Width="111" Height="43" Click="btnPause_Click"/>
            <Button x:Name="btnStop" Content="Stop"  Width="111" Height="43" Click="btnStop_Click"/>
            <CheckBox x:Name="chkAutoPlay" Content="Auto Play" Height="55" Width="Auto" IsChecked="{Binding AutoPlay, ElementName=mediaElement, Mode=TwoWay}"/>
            <CheckBox x:Name="chkMute" Content="Mute" Height="55" Width="67" IsChecked="{Binding IsMuted, ElementName=mediaElement, Mode=TwoWay}"/>
         </StackPanel>

         <StackPanel Name="spMediaElement" Grid.Row="2" Height="435" Width="1072"
                    HorizontalAlignment="Center" VerticalAlignment="Center">
            <MediaElement x:Name="mediaElement" Height="356" Width="924" MinHeight="225"
                          HorizontalAlignment="Center" VerticalAlignment="Center" 
                          AudioCategory="BackgroundCapableMedia" />
            <StackPanel Orientation="Horizontal">
                <Slider x:Name="sliderProgress" Width="924" Height="44"
                        HorizontalAlignment="Center" VerticalAlignment="Center"
                        PointerPressed="sliderProgress_PointerPressed"/>
                <Slider x:Name="sliderVolume" 
                        HorizontalAlignment="Right" VerticalAlignment="Center" Orientation="Vertical" 
                        Height="79" Width="148" Minimum="0" Maximum="1" StepFrequency="0.1" 
                        Value="{Binding Volume, ElementName=mediaElement, Mode=TwoWay}" 
                        ToolTipService.ToolTip="{Binding Value, RelativeSource={RelativeSource Mode=Self}}"/>
            </StackPanel>
         </StackPanel>

         <StackPanel Name="spStatus" Grid.Row="4" Orientation="Horizontal">
            <TextBlock x:Name="tbStatus" Text="Status :  " 
               FontSize="16" FontWeight="Bold" VerticalAlignment="Center" HorizontalAlignment="Center" />
            <TextBox x:Name="txtStatus" FontSize="10" Width="700" VerticalAlignment="Center"/>
         </StackPanel>
   
   <span data-ttu-id="97269-168">Hola control MediaElement es un medio tooplayback usado.</span><span class="sxs-lookup"><span data-stu-id="97269-168">hello MediaElement control is used tooplayback media.</span></span> <span data-ttu-id="97269-169">control deslizante de Hello denominado sliderProgress se usará en curso de hello siguiente lección toocontrol Hola multimedia.</span><span class="sxs-lookup"><span data-stu-id="97269-169">hello slider control named sliderProgress will be used in hello next lesson toocontrol hello media progress.</span></span>
3. <span data-ttu-id="97269-170">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-170">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-171">Hola control MediaElement no admite la transmisión por secuencias suave contenido out-of-box.</span><span class="sxs-lookup"><span data-stu-id="97269-171">hello MediaElement control does not support Smooth Streaming content out-of-box.</span></span> <span data-ttu-id="97269-172">compatibilidad tooenable Hola Smooth Streaming, debe registrar el controlador hello secuencia de bytes de transmisión por secuencias suave por extensión de nombre de archivo y el tipo MIME.</span><span class="sxs-lookup"><span data-stu-id="97269-172">tooenable hello Smooth Streaming support, you must register hello Smooth Streaming byte-stream handler by file name extension and MIME type.</span></span>  <span data-ttu-id="97269-173">tooregister, hello MediaExtensionManager.RegisterByteStremHandler método de se utiliza el espacio de nombres de hello Windows.Media.</span><span class="sxs-lookup"><span data-stu-id="97269-173">tooregister, you use hello MediaExtensionManager.RegisterByteStremHandler method of hello Windows.Media namespace.</span></span>

<span data-ttu-id="97269-174">En este archivo XAML, algunos controladores de eventos están asociados a controles de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-174">In this XAML file, some event handlers are associated with hello controls.</span></span>  <span data-ttu-id="97269-175">Debe definir dichos controladores de eventos.</span><span class="sxs-lookup"><span data-stu-id="97269-175">You must define those event handlers.</span></span>

<span data-ttu-id="97269-176">**toomodify Hola archivo de código subyacente**</span><span class="sxs-lookup"><span data-stu-id="97269-176">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="97269-177">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-177">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-178">Hola parte superior de archivo hello, agregue el siguiente de hello instrucción using:</span><span class="sxs-lookup"><span data-stu-id="97269-178">At hello top of hello file, add hello following using statement:</span></span>
   
        using Windows.Media;
3. <span data-ttu-id="97269-179">En principio Hola de hello **MainPage** clase, agregue Hola siguiente miembro de datos:</span><span class="sxs-lookup"><span data-stu-id="97269-179">At hello beginning of hello **MainPage** class, add hello following data member:</span></span>
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. <span data-ttu-id="97269-180">Al final de Hola de hello **MainPage** constructor, agregue Hola después de dos líneas:</span><span class="sxs-lookup"><span data-stu-id="97269-180">At hello end of hello **MainPage** constructor, add hello following two lines:</span></span>
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. <span data-ttu-id="97269-181">Al final de Hola de hello **MainPage** clase, pegue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="97269-181">At hello end of hello **MainPage** class, paste hello following code:</span></span>
   
         # region UI Button Click Events
         private void btnPlay_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Play();
         txtStatus.Text = "MediaElement is playing ...";
         }
         private void btnPause_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Pause();
         txtStatus.Text = "MediaElement is paused";
         }
         private void btnSetSource_Click(object sender, RoutedEventArgs e)
         {

         sliderProgress.Value = 0;
         mediaElement.Source = new Uri(txtMediaSource.Text);

         if (chkAutoPlay.IsChecked == true)
         {
             txtStatus.Text = "MediaElement is playing ...";
         }
         else
         {
             txtStatus.Text = "Click hello Play button tooplay hello media source.";
         }
         }
         private void btnStop_Click(object sender, RoutedEventArgs e)
         {

         mediaElement.Stop();
         txtStatus.Text = "MediaElement is stopped";
         }
         private void sliderProgress_PointerPressed(object sender, PointerRoutedEventArgs e)
         {

         txtStatus.Text = "Seek tooposition " + sliderProgress.Value;
         mediaElement.Position = new TimeSpan(0, 0, (int)(sliderProgress.Value));
         }
         # endregion

<span data-ttu-id="97269-182">aquí se define un controlador de eventos de sliderProgress_PointerPressed Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-182">hello sliderProgress_PointerPressed event handler is defined here.</span></span>  <span data-ttu-id="97269-183">Hay más funciona toodo tooget trabajar, que se explicará en la siguiente lección de Hola de este tutorial.</span><span class="sxs-lookup"><span data-stu-id="97269-183">There are more works toodo tooget it working, which will be covered in hello next lesson of this tutorial.</span></span>
6. <span data-ttu-id="97269-184">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-184">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-185">Hola Hola termine de archivo de código subyacente será este aspecto:</span><span class="sxs-lookup"><span data-stu-id="97269-185">hello finished hello code behind file shall look like this:</span></span>

![Vista del código en Visual Studio de la aplicación de Tienda Windows de Smooth Streaming][CodeViewPic]

<span data-ttu-id="97269-187">**toocompile y prueba una aplicación Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-187">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="97269-188">De hello **generar** menú, haga clic en **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="97269-188">From hello **BUILD** menu, click **Configuration Manager**.</span></span>
2. <span data-ttu-id="97269-189">Cambio **plataforma de soluciones activas** toomatch la plataforma de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="97269-189">Change **Active solution platform** toomatch your development platform.</span></span>
3. <span data-ttu-id="97269-190">Presione **F6** proyecto de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="97269-190">Press **F6** toocompile hello project.</span></span> 
4. <span data-ttu-id="97269-191">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="97269-191">Press **F5** toorun hello application.</span></span>
5. <span data-ttu-id="97269-192">Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente.</span><span class="sxs-lookup"><span data-stu-id="97269-192">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
6. <span data-ttu-id="97269-193">Haga clic en **Establecer origen**.</span><span class="sxs-lookup"><span data-stu-id="97269-193">Click **Set Source**.</span></span> <span data-ttu-id="97269-194">Dado que **reproducción automática** está habilitada de forma predeterminada, Hola medios deben reproducir automáticamente.</span><span class="sxs-lookup"><span data-stu-id="97269-194">Because **Auto Play** is enabled by default, hello media shall play automatically.</span></span>  <span data-ttu-id="97269-195">Puede controlar el medio de hello mediante hello **reproducir**, **pausa** y **detener** botones.</span><span class="sxs-lookup"><span data-stu-id="97269-195">You can control hello media using hello **Play**, **Pause** and **Stop** buttons.</span></span>  <span data-ttu-id="97269-196">Puede controlar el volumen de medios de hello mediante el control deslizante vertical de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-196">You can control hello media volume using hello vertical slider.</span></span>  <span data-ttu-id="97269-197">Sin embargo, Hola control deslizante horizontal para controlar Hola progreso de medios no está totalmente implementado todavía.</span><span class="sxs-lookup"><span data-stu-id="97269-197">However hello horizontal slider for controlling hello media progress is not fully implemented yet.</span></span> 

<span data-ttu-id="97269-198">Ha terminado la lección 1.</span><span class="sxs-lookup"><span data-stu-id="97269-198">You have completed lesson1.</span></span>  <span data-ttu-id="97269-199">En esta lección, utilizará un tooplayback de control MediaElement contenido de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="97269-199">In this lesson, you use a MediaElement control tooplayback Smooth Streaming content.</span></span>  <span data-ttu-id="97269-200">En la siguiente lección hello, agregará un progreso de hello toocontrol de control deslizante de hello contenido de Smooth Streaming.</span><span class="sxs-lookup"><span data-stu-id="97269-200">In hello next lesson, you will add a slider toocontrol hello progress of hello Smooth Streaming content.</span></span>

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a><span data-ttu-id="97269-201">Lección 2: Agregar un control deslizante barra tooControl Hola progreso de medios</span><span class="sxs-lookup"><span data-stu-id="97269-201">Lesson 2: Add a Slider Bar tooControl hello Media Progress</span></span>

<span data-ttu-id="97269-202">En la lección 1, se crea una aplicación de tienda Windows con un tooplayback de control MediaElement XAML contenido de multimedia de transmisión por secuencias suave.</span><span class="sxs-lookup"><span data-stu-id="97269-202">In lesson 1, you created a Windows Store application with a MediaElement XAML control tooplayback Smooth Streaming media content.</span></span>  <span data-ttu-id="97269-203">Esta incorpora algunas funciones multimedia básicas como iniciar, detener y poner en pausa.</span><span class="sxs-lookup"><span data-stu-id="97269-203">It comes some basic media functions like start, stop and pause.</span></span>  <span data-ttu-id="97269-204">En esta lección, agregará una aplicación de toohello de control de barra de control deslizante.</span><span class="sxs-lookup"><span data-stu-id="97269-204">In this lesson, you will add a slider bar control toohello application.</span></span>

<span data-ttu-id="97269-205">En este tutorial, usaremos una posición del control deslizante de hello tooupdate del temporizador, según la posición actual de Hola de hello control MediaElement.</span><span class="sxs-lookup"><span data-stu-id="97269-205">In this tutorial, we will use a timer tooupdate hello slider position based on hello current position of hello MediaElement control.</span></span>  <span data-ttu-id="97269-206">control deslizante de Hello inicio y hora de finalización también toobe necesidad actualizado en el caso de contenido en directo.</span><span class="sxs-lookup"><span data-stu-id="97269-206">hello slider start and end time also need toobe updated in case of live content.</span></span>  <span data-ttu-id="97269-207">Esto se puede controlar mejor en el evento de actualización de origen adaptable de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-207">This can be better handled in hello adaptive source update event.</span></span>

<span data-ttu-id="97269-208">Los orígenes multimedia son objetos que generan datos multimedia.</span><span class="sxs-lookup"><span data-stu-id="97269-208">Media sources are objects that generate media data.</span></span>  <span data-ttu-id="97269-209">resolución de origen de Hello toma una secuencia de dirección URL o byte y crea el origen de medios adecuados de hello para el contenido.</span><span class="sxs-lookup"><span data-stu-id="97269-209">hello source resolver takes a URL or byte stream and creates hello appropriate media source for that content.</span></span>  <span data-ttu-id="97269-210">resolución de origen de Hello es la forma estándar de hello orígenes de contenido multimedia de hello aplicaciones toocreate.</span><span class="sxs-lookup"><span data-stu-id="97269-210">hello source resolver is hello standard way for hello applications toocreate media sources.</span></span> 

<span data-ttu-id="97269-211">Esta lección contiene Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="97269-211">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="97269-212">Registrar el controlador de transmisión por secuencias suave Hola</span><span class="sxs-lookup"><span data-stu-id="97269-212">Register hello Smooth Streaming handler</span></span> 
2. <span data-ttu-id="97269-213">Agregar controladores de eventos de nivel de administrador de hello origen adaptable</span><span class="sxs-lookup"><span data-stu-id="97269-213">Add hello adaptive source manager level event handlers</span></span>
3. <span data-ttu-id="97269-214">Agregar controladores de eventos de nivel de origen adaptable de Hola</span><span class="sxs-lookup"><span data-stu-id="97269-214">Add hello adaptive source level event handlers</span></span>
4. <span data-ttu-id="97269-215">Incorporación de controladores de eventos MediaElement</span><span class="sxs-lookup"><span data-stu-id="97269-215">Add MediaElement event handlers</span></span>
5. <span data-ttu-id="97269-216">Incorporación de código relacionado con la barra deslizante</span><span class="sxs-lookup"><span data-stu-id="97269-216">Add slider bar related code</span></span>
6. <span data-ttu-id="97269-217">Compilar y probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="97269-217">Compile and test hello application</span></span>

<span data-ttu-id="97269-218">**hello secuencia de bytes de transmisión por secuencias suave de tooregister controlador y pase propertyset Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-218">**tooregister hello Smooth Streaming byte-stream handler and pass hello propertyset**</span></span>

1. <span data-ttu-id="97269-219">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-219">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-220">En principio de Hola de archivo hello, agregue el siguiente de hello instrucción using:</span><span class="sxs-lookup"><span data-stu-id="97269-220">At hello beginning of hello file, add hello following using statement:</span></span>

        using Microsoft.Media.AdaptiveStreaming;
3. <span data-ttu-id="97269-221">En principio Hola de hello clase MainPage, agregue Hola después de los miembros de datos:</span><span class="sxs-lookup"><span data-stu-id="97269-221">At hello beginning of hello MainPage class, add hello following data members:</span></span>

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. <span data-ttu-id="97269-222">Hola interior **MainPage** constructor, agregue Hola siguiente código después de hello **esto. Inicializar Components();**  línea y las líneas de código de registro Hola escritas en la lección anterior hello:</span><span class="sxs-lookup"><span data-stu-id="97269-222">Inside hello **MainPage** constructor, add hello following code after hello **this.Initialize Components();** line and hello registration code lines written in hello previous lesson:</span></span>

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. <span data-ttu-id="97269-223">Hola interior **MainPage** constructor, modifique Hola de hello dos RegisterByteStreamHandler métodos tooadd sucesivamente parámetros:</span><span class="sxs-lookup"><span data-stu-id="97269-223">Inside hello **MainPage** constructor, modify hello two RegisterByteStreamHandler methods tooadd hello forth parameters:</span></span>

         // Registers Smooth Streaming byte-stream handler for ".ism" extension and, 
         // "text/xml" and "application/vnd.ms-ss" mime-types and pass hello propertyset. 
         // http://*.ism/manifest URI resources will be resolved by Byte-stream handler.
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "text/xml", 
            propertySet );
         extensions.RegisterByteStreamHandler(

            "Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", 
            ".ism", 
            "application/vnd.ms-sstr+xml", 
         propertySet);
6. <span data-ttu-id="97269-224">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-224">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-225">**controlador de eventos de nivel de administrador de origen adaptable de tooadd Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-225">**tooadd hello adaptive source manager level event handler**</span></span>

1. <span data-ttu-id="97269-226">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-226">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-227">Hola interior **MainPage** clase, agregue Hola siguiente miembro de datos:</span><span class="sxs-lookup"><span data-stu-id="97269-227">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="97269-228">private AdaptiveSource adaptiveSource = null;</span><span class="sxs-lookup"><span data-stu-id="97269-228">private AdaptiveSource adaptiveSource = null;</span></span>
3. <span data-ttu-id="97269-229">Al final de Hola de hello **MainPage** clase, agregue Hola siguiente controlador de eventos:</span><span class="sxs-lookup"><span data-stu-id="97269-229">At hello end of hello **MainPage** class, add hello following event handler:</span></span>
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. <span data-ttu-id="97269-230">Al final de Hola de hello **MainPage** constructor, agregue Hola siguiente evento open de línea toosubscribe toohello origen adaptable:</span><span class="sxs-lookup"><span data-stu-id="97269-230">At hello end of hello **MainPage** constructor, add hello following line toosubscribe toohello adaptive source open event:</span></span>
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. <span data-ttu-id="97269-231">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-231">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-232">**controladores de eventos de nivel de origen adaptable de tooadd**</span><span class="sxs-lookup"><span data-stu-id="97269-232">**tooadd adaptive source level event handlers**</span></span>

1. <span data-ttu-id="97269-233">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-233">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-234">Hola interior **MainPage** clase, agregue Hola siguiente miembro de datos:</span><span class="sxs-lookup"><span data-stu-id="97269-234">Inside hello **MainPage** class, add hello following data member:</span></span>
   
     <span data-ttu-id="97269-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span><span class="sxs-lookup"><span data-stu-id="97269-235">private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;</span></span>
3. <span data-ttu-id="97269-236">Al final de Hola de hello **MainPage** clase, agregue Hola después de controladores de eventos:</span><span class="sxs-lookup"><span data-stu-id="97269-236">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Adaptive Source Level Events
         private void mediaElement_ManifestReady(AdaptiveSource sender, ManifestReadyEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
            manifestObject = args.AdaptiveSource.Manifest;
         }

         private void mediaElement_AdaptiveSourceStatusUpdated(AdaptiveSource sender, AdaptiveSourceStatusUpdatedEventArgs args)
         {

            adaptiveSourceStatusUpdate = args;
         }

         private void mediaElement_AdaptiveSourceFailed(AdaptiveSource sender, AdaptiveSourceFailedEventArgs args)
         {

            txtStatus.Text = "Error: " + args.HttpResponse;
         }

         # endregion Adaptive Source Level Events
4. <span data-ttu-id="97269-237">Al final de Hola de hello **mediaElement AdaptiveSourceOpened** método, agregue Hola después de codificar toosubscribe toohello eventos:</span><span class="sxs-lookup"><span data-stu-id="97269-237">At hello end of hello **mediaElement AdaptiveSourceOpened** method, add hello following code toosubscribe toohello events:</span></span>
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. <span data-ttu-id="97269-238">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-238">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-239">Hola mismos eventos están disponibles en adaptable Manager nivel de origen, que puede utilizarse para controlar los elementos de la media de tooall comunes de la funcionalidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="97269-239">hello same events are available on Adaptive Source manger level as well, which can be used for handling functionality common tooall media elements in hello app.</span></span> <span data-ttu-id="97269-240">Cada AdaptiveSource incluye sus propios eventos y todos los eventos AdaptiveSource se aplicarán en cascada debajo de AdaptiveSourceManager.</span><span class="sxs-lookup"><span data-stu-id="97269-240">Each AdaptiveSource includes its own events and all AdaptiveSource events will be cascaded under AdaptiveSourceManager.</span></span>

<span data-ttu-id="97269-241">**controladores de eventos del elemento multimedia tooadd**</span><span class="sxs-lookup"><span data-stu-id="97269-241">**tooadd Media Element event handlers**</span></span>

1. <span data-ttu-id="97269-242">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-242">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-243">Al final de Hola de hello **MainPage** clase, agregue Hola después de controladores de eventos:</span><span class="sxs-lookup"><span data-stu-id="97269-243">At hello end of hello **MainPage** class, add hello following event handlers:</span></span>

         # region Media Element Event Handlers
         private void MediaOpened(object sender, RoutedEventArgs e)
         {

            txtStatus.Text = "MediaElement opened";
         }

         private void MediaFailed(object sender, ExceptionRoutedEventArgs e)
         {

            txtStatus.Text= "MediaElement failed: " + e.ErrorMessage;
         }

         private void MediaEnded(object sender, RoutedEventArgs e)
         {

            txtStatus.Text ="MediaElement ended.";
         }

         # endregion Media Element Event Handlers
3. <span data-ttu-id="97269-244">Al final de Hola de hello **MainPage** constructor, agregue Hola después de codificar toosubscript toohello eventos:</span><span class="sxs-lookup"><span data-stu-id="97269-244">At hello end of hello **MainPage** constructor, add hello following code toosubscript toohello events:</span></span>

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. <span data-ttu-id="97269-245">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-245">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-246">**control deslizante tooadd relacionados con código de barras**</span><span class="sxs-lookup"><span data-stu-id="97269-246">**tooadd slider bar related code**</span></span>

1. <span data-ttu-id="97269-247">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-247">From Solution Explorer, right click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-248">En principio de Hola de archivo hello, agregue el siguiente de hello instrucción using:</span><span class="sxs-lookup"><span data-stu-id="97269-248">At hello beginning of hello file, add hello following using statement:</span></span>
      
        using Windows.UI.Core;
3. <span data-ttu-id="97269-249">Hola interior **MainPage** clase, agregue Hola después de los miembros de datos:</span><span class="sxs-lookup"><span data-stu-id="97269-249">Inside hello **MainPage** class, add hello following data members:</span></span>
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. <span data-ttu-id="97269-250">Al final de Hola de hello **MainPage** constructor, agregue Hola siguiente código:</span><span class="sxs-lookup"><span data-stu-id="97269-250">At hello end of hello **MainPage** constructor, add hello following code:</span></span>
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. <span data-ttu-id="97269-251">Al final de Hola de hello **MainPage** clase, agregue el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="97269-251">At hello end of hello **MainPage** class, add hello following code:</span></span>

         # region sliderMediaPlayer
         private double SliderFrequency(TimeSpan timevalue)
         {

            long absvalue = 0;
            double stepfrequency = -1;

            if (manifestObject != null)
            {
                absvalue = manifestObject.Duration - (long)manifestObject.StartTime;
            }
            else
            {
                absvalue = mediaElement.NaturalDuration.TimeSpan.Ticks;
            }

            TimeSpan totalDVRDuration = new TimeSpan(absvalue);

            if (totalDVRDuration.TotalMinutes >= 10 && totalDVRDuration.TotalMinutes < 30)
            {
               stepfrequency = 10;
            }
            else if (totalDVRDuration.TotalMinutes >= 30 
                     && totalDVRDuration.TotalMinutes < 60)
            {
                stepfrequency = 30;
            }
            else if (totalDVRDuration.TotalHours >= 1)
            {
                stepfrequency = 60;
            }

            return stepfrequency;
         }

         void updateSliderPositionoNTicks(object sender, object e)
         {

            sliderProgress.Value = mediaElement.Position.TotalSeconds;
         }

         public void setupTimer()
         {

            sliderPositionUpdateDispatcher = new DispatcherTimer();
            sliderPositionUpdateDispatcher.Interval = new TimeSpan(0, 0, 0, 0, 300);
            startTimer();
         }

         public void startTimer()
         {

            sliderPositionUpdateDispatcher.Tick += updateSliderPositionoNTicks;
            sliderPositionUpdateDispatcher.Start();
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderStartTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.StartTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Minimum = absvalue;
            });
         }

         // Slider start and end time must be updated in case of live content
         public async void setSliderEndTime(long startTime)
         {

            await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
            {
                TimeSpan timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime);
                double absvalue = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero);
                sliderProgress.Maximum = absvalue;
            });
         }

         # endregion sliderMediaPlayer
      
>[!NOTE]
><span data-ttu-id="97269-252">CoreDispatcher es cambios toomake usado toohello interfaz de usuario de subproceso del subproceso de interfaz de usuario no.</span><span class="sxs-lookup"><span data-stu-id="97269-252">CoreDispatcher is used toomake changes toohello UI thread from non UI Thread.</span></span> <span data-ttu-id="97269-253">En el caso de cuello de botella en el subproceso de distribución, el desarrollador puede elegir toouse distribuidor proporcionada por elemento de interfaz de usuario que tenga la intención de tooupdate.</span><span class="sxs-lookup"><span data-stu-id="97269-253">In case of bottleneck on dispatcher thread, developer can choose toouse dispatcher provided by UI-element he/she intends tooupdate.</span></span>  <span data-ttu-id="97269-254">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="97269-254">For example:</span></span>
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. <span data-ttu-id="97269-255">Al final de Hola de hello **mediaElement_AdaptiveSourceStatusUpdated** método, agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="97269-255">At hello end of hello **mediaElement_AdaptiveSourceStatusUpdated** method, add hello following code:</span></span>

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. <span data-ttu-id="97269-256">Al final de Hola de hello **MediaOpened** método, agregar el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="97269-256">At hello end of hello **MediaOpened** method, add hello following code:</span></span>

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. <span data-ttu-id="97269-257">Presione **CTRL+S** archivo de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-257">Press **CTRL+S** toosave hello file.</span></span>

<span data-ttu-id="97269-258">**toocompile y prueba una aplicación Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-258">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="97269-259">Presione **F6** proyecto de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="97269-259">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="97269-260">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="97269-260">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="97269-261">Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente.</span><span class="sxs-lookup"><span data-stu-id="97269-261">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="97269-262">Haga clic en **Establecer origen**.</span><span class="sxs-lookup"><span data-stu-id="97269-262">Click **Set Source**.</span></span> 
5. <span data-ttu-id="97269-263">Barra del control deslizante de Hola de prueba.</span><span class="sxs-lookup"><span data-stu-id="97269-263">Test hello slider bar.</span></span>

<span data-ttu-id="97269-264">Ha completado la lección 2.</span><span class="sxs-lookup"><span data-stu-id="97269-264">You have completed lesson 2.</span></span>  <span data-ttu-id="97269-265">En esta lección, ha agregado un tooapplication del control deslizante.</span><span class="sxs-lookup"><span data-stu-id="97269-265">In this lesson you added a slider tooapplication.</span></span> 

## <a name="lesson-3-select-smooth-streaming-streams"></a><span data-ttu-id="97269-266">Lección 3: Selección de secuencias de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-266">Lesson 3: Select Smooth Streaming Streams</span></span>
<span data-ttu-id="97269-267">Transmisión por secuencias suave es toostream compatibles con contenido con varias pistas de audio de lenguaje que se pueden seleccionar mediante visores de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-267">Smooth Streaming is capable toostream content with multiple language audio tracks that are selectable by hello viewers.</span></span>  <span data-ttu-id="97269-268">En esta lección, podrá aplicar secuencias de tooselect visores.</span><span class="sxs-lookup"><span data-stu-id="97269-268">In this lesson, you will enable viewers tooselect streams.</span></span> <span data-ttu-id="97269-269">Esta lección contiene Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="97269-269">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="97269-270">Modificar el archivo XAML de hello</span><span class="sxs-lookup"><span data-stu-id="97269-270">Modify hello XAML file</span></span>
2. <span data-ttu-id="97269-271">Modificar el archivo de behand de código de hello</span><span class="sxs-lookup"><span data-stu-id="97269-271">Modify hello code behand file</span></span>
3. <span data-ttu-id="97269-272">Compilar y probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="97269-272">Compile and test hello application</span></span>

<span data-ttu-id="97269-273">**archivo XAML de hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="97269-273">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="97269-274">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Diseñador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="97269-274">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="97269-275">Busque &lt;Grid.RowDefinitions&gt;y modificar Hola RowDefinitions por lo que el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="97269-275">Locate &lt;Grid.RowDefinitions&gt;, and modify hello RowDefinitions so they looks like:</span></span>
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. <span data-ttu-id="97269-276">Hola interior &lt;cuadrícula&gt;&lt;/Grid&gt; etiquetas, agregar Hola de código siguiente toodefine un control de cuadro de lista, por lo que los usuarios pueden ver lista de Hola de secuencias disponibles y seleccione secuencias:</span><span class="sxs-lookup"><span data-stu-id="97269-276">Inside hello &lt;Grid&gt;&lt;/Grid&gt; tags, add hello following code toodefine a listbox control, so users can see hello list of available streams, and select streams:</span></span>

         <Grid Name="gridStreamAndBitrateSelection" Grid.Row="3">
            <Grid.RowDefinitions>
                <RowDefinition Height="300"/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="250*"/>
                <ColumnDefinition Width="250*"/>
            </Grid.ColumnDefinitions>
            <StackPanel Name="spStreamSelection" Grid.Row="1" Grid.Column="0">
                <StackPanel Orientation="Horizontal">
                    <TextBlock Name="tbAvailableStreams" Text="Available Streams:" FontSize="16" VerticalAlignment="Center"></TextBlock>
                    <Button Name="btnChangeStreams" Content="Submit" Click="btnChangeStream_Click"/>
                </StackPanel>
                <ListBox x:Name="lbAvailableStreams" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                    ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
                    <ListBox.ItemTemplate>
                        <DataTemplate>
                            <CheckBox Content="{Binding Name}" IsChecked="{Binding isChecked, Mode=TwoWay}" />
                        </DataTemplate>
                    </ListBox.ItemTemplate>
                </ListBox>
            </StackPanel>
         </Grid>
4. <span data-ttu-id="97269-277">Presione **CTRL+S** cambios de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="97269-277">Press **CTRL+S** toosave hello changes.</span></span>

<span data-ttu-id="97269-278">**toomodify Hola archivo de código subyacente**</span><span class="sxs-lookup"><span data-stu-id="97269-278">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="97269-279">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-279">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-280">Dentro de espacio de nombres de hello SSPlayer, agregue una nueva clase:</span><span class="sxs-lookup"><span data-stu-id="97269-280">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Stream
   
        public class Stream
        {
            private IManifestStream stream;
            public bool isCheckedValue;
            public string name;
   
            public string Name
            {
                get { return name; }
                set { name = value; }
            }
   
            public IManifestStream ManifestStream
            {
                get { return stream; }
                set { stream = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    // mMke hello video stream always checked.
                    if (stream.Type == MediaStreamType.Video)
                    {
                        isCheckedValue = true;
                    }
                    else
                    {
                        isCheckedValue = value;
                    }
                }
            }
   
            public Stream(IManifestStream streamIn)
            {
                stream = streamIn;
                name = stream.Name;
            }
        }
        #endregion class Stream
3. <span data-ttu-id="97269-281">En principio Hola de hello clase MainPage, agregue Hola después de definiciones de variables:</span><span class="sxs-lookup"><span data-stu-id="97269-281">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. <span data-ttu-id="97269-282">Dentro de la clase MainPage hello, agregue Hola después de región:</span><span class="sxs-lookup"><span data-stu-id="97269-282">Inside hello MainPage class, add hello following region:</span></span>
   
        #region stream selection
        ///<summary>
        ///Functionality tooselect streams from IManifestStream available streams
        /// </summary>
   
        // This function is called from hello mediaElement_ManifestReady event handler 
        // tooretrieve hello streams and populate them toohello local data members.
        public void getStreams(Manifest manifestObject)
        {
            availableStreams = new List<Stream>();
            availableVideoStreams = new List<Stream>();
            availableAudioStreams = new List<Stream>();
            availableTextStreams = new List<Stream>();
   
            try
            {
                for (int i = 0; i<manifestObject.AvailableStreams.Count; i++)
                {
                    Stream newStream = new Stream(manifestObject.AvailableStreams[i]);
                    newStream.isChecked = false;
   
                    //populate hello stream lists based on hello types
                    availableStreams.Add(newStream);
   
                    switch (newStream.ManifestStream.Type)
                    {
                        case MediaStreamType.Video:
                            availableVideoStreams.Add(newStream);
                            break;
                        case MediaStreamType.Audio:
                            availableAudioStreams.Add(newStream);
                            break;
                        case MediaStreamType.Text:
                            availableTextStreams.Add(newStream);
                            break;
                    }
   
                    // Select hello default selected streams from hello manifest.
                    for (int j = 0; j<manifestObject.SelectedStreams.Count; j++)
                    {
                        string selectedStreamName = manifestObject.SelectedStreams[j].Name;
                        if (selectedStreamName.Equals(newStream.Name))
                        {
                            newStream.isChecked = true;
                            break;
                        }
                    }
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function set hello list box ItemSource
        private async void refreshAvailableStreamsListBoxItemSource()
        {
            try
            {
                //update hello stream check box list on hello UI
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableStreams.ItemsSource = availableStreams; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
   
        // This function creates a selected streams list
        private void createSelectedStreamsList(List<IManifestStream> selectedStreams)
        {
            bool isOneVideoSelected = false;
            bool isOneAudioSelected = false;
   
            // Only one video stream can be selected
            for (int j = 0; j<availableVideoStreams.Count; j++)
            {
                if (availableVideoStreams[j].isChecked && (!isOneVideoSelected))
                {
                    selectedStreams.Add(availableVideoStreams[j].ManifestStream);
                    isOneVideoSelected = true;
                }
            }
   
            // Select hello frist video stream from hello list if no video stream is selected
            if (!isOneVideoSelected)
            {
                availableVideoStreams[0].isChecked = true;
                selectedStreams.Add(availableVideoStreams[0].ManifestStream);
            }
   
            // Only one audio stream can be selected
            for (int j = 0; j<availableAudioStreams.Count; j++)
            {
                if (availableAudioStreams[j].isChecked && (!isOneAudioSelected))
                {
                    selectedStreams.Add(availableAudioStreams[j].ManifestStream);
                    isOneAudioSelected = true;
                    txtStatus.Text = "hello audio stream is changed too" + availableAudioStreams[j].ManifestStream.Name;
                }
            }
   
            // Select hello frist audio stream from hello list if no audio steam is selected.
            if (!isOneAudioSelected)
            {
                availableAudioStreams[0].isChecked = true;
                selectedStreams.Add(availableAudioStreams[0].ManifestStream);
            }
   
            // Multiple text streams are supported.
            for (int j = 0; j < availableTextStreams.Count; j++)
            {
                if (availableTextStreams[j].isChecked)
                {
                    selectedStreams.Add(availableTextStreams[j].ManifestStream);
                }
            }
        }
   
        // Change streams on a smooth streaming presentation with multiple video streams.
        private async void changeStreams(List<IManifestStream> selectStreams)
        {
            try
            {
                IReadOnlyList<IStreamChangedResult> returnArgs =
                    await manifestObject.SelectStreamsAsync(selectStreams);
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }
        }
        #endregion stream selection
5. <span data-ttu-id="97269-283">Busque el método mediaElement_ManifestReady de hello, anexar Hola siguiente código al final de Hola de función hello:</span><span class="sxs-lookup"><span data-stu-id="97269-283">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    <span data-ttu-id="97269-284">Por lo que cuando MediaElement manifiesto esté preparado, código de hello Obtiene una lista de secuencias disponibles hello y rellena el cuadro de lista de interfaz de usuario de hello con lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-284">So when MediaElement manifest is ready, hello code gets a list of hello available streams, and populates hello UI list box with hello list.</span></span>
6. <span data-ttu-id="97269-285">Dentro de la clase MainPage hello, busque botones de la interfaz de usuario de hello haga clic en la región de eventos y, a continuación, agregue Hola después de la definición de función:</span><span class="sxs-lookup"><span data-stu-id="97269-285">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

<span data-ttu-id="97269-286">**toocompile y prueba una aplicación Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-286">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="97269-287">Presione **F6** proyecto de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="97269-287">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="97269-288">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="97269-288">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="97269-289">Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente.</span><span class="sxs-lookup"><span data-stu-id="97269-289">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="97269-290">Haga clic en **Establecer origen**.</span><span class="sxs-lookup"><span data-stu-id="97269-290">Click **Set Source**.</span></span> 
5. <span data-ttu-id="97269-291">idioma predeterminado de Hello es audio_eng.</span><span class="sxs-lookup"><span data-stu-id="97269-291">hello default language is audio_eng.</span></span> <span data-ttu-id="97269-292">Intente tooswitch entre audio_eng y audio_es.</span><span class="sxs-lookup"><span data-stu-id="97269-292">Try tooswitch between audio_eng and audio_es.</span></span> <span data-ttu-id="97269-293">Cada vez, seleccione un nuevo flujo, debe hacer clic en el botón de envío de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-293">Everytime, you select a new stream, you must click hello Submit button.</span></span>

<span data-ttu-id="97269-294">Ha completado la lección 3.</span><span class="sxs-lookup"><span data-stu-id="97269-294">You have completed lesson 3.</span></span>  <span data-ttu-id="97269-295">En esta lección, agregar secuencias de hello funcionalidad toochoose.</span><span class="sxs-lookup"><span data-stu-id="97269-295">In this lesson, you add hello functionality toochoose streams.</span></span>

## <a name="lesson-4-select-smooth-streaming-tracks"></a><span data-ttu-id="97269-296">Lección 4: Selección de pistas de Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-296">Lesson 4: Select Smooth Streaming Tracks</span></span>
<span data-ttu-id="97269-297">Una presentación de Smooth Streaming puede contener varios archivos de vídeo codificados con diferentes niveles de calidad (velocidad de bits) y resoluciones.</span><span class="sxs-lookup"><span data-stu-id="97269-297">A Smooth Streaming presentation can contain multiple video files encoded with different quality levels (bit rates) and resolutions.</span></span> <span data-ttu-id="97269-298">En esta lección, podrá aplicar realiza un seguimiento de los usuarios tooselect.</span><span class="sxs-lookup"><span data-stu-id="97269-298">In this lesson, you will enable users tooselect tracks.</span></span> <span data-ttu-id="97269-299">Esta lección contiene Hola procedimientos siguientes:</span><span class="sxs-lookup"><span data-stu-id="97269-299">This lesson contains hello following procedures:</span></span>

1. <span data-ttu-id="97269-300">Modificar el archivo XAML de hello</span><span class="sxs-lookup"><span data-stu-id="97269-300">Modify hello XAML file</span></span>
2. <span data-ttu-id="97269-301">Modificar el archivo de behand de código de hello</span><span class="sxs-lookup"><span data-stu-id="97269-301">Modify hello code behand file</span></span>
3. <span data-ttu-id="97269-302">Compilar y probar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="97269-302">Compile and test hello application</span></span>

<span data-ttu-id="97269-303">**archivo XAML de hello toomodify**</span><span class="sxs-lookup"><span data-stu-id="97269-303">**toomodify hello XAML file**</span></span>

1. <span data-ttu-id="97269-304">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Diseñador de vistas**.</span><span class="sxs-lookup"><span data-stu-id="97269-304">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Designer**.</span></span>
2. <span data-ttu-id="97269-305">Busque hello &lt;cuadrícula&gt; etiqueta con nombre hello **gridStreamAndBitrateSelection**, anexar Hola siguiente código al final de Hola de etiqueta de hello:</span><span class="sxs-lookup"><span data-stu-id="97269-305">Locate hello &lt;Grid&gt; tag with hello name **gridStreamAndBitrateSelection**, append hello following code at hello end of hello tag:</span></span>
   
         <StackPanel Name="spBitRateSelection" Grid.Row="1" Grid.Column="1">
         <StackPanel Orientation="Horizontal">
             <TextBlock Name="tbBitRate" Text="Available Bitrates:" FontSize="16" VerticalAlignment="Center"/>
             <Button Name="btnChangeTracks" Content="Submit" Click="btnChangeTrack_Click" />
         </StackPanel>
         <ListBox x:Name="lbAvailableVideoTracks" Height="200" Width="200" Background="Transparent" HorizontalAlignment="Left" 
                  ScrollViewer.VerticalScrollMode="Enabled" ScrollViewer.VerticalScrollBarVisibility="Visible">
             <ListBox.ItemTemplate>
                 <DataTemplate>
                     <CheckBox Content="{Binding Bitrate}" IsChecked="{Binding isChecked, Mode=TwoWay}"/>
                 </DataTemplate>
             </ListBox.ItemTemplate>
         </ListBox>
         </StackPanel>
3. <span data-ttu-id="97269-306">Presione **CTRL+S** toosave cambia</span><span class="sxs-lookup"><span data-stu-id="97269-306">Press **CTRL+S** toosave he changes</span></span>

<span data-ttu-id="97269-307">**toomodify Hola archivo de código subyacente**</span><span class="sxs-lookup"><span data-stu-id="97269-307">**toomodify hello code behind file**</span></span>

1. <span data-ttu-id="97269-308">En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.</span><span class="sxs-lookup"><span data-stu-id="97269-308">From Solution Explorer, right-click **MainPage.xaml**, and then click **View Code**.</span></span>
2. <span data-ttu-id="97269-309">Dentro de espacio de nombres de hello SSPlayer, agregue una nueva clase:</span><span class="sxs-lookup"><span data-stu-id="97269-309">Inside hello SSPlayer namespace, add a new class:</span></span>
   
        #region class Track
        public class Track
        {
            private IManifestTrack trackInfo;
            public string _bitrate;
            public bool isCheckedValue;
   
            public IManifestTrack TrackInfo
            {
                get { return trackInfo; }
                set { trackInfo = value; }
            }
   
            public string Bitrate
            {
                get { return _bitrate; }
                set { _bitrate = value; }
            }
   
            public bool isChecked
            {
                get { return isCheckedValue; }
                set
                {
                    isCheckedValue = value;
                }
            }
   
            public Track(IManifestTrack trackInfoIn)
            {
                trackInfo = trackInfoIn;
                _bitrate = trackInfoIn.Bitrate.ToString();
            }
            //public Track() { }
        }
        #endregion class Track
3. <span data-ttu-id="97269-310">En principio Hola de hello clase MainPage, agregue Hola después de definiciones de variables:</span><span class="sxs-lookup"><span data-stu-id="97269-310">At hello beginning of hello MainPage class, add hello following variable definitions:</span></span>
   
        private List<Track> availableTracks;
4. <span data-ttu-id="97269-311">Dentro de la clase MainPage hello, agregue Hola después de región:</span><span class="sxs-lookup"><span data-stu-id="97269-311">Inside hello MainPage class, add hello following region:</span></span>
   
        #region track selection
        /// <summary>
        /// Functionality tooselect video streams
        /// </summary>
   
        /// This Function gets hello tracks for hello selected video stream
        public void getTracks(Manifest manifestObject)
        {
            availableTracks = new List<Track>();
   
            IManifestStream videoStream = getVideoStream();
            IReadOnlyList<IManifestTrack> availableTracksLocal = videoStream.AvailableTracks;
            IReadOnlyList<IManifestTrack> selectedTracksLocal = videoStream.SelectedTracks;
   
            try
            {
                for (int i = 0; i < availableTracksLocal.Count; i++)
                {
                    Track thisTrack = new Track(availableTracksLocal[i]);
                    thisTrack.isChecked = true;
   
                    for (int j = 0; j < selectedTracksLocal.Count; j++)
                    {
                        string selectedTrackName = selectedTracksLocal[j].Bitrate.ToString();
                        if (selectedTrackName.Equals(thisTrack.Bitrate))
                        {
                            thisTrack.isChecked = true;
                            break;
                        }
                    }
                    availableTracks.Add(thisTrack);
                }
            }
            catch (Exception e)
            {
                txtStatus.Text = e.Message;
            }
        }
   
        // This function gets hello video stream that is playing
        private IManifestStream getVideoStream()
        {
            IManifestStream videoStream = null;
            for (int i = 0; i < manifestObject.SelectedStreams.Count; i++)
            {
                if (manifestObject.SelectedStreams[i].Type == MediaStreamType.Video)
                {
                    videoStream = manifestObject.SelectedStreams[i];
                    break;
                }
            }
            return videoStream;
        }
   
        // This function set hello UI list box control ItemSource
        private async void refreshAvailableTracksListBoxItemSource()
        {
            try
            {
                // Update hello track check box list on hello UI 
                await _dispatcher.RunAsync(CoreDispatcherPriority.Normal, ()
                    => { lbAvailableVideoTracks.ItemsSource = availableTracks; });
            }
            catch (Exception e)
            {
                txtStatus.Text = "Error: " + e.Message;
            }        
        }
   
        // This function creates a list of hello selected tracks.
        private void createSelectedTracksList(List<IManifestTrack> selectedTracks)
        {
            // Create a list of selected tracks
            for (int j = 0; j < availableTracks.Count; j++)
            {
                if (availableTracks[j].isCheckedValue == true)
                {
                    selectedTracks.Add(availableTracks[j].TrackInfo);
                }
            }
        }
   
        // This function selects hello tracks based on user selection 
        private void changeTracks(List<IManifestTrack> selectedTracks)
        {
            IManifestStream videoStream = getVideoStream();
            try
            {
                videoStream.SelectTracks(selectedTracks);
            }
            catch (Exception ex)
            {
                txtStatus.Text = ex.Message;
            }
        }
        #endregion track selection
5. <span data-ttu-id="97269-312">Busque el método mediaElement_ManifestReady de hello, anexar Hola siguiente código al final de Hola de función hello:</span><span class="sxs-lookup"><span data-stu-id="97269-312">Locate hello mediaElement_ManifestReady method, append hello following code at hello end of hello function:</span></span>
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. <span data-ttu-id="97269-313">Dentro de la clase MainPage hello, busque botones de la interfaz de usuario de hello haga clic en la región de eventos y, a continuación, agregue Hola después de la definición de función:</span><span class="sxs-lookup"><span data-stu-id="97269-313">Inside hello MainPage class, locate hello UI buttons click events region, and then add hello following function definition:</span></span>
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

<span data-ttu-id="97269-314">**toocompile y prueba una aplicación Hola**</span><span class="sxs-lookup"><span data-stu-id="97269-314">**toocompile and test hello application**</span></span>

1. <span data-ttu-id="97269-315">Presione **F6** proyecto de hello toocompile.</span><span class="sxs-lookup"><span data-stu-id="97269-315">Press **F6** toocompile hello project.</span></span> 
2. <span data-ttu-id="97269-316">Presione **F5** aplicación de hello toorun.</span><span class="sxs-lookup"><span data-stu-id="97269-316">Press **F5** toorun hello application.</span></span>
3. <span data-ttu-id="97269-317">Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente.</span><span class="sxs-lookup"><span data-stu-id="97269-317">At hello top of hello application, you can either use hello default Smooth Streaming URL or enter a different one.</span></span> 
4. <span data-ttu-id="97269-318">Haga clic en **Establecer origen**.</span><span class="sxs-lookup"><span data-stu-id="97269-318">Click **Set Source**.</span></span> 
5. <span data-ttu-id="97269-319">De forma predeterminada, se seleccionan todas las pistas de hello hello secuencia de vídeo.</span><span class="sxs-lookup"><span data-stu-id="97269-319">By default, all of hello tracks of hello video stream are selected.</span></span> <span data-ttu-id="97269-320">Hola tooexperiment cambios de velocidad de bits, puede seleccionar la velocidad de bits más baja de hello disponible y, a continuación, seleccione la velocidad de bits más alta de hello disponible.</span><span class="sxs-lookup"><span data-stu-id="97269-320">tooexperiment hello bit rate changes, you can select hello lowest bit rate available, and then select hello highest bit rate available.</span></span> <span data-ttu-id="97269-321">Debe hacer clic en Submit después de realizar cada uno de los cambios.</span><span class="sxs-lookup"><span data-stu-id="97269-321">You must click Submit after each change.</span></span>  <span data-ttu-id="97269-322">Puede ver los cambios de la calidad del vídeo de Hola.</span><span class="sxs-lookup"><span data-stu-id="97269-322">You can see hello video quality changes.</span></span>

<span data-ttu-id="97269-323">Ha completado la lección 4.</span><span class="sxs-lookup"><span data-stu-id="97269-323">You have completed lesson 4.</span></span>  <span data-ttu-id="97269-324">En esta lección, agregará Hola funcionalidad toochoose realiza un seguimiento.</span><span class="sxs-lookup"><span data-stu-id="97269-324">In this lesson, you add hello functionality toochoose tracks.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="97269-325">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="97269-325">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="97269-326">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="97269-326">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a><span data-ttu-id="97269-327">Otros recursos:</span><span class="sxs-lookup"><span data-stu-id="97269-327">Other Resources:</span></span>
* [<span data-ttu-id="97269-328">¿Cómo toobuild una aplicación Smooth Streaming Windows 8 JavaScript con las características avanzadas</span><span class="sxs-lookup"><span data-stu-id="97269-328">How toobuild a Smooth Streaming Windows 8 JavaScript application with advanced features</span></span>](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [<span data-ttu-id="97269-329">Información técnica sobre Smooth Streaming</span><span class="sxs-lookup"><span data-stu-id="97269-329">Smooth Streaming Technical Overview</span></span>](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

