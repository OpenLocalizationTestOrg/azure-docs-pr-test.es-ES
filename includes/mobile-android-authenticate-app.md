
1. <span data-ttu-id="da9fa-101">Abra el proyecto de hello en Android Studio.</span><span class="sxs-lookup"><span data-stu-id="da9fa-101">Open hello project in Android Studio.</span></span>

2. <span data-ttu-id="da9fa-102">En **el Explorador de proyectos** en Android Studio, abra el archivo de ToDoActivity.java de Hola y agregue Hola siguiendo las instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="da9fa-102">In **Project Explorer** in Android Studio, open hello ToDoActivity.java file and add hello following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="da9fa-103">Agregar Hola siguiendo el método toohello **ToDoActivity** clase:</span><span class="sxs-lookup"><span data-stu-id="da9fa-103">Add hello following method toohello **ToDoActivity** class:</span></span>

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

    <span data-ttu-id="da9fa-104">Este código crea un Hola de toohandle método proceso de autenticación de Google.</span><span class="sxs-lookup"><span data-stu-id="da9fa-104">This code creates a method toohandle hello Google authentication process.</span></span> <span data-ttu-id="da9fa-105">Un cuadro de diálogo muestra el identificador hello Hola autenticado.</span><span class="sxs-lookup"><span data-stu-id="da9fa-105">A dialog displays hello ID of hello authenticated user.</span></span> <span data-ttu-id="da9fa-106">Solo puede continuar si la autenticación es correcta.</span><span class="sxs-lookup"><span data-stu-id="da9fa-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="da9fa-107">Si está utilizando un proveedor de identidades distinto de Google, cambiar valor Hola pasado toohello **inicio de sesión** tooone de método de hello siguientes valores: _cuenta de Microsoft_, _Facebook_, _Twitter_, o _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="da9fa-107">If you are using an identity provider other than Google, change hello value passed toohello **login** method tooone of hello following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="da9fa-108">Hola **onCreate** método, agregue Hola siguiente línea de código después de código de hello que cree instancias de hello `MobileServiceClient` objeto.</span><span class="sxs-lookup"><span data-stu-id="da9fa-108">In hello **onCreate** method, add hello following line of code after hello code that instantiates hello `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="da9fa-109">Esta llamada inicia el proceso de autenticación de Hola.</span><span class="sxs-lookup"><span data-stu-id="da9fa-109">This call starts hello authentication process.</span></span>

5. <span data-ttu-id="da9fa-110">Hola restantes código después de mover `authenticate();` en hello **onCreate** método tooa nueva **createTable** método:</span><span class="sxs-lookup"><span data-stu-id="da9fa-110">Move hello remaining code after `authenticate();` in hello **onCreate** method tooa new **createTable** method:</span></span>

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

6. <span data-ttu-id="da9fa-111">tooensure redirección funciona según lo esperado, agrega Hola siguiente fragmento de código de _RedirectUrlActivity_ too_AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="da9fa-111">tooensure redirection works as expected, add hello following snippet of _RedirectUrlActivity_ too_AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="da9fa-112">Agregar redirectUriScheme too_build.gradle_ de la aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="da9fa-112">Add redirectUriScheme too_build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="da9fa-113">Agregar dependencias de toohello com.android.support:customtabs:23.0.1 en su build.gradle:</span><span class="sxs-lookup"><span data-stu-id="da9fa-113">Add com.android.support:customtabs:23.0.1 toohello dependencies in your build.gradle:</span></span>

      <span data-ttu-id="da9fa-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="da9fa-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="da9fa-115">De hello **ejecutar** menú, haga clic en **ejecutar aplicación** toostart Hola aplicaciones e inicie sesión con su proveedor de identidades elegido.</span><span class="sxs-lookup"><span data-stu-id="da9fa-115">From hello **Run** menu, click **Run app** toostart hello app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="da9fa-116">Hola menciona el esquema de dirección URL distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="da9fa-116">hello URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="da9fa-117">Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` uso Hola mismo caso.</span><span class="sxs-lookup"><span data-stu-id="da9fa-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use hello same case.</span></span>

<span data-ttu-id="da9fa-118">Cuando se iniciado sesión correctamente, debe ejecutar la aplicación hello sin errores y debe tener el servicio back-end de tooquery capaz de Hola y realizar actualizaciones toodata.</span><span class="sxs-lookup"><span data-stu-id="da9fa-118">When you are successfully signed in, hello app should run without errors, and you should be able tooquery hello back-end service and make updates toodata.</span></span>
