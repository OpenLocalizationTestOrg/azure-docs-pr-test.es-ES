---
título: aaa "base de datos de Azure Cosmos: compilar una aplicación de consola de API de MongoDB con Golang y Hola portal de Azure | Descripción de Microsoft Docs": presenta un ejemplo de código de Golang puede usar tooconnect tooand consultar los servicios de Azure Cosmos DB: cosmos db autor: Durgaprasad Budhwani manager: editor jhubbard: mimig1

MS.Service: cosmos db ms.topic: artículo héroe ms.date: 07/21/2017 ms.author: mimig
---

# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-hello-azure-portal"></a>Azure Cosmos DB: Compilar una aplicación de consola de API de MongoDB con Golang y Hola portal de Azure

Azure Cosmos DB es un servicio de base de datos con varios modelos y de distribución global de Microsoft. Puede crear y consultar documentos, clave/valor y bases de datos de gráfico, todos ellos se benefician de la distribución global de Hola y capacidades de escala horizontal en el núcleo de hello de la base de datos de Azure Cosmos rápidamente.

Este inicio rápido se muestra cómo toouse existente [MongoDB](https://docs.microsoft.com/en-us/azure/cosmos-db/mongodb-introduction) aplicación escrita en [Golang](https://golang.org/) y conéctelo tooyour base de datos de Azure Cosmos base de datos, que es compatible con conexiones de cliente de MongoDB.

En otras palabras, la aplicación Golang sólo sabe que se está conectando con MongoDB APIs de base de datos de tooa. Es transparente toohello aplicación Hola a datos se almacena en la base de datos de Azure Cosmos.

## <a name="prerequisites"></a>Requisitos previos

- Una suscripción de Azure. Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free) antes de empezar.
- [Vaya](https://golang.org/dl/) y un conocimiento básico de hello [vaya](https://golang.org/) language.
- Un IDE: [Gogland](https://www.jetbrains.com/go/) de Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) de Microsoft o [Atom](https://atom.io/). En este tutorial, utilizo Goglang.

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Creación de una cuenta de base de datos

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Clonar aplicación de ejemplo de Hola

Clonar aplicación de ejemplo de Hola e instalar paquetes de hello necesario.

1. Cree una carpeta denominada CosmosDBSample dentro de la carpeta de GOROOT\src de hello, que es C:\Go\ de forma predeterminada.
2. Ejecute hello siguiente comando con una ventana de terminal de git como repositorio de git bash tooclone Hola ejemplo en la carpeta de CosmosDBSample Hola. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  Ejecute hello después el paquete de comando tooget Hola mgo. 

    ```
    go get gopkg.in/mgo.v2
    ```

Hola [mgo](http://labix.org/mgo) controlador (pronunciado como *mango*) es una [MongoDB](http://www.mongodb.org/) controlador para hello [vaya lenguaje](http://golang.org/) que implementa un variado y probando selección de características en una API muy sencilla después estándares giros de Go.

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a>Actualizar la cadena de conexión

Ahora vuelva atrás toohello tooget portal Azure la información de la cadena de conexión y se copia en la aplicación hello.

1. Haga clic en **inicio rápido** en Hola menú de navegación izquierdo y, a continuación, haga clic en **otros** información de cadena de conexión tooview Hola requerido Hola aplicación Go.

2. En Goglang, abra el archivo de main.go de hello en el directorio de GOROOT\CosmosDBSample hello y actualice Hola siguientes líneas de código que usa la información de cadena de conexión de Hola de hello portal de Azure como se muestra en la siguiente captura de pantalla de Hola. 

    nombre de la base de datos de Hello es el prefijo de Hola de hello **Host** valor en el panel de cadena de conexión de portal de Azure Hola. De la cuenta de hello que se muestra en la imagen de hello siguiente, nombre de la base de datos de hello es entrenador golang.

    ```go
    Database: "hello prefix of hello Host value in hello Azure portal",
    Username: "hello Username in hello Azure portal",
    Password: "hello Password in hello Azure portal",
    ```

    ![Inicio rápido de panel, otra ficha de información de la cadena de conexión de hello mostrando portal Azure Hola](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. Guarde el archivo de hello main.go.

## <a name="review-hello-code"></a>Revise el código de hello

Vamos a hacer una revisión rápida de lo que ocurre en el archivo de hello main.go. 

### <a name="connecting-hello-go-app-tooazure-cosmos-db"></a>Conectar Hola Go aplicación tooAzure Cosmos DB

Base de datos de Azure Cosmos admite Hola MongoDB SSL habilitado. tooconnect tooan MongoDB habilitado para SSL, necesita hello toodefine **DialServer** funcionando en [mgo. DialInfo](http://gopkg.in/mgo.v2#DialInfo)y asegúrese de usar de hello [tls. *Acceso telefónico* ](http://golang.org/pkg/crypto/tls#Dial) función conexión de hello tooperform.

Hola siguiente fragmento de código de Golang conecta Hola aplicación vaya a la base de datos MongoDB API de Azure Cosmos. Hola *DialInfo* clase contiene opciones para establecer una sesión con un clúster de MongoDB.

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// tooour Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect toomongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes hello session safety mode.
// If hello safe parameter is nil, hello session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. hello unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

Hola **mgo. Dial()** método se utiliza cuando no hay ninguna conexión de SSL. Para una conexión SSL, Hola **mgo. DialWithInfo()** método es necesario.

Una instancia de hello **{} DialWIthInfo** es objeto de sesión de hello toocreate usado. Una vez establecida la sesión de hello, puede tener acceso a colección Hola utilizando el siguiente fragmento de código de hello:

```go
collection := session.DB(“database”).C(“package”)
```

<a id="create-document"></a>

### <a name="create-a-document"></a>Creación de un documento

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a>Realizar consultas o leer un documento

Azure Cosmos DB admite consultas enriquecidas en los documentos JSON que se almacenan en las colecciones. Hello código de ejemplo siguiente muestra una consulta que se pueden ejecutar en documentos de hello en la colección.

```go
// Get a Document from hello collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a>Actualización de un documento

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a>Eliminar un documento

Azure Cosmos DB admite la eliminación de documentos JSON.

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-hello-app"></a>Ejecutar aplicación hello

1. En Goglang, asegúrese de que su GOPATH (disponible en **archivo**, **configuración**, **vaya**, **GOPATH**) incluyan la ubicación de hello en qué Hola gopkg se instaló, que es USERPROFILE\go de forma predeterminada. 
2. Comentario líneas de Hola que eliminar el documento de hello, líneas 91-96, para que puedan ver el documento de hello después de la aplicación hello en ejecución.
3. En Goglang, haga clic en **Ejecutar**y, a continuación, haga clic en **Ejecutar "Build main.go and run"**.

    aplicación Hello finaliza y muestra la descripción de Hola Hola del documento de creado en [crear un documento](#create-document).
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang que muestra la salida de hello de aplicación hello](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a>Revisar el documento en el Explorador de datos

Volver atrás toohello toosee portal Azure el documento en el Explorador de datos.

1. Haga clic en **Explorador de datos (vista previa)** en el menú de navegación izquierdo de hello, expanda **golang entrenador**, **paquete**y, a continuación, haga clic en **documentos**. Hola **documentos** , haga clic en hello \_documento de hello toodisplay de Id. en el panel derecho de Hola. 

    ![Documento de hello recién creado del explorador de datos que muestra](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. Puede trabajar con el documento de hello en línea y haga clic en **actualización** toosave lo. También puede eliminar el documento de hello, o crear nuevos documentos o las consultas.

## <a name="review-slas-in-hello-azure-portal"></a>Revise los SLA de hello portal de Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpieza de recursos

Si no va toocontinue toouse esta aplicación, eliminar todos los recursos creados por este tutorial rápido de hello portal de Azure con hello pasos:

1. En el menú de la izquierda de Hola Hola portal de Azure, haga clic en **grupos de recursos** y, a continuación, haga clic en nombre de hello del recurso de Hola que creó. 
2. En la página del grupo de recursos, haga clic en **eliminar**, escriba el nombre de Hola de hello recursos toodelete en el cuadro de texto hello y, a continuación, haga clic en **eliminar**.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo toocreate una cuenta de base de datos de Azure Cosmos y ejecutar una aplicación Golang con Hola API para MongoDB. Ahora puede importar la cuenta de base de datos de Cosmos tooyour datos adicionales. 

> [!div class="nextstepaction"]
> [Importar datos en la base de datos de Azure Cosmos para hello API de MongoDB](mongodb-migrate.md)
