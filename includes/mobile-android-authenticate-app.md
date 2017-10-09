
1. Abra el proyecto de hello en Android Studio.

2. En **el Explorador de proyectos** en Android Studio, abra el archivo de ToDoActivity.java de Hola y agregue Hola siguiendo las instrucciones de importación:

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. Agregar Hola siguiendo el método toohello **ToDoActivity** clase:

        // You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using hello Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check hello request code matches hello one we send in hello login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check hello error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    Este código crea un Hola de toohandle método proceso de autenticación de Google. Un cuadro de diálogo muestra el identificador hello Hola autenticado. Solo puede continuar si la autenticación es correcta.

    > [!NOTE]
    > Si está utilizando un proveedor de identidades distinto de Google, cambiar valor Hola pasado toohello **inicio de sesión** tooone de método de hello siguientes valores: _cuenta de Microsoft_, _Facebook_, _Twitter_, o _windowsazureactivedirectory_.

4. Hola **onCreate** método, agregue Hola siguiente línea de código después de código de hello que cree instancias de hello `MobileServiceClient` objeto.

        authenticate();

    Esta llamada inicia el proceso de autenticación de Hola.

5. Hola restantes código después de mover `authenticate();` en hello **onCreate** método tooa nueva **createTable** método:

        private void createTable() {

            // Get hello table instance toouse.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter toobind hello items with hello view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load hello items from Azure.
            refreshItemsFromTable();
        }

6. tooensure redirección funciona según lo esperado, agrega Hola siguiente fragmento de código de _RedirectUrlActivity_ too_AndroidManifest.xml_:

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. Agregar redirectUriScheme too_build.gradle_ de la aplicación Android.

        android {
            buildTypes {
                release {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
                debug {
                    // … …
                    manifestPlaceholders = ['redirectUriScheme': '{url_scheme_of_your_app}://easyauth.callback']
                }
            }
        }

8. Agregar dependencias de toohello com.android.support:customtabs:23.0.1 en su build.gradle:

      dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }

9. De hello **ejecutar** menú, haga clic en **ejecutar aplicación** toostart Hola aplicaciones e inicie sesión con su proveedor de identidades elegido.

> [!WARNING]
> Hola menciona el esquema de dirección URL distingue mayúsculas de minúsculas.  Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` uso Hola mismo caso.

Cuando se iniciado sesión correctamente, debe ejecutar la aplicación hello sin errores y debe tener el servicio back-end de tooquery capaz de Hola y realizar actualizaciones toodata.
