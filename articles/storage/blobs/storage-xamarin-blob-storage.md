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
ms.openlocfilehash: 688484fc560b5c89ed1692f5cbf5713aa8fc90a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-xamarin"></a><span data-ttu-id="60148-104">¿Cómo toouse almacenamiento de blobs de Xamarin</span><span class="sxs-lookup"><span data-stu-id="60148-104">How toouse Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="60148-105">Información general</span><span class="sxs-lookup"><span data-stu-id="60148-105">Overview</span></span>
<span data-ttu-id="60148-106">Xamarin permite a los desarrolladores toouse compartido C# codebase toocreate iOS, Android y aplicaciones de la tienda con sus interfaces de usuario nativas de Windows.</span><span class="sxs-lookup"><span data-stu-id="60148-106">Xamarin enables developers toouse a shared C# codebase toocreate iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="60148-107">Este tutorial muestra cómo toouse almacenamiento de blobs de Azure con una aplicación de Xamarin.</span><span class="sxs-lookup"><span data-stu-id="60148-107">This tutorial shows you how toouse Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="60148-108">Si desea que toolearn más sobre el almacenamiento de Azure, antes de entrar en el código de hello, consulte [Introducción tooMicrosoft almacenamiento de Azure](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="60148-108">If you'd like toolearn more about Azure Storage, before diving into hello code, see [Introduction tooMicrosoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="60148-109">Creación de una nueva aplicación Xamarin</span><span class="sxs-lookup"><span data-stu-id="60148-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="60148-110">En este tutorial, crearemos una aplicación destinada a Android, iOS y Windows.</span><span class="sxs-lookup"><span data-stu-id="60148-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="60148-111">Esta aplicación creará simplemente un contenedor y cargará un blob en este contenedor.</span><span class="sxs-lookup"><span data-stu-id="60148-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="60148-112">Nos vamos a usar Visual Studio en Windows, pero Hola aprendizajes mismo pueden aplicarse al crear una aplicación con Xamarin Studio en macOS.</span><span class="sxs-lookup"><span data-stu-id="60148-112">We'll be using Visual Studio on Windows, but hello same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="60148-113">Siga estos pasos toocreate la aplicación:</span><span class="sxs-lookup"><span data-stu-id="60148-113">Follow these steps toocreate your application:</span></span>

1. <span data-ttu-id="60148-114">Si aún no lo ha hecho, descargue e instale o [Xamarin para Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="60148-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="60148-115">Abra Visual Studio y cree una aplicación en blanco (nativa portátil): **Archivo > Nuevo > Proyecto > Multiplataforma > Aplicación en blanco (nativa portátil)**.</span><span class="sxs-lookup"><span data-stu-id="60148-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="60148-116">Haga clic en la solución en el panel del explorador de soluciones de Hola y seleccione **administrar paquetes de NuGet para la solución**.</span><span class="sxs-lookup"><span data-stu-id="60148-116">Right-click your solution in hello Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="60148-117">Busque **WindowsAzure.Storage** e instalar proyectos tooall de la versión estable más recientes de hello en la solución.</span><span class="sxs-lookup"><span data-stu-id="60148-117">Search for **WindowsAzure.Storage** and install hello latest stable version tooall projects in your solution.</span></span>
4. <span data-ttu-id="60148-118">Compile y ejecute el proyecto.</span><span class="sxs-lookup"><span data-stu-id="60148-118">Build and run your project.</span></span>

<span data-ttu-id="60148-119">Ahora debería tener una aplicación que permita tooclick un botón que se incrementa un contador.</span><span class="sxs-lookup"><span data-stu-id="60148-119">You should now have an application that allows you tooclick a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="60148-120">Creación de un contenedor y carga de un blob</span><span class="sxs-lookup"><span data-stu-id="60148-120">Create container and upload blob</span></span>
<span data-ttu-id="60148-121">Después, en su `(Portable)` proyecto, agregará código demasiado`MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="60148-121">Next, under your `(Portable)` project, you'll add some code too`MyClass.cs`.</span></span> <span data-ttu-id="60148-122">Este código crea un contenedor y carga un blob en dicho contenedor.</span><span class="sxs-lookup"><span data-stu-id="60148-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="60148-123">`MyClass.cs`debería ser similar Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="60148-123">`MyClass.cs` should look like hello following:</span></span>

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

<span data-ttu-id="60148-124">Asegúrese de que tooreplace "your_account_name_here" y "your_account_key_here" con el nombre de la cuenta real y la clave de cuenta.</span><span class="sxs-lookup"><span data-stu-id="60148-124">Make sure tooreplace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="60148-125">Su iOS, Android y Windows Phone todos los proyectos tienen Portable tooyour de referencias proyecto - lo que significa que puede escribir todo su código compartido en uno coloque y utilizarlo en todos los proyectos.</span><span class="sxs-lookup"><span data-stu-id="60148-125">Your iOS, Android, and Windows Phone projects all have references tooyour Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="60148-126">Ahora puede agregar Hola después de la línea de código tooeach proyecto toostart gracias a las ventajas:`MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="60148-126">You can now add hello following line of code tooeach project toostart taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="60148-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="60148-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="60148-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="60148-128">XamarinApp.iOS > ViewController.cs</span></span>

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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="60148-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="60148-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

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

## <a name="run-hello-application"></a><span data-ttu-id="60148-130">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="60148-130">Run hello application</span></span>
<span data-ttu-id="60148-131">Ahora puede ejecutar esta aplicación en un emulador Android o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="60148-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="60148-132">También puede ejecutar esta aplicación en un emulador de iOS, pero necesitará un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="60148-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="60148-133">Para obtener instrucciones específicas sobre cómo toodo esto, lea la documentación de Hola para [conectar Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="60148-133">For specific instructions on how toodo this, please read hello documentation for [connecting Visual Studio tooa Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="60148-134">Una vez que ejecute la aplicación, creará el contenedor de hello `mycontainer` en su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="60148-134">Once you run your app, it will create hello container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="60148-135">Debe contener el blob de hello, `myblob`, que tiene texto hello, `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="60148-135">It should contain hello blob, `myblob`, which has hello text, `Hello, world!`.</span></span> <span data-ttu-id="60148-136">Puede comprobarlo mediante el uso de hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="60148-136">You can verify this by using hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60148-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="60148-137">Next steps</span></span>
<span data-ttu-id="60148-138">En este tutorial, ha aprendido cómo toocreate una aplicación multiplataforma en Xamarin que utiliza el almacenamiento de Azure, centrándose específicamente en un escenario en el almacenamiento de blobs.</span><span class="sxs-lookup"><span data-stu-id="60148-138">In this tutorial, you learned how toocreate a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="60148-139">Pero se puede hacer mucho más no solo con Blob Storage, sino también con Table, File y Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="60148-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="60148-140">Consulte la Hola siguiendo artículos toolearn más:</span><span class="sxs-lookup"><span data-stu-id="60148-140">Please check out hello following articles toolearn more:</span></span>

* [<span data-ttu-id="60148-141">Introducción al Almacenamiento de blobs de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="60148-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="60148-142">Introducción a Azure Table Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="60148-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="60148-143">Introducción a Azure Queue Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="60148-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="60148-144">Introducción a Azure File Storage en Windows</span><span class="sxs-lookup"><span data-stu-id="60148-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

