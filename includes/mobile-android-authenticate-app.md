
1. <span data-ttu-id="c8d8c-101">Abra el proyecto en Android Studio.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-101">Open the project in Android Studio.</span></span>

2. <span data-ttu-id="c8d8c-102">En el **Explorador de proyectos** en Android Studio, abra el archivo ToDoActivity.java y agregue las siguientes instrucciones de importación:</span><span class="sxs-lookup"><span data-stu-id="c8d8c-102">In **Project Explorer** in Android Studio, open the ToDoActivity.java file and add the following import statements:</span></span>

        import java.util.concurrent.ExecutionException;
        import java.util.concurrent.atomic.AtomicBoolean;

        import android.content.Context;
        import android.content.SharedPreferences;
        import android.content.SharedPreferences.Editor;

        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceAuthenticationProvider;
        import com.microsoft.windowsazure.mobileservices.authentication.MobileServiceUser;

3. <span data-ttu-id="c8d8c-103">Agregue el método siguiente a la clase **TodoActivity** :</span><span class="sxs-lookup"><span data-stu-id="c8d8c-103">Add the following method to the **ToDoActivity** class:</span></span>

        // You can choose any unique number here to differentiate auth providers from each other. Note this is the same code at login() and onActivityResult().
        public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

        private void authenticate() {
            // Login using the Google provider.
            mClient.login("Google", "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
        }

        @Override
        protected void onActivityResult(int requestCode, int resultCode, Intent data) {
            // When request completes
            if (resultCode == RESULT_OK) {
                // Check the request code matches the one we send in the login request
                if (requestCode == GOOGLE_LOGIN_REQUEST_CODE) {
                    MobileServiceActivityResult result = mClient.onActivityResult(data);
                    if (result.isLoggedIn()) {
                        // login succeeded
                        createAndShowDialog(String.format("You are now logged in - %1$2s", mClient.getCurrentUser().getUserId()), "Success");
                        createTable();
                    } else {
                        // login failed, check the error message
                        String errorMessage = result.getErrorMessage();
                        createAndShowDialog(errorMessage, "Error");
                    }
                }
            }
        }

    <span data-ttu-id="c8d8c-104">Con este código, se crea un método para administrar el proceso de autenticación de Google.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-104">This code creates a method to handle the Google authentication process.</span></span> <span data-ttu-id="c8d8c-105">Aparece un cuadro de diálogo que muestra el identificador del usuario autenticado.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-105">A dialog displays the ID of the authenticated user.</span></span> <span data-ttu-id="c8d8c-106">Solo puede continuar si la autenticación es correcta.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-106">You can only proceed on a successful authentication.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c8d8c-107">Si usa un proveedor de identidades que no sea Google, cambie el valor pasado al método **login** a uno de los siguientes: _MicrosoftAccount_, _Facebook_, _Twitter_ o _windowsazureactivedirectory_.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-107">If you are using an identity provider other than Google, change the value passed to the **login** method to one of the following values: _MicrosoftAccount_, _Facebook_, _Twitter_, or _windowsazureactivedirectory_.</span></span>

4. <span data-ttu-id="c8d8c-108">En el método **onCreate**, agregue la siguiente línea de código después del código que crea una instancia del objeto `MobileServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-108">In the **onCreate** method, add the following line of code after the code that instantiates the `MobileServiceClient` object.</span></span>

        authenticate();

    <span data-ttu-id="c8d8c-109">De este modo se llama al proceso de autenticación.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-109">This call starts the authentication process.</span></span>

5. <span data-ttu-id="c8d8c-110">Mueva el código restante situado después de `authenticate();` en el método **onCreate** a un nuevo método **createTable**:</span><span class="sxs-lookup"><span data-stu-id="c8d8c-110">Move the remaining code after `authenticate();` in the **onCreate** method to a new **createTable** method:</span></span>

        private void createTable() {

            // Get the table instance to use.
            mToDoTable = mClient.getTable(ToDoItem.class);

            mTextNewToDo = (EditText) findViewById(R.id.textNewToDo);

            // Create an adapter to bind the items with the view.
            mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
            ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
            listViewToDo.setAdapter(mAdapter);

            // Load the items from Azure.
            refreshItemsFromTable();
        }

6. <span data-ttu-id="c8d8c-111">Para asegurarse de que el redireccionamiento funcione, agregue el siguiente fragmento de código de _RedirectUrlActivity_ a _AndroidManifest.xml_:</span><span class="sxs-lookup"><span data-stu-id="c8d8c-111">To ensure redirection works as expected, add the following snippet of _RedirectUrlActivity_ to _AndroidManifest.xml_:</span></span>

        <activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
            <intent-filter>
                <action android:name="android.intent.action.VIEW" />
                <category android:name="android.intent.category.DEFAULT" />
                <category android:name="android.intent.category.BROWSABLE" />
                <data android:scheme="{url_scheme_of_your_app}"
                    android:host="easyauth.callback"/>
            </intent-filter>
        </activity>

7. <span data-ttu-id="c8d8c-112">Agregue redirectUriScheme a _build.gradle_ de la aplicación Android.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-112">Add redirectUriScheme to _build.gradle_ of your Android application.</span></span>

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

8. <span data-ttu-id="c8d8c-113">Agregue com.android.support:customtabs:23.0.1 a las dependencias de build.gradle:</span><span class="sxs-lookup"><span data-stu-id="c8d8c-113">Add com.android.support:customtabs:23.0.1 to the dependencies in your build.gradle:</span></span>

      <span data-ttu-id="c8d8c-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span><span class="sxs-lookup"><span data-stu-id="c8d8c-114">dependencies {        // ...        compile 'com.android.support:customtabs:23.0.1'    }</span></span>

9. <span data-ttu-id="c8d8c-115">En el menú **Ejecutar**, haga clic en **Ejecutar aplicación** para iniciar la aplicación e inicie sesión con el proveedor de identidades que haya elegido.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-115">From the **Run** menu, click **Run app** to start the app and sign in with your chosen identity provider.</span></span>

> [!WARNING]
> <span data-ttu-id="c8d8c-116">El esquema de dirección URL mencionado distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-116">The URL Scheme mentioned is case-sensitive.</span></span>  <span data-ttu-id="c8d8c-117">Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` usen las mayúsculas y minúsculas del mismo modo.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-117">Ensure that all occurrences of `{url_scheme_of_you_app}` use the same case.</span></span>

<span data-ttu-id="c8d8c-118">Si ha iniciado sesión correctamente, la aplicación se ejecutará sin errores y deberá poder consultar el servicio back-end y realizar actualizaciones en los datos.</span><span class="sxs-lookup"><span data-stu-id="c8d8c-118">When you are successfully signed in, the app should run without errors, and you should be able to query the back-end service and make updates to data.</span></span>
