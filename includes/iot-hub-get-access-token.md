## <a name="obtain-an-azure-resource-manager-token"></a>Obtención de un token de Azure Resource Manager
Azure Active Directory debe autenticar todas las tareas de Hola que se realizan en los recursos con hello Azure Resource Manager. Hello ejemplo utiliza la autenticación de contraseña, para otros enfoques, consulte [las solicitudes de autenticación de Azure Resource Manager][lnk-authenticate-arm].

1. Agregar Hola después código toohello **Main** método en Program.cs tooretrieve un token desde Azure AD con el identificador de la aplicación hello y una contraseña.
   
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
2. Crear un **ResourceManagementClient** objeto que usa Hola token agregando Hola siguiente código toohello final de hello **Main** método:
   
    ```
    var creds = new TokenCredentials(token.AccessToken);
    var client = new ResourceManagementClient(creds);
    client.SubscriptionId = subscriptionId;
    ```
3. Crear, o para obtener una referencia al grupo de recursos de Hola que usa:
   
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