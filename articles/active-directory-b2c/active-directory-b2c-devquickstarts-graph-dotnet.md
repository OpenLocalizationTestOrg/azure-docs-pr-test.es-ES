---
title: 'Azure B2C Directory Active: Hola de uso API Graph | Documentos de Microsoft'
description: "¿Cómo toocall Hola API Graph para un inquilino B2C mediante un proceso de Hola de tooautomate de identidad de aplicación."
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
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="d8da4-103">B2C de Azure AD: Usar hello API Graph</span><span class="sxs-lookup"><span data-stu-id="d8da4-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="d8da4-104">Inquilinos de Azure Active Directory (Azure AD) B2C suelen toobe muy grande.</span><span class="sxs-lookup"><span data-stu-id="d8da4-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="d8da4-105">Esto significa que muchas tareas comunes de administración de inquilinos necesitan toobe realizar mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="d8da4-106">Un ejemplo importante es la administración de usuarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-106">A primary example is user management.</span></span> <span data-ttu-id="d8da4-107">Tendrá que toomigrate un inquilino de B2C de tooa de almacén de usuario existente.</span><span class="sxs-lookup"><span data-stu-id="d8da4-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="d8da4-108">Puede desea toohost registro de usuario en su propia página y crear cuentas de usuario en el directorio de Azure AD B2C entre bastidores de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="d8da4-109">Estos tipos de tareas requieren Hola capacidad toocreate, lectura, actualización y eliminar cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="d8da4-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="d8da4-110">Puede realizar estas tareas mediante el uso de API de Azure AD Graph Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="d8da4-111">Para los inquilinos B2C, hay dos modos principales de la comunicación con hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="d8da4-112">Para las tareas interactivas, ejecutar una vez, debe actuar como una cuenta de administrador de inquilinos de hello B2C al realizar tareas de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="d8da4-113">Este modo requiere un toosign Administrador con las credenciales antes de que un administrador puede llevar a cabo cualquier toohello llamadas API Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="d8da4-114">Para las tareas automatizadas, continuadas, debe usar algún tipo de cuenta de servicio que proporciona con las tareas de administración de tooperform de hello privilegios necesarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="d8da4-115">En Azure AD, puede hacerlo mediante el registro de una aplicación y autenticar tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="d8da4-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="d8da4-116">Esto se realiza mediante un **Id. de aplicación** que usa hello [concesión las credenciales del cliente de OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="d8da4-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="d8da4-117">En este caso, aplicación hello actúa por sí misma, no como un usuario, toocall Hola API Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="d8da4-118">En este artículo, analizaremos cómo tooperform Hola caso de uso automatizada.</span><span class="sxs-lookup"><span data-stu-id="d8da4-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="d8da4-119">toodemonstrate, vamos a crear un .NET 4.5 `B2CGraphClient` que realiza el usuario crear, leer, actualizar y eliminar operaciones (CRUD).</span><span class="sxs-lookup"><span data-stu-id="d8da4-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="d8da4-120">cliente de Hello tendrá una interfaz de línea de comandos de Windows (CLI) que permite tooinvoke diversos métodos.</span><span class="sxs-lookup"><span data-stu-id="d8da4-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="d8da4-121">Sin embargo, el código de hello se escribe toobehave de forma no interactiva y automatizada.</span><span class="sxs-lookup"><span data-stu-id="d8da4-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="d8da4-122">Obtención de un inquilino de Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="d8da4-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="d8da4-123">Para poder crear aplicaciones o los usuarios o interactuar con Azure AD en absoluto, necesitará un inquilino de Azure AD B2C y una cuenta de administrador global de inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="d8da4-124">Si aún no tiene ningún inquilino, [comience con la introducción a Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d8da4-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="d8da4-125">Registro de la aplicación en el inquilino</span><span class="sxs-lookup"><span data-stu-id="d8da4-125">Register your application in your tenant</span></span>
<span data-ttu-id="d8da4-126">Una vez que un inquilino B2C, necesita tooregister la aplicación a través de hello [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8da4-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8da4-127">toouse Hola API de Graph con su inquilino B2C, deberá tooregister una aplicación dedicada mediante el uso de hello genérico *registros de aplicaciones* hoja en el Portal de Azure, hello **no** Azure AD B2C  *Aplicaciones* hoja.</span><span class="sxs-lookup"><span data-stu-id="d8da4-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="d8da4-128">No se puede reutilizar Hola ya existente B2C aplicaciones que se ha registrado en Azure AD B2C hello *aplicaciones* hoja.</span><span class="sxs-lookup"><span data-stu-id="d8da4-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="d8da4-129">Inicie sesión en toohello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8da4-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8da4-130">Elija al inquilino de Azure AD B2C seleccionando su cuenta en hello superior derecho de la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="d8da4-131">En el panel de navegación izquierdo de hello, elija **más servicios**, haga clic en **registros de aplicaciones**y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="d8da4-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="d8da4-132">Siga las indicaciones de Hola y cree una nueva aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="d8da4-133">Seleccione **aplicación Web / API** como Hola tipo de aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="d8da4-134">Proporcione **cualquier URI de redirección** (p. ej., https://B2CGraphAPI), ya que no es relevante para este ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="d8da4-135">Hello aplicación tendrán ahora aparecen en la lista de Hola de aplicaciones, haga clic en ella hello tooobtain **Id. de aplicación** (también conocido como Id. de cliente).</span><span class="sxs-lookup"><span data-stu-id="d8da4-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="d8da4-136">Cópielo, pues lo necesitará en una sección posterior.</span><span class="sxs-lookup"><span data-stu-id="d8da4-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="d8da4-137">En la hoja de configuración de hello, haga clic en **claves** y agregue una nueva clave (también conocido como secreto de cliente).</span><span class="sxs-lookup"><span data-stu-id="d8da4-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="d8da4-138">Cópiela también para usarla en una sección posterior.</span><span class="sxs-lookup"><span data-stu-id="d8da4-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="d8da4-139">Configuración de permisos de creación, lectura y actualización para la aplicación</span><span class="sxs-lookup"><span data-stu-id="d8da4-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="d8da4-140">Ahora tiene que tooconfigure su tooget aplicación que Hola a todos los necesarios permisos toocreate, leer, actualizar y eliminar usuarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="d8da4-141">Continuar en Hola hoja de registros de aplicación del portal de Azure, seleccione la aplicación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="d8da4-142">En la hoja de configuración de hello, haga clic en **los permisos necesarios**.</span><span class="sxs-lookup"><span data-stu-id="d8da4-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="d8da4-143">En la hoja de hello permisos necesarios, haga clic en **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d8da4-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="d8da4-144">En la hoja de habilitar el acceso de hello, seleccione hello **leer y escribir datos de directorio** permiso de **permisos de aplicación** y haga clic en **guardar**.</span><span class="sxs-lookup"><span data-stu-id="d8da4-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="d8da4-145">Por último, nuevo en la hoja de hello permisos necesarios, haga clic en hello **conceder permisos** botón.</span><span class="sxs-lookup"><span data-stu-id="d8da4-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="d8da4-146">Ahora tiene una aplicación que tenga permiso toocreate, lectura y actualización a los usuarios de su inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="d8da4-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="d8da4-147">Configuración de permisos de eliminación para la aplicación</span><span class="sxs-lookup"><span data-stu-id="d8da4-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="d8da4-148">Actualmente, Hola *leer y escribir datos de directorio* permiso **no** incluyen hello capacidad toodo cualquier eliminación como la eliminación de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="d8da4-149">Si desea toogive los usuarios de aplicación Hola capacidad toodelete, necesitará toodo estos pasos adicionales que implican PowerShell, de lo contrario, puede omitir la sección siguiente toohello.</span><span class="sxs-lookup"><span data-stu-id="d8da4-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="d8da4-150">En primer lugar, descargue e instale hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="d8da4-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="d8da4-151">A continuación, descargue e instale hello [módulo de Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="d8da4-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="d8da4-152">Después de instalar el módulo de PowerShell de hello, abra PowerShell y conéctese a tooyour B2C inquilino.</span><span class="sxs-lookup"><span data-stu-id="d8da4-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="d8da4-153">Después de ejecutar `Get-Credential`, se le pedirá para un nombre de usuario y contraseña, escriba el nombre de usuario de hello y una contraseña de la cuenta de administrador de inquilinos B2C.</span><span class="sxs-lookup"><span data-stu-id="d8da4-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d8da4-154">Necesita la cuenta de administrador de inquilinos de toouse un B2C es **local** toohello B2C inquilino.</span><span class="sxs-lookup"><span data-stu-id="d8da4-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="d8da4-155">Estas cuentas tienen este aspecto: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="d8da4-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="d8da4-156">Ahora vamos a usar hello **Id. de aplicación** en script de Hola tooassign Hola aplicación Hola cuenta Administrador rol de usuario que le permitirá toodelete a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="d8da4-157">Estas funciones tienen identificadores conocidos, por lo que todo lo que necesita toodo se introduce la **Id. de aplicación** en el siguiente script de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="d8da4-158">La aplicación ahora también tiene permisos toodelete los usuarios del inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="d8da4-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="d8da4-159">Descargar, configurar y compilar el código de ejemplo de Hola</span><span class="sxs-lookup"><span data-stu-id="d8da4-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="d8da4-160">En primer lugar, descargue el código de ejemplo de Hola y ejecutarlo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="d8da4-161">A continuación, lo examinaremos más de cerca.</span><span class="sxs-lookup"><span data-stu-id="d8da4-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="d8da4-162">También puede [descargar código de muestra de Hola como un archivo .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="d8da4-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="d8da4-163">También puede clonarlo en un directorio de su elección:</span><span class="sxs-lookup"><span data-stu-id="d8da4-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="d8da4-164">Abra hello `B2CGraphClient\B2CGraphClient.sln` solución de Visual Studio en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8da4-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="d8da4-165">Hola `B2CGraphClient` proyecto, archivo abierto hello `App.config`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="d8da4-166">Reemplazar configuración de aplicación de tres de hello con sus propios valores:</span><span class="sxs-lookup"><span data-stu-id="d8da4-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="d8da4-167">A continuación, haga doble clic en hello `B2CGraphClient` ejemplo de Hola de solución y volver a generar.</span><span class="sxs-lookup"><span data-stu-id="d8da4-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="d8da4-168">Si todo es correcto, ahora debería tener un archivo ejecutable `B2C.exe` que se encuentra en `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="d8da4-169">Generar operaciones CRUD de usuario mediante Hola API Graph</span><span class="sxs-lookup"><span data-stu-id="d8da4-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="d8da4-170">Hola toouse B2CGraphClient, abra un `cmd` Windows comando símbolo del sistema y cambie el directorio toohello `Debug` directory.</span><span class="sxs-lookup"><span data-stu-id="d8da4-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="d8da4-171">A continuación, ejecute hello `B2C Help` comando.</span><span class="sxs-lookup"><span data-stu-id="d8da4-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="d8da4-172">Se mostrará una breve descripción de cada comando.</span><span class="sxs-lookup"><span data-stu-id="d8da4-172">This will display a brief description of each command.</span></span> <span data-ttu-id="d8da4-173">Cada vez que uno de estos comandos, invoque `B2CGraphClient` hace un toohello de solicitud API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="d8da4-174">Obtención de un token de acceso</span><span class="sxs-lookup"><span data-stu-id="d8da4-174">Get an access token</span></span>
<span data-ttu-id="d8da4-175">Cualquier toohello de solicitud API Graph requiere un token de acceso para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="d8da4-176">`B2CGraphClient`toohelp de biblioteca de autenticación de Active Directory (ADAL) de código abierto de hello usa adquirir tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8da4-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="d8da4-177">ADAL facilita la adquisición de tokens al proporcionar una API sencilla y ocuparse de algunos detalles importantes, como el almacenamiento en caché de tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8da4-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="d8da4-178">No es necesario toouse tooget AAL tokens, aunque.</span><span class="sxs-lookup"><span data-stu-id="d8da4-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="d8da4-179">También puede obtener tokens elaborando solicitudes HTTP.</span><span class="sxs-lookup"><span data-stu-id="d8da4-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="d8da4-180">Este ejemplo de código usa AAL v2 en orden toocommunicate con hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="d8da4-181">Debe usar AAL v2 o v3 en tokens de acceso de tooget de orden que se pueden usar con hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="d8da4-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="d8da4-182">Cuando `B2CGraphClient` se ejecuta, crea una instancia de hello `B2CGraphClient` clase.</span><span class="sxs-lookup"><span data-stu-id="d8da4-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="d8da4-183">constructor de Hola para esta clase se configura una técnica de scaffolding de autenticación de ADAL:</span><span class="sxs-lookup"><span data-stu-id="d8da4-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="d8da4-184">Vamos a usar hello `B2C Get-User` comando como un ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="d8da4-185">Cuando `B2C Get-User` se invoca sin ninguna entrada adicional, Hola Hola de llamadas CLI `B2CGraphClient.GetAllUsers(...)` método.</span><span class="sxs-lookup"><span data-stu-id="d8da4-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="d8da4-186">Este método llama a `B2CGraphClient.SendGraphGetRequest(...)`, que envía una solicitud HTTP GET, toohello API Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="d8da4-187">Antes de `B2CGraphClient.SendGraphGetRequest(...)` envía Hola solicitud GET, primero obtiene un token de acceso mediante el uso de ADAL:</span><span class="sxs-lookup"><span data-stu-id="d8da4-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="d8da4-188">Puede obtener un acceso token para hello API Graph por llamada Hola AAL `AuthenticationContext.AcquireToken(...)` método.</span><span class="sxs-lookup"><span data-stu-id="d8da4-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="d8da4-189">AAL, a continuación, devuelve un `access_token` que representa la identidad de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="d8da4-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="d8da4-190">Lectura de usuarios</span><span class="sxs-lookup"><span data-stu-id="d8da4-190">Read users</span></span>
<span data-ttu-id="d8da4-191">Cuando desee tooget una lista de usuarios o hacer que un usuario determinado de hello API Graph, puede enviar un elemento HTTP `GET` solicitar toohello `/users` punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="d8da4-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="d8da4-192">Una solicitud para todos los usuarios de hello en un inquilino tiene el siguiente aspecto:</span><span class="sxs-lookup"><span data-stu-id="d8da4-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d8da4-193">toosee esta solicitud, ejecute:</span><span class="sxs-lookup"><span data-stu-id="d8da4-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="d8da4-194">Hay dos toonote aspectos importantes:</span><span class="sxs-lookup"><span data-stu-id="d8da4-194">There are two important things toonote:</span></span>

* <span data-ttu-id="d8da4-195">Hello token de acceso adquirido a través de AAL se agrega toohello `Authorization` encabezado mediante el uso de hello `Bearer` esquema.</span><span class="sxs-lookup"><span data-stu-id="d8da4-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="d8da4-196">Para los inquilinos B2C, debe usar el parámetro de consulta de hello `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="d8da4-197">Ambos de estos detalles se tratan en hello `B2CGraphClient.SendGraphGetRequest(...)` método:</span><span class="sxs-lookup"><span data-stu-id="d8da4-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="d8da4-198">Creación de cuentas de usuario consumidor</span><span class="sxs-lookup"><span data-stu-id="d8da4-198">Create consumer user accounts</span></span>
<span data-ttu-id="d8da4-199">Al crear cuentas de usuario en el inquilino B2C, puede enviar un elemento HTTP `POST` solicitar toohello `/users` punto de conexión:</span><span class="sxs-lookup"><span data-stu-id="d8da4-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="d8da4-200">La mayoría de estas propiedades en esta solicitud es usuarios de consumidor de toocreate necesarios.</span><span class="sxs-lookup"><span data-stu-id="d8da4-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="d8da4-201">más información, haga clic en la toolearn [aquí](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="d8da4-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="d8da4-202">Tenga en cuenta que hello `//` comentarios se han incluido a modo de ilustración.</span><span class="sxs-lookup"><span data-stu-id="d8da4-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="d8da4-203">No los incluya en una solicitud real.</span><span class="sxs-lookup"><span data-stu-id="d8da4-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="d8da4-204">solicitud de hello toosee, ejecute uno de hello siguientes comandos:</span><span class="sxs-lookup"><span data-stu-id="d8da4-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d8da4-205">Hola `Create-User` comando toma un archivo .json como un parámetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="d8da4-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="d8da4-206">Contiene una representación JSON de un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="d8da4-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="d8da4-207">Hay dos archivos .json de ejemplo en el código de ejemplo de Hola: `usertemplate-email.json` y `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="d8da4-208">Puede modificar estos archivos toosuit sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="d8da4-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="d8da4-209">Además toohello tengan campos anteriores, se incluyen varios campos opcionales que puede usar en estos archivos.</span><span class="sxs-lookup"><span data-stu-id="d8da4-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="d8da4-210">Obtener más información sobre los campos opcionales de hello puede encontrarse en hello [referencia de entidad de API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="d8da4-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="d8da4-211">Puede ver cómo se construye la solicitud POST de hello en `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="d8da4-212">Se adjunta una toohello de token de acceso `Authorization` encabezado de solicitud de saludo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="d8da4-213">Establece `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="d8da4-214">Incluye objetos de usuario JSON de hello en el cuerpo de saludo de solicitud de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="d8da4-215">Si hello las cuentas que desea toomigrate desde un almacén de usuario existente tiene menos seguros de contraseña que hello [intensidad de contraseña segura aplicado Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), puede deshabilitar el requisito de contraseña segura de hello mediante hello `DisableStrongPassword`valor Hola `passwordPolicies` propiedad.</span><span class="sxs-lookup"><span data-stu-id="d8da4-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="d8da4-216">Por ejemplo, puede modificar Hola crear solicitud de usuario proporcionado anteriormente como sigue: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="d8da4-217">Actualización de cuentas de usuario consumidor</span><span class="sxs-lookup"><span data-stu-id="d8da4-217">Update consumer user accounts</span></span>
<span data-ttu-id="d8da4-218">Al actualizar los objetos de usuario, el proceso de hello es toohello similar que utiliza objetos de usuario de toocreate.</span><span class="sxs-lookup"><span data-stu-id="d8da4-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="d8da4-219">Pero este proceso utiliza Hola HTTP `PATCH` método:</span><span class="sxs-lookup"><span data-stu-id="d8da4-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="d8da4-220">Intente tooupdate un usuario mediante la actualización de los archivos JSON con nuevos datos.</span><span class="sxs-lookup"><span data-stu-id="d8da4-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="d8da4-221">A continuación, puede usar `B2CGraphClient` toorun uno de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="d8da4-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="d8da4-222">Inspeccionar hello `B2CGraphClient.SendGraphPatchRequest(...)` método para obtener más información acerca de cómo toosend esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="d8da4-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="d8da4-223">Búsqueda de usuarios</span><span class="sxs-lookup"><span data-stu-id="d8da4-223">Search users</span></span>
<span data-ttu-id="d8da4-224">Puede buscar usuarios en el inquilino de B2C de dos maneras.</span><span class="sxs-lookup"><span data-stu-id="d8da4-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="d8da4-225">Uno, con Id. de objeto del usuario de Hola o dos, utilizando el identificador de inicio de sesión del usuario de hello (es decir, hello `signInNames` propiedad).</span><span class="sxs-lookup"><span data-stu-id="d8da4-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="d8da4-226">Ejecute uno de hello después toosearch de comandos para un usuario específico:</span><span class="sxs-lookup"><span data-stu-id="d8da4-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="d8da4-227">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="d8da4-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="d8da4-228">Eliminación de usuarios</span><span class="sxs-lookup"><span data-stu-id="d8da4-228">Delete users</span></span>
<span data-ttu-id="d8da4-229">proceso de Hola para eliminar un usuario es muy sencillo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="d8da4-230">Hola use HTTP `DELETE` método y construir una URL de hello con hello corregir Id. de objeto:</span><span class="sxs-lookup"><span data-stu-id="d8da4-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="d8da4-231">toosee por ejemplo, escriba este comando y vista de solicitud de eliminación de Hola que es toohello impreso consola:</span><span class="sxs-lookup"><span data-stu-id="d8da4-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="d8da4-232">Inspeccionar hello `B2CGraphClient.SendGraphDeleteRequest(...)` método para obtener más información acerca de cómo toosend esta solicitud.</span><span class="sxs-lookup"><span data-stu-id="d8da4-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="d8da4-233">Puede realizar muchas otras acciones con hello Azure AD Graph API de administración de toouser de adición.</span><span class="sxs-lookup"><span data-stu-id="d8da4-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="d8da4-234">La [referencia de la API de Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) proporciona detalles sobre cada acción, junto con solicitudes de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="d8da4-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="d8da4-235">Uso de atributos personalizados</span><span class="sxs-lookup"><span data-stu-id="d8da4-235">Use custom attributes</span></span>
<span data-ttu-id="d8da4-236">La mayoría de las aplicaciones de consumidor necesitan toostore algún tipo de información de perfil de usuario personalizada.</span><span class="sxs-lookup"><span data-stu-id="d8da4-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="d8da4-237">Una manera de hacer esto es toodefine un atributo personalizado en el inquilino B2C.</span><span class="sxs-lookup"><span data-stu-id="d8da4-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="d8da4-238">A continuación, puede tratar ese Hola de atributo igual tratar cualquier otra propiedad en un objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="d8da4-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="d8da4-239">Puede actualizar el atributo de hello, delete Hola atributo, consulta mediante el atributo de hello, enviar atributo hello como una notificación de tokens de inicio de sesión y mucho más.</span><span class="sxs-lookup"><span data-stu-id="d8da4-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="d8da4-240">toodefine un atributo personalizado en el inquilino B2C, consulte hello [referencia de atributo personalizado de B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="d8da4-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="d8da4-241">Puede ver los atributos personalizados de hello definidos en el inquilino B2C usando `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="d8da4-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="d8da4-242">salida de Hello de estas funciones revela detalles Hola de cada atributo personalizado, como:</span><span class="sxs-lookup"><span data-stu-id="d8da4-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="d8da4-243">Puede usar Hola nombre completo, como `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como una propiedad en los objetos de usuario.</span><span class="sxs-lookup"><span data-stu-id="d8da4-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="d8da4-244">Actualizar el archivo .json con la nueva propiedad de Hola y un valor de propiedad de hello y, a continuación, ejecute:</span><span class="sxs-lookup"><span data-stu-id="d8da4-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="d8da4-245">Con `B2CGraphClient`, tiene una aplicación de servicio que puede administrar sus usuarios del inquilino de B2C mediante programación.</span><span class="sxs-lookup"><span data-stu-id="d8da4-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="d8da4-246">`B2CGraphClient`usa su propio toohello tooauthenticate de identidad de aplicación API de Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="d8da4-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="d8da4-247">También adquiere tokens mediante un secreto de cliente.</span><span class="sxs-lookup"><span data-stu-id="d8da4-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="d8da4-248">Según vaya incorporando esta funcionalidad a su aplicación, debe recordar algunos puntos clave para las aplicaciones B2C:</span><span class="sxs-lookup"><span data-stu-id="d8da4-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="d8da4-249">Necesita toogrant Hola aplicación Hola permisos adecuados en el inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="d8da4-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="d8da4-250">Por ahora, debe toouse AAL (no MSAL) tooget los tokens de acceso.</span><span class="sxs-lookup"><span data-stu-id="d8da4-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="d8da4-251">(Puede también enviar mensajes de protocolo directamente, sin usar una biblioteca.)</span><span class="sxs-lookup"><span data-stu-id="d8da4-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="d8da4-252">Cuando se llama a Hola API Graph, utilice `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="d8da4-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="d8da4-253">Al crear y actualizar los usuarios consumidores, hay algunas propiedades obligatorias, tal como se describió anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d8da4-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="d8da4-254">Si tiene alguna pregunta o las solicitudes para las acciones que desea que tooperform mediante la API Graph hello en el inquilino B2C, deje un comentario en este artículo o un problema de archivos en el repositorio de ejemplo de código de hello GitHub.</span><span class="sxs-lookup"><span data-stu-id="d8da4-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

