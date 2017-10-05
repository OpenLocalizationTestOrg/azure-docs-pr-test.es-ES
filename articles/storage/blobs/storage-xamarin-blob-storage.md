---
title: Uso de Blob Storage en Xamarin | Microsoft Docs
description: "La biblioteca de cliente de Azure Storage para Xamarin permite a los desarrolladores crear aplicaciones iOS, Android y de la Tienda Windows con sus interfaces de usuario nativas. Este tutorial muestra cómo usar Xamarin para crear una aplicación Android que usa Azure Blob Storage."
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
ms.openlocfilehash: 5ff4d86082c03dcd7098743a984a97aa70232d1d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-xamarin"></a><span data-ttu-id="7e344-104">Uso de Blob Storage desde Xamarin</span><span class="sxs-lookup"><span data-stu-id="7e344-104">How to use Blob Storage from Xamarin</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

## <a name="overview"></a><span data-ttu-id="7e344-105">Información general</span><span class="sxs-lookup"><span data-stu-id="7e344-105">Overview</span></span>
<span data-ttu-id="7e344-106">Xamarin permite a los desarrolladores usar un código base C# compartida para crear aplicaciones de iOS, Android y de la Tienda Windows con sus interfaces de usuario nativas.</span><span class="sxs-lookup"><span data-stu-id="7e344-106">Xamarin enables developers to use a shared C# codebase to create iOS, Android, and Windows Store apps with their native user interfaces.</span></span> <span data-ttu-id="7e344-107">En este tutorial se muestra cómo usar Azure Blob Storage con una aplicación de Xamarin.</span><span class="sxs-lookup"><span data-stu-id="7e344-107">This tutorial shows you how to use Azure Blob storage with a Xamarin application.</span></span> <span data-ttu-id="7e344-108">Si desea más información sobre Azure Storage, antes de entrar en el código, consulte [Introducción a Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7e344-108">If you'd like to learn more about Azure Storage, before diving into the code, see [Introduction to Microsoft Azure Storage](../common/storage-introduction.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-mobile-authentication-guidance](../../../includes/storage-mobile-authentication-guidance.md)]

## <a name="create-a-new-xamarin-application"></a><span data-ttu-id="7e344-109">Creación de una nueva aplicación Xamarin</span><span class="sxs-lookup"><span data-stu-id="7e344-109">Create a new Xamarin Application</span></span>
<span data-ttu-id="7e344-110">En este tutorial, crearemos una aplicación destinada a Android, iOS y Windows.</span><span class="sxs-lookup"><span data-stu-id="7e344-110">For this tutorial, we'll be creating an app that targets Android, iOS, and Windows.</span></span> <span data-ttu-id="7e344-111">Esta aplicación creará simplemente un contenedor y cargará un blob en este contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e344-111">This app will simply create a container and upload a blob into this container.</span></span> <span data-ttu-id="7e344-112">Aunque vamos a usar Visual Studio en Windows, se pueden aplicar los mismos conocimientos al crear una aplicación mediante Xamarin Studio en Mac OS.</span><span class="sxs-lookup"><span data-stu-id="7e344-112">We'll be using Visual Studio on Windows, but the same learnings can be applied when creating an app using Xamarin Studio on macOS.</span></span>

<span data-ttu-id="7e344-113">Para crear la aplicación, siga estos pasos:</span><span class="sxs-lookup"><span data-stu-id="7e344-113">Follow these steps to create your application:</span></span>

