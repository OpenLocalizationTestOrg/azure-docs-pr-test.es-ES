## <a name="obtain-an-azure-resource-manager-token"></a><span data-ttu-id="4082f-101">Obtención de un token de Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4082f-101">Obtain an Azure Resource Manager token</span></span>
<span data-ttu-id="4082f-102">Azure Active Directory debe autenticar todas las tareas que se realizan en los recursos mediante el Administrador de recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="4082f-102">Azure Active Directory must authenticate all the tasks that you perform on resources using the Azure Resource Manager.</span></span> <span data-ttu-id="4082f-103">En este ejemplo se usa la autenticación de contraseña; para otros métodos, consulte [Autenticación de solicitudes de Azure Resource Manager][lnk-authenticate-arm].</span><span class="sxs-lookup"><span data-stu-id="4082f-103">The example shown here uses password authentication, for other approaches see [Authenticating Azure Resource Manager requests][lnk-authenticate-arm].</span></span>

1. <span data-ttu-id="4082f-104">Agregue el código siguiente al método **Main** en Program.cs para recuperar un token de Azure AD mediante el identificador y la contraseña de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4082f-104">Add the following code to the **Main** method in Program.cs to retrieve a token from Azure AD using the application id and password.</span></span>
   
    ```
    var authContext = new AuthenticationContext(string.Format  
      ("https://login.microsoftonline.com/{0}", tenantId));
    var credential = new ClientCredential(applicationId, password);
    AuthenticationResult token = authContext.AcquireTokenAsync
      ("https://management.core.windows.net/", credential).Result;
   
    if (token == null)
    {
      Console.WriteLine("Failed to obtain the token");
      return;
    }
    ```
2. <span data-ttu-id="4082f-105">Cree un objeto **ResourceManagementClient** que use el token, agregando el código siguiente al final del método **Main**:</span><span class="sxs-lookup"><span data-stu-id="4082f-105">Create a **ResourceManagementClient** object that uses the token by adding the following code to the end of the **Main** method:</span></span>
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. <span data-ttu-id="4082f-106">Cree u obtenga una referencia al grupo de recursos que está usando:</span><span class="sxs-lookup"><span data-stu-id="4082f-106">Create, or obtain a reference to, the resource group you are using:</span></span>
   
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