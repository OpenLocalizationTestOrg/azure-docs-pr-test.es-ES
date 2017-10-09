
Hola ejemplo anterior, mostramos un estándar inicio de sesión de, lo que requiere Hola cliente toocontact ambos Hola identidad hello y proveedor de servicio back-end Azure cada vez que inicia la aplicación hello. Este método es ineficiente y puede tener problemas relacionados con el uso si muchos clientes intentan la aplicación con toostart de forma simultánea. Un enfoque más adecuado es toocache Hola autorización token devuelto por hello servicio de Azure y try toouse esto antes de utilizar un inicio de sesión de basada en el proveedor.

> [!NOTE]
> Puede almacenar en caché el token de hello emitido Hola back-end servicio de Azure, independientemente de si está usando autenticación administrada por el cliente o servicio. Este tutorial utiliza la autenticación administrada por el servicio.
>
>

1. Abra el archivo de ToDoActivity.java hello y agregue Hola siguiendo las instrucciones de importación:

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;
2. Agregar Hola después miembros toohello `ToDoActivity` clase.

        public static final String SHAREDPREFFILE = "temp";    
        public static final String USERIDPREF = "uid";    
        public static final String TOKENPREF = "tkn";    
3. En archivo de ToDoActivity.java de hello, agregue Hola después de la definición de hello `cacheUserToken` método.

        private void cacheUserToken(MobileServiceUser user)
        {
            SharedPreferences prefs = getSharedPreferences(SHAREDPREFFILE, Context.MODE_PRIVATE);
            Editor editor = prefs.edit();
            editor.putString(USERIDPREF, user.getUserId());
            editor.putString(TOKENPREF, user.getAuthenticationToken());
            editor.commit();
        }    

    Este método almacena el Id. de usuario de Hola y símbolo (token) en un archivo de preferencias que se marca como privado. Esto debe proteger acceso toohello caché para que otras aplicaciones en dispositivos de hello no tiene el token de acceso toohello. preferencia de Hello es en recintos de seguridad para la aplicación hello. Sin embargo, si alguien logra dispositivo toohello de acceso, es posible que puede obtener caché de tokens de acceso toohello a través de otros medios.

   > [!NOTE]
   > Puede proteger aún más el token de hello con cifrado, si se consideran confidenciales datos tooyour de token de acceso y un usuario puede obtener dispositivo toohello de acceso. Sin embargo, una solución completamente segura está más allá del ámbito de Hola de este tutorial y depende de los requisitos de seguridad.
   >
   >
4. En archivo de ToDoActivity.java de hello, agregue Hola después de la definición de hello `loadUserTokenCache` método.

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
5. Hola *ToDoActivity.java* archivo, reemplace hello `authenticate` método con hello siguiendo el método, que utiliza una caché de tokens. Cambiar el proveedor de inicio de sesión de hello si desea toouse una cuenta distinta de Google.

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
6. Compile la autenticación de aplicación y prueba de hello con una cuenta válida. Ejecútela al menos dos veces. Durante el saludo ejecuta por primera vez, debe recibir un símbolo del sistema toosign en y crear caché de tokens de Hola. Después de eso, cada serie de intentos de caché de tokens de hello tooload para la autenticación. No debe ser necesario toosign en.