1. <span data-ttu-id="7e344-114">Si aún no lo ha hecho, descargue e instale o [Xamarin para Visual Studio](https://www.xamarin.com/download).</span><span class="sxs-lookup"><span data-stu-id="7e344-114">If you haven't already, download and install [Xamarin for Visual Studio](https://www.xamarin.com/download).</span></span>
2. <span data-ttu-id="7e344-115">Abra Visual Studio y cree una aplicación en blanco (nativa portátil): **Archivo > Nuevo > Proyecto > Multiplataforma > Aplicación en blanco (nativa portátil)**.</span><span class="sxs-lookup"><span data-stu-id="7e344-115">Open Visual Studio, and create a Blank App (Native Portable): **File > New > Project > Cross-Platform > Blank App(Native Portable)**.</span></span>
3. <span data-ttu-id="7e344-116">Haga clic con el botón derecho en la solución en el panel del Explorador de soluciones y seleccione **Administrar paquetes NuGet para la solución**.</span><span class="sxs-lookup"><span data-stu-id="7e344-116">Right-click your solution in the Solution Explorer pane and select **Manage NuGet Packages for Solution**.</span></span> <span data-ttu-id="7e344-117">Busque **WindowsAzure.Storage** e instale la versión estable más reciente para todos los proyectos de su solución.</span><span class="sxs-lookup"><span data-stu-id="7e344-117">Search for **WindowsAzure.Storage** and install the latest stable version to all projects in your solution.</span></span>
4. <span data-ttu-id="7e344-118">Compile y ejecute el proyecto.</span><span class="sxs-lookup"><span data-stu-id="7e344-118">Build and run your project.</span></span>

<span data-ttu-id="7e344-119">Ahora debería tener una aplicación que le permita hacer clic en un botón e incrementar un contador.</span><span class="sxs-lookup"><span data-stu-id="7e344-119">You should now have an application that allows you to click a button which increments a counter.</span></span>

## <a name="create-container-and-upload-blob"></a><span data-ttu-id="7e344-120">Creación de un contenedor y carga de un blob</span><span class="sxs-lookup"><span data-stu-id="7e344-120">Create container and upload blob</span></span>
<span data-ttu-id="7e344-121">Después, en su proyecto `(Portable)`, agregará código a `MyClass.cs`.</span><span class="sxs-lookup"><span data-stu-id="7e344-121">Next, under your `(Portable)` project, you'll add some code to `MyClass.cs`.</span></span> <span data-ttu-id="7e344-122">Este código crea un contenedor y carga un blob en dicho contenedor.</span><span class="sxs-lookup"><span data-stu-id="7e344-122">This code creates a container and uploads a blob into this container.</span></span> <span data-ttu-id="7e344-123">`MyClass.cs` debería ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="7e344-123">`MyClass.cs` should look like the following:</span></span>

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

            // Create the blob client.
            CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

            // Retrieve reference to a previously created container.
            CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

            // Create the container if it doesn't already exist.
            await container.CreateIfNotExistsAsync();

            // Retrieve reference to a blob named "myblob".
            CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

            // Create the "myblob" blob with the text "Hello, world!"
            await blockBlob.UploadTextAsync("Hello, world!");
        }
    }
}
```

<span data-ttu-id="7e344-124">Asegúrese de reemplazar "su_nombre_de_cuenta_aquí" y "su_clave_de_cuenta_aquí" por el nombre de cuenta y la clave de cuenta reales.</span><span class="sxs-lookup"><span data-stu-id="7e344-124">Make sure to replace "your_account_name_here" and "your_account_key_here" with your actual account name and account key.</span></span> 

<span data-ttu-id="7e344-125">Todos los proyectos para iOS, Android y Windows Phone tienen referencias al proyecto portátil, lo que significa que puede escribir todo su código compartido en un lugar y utilizarlo en todos los proyectos.</span><span class="sxs-lookup"><span data-stu-id="7e344-125">Your iOS, Android, and Windows Phone projects all have references to your Portable project - meaning you can write all of your shared code in one place and use it across all of your projects.</span></span> <span data-ttu-id="7e344-126">Ahora puede agregar la siguiente línea de código a cada proyecto para empezar a aprovechar: `MyClass.performBlobOperation()`</span><span class="sxs-lookup"><span data-stu-id="7e344-126">You can now add the following line of code to each project to start taking advantage: `MyClass.performBlobOperation()`</span></span>

### <a name="xamarinappdroid--mainactivitycs"></a><span data-ttu-id="7e344-127">XamarinApp.Droid > MainActivity.cs</span><span class="sxs-lookup"><span data-stu-id="7e344-127">XamarinApp.Droid > MainActivity.cs</span></span>

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

            // Set our view from the "main" layout resource
            SetContentView (Resource.Layout.Main);

            // Get our button from the layout resource,
            // and attach an event to it
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

### <a name="xamarinappios--viewcontrollercs"></a><span data-ttu-id="7e344-128">XamarinApp.iOS > ViewController.cs</span><span class="sxs-lookup"><span data-stu-id="7e344-128">XamarinApp.iOS > ViewController.cs</span></span>

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
                // Perform any additional setup after loading the view, typically from a nib.
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

### <a name="xamarinappwinphone--mainpagexaml--mainpagexamlcs"></a><span data-ttu-id="7e344-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span><span class="sxs-lookup"><span data-stu-id="7e344-129">XamarinApp.WinPhone > MainPage.xaml > MainPage.xaml.cs</span></span>

```csharp
using Windows.UI.Xaml.Controls;
using Windows.UI.Xaml.Navigation;

