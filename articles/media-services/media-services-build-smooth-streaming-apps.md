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
# <a name="how-toobuild-a-smooth-streaming-windows-store-application"></a>¿Cómo tooBuild una aplicación Smooth Streaming Windows Store

Hola Smooth Streaming Client SDK para Windows 8 permite que las aplicaciones de tienda Windows de toobuild a los desarrolladores que pueden reproducir contenido de transmisión por secuencias suave a petición y en directo. Además toohello básica reproducción de Smooth Streaming de contenido, Hola SDK también proporciona características avanzadas como la protección de Microsoft PlayReady, restricción del nivel de calidad, Live DVR, la secuencia de audio de conmutación, realizar escuchas para las actualizaciones de estado (por ejemplo, los cambios de nivel de calidad ) y eventos de error y así sucesivamente. Para obtener más información de características de hello compatibles, vea hello [notas de la versión](http://www.iis.net/learn/media/smooth-streaming/smooth-streaming-client-sdk-for-windows-8-release-notes). Para más información, vea [Player Framework para Windows 8](http://playerframework.codeplex.com/). 

Este tutorial contiene cuatro lecciones:

1. Creación de una aplicación básica de Tienda de Smooth Streaming
2. Agregar un control deslizante barra tooControl Hola progreso de medios
3. Selección de secuencias de Smooth Streaming
4. Selección de pistas de Smooth Streaming

## <a name="prerequisites"></a>Requisitos previos
* Windows 8 de 32 o 64 bits. Puede conseguir la [Evaluación de Windows 8 Enterprise](http://msdn.microsoft.com/evalcenter/jj554510.aspx) en MSDN.
* Visual Studio 2012 o Visual Studio Express 2012 (o una versión posterior). Puede obtener la versión de prueba de hello [aquí](http://www.microsoft.com/visualstudio/11/downloads).
* [SDK de cliente Smooth Streaming de Microsoft para Windows 8](http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Homehttp://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6?SRC=Home).

solución de Hello completado de cada lección puede descargarse de ejemplos de código para desarrolladores de MSDN (Galería de código): 

* [Lección 1](http://code.msdn.microsoft.com/Smooth-Streaming-Client-0bb1471f) : Un sencillo reproductor multimedia de Smooth Streaming para Windows 8 
* [Lección 2](http://code.msdn.microsoft.com/A-simple-Windows-8-Smooth-ee98f63a) : Un sencillo reproductor multimedia de Smooth Streaming para Windows 8 con un control de barra deslizante 
* [Lección 3](http://code.msdn.microsoft.com/A-Windows-8-Smooth-883c3b44) : Un reproductor multimedia de Smooth Streaming para Windows 8 con selección de secuencias  
* [Lección 4](http://code.msdn.microsoft.com/A-Windows-8-Smooth-aa9e4907): Un reproductor multimedia de Smooth Streaming para Windows 8 con selección de pistas

## <a name="lesson-1-create-a-basic-smooth-streaming-store-application"></a>Lección 1: Creación de una aplicación básica de Tienda de Smooth Streaming

En esta lección, creará una aplicación de tienda Windows con un MediaElement control tooplay transmisión por secuencias suave contenido.  aplicación en ejecución Hello tiene el siguiente aspecto:

![Ejemplo de aplicación de Tienda Windows de Smooth Streaming][PlayerApplication]

Para obtener más información acerca del desarrollo de la aplicación de la Tienda Windows, consulte [Desarrollo de magníficas aplicaciones para Windows 8](http://msdn.microsoft.com/windows/apps/br229512.aspx). Esta lección contiene Hola procedimientos siguientes:

1. Creación de un proyecto de Tienda Windows
2. Diseñar la interfaz de usuario de hello (XAML)
3. Modificar Hola archivo de código subyacente
4. Compilar y probar la aplicación hello

**toocreate un proyecto de la tienda de Windows**

1. Ejecute Visual Studio 2012 o posterior.
2. De hello **archivo** menú, haga clic en **New**y, a continuación, haga clic en **proyecto**.
3. Del cuadro de diálogo nuevo proyecto de hello, tipo o seleccione hello siguientes valores:

| Nombre | Valor |
| --- | --- |
| Grupo de plantillas |Instalado/Plantillas/Visual C#/Tienda Windows |
| Plantilla |Aplicación vacía (XAML) |
| Nombre |SSPlayer |
| Ubicación |C:\SSTutorials |
| Nombre de la solución |SSPlayer |
| Crear directorio para la solución |(seleccionado) |

1. Haga clic en **Aceptar**.

**tooadd un toohello referencia SDK de cliente de transmisión por secuencias suave**

1. En el Explorador de soluciones, haga clic con el botón derecho en **SSPlayer** y haga clic en **Agregar referencia**.
2. Escriba o seleccione Hola siguientes valores:

| Nombre | Valor |
| --- | --- |
| Grupo de referencia |Windows/Extensiones |
| Referencia |Seleccione el SDK de cliente Smooth Streaming de Microsoft para Windows 8 y el paquete en tiempo de ejecución de Microsoft Visual C++ |

1. Haga clic en **Aceptar**. 

Después de agregar las referencias de hello, debe seleccionar la plataforma de destino de hello (x64 o x86), agregar referencias no funcionará para la configuración de la plataforma de cualquier CPU.  En el Explorador de soluciones, verá una marca de advertencia amarilla en estas referencias agregadas.

**interfaz de usuario de Reproductor de hello toodesign**

1. En el Explorador de soluciones, haga doble clic en **MainPage.xaml** tooopen en diseño de hello ver.
2. Busque hello  **&lt;cuadrícula&gt;**  y  **&lt;/Grid&gt;**  etiquetas Hola archivo XAML y pegar Hola siguiente de código entre las etiquetas de hello dos:

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
   
   Hola control MediaElement es un medio tooplayback usado. control deslizante de Hello denominado sliderProgress se usará en curso de hello siguiente lección toocontrol Hola multimedia.
3. Presione **CTRL+S** archivo de hello toosave.

Hola control MediaElement no admite la transmisión por secuencias suave contenido out-of-box. compatibilidad tooenable Hola Smooth Streaming, debe registrar el controlador hello secuencia de bytes de transmisión por secuencias suave por extensión de nombre de archivo y el tipo MIME.  tooregister, hello MediaExtensionManager.RegisterByteStremHandler método de se utiliza el espacio de nombres de hello Windows.Media.

En este archivo XAML, algunos controladores de eventos están asociados a controles de Hola.  Debe definir dichos controladores de eventos.

**toomodify Hola archivo de código subyacente**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Hola parte superior de archivo hello, agregue el siguiente de hello instrucción using:
   
        using Windows.Media;
3. En principio Hola de hello **MainPage** clase, agregue Hola siguiente miembro de datos:
   
         private MediaExtensionManager extensions = new MediaExtensionManager();
4. Al final de Hola de hello **MainPage** constructor, agregue Hola después de dos líneas:
   
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "text/xml");
        extensions.RegisterByteStreamHandler("Microsoft.Media.AdaptiveStreaming.SmoothByteStreamHandler", ".ism", "application/vnd.ms-sstr+xml");
5. Al final de Hola de hello **MainPage** clase, pegue el siguiente código de hello:
   
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

aquí se define un controlador de eventos de sliderProgress_PointerPressed Hola.  Hay más funciona toodo tooget trabajar, que se explicará en la siguiente lección de Hola de este tutorial.
6. Presione **CTRL+S** archivo de hello toosave.

Hola Hola termine de archivo de código subyacente será este aspecto:

![Vista del código en Visual Studio de la aplicación de Tienda Windows de Smooth Streaming][CodeViewPic]

**toocompile y prueba una aplicación Hola**

1. De hello **generar** menú, haga clic en **Configuration Manager**.
2. Cambio **plataforma de soluciones activas** toomatch la plataforma de desarrollo.
3. Presione **F6** proyecto de hello toocompile. 
4. Presione **F5** aplicación de hello toorun.
5. Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente. 
6. Haga clic en **Establecer origen**. Dado que **reproducción automática** está habilitada de forma predeterminada, Hola medios deben reproducir automáticamente.  Puede controlar el medio de hello mediante hello **reproducir**, **pausa** y **detener** botones.  Puede controlar el volumen de medios de hello mediante el control deslizante vertical de Hola.  Sin embargo, Hola control deslizante horizontal para controlar Hola progreso de medios no está totalmente implementado todavía. 

Ha terminado la lección 1.  En esta lección, utilizará un tooplayback de control MediaElement contenido de Smooth Streaming.  En la siguiente lección hello, agregará un progreso de hello toocontrol de control deslizante de hello contenido de Smooth Streaming.

## <a name="lesson-2-add-a-slider-bar-toocontrol-hello-media-progress"></a>Lección 2: Agregar un control deslizante barra tooControl Hola progreso de medios

En la lección 1, se crea una aplicación de tienda Windows con un tooplayback de control MediaElement XAML contenido de multimedia de transmisión por secuencias suave.  Esta incorpora algunas funciones multimedia básicas como iniciar, detener y poner en pausa.  En esta lección, agregará una aplicación de toohello de control de barra de control deslizante.

En este tutorial, usaremos una posición del control deslizante de hello tooupdate del temporizador, según la posición actual de Hola de hello control MediaElement.  control deslizante de Hello inicio y hora de finalización también toobe necesidad actualizado en el caso de contenido en directo.  Esto se puede controlar mejor en el evento de actualización de origen adaptable de Hola.

Los orígenes multimedia son objetos que generan datos multimedia.  resolución de origen de Hello toma una secuencia de dirección URL o byte y crea el origen de medios adecuados de hello para el contenido.  resolución de origen de Hello es la forma estándar de hello orígenes de contenido multimedia de hello aplicaciones toocreate. 

Esta lección contiene Hola procedimientos siguientes:

1. Registrar el controlador de transmisión por secuencias suave Hola 
2. Agregar controladores de eventos de nivel de administrador de hello origen adaptable
3. Agregar controladores de eventos de nivel de origen adaptable de Hola
4. Incorporación de controladores de eventos MediaElement
5. Incorporación de código relacionado con la barra deslizante
6. Compilar y probar la aplicación hello

**hello secuencia de bytes de transmisión por secuencias suave de tooregister controlador y pase propertyset Hola**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. En principio de Hola de archivo hello, agregue el siguiente de hello instrucción using:

        using Microsoft.Media.AdaptiveStreaming;
3. En principio Hola de hello clase MainPage, agregue Hola después de los miembros de datos:

         private Windows.Foundation.Collections.PropertySet propertySet = new Windows.Foundation.Collections.PropertySet();             
         private IAdaptiveSourceManager adaptiveSourceManager;
4. Hola interior **MainPage** constructor, agregue Hola siguiente código después de hello **esto. Inicializar Components();**  línea y las líneas de código de registro Hola escritas en la lección anterior hello:

        // Gets hello default instance of AdaptiveSourceManager which manages Smooth 
        //Streaming media sources.
        adaptiveSourceManager = AdaptiveSourceManager.GetDefault();
        // Sets property key value tooAdaptiveSourceManager default instance.
        // {A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}" must be hardcoded.
        propertySet["{A5CE1DE8-1D00-427B-ACEF-FB9A3C93DE2D}"] = adaptiveSourceManager;
5. Hola interior **MainPage** constructor, modifique Hola de hello dos RegisterByteStreamHandler métodos tooadd sucesivamente parámetros:

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
6. Presione **CTRL+S** archivo de hello toosave.

**controlador de eventos de nivel de administrador de origen adaptable de tooadd Hola**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Hola interior **MainPage** clase, agregue Hola siguiente miembro de datos:
   
     private AdaptiveSource adaptiveSource = null;
3. Al final de Hola de hello **MainPage** clase, agregue Hola siguiente controlador de eventos:
   
         # region Adaptive Source Manager Level Events
         private void mediaElement_AdaptiveSourceOpened(AdaptiveSource sender, AdaptiveSourceOpenedEventArgs args)
         {

            adaptiveSource = args.AdaptiveSource;
         }

         # endregion Adaptive Source Manager Level Events
4. Al final de Hola de hello **MainPage** constructor, agregue Hola siguiente evento open de línea toosubscribe toohello origen adaptable:
   
         adaptiveSourceManager.AdaptiveSourceOpenedEvent += 
           new AdaptiveSourceOpenedEventHandler(mediaElement_AdaptiveSourceOpened);
5. Presione **CTRL+S** archivo de hello toosave.

**controladores de eventos de nivel de origen adaptable de tooadd**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Hola interior **MainPage** clase, agregue Hola siguiente miembro de datos:
   
     private AdaptiveSourceStatusUpdatedEventArgs adaptiveSourceStatusUpdate;   private Manifest manifestObject;
3. Al final de Hola de hello **MainPage** clase, agregue Hola después de controladores de eventos:

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
4. Al final de Hola de hello **mediaElement AdaptiveSourceOpened** método, agregue Hola después de codificar toosubscribe toohello eventos:
   
         adaptiveSource.ManifestReadyEvent +=

                    mediaElement_ManifestReady;
         adaptiveSource.AdaptiveSourceStatusUpdatedEvent += 

            mediaElement_AdaptiveSourceStatusUpdated;
         adaptiveSource.AdaptiveSourceFailedEvent += 

            mediaElement_AdaptiveSourceFailed;
5. Presione **CTRL+S** archivo de hello toosave.

Hola mismos eventos están disponibles en adaptable Manager nivel de origen, que puede utilizarse para controlar los elementos de la media de tooall comunes de la funcionalidad de la aplicación hello. Cada AdaptiveSource incluye sus propios eventos y todos los eventos AdaptiveSource se aplicarán en cascada debajo de AdaptiveSourceManager.

**controladores de eventos del elemento multimedia tooadd**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Al final de Hola de hello **MainPage** clase, agregue Hola después de controladores de eventos:

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
3. Al final de Hola de hello **MainPage** constructor, agregue Hola después de codificar toosubscript toohello eventos:

         mediaElement.MediaOpened += MediaOpened;
         mediaElement.MediaEnded += MediaEnded;
         mediaElement.MediaFailed += MediaFailed;
4. Presione **CTRL+S** archivo de hello toosave.

**control deslizante tooadd relacionados con código de barras**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. En principio de Hola de archivo hello, agregue el siguiente de hello instrucción using:
      
        using Windows.UI.Core;
3. Hola interior **MainPage** clase, agregue Hola después de los miembros de datos:
   
         public static CoreDispatcher _dispatcher;
         private DispatcherTimer sliderPositionUpdateDispatcher;
4. Al final de Hola de hello **MainPage** constructor, agregue Hola siguiente código:
   
         _dispatcher = Window.Current.Dispatcher;
         PointerEventHandler pointerpressedhandler = new PointerEventHandler(sliderProgress_PointerPressed);
         sliderProgress.AddHandler(Control.PointerPressedEvent, pointerpressedhandler, true);    
5. Al final de Hola de hello **MainPage** clase, agregue el siguiente código de hello:

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
>CoreDispatcher es cambios toomake usado toohello interfaz de usuario de subproceso del subproceso de interfaz de usuario no. En el caso de cuello de botella en el subproceso de distribución, el desarrollador puede elegir toouse distribuidor proporcionada por elemento de interfaz de usuario que tenga la intención de tooupdate.  Por ejemplo:
   
         await sliderProgress.Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () => { TimeSpan 

         timespan = new TimeSpan(adaptiveSourceStatusUpdate.EndTime); 
         double absvalue  = (int)Math.Round(timespan.TotalSeconds, MidpointRounding.AwayFromZero); 

         sliderProgress.Maximum = absvalue; }); 
6. Al final de Hola de hello **mediaElement_AdaptiveSourceStatusUpdated** método, agregar el siguiente código de hello:

         setSliderStartTime(args.StartTime);
         setSliderEndTime(args.EndTime);
7. Al final de Hola de hello **MediaOpened** método, agregar el siguiente código de hello:

         sliderProgress.StepFrequency = SliderFrequency(mediaElement.NaturalDuration.TimeSpan);
         sliderProgress.Width = mediaElement.Width;
         setupTimer();
8. Presione **CTRL+S** archivo de hello toosave.

**toocompile y prueba una aplicación Hola**

1. Presione **F6** proyecto de hello toocompile. 
2. Presione **F5** aplicación de hello toorun.
3. Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente. 
4. Haga clic en **Establecer origen**. 
5. Barra del control deslizante de Hola de prueba.

Ha completado la lección 2.  En esta lección, ha agregado un tooapplication del control deslizante. 

## <a name="lesson-3-select-smooth-streaming-streams"></a>Lección 3: Selección de secuencias de Smooth Streaming
Transmisión por secuencias suave es toostream compatibles con contenido con varias pistas de audio de lenguaje que se pueden seleccionar mediante visores de Hola.  En esta lección, podrá aplicar secuencias de tooselect visores. Esta lección contiene Hola procedimientos siguientes:

1. Modificar el archivo XAML de hello
2. Modificar el archivo de behand de código de hello
3. Compilar y probar la aplicación hello

**archivo XAML de hello toomodify**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Diseñador de vistas**.
2. Busque &lt;Grid.RowDefinitions&gt;y modificar Hola RowDefinitions por lo que el siguiente aspecto:
   
         <Grid.RowDefinitions>            
            <RowDefinition Height="20"/>
            <RowDefinition Height="50"/>
            <RowDefinition Height="100"/>
            <RowDefinition Height="80"/>
            <RowDefinition Height="50"/>
         </Grid.RowDefinitions>
3. Hola interior &lt;cuadrícula&gt;&lt;/Grid&gt; etiquetas, agregar Hola de código siguiente toodefine un control de cuadro de lista, por lo que los usuarios pueden ver lista de Hola de secuencias disponibles y seleccione secuencias:

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
4. Presione **CTRL+S** cambios de hello toosave.

**toomodify Hola archivo de código subyacente**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Dentro de espacio de nombres de hello SSPlayer, agregue una nueva clase:
   
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
3. En principio Hola de hello clase MainPage, agregue Hola después de definiciones de variables:
   
         private List<Stream> availableStreams;
         private List<Stream> availableAudioStreams;
         private List<Stream> availableTextStreams;
         private List<Stream> availableVideoStreams;
4. Dentro de la clase MainPage hello, agregue Hola después de región:
   
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
5. Busque el método mediaElement_ManifestReady de hello, anexar Hola siguiente código al final de Hola de función hello:
   
        getStreams(manifestObject);
        refreshAvailableStreamsListBoxItemSource();
   
    Por lo que cuando MediaElement manifiesto esté preparado, código de hello Obtiene una lista de secuencias disponibles hello y rellena el cuadro de lista de interfaz de usuario de hello con lista de Hola.
6. Dentro de la clase MainPage hello, busque botones de la interfaz de usuario de hello haga clic en la región de eventos y, a continuación, agregue Hola después de la definición de función:
   
        private void btnChangeStream_Click(object sender, RoutedEventArgs e)
        {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();
   
            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);
   
            // Change streams on hello presentation
            changeStreams(selectedStreams);
        }

**toocompile y prueba una aplicación Hola**

1. Presione **F6** proyecto de hello toocompile. 
2. Presione **F5** aplicación de hello toorun.
3. Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente. 
4. Haga clic en **Establecer origen**. 
5. idioma predeterminado de Hello es audio_eng. Intente tooswitch entre audio_eng y audio_es. Cada vez, seleccione un nuevo flujo, debe hacer clic en el botón de envío de Hola.

Ha completado la lección 3.  En esta lección, agregar secuencias de hello funcionalidad toochoose.

## <a name="lesson-4-select-smooth-streaming-tracks"></a>Lección 4: Selección de pistas de Smooth Streaming
Una presentación de Smooth Streaming puede contener varios archivos de vídeo codificados con diferentes niveles de calidad (velocidad de bits) y resoluciones. En esta lección, podrá aplicar realiza un seguimiento de los usuarios tooselect. Esta lección contiene Hola procedimientos siguientes:

1. Modificar el archivo XAML de hello
2. Modificar el archivo de behand de código de hello
3. Compilar y probar la aplicación hello

**archivo XAML de hello toomodify**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Diseñador de vistas**.
2. Busque hello &lt;cuadrícula&gt; etiqueta con nombre hello **gridStreamAndBitrateSelection**, anexar Hola siguiente código al final de Hola de etiqueta de hello:
   
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
3. Presione **CTRL+S** toosave cambia

**toomodify Hola archivo de código subyacente**

1. En el Explorador de soluciones, haga clic con el botón derecho en **MainPage.xaml** y haga clic en **Ver código**.
2. Dentro de espacio de nombres de hello SSPlayer, agregue una nueva clase:
   
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
3. En principio Hola de hello clase MainPage, agregue Hola después de definiciones de variables:
   
        private List<Track> availableTracks;
4. Dentro de la clase MainPage hello, agregue Hola después de región:
   
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
5. Busque el método mediaElement_ManifestReady de hello, anexar Hola siguiente código al final de Hola de función hello:
   
         getTracks(manifestObject);
         refreshAvailableTracksListBoxItemSource();
6. Dentro de la clase MainPage hello, busque botones de la interfaz de usuario de hello haga clic en la región de eventos y, a continuación, agregue Hola después de la definición de función:
   
         private void btnChangeStream_Click(object sender, RoutedEventArgs e)
         {
            List<IManifestStream> selectedStreams = new List<IManifestStream>();

            // Create a list of hello selected streams
            createSelectedStreamsList(selectedStreams);

            // Change streams on hello presentation
            changeStreams(selectedStreams);
         }

**toocompile y prueba una aplicación Hola**

1. Presione **F6** proyecto de hello toocompile. 
2. Presione **F5** aplicación de hello toorun.
3. Hola parte superior de aplicación hello, puede usar valor predeterminado de hello URL de Smooth Streaming o escriba uno diferente. 
4. Haga clic en **Establecer origen**. 
5. De forma predeterminada, se seleccionan todas las pistas de hello hello secuencia de vídeo. Hola tooexperiment cambios de velocidad de bits, puede seleccionar la velocidad de bits más baja de hello disponible y, a continuación, seleccione la velocidad de bits más alta de hello disponible. Debe hacer clic en Submit después de realizar cada uno de los cambios.  Puede ver los cambios de la calidad del vídeo de Hola.

Ha completado la lección 4.  En esta lección, agregará Hola funcionalidad toochoose realiza un seguimiento.

## <a name="media-services-learning-paths"></a>Rutas de aprendizaje de Servicios multimedia
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Envío de comentarios
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="other-resources"></a>Otros recursos:
* [¿Cómo toobuild una aplicación Smooth Streaming Windows 8 JavaScript con las características avanzadas](http://blogs.iis.net/cenkd/archive/2012/08/10/how-to-build-a-smooth-streaming-windows-8-javascript-application-with-advanced-features.aspx)
* [Información técnica sobre Smooth Streaming](http://www.iis.net/learn/media/on-demand-smooth-streaming/smooth-streaming-technical-overview)

[PlayerApplication]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-1.png
[CodeViewPic]: ./media/media-services-build-smooth-streaming-apps/SSClientWin8-2.png

