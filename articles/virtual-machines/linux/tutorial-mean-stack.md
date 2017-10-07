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
# <a name="create-a-mongodb-express-angularjs-and-nodejs-mean-stack-on-a-linux-vm-in-azure"></a><span data-ttu-id="cbb3d-103">Creación de una pila de MongoDB, Express, AngularJS y Node.js (MEAN) en una máquina virtual Linux en Azure</span><span class="sxs-lookup"><span data-stu-id="cbb3d-103">Create a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure</span></span>

<span data-ttu-id="cbb3d-104">Este tutorial muestra cómo la pila tooimplement un MongoDB, rápida, AngularJS y Node.js (Media) en una VM de Linux en Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-104">This tutorial shows you how tooimplement a MongoDB, Express, AngularJS, and Node.js (MEAN) stack on a Linux VM in Azure.</span></span> <span data-ttu-id="cbb3d-105">pila de medio de Hola que cree permite agregar, eliminar y enumerar los libros en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-105">hello MEAN stack that you create enables adding, deleting, and listing books in a database.</span></span> <span data-ttu-id="cbb3d-106">Aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cbb3d-107">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cbb3d-107">Create a Linux VM</span></span>
> * <span data-ttu-id="cbb3d-108">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="cbb3d-108">Install Node.js</span></span>
> * <span data-ttu-id="cbb3d-109">MongoDB de instalar y configurar el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="cbb3d-109">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="cbb3d-110">Instale Express y configurar el servidor de toohello de rutas</span><span class="sxs-lookup"><span data-stu-id="cbb3d-110">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="cbb3d-111">Rutas de acceso Hola con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cbb3d-111">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="cbb3d-112">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="cbb3d-112">Run hello application</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cbb3d-113">Si elige tooinstall y usar hello CLI localmente, este tutorial requiere que se ejecuta la versión de CLI de Azure de hello 2.0.4 o versiones posteriores.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="cbb3d-114">Ejecutar `az --version` toofind versión de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cbb3d-115">Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cbb3d-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>


## <a name="create-a-linux-vm"></a><span data-ttu-id="cbb3d-116">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cbb3d-116">Create a Linux VM</span></span>

