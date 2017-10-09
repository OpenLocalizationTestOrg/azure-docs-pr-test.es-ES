---
title: aaaHow toouse almacenamiento de blobs de Xamarin | Documentos de Microsoft
description: "Hola biblioteca de cliente de almacenamiento de Azure para Xamarin permite a los desarrolladores toocreate iOS, Android y aplicaciones de la tienda con sus interfaces de usuario nativas de Windows. Este tutorial se muestra cómo toouse Xamarin toocreate una aplicación que usa almacenamiento de blobs de Azure."
services: storage
documentationcenter: xamarin
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 44cb845d-cf78-4942-95b8-952da4f9a2c2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/11/2017
ms.author: michaelhauss
ms.openlocfilehash: 751f66d1d2392c8bcf6e5f8d1b185af73582fab3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a>¿Cómo toouse almacenamiento de blobs de Xamarin
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a>Información general
Xamarin permite a los desarrolladores toouse compartido C# codebase toocreate iOS, Android y aplicaciones de la tienda con sus interfaces de usuario nativas de Windows. Este tutorial muestra cómo toouse almacenamiento de blobs de Azure con una aplicación de Xamarin. Si desea que toolearn más sobre el almacenamiento de Azure, antes de entrar en el código de hello, consulte [Introducción tooMicrosoft almacenamiento de Azure](storage-introduction.md).

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a>Creación de una nueva aplicación Xamarin
En este tutorial, crearemos una aplicación destinada a Android, iOS y Windows. Esta aplicación creará simplemente un contenedor y cargará un blob en este contenedor. Nos vamos a usar Visual Studio en Windows, pero Hola aprendizajes mismo pueden aplicarse al crear una aplicación con Xamarin Studio en macOS.

Siga estos pasos toocreate la aplicación:

1. Si aún no lo ha hecho, descargue e instale o [Xamarin para Visual Studio](https://www.xamarin.com/download).
2. Abra Visual Studio y cree una aplicación en blanco (nativa portátil): **Archivo > Nuevo > Proyecto > Multiplataforma > Aplicación en blanco (nativa portátil)**.
3. Haga clic en la solución en el panel del explorador de soluciones de Hola y seleccione **administrar paquetes de NuGet para la solución**. Busque **WindowsAzure.Storage** e instalar proyectos tooall de la versión estable más recientes de hello en la solución.
4. Compile y ejecute el proyecto.

Ahora debería tener una aplicación que permita tooclick un botón que se incrementa un contador.

## <a name="create-container-and-upload-blob"></a>Creación de un contenedor y carga de un blob
Después, en su `(Portable)` proyecto, agregará código demasiado`MyClass.cs`. Este código crea un contenedor y carga un blob en dicho contenedor. `MyClass.cs`debería ser similar Hola siguiente:

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using System.Threading.Tasks;

namespace XamarinApp
{
    public class MyClass
    {
        public MyClass ()
        {
        }

        public static async Task performBlobOperation()
        {
            // Retrieve storage account from connection string.
            CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=your_account_name_here;AccountKey=your_account_key_here");

            // Create hello blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference tooa previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create hello container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference tooa blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create hello "myblob" blob with hello text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

Asegúrese de que tooreplace "your_account_name_here" y "your_account_key_here" con el nombre de la cuenta real y la clave de cuenta. 

Su iOS, Android y Windows Phone todos los proyectos tienen Portable tooyour de referencias proyecto - lo que significa que puede escribir todo su código compartido en uno coloque y utilizarlo en todos los proyectos. Ahora puede agregar Hola después de la línea de código tooeach proyecto toostart gracias a las ventajas:`MyClass.performBlobOperation()`

### <a name="xamarinappdroid--mainactivitycs"></a>XamarinApp.Droid > MainActivity.cs

```csharp
using Android.App;
using Android.Widget;
using Android.OS;

namespace XamarinApp.Droid
{
    [Activity (Label = "XamarinApp.Droid", MainLauncher = true, Icon = "@drawable/icon")]
    public class MainActivity : Activity
    {
        int count = 1;

        protected override async void OnCreate (Bundle bundle)
        {
            base.OnCreate (bundle);

            // Set our view from hello "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from hello layout resource,
            // and attach an event tooit
            Button button = FindViewById<Button> (Resource.Id.myButton);

            button.Click += delegate {
                button.Text = string.Format ("{0} clicks!", count++);
            };

            await MyClass.performBlobOperation();
            }
        }
    }
}
```

### <a name="xamarinappios--viewcontrollercs"></a>XamarinApp.iOS > ViewController.cs

```csharp
using System;
using UIKit;

namespace XamarinApp.iOS
{
    public partial class ViewController : UIViewController
    {
        int count = 1;

        public ViewController (IntPtr handle) : base (handle)
        {
        }

        public override async void ViewDidLoad ()
        {
            int count = 1;

            public ViewController (IntPtr handle) : base (handle)
            {
            }

            public override async void ViewDidLoad ()
            {
                base.ViewDidLoad ();
                // Perform any additional setup after loading hello view, typically from a nib.
                Button.AccessibilityIdentifier = "myButton";
                Button.TouchUpInside += delegate {
                    var title = string.Format ("{0} clicks!", count++);
                    Button.SetTitle (title, UIControlState.Normal);
                };

                await MyClass.performBlobOperation();
            }

            public override void DidReceiveMemoryWarning ()
            {
                base.DidReceiveMemoryWarning ();
                // Release any cached data, images, etc that aren't in use.
            }
        }
    }
}
```

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a>XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// hello Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated toowithin a Frame.
    /// </summary>
    public sealed partial class MainPage : Page
    {
        int count = 1;

        public MainPage()
        {
            this.InitializeComponent();

            this.NavigationCacheMode = NavigationCacheMode.Required;
        }

        /// <summary>
        /// Invoked when this page is about toobe displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used tooconfigure hello page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about toobe displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used tooconfigure hello page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling hello hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using hello NavigationHelper provided by some templates,
                // this event is handled for you.
                Button.Click += delegate {
                    var title = string.Format("{0} clicks!", count++);
                    Button.Content = title;
                };

                await MyClass.performBlobOperation();
            }
        }
    }
}
```

## <a name="run-hello-application"></a>Ejecutar la aplicación hello
Ahora puede ejecutar esta aplicación en un emulador Android o Windows Phone. También puede ejecutar esta aplicación en un emulador de iOS, pero necesitará un equipo Mac. Para obtener instrucciones específicas sobre cómo toodo esto, lea la documentación de Hola para [conectar Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)

Una vez que ejecute la aplicación, creará el contenedor de hello `mycontainer` en su cuenta de almacenamiento. Debe contener el blob de hello, `myblob`, que tiene texto hello, `Hello, world!`. Puede comprobarlo mediante el uso de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha aprendido cómo toocreate una aplicación multiplataforma en Xamarin que utiliza el almacenamiento de Azure, centrándose específicamente en un escenario en el almacenamiento de blobs. Pero se puede hacer mucho más no solo con Blob Storage, sino también con Table, File y Queue Storage. Consulte la Hola siguiendo artículos toolearn más:

* [Introducción al Almacenamiento de blobs de Azure mediante .NET](storage-dotnet-how-to-use-blobs.md)
* [Introducción al Almacenamiento de tablas de Azure mediante .NET](storage-dotnet-how-to-use-tables.md)
* [Introducción al Almacenamiento en cola de Azure mediante .NET](storage-dotnet-how-to-use-queues.md)
* [Introducción a Azure File Storage en Windows](storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

