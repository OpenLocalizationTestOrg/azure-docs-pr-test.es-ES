---
title: "aaaGet partió Hola biblioteca de red CDN de Azure para .NET | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toowrite .NET aplicaciones toomanage CDN de Azure con Visual Studio."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="436dc-103">Introducción al desarrollo de la red de entrega de contenido (CDN) de Azure</span><span class="sxs-lookup"><span data-stu-id="436dc-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="436dc-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="436dc-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="436dc-105">.NET</span><span class="sxs-lookup"><span data-stu-id="436dc-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="436dc-106">Puede usar hello [biblioteca de red CDN de Azure para .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creación y administración de perfiles de red CDN y puntos de conexión.</span><span class="sxs-lookup"><span data-stu-id="436dc-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="436dc-107">Este tutorial le guía por la creación de hello de una aplicación de consola .NET simple que muestra algunas de las operaciones disponibles de Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="436dc-108">Este tutorial es todos los aspectos de la biblioteca de Azure CDN Hola toodescribe no está diseñado para .NET en detalle.</span><span class="sxs-lookup"><span data-stu-id="436dc-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="436dc-109">Debe toocomplete de Visual Studio 2015 en este tutorial.</span><span class="sxs-lookup"><span data-stu-id="436dc-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="436dc-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) está disponible gratis para descargarse.</span><span class="sxs-lookup"><span data-stu-id="436dc-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="436dc-111">Hola [proyecto completado de este tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponible para su descarga en MSDN.</span><span class="sxs-lookup"><span data-stu-id="436dc-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="436dc-112">Creación del proyecto e incorporación de paquetes NuGet</span><span class="sxs-lookup"><span data-stu-id="436dc-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="436dc-113">Ahora que hemos creado un grupo de recursos para los perfiles de la red CDN y dada nuestra perfiles de red CDN de Azure AD aplicación permiso toomanage y los puntos de conexión dentro de ese grupo, podemos comenzar a crear nuestra aplicación.</span><span class="sxs-lookup"><span data-stu-id="436dc-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="436dc-114">Desde Visual Studio 2015, haga clic en **archivo**, **New**, **proyecto...**  cuadro de diálogo de proyecto nuevo de tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="436dc-115">Expanda **Visual C#**, a continuación, seleccione **Windows** en panel de Hola Hola izquierda.</span><span class="sxs-lookup"><span data-stu-id="436dc-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="436dc-116">Haga clic en **aplicación de consola** en el panel central de Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="436dc-117">Asigne un nombre al proyecto y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="436dc-117">Name your project, then click **OK**.</span></span>  

