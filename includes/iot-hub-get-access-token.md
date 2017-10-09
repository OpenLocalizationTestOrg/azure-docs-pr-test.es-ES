## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="f989e-101">Obtención de un token de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="f989e-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="f989e-102">Azure Active Directory debe autenticar todas las tareas de Hola que se realizan en los recursos con hello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f989e-102">Azure Active Directory must authenticate all hello tasks that you perform on resources using hello Azure Resource Manager.</span></span> <span data-ttu-id="f989e-103">Hello ejemplo utiliza la autenticación de contraseña, para otros enfoques, consulte [las solicitudes de autenticación de Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="f989e-103">hello example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="f989e-104">Agregar Hola después código toohello **Main** método en Program.cs tooretrieve un token desde Azure AD con el identificador de la aplicación hello y una contraseña.</span><span class="sxs-lookup"><span data-stu-id="f989e-104">Add hello following code toohello **Main** method in Program.cs tooretrieve a token from Azure AD using hello application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed tooobtain hello token");
      return;
    }
    ```
2. <span data-ttu-id="f989e-105">Crear un **ResourceManagementClient** objeto que usa Hola token agregando Hola siguiente código toohello final de hello **Main** método:</span><span class="sxs-lookup"><span data-stu-id="f989e-105">Create a **ResourceManagementClient** object that uses hello token by adding hello following code toohello end of hello **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="f989e-106">Crear, o para obtener una referencia al grupo de recursos de Hola que usa:</span><span class="sxs-lookup"><span data-stu-id="f989e-106">Create, or obtain a reference to, hello resource group you are using:</span></span>
   
    ```
    var rgResponse = client.ResourceGroups.CreateOrUpdate(rgName,
        new ResourceGroup("East US"));
    if (rgResponse.Properties.ProvisioningState != "Succeeded")
    {
      Console.WriteLine("Problem creating resource group");
      return;
    }
    ```

[lnk-authenticate-arm]: https://msdn.microsoft.com/library/azure/dn790557.aspx