---
title: "aaaHow toouse hello Azure SDK para aplicaciones móviles para Android | Documentos de Microsoft"
description: "¿Cómo toouse Hola SDK de aplicaciones móviles de Azure para Android"
services: app-service\mobile
documentationcenter: android
author: ggailey777
manager: syntaxc4
ms.assetid: 5352d1e4-7685-4a11-aaf4-10bd2fa9f9fc
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 04/25/2017
ms.author: glenga
ms.openlocfilehash: 56eb73c4e1703d69877be499a09fc2130f1d68e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-mobile-apps-sdk-for-android"></a>¿Cómo toouse Hola SDK de aplicaciones móviles de Azure para Android

Esta guía le mostrará cómo toouse Hola a cliente de Android SDK para aplicaciones móviles tooimplement los escenarios comunes, como:

* Consultas de datos (inserción, actualización y eliminación)
* Autenticación
* Control de errores
* Personalización de cliente de Hola.

Esta guía se centra en hello cliente SDK de Android.  toolearn Obtenga más información sobre hello servidor SDK para aplicaciones móviles, consulte [trabajar con back-end de .NET SDK] [ 10] o [cómo toouse Hola Node.js back-end SDK] [ 11].

## <a name="reference-documentation"></a>Documentación de referencia

Puede encontrar Hola [referencia de la API de Javadocs] [ 12] de la biblioteca de cliente de Android hello en GitHub.

## <a name="supported-platforms"></a>Plataformas compatibles

Hello Azure SDK para aplicaciones móviles para Android admite niveles de API 19 y 24 (KitKat a través de nueces) para factores de forma de teléfono y Tablet PC.  La autenticación, en concreto, utiliza un credenciales de toogather del enfoque de framework web comunes.  La autenticación de flujo de servidor no funciona con dispositivos pequeños, por ejemplo, relojes.

## <a name="setup-and-prerequisites"></a>Configuración y requisitos previos

Hola completa [inicio rápido de aplicaciones móviles](app-service-mobile-android-get-started.md) tutorial.  Esta tarea garantiza que se cumplan todos los requisitos previos del desarrollo de aplicaciones de Mobile Apps de Azure.  Hola inicio rápido también ayuda a configurar su cuenta y crear su primer back-end de aplicación móvil.

Si decide no toocomplete tutorial de inicio rápido de hello, complete Hola siguientes tareas:

