---
title: "aaaAzure AD v2 Windows Desktop introducción - el programa de instalación | Documentos de Microsoft"
description: "Cómo pueden llamar las aplicaciones .NET de escritorio de Windows (XAML) a una API que requiera tokens de acceso mediante el punto de conexión de Azure Active Directory v2"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 097ea99bef01e15edaa5ff914ff4e18392b77c5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
## <a name="set-up-your-project"></a><span data-ttu-id="51ff6-103">Configurar su proyecto</span><span class="sxs-lookup"><span data-stu-id="51ff6-103">Set up your project</span></span>

<span data-ttu-id="51ff6-104">En esta sección proporciona instrucciones paso a paso sobre cómo toocreate un nuevo toodemonstrate proyecto cómo toointegrate .NET de escritorio de Windows (XAML) de la aplicación con *inicie sesión con Microsoft* para que pueden consultar las API Web que requiere un token.</span><span class="sxs-lookup"><span data-stu-id="51ff6-104">This section provides step-by-step instructions for how toocreate a new project toodemonstrate how toointegrate a Windows Desktop .NET application (XAML) with *Sign-In with Microsoft* so it can query Web APIs that requires a token.</span></span>

<span data-ttu-id="51ff6-105">aplicación Hello creado por esta guía muestra un botón toograph y mostrar los resultados en pantalla y un botón de cierre de sesión.</span><span class="sxs-lookup"><span data-stu-id="51ff6-105">hello application created by this guide exposes a button toograph and show results on screen and a sign-out button.</span></span>

> <span data-ttu-id="51ff6-106">¿Prefiere toodownload proyecto de Visual Studio de este ejemplo en su lugar?</span><span class="sxs-lookup"><span data-stu-id="51ff6-106">Prefer toodownload this sample's Visual Studio project instead?</span></span> <span data-ttu-id="51ff6-107">[Descargar un proyecto](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) y omitir toohello [paso de configuración](#create-an-application-express) ejemplo de código de hello tooconfigure antes de ejecutar.</span><span class="sxs-lookup"><span data-stu-id="51ff6-107">[Download a project](https://github.com/Azure-Samples/active-directory-dotnet-desktop-msgraph-v2/archive/master.zip) and skip toohello [Configuration step](#create-an-application-express) tooconfigure hello code sample before executing.</span></span>


