
1. <span data-ttu-id="480e3-101">En el archivo de proyecto de hello MainPage.xaml.cs, agregue el siguiente de hello **con** instrucciones:</span><span class="sxs-lookup"><span data-stu-id="480e3-101">In hello MainPage.xaml.cs project file, add hello following **using** statements:</span></span>
   
        using System.Linq;        
        using Windows.Security.Credentials;
2. <span data-ttu-id="480e3-102">Reemplace hello **AuthenticateAsync** método con el siguiente código de hello:</span><span class="sxs-lookup"><span data-stu-id="480e3-102">Replace hello **AuthenticateAsync** method with hello following code:</span></span>
   
        private async System.Threading.Tasks.Task<bool> AuthenticateAsync()
        {
            string message;
            bool success = false;
   
            // This sample uses hello Facebook provider.
            var provider = MobileServiceAuthenticationProvider.Facebook;
   
            // Use hello PasswordVault toosecurely store and access credentials.
            PasswordVault vault = new PasswordVault();
            PasswordCredential credential = null;
   
            try
            {
                // Try tooget an existing credential from hello vault.
                credential = vault.FindAllByResource(provider.ToString()).FirstOrDefault();
            }
            catch (Exception)
            {
                // When there is no matching resource an error occurs, which we ignore.
            }
   
            if (credential != null)
            {
                // Create a user from hello stored credentials.
                user = new MobileServiceUser(credential.UserName);
                credential.RetrievePassword();
                user.MobileServiceAuthenticationToken = credential.Password;
   
                // Set hello user from hello stored credentials.
                App.MobileService.CurrentUser = user;
   
                // Consider adding a check toodetermine if hello token is 
                // expired, as shown in this post: http://aka.ms/jww5vp.
   
                success = true;
                message = string.Format("Cached credentials for user - {0}", user.UserId);
            }
            else
            {
                try
                {
                    // Login with hello identity provider.
                    user = await App.MobileService
                        .LoginAsync(provider);
   
                    // Create and store hello user credentials.
                    credential = new PasswordCredential(provider.ToString(),
                        user.UserId, user.MobileServiceAuthenticationToken);
                    vault.Add(credential);
   
                    success = true;
                    message = string.Format("You are now logged in - {0}", user.UserId);
                }
                catch (MobileServiceInvalidOperationException)
                {
                    message = "You must log in. Login Required";
                }
            }
   
            var dialog = new MessageDialog(message);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
   
            return success;
        }
   
    <span data-ttu-id="480e3-103">En esta versión de **AuthenticateAsync**, aplicación hello trata las credenciales de toouse almacenadas en hello **PasswordVault** tooaccess Hola servicio.</span><span class="sxs-lookup"><span data-stu-id="480e3-103">In this version of **AuthenticateAsync**, hello app tries toouse credentials stored in hello **PasswordVault** tooaccess hello service.</span></span> <span data-ttu-id="480e3-104">También se realiza un inicio de sesión normal cuando no hay ninguna credencial almacenada.</span><span class="sxs-lookup"><span data-stu-id="480e3-104">A regular sign-in is also performed when there is no stored credential.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="480e3-105">Puede haber expirado un token de caché y vencimiento del token también puede producirse después de la autenticación cuando se utiliza la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="480e3-105">A cached token may be expired, and token expiration can also occur after authentication when hello app is in use.</span></span> <span data-ttu-id="480e3-106">toolearn toodetermine si expira un token, vea [comprobar tokens de autenticación expirado](http://aka.ms/jww5vp).</span><span class="sxs-lookup"><span data-stu-id="480e3-106">toolearn how toodetermine if a token is expired, see [Check for expired authentication tokens](http://aka.ms/jww5vp).</span></span> <span data-ttu-id="480e3-107">Para los errores de autorización de toohandling de una solución tokens de tooexpiring relacionados, vea Hola registrar [almacenamiento en caché y control de tokens caducados en servicios móviles de Azure administran SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span><span class="sxs-lookup"><span data-stu-id="480e3-107">For a solution toohandling authorization errors related tooexpiring tokens, see hello post [Caching and handling expired tokens in Azure Mobile Services managed SDK](http://blogs.msdn.com/b/carlosfigueira/archive/2014/03/13/caching-and-handling-expired-tokens-in-azure-mobile-services-managed-sdk.aspx).</span></span> 
   > 
   > 
3. <span data-ttu-id="480e3-108">Reinicie la aplicación hello dos veces.</span><span class="sxs-lookup"><span data-stu-id="480e3-108">Restart hello app twice.</span></span>
   
    <span data-ttu-id="480e3-109">Tenga en cuenta que en el primer inicio de hello, inicie sesión con el proveedor de hello nuevo es necesario.</span><span class="sxs-lookup"><span data-stu-id="480e3-109">Notice that on hello first start-up, sign-in with hello provider is again required.</span></span> <span data-ttu-id="480e3-110">Sin embargo, en el segundo reinicio de Hola se usan las credenciales de hello en caché y se omite en el inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="480e3-110">However, on hello second restart hello cached credentials are used and sign-in is bypassed.</span></span> 