* [crear un aplicación móvil de back-end] [ 13] toouse con la aplicación Android.
* En Android Studio [actualización hello Gradle compilar archivos](#gradle-build).
* [Habilite permisos de Internet](#enable-internet).

### <a name="gradle-build"></a>Actualizar hello Gradle crear archivo

Cambie ambos archivos **build.gradle** :

1. Agregue este código toohello *proyecto* nivel **build.gradle** archivo dentro de hello *buildscript* etiqueta:

    ```text
    buildscript {
        repositories {
            jcenter()
        }
    }
    ```

2. Agregue este código toohello *módulo aplicación* nivel **build.gradle** archivo dentro de hello *dependencias* etiqueta:

    ```text
    compile 'com.microsoft.azure:azure-mobile-android:3.3.0'
    ```

    Actualmente la versión más reciente de hello es 3.3.0. se enumeran las versiones compatibles de Hello [en bintray][14].

### <a name="enable-internet"></a>Habilitación de permisos de Internet

tooaccess Azure, la aplicación debe tener permiso de INTERNET de hello habilitado. Si aún no está habilitado, agregue Hola después de la línea de código tooyour **AndroidManifest.xml** archivo:

```xml
<uses-permission android:name="android.permission.INTERNET" />
```

## <a name="create-a-client-connection"></a>Creación de una conexión de cliente

Aplicaciones móviles de Azure proporciona cuatro funciones tooyour de aplicaciones móviles:

* Acceso a datos y sincronización sin conexión con un servicio de Azure Mobile Apps.
* Llamar a las API de personalizado que se escriben con hello SDK de servidor de aplicaciones móviles de Azure.
* Autenticación con Autenticación y autorización de Azure App Service.
* Registro de notificaciones push con Notification Hubs.

Cada una de estas funciones requiere en primer lugar que se cree un objeto `MobileServiceClient`.  Solo se debe crear un objeto `MobileServiceClient` dentro de su cliente móvil (es decir, debe tener un patrón singleton).  toocreate un `MobileServiceClient` objeto:

```java
MobileServiceClient mClient = new MobileServiceClient(
    "<MobileAppUrl>",       // Replace with hello Site URL
    this);                  // Your application Context
```

Hola `<MobileAppUrl>` es una cadena o un objeto de dirección URL que señala el back-end de tooyour móvil.  Si usas toohost de servicio de aplicaciones de Azure el back-end móvil, a continuación, asegúrese de usar Hola segura `https://` versión de dirección URL de Hola.

Hola cliente también requiere acceso toohello actividad o contexto - hello `this` parámetro en el ejemplo de Hola.  Hola MobileServiceClient construcción debe realizarse en hello `onCreate()` método de hello al que hace referencia la actividad en hello `AndroidManifest.xml` archivo.

Como procedimiento recomendado, debe abstraer la comunicación del servidor en su propia clase (patrón singleton).  En este caso, debería pasar Hola actividad dentro de hello constructor tooappropriately Configurar servicio Hola.  Por ejemplo:

```java
package com.example.appname.services;

import android.content.Context;
import com.microsoft.windowsazure.mobileservices.*;

public AzureServiceAdapter {
    private String mMobileBackendUrl = "https://myappname.azurewebsites.net";
    private Context mContext;
    private MobileServiceClient mClient;
    private static AzureServiceAdapter mInstance = null;

    private AzureServiceAdapter(Context context) {
        mContext = context;
        mClient = new MobileServiceClient(mMobileBackendUrl, mContext);
    }

    public static void Initialize(Context context) {
        if (mInstance == null) {
            mInstance = new AzureServiceAdapter(context);
        } else {
            throw new IllegalStateException("AzureServiceAdapter is already initialized");
        }
    }

    public static AzureServiceAdapter getInstance() {
        if (mInstance == null) {
            throw new IllegalStateException("AzureServiceAdapter is not initialized");
        }
        return mInstance;
    }

    public MobileServiceClient getClient() {
        return mClient;
    }

    // Place any public methods that operate on mClient here.
}
```

Ahora puede llamar a `AzureServiceAdapter.Initialize(this);` en hello `onCreate()` método de su actividad principal.  Usa ningún otro método necesidad de cliente de acceso toohello `AzureServiceAdapter.getInstance();` tooobtain un adaptador de servicio de toohello de referencia.

## <a name="data-operations"></a>Operaciones de datos

núcleo de Hola de hello SDK de aplicaciones móviles de Azure es tooprovide acceso toodata almacenado en SQL Azure en el back-end de hello aplicación móvil.  Se puede acceder a estos datos mediante clases fuertemente tipadas (preferidas) o consultas sin tipo (no se recomienda).  masiva Hola de esta sección se ocupa utilizando clases fuertemente tipadas.

### <a name="define-client-data-classes"></a>Definición de clases de datos de cliente

tooaccess datos de tablas de SQL Azure, definir clases de datos de cliente que se corresponden toohello tablas en el back-end de hello aplicación móvil. Ejemplos de este tema supone que una tabla denominada **MyDataTable**, que tiene Hola siguientes columnas:

* id
* text
* complete

Hello correspondiente objeto de cliente escrito reside en un archivo denominado **MyDataTable.java**:

```java
public class ToDoItem {
    private String id;
    private String text;
    private Boolean complete;
}
```

Agregue los métodos captador y establecedor para cada campo que agregue.  Si la tabla de SQL Azure contiene más columnas, podría agregar clase de hello correspondientes campos toothis.  Por ejemplo, si hello DTO (objeto de transferencia de datos) tenía una columna de prioridad de tipo entero, a continuación, puede agregar este campo, junto con sus métodos de captador y establecedor:

```java
private Integer priority;

/**
* Returns hello item priority
*/
public Integer getPriority() {
    return mPriority;
}

/**
* Sets hello item priority
*
* @param priority
*            priority tooset
*/
public final void setPriority(Integer priority) {
    mPriority = priority;
}
```

toolearn toocreate tablas adicionales en el back-end de aplicaciones móviles, vea [Cómo: definir un controlador de tabla] [ 15] (back-end de. NET) o [definir tablas mediante un esquema dinámico] [ 16] (Node.js back-end).

Una tabla de back-end de aplicaciones móviles de Azure define cinco campos especiales, cuatro de los cuales son tooclients disponibles:

* `String id`: Hola identificador único global para el registro de hello.  Como práctica recomendada, asegúrese de representación de cadena de Hola Hola Id. de un [UUID] [ 17] objeto.
* `DateTimeOffset updatedAt`: Hola fecha/hora de la última actualización de Hola.  campo de Hello updatedAt se establece por servidor hello y nunca se debe establecer el código de cliente.
* `DateTimeOffset createdAt`: Hola fecha y hora se creó ese objeto Hola.  campo de registroen Hola se establece por servidor hello y nunca se debe establecer el código de cliente.
* `byte[] version`: Versión de hello normalmente se representa como una cadena, también se establece por servidor hello.
* `boolean deleted`: Indica que el registro de hello se ha eliminado pero no se purgan todavía.  No use `deleted` como propiedad en la clase.

Hola `id` campo es obligatorio.  Hola `updatedAt` campo y `version` campo se usa para la sincronización sin conexión (para la resolución de conflictos y de sincronización incremental respectivamente).  Hola `createdAt` campo es un campo de referencia y no se usa en el cliente de Hola.  nombres de Hello "en el cable" nombres de propiedades de hello y no son ajustables.  Sin embargo, puede crear una asignación entre el objeto y Hola nombres "en el cable" hello [gson] [ 3] biblioteca.  Por ejemplo:

```java
package com.example.zumoappname;

import com.microsoft.windowsazure.mobileservices.table.DateTimeOffset;

public class ToDoItem
{
    @com.google.gson.annotations.SerializedName("id")
    private String mId;
    public String getId() { return mId; }
    public final void setId(String id) { mId = id; }

    @com.google.gson.annotations.SerializedName("complete")
    private boolean mComplete;
    public boolean isComplete() { return mComplete; }
    public void setComplete(boolean complete) { mComplete = complete; }

    @com.google.gson.annotations.SerializedName("text")
    private String mText;
    public String getText() { return mText; }
    public final void setText(String text) { mText = text; }

    @com.google.gson.annotations.SerializedName("createdAt")
    private DateTimeOffset mCreatedAt;
    public DateTimeOffset getUpdatedAt() { return mCreatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset createdAt) { mCreatedAt = createdAt; }

    @com.google.gson.annotations.SerializedName("updatedAt")
    private DateTimeOffset mUpdatedAt;
    public DateTimeOffset getUpdatedAt() { return mUpdatedAt; }
    protected DateTimeOffset setUpdatedAt(DateTimeOffset updatedAt) { mUpdatedAt = updatedAt; }

    @com.google.gson.annotations.SerializedName("version")
    private String mVersion;
    public String getText() { return mVersion; }
    public final void setText(String version) { mVersion = version; }

    public ToDoItem() { }

    public ToDoItem(String id, String text) {
        this.setId(id);
        this.setText(text);
    }

    @Override
    public boolean equals(Object o) {
        return o instanceof ToDoItem && ((ToDoItem) o).mId == mId;
    }

    @Override
    public String toString() {
        return getText();
    }
}
```

### <a name="create-a-table-reference"></a>Creación de una referencia de tabla

tooaccess una tabla, cree primero un [MobileServiceTable] [ 8] objeto que realiza la llamada hello **getTable** método en hello [MobileServiceClient][9].  Este método tiene dos sobrecargas:

```java
public class MobileServiceClient {
    public <E> MobileServiceTable<E> getTable(Class<E> clazz);
    public <E> MobileServiceTable<E> getTable(String name, Class<E> clazz);
}
```

Hola siguiente código, **mClient** es un objeto de referencia tooyour MobileServiceClient.  Hola primera sobrecarga se utiliza donde son nombre de clase de Hola y el nombre de la tabla de Hola Hola mismo, y se hello uno usa Hola inicio rápido:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable(ToDoItem.class);
```

Hello segunda sobrecarga se utiliza al nombre de la tabla de hello es diferente del nombre de la clase hello: Hola primer parámetro es el nombre de la tabla de Hola.

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getTable("ToDoItemBackup", ToDoItem.class);
```

## <a name="query"></a>Consulta de una tabla de back-end

En primer lugar, obtenga una referencia de tabla.  A continuación, ejecutar una consulta en la referencia de tabla Hola.  Una consulta es cualquier combinación de:

* Una `.where()` [cláusula de filtro](#filtering).
* Una `.orderBy()` [cláusula de ordenación](#sorting).
* Una `.select()` [cláusula de selección de campos](#selection).
* Una cláusula `.skip()` y `.top()` para [resultados paginados](#paging).

cláusulas de Hello deben presentarse en hello anterior orden.

### <a name="filter"></a>Filtrado de los resultados

Hola forma general de una consulta es:

```java
List<MyDataTable> results = mDataTable
    // More filters here
    .execute()          // Returns a ListenableFuture<E>
    .get()              // Converts hello async into a sync result
```

Hello en el ejemplo anterior se devuelve todos los resultados (arriba toohello tamaño de página máximo establecido por servidor hello).  Hola `.execute()` método ejecuta consultas de hello en hello back-end.  consulta Hello es convertido tooan [OData v3] [ 19] consulta antes de back-end de transmisión toohello aplicaciones móviles.  Una vez recibido, back-end de aplicaciones móviles de hello convierte la consulta de hello en una instrucción SQL antes de ejecutarlo en la instancia de SQL Azure Hola.  Puesto que la actividad de red tarda algún tiempo, Hola `.execute()` método devuelve un [ `ListenableFuture<E>` ] [ 18].

### <a name="filtering"></a>Filtrado de datos devueltos

Hola después de la ejecución de la consulta devuelve todos los elementos de hello **ToDoItem** tabla where **completa** es igual a **false**.

```java
List<ToDoItem> result = mToDoTable
    .where()
    .field("complete").eq(false)
    .execute()
    .get();
```

**mToDoTable** es Hola referencia toohello servicio móvil tabla que hemos creado anteriormente.

Definir un filtro mediante hello **donde** llamada al método en la referencia de tabla Hola. Hola **donde** método va seguido de un **campo** método seguido por un método que especifica el predicado lógico Hola. Los posibles métodos de predicado incluyen **eq** (igual a), **ne** (no igual a), **gt** (mayor que), **ge** (mayor o igual que), **lt** (menor que) o **le** (menor o igual que). Estos métodos permiten comparar el número y toospecific valores de campos de cadena.

Puede filtrar por fechas. Hello métodos siguientes permiten comparar el campo de fecha completa de Hola o partes de fecha de hello: **año**, **mes**, **día**, **hora**, **minuto**, y **segundo**. Hello en el ejemplo siguiente se agrega un filtro para los elementos cuyos *fecha de vencimiento* es igual a 2013.

```java
List<ToDoItem> results = MToDoTable
    .where()
    .year("due").eq(2013)
    .execute()
    .get();
```

Hello métodos siguientes admiten filtros complejos en campos de cadena: **startsWith**, **endsWith**, **concat**, **subcadena**, **indexOf**, **reemplazar**, **toLower**, **toUpper**, **recortar**, y  **longitud**. Hola siguiendo el ejemplo se filtra para filas de la tabla donde hello *texto* columna empieza por "PRI0".

```java
List<ToDoItem> results = mToDoTable
    .where()
    .startsWith("text", "PRI0")
    .execute()
    .get();
```

Hola siguiendo métodos de operador se admite en los campos de número: **agregar**, **sub**, **mul**, **div**, **mod**, **floor**, **ceiling**, y **de ida y vuelta**. Hola siguiendo el ejemplo se filtra para filas de la tabla donde hello **duración** es un número par.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .field("duration").mod(2).eq(0)
    .execute()
    .get();
```

Puede combinar predicados con estos métodos lógicos: **and**, **or** y **not**. Hola siguiente ejemplo combina dos Hola anteriores ejemplos.

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013).and().startsWith("text", "PRI0")
    .execute()
    .get();
```

Agrupe y anide los operadores lógicos:

```java
List<ToDoItem> results = mToDoTable
    .where()
    .year("due").eq(2013)
    .and(
        startsWith("text", "PRI0")
        .or()
        .field("duration").gt(10)
    )
    .execute().get();
```

Para obtener más descripción y ejemplos de filtrado, consulte [explorar la riqueza de Hola de modelo de consultas de cliente de Android hello][20].

### <a name="sorting"></a>Ordenación de datos devueltos

Hello código siguiente devuelve todos los elementos de una tabla de **ToDoItems** ordena de forma ascendente por hello *texto* campo. *mToDoTable* es hello toohello back-end tabla de referencia que creó anteriormente:

```java
List<ToDoItem> results = mToDoTable
    .orderBy("text", QueryOrder.Ascending)
    .execute()
    .get();
```

Hola el primer parámetro de hello **orderBy** método es un nombre de toohello igual de cadena del campo de hello en qué toosort. segundo parámetro de Hello usa hello **QueryOrder** toospecify de enumeración si toosort orden ascendente o descendente.  Si va a filtrar utilizando hello ***donde*** /método siguiente, hello ***donde*** se debe invocar el método antes de hello ***orderBy*** método.

### <a name="selection"></a>Selección de columnas específicas

Hello código siguiente muestra cómo tooreturn todos los elementos de una tabla de **ToDoItems**, pero solo se muestra hello **completa** y **texto** campos. **mToDoTable** es la tabla de back-end de toohello de referencia de Hola que hemos creado anteriormente.

```java
List<ToDoItemNarrow> result = mToDoTable
    .select("complete", "text")
    .execute()
    .get();
```

función select de Hello parámetros toohello son nombres de cadena de Hola Hola las columnas de tabla que desea tooreturn.  Hola **seleccione** método necesita toofollow métodos como **donde** y **orderBy**. Puede ir seguido de métodos de paginación como **skip** y **top**.

### <a name="paging"></a>Devolución de datos en páginas

Los datos **SIEMPRE** se devuelven en páginas.  número máximo de Hola de registros devueltos se establece por servidor hello.  Si el cliente de hello solicita más registros, servidor hello devuelve número máximo de Hola de registros.  De forma predeterminada, el tamaño de página máximo de hello en el servidor hello es 50 registros.

Hola primer ejemplo muestra cómo tooselect Hola cinco elementos principales de una tabla. consulta de Hello devuelve elementos de Hola de una tabla de **ToDoItems**. **mToDoTable** es hello toohello back-end tabla de referencia que creó anteriormente:

```java
List<ToDoItem> result = mToDoTable
    .top(5)
    .execute()
    .get();
```

Esta es una consulta que omite Hola cinco primeros elementos y, a continuación, devuelve Hola cinco siguiente:

```java
List<ToDoItem> result = mToDoTable
    .skip(5).top(5)
    .execute()
    .get();
```

Si desea tooget todos los registros en una tabla, implementan código tooiterate sobre todas las páginas:

```java
List<MyDataModel> results = new List<MyDataModel>();
int nResults;
do {
    int currentCount = results.size();
    List<MyDataModel> pagedResults = mDataTable
        .skip(currentCount).top(500)
        .execute().get();
    nResults = pagedResults.size();
    if (nResults > 0) {
        results.addAll(pagedResults);
    }
} while (nResults > 0);
```

Una solicitud para todos los registros con este método crea un mínimo de dos solicitudes toohello aplicaciones móviles back-end.

> [!TIP]
> Elige la opción tamaño de página derecha hello es un equilibrio entre el uso de memoria mientras está teniendo lugar solicitud hello, uso de ancho de banda y demora al recibir datos de hello completamente.  valor predeterminado de Hello (50 registros) es adecuado para todos los dispositivos.  Si exclusivamente opera en los dispositivos de memoria más grandes, aumentar hasta too500.  Hemos encontrado ese tamaño de página Hola aumenta más allá de 500 registra los resultados en inaceptables retrasos y problemas de memoria de gran tamaño.

### <a name="chaining"></a>Concatenación de métodos de consulta

métodos de Hola que se utilizan al consultar tablas de back-end se pueden concatenar. El encadenamiento de métodos permite tooselect columnas específicas de las filas filtradas que se ordenan y paginan de consulta. Puede crear filtros lógicos complejos.  Cada método de consulta devuelve un objeto Query. serie de hello tooend de métodos y consulta de ejecución realmente hello, llamada hello **ejecutar** método. Por ejemplo:

```java
List<ToDoItem> results = mToDoTable
        .where()
        .year("due").eq(2013)
        .and(
            startsWith("text", "PRI0").or().field("duration").gt(10)
        )
        .orderBy(duration, QueryOrder.Ascending)
        .select("id", "complete", "text", "duration")
        .skip(200).top(100)
        .execute()
        .get();
```

Hola encadenadas consulta métodos se deben ordenar como sigue:

1. Métodos de filtro (**where**)
2. Métodos de ordenación (**orderBy**)
3. Métodos de selección (**select**)
4. Métodos de paginación (**skip** y **top**)

## <a name="binding"></a>Enlazar la interfaz de usuario de datos toohello

El enlace de datos implica tres componentes:

* origen de datos de Hola
* diseño de pantalla de Hola
* adaptador de Hola que vincula dos Hola juntos.

En el código de ejemplo se devuelven datos Hola de tabla de Mobile aplicaciones SQL Azure de hello **ToDoItem** en una matriz. Esta actividad es uno de los patrones más comunes para las aplicaciones de datos.  Las consultas de base de datos a menudo devuelven un conjunto de filas que Hola obtiene de cliente en una lista o matriz. En este ejemplo, la matriz de hello es origen de datos de Hola.  código de Hello especifica un diseño de pantalla que define la vista de Hola de datos de Hola que aparece en el dispositivo de Hola.  Hello dos se enlazan junto con un adaptador, que en este código es una extensión de hello **ArrayAdapter&lt;ToDoItem&gt;**  clase.

#### <a name="layout"></a>Definir el diseño de Hola

diseño de Hola se define mediante varios fragmentos de código XML. Proporciona un diseño existente, Hola siguiente código representa hello **ListView** queremos toopopulate con nuestros datos del servidor.

```xml
    <ListView
        android:id="@+id/listViewToDo"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        tools:listitem="@layout/row_list_to_do" >
    </ListView>
```

En el anterior código de hello, Hola *listitem* atributo especifica el identificador de Hola de diseño de Hola para una fila individual en la lista de Hola. Este código especifica una casilla de verificación y su texto asociado y crea instancias una vez para cada elemento de lista de Hola. Este diseño no muestra hello **identificador** campo y un diseño más complejo debería especificar campos adicionales de presentación de Hola. Este código está en hello **row_list_to_do.xml** archivo.

```java
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="horizontal">
    <CheckBox
        android:id="@+id/checkToDoItem"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/checkbox_text" />
</LinearLayout>
```

#### <a name="adapter"></a>Definir adaptador Hola
Puesto que el origen de datos de Hola de nuestro punto de vista es una matriz de **ToDoItem**, nos subclase nuestro adaptador desde una **ArrayAdapter&lt;ToDoItem&gt;**  clase. Esta subclase genera una vista para cada **ToDoItem** con hello **row_list_to_do** diseño.  En el código, definimos Hola después de la clase que es una extensión de hello **ArrayAdapter&lt;E&gt;**  clase:

```java
public class ToDoItemAdapter extends ArrayAdapter<ToDoItem> {
}
```

Invalidar adaptadores hello **getView** método. Por ejemplo:

```
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        View row = convertView;

        final ToDoItem currentItem = getItem(position);

        if (row == null) {
            LayoutInflater inflater = ((Activity) mContext).getLayoutInflater();
            row = inflater.inflate(R.layout.row_list_to_do, parent, false);
        }
        row.setTag(currentItem);

        final CheckBox checkBox = (CheckBox) row.findViewById(R.id.checkToDoItem);
        checkBox.setText(currentItem.getText());
        checkBox.setChecked(false);
        checkBox.setEnabled(true);

        checkBox.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View arg0) {
                if (checkBox.isChecked()) {
                    checkBox.setEnabled(false);
                    if (mContext instanceof ToDoActivity) {
                        ToDoActivity activity = (ToDoActivity) mContext;
                        activity.checkItem(currentItem);
                    }
                }
            }
        });
        return row;
    }
```

Creamos una instancia de esta clase en nuestra actividad de la forma siguiente:

```java
    ToDoItemAdapter mAdapter;
    mAdapter = new ToDoItemAdapter(this, R.layout.row_list_to_do);
```

Hola segundo parámetro toohello ToDoItemAdapter constructor es un diseño de toohello de referencia. Ahora se puede crear una instancia hello **ListView** y asignar Hola adaptador toohello **ListView**.

```java
    ListView listViewToDo = (ListView) findViewById(R.id.listViewToDo);
    listViewToDo.setAdapter(mAdapter);
```

#### <a name="use-adapter"></a>Usar Hola adaptador tooBind toohello interfaz de usuario

Ya estás listo toouse enlace de datos. Hello código siguiente muestra cómo tooget elementos en la tabla de Hola y rellenos Hola adaptador local con hello productos devuelto.

```java
    public void showAll(View view) {
        AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
            @Override
            protected Void doInBackground(Void... params) {
                try {
                    final List<ToDoItem> results = mToDoTable.execute().get();
                    runOnUiThread(new Runnable() {

                        @Override
                        public void run() {
                            mAdapter.clear();
                            for (ToDoItem item : results) {
                                mAdapter.add(item);
                            }
                        }
                    });
                } catch (Exception exception) {
                    createAndShowDialog(exception, "Error");
                }
                return null;
            }
        };
        runAsyncTask(task);
    }
```

Llame al adaptador de hello cualquier momento modificar hello **ToDoItem** tabla. Como las modificaciones se realizan de registro en registro, se ocupará de una sola fila en lugar de una serie de ellas. Cuando se inserta un elemento, llame a hello **agregar** método en Hola adaptador; cuando se elimina, llamar a hello **quitar** método.

Puede encontrar un ejemplo completo en hello [proyecto de inicio rápido Android][21].

## <a name="inserting"></a>Insertar datos en hello back-end

Crear una instancia de hello *ToDoItem* clase y establecer sus propiedades.

```java
ToDoItem item = new ToDoItem();
item.text = "Test Program";
item.complete = false;
```

A continuación, utilice **insert()** tooinsert un objeto:

```java
ToDoItem entity = mToDoTable
    .insert(item)       // Returns a ListenableFuture<ToDoItem>
    .get();
```

Hola devuelve coincidencias de entidad datos Hola insertados en la tabla de back-end de hello, Id. de hello incluye y cualquier otro valor (como hello `createdAt`, `updatedAt`, y `version` campos) establecido en hello back-end.

Las tablas de Mobile Apps requieren una columna de clave principal denominada " **id**". Esta columna debe ser una cadena. valor predeterminado de Hola de columna de Id. de hello es un GUID.  Puede proporcionar otros valores únicos, como nombres de usuario o direcciones de correo electrónico. Cuando no se proporciona un valor de identificador de cadena para un registro insertado, Hola back-end genera un nuevo GUID.

Los valores de Id. de cadena proporcionan Hola siguientes ventajas:

* Se pueden generar identificadores sin crear una base de datos de toohello de ida y vuelta.
* Los registros son toomerge más fácil de diferentes tablas o bases de datos.
* Los valores de los identificadores se integran mejor con una lógica de aplicación.

Los valores de identificador de cadena son **OBLIGATORIOS** para poder utilizar la sincronización sin conexión.  No se puede cambiar un Id. una vez que se almacena en la base de datos de back-end de Hola.

## <a name="updating"></a>Actualización de los datos en una aplicación móvil

tooupdate datos en una tabla, pasar Hola nuevo objeto toohello **update()** método.

```java
mToDoTable
    .update(item)   // Returns a ListenableFuture<ToDoItem>
    .get();
```

En este ejemplo, *elemento* es una fila de tooa de referencia en hello *ToDoItem* tabla, lo que ha tenido algún tooit cambios realizados.  Hola de fila con hello mismo **identificador** se actualiza.

## <a name="deleting"></a>Eliminación de datos en una aplicación móvil

Hola siguiente código muestra cómo toodelete datos de una tabla especificando Hola objeto de datos.

```java
mToDoTable
    .delete(item);
```

También puede eliminar un elemento mediante la especificación de hello **identificador** campo de hello toodelete de fila.

```java
String myRowId = "2FA404AB-E458-44CD-BC1B-3BC847EF0902";
mToDoTable
    .delete(myRowId);
```

## <a name="lookup"></a>Búsqueda de un elemento específico por el identificador

Buscar un elemento con un valor concreto **identificador** campo con hello **lookUp()** método:

```java
ToDoItem result = mToDoTable
    .lookUp("0380BAFB-BCFF-443C-B7D5-30199F730335")
    .get();
```

## <a name="untyped"></a>Trabajo con datos sin tipo

modelo de programación sin tipo Hello ofrece control exacto sobre la serialización de JSON.  Hay algunos escenarios comunes donde puede toouse un modelo de programación sin tipo. Por ejemplo, si la tabla de back-end contiene muchas columnas y sólo necesita tooreference un subconjunto de columnas de Hola.  modelo con tipo Hello requiere toodefine todas las columnas de hello definidas en el back-end de hello aplicaciones móviles en la clase de datos.  La mayoría de hello llamadas de API para tener acceso a datos es similar toohello escrito llamadas de programación. Hello principal diferencia es que en el modelo sin tipo hello invoca métodos en hello **MobileServiceJsonTable** objeto, en lugar de hello **MobileServiceTable** objeto.

### <a name="json_instance"></a>Creación de una instancia de tabla sin tipo

Toohello similar con tipo modelo, primero debe obtener una referencia de tabla, pero en este caso es un **MobileServicesJsonTable** objeto. Obtener referencia Hola Hola llamada **getTable** método en una instancia de cliente hello:

```java
private MobileServiceJsonTable mJsonToDoTable;
//...
mJsonToDoTable = mClient.getTable("ToDoItem");
```

Una vez haya creado una instancia de hello **MobileServiceJsonTable**, prácticamente ha Hola misma API disponible como modelo de programación con tipo hello. En algunos casos, los métodos de hello toman un parámetro sin tipo en lugar de un parámetro con tipo.

### <a name="json_insert"></a>Inserción de una tabla sin tipo
Hola el siguiente código muestra cómo toodo una instrucción insert. primer paso Hello es toocreate una [JsonObject][1], que forma parte del programa Hola a [gson] [ 3] biblioteca.

```java
JsonObject jsonItem = new JsonObject();
jsonItem.addProperty("text", "Wake up");
jsonItem.addProperty("complete", false);
```

A continuación, utilice **insert()** objeto sin tipo de hello tooinsert en tabla Hola.

```java
JsonObject insertedItem = mJsonToDoTable
    .insert(jsonItem)
    .get();
```

Si necesita tooget Hola ID de objeto de hello insertado, usar hello **getAsJsonPrimitive()** método.

```java
String id = insertedItem.getAsJsonPrimitive("id").getAsString();
```
### <a name="json_delete"></a>Eliminación de una tabla sin tipo
Hello código siguiente muestra cómo toodelete una instancia, en este caso, Hola la misma instancia de un **JsonObject** que se creó en antes de hello *insertar* ejemplo. código de Hello es hello igual que con hello escribir caso, aunque método hello tiene una signatura diferente puesto que hace referencia a un **JsonObject**.

```java
mToDoTable
    .delete(insertedItem);
```

También puede eliminar una instancia directamente usando su identificador:

```java
mToDoTable.delete(ID);
```

### <a name="json_get"></a>Devolución de todas las filas de una tabla sin tipo
Hola el siguiente código muestra cómo tooretrieve una tabla completa. Puesto que utiliza una tabla de JSON, puede recuperar selectivamente solo algunas de las columnas de tabla de Hola.

```java
public void showAllUntyped(View view) {
    new AsyncTask<Void, Void, Void>() {
        @Override
        protected Void doInBackground(Void... params) {
            try {
                final JsonElement result = mJsonToDoTable.execute().get();
                final JsonArray results = result.getAsJsonArray();
                runOnUiThread(new Runnable() {

                    @Override
                    public void run() {
                        mAdapter.clear();
                        for (JsonElement item : results) {
                            String ID = item.getAsJsonObject().getAsJsonPrimitive("id").getAsString();
                            String mText = item.getAsJsonObject().getAsJsonPrimitive("text").getAsString();
                            Boolean mComplete = item.getAsJsonObject().getAsJsonPrimitive("complete").getAsBoolean();
                            ToDoItem mToDoItem = new ToDoItem();
                            mToDoItem.setId(ID);
                            mToDoItem.setText(mText);
                            mToDoItem.setComplete(mComplete);
                            mAdapter.add(mToDoItem);
                        }
                    }
                });
            } catch (Exception exception) {
                createAndShowDialog(exception, "Error");
            }
            return null;
        }
    }.execute();
}
```

Hello mismo conjunto de filtrado, filtrado y paginación métodos que están disponibles para el modelo con tipo hello están disponibles para hello sin tipo modelo.

## <a name="offline-sync"></a>Implementación de la sincronización sin conexión

Hola SDK de cliente de aplicaciones móviles de Azure también implementa sincronización sin conexión de datos con un toostore de base de datos de SQLite localmente una copia de datos del servidor de saludo.  Las operaciones realizadas en una tabla sin conexión no requieren conectividad móvil toowork.  Ayuda de sincronización sin conexión en la resistencia y el rendimiento a costa de Hola de una lógica más compleja para la resolución de conflictos.  Hola SDK de cliente de aplicaciones móviles de Azure implementa Hola siguientes características:

* Sincronización incremental: solo se descargan registros nuevos y actualizados, lo que ahorra ancho de banda y consumo de memoria.
* Simultaneidad optimista: Las operaciones se supone que toosucceed.  Resolución de conflictos se aplaza hasta que las actualizaciones se realizan en el servidor de Hola.
* La resolución de conflictos: Hola que SDK detecta cuándo un cambio conflictivo se ha realizado en el servidor de Hola y proporciona enlaces de usuario de hello tooalert.
* Eliminación temporal: Registros eliminados se marcan como eliminados, lo que permite a otro tooupdate de dispositivos en su caché sin conexión.

### <a name="initialize-offline-sync"></a>Inicialización de la sincronización sin conexión

Cada tabla sin conexión debe definirse en caché sin conexión de hello antes de su uso.  Normalmente, la definición de la tabla se realiza inmediatamente después de la creación de hello de cliente hello:

```java
AsyncTask<Void, Void, Void> initializeStore(MobileServiceClient mClient)
    throws MobileServiceLocalStoreException, ExecutionException, InterruptedException
{
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>() {
        @Override
        protected void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                if (syncContext.isInitialized()) {
                    return null;
                }
                SQLiteLocalStore localStore = new SQLiteLocalStore(mClient.getContext(), "offlineStore", null, 1);

                // Create a table definition.  As a best practice, store this with hello model definition and return it via
                // a static method
                Map<String, ColumnDataType> toDoItemDefinition = new HashMap<String, ColumnDataType>();
                toDoItemDefinition.put("id", ColumnDataType.String);
                toDoItemDefinition.put("complete", ColumnDataType.Boolean);
                toDoItemDefinition.put("text", ColumnDataType.String);
                toDoItemDefinition.put("version", ColumnDataType.String);
                toDoItemDefinition.put("updatedAt", ColumnDataType.DateTimeOffset);

                // Now define hello table in hello local store
                localStore.defineTable("ToDoItem", toDoItemDefinition);

                // Specify a sync handler for conflict resolution
                SimpleSyncHandler handler = new SimpleSyncHandler();

                // Initialize hello local store
                syncContext.initialize(localStore, handler).get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

### <a name="obtain-a-reference-toohello-offline-cache-table"></a>Obtener una tabla de la caché sin conexión de referencia toohello

Para una tabla en línea, use `.getTable()`.  Para una tabla sin conexión, use `.getSyncTable()`:

```java
MobileServiceTable<ToDoItem> mToDoTable = mClient.getSyncTable("ToDoItem", ToDoItem.class);
```

Todos los Hola métodos que están disponibles para las tablas en línea (incluido el filtrado, ordenación, paginación, insertar datos, actualizar datos y eliminación de datos) también funcionan bien en tablas en línea y sin conexión.

### <a name="synchronize-hello-local-offline-cache"></a>Sincronizar Hola caché sin conexión Local

La sincronización está dentro del control de saludo de la aplicación.  A continuación se muestra un método de sincronización de ejemplo:

```java
private AsyncTask<Void, Void, Void> sync(MobileServiceClient mClient) {
    AsyncTask<Void, Void, Void> task = new AsyncTask<Void, Void, Void>(){
        @Override
        protected Void doInBackground(Void... params) {
            try {
                MobileServiceSyncContext syncContext = mClient.getSyncContext();
                syncContext.push().get();
                mToDoTable.pull(null, "todoitem").get();
            } catch (final Exception e) {
                createAndShowDialogFromTask(e, "Error");
            }
            return null;
        }
    };
    return runAsyncTask(task);
}
```

Si se proporciona un nombre de consulta toohello `.pull(query, queryname)` método, sincronización incremental es tooreturn utilizados solo los registros que se hayan creado o modificado desde la extracción de hello última se completó correctamente.

### <a name="handle-conflicts-during-offline-synchronization"></a>Control de los conflictos durante la sincronización sin conexión

Si tiene lugar un conflicto durante una operación `.push()`, se produce una excepción `MobileServiceConflictException`.   el elemento de servidor emitido Hola se incrusta en excepción hello y se puede recuperar `.getItem()` en la excepción de Hola.  Ajustar la inserción de Hola por llamada Hola siguientes elementos en el objeto de Hola MobileServiceSyncContext:

*  `.cancelAndDiscardItem()`
*  `.cancelAndUpdateItem()`
*  `.updateOperationAndItem()`

Una vez que todos los conflictos se marcan como desee, llame a `.push()` nuevo tooresolve Hola a todos los conflictos.

## <a name="custom-api"></a>Llamada a una API personalizada

Una API personalizada le permite toodefine extremos personalizados que exponen la funcionalidad de servidor que no asigne tooan Insertar, actualizar, eliminar o la operación de lectura. Al usar una API personalizada, puede tener más control sobre la mensajería, incluida la lectura y el establecimiento de encabezados de mensajes HTTP y la definición del formato del cuerpo de un mensaje diferente de JSON.

Desde un cliente de Android, se llama a hello **invokeApi** método toocall Hola API punto de conexión personalizado. Hello en el ejemplo siguiente se muestra cómo toocall un punto de conexión de API denominado **completeAll**, que devuelve una clase de colección denominada **MarkAllResult**.

```java
public void completeItem(View view) {
    ListenableFuture<MarkAllResult> result = mClient.invokeApi("completeAll", MarkAllResult.class);
    Futures.addCallback(result, new FutureCallback<MarkAllResult>() {
        @Override
        public void onFailure(Throwable exc) {
            createAndShowDialog((Exception) exc, "Error");
        }

        @Override
        public void onSuccess(MarkAllResult result) {
            createAndShowDialog(result.getCount() + " item(s) marked as complete.", "Completed Items");
            refreshItemsFromTable();
        }
    });
}
```

Hola **invokeApi** método se llama en el cliente de hello, que envía una solicitud de una entrada de blog toohello nueva API personalizada. resultado de Hello devuelto por la API personalizada hello se muestra en un cuadro de diálogo de mensaje, tal y como se han producido errores. Otras versiones de **invokeApi** le permiten enviar un objeto en el cuerpo de la solicitud de hello, especificar método hello HTTP y enviar parámetros de consulta con la solicitud de hello si lo desea. También se proporcionan versiones sin tipo de **invokeApi** .

## <a name="authentication"></a>Agregar aplicación de autenticación tooyour

Tutoriales ya se describen en detalle cómo tooadd estas características.

App Service admite la [autenticación de los usuarios de aplicaciones](app-service-mobile-android-get-started-users.md) mediante diversos proveedores de identidades externos: Facebook, Google, cuenta de Microsoft, Twitter y Azure Active Directory. Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios. También puede utilizar la identidad de Hola a los usuarios autenticados tooimplement de reglas de autorización en el back-end.

Se admiten dos flujos de autenticación: un flujo de **servidor** y un flujo de **cliente**. flujo de servidor Hello proporciona experiencia de autenticación más sencilla de hello, tal y como se basa en la interfaz de web de proveedores de identidad de Hola.  Ningún SDK adicionales es tooimplement requiere autenticación de flujo del servidor. Autenticación de servidor flujo no proporciona una estrecha integración en dispositivos móviles de Hola y sólo se recomienda para la prueba de escenarios de concepto.

flujo de cliente Hello permite una integración más profunda con capacidades específicas del dispositivo, como el inicio de sesión único ya que se basa en SDK proporcionado por el proveedor de identidades de Hola.  Por ejemplo, puede integrar Hola Facebook SDK en la aplicación móvil.  cliente móvil de Hello intercambia en aplicación de Facebook hello y confirma su inicio de sesión antes de intercambiar las aplicación móvil de back-tooyour.

Cuatro pasos son tooenable requiere la autenticación en la aplicación:

* Registre la aplicación para llevar a cabo la autenticación con un proveedor de identidades.
* Configure el back-end de App Service.
* Restringir permisos de tabla tooauthenticated los usuarios solo en hello back-end del servicio de aplicaciones.
* Agregar aplicación de tooyour de código de autenticación.

Puede establecer permisos de acceso de toorestrict de tablas para operaciones específicas tooonly autenticado a los usuarios. También puede usar Hola SID de un usuario autenticado toomodify solicitudes.  Para obtener más información, consulte [empezar a trabajar con autenticación] y Hola documentación HOWTO de SDK de servidor.

### <a name="caching"></a>Autenticación: flujo de servidor

Hello código siguiente inicia un proceso de inicio de sesión de flujo de servidor mediante el proveedor de Google Hola.  Se requiere configuración adicional debido a los requisitos de seguridad de hello para el proveedor de Hola de Google:

```java
MobileServiceUser user = mClient.login(MobileServiceAuthenticationProvider.Google, "{url_scheme_of_your_app}", GOOGLE_LOGIN_REQUEST_CODE);
```

Además, agregue Hola después de la clase de actividad de método toohello principal:

```java
// You can choose any unique number here toodifferentiate auth providers from each other. Note this is hello same code at login() and onActivityResult().
public static final int GOOGLE_LOGIN_REQUEST_CODE = 1;

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
```

Hola `GOOGLE_LOGIN_REQUEST_CODE` definido en la ventana principal de actividad se usa para hello `login()` método y dentro de hello `onActivityResult()` método.  Puede elegir cualquier número único, como hello tantos sirve de hello `login()` hello y método `onActivityResult()` método.  Si se abstraer el código de cliente de hello en un adaptador de servicio (como se muestra anteriormente), debe llamar a los métodos adecuados de hello en el adaptador del servicio Hola.

También necesita proyecto de hello tooconfigure para customtabs.  En primer lugar, especifique una dirección URL de redireccionamiento.  Agregar Hola siguiente fragmento de código demasiado`AndroidManifest.xml`:

```xml
<activity android:name="com.microsoft.windowsazure.mobileservices.authentication.RedirectUrlActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        <data android:scheme="{url_scheme_of_your_app}" android:host="easyauth.callback"/>
    </intent-filter>
</activity>
```

Agregar hello **redirectUriScheme** toohello `build.gradle` archivo de la aplicación:

```text
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
```

Por último, agregue `com.android.support:customtabs:23.0.1` toohello lista de dependencias en hello `build.gradle` archivo:

```text
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.google.code.gson:gson:2.3'
    compile 'com.google.guava:guava:18.0'
    compile 'com.android.support:customtabs:23.0.1'
    compile 'com.squareup.okhttp:okhttp:2.5.0'
    compile 'com.microsoft.azure:azure-mobile-android:3.2.0@aar'
    compile 'com.microsoft.azure:azure-notifications-handler:1.0.1@jar'
}
```

Obtener Id. de Hola Hola ha iniciado la sesión del usuario de desde una **MobileServiceUser** con hello **getUserId** método. Para obtener un ejemplo de cómo toouse futuros toocall Hola API de inicio de sesión asincrónica, vea [empezar a trabajar con autenticación].

> [!WARNING]
> Hola menciona el esquema de dirección URL distingue mayúsculas de minúsculas.  Asegúrese de que todas las apariciones de `{url_scheme_of_you_app}` coincidan en las mayúsculas y minúsculas.

### <a name="caching"></a>Almacenamiento en caché de tokens de autenticación

Almacenamiento en caché de tokens de autenticación requiere toostore Hola Id. de usuario y el token de autenticación localmente en el dispositivo de Hola. Hello próxima vez que se inicia la aplicación hello, compruebe caché hello, y si estos valores están presentes, puede omitir el registro de hello en procedimiento y rehidratar a cliente hello con estos datos. Sin embargo, estos datos son importantes y deben almacenarse cifrarse por razones de seguridad en caso de que roben phone Hola.  Puede ver un ejemplo completo de cómo los tokens de autenticación de toocache en [sección de tokens de autenticación de caché][7].

Cuando intente toouse un token caducado, recibirá un *401 no autorizado* respuesta. Puede controlar los errores de autenticación usando filtros.  Filtros de interceptan las solicitudes toohello back-end del servicio de aplicaciones. código de filtro de Hello comprueba la respuesta de Hola para 401, desencadena el proceso de inicio de sesión de hello y, a continuación, reanuda la solicitud de Hola que generan Hola 401.

### <a name="refresh"></a>Uso de tokens de actualización

símbolo (token) de Hello devuelto por la autorización y autenticación del servicio de aplicación de Azure tiene un tiempo de vida definidos de una hora.  Después de este período, debe volver a autenticar usuario Hola.  Si está utilizando un token de larga duración que han recibido a través de la autenticación de flujo de cliente, a continuación, puede volver a autenticar con la autenticación de servicio de aplicación de Azure y la autorización mediante Hola mismo símbolo (token).  Se genera otro token de Azure App Service con una nueva duración.

También puede registrar Hola proveedor toouse Tokens de actualización.  Un token de actualización no está siempre disponible.  Se requiere configuración adicional:

* Para **Azure Active Directory**, configurar un secreto de cliente para hello aplicación de Azure Active Directory.  Especifique el secreto del cliente de Hola en Hola servicio de aplicaciones de Azure al configurar la autenticación de Azure Active Directory.  Al llamar a `.login()`, pase `response_type=code id_token` como parámetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("response_type", "code id_token");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.AzureActiveDirectory,
        "{url_scheme_of_your_app}",
        AAD_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Google**, pasar hello `access_type=offline` como parámetro:

    ```java
    HashMap<String, String> parameters = new HashMap<String, String>();
    parameters.put("access_type", "offline");
    MobileServiceUser user = mClient.login
        MobileServiceAuthenticationProvider.Google,
        "{url_scheme_of_your_app}",
        GOOGLE_LOGIN_REQUEST_CODE,
        parameters);
    ```

* Para **Account Microsoft**, seleccione hello `wl.offline_access` ámbito.

toorefresh un token, llame a `.refreshUser()`:

```java
MobileServiceUser user = mClient
    .refreshUser()  // async - returns a ListenableFuture<MobileServiceUser>
    .get();
```

Como práctica recomendada, cree un filtro que detecta una respuesta 401 desde servidor hello y trata de token de usuario de toorefresh Hola.

## <a name="log-in-with-client-flow-authentication"></a>Inicio de sesión con la autenticación de flujo de cliente

proceso general de Hello para iniciar sesión con autenticación de cliente flujo es como sigue:

* Configure Autenticación y autorización de Azure App Service como haría con la autenticación de flujo de servidor.
* Integrar el proveedor de autenticación de hello SDK para autenticación tooproduce un token de acceso.
* Llamar a hello `.login()` método tal como se indica a continuación:

    ```java
    JSONObject payload = new JSONObject();
    payload.put("access_token", result.getAccessToken());
    ListenableFuture<MobileServiceUser> mLogin = mClient.login("{provider}", payload.toString());
    Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
        @Override
        public void onFailure(Throwable exc) {
            exc.printStackTrace();
        }
        @Override
        public void onSuccess(MobileServiceUser user) {
            Log.d(TAG, "Login Complete");
        }
    });
    ```

Reemplace hello `onSuccess()` método con cualquier código que se desea toouse en un inicio de sesión correcto.  Hola `{provider}` cadena es un proveedor válido: **aad** (Azure Active Directory), **facebook**, **google**, **cuenta de Microsoft**, o **twitter**.  Si ha implementado la autenticación personalizada, también puede utilizar etiquetas de proveedor de autenticación personalizada hello.

### <a name="adal"></a>Autenticar a los usuarios con hello biblioteca de autenticación de Active Directory (ADAL)

Puede usar los usuarios de toosign de hello biblioteca de autenticación de Active Directory (ADAL) en la aplicación con Azure Active Directory. Mediante un inicio de sesión de flujo de cliente suele ser preferible toousing hello `loginAsync()` métodos tal como se proporciona una idea UX más nativa y permite la personalización adicional.

1. Configurar el aplicación móvil de back-end para el inicio de sesión AAD Hola siguiente [cómo tooconfigure aplicación de servicio de inicio de sesión de Active Directory] [ 22] tutorial. Asegúrese de que paso opcional de Hola de toocomplete de registrar una aplicación cliente nativa.
2. Instalar AAL modificando su Hola de tooinclude de archivo build.gradle siguientes definiciones:

```
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
packagingOptions {
    exclude 'META-INF/MSFTSIG.RSA'
    exclude 'META-INF/MSFTSIG.SF'
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
    compile 'com.android.support:support-v4:23.0.0'
}
```

1. Agregue Hola tras la aplicación de código tooyour, por lo que Hola después reemplazos:

* Reemplace **aquí de autoridad de INSERCIÓN** por nombre de Hola de inquilino de hello en el que se aprovisiona la aplicación. formato de Hello debe ser https://login.microsoftonline.com/contoso.onmicrosoft.com.
* Reemplace **Insertar recurso identificador aquí** con el identificador de cliente de Hola para su aplicación móvil de back-end. Puede obtener Id. de cliente de Hola de hello **avanzadas** en la ficha **configuración de Azure Active Directory** en el portal de Hola.
* Reemplace **INSERT-CLIENT-ID-aquí** con el Id. de cliente de Hola que copió de la aplicación de cliente nativo de Hola.
* Reemplace **INSERT-REDIRECT-URI-aquí** con su sitio */.auth/login/done* punto de conexión, mediante el esquema de hello HTTPS. Este valor debe ser similar demasiado*https://contoso.azurewebsites.net/.auth/login/done*.

```java
private AuthenticationContext mContext;

private void authenticate() {
    String authority = "INSERT-AUTHORITY-HERE";
    String resourceId = "INSERT-RESOURCE-ID-HERE";
    String clientId = "INSERT-CLIENT-ID-HERE";
    String redirectUri = "INSERT-REDIRECT-URI-HERE";
    try {
        mContext = new AuthenticationContext(this, authority, true);
        mContext.acquireToken(this, resourceId, clientId, redirectUri, PromptBehavior.Auto, "", callback);
    } catch (Exception exc) {
        exc.printStackTrace();
    }
}

private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {
    @Override
    public void onError(Exception exc) {
        if (exc instanceof AuthenticationException) {
            Log.d(TAG, "Cancelled");
        } else {
            Log.d(TAG, "Authentication error:" + exc.getMessage());
        }
    }

    @Override
    public void onSuccess(AuthenticationResult result) {
        if (result == null || result.getAccessToken() == null
                || result.getAccessToken().isEmpty()) {
            Log.d(TAG, "Token is empty");
        } else {
            try {
                JSONObject payload = new JSONObject();
                payload.put("access_token", result.getAccessToken());
                ListenableFuture<MobileServiceUser> mLogin = mClient.login("aad", payload.toString());
                Futures.addCallback(mLogin, new FutureCallback<MobileServiceUser>() {
                    @Override
                    public void onFailure(Throwable exc) {
                        exc.printStackTrace();
                    }
                    @Override
                    public void onSuccess(MobileServiceUser user) {
                        Log.d(TAG, "Login Complete");
                    }
                });
            }
            catch (Exception exc){
                Log.d(TAG, "Authentication error:" + exc.getMessage());
            }
        }
    }
};

@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);
    if (mContext != null) {
        mContext.onActivityResult(requestCode, resultCode, data);
    }
}
```

## <a name="filters"></a>Ajustar Hola comunicación entre cliente y servidor

Hola conexión de cliente es normalmente una conexión HTTP básica con hello subyacente de la biblioteca HTTP que se suministra con hello SDK de Android.  Hay varios motivos por los que desearía toochange que:

* Que se van a toouse una alternativa HTTP biblioteca tooadjust los tiempos de espera.
* Que se va a tooprovide una barra de progreso.
* Que se va a tooadd una funcionalidad de administración de toosupport API de encabezado personalizado.
* Que se va a toointercept una respuesta error para que puedan implementar la reautenticación.
* Desea que el servicio de análisis de tooan las solicitudes de toolog back-end.

### <a name="using-an-alternate-http-library"></a>Uso de una biblioteca HTTP alternativa

Llamar a hello `.setAndroidHttpClientFactory()` método inmediatamente después de crear la referencia de cliente.  Por ejemplo, tooset Hola conexión too60 segundos de espera (en lugar de valor predeterminado de hello 10 segundos):

```java
mClient = new MobileServiceClient("https://myappname.azurewebsites.net");
mClient.setAndroidHttpClientFactory(new OkHttpClientFactory() {
    @Override
    public OkHttpClient createOkHttpClient() {
        OkHttpClient client = new OkHttpClinet();
        client.setReadTimeout(60, TimeUnit.SECONDS);
        client.setWriteTimeout(60, TimeUnit.SECONDS);
        return client;
    }
});
```

### <a name="implement-a-progress-filter"></a>Implementación de un filtro de progreso

Puede implementar una intersección de todas las solicitudes mediante la implementación de `ServiceFilter`.  Por ejemplo, la siguiente Hola actualiza una barra de progreso creada previamente:

```java
private class ProgressFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        final SettableFuture<ServiceFilterResponse> resultFuture = SettableFuture.create();
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                if (mProgressBar != null) mProgressBar.setVisibility(ProgressBar.VISIBLE);
            }
        });

        ListenableFuture<ServiceFilterResponse> future = next.onNext(request);
        Futures.addCallback(future, new FutureCallback<ServiceFilterResponse>() {
            @Override
            public void onFailure(Throwable e) {
                resultFuture.setException(e);
            }
            @Override
            public void onSuccess(ServiceFilterResponse response) {
                runOnUiThread(new Runnable() {
                    @Override
                    pubic void run() {
                        if (mProgressBar != null)
                            mProgressBar.setVisibility(ProgressBar.GONE);
                    }
                });
                resultFuture.set(response);
            }
        });
        return resultFuture;
    }
}
```

Puede adjuntar a este cliente de toohello de filtro como se indica a continuación:

```java
mClient = new MobileServiceClient(applicationUrl).withFilter(new ProgressFilter());
```

### <a name="customize-request-headers"></a>Personalización de los encabezados de solicitud

Utilice Hola siguiente `ServiceFilter` y adjuntar filtro Hola Hola igual que Hola `ProgressFilter`:

```java
private class CustomHeaderFilter implements ServiceFilter {
    @Override
    public ListenableFuture<ServiceFilterResponse> handleRequest(ServiceFilterRequest request, NextServiceFilterCallback next) {
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                request.addHeader("X-APIM-Router", "mobileBackend");
            }
        });
        SettableFuture<ServiceFilterResponse> result = SettableFuture.create();
        try {
            ServiceFilterResponse response = next.onNext(request).get();
            result.set(response);
        } catch (Exception exc) {
            result.setException(exc);
        }
    }
}
```

### <a name="conversions"></a>Configuración de serialización automática

Puede especificar una estrategia de conversión que se aplica tooevery columna mediante el uso de hello [gson] [ 3] API. biblioteca de cliente de Android Hello usa [gson] [ 3] entre bastidores de hello tooserialize Java objetos tooJSON datos antes de enviar datos de hello tooAzure servicio de aplicaciones.  Hello código siguiente usa hello **setFieldNamingStrategy()** estrategia del método tooset Hola. En este ejemplo se eliminará Hola inicial (una "m"), minúsculas, a continuación, Hola siguiente caracteres y, por cada nombre de campo. Por ejemplo, convertiría "mld" en "id".  Implemente un hello tooreduce de estrategia de conversión necesita para `SerializedName()` las anotaciones en la mayoría de los campos.

```java
FieldNamingStrategy namingStrategy = new FieldNamingStrategy() {
    public String translateName(File field) {
        String name = field.getName();
        return Character.toLowerCase(name.charAt(1)) + name.substring(2);
    }
}

