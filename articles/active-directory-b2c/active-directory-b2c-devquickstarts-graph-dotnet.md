---
title: 'Azure Active Directory B2C: uso de API Graph | Microsoft Docs'
description: "Cómo llamar a la API Graph para un inquilino de B2C mediante una identidad de aplicación para automatizar el proceso."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="9cd77-103">Azure AD B2C: uso de la API Graph</span><span class="sxs-lookup"><span data-stu-id="9cd77-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="9cd77-104">Los inquilinos de Azure Active Directory (Azure AD) B2C tienden a ser muy grandes.</span><span class="sxs-lookup"><span data-stu-id="9cd77-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="9cd77-105">Esto supone que muchas tareas comunes de administración de inquilinos necesitan realizarse mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="9cd77-106">Un ejemplo importante es la administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9cd77-106">A primary example is user management.</span></span> <span data-ttu-id="9cd77-107">Quizá necesite migrar un almacén de usuario existente a un inquilino de B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="9cd77-108">Puede que desee hospedar un registro de usuarios en su propia página y crear cuentas de usuario en su directorio de Azure AD B2C en segundo plano.</span><span class="sxs-lookup"><span data-stu-id="9cd77-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="9cd77-109">Estos tipos de tareas requieren la capacidad de crear, leer, actualizar y eliminar cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="9cd77-110">Puede realizar estas tareas mediante la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="9cd77-111">Para los inquilinos de B2C, existen dos modos de comunicación principales con la API Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="9cd77-112">Para las tareas interactivas, que se ejecutan una vez, deberá actuar como una cuenta de administrador en el inquilino de B2C al ejecutar las tareas.</span><span class="sxs-lookup"><span data-stu-id="9cd77-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="9cd77-113">Este modo requiere que un administrador inicie sesión con credenciales antes de que este pueda realizar llamadas a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="9cd77-114">Para las tareas automatizadas y continuas, tiene que usar algún tipo de cuenta de servicio a la que conceda los privilegios necesarios para realizar tareas de administración.</span><span class="sxs-lookup"><span data-stu-id="9cd77-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="9cd77-115">En Azure AD, puede hacerlo mediante el registro de una aplicación y la autenticación en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9cd77-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="9cd77-116">Esto se realiza con un **identificador de aplicación** que usa la [concesión de credenciales de cliente OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="9cd77-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="9cd77-117">En este caso, la aplicación actúa como tal, no como un usuario, para llamar a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="9cd77-118">En este artículo, abordaremos cómo realizar este caso de uso automatizado.</span><span class="sxs-lookup"><span data-stu-id="9cd77-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="9cd77-119">Para demostrarlo, crearemos un `B2CGraphClient` de .NET 4.5 que realiza operaciones de creación, lectura, actualización y eliminación (CRUD) de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="9cd77-120">El cliente tendrá una interfaz de línea de comandos (CLI) de Windows que permite invocar diversos métodos.</span><span class="sxs-lookup"><span data-stu-id="9cd77-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="9cd77-121">Sin embargo, el código se escribe para que se comporte de forma no interactiva y automatizada.</span><span class="sxs-lookup"><span data-stu-id="9cd77-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="9cd77-122">Obtención de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="9cd77-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="9cd77-123">Antes de crear aplicaciones, usuarios o interactuar con Azure AD, necesitará un inquilino de Azure AD B2C y una cuenta de administrador global en ese inquilino.</span><span class="sxs-lookup"><span data-stu-id="9cd77-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="9cd77-124">Si aún no tiene ningún inquilino, [comience con la introducción a Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9cd77-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="9cd77-125">Registro de la aplicación en el inquilino</span><span class="sxs-lookup"><span data-stu-id="9cd77-125">Register your application in your tenant</span></span>
<span data-ttu-id="9cd77-126">Una vez que tenga un inquilino B2C, debe registrar la aplicación a través de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cd77-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cd77-127">Para usar la API Graph con el inquilino B2C, deberá registrar una aplicación dedicada mediante la hoja *Registros de aplicaciones* genérica en Azure Portal, **NO** mediante la hoja *Aplicaciones* de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="9cd77-128">No puede volver a usar las aplicaciones B2C ya existentes que registró en la hoja *Aplicaciones* de Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="9cd77-129">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9cd77-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9cd77-130">Para elegir el inquilino de Azure AD B2C, seleccione una cuenta en la esquina superior derecha de la página.</span><span class="sxs-lookup"><span data-stu-id="9cd77-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="9cd77-131">En el panel de navegación izquierdo, elija **Más servicios**, haga clic en **Registros de aplicaciones**y, luego, en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="9cd77-132">Siga las indicaciones y cree una nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="9cd77-133">Seleccione **Aplicación web o API** como Tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="9cd77-134">Proporcione **cualquier URI de redirección** (p. ej., https://B2CGraphAPI), ya que no es relevante para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="9cd77-135">La aplicación aparecerá ahora en la lista de aplicaciones. Haga clic en ella para obtener el **Identificador de aplicación** (también conocido como id. de cliente).</span><span class="sxs-lookup"><span data-stu-id="9cd77-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="9cd77-136">Cópielo, pues lo necesitará en una sección posterior.</span><span class="sxs-lookup"><span data-stu-id="9cd77-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="9cd77-137">En la hoja Configuración, haga clic en **Claves** y agregue una nueva clave (también conocida como secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="9cd77-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="9cd77-138">Cópiela también para usarla en una sección posterior.</span><span class="sxs-lookup"><span data-stu-id="9cd77-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="9cd77-139">Configuración de permisos de creación, lectura y actualización para la aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd77-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="9cd77-140">Ahora debe configurar la aplicación para obtener todos los permisos necesarios para crear, leer, actualizar y eliminar usuarios.</span><span class="sxs-lookup"><span data-stu-id="9cd77-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="9cd77-141">Aún en la hoja Registros de aplicaciones de Azure Portal, seleccione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="9cd77-142">En la hoja Configuración, haga clic en **Permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="9cd77-143">En la hoja Permisos necesarios, haga clic en **Microsoft Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="9cd77-144">En la hoja Habilitar el acceso, seleccione el permiso **Leer y escribir en datos de directorio** en **Permisos de la aplicación** y haga clic en **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="9cd77-145">Por último, de nuevo en la hoja Permisos necesarios, haga clic en el botón **Conceder permisos**.</span><span class="sxs-lookup"><span data-stu-id="9cd77-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="9cd77-146">Ahora tiene una aplicación con permiso para crear, leer y actualizar usuarios en el inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="9cd77-147">Configuración de permisos de eliminación para la aplicación</span><span class="sxs-lookup"><span data-stu-id="9cd77-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="9cd77-148">Actualmente, el permiso *Leer y escribir en datos de directorio* **NO** incluye la capacidad de llevar a cabo cualquier eliminación, como la de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9cd77-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="9cd77-149">Si desea dotar a la aplicación de la capacidad de eliminar usuarios, deberá seguir estos pasos adicionales que hacen partícipe a PowerShell. De lo contrario, puede ir a la sección siguiente.</span><span class="sxs-lookup"><span data-stu-id="9cd77-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="9cd77-150">En primer lugar, descargue e instale el [Ayudante para el inicio de sesión de Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="9cd77-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="9cd77-151">A continuación, descargue e instale el [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="9cd77-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="9cd77-152">Una vez instalado el módulo de PowerShell, abra PowerShell y conéctese al inquilino de B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="9cd77-153">Después de ejecutar `Get-Credential`, se le pedirá un nombre de usuario y una contraseña. Escriba el nombre de usuario y la contraseña de la cuenta del administrador de inquilinos de B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9cd77-154">Debe usar una cuenta de administrador de inquilinos B2C que sea **local** para el inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="9cd77-155">Estas cuentas tienen este aspecto: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9cd77-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="9cd77-156">Ahora usaremos el **Identificador de aplicación** en el script siguiente para asignar a la aplicación el rol de administrador de cuentas de usuario que permitirá a esta eliminar usuarios.</span><span class="sxs-lookup"><span data-stu-id="9cd77-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="9cd77-157">Estos roles tienen identificadores conocidos, por lo que lo único que debe hacer es escribir el **Identificador de aplicación** en el siguiente script.</span><span class="sxs-lookup"><span data-stu-id="9cd77-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="9cd77-158">Ahora la aplicación cuenta con permisos para eliminar usuarios del inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="9cd77-159">Descarga, configuración y compilación del código de ejemplo</span><span class="sxs-lookup"><span data-stu-id="9cd77-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="9cd77-160">En primer lugar, descargue el código de ejemplo y ejecútelo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="9cd77-161">A continuación, lo examinaremos más de cerca.</span><span class="sxs-lookup"><span data-stu-id="9cd77-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="9cd77-162">Puede [descargar el código de ejemplo como archivo .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="9cd77-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="9cd77-163">También puede clonarlo en un directorio de su elección:</span><span class="sxs-lookup"><span data-stu-id="9cd77-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="9cd77-164">Abra la solución de Visual Studio `B2CGraphClient\B2CGraphClient.sln` en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9cd77-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="9cd77-165">En el proyecto `B2CGraphClient`, abra el archivo `App.config`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="9cd77-166">Reemplace las tres configuraciones de la aplicación por sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="9cd77-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="9cd77-167">A continuación, haga clic con el botón derecho en la solución `B2CGraphClient` y vuelva a compilar el ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="9cd77-168">Si todo es correcto, ahora debería tener un archivo ejecutable `B2C.exe` que se encuentra en `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="9cd77-169">Compilación de operaciones CRUD de usuario mediante la API Graph</span><span class="sxs-lookup"><span data-stu-id="9cd77-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="9cd77-170">Para usar B2CGraphClient, abra un símbolo del sistema de Windows `cmd` y cambie al directorio `Debug`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="9cd77-171">A continuación, ejecute el comando `B2C Help` .</span><span class="sxs-lookup"><span data-stu-id="9cd77-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="9cd77-172">Se mostrará una breve descripción de cada comando.</span><span class="sxs-lookup"><span data-stu-id="9cd77-172">This will display a brief description of each command.</span></span> <span data-ttu-id="9cd77-173">Cada vez que invoque uno de estos comandos, `B2CGraphClient` realiza una solicitud a la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="9cd77-174">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="9cd77-174">Get an access token</span></span>
<span data-ttu-id="9cd77-175">Cualquier solicitud a la API Graph requiere un token de acceso para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="9cd77-176">`B2CGraphClient` utiliza la Biblioteca de autenticación de Active Directory (ADAL) para ayudarle a adquirir tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cd77-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="9cd77-177">ADAL facilita la adquisición de tokens al proporcionar una API sencilla y ocuparse de algunos detalles importantes, como el almacenamiento en caché de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cd77-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="9cd77-178">Sin embargo, no tiene que usar ADAL para obtener tokens.</span><span class="sxs-lookup"><span data-stu-id="9cd77-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="9cd77-179">También puede obtener tokens elaborando solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="9cd77-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd77-180">Este ejemplo de código usa ADAL v2 para comunicarse con la API Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="9cd77-181">Debe usar AAL v2 o v3 con el fin de obtener los tokens de acceso que se pueden utilizar con la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="9cd77-182">Cuando se ejecuta `B2CGraphClient`, se crea una instancia de la clase `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="9cd77-183">El constructor para esta clase configura scaffolding de autenticación de ADAL:</span><span class="sxs-lookup"><span data-stu-id="9cd77-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="9cd77-184">Vamos a usar el comando `B2C Get-User` como ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="9cd77-185">Cuando se invoca `B2C Get-User` sin ninguna entrada adicional, la CLI llama al método `B2CGraphClient.GetAllUsers(...)`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="9cd77-186">Este método llama a `B2CGraphClient.SendGraphGetRequest(...)`, que envía una solicitud HTTP GET a la API Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="9cd77-187">Antes de que `B2CGraphClient.SendGraphGetRequest(...)` envíe la solicitud GET, primero obtiene un token de acceso mediante ADAL:</span><span class="sxs-lookup"><span data-stu-id="9cd77-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="9cd77-188">Puede obtener un token de acceso para la API Graph mediante una llamada al método `AuthenticationContext.AcquireToken(...)` de ADAL.</span><span class="sxs-lookup"><span data-stu-id="9cd77-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="9cd77-189">ADAL devuelve un `access_token` que representa la identidad de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="9cd77-190">Lectura de usuarios</span><span class="sxs-lookup"><span data-stu-id="9cd77-190">Read users</span></span>
<span data-ttu-id="9cd77-191">Si desea obtener una lista de usuarios o un usuario determinado de la API Graph, puede enviar una solicitud HTTP `GET` al punto de conexión `/users`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="9cd77-192">Una solicitud para todos los usuarios de un inquilino tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9cd77-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="9cd77-193">Para ver esta solicitud, ejecute:</span><span class="sxs-lookup"><span data-stu-id="9cd77-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="9cd77-194">Hay dos aspectos importantes que se deben tener en cuenta:</span><span class="sxs-lookup"><span data-stu-id="9cd77-194">There are two important things to note:</span></span>

* <span data-ttu-id="9cd77-195">El token de acceso adquirido mediante ADAL se agrega al encabezado `Authorization` según el esquema `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="9cd77-196">Para los inquilinos de B2C, debe usar el parámetro de consulta `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="9cd77-197">Estos dos detalles se controlan en el método `B2CGraphClient.SendGraphGetRequest(...)` :</span><span class="sxs-lookup"><span data-stu-id="9cd77-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="9cd77-198">Creación de cuentas de usuario consumidor</span><span class="sxs-lookup"><span data-stu-id="9cd77-198">Create consumer user accounts</span></span>
<span data-ttu-id="9cd77-199">Al crear cuentas de usuario en el inquilino de B2C, puede enviar una solicitud HTTP `POST` al punto de conexión `/users`:</span><span class="sxs-lookup"><span data-stu-id="9cd77-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="9cd77-200">La mayoría de las propiedades de esta solicitud son necesarias para crear usuarios consumidores.</span><span class="sxs-lookup"><span data-stu-id="9cd77-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="9cd77-201">Para obtener más información, haga clic [aquí](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="9cd77-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="9cd77-202">Tenga en cuenta que los comentarios `//` se han incluido con fines ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="9cd77-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="9cd77-203">No los incluya en una solicitud real.</span><span class="sxs-lookup"><span data-stu-id="9cd77-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="9cd77-204">Para ver la solicitud, ejecute uno de los siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="9cd77-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="9cd77-205">El comando `Create-User` toma un archivo .json como parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="9cd77-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="9cd77-206">Contiene una representación JSON de un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="9cd77-207">Hay dos archivos .json de ejemplo en el código de ejemplo: `usertemplate-email.json` y `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="9cd77-208">Puede modificar estos archivos para satisfacer sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="9cd77-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="9cd77-209">Además de los campos obligatorios anteriores, hay varios campos opcionales que puede usar incluidos en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="9cd77-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="9cd77-210">Encontrará detalles sobre los campos opcionales en la [referencia de entidad de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="9cd77-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="9cd77-211">Puede ver cómo se construye la solicitud POST en `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="9cd77-212">Adjunta un token de acceso al encabezado `Authorization` de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="9cd77-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="9cd77-213">Establece `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="9cd77-214">Incluye el objeto de usuario JSON en el cuerpo de la solicitud.</span><span class="sxs-lookup"><span data-stu-id="9cd77-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="9cd77-215">Si las cuentas que se van a migrar desde un almacén de usuario existente tienen menos seguridad de contraseña que la [seguridad de contraseña exigida por Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), puede deshabilitar el requisito de contraseña segura mediante el valor `DisableStrongPassword` de la propiedad `passwordPolicies`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="9cd77-216">Por ejemplo, puede modificar la solicitud de creación de usuario proporcionada anteriormente de la siguiente manera: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="9cd77-217">Actualización de cuentas de usuario consumidor</span><span class="sxs-lookup"><span data-stu-id="9cd77-217">Update consumer user accounts</span></span>
<span data-ttu-id="9cd77-218">Al actualizar objetos de usuario, el proceso es similar al que se utiliza para crear objetos de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="9cd77-219">Sin embargo, este proceso usa el método HTTP `PATCH` :</span><span class="sxs-lookup"><span data-stu-id="9cd77-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="9cd77-220">Intente actualizar un usuario mediante la actualización de los archivos JSON con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="9cd77-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="9cd77-221">A continuación, puede usar `B2CGraphClient` para ejecutar uno de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="9cd77-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="9cd77-222">Consulte el método `B2CGraphClient.SendGraphPatchRequest(...)` para obtener más información sobre cómo enviar esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="9cd77-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="9cd77-223">Búsqueda de usuarios</span><span class="sxs-lookup"><span data-stu-id="9cd77-223">Search users</span></span>
<span data-ttu-id="9cd77-224">Puede buscar usuarios en el inquilino de B2C de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="9cd77-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="9cd77-225">Una es con el identificador de objeto del usuario, y otra es con el identificador de inicio de sesión del usuario (es decir, la propiedad `signInNames` ).</span><span class="sxs-lookup"><span data-stu-id="9cd77-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="9cd77-226">Ejecute uno de los comandos siguientes para buscar un usuario específico:</span><span class="sxs-lookup"><span data-stu-id="9cd77-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="9cd77-227">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="9cd77-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="9cd77-228">Eliminación de usuarios</span><span class="sxs-lookup"><span data-stu-id="9cd77-228">Delete users</span></span>
<span data-ttu-id="9cd77-229">El proceso para eliminar un usuario es sencillo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="9cd77-230">Use el método HTTP `DELETE` y construya la dirección URL con el identificador de objeto correcto:</span><span class="sxs-lookup"><span data-stu-id="9cd77-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="9cd77-231">Para ver un ejemplo, ejecute este comando y vea la solicitud Delete que se imprime en la consola:</span><span class="sxs-lookup"><span data-stu-id="9cd77-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="9cd77-232">Consulte el método `B2CGraphClient.SendGraphDeleteRequest(...)` para obtener más información sobre cómo enviar esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="9cd77-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="9cd77-233">Puede realizar muchas otras acciones con la API de Azure AD Graph además de la administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="9cd77-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="9cd77-234">La [referencia de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) proporciona detalles sobre cada acción, junto con solicitudes de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9cd77-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="9cd77-235">Uso de atributos personalizados</span><span class="sxs-lookup"><span data-stu-id="9cd77-235">Use custom attributes</span></span>
<span data-ttu-id="9cd77-236">La mayoría de las aplicaciones de consumidor necesita almacenar algún tipo de información de perfil de usuario personalizada.</span><span class="sxs-lookup"><span data-stu-id="9cd77-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="9cd77-237">Una manera de hacerlo es definiendo un atributo personalizado en el inquilino de B2C.</span><span class="sxs-lookup"><span data-stu-id="9cd77-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="9cd77-238">Puede tratar este atributo de la misma manera que trataría cualquier otra propiedad en un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="9cd77-239">Puede actualizar el atributo, eliminarlo, consultarlo, enviarlo como notificación en tokens de inicio de sesión, etc.</span><span class="sxs-lookup"><span data-stu-id="9cd77-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="9cd77-240">Para definir un atributo personalizado en el inquilino de B2C, consulte la [referencia de atributos personalizados de B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="9cd77-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="9cd77-241">Puede ver los atributos personalizados definidos en el inquilino de B2C mediante `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="9cd77-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="9cd77-242">El resultado de estas funciones muestra los detalles de cada atributo personalizado, como:</span><span class="sxs-lookup"><span data-stu-id="9cd77-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="9cd77-243">Puede usar el nombre completo, por ejemplo `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como propiedad en los objetos de usuario.</span><span class="sxs-lookup"><span data-stu-id="9cd77-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="9cd77-244">Actualice el archivo .json con la nueva propiedad, un valor para la propiedad y ejecute:</span><span class="sxs-lookup"><span data-stu-id="9cd77-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="9cd77-245">Con `B2CGraphClient`, tiene una aplicación de servicio que puede administrar sus usuarios del inquilino de B2C mediante programación.</span><span class="sxs-lookup"><span data-stu-id="9cd77-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="9cd77-246">`B2CGraphClient` usa su propia identidad de aplicación para autenticarse en la API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="9cd77-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="9cd77-247">También adquiere tokens mediante un secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="9cd77-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="9cd77-248">Según vaya incorporando esta funcionalidad a su aplicación, debe recordar algunos puntos clave para las aplicaciones B2C:</span><span class="sxs-lookup"><span data-stu-id="9cd77-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="9cd77-249">Tiene que conceder a la aplicación los permisos adecuados en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="9cd77-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="9cd77-250">Por ahora, debe usar ADAL (no MSAL) para obtener tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="9cd77-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="9cd77-251">(Puede también enviar mensajes de protocolo directamente, sin usar una biblioteca.)</span><span class="sxs-lookup"><span data-stu-id="9cd77-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="9cd77-252">Cuando llame a la API Graph, use `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="9cd77-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="9cd77-253">Al crear y actualizar los usuarios consumidores, hay algunas propiedades obligatorias, tal como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="9cd77-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="9cd77-254">Si tiene alguna pregunta o desea presentar una solicitud para acciones que le gustaría realizar con la API Graph en su inquilino B2C, deje un comentario en este artículo o registre un problema en el repositorio de ejemplos de código de GitHub.</span><span class="sxs-lookup"><span data-stu-id="9cd77-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