// The Blank Page item template is documented at http://go.microsoft.com/fwlink/?LinkId=391641

namespace XamarinApp.WinPhone
{
    /// <summary>
    /// An empty page that can be used on its own or navigated to within a Frame.
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
        /// Invoked when this page is about to be displayed in a Frame.
        /// </summary>
        /// <param name="e">Event data that describes how this page was reached.
        /// This parameter is typically used to configure the page.</param>
        protected override async void OnNavigatedTo(NavigationEventArgs e)
        {
            int count = 1;

            public MainPage()
            {
                this.InitializeComponent();

                this.NavigationCacheMode = NavigationCacheMode.Required;
            }

            /// <summary>
            /// Invoked when this page is about to be displayed in a Frame.
            /// </summary>
            /// <param name="e">Event data that describes how this page was reached.
            /// This parameter is typically used to configure the page.</param>
            protected override async void OnNavigatedTo(NavigationEventArgs e)
            {
                // TODO: Prepare page for display here.

                // TODO: If your application contains multiple pages, ensure that you are
                // handling the hardware Back button by registering for the
                // Windows.Phone.UI.Input.HardwareButtons.BackPressed event.
                // If you are using the NavigationHelper provided by some templates,
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

## <a name="run-the-application"></a><span data-ttu-id="7e344-130">Ejecución de la aplicación</span><span class="sxs-lookup"><span data-stu-id="7e344-130">Run the application</span></span>
<span data-ttu-id="7e344-131">Ahora puede ejecutar esta aplicación en un emulador Android o Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="7e344-131">You can now run this application in an Android or Windows Phone emulator.</span></span> <span data-ttu-id="7e344-132">También puede ejecutar esta aplicación en un emulador de iOS, pero necesitará un equipo Mac.</span><span class="sxs-lookup"><span data-stu-id="7e344-132">You can also run this application in an iOS emulator, but this will require a Mac.</span></span> <span data-ttu-id="7e344-133">Para obtener instrucciones específicas al respecto, lea la documentación sobre [cómo conectar Visual Studio con un equipo Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span><span class="sxs-lookup"><span data-stu-id="7e344-133">For specific instructions on how to do this, please read the documentation for [connecting Visual Studio to a Mac](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/connecting-to-mac/)</span></span>

<span data-ttu-id="7e344-134">Después de ejecutar su aplicación, se creará el contenedor `mycontainer` en su cuenta de Storage.</span><span class="sxs-lookup"><span data-stu-id="7e344-134">Once you run your app, it will create the container `mycontainer` in your Storage account.</span></span> <span data-ttu-id="7e344-135">Contendrá el blob `myblob`, que tiene el texto `Hello, world!`.</span><span class="sxs-lookup"><span data-stu-id="7e344-135">It should contain the blob, `myblob`, which has the text, `Hello, world!`.</span></span> <span data-ttu-id="7e344-136">Para comprobar esto, use el [Explorador de Microsoft Azure Storage](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="7e344-136">You can verify this by using the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e344-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="7e344-137">Next steps</span></span>
<span data-ttu-id="7e344-138">En este tutorial, aprendió a crear una aplicación multiplataforma en Xamarin que usa Azure Storage, centrándose específicamente en un escenario en Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="7e344-138">In this tutorial, you learned how to create a cross-platform application in Xamarin that uses Azure Storage, specifically focusing on one scenario in Blob Storage.</span></span> <span data-ttu-id="7e344-139">Pero se puede hacer mucho más no solo con Blob Storage, sino también con Table, File y Queue Storage.</span><span class="sxs-lookup"><span data-stu-id="7e344-139">However, you can do a lot more with not only Blob Storage, but also with Table, File, and Queue Storage.</span></span> <span data-ttu-id="7e344-140">Consulte los artículos siguientes para más información:</span><span class="sxs-lookup"><span data-stu-id="7e344-140">Please check out the following articles to learn more:</span></span>

* [<span data-ttu-id="7e344-141">Introducción al Almacenamiento de blobs de Azure mediante .NET</span><span class="sxs-lookup"><span data-stu-id="7e344-141">Get started with Azure Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="7e344-142">Introducción a Azure Table Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="7e344-142">Get started with Azure Table storage using .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="7e344-143">Introducción a Azure Queue Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="7e344-143">Get started with Azure Queue storage using .NET</span></span>](../queues/storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="7e344-144">Introducción a Azure File Storage en Windows</span><span class="sxs-lookup"><span data-stu-id="7e344-144">Get started with Azure File storage on Windows</span></span>](../files/storage-dotnet-how-to-use-files.md)

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

