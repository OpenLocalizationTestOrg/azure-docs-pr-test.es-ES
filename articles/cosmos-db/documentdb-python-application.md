---
title: "tutorial de aplicación de aaaPython matraz web para la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Revise un tutorial de base de datos sobre el uso de datos de base de datos de Azure Cosmos toostore y acceso desde una aplicación web de Python matraz hospedada en Azure. Encuentre soluciones de desarrollo de aplicaciones."
keywords: "Desarrollo de aplicaciones, python flask, aplicación web de python, desarrollo web de python"
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Compilación de una aplicación web Node.js de Python Flask mediante Azure cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Este tutorial muestra cómo toouse base de datos de Azure Cosmos toostore y acceso a datos desde un Python web aplicación hospedada en Azure y se da por supuesto que tiene cierta experiencia previa con Python y sitios Web de Azure.

En este tutorial de base de datos se trata lo siguiente:

1. Crear y aprovisionar una cuenta de Cosmos DB.
2. Crear una aplicación Python Flask.
3. Conexión tooand con Cosmos DB desde la aplicación web.
4. Implementación de aplicación tooAzure de hello web.

Si sigue este tutorial, compilará una aplicación simple de votación que le permite toovote para un sondeo.

![Captura de pantalla de aplicación de votación de hello creada por este tutorial de base de datos](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Requisitos previos del tutorial de base de datos
Antes de seguir las instrucciones de hello en este artículo, debe asegurarse de que tiene instalado el siguiente hello:

* Una cuenta de Azure activa. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Para obtener más información, consulte [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    OR 

    Una instalación local de hello [emulador de base de datos de Azure Cosmos](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/)  
* [Herramientas de Python para Visual Studio](https://github.com/Microsoft/PTVS/)  
* [SDK de Microsoft Azure para Python 2.7](https://azure.microsoft.com/downloads/) 
* [Python 2.7.13](https://www.python.org/downloads/windows/) 

> [!IMPORTANT]
> Si va a instalar Python 2.7 para hello primera vez, asegúrese de que en la pantalla de bienvenida personalizar Python 2.7.13, selecciona **agregar python.exe tooPath**.
> 
> ![Captura de pantalla de pantalla de Python personalizar 2.7.11 de bienvenida, donde es necesario tooselect agregar python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Compilador de Microsoft Visual C++ 2013 para Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266)

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Paso 1: Creación de una cuenta de base de datos de Azure Cosmos DB
Para comenzar, creemos una cuenta de Cosmos DB. Si ya tiene una cuenta o si usas Hola emulador de base de datos de Azure Cosmos para este tutorial, puede omitir demasiado[paso 2: crear una nueva aplicación web de Python matraz](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Ahora se le indicará cómo toocreate una nueva aplicación web de Python matraz de hello masa.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Paso 2: Creación de una nueva aplicación web de Python Flask
1. En Visual Studio, en hello **archivo** menú, seleccione demasiado**New**y, a continuación, haga clic en **proyecto**.
   
    Hola **nuevo proyecto** aparece el cuadro de diálogo.
2. En el panel izquierdo de hello, expanda **plantillas** y, a continuación, **Python**y, a continuación, haga clic en **Web**. 
3. Seleccione **matraz Web proyecto** en el panel central de hello, luego, en hello **nombre** cuadro, escriba **tutorial**y, a continuación, haga clic en **Aceptar**. Recuerde que los nombres de paquete de Python deben ser en minúsculas, como se describe en hello [Guía de estilo para el código de Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Para esos tooPython nueva matraz, es un marco de desarrollo de aplicaciones web que permite crear aplicaciones web de Python con mayor rapidez.
   
    ![Captura de pantalla de ventana de hello nuevo proyecto en Visual Studio con Python resaltado en hello dejado, Python matraz Web proyecto seleccionado en medio de Hola y tutorial de nombre de hello en el cuadro de nombre de Hola](./media/documentdb-python-application/image9.png)
4. Hola **Python Tools para Visual Studio** ventana, haga clic en **instalar en un entorno virtual**. 
   
    ![Captura de pantalla de tutorial de base de datos de hello - Python Tools para la ventana de Visual Studio](./media/documentdb-python-application/python-install-virtual-environment.png)
5. Hola **agregar entorno Virtual** ventana, puede aceptar los valores predeterminados de Hola y usar Python 2.7 como entorno de base de hello porque PyDocumentDB no admite actualmente Python 3.x y, a continuación, haga clic en **crear**. Esto configura el entorno virtual de Python Hola necesario para el proyecto.
   
    ![Captura de pantalla de tutorial de base de datos de hello - Python Tools para la ventana de Visual Studio](./media/documentdb-python-application/image10_A.png)
   
    muestra de la ventana de salida de Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` cuando se instala correctamente el entorno de Hola.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Paso 3: Modificar la aplicación web de hello matraz de Python
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Agregar proyecto de tooyour de paquetes de saludo matraz de Python
Después de configurar el proyecto, deberá tooadd Hola necesario matraz paquetes tooyour proyecto, incluida la pydocumentdb, paquete de Python Hola de documentos.

1. En el Explorador de soluciones, abra el archivo de hello denominado **requirements.txt** y reemplace el contenido de hello con siguiente hello:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Guardar hello **requirements.txt** archivo. 
3. En el Explorador de soluciones, haga clic con el botón derecho en **env** y haga clic en **Install from requirements.txt**.
   
    ![Captura de pantalla que muestra env (Python 2.7) seleccionado con la instalación de requirements.txt resaltado en la lista de Hola](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Después de la instalación correcta, la ventana de salida de hello muestra siguiente hello:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > En raras ocasiones, podría ver un error en la ventana de salida de hello. Si esto ocurre, comprobar si el error de hello es toocleanup relacionado. A veces se produce un error en la limpieza de hello, pero la instalación Hola aún será correcto (desplazarse hacia arriba en tooverify de ventana de salida de hello esto). Puede comprobar la instalación por [entorno virtual de comprobación hello](#verify-the-virtual-environment). Si no se pudo instalar Hola pero Hola comprobación es correcta, es toocontinue Aceptar.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Comprobar el entorno virtual de Hola
Asegurémonos de que todo esté instalado correctamente.

1. Compile la solución de hello presionando **Ctrl**+**MAYÚS**+**B**.
2. Cuando se complete correctamente la compilación de hello, iniciar sitio Web de hello presionando **F5**. Esta acción inicia el servidor de desarrollo de hello matraz e inicia el explorador web. Debería ver Hola después de la página.
   
    ![Hola Python matraz proyecto web vacío desarrollo mostrado en un explorador](./media/documentdb-python-application/image12.png)
3. Detener la depuración de sitio Web de hello presionando **MAYÚS**+**F5** en Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Creación de definiciones de base de datos, colección y documento
Ahora vamos a crear la aplicación de votación mediante la adición de archivos nuevos y de la actualización de otros.

1. En el Explorador de soluciones, haga clic en hello **tutorial** proyecto de equipo y haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento**. Seleccione **vaciar el archivo Python** y archivo de nombre hello **forms.py**.  
2. Agregar Hola siguiente archivo de código toohello forms.py y, a continuación, guarde el archivo hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Agregar tooviews.py de importaciones de hello necesario
1. En el Explorador de soluciones, expanda hello **tutorial** carpeta y abra hello **views.py** archivo. 
2. Agregar Hola siguiendo las instrucciones de importación toohello parte superior de hello **views.py** de archivos, a continuación, guarde el archivo hello. Estos importación PythonSDK de Cosmos DB y Hola paquetes matraz.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Creación de base de datos, colección y documento
* Todavía en **views.py**, agregar Hola siguiente código toohello final de archivo hello. Esto se encarga de crear base de datos de hello utilizado por formulario Hola. No elimine ninguno de código existente de hello en **views.py**. Basta con anexar este extremo toohello.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Lectura de la base de datos, la colección y el documento, y envío del formulario
* Todavía en **views.py**, agregar Hola siguiente código toohello final de archivo hello. Esto se encarga de configurar la forma de hello, leer el documento, la recopilación y la base de datos de Hola. No elimine ninguno de código existente de hello en **views.py**. Basta con anexar este extremo toohello.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Crear Hola archivos HTML
1. En el Explorador de soluciones, en hello **tutorial** carpeta, derecho, haga clic en hello **plantillas** carpeta, haga clic en **agregar**y, a continuación, haga clic en **nuevo elemento**. 
2. Seleccione **página HTML**y, a continuación, en hello cuadro Nombre, escriba **create.html**. 
3. Repita los pasos 1 y 2 toocreate dos otros HTML archivos: results.html y vote.html.
4. Agregar Hola sigue código demasiado**create.html** en hello `<body>` elemento. Se muestra un mensaje que indica que hemos creado una nueva base de datos, colección y documento.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Agregar Hola sigue código demasiado**results.html** en hello `<body`> elemento. Muestra los resultados de Hola de sondeo de Hola.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Agregar Hola sigue código demasiado**vote.html** en hello `<body`> elemento. Muestra el sondeo de Hola y acepta Hola votos. Sobre cómo registrar los votos de hello, el control de hello pasa a través de tooviews.py donde se reconocerá Hola voto conversión y anexar documento hello en consecuencia.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. Hola **plantillas** carpeta, contenido de Hola de reemplazo de **index.html** con siguiente Hola. Esto sirve como Hola página para la aplicación de destino.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Agregue un archivo de configuración y cambie hello \_ \_init\_\_.py
1. En el Explorador de soluciones, haga clic en hello **tutorial** proyecto de equipo y haga clic en **agregar**, haga clic en **nuevo elemento**, seleccione **vaciar el archivo Python**y, a continuación, archivo de nombre hello **config.py**. Los formularios de Flask requieren este archivo de configuración. Puede usar tooprovide también una clave secreta. Sin embargo, dicha clave no es necesaria para este tutorial.
2. Agregue Hola siguiente tooconfig.py de código, necesitará los valores de hello tooalter de **documentos\_HOST** y **DOCUMENTDB\_clave** en el paso siguiente Hola.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. Hola [portal de Azure](https://portal.azure.com/), navegue toohello **claves** hoja haciendo clic en **examinar**, **cuentas de base de datos de Azure Cosmos**, haga doble clic en el nombre de Hola Hola toouse de la cuenta y, a continuación, haga clic en hello **claves** botón en hello **Essentials** área. Hola **claves** hoja, Hola copia **URI** valor y pegarlo en hello **config.py** archivo, como valor de Hola de hello **documentos\_HOST**  propiedad. 
4. En el portal de Azure, en Hola Hola **claves** hoja, copiar el valor de Hola de hello **Primary Key** o hello **clave secundaria**y péguela en hello **config.py**  archivo, como valor de Hola de hello **DOCUMENTDB\_clave** propiedad.
5. Hola  **\_ \_init\_\_.py** , agregue Hola después de línea. 
   
        app.config.from_object('config')
   
    Para que el contenido de hello del archivo hello es:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Después de agregar todos los archivos de hello, el Explorador de soluciones debe ser similar al siguiente:
   
    ![Captura de pantalla de ventana de Visual Studio Solution Explorer hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Paso 4: Ejecución local de la aplicación web
1. Compile la solución de hello presionando **Ctrl**+**MAYÚS**+**B**.
2. Cuando se complete correctamente la compilación de hello, iniciar sitio Web de hello presionando **F5**. Debería ver siguiente de hello en la pantalla.
   
    ![Captura de pantalla de Hola Python + Azure Cosmos DB votos de aplicación que se muestra en un explorador web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Haga clic en **crear o borrar Hola votos de base de datos** base de datos de toogenerate Hola.
   
    ![Captura de pantalla de Hola Crear página de aplicación web de hello: detalles sobre el desarrollo](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. A continuación, haga clic en **Vote** (Votar) y seleccione su opción.
   
    ![Captura de pantalla de aplicación web de hello con una pregunta de votación que supone](./media/documentdb-python-application/cosmos-db-vote.png)
5. Para cada voto que convierte, incrementa el contador adecuado de Hola.
   
    ![Captura de pantalla de resultados de página de voto Hola que se muestra de Hola](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Detenga la depuración de proyectos de hello presionando MAYÚS+F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Paso 5: Implementar tooAzure de aplicación web de Hola
Ahora que tiene la aplicación completa Hola funciona correctamente en la base de datos de Cosmos, vamos toodeploy esta tooAzure.

1. Menú contextual proyecto de hello en el Explorador de soluciones (asegúrese de que no está todavía ejecuta localmente) y seleccione **publicar**.  
   
     ![Captura de pantalla de tutorial de hello seleccionado en el Explorador de soluciones, con la opción de publicación de hello resaltado](./media/documentdb-python-application/image20.png)
2. Hola **publicar** cuadro de diálogo, seleccione **servicio de aplicaciones de Microsoft Azure**, seleccione **crear nuevo**y, a continuación, haga clic en **publicar**.
   
    ![Captura de pantalla de ventana de publicación Web de hello con el servicio de aplicación de Microsoft Azure resaltado](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. Hola **crear servicio en la aplicación** diálogo cuadro, escriba el nombre de hello para la aplicación web junto con su **suscripción**, **grupo de recursos**, y **Plan de servicio de aplicaciones** , a continuación, haga clic en **crear**.
   
    ![Captura de pantalla de ventana de la ventana de aplicaciones Web de Microsoft Azure de hello](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. En pocos segundos, Visual Studio terminará de publicar el servicio de aplicaciones y ejecutará un explorador donde podrá ver su trabajo ejecutándose en Azure.

    ![Captura de pantalla de ventana de la ventana de aplicaciones Web de Microsoft Azure de hello](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Solución de problemas
Si esta es la primera aplicación de Python hello haya ejecutado en el equipo, asegúrese de que siguiente de hello carpetas (o ubicaciones de instalación equivalente de Hola) se incluyen en la variable de ruta de acceso:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Si recibe un error en la página de voto y dio el nombre del proyecto algo distinto de **tutorial**, asegúrese de que  **\_ \_init\_\_.py** referencias Hola nombre correcto del proyecto en línea hello: `import tutorial.view`.

## <a name="next-steps"></a>Pasos siguientes
¡Enhorabuena! Acaba de completar su primera aplicación web de Python mediante DB Cosmos y haberlo publicado tooAzure.

Actualizamos y mejoramos este tema con frecuencia en función de los comentarios que recibimos.  Una vez se ha completado el tutorial de hello, póngase con hello votos botones en hello superior e inferior de esta página y estar seguro tooinclude sus comentarios acerca de qué mejoras que desee toosee realizado. Si desea que nos toocontact directamente, cree libre tooinclude dirección de su correo electrónico en sus comentarios.

aplicación de web tooyour tooadd funcionalidad adicional, revisión Hola API disponibles en hello [SDK de Azure Cosmos DB Python](documentdb-sdk-python.md).

Para obtener más información acerca de Azure, Visual Studio y Python, vea hello [Centro para desarrolladores de Python](https://azure.microsoft.com/develop/python/). 

Para ver los tutoriales Python matraz adicionales, consulte [Hola matraz Mega-Tutorial, parte I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