### <a name="create-your-application"></a><span data-ttu-id="51ff6-108">Creación de la aplicación</span><span class="sxs-lookup"><span data-stu-id="51ff6-108">Create your application</span></span>
1. <span data-ttu-id="51ff6-109">En Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="51ff6-109">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="51ff6-110">En *Plantillas*, seleccione `Visual C#`.</span><span class="sxs-lookup"><span data-stu-id="51ff6-110">Under *Templates*, select `Visual C#`</span></span>
3. <span data-ttu-id="51ff6-111">Seleccione `WPF App` (o *aplicación WPF* según la versión de Hola de su Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="51ff6-111">Select `WPF App` (or *WPF Application* depending on hello version of your Visual Studio)</span></span>

## <a name="add-hello-microsoft-authentication-library-msal-tooyour-project"></a><span data-ttu-id="51ff6-112">Agregar proyecto de hello biblioteca de autenticación de Microsoft (MSAL) tooyour</span><span class="sxs-lookup"><span data-stu-id="51ff6-112">Add hello Microsoft Authentication Library (MSAL) tooyour project</span></span>
1. <span data-ttu-id="51ff6-113">En Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="51ff6-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="51ff6-114">Copiar y pegar siguiente Hola Hola ventana de la consola de administrador de paquetes:</span><span class="sxs-lookup"><span data-stu-id="51ff6-114">Copy/paste hello following in hello Package Manager Console window:</span></span>

```powershell
Install-Package Microsoft.Identity.Client -Pre
```

> <span data-ttu-id="51ff6-115">paquete de Hello anterior instala Hola biblioteca de autenticación de Microsoft (MSAL).</span><span class="sxs-lookup"><span data-stu-id="51ff6-115">hello package above installs hello Microsoft Authentication Library (MSAL).</span></span> <span data-ttu-id="51ff6-116">MSAL controla la adquisición, almacenamiento en caché y actualizar usuario toskens utiliza tooaccess API protegidas por Azure Active Directory v2.</span><span class="sxs-lookup"><span data-stu-id="51ff6-116">MSAL handles acquiring, caching and refreshing user toskens used tooaccess APIs protected by Azure Active Directory v2.</span></span>

## <a name="add-hello-code-tooinitialize-msal"></a><span data-ttu-id="51ff6-117">Agregar código de hello tooinitialize MSAL</span><span class="sxs-lookup"><span data-stu-id="51ff6-117">Add hello code tooinitialize MSAL</span></span>
<span data-ttu-id="51ff6-118">Este paso le ayudará a crear una interacción de toohandle de clase con la biblioteca de MSAL, como el control de tokens.</span><span class="sxs-lookup"><span data-stu-id="51ff6-118">This step will help you create a class toohandle interaction with MSAL Library, such as handling of tokens.</span></span>

1. <span data-ttu-id="51ff6-119">Abra hello `App.xaml.cs` de archivos y agregar referencia de hello para la clase MSAL biblioteca toohello:</span><span class="sxs-lookup"><span data-stu-id="51ff6-119">Open hello `App.xaml.cs` file and add hello reference for MSAL library toohello class:</span></span>

```csharp
using Microsoft.Identity.Client;
```
<!-- Workaround for Docs conversion bug -->
<ol start="2">
<li>
<span data-ttu-id="51ff6-120">Actualizar Hola aplicación clase toohello a continuación:</span><span class="sxs-lookup"><span data-stu-id="51ff6-120">Update hello App class toohello following:</span></span>
</li>
</ol>

```csharp
public partial class App : Application
{
    //Below is hello clientId of your app registration. 
    //You have tooreplace hello below with hello Application Id for your app registration
    private static string ClientId = "your_client_id_here";

    public static PublicClientApplication PublicClientApp = new PublicClientApplication(ClientId);

}
```

## <a name="create-your-applications-ui"></a><span data-ttu-id="51ff6-121">Creación de la IU de la aplicación</span><span class="sxs-lookup"><span data-stu-id="51ff6-121">Create your application’s UI</span></span>
<span data-ttu-id="51ff6-122">sección de Hello siguiente muestra cómo una aplicación puede consultar un servidor protegido de back-end como Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="51ff6-122">hello section below shows how an application can query a protected backend server like Microsoft Graph.</span></span> <span data-ttu-id="51ff6-123">Debe crearse un archivo MainWindow.xaml automáticamente como parte de la plantilla de proyecto.</span><span class="sxs-lookup"><span data-stu-id="51ff6-123">A MainWindow.xaml file should automatically be created as a part of your project template.</span></span> <span data-ttu-id="51ff6-124">Abra este archivo de este archivo y, a continuación, siga estas instrucciones hello:</span><span class="sxs-lookup"><span data-stu-id="51ff6-124">Open this file this file and then follow hello instructions below:</span></span>

<span data-ttu-id="51ff6-125">Reemplace la aplicación `<Grid>` con ser siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="51ff6-125">Replace your application’s `<Grid>` with be hello following:</span></span>

```xml
<Grid>
    <StackPanel Background="Azure">
        <StackPanel Orientation="Horizontal" HorizontalAlignment="Right">
            <Button x:Name="CallGraphButton" Content="Call Microsoft Graph API" HorizontalAlignment="Right" Padding="5" Click="CallGraphButton_Click" Margin="5" FontFamily="Segoe Ui"/>
            <Button x:Name="SignOutButton" Content="Sign-Out" HorizontalAlignment="Right" Padding="5" Click="SignOutButton_Click" Margin="5" Visibility="Collapsed" FontFamily="Segoe Ui"/>
        </StackPanel>
        <Label Content="API Call Results" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="ResultText" TextWrapping="Wrap" MinHeight="120" Margin="5" FontFamily="Segoe Ui"/>
        <Label Content="Token Info" Margin="0,0,0,-5" FontFamily="Segoe Ui" />
        <TextBox x:Name="TokenInfoText" TextWrapping="Wrap" MinHeight="70" Margin="5" FontFamily="Segoe Ui"/>
    </StackPanel>
</Grid>
```
