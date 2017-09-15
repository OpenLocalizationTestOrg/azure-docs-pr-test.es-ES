
<span data-ttu-id="16221-101">En el ejemplo anterior se mostró un inicio de sesión estándar, que requiere que el cliente se ponga en contacto con el proveedor de identidades y con el servicio de Azure de back-end cada vez que se inicia la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16221-101">The previous example showed a standard sign-in, which requires the client to contact both the identity provider and the back-end Azure service every time the app starts.</span></span> <span data-ttu-id="16221-102">Este método no es eficaz y puede tener problemas relacionados con el uso si muchos clientes intentan iniciar la aplicación al mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="16221-102">This method is inefficient, and you can have usage-related issues if many customers try to start your app simultaneously.</span></span> <span data-ttu-id="16221-103">Un método mejor es almacenar en caché el token de autorización devuelto por el servicio de Azure e intentar usarlo primero antes de emplear un inicio de sesión basado en proveedores.</span><span class="sxs-lookup"><span data-stu-id="16221-103">A better approach is to cache the authorization token returned by the Azure service, and try to use this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="16221-104">Puede almacenar en caché el token emitido por el servicio de Azure de back-end con independencia de si es una autenticación administrada por el cliente o por el servicio.</span><span class="sxs-lookup"><span data-stu-id="16221-104">You can cache the token issued by the back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="16221-105">Este tutorial utiliza la autenticación administrada por el servicio.</span><span class="sxs-lookup"><span data-stu-id="16221-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="16221-106">Abra el archivo ToDoActivity.java y agregue las siguientes instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="16221-106">Open the ToDoActivity.java file and add the following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="16221-107">Agregue los siguientes métodos a la clase `ToDoActivity` .</span><span class="sxs-lookup"><span data-stu-id="16221-107">Add the following members to the `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="16221-108">En el archivo ToDoActivity.java, agregue la siguiente definición para el método `cacheUserToken`.</span><span class="sxs-lookup"><span data-stu-id="16221-108">In the ToDoActivity.java file, add the following definition for the `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="16221-109">Este método almacena el identificador de usuario y el token en un archivo de preferencias que está marcado como privado.</span><span class="sxs-lookup"><span data-stu-id="16221-109">This method stores the user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="16221-110">Esto debería proteger el acceso a la memoria caché para que otras aplicaciones del dispositivo no tengan acceso al token.</span><span class="sxs-lookup"><span data-stu-id="16221-110">This should protect access to the cache so that other apps on the device do not have access to the token.</span></span> <span data-ttu-id="16221-111">La preferencia es un espacio aislado de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="16221-111">The preference is sandboxed for the app.</span></span> <span data-ttu-id="16221-112">Sin embargo, si alguien obtiene acceso al dispositivo, es posible que pueda tener acceso a la caché del token mediante otros medios.</span><span class="sxs-lookup"><span data-stu-id="16221-112">However, if someone gains access to the device, it is possible that they may gain access to the token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="16221-113">Puede proteger adicionalmente el token con cifrado si el acceso del token a los datos se considera sumamente sensible y alguien puede obtener acceso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="16221-113">You can further protect the token with encryption, if token access to your data is considered highly sensitive and someone may gain access to the device.</span></span> <span data-ttu-id="16221-114">Sin embargo, una solución completamente segura está fuera del alcance de este tutorial y depende de los requisitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="16221-114">A completely secure solution is beyond the scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="16221-115">En el archivo ToDoActivity.java, agregue la siguiente definición para el método `loadUserTokenCache`.</span><span class="sxs-lookup"><span data-stu-id="16221-115">In the ToDoActivity.java file, add the following definition for the `loadUserTokenCache` method.</span></span>

        private boolean loadUserTokenCache(MobileServiceClient client)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            String userId = prefs.getString(USERIDPREF, null);
            if (userId == null)
                return false;
            String token = prefs.getString(TOKENPREF, null);
            if (token == null)
                return false;

            MobileServiceUser user = new MobileServiceUser(userId);
            user.setAuthenticationToken(token);
            client.setCurrentUser(user);

            return true;
        }
5. <span data-ttu-id="16221-116">En el archivo *ToDoActivity.java*, reemplace el método `authenticate` por el método siguiente que usa una caché del token.</span><span class="sxs-lookup"><span data-stu-id="16221-116">In the *ToDoActivity.java* file, replace the `authenticate` method with the following method, which uses a token cache.</span></span> <span data-ttu-id="16221-117">Cambie el proveedor de inicio de sesión si desea usar otra cuenta que no sea la de Google.</span><span class="sxs-lookup"><span data-stu-id="16221-117">Change the login provider if you want to use an account other than Google.</span></span>

        private void authenticate() {
            // We first try to load a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed to load a token cache, login and create a token cache
            else
            {
                // Login using the Google provider.    
                ListenableFuture<MobileServiceUser> mLogin = mClient.login(MobileServiceAuthenticationProvider.Google);

                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        createAndShowDialog("You must log in. Login Required", "Error");
                    }           
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        createAndShowDialog(String.format(
                                "You are now logged in - %1$2s",
                                user.getUserId()), "Success");
                        cacheUserToken(mClient.getCurrentUser());
                        createTable();    
                    }
                });
            }
        }
6. <span data-ttu-id="16221-118">Cree la aplicación y pruebe la autenticación mediante una cuenta válida.</span><span class="sxs-lookup"><span data-stu-id="16221-118">Build the app and test authentication using a valid account.</span></span> <span data-ttu-id="16221-119">Ejecútela al menos dos veces.</span><span class="sxs-lookup"><span data-stu-id="16221-119">Run it at least twice.</span></span> <span data-ttu-id="16221-120">Durante la primera ejecución, debe recibir un mensaje para iniciar sesión y crear la memoria caché del token.</span><span class="sxs-lookup"><span data-stu-id="16221-120">During the first run, you should receive a prompt to sign in and create the token cache.</span></span> <span data-ttu-id="16221-121">Después de eso, cada ejecución intenta cargar la caché de tokens para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="16221-121">After that, each run attempts to load the token cache for authentication.</span></span> <span data-ttu-id="16221-122">No es necesario para iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="16221-122">You should not be required to sign in.</span></span>