client.setGsonBuilder(
    MobileServiceClient
        .createMobileServiceGsonBuilder()
        .setFieldNamingStrategy(namingStategy)
);
```

Este código debe ejecutarse antes de crear una referencia de cliente móvil mediante hello **MobileServiceClient**.

<!-- URLs. -->
[Get started with Azure Mobile Apps]: app-service-mobile-android-get-started.md
[ASCII control codes C0 and C1]: http://en.wikipedia.org/wiki/Data_link_escape_character#C1_set
[Mobile Services SDK for Android]: http://go.microsoft.com/fwlink/p/?LinkID=717033
[Azure portal]: https://portal.azure.com
[empezar a trabajar con autenticación]: app-service-mobile-android-get-started-users.md
[1]: http://google-gson.googlecode.com/svn/trunk/gson/docs/javadocs/com/google/gson/JsonObject.html
[2]: http://hashtagfail.com/post/44606137082/mobile-services-android-serialization-gson
[3]: http://go.microsoft.com/fwlink/p/?LinkId=290801
[4]: http://go.microsoft.com/fwlink/p/?LinkId=296840
[5]: app-service-mobile-android-get-started-push.md
[6]: ../notification-hubs/notification-hubs-push-notification-overview.md#integration-with-app-service-mobile-apps
[7]: app-service-mobile-android-get-started-users.md#cache-tokens
[8]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/table/MobileServiceTable.html
[9]: http://azure.github.io/azure-mobile-apps-android-client/com/microsoft/windowsazure/mobileservices/MobileServiceClient.html
[10]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[11]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[12]: http://azure.github.io/azure-mobile-apps-android-client/
[13]: app-service-mobile-android-get-started.md#create-a-new-azure-mobile-app-backend
[14]: http://go.microsoft.com/fwlink/p/?LinkID=717034
[15]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#define-table-controller
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations
[17]: https://developer.android.com/reference/java/util/UUID.html
[18]: https://github.com/google/guava/wiki/ListenableFutureExplained
[19]: http://www.odata.org/documentation/odata-version-3-0/
[20]: http://hashtagfail.com/post/46493261719/mobile-services-android-querying
[21]: https://github.com/Azure-Samples/azure-mobile-apps-android-quickstart
[22]: app-service-mobile-how-to-configure-active-directory-authentication.md
[Future]: http://developer.android.com/reference/java/util/concurrent/Future.html
[AsyncTask]: http://developer.android.com/reference/android/os/AsyncTask.html
