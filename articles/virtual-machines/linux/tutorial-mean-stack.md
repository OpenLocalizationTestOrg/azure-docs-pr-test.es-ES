---
title: aaaCreate una media de pila en una VM de Linux en Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo la pila toocreate un MongoDB, rápida, AngularJS y Node.js (Media) en una VM de Linux en Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/08/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 82a8e34e60d2bb6e6670ee007faa1113ea78b716
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a>Creación de una pila de MongoDB, Express, AngularJS y Node.js (MEAN) en una máquina virtual Linux en Azure

Este tutorial muestra cómo la pila tooimplement un MongoDB, rápida, AngularJS y Node.js (Media) en una VM de Linux en Azure. pila de medio de Hola que cree permite agregar, eliminar y enumerar los libros en una base de datos. Aprenderá a:

> [!div class="checklist"]
> * Creación de una máquina virtual Linux
> * Instalación de Node.js
> * MongoDB de instalar y configurar el servidor de Hola
> * Instale Express y configurar el servidor de toohello de rutas
> * Rutas de acceso Hola con AngularJS
> * Ejecutar la aplicación hello

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores. Ejecutar `az --version` toofind versión de Hola. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).


## <a name="create-a-linux-vm"></a>Creación de una máquina virtual Linux

Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando y crear una VM de Linux con hello [crear vm az](https://docs.microsoft.com/cli/azure/vm#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.

Hello en el ejemplo siguiente se usa hello Azure CLI toocreate un grupo de recursos denominado *myResourceGroupMEAN* en hello *eastus* ubicación. También se crea una máquina virtual denominada *myVM* con claves SSH, si aún no existen en una ubicación de claves predeterminada. toouse un determinado conjunto de claves, use Hola--opción ssh-clave y valor.

```azurecli-interactive
az group create --name myResourceGroupMEAN --location eastus
az vm create \
    --resource-group myResourceGroupMEAN \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --admin-password 'Azure12345678!' \
    --generate-ssh-keys
az vm open-port --port 3300 --resource-group myResourceGroupMEAN --name myVM
```

Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo: 

```azurecli-interactive
{
  "fqdns": "",
  "id": "/subscriptions/{subscription-id}/resourceGroups/myResourceGroupMEAN/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.72.77.9",
  "resourceGroup": "myResourceGroupMEAN"
}
```
Tome nota de hello `publicIpAddress`. Esta dirección es hello tooaccess usa máquinas virtuales.

Siguiente Hola de uso del comando toocreate una sesión SSH con hello VM. Asegúrese de que toouse Hola dirección IP pública. En el ejemplo anterior, la dirección IP era 13.72.77.9.

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a>Instalación de Node.js

[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript integrado en el motor de V8 JavaScript de Chrome. Node.js se utiliza en este tutorial tooset Hola que enruta Express y controladores de AngularJS.

En hello VM, mediante el shell de bash Hola que abrió mediante SSH, instale Node.js.

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a>MongoDB de instalar y configurar el servidor de Hola
[MongoDB](http://www.mongodb.com) almacena los datos en documentos flexibles, similares a JSON. Campos de una base de datos pueden variar desde toodocument de documento y se puede cambiar la estructura de datos con el tiempo. Para nuestra aplicación de ejemplo, vamos a agregar libro tooMongoDB de registros que contienen el nombre del libro, número isbn, autor y número de páginas. 

1. En hello VM, mediante el shell de bash Hola que abrió mediante SSH, establezca la clave de MongoDB de Hola.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. Actualizar administrador de paquetes de saludo con clave de Hola.
  
    ```bash
    sudo apt-get update
    ```

3. Instale MongoDB.

    ```bash
    sudo apt-get install -y mongodb
    ```

4. Iniciar servidor hello.

    ```bash
    sudo service mongodb start
    ```

5. También es necesario hello tooinstall [cuerpo analizador](https://www.npmjs.com/package/body-parser-json) paquete toohelp nos procesar Hola JSON se pasa en el servidor de toohello de solicitudes.

    Instalar el Administrador de paquetes de npm Hola.

    ```bash
    sudo apt-get install npm
    ```

    Instalar el paquete de analizador de cuerpo de Hola.
    
    ```bash
    sudo npm install body-parser
    ```

6. Cree una carpeta denominada *libros* y agregue un tooit archivo denominado *server.js* que contiene la configuración de Hola para hello web server.

    ```node.js
    var express = require('express');
    var bodyParser = require('body-parser');
    var app = express();
    app.use(express.static(__dirname + '/public'));
    app.use(bodyParser.json());
    require('./apps/routes')(app);
    app.set('port', 3300);
    app.listen(app.get('port'), function() {
        console.log('Server up: http://localhost:' + app.get('port'));
    });
    ```

## <a name="install-express-and-set-up-routes-toohello-server"></a>Instale Express y configurar el servidor de toohello de rutas

[Express](https://expressjs.com) es una plataforma mínima y flexible para aplicaciones web que proporciona características para aplicaciones web y móviles. Express se utiliza en este tooand de información de libreta de toopass tutorial de nuestra base de datos de MongoDB. [Mongoose](http://mongoosejs.com) proporciona una solución basada en el esquema, directa toomodel datos de su aplicación. Mongoose se utiliza en este tutorial tooprovide un esquema de libro para base de datos de Hola.

1. Instale Express y Mongoose.

    ```bash
    sudo npm install express mongoose
    ```

2. Hola *libros* carpeta, cree una carpeta denominada *aplicaciones* y agregue un archivo denominado *routes.js* con hello express rutas definidas.

    ```node.js
    var Book = require('./models/book');
    module.exports = function(app) {
      app.get('/book', function(req, res) {
        Book.find({}, function(err, result) {
          if ( err ) throw err;
          res.json(result);
        });
      }); 
      app.post('/book', function(req, res) {
        var book = new Book( {
          name:req.body.name,
          isbn:req.body.isbn,
          author:req.body.author,
          pages:req.body.pages
        });
        book.save(function(err, result) {
          if ( err ) throw err;
          res.json( {
            message:"Successfully added book",
            book:result
          });
        });
      });
      app.delete("/book/:isbn", function(req, res) {
        Book.findOneAndRemove(req.query, function(err, result) {
          if ( err ) throw err;
          res.json( {
            message: "Successfully deleted hello book",
            book: result
          });
        });
      });
      var path = require('path');
      app.get('*', function(req, res) {
        res.sendfile(path.join(__dirname + '/public', 'index.html'));
      });
    };
    ```

3. Hola *aplicaciones* carpeta, cree una carpeta denominada *modelos* y agregue un archivo denominado *book.js* con configuración de modelo de libreta de hello definida.  

    ```node.js
    var mongoose = require('mongoose');
    var dbHost = 'mongodb://localhost:27017/test';
    mongoose.connect(dbHost);
    mongoose.connection;
    mongoose.set('debug', true);
    var bookSchema = mongoose.Schema( {
      name: String,
      isbn: {type: String, index: true},
      author: String,
      pages: Number
    });
    var Book = mongoose.model('Book', bookSchema);
    module.exports = mongoose.model('Book', bookSchema); 
    ```

## <a name="access-hello-routes-with-angularjs"></a>Rutas de acceso Hola con AngularJS

[AngularJS](https://angularjs.org) proporciona una plataforma web para crear vistas dinámicas en las aplicaciones web. En este tutorial, se usa AngularJS tooconnect nuestra página web con Express y realizar acciones en nuestra base de datos del libro.

1. Cambiar directorio de hello realizar copias de seguridad también*libros* (`cd ../..`) y, a continuación, cree una carpeta denominada *público* y agregue un archivo denominado *script.js* con controlador Hola configuración definida.

    ```node.js
    var app = angular.module('myApp', []);
    app.controller('myCtrl', function($scope, $http) {
      $http( {
        method: 'GET',
        url: '/book'
      }).then(function successCallback(response) {
        $scope.books = response.data;
      }, function errorCallback(response) {
        console.log('Error: ' + response);
      });
      $scope.del_book = function(book) {
        $http( {
          method: 'DELETE',
          url: '/book/:isbn',
          params: {'isbn': book.isbn}
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
      $scope.add_book = function() {
        var body = '{ "name": "' + $scope.Name + 
        '", "isbn": "' + $scope.Isbn +
        '", "author": "' + $scope.Author + 
        '", "pages": "' + $scope.Pages + '" }';
        $http({
          method: 'POST',
          url: '/book',
          data: body
        }).then(function successCallback(response) {
          console.log(response);
        }, function errorCallback(response) {
          console.log('Error: ' + response);
        });
      };
    });
    ```
    
2. Hola *público* carpeta, cree un archivo denominado *index.html* con la página web de hello definido.

    ```html
    <!doctype html>
    <html ng-app="myApp" ng-controller="myCtrl">
      <head>
        <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
        <script src="script.js"></script>
      </head>
      <body>
        <div>
          <table>
            <tr>
              <td>Name:</td> 
              <td><input type="text" ng-model="Name"></td>
            </tr>
            <tr>
              <td>Isbn:</td>
              <td><input type="text" ng-model="Isbn"></td>
            </tr>
            <tr>
              <td>Author:</td> 
              <td><input type="text" ng-model="Author"></td>
            </tr>
            <tr>
              <td>Pages:</td>
              <td><input type="number" ng-model="Pages"></td>
            </tr>
          </table>
          <button ng-click="add_book()">Add</button>
        </div>
        <hr>
        <div>
          <table>
            <tr>
              <th>Name</th>
              <th>Isbn</th>
              <th>Author</th>
              <th>Pages</th>
            </tr>
            <tr ng-repeat="book in books">
              <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
              <td>{{book.name}}</td>
              <td>{{book.isbn}}</td>
              <td>{{book.author}}</td>
              <td>{{book.pages}}</td>
            </tr>
          </table>
        </div>
      </body>
    </html>
    ```

##  <a name="run-hello-application"></a>Ejecutar la aplicación hello

1. Cambiar directorio de hello realizar copias de seguridad también*libros* (`cd ..`) e inicie el servidor de hello, ejecute este comando:

    ```bash
    nodejs server.js
    ```

2. Abra una dirección de toohello de explorador web que registró para hello máquina virtual. Por ejemplo, *http://13.72.77.9:3300*. Debería ver algo parecido a Hola después de página:

    ![Registro de libro](media/tutorial-mean/meanstack-init.png)

3. Escriba los datos en cuadros de texto hello y haga clic en **agregar**. Por ejemplo:

    ![Agregar registro de libro](media/tutorial-mean/meanstack-add.png)

4. Después de actualizar página hello, debería ver algo parecido a esta página:

    ![Agregar registros de libro](media/tutorial-mean/meanstack-list.png)

5. Puede hacer clic en **eliminar** y quitar el registro de arranque de Hola de base de datos de Hola.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, creó una aplicación web que realiza un seguimiento de los registros de libros con una pila MEAN en una máquina virtual Linux. Ha aprendido a:

> [!div class="checklist"]
> * Creación de una máquina virtual Linux
> * Instalación de Node.js
> * MongoDB de instalar y configurar el servidor de Hola
> * Instale Express y configurar el servidor de toohello de rutas
> * Rutas de acceso Hola con AngularJS
> * Ejecutar la aplicación hello

Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.

> [!div class="nextstepaction"]
> [Protección de un servidor web con SSL](tutorial-secure-web-server.md)
