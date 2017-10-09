
<span data-ttu-id="7e495-101">Hola ejemplo anterior, mostramos un estándar inicio de sesión de, lo que requiere Hola cliente toocontact ambos Hola identidad hello y proveedor de servicio back-end Azure cada vez que inicia la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7e495-101">hello previous example showed a standard sign-in, which requires hello client toocontact both hello identity provider and hello back-end Azure service every time hello app starts.</span></span> <span data-ttu-id="7e495-102">Este método es ineficiente y puede tener problemas relacionados con el uso si muchos clientes intentan la aplicación con toostart de forma simultánea.</span><span class="sxs-lookup"><span data-stu-id="7e495-102">This method is inefficient, and you can have usage-related issues if many customers try toostart your app simultaneously.</span></span> <span data-ttu-id="7e495-103">Un enfoque más adecuado es toocache Hola autorización token devuelto por hello servicio de Azure y try toouse esto antes de utilizar un inicio de sesión de basada en el proveedor.</span><span class="sxs-lookup"><span data-stu-id="7e495-103">A better approach is toocache hello authorization token returned by hello Azure service, and try toouse this first before using a provider-based sign-in.</span></span>

> [!NOTE]
> <span data-ttu-id="7e495-104">Puede almacenar en caché el token de hello emitido Hola back-end servicio de Azure, independientemente de si está usando autenticación administrada por el cliente o servicio.</span><span class="sxs-lookup"><span data-stu-id="7e495-104">You can cache hello token issued by hello back-end Azure service regardless of whether you are using client-managed or service-managed authentication.</span></span> <span data-ttu-id="7e495-105">Este tutorial utiliza la autenticación administrada por el servicio.</span><span class="sxs-lookup"><span data-stu-id="7e495-105">This tutorial uses service-managed authentication.</span></span>
>
>

1. <span data-ttu-id="7e495-106">Abra el archivo de ToDoActivity.java hello y agregue Hola siguiendo las instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="7e495-106">Open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. <span data-ttu-id="7e495-107">Agregar Hola después miembros toohello `ToDoActivity` clase.</span><span class="sxs-lookup"><span data-stu-id="7e495-107">Add hello following members toohello `ToDoActivity` class.</span></span>

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. <span data-ttu-id="7e495-108">En archivo de ToDoActivity.java de hello, agregue Hola después de la definición de hello `cacheUserToken` método.</span><span class="sxs-lookup"><span data-stu-id="7e495-108">In hello ToDoActivity.java file, add hello following definition for hello `cacheUserToken` method.</span></span>

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    <span data-ttu-id="7e495-109">Este método almacena el Id. de usuario de Hola y símbolo (token) en un archivo de preferencias que se marca como privado.</span><span class="sxs-lookup"><span data-stu-id="7e495-109">This method stores hello user ID and token in a preference file that is marked private.</span></span> <span data-ttu-id="7e495-110">Esto debe proteger acceso toohello caché para que otras aplicaciones en dispositivos de hello no tiene el token de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="7e495-110">This should protect access toohello cache so that other apps on hello device do not have access toohello token.</span></span> <span data-ttu-id="7e495-111">preferencia de Hello es en recintos de seguridad para la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="7e495-111">hello preference is sandboxed for hello app.</span></span> <span data-ttu-id="7e495-112">Sin embargo, si alguien logra dispositivo toohello de acceso, es posible que puede obtener caché de tokens de acceso toohello a través de otros medios.</span><span class="sxs-lookup"><span data-stu-id="7e495-112">However, if someone gains access toohello device, it is possible that they may gain access toohello token cache through other means.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7e495-113">Puede proteger aún más el token de hello con cifrado, si se consideran confidenciales datos tooyour de token de acceso y un usuario puede obtener dispositivo toohello de acceso.</span><span class="sxs-lookup"><span data-stu-id="7e495-113">You can further protect hello token with encryption, if token access tooyour data is considered highly sensitive and someone may gain access toohello device.</span></span> <span data-ttu-id="7e495-114">Sin embargo, una solución completamente segura está más allá del ámbito de Hola de este tutorial y depende de los requisitos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="7e495-114">A completely secure solution is beyond hello scope of this tutorial, however, and depends on your security requirements.</span></span>
   >
   >
4. <span data-ttu-id="7e495-115">En archivo de ToDoActivity.java de hello, agregue Hola después de la definición de hello `loadUserTokenCache` método.</span><span class="sxs-lookup"><span data-stu-id="7e495-115">In hello ToDoActivity.java file, add hello following definition for hello `loadUserTokenCache` method.</span></span>

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
5. <span data-ttu-id="7e495-116">Hola *ToDoActivity.java* archivo, reemplace hello `authenticate` método con hello siguiendo el método, que utiliza una caché de tokens.</span><span class="sxs-lookup"><span data-stu-id="7e495-116">In hello *ToDoActivity.java* file, replace hello `authenticate` method with hello following method, which uses a token cache.</span></span> <span data-ttu-id="7e495-117">Cambiar el proveedor de inicio de sesión de hello si desea toouse una cuenta distinta de Google.</span><span class="sxs-lookup"><span data-stu-id="7e495-117">Change hello login provider if you want toouse an account other than Google.</span></span>

        private void authenticate() {
            // We first try tooload a token cache if one exists.
            if (loadUserTokenCache(mClient))
            {
                createTable();
            }
            // If we failed tooload a token cache, login and create a token cache
            else
            {
                // Login using hello Google provider.    
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
6. <span data-ttu-id="7e495-118">Compile la autenticación de aplicación y prueba de hello con una cuenta válida.</span><span class="sxs-lookup"><span data-stu-id="7e495-118">Build hello app and test authentication using a valid account.</span></span> <span data-ttu-id="7e495-119">Ejecútela al menos dos veces.</span><span class="sxs-lookup"><span data-stu-id="7e495-119">Run it at least twice.</span></span> <span data-ttu-id="7e495-120">Durante el saludo ejecuta por primera vez, debe recibir un símbolo del sistema toosign en y crear caché de tokens de Hola.</span><span class="sxs-lookup"><span data-stu-id="7e495-120">During hello first run, you should receive a prompt toosign in and create hello token cache.</span></span> <span data-ttu-id="7e495-121">Después de eso, cada serie de intentos de caché de tokens de hello tooload para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="7e495-121">After that, each run attempts tooload hello token cache for authentication.</span></span> <span data-ttu-id="7e495-122">No debe ser necesario toosign en.</span><span class="sxs-lookup"><span data-stu-id="7e495-122">You should not be required toosign in.</span></span>