<span data-ttu-id="cbb3d-117">Crear un grupo de recursos con hello [crear grupo az](https://docs.microsoft.com/cli/azure/group#create) comando y crear una VM de Linux con hello [crear vm az](https://docs.microsoft.com/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-117">Create a resource group with hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command and create a Linux VM with hello [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> <span data-ttu-id="cbb3d-118">Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-118">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="cbb3d-119">Hello en el ejemplo siguiente se usa hello Azure CLI toocreate un grupo de recursos denominado *myResourceGroupMEAN* en hello *eastus* ubicación.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-119">hello following example uses hello Azure CLI toocreate a resource group named *myResourceGroupMEAN* in hello *eastus* location.</span></span> <span data-ttu-id="cbb3d-120">También se crea una máquina virtual denominada *myVM* con claves SSH, si aún no existen en una ubicación de claves predeterminada.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-120">A VM is created named *myVM* with SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="cbb3d-121">toouse un determinado conjunto de claves, use Hola--opción ssh-clave y valor.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-121">toouse a specific set of keys, use hello --ssh-key-value option.</span></span>

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

<span data-ttu-id="cbb3d-122">Cuando se ha creado la VM de hello, Hola CLI de Azure muestra información toohello similar siguiente ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-122">When hello VM has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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
<span data-ttu-id="cbb3d-123">Tome nota de hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-123">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="cbb3d-124">Esta dirección es hello tooaccess usa máquinas virtuales.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-124">This address is used tooaccess hello VM.</span></span>

<span data-ttu-id="cbb3d-125">Siguiente Hola de uso del comando toocreate una sesión SSH con hello VM.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-125">Use hello following command toocreate an SSH session with hello VM.</span></span> <span data-ttu-id="cbb3d-126">Asegúrese de que toouse Hola dirección IP pública.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-126">Make sure toouse hello correct public IP address.</span></span> <span data-ttu-id="cbb3d-127">En el ejemplo anterior, la dirección IP era 13.72.77.9.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-127">In our example above our IP address was 13.72.77.9.</span></span>

```bash
ssh azureuser@13.72.77.9
```

## <a name="install-nodejs"></a><span data-ttu-id="cbb3d-128">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="cbb3d-128">Install Node.js</span></span>

<span data-ttu-id="cbb3d-129">[Node.js](https://nodejs.org/en/) es un entorno de tiempo de ejecución de JavaScript integrado en el motor de V8 JavaScript de Chrome.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-129">[Node.js](https://nodejs.org/en/) is a JavaScript runtime built on Chrome's V8 JavaScript engine.</span></span> <span data-ttu-id="cbb3d-130">Node.js se utiliza en este tutorial tooset Hola que enruta Express y controladores de AngularJS.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-130">Node.js is used in this tutorial tooset up hello Express routes and AngularJS controllers.</span></span>

<span data-ttu-id="cbb3d-131">En hello VM, mediante el shell de bash Hola que abrió mediante SSH, instale Node.js.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-131">On hello VM, using hello bash shell that you opened with SSH, install Node.js.</span></span>

```bash
sudo apt-get install -y nodejs
```

## <a name="install-mongodb-and-set-up-hello-server"></a><span data-ttu-id="cbb3d-132">MongoDB de instalar y configurar el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="cbb3d-132">Install MongoDB and set up hello server</span></span>
<span data-ttu-id="cbb3d-133">[MongoDB](http://www.mongodb.com) almacena los datos en documentos flexibles, similares a JSON.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-133">[MongoDB](http://www.mongodb.com) stores data in flexible, JSON-like documents.</span></span> <span data-ttu-id="cbb3d-134">Campos de una base de datos pueden variar desde toodocument de documento y se puede cambiar la estructura de datos con el tiempo.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-134">Fields in a database can vary from document toodocument and data structure can be changed over time.</span></span> <span data-ttu-id="cbb3d-135">Para nuestra aplicación de ejemplo, vamos a agregar libro tooMongoDB de registros que contienen el nombre del libro, número isbn, autor y número de páginas.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-135">For our example application, we are adding book records tooMongoDB that contain book name, isbn number, author, and number of pages.</span></span> 

1. <span data-ttu-id="cbb3d-136">En hello VM, mediante el shell de bash Hola que abrió mediante SSH, establezca la clave de MongoDB de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-136">On hello VM, using hello bash shell that you opened with SSH, set hello MongoDB key.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64 ] http://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    ```

2. <span data-ttu-id="cbb3d-137">Actualizar administrador de paquetes de saludo con clave de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-137">Update hello package manager with hello key.</span></span>
  
    ```bash
    sudo apt-get update
    ```

3. <span data-ttu-id="cbb3d-138">Instale MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-138">Install MongoDB.</span></span>

    ```bash
    sudo apt-get install -y mongodb
    ```

4. <span data-ttu-id="cbb3d-139">Iniciar servidor hello.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-139">Start hello server.</span></span>

    ```bash
    sudo service mongodb start
    ```

5. <span data-ttu-id="cbb3d-140">También es necesario hello tooinstall [cuerpo analizador](https://www.npmjs.com/package/body-parser-json) paquete toohelp nos procesar Hola JSON se pasa en el servidor de toohello de solicitudes.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-140">We also need tooinstall hello [body-parser](https://www.npmjs.com/package/body-parser-json) package toohelp us process hello JSON passed in requests toohello server.</span></span>

    <span data-ttu-id="cbb3d-141">Instalar el Administrador de paquetes de npm Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-141">Install hello npm package manager.</span></span>

    ```bash
    sudo apt-get install npm
    ```

    <span data-ttu-id="cbb3d-142">Instalar el paquete de analizador de cuerpo de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-142">Install hello body parser package.</span></span>
    
    ```bash
    sudo npm install body-parser
    ```

6. <span data-ttu-id="cbb3d-143">Cree una carpeta denominada *libros* y agregue un tooit archivo denominado *server.js* que contiene la configuración de Hola para hello web server.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-143">Create a folder named *Books* and add a file tooit named *server.js* that contains hello configuration for hello web server.</span></span>

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

## <a name="install-express-and-set-up-routes-toohello-server"></a><span data-ttu-id="cbb3d-144">Instale Express y configurar el servidor de toohello de rutas</span><span class="sxs-lookup"><span data-stu-id="cbb3d-144">Install Express and set up routes toohello server</span></span>

<span data-ttu-id="cbb3d-145">[Express](https://expressjs.com) es una plataforma mínima y flexible para aplicaciones web que proporciona características para aplicaciones web y móviles.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-145">[Express](https://expressjs.com) is a minimal and flexible Node.js web application framework that provides features for web and mobile applications.</span></span> <span data-ttu-id="cbb3d-146">Express se utiliza en este tooand de información de libreta de toopass tutorial de nuestra base de datos de MongoDB.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-146">Express is used in this tutorial toopass book information tooand from our MongoDB database.</span></span> <span data-ttu-id="cbb3d-147">[Mongoose](http://mongoosejs.com) proporciona una solución basada en el esquema, directa toomodel datos de su aplicación.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-147">[Mongoose](http://mongoosejs.com) provides a straight-forward, schema-based solution toomodel your application data.</span></span> <span data-ttu-id="cbb3d-148">Mongoose se utiliza en este tutorial tooprovide un esquema de libro para base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-148">Mongoose is used in this tutorial tooprovide a book schema for hello database.</span></span>

1. <span data-ttu-id="cbb3d-149">Instale Express y Mongoose.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-149">Install Express and Mongoose.</span></span>

    ```bash
    sudo npm install express mongoose
    ```

2. <span data-ttu-id="cbb3d-150">Hola *libros* carpeta, cree una carpeta denominada *aplicaciones* y agregue un archivo denominado *routes.js* con hello express rutas definidas.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-150">In hello *Books* folder, create a folder named *apps* and add a file named *routes.js* with hello express routes defined.</span></span>

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

3. <span data-ttu-id="cbb3d-151">Hola *aplicaciones* carpeta, cree una carpeta denominada *modelos* y agregue un archivo denominado *book.js* con configuración de modelo de libreta de hello definida.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-151">In hello *apps* folder, create a folder named *models* and add a file named *book.js* with hello book model configuration defined.</span></span>  

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

## <a name="access-hello-routes-with-angularjs"></a><span data-ttu-id="cbb3d-152">Rutas de acceso Hola con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cbb3d-152">Access hello routes with AngularJS</span></span>

<span data-ttu-id="cbb3d-153">[AngularJS](https://angularjs.org) proporciona una plataforma web para crear vistas dinámicas en las aplicaciones web.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-153">[AngularJS](https://angularjs.org) provides a web framework for creating dynamic views in your web applications.</span></span> <span data-ttu-id="cbb3d-154">En este tutorial, se usa AngularJS tooconnect nuestra página web con Express y realizar acciones en nuestra base de datos del libro.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-154">In this tutorial, we use AngularJS tooconnect our web page with Express and perform actions on our book database.</span></span>

1. <span data-ttu-id="cbb3d-155">Cambiar directorio de hello realizar copias de seguridad también*libros* (`cd ../..`) y, a continuación, cree una carpeta denominada *público* y agregue un archivo denominado *script.js* con controlador Hola configuración definida.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-155">Change hello directory back up too*Books* (`cd ../..`), and then create a folder named *public* and add a file named *script.js* with hello controller configuration defined.</span></span>

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
    
2. <span data-ttu-id="cbb3d-156">Hola *público* carpeta, cree un archivo denominado *index.html* con la página web de hello definido.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-156">In hello *public* folder, create a file named *index.html* with hello web page defined.</span></span>

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

##  <a name="run-hello-application"></a><span data-ttu-id="cbb3d-157">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="cbb3d-157">Run hello application</span></span>

1. <span data-ttu-id="cbb3d-158">Cambiar directorio de hello realizar copias de seguridad también*libros* (`cd ..`) e inicie el servidor de hello, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-158">Change hello directory back up too*Books* (`cd ..`) and start hello server by running this command:</span></span>

    ```bash
    nodejs server.js
    ```

2. <span data-ttu-id="cbb3d-159">Abra una dirección de toohello de explorador web que registró para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-159">Open a web browser toohello address that you recorded for hello VM.</span></span> <span data-ttu-id="cbb3d-160">Por ejemplo, *http://13.72.77.9:3300*.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-160">For example, *http://13.72.77.9:3300*.</span></span> <span data-ttu-id="cbb3d-161">Debería ver algo parecido a Hola después de página:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-161">You should see something like hello following page:</span></span>

    ![Registro de libro](media/tutorial-mean/meanstack-init.png)

3. <span data-ttu-id="cbb3d-163">Escriba los datos en cuadros de texto hello y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-163">Enter data into hello textboxes and click **Add**.</span></span> <span data-ttu-id="cbb3d-164">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-164">For example:</span></span>

    ![Agregar registro de libro](media/tutorial-mean/meanstack-add.png)

4. <span data-ttu-id="cbb3d-166">Después de actualizar página hello, debería ver algo parecido a esta página:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-166">After refreshing hello page, you should see something like this page:</span></span>

    ![Agregar registros de libro](media/tutorial-mean/meanstack-list.png)

5. <span data-ttu-id="cbb3d-168">Puede hacer clic en **eliminar** y quitar el registro de arranque de Hola de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-168">You could click **Delete** and remove hello book record from hello database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbb3d-169">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cbb3d-169">Next steps</span></span>

<span data-ttu-id="cbb3d-170">En este tutorial, creó una aplicación web que realiza un seguimiento de los registros de libros con una pila MEAN en una máquina virtual Linux.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-170">In this tutorial, you created a web application that keeps track of book records using a MEAN stack on a Linux VM.</span></span> <span data-ttu-id="cbb3d-171">Ha aprendido a:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-171">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cbb3d-172">Creación de una máquina virtual Linux</span><span class="sxs-lookup"><span data-stu-id="cbb3d-172">Create a Linux VM</span></span>
> * <span data-ttu-id="cbb3d-173">Instalación de Node.js</span><span class="sxs-lookup"><span data-stu-id="cbb3d-173">Install Node.js</span></span>
> * <span data-ttu-id="cbb3d-174">MongoDB de instalar y configurar el servidor de Hola</span><span class="sxs-lookup"><span data-stu-id="cbb3d-174">Install MongoDB and set up hello server</span></span>
> * <span data-ttu-id="cbb3d-175">Instale Express y configurar el servidor de toohello de rutas</span><span class="sxs-lookup"><span data-stu-id="cbb3d-175">Install Express and set up routes toohello server</span></span>
> * <span data-ttu-id="cbb3d-176">Rutas de acceso Hola con AngularJS</span><span class="sxs-lookup"><span data-stu-id="cbb3d-176">Access hello routes with AngularJS</span></span>
> * <span data-ttu-id="cbb3d-177">Ejecutar la aplicación hello</span><span class="sxs-lookup"><span data-stu-id="cbb3d-177">Run hello application</span></span>

<span data-ttu-id="cbb3d-178">Avanzar toohello siguiente tutorial toolearn cómo toosecure los servidores web con certificados SSL.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-178">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cbb3d-179">Protección de un servidor web con SSL</span><span class="sxs-lookup"><span data-stu-id="cbb3d-179">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)
