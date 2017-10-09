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
# <a name="get-started-with-azure-cdn-development"></a>Introducción al desarrollo de la red de entrega de contenido (CDN) de Azure
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Puede usar hello [biblioteca de red CDN de Azure para .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creación y administración de perfiles de red CDN y puntos de conexión.  Este tutorial le guía por la creación de hello de una aplicación de consola .NET simple que muestra algunas de las operaciones disponibles de Hola.  Este tutorial es todos los aspectos de la biblioteca de Azure CDN Hola toodescribe no está diseñado para .NET en detalle.

Debe toocomplete de Visual Studio 2015 en este tutorial.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) está disponible gratis para descargarse.

> [!TIP]
> Hola [proyecto completado de este tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponible para su descarga en MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Creación del proyecto e incorporación de paquetes NuGet
Ahora que hemos creado un grupo de recursos para los perfiles de la red CDN y dada nuestra perfiles de red CDN de Azure AD aplicación permiso toomanage y los puntos de conexión dentro de ese grupo, podemos comenzar a crear nuestra aplicación.

Desde Visual Studio 2015, haga clic en **archivo**, **New**, **proyecto...**  cuadro de diálogo de proyecto nuevo de tooopen Hola.  Expanda **Visual C#**, a continuación, seleccione **Windows** en panel de Hola Hola izquierda.  Haga clic en **aplicación de consola** en el panel central de Hola.  Asigne un nombre al proyecto y haga clic en **Aceptar**.  

![Nuevo proyecto](./media/cdn-app-dev-net/cdn-new-project.png)

Nuestro proyecto va toouse algunas bibliotecas de Azure contenidos en los paquetes de Nuget.  Vamos a agregar los proyectos de toohello.

1. Haga clic en hello **herramientas** menú, **Administrador de paquetes de Nuget**, a continuación, **Package Manager Console**.
   
    ![Administrar paquetes NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. En la consola de administrador de paquetes de saludo, ejecutar Hola después comando tooinstall hello **biblioteca de autenticación de Active Directory (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Ejecutar Hola después hello tooinstall **biblioteca de administración de red CDN de Azure**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Directivas, constantes, método Main y métodos auxiliares
Seamos estructura básica de Hola de nuestro programa escrito.

1. En la ficha de Program.cs hello, reemplace hello `using` directivas princip Hola con siguiente hello:
   
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
2. Necesitamos toodefine algunas constantes que nuestros métodos va a usar.  Hola `Program` (clase), pero antes de Hola `Main` método, agregue Hola siguiente.  Ser seguro tooreplace marcadores de posición de hello, incluidos hello  **&lt;corchetes angulares&gt;**, con sus propios valores según sea necesario.
   
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
3. En el nivel de clase de hello, definir estas dos variables.  Vamos a usar estas toodetermine más adelante si nuestro perfil y el punto de conexión ya existen.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Reemplace hello `Main` método tal como se indica a continuación:
   
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
5. Algunos de nuestros otros métodos va usuario de hello tooprompt con preguntas de "Sí/No".  Agregar Hola siguiendo el método toomake que un poco más fácil:
   
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

Ahora que se escribe la estructura básica de Hola de nuestro programa, debemos crear métodos de hello llamados por hello `Main` método.

## <a name="authentication"></a>Autenticación
Antes de que podemos usar Hola biblioteca de administración de red CDN de Azure, se necesita que nuestro servicio tooauthenticate principal y obtener un token de autenticación.  Este método usa el token de hello tooretrieve ADAL.

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

Si usa la autenticación de usuario individual, Hola `GetAccessToken` método tendrá un aspecto ligeramente distinto.

> [!IMPORTANT]
> Sólo puede utilizar este ejemplo de código si se elige el toohave autenticación de usuario individuales en lugar de una entidad de servicio.
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

Ser seguro tooreplace `<redirect URI>` con hello redirigir el URI especificado al registrar la aplicación hello en Azure AD.

## <a name="list-cdn-profiles-and-endpoints"></a>Lista de perfiles y puntos de conexión de CDN
Ahora estamos operaciones de red CDN tooperform listo.  Hello primero que hace el método es la lista de todos los perfiles de Hola y puntos de conexión en el grupo de recursos y si encuentra una coincidencia para los nombres de perfil y del extremo de hello especificado en nuestras constantes, hace una nota de para más tarde por lo que no intentaremos toocreate duplicados.

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

## <a name="create-cdn-profiles-and-endpoints"></a>Creación de perfiles y puntos de conexión de CDN
A continuación, vamos a crear un perfil.

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

Una vez creado el perfil de hello, vamos a crear un punto de conexión.

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
> ejemplo de Hola anterior asigna el punto de conexión de hello un origen con el nombre *Contoso* con un nombre de host `www.contoso.com`.  Debe cambiar el nombre de host de esta toopoint tooyour propio del origen.
> 
> 

## <a name="purge-an-endpoint"></a>Purga de un punto de conexión
Suponiendo que ha creado el extremo de hello, una tarea habitual que tengamos que queremos tooperform en nuestro programa purga de contenido de hello en el punto de conexión.

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
> En el ejemplo de Hola anterior, Hola cadena `/*` denota que deseo toopurge todo el contenido de la raíz de Hola de ruta de acceso de punto de conexión de Hola.  Esto es equivalente toochecking **purgar todos los** Hola portal de Azure "purga" cuadro de diálogo. Hola `CreateCdnProfile` método, creé nuestro perfil como un **CDN de Azure de Verizon** perfil mediante código de hello `Sku = new Sku(SkuName.StandardVerizon)`, por lo que esto se realice correctamente.  Sin embargo, **Azure CDN de Akamai** perfiles no son compatibles con **purgar todos los**, por lo que si estaba usando un perfil de Akamai para este tutorial, necesitaría tooinclude toopurge de rutas de acceso específicas.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Eliminación de perfiles y puntos de conexión de CDN
métodos último Hola eliminará nuestro punto de conexión y el perfil.

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

## <a name="running-hello-program"></a>Programa hello en ejecución
Ahora podemos compilar y ejecutar el programa Hola haciendo clic en hello **iniciar** botón en Visual Studio.

![Programa en ejecución](./media/cdn-app-dev-net/cdn-program-running-1.png)

Cuando programa Hola alcanza Hola por encima del símbolo del sistema, debe ser capaz de tooreturn grupo de recursos tooyour Hola portal de Azure y comprobar que se ha creado el perfil de Hola.

![¡Éxito!](./media/cdn-app-dev-net/cdn-success.png)

A continuación, se puede confirmar Hola indicaciones toorun Hola resto del programa Hola.

![Finalización del programa](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Pasos siguientes
proyecto de toosee Hola completado de este tutorial, [Descargar ejemplo hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

documentación adicional toofind en hello biblioteca de administración de red CDN de Azure para. NET, Hola vista [referencia en MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Administre sus recursos de red CDN con [PowerShell](cdn-manage-powershell.md).