![Nuevo proyecto](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="436dc-119">Nuestro proyecto va toouse algunas bibliotecas de Azure contenidos en los paquetes de Nuget.</span><span class="sxs-lookup"><span data-stu-id="436dc-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="436dc-120">Vamos a agregar los proyectos de toohello.</span><span class="sxs-lookup"><span data-stu-id="436dc-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="436dc-121">Haga clic en hello **herramientas** menú, **Administrador de paquetes de Nuget**, a continuación, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="436dc-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Administrar paquetes NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="436dc-123">En la consola de administrador de paquetes de saludo, ejecutar Hola después comando tooinstall hello **biblioteca de autenticación de Active Directory (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="436dc-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="436dc-124">Ejecutar Hola después hello tooinstall **biblioteca de administración de red CDN de Azure**:</span><span class="sxs-lookup"><span data-stu-id="436dc-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="436dc-125">Directivas, constantes, método Main y métodos auxiliares</span><span class="sxs-lookup"><span data-stu-id="436dc-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="436dc-126">Seamos estructura básica de Hola de nuestro programa escrito.</span><span class="sxs-lookup"><span data-stu-id="436dc-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="436dc-127">En la ficha de Program.cs hello, reemplace hello `using` directivas princip Hola con siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="436dc-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. <span data-ttu-id="436dc-128">Necesitamos toodefine algunas constantes que nuestros métodos va a usar.</span><span class="sxs-lookup"><span data-stu-id="436dc-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="436dc-129">Hola `Program` (clase), pero antes de Hola `Main` método, agregue Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="436dc-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="436dc-130">Ser seguro tooreplace marcadores de posición de hello, incluidos hello  **&lt;corchetes angulares&gt;**, con sus propios valores según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="436dc-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="436dc-131">En el nivel de clase de hello, definir estas dos variables.</span><span class="sxs-lookup"><span data-stu-id="436dc-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="436dc-132">Vamos a usar estas toodetermine más adelante si nuestro perfil y el punto de conexión ya existen.</span><span class="sxs-lookup"><span data-stu-id="436dc-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="436dc-133">Reemplace hello `Main` método tal como se indica a continuación:</span><span class="sxs-lookup"><span data-stu-id="436dc-133">Replace hello `Main` method as follows:</span></span>
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="436dc-134">Algunos de nuestros otros métodos va usuario de hello tooprompt con preguntas de "Sí/No".</span><span class="sxs-lookup"><span data-stu-id="436dc-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="436dc-135">Agregar Hola siguiendo el método toomake que un poco más fácil:</span><span class="sxs-lookup"><span data-stu-id="436dc-135">Add hello following method toomake that a little easier:</span></span>
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

<span data-ttu-id="436dc-136">Ahora que se escribe la estructura básica de Hola de nuestro programa, debemos crear métodos de hello llamados por hello `Main` método.</span><span class="sxs-lookup"><span data-stu-id="436dc-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="436dc-137">Autenticación</span><span class="sxs-lookup"><span data-stu-id="436dc-137">Authentication</span></span>
<span data-ttu-id="436dc-138">Antes de que podemos usar Hola biblioteca de administración de red CDN de Azure, se necesita que nuestro servicio tooauthenticate principal y obtener un token de autenticación.</span><span class="sxs-lookup"><span data-stu-id="436dc-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="436dc-139">Este método usa el token de hello tooretrieve ADAL.</span><span class="sxs-lookup"><span data-stu-id="436dc-139">This method uses ADAL tooretrieve hello token.</span></span>

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

<span data-ttu-id="436dc-140">Si usa la autenticación de usuario individual, Hola `GetAccessToken` método tendrá un aspecto ligeramente distinto.</span><span class="sxs-lookup"><span data-stu-id="436dc-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="436dc-141">Sólo puede utilizar este ejemplo de código si se elige el toohave autenticación de usuario individuales en lugar de una entidad de servicio.</span><span class="sxs-lookup"><span data-stu-id="436dc-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

<span data-ttu-id="436dc-142">Ser seguro tooreplace `<redirect URI>` con hello redirigir el URI especificado al registrar la aplicación hello en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="436dc-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="436dc-143">Lista de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="436dc-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="436dc-144">Ahora estamos operaciones de red CDN tooperform listo.</span><span class="sxs-lookup"><span data-stu-id="436dc-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="436dc-145">Hello primero que hace el método es la lista de todos los perfiles de Hola y puntos de conexión en el grupo de recursos y si encuentra una coincidencia para los nombres de perfil y del extremo de hello especificado en nuestras constantes, hace una nota de para más tarde por lo que no intentaremos toocreate duplicados.</span><span class="sxs-lookup"><span data-stu-id="436dc-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="436dc-146">Creación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="436dc-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="436dc-147">A continuación, vamos a crear un perfil.</span><span class="sxs-lookup"><span data-stu-id="436dc-147">Next, we'll create a profile.</span></span>

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

<span data-ttu-id="436dc-148">Una vez creado el perfil de hello, vamos a crear un punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="436dc-148">Once hello profile is created, we'll create an endpoint.</span></span>

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> <span data-ttu-id="436dc-149">ejemplo de Hola anterior asigna el punto de conexión de hello un origen con el nombre *Contoso* con un nombre de host `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="436dc-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="436dc-150">Debe cambiar el nombre de host de esta toopoint tooyour propio del origen.</span><span class="sxs-lookup"><span data-stu-id="436dc-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="436dc-151">Purga de un punto de conexión</span><span class="sxs-lookup"><span data-stu-id="436dc-151">Purge an endpoint</span></span>
<span data-ttu-id="436dc-152">Suponiendo que ha creado el extremo de hello, una tarea habitual que tengamos que queremos tooperform en nuestro programa purga de contenido de hello en el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="436dc-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> <span data-ttu-id="436dc-153">En el ejemplo de Hola anterior, Hola cadena `/*` denota que deseo toopurge todo el contenido de la raíz de Hola de ruta de acceso de punto de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="436dc-154">Esto es equivalente toochecking **purgar todos los** Hola portal de Azure "purga" cuadro de diálogo.</span><span class="sxs-lookup"><span data-stu-id="436dc-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="436dc-155">Hola `CreateCdnProfile` método, creé nuestro perfil como un **CDN de Azure de Verizon** perfil mediante código de hello `Sku = new Sku(SkuName.StandardVerizon)`, por lo que esto se realice correctamente.</span><span class="sxs-lookup"><span data-stu-id="436dc-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="436dc-156">Sin embargo, **Azure CDN de Akamai** perfiles no son compatibles con **purgar todos los**, por lo que si estaba usando un perfil de Akamai para este tutorial, necesitaría tooinclude toopurge de rutas de acceso específicas.</span><span class="sxs-lookup"><span data-stu-id="436dc-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="436dc-157">Eliminación de perfiles y puntos de conexión de CDN</span><span class="sxs-lookup"><span data-stu-id="436dc-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="436dc-158">métodos último Hola eliminará nuestro punto de conexión y el perfil.</span><span class="sxs-lookup"><span data-stu-id="436dc-158">hello last methods will delete our endpoint and profile.</span></span>

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a><span data-ttu-id="436dc-159">Programa hello en ejecución</span><span class="sxs-lookup"><span data-stu-id="436dc-159">Running hello program</span></span>
<span data-ttu-id="436dc-160">Ahora podemos compilar y ejecutar el programa Hola haciendo clic en hello **iniciar** botón en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="436dc-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Programa en ejecución](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="436dc-162">Cuando programa Hola alcanza Hola por encima del símbolo del sistema, debe ser capaz de tooreturn grupo de recursos tooyour Hola portal de Azure y comprobar que se ha creado el perfil de Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![¡Éxito!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="436dc-164">A continuación, se puede confirmar Hola indicaciones toorun Hola resto del programa Hola.</span><span class="sxs-lookup"><span data-stu-id="436dc-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Finalización del programa](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="436dc-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="436dc-166">Next Steps</span></span>
<span data-ttu-id="436dc-167">proyecto de toosee Hola completado de este tutorial, [Descargar ejemplo hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="436dc-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="436dc-168">documentación adicional toofind en hello biblioteca de administración de red CDN de Azure para. NET, Hola vista [referencia en MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="436dc-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="436dc-169">Administre sus recursos de red CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="436dc-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

