---
title: "aaaConnect tooAzure DB Cosmos mediante herramientas de análisis de BI | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse hello Azure Cosmos DB ODBC driver toocreate tablas y vistas para que los datos normalizados pueden verse en el software de análisis de BI y los datos."
keywords: odbc, controlador odbc
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 9967f4e5-4b71-4cd7-8324-221a8c789e6b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: e12a70f7805445f09fac01411e4bfbccc9a29c7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-cosmos-db-using-bi-analytics-tools-with-hello-odbc-driver"></a>Conectar tooAzure Cosmos DB con las herramientas de análisis de BI con el controlador ODBC de Hola

habilita el controlador Hello Azure Cosmos base de datos ODBC tooconnect tooAzure base de datos de Cosmos con análisis de BI herramientas como SQL Server Integration Services, Power BI Desktop y Tableau para que pueda analizar y crear visualizaciones de los datos de la base de datos de Azure Cosmos en aquellas soluciones.

controlador de ODBC de base de datos de Azure Cosmos Hello es ODBC 3.8 compatible y admite la sintaxis de ANSI SQL-92. Hola controlador ofrece características enriquecidas toohelp renormalize datos en la base de datos de Azure Cosmos. Controlador de Hola se pueden representar datos en la base de datos de Azure Cosmos como tablas y vistas. controlador de Hello permite las operaciones de SQL de tooperform en tablas de Hola y vistas incluidas Agrupar por las consultas, las inserciones, actualizaciones y eliminaciones.

## <a name="why-do-i-need-toonormalize-my-data"></a>¿Por qué necesito toonormalize Mis datos?
DB de Cosmos Azure es una base de datos schemaless, por lo que permite el desarrollo rápido de aplicaciones, habilitando las aplicaciones tooiterate sus datos de modelo en marcha de hello y no limitar tooa estricta del esquema. Una sola base de datos de Azure Cosmos DB puede contener documentos JSON de varias estructuras. Esto es ideal para el desarrollo rápido de aplicaciones, pero cuando desee tooanalyze y crear informes de los datos mediante el análisis de datos y herramientas de BI, datos de Hola a menudo necesita toobe una estructura jerárquica y cumplen tooa de esquema específico.

Esto es donde entra en juego el controlador ODBC de Hola. Utilizando el controlador ODBC de hello, puede ahora normalizarse datos en la base de datos de Azure Cosmos en tablas y vistas tooyour datos analíticos y de informes de conexión es necesario. esquemas de Hello normalizarse no tienen ningún impacto en los datos subyacentes de hello y no limitar a los desarrolladores tooadhere toothem, simplemente permiten tooleverage compatible con ODBC tooaccess Hola datos de las herramientas. Por tanto, la base de datos de Azure Cosmos DB no solo será ahora la favorita del equipo de desarrollo, sino que a los analistas de datos también les encantará.

Ahora permite empezar a trabajar con el controlador ODBC de Hola.

## <a id="install"></a>Paso 1: Instalar el controlador de ODBC de base de datos de Azure Cosmos Hola

1. Descargar controladores de Hola para su entorno:

    * [Microsoft Azure Cosmos DB ODBC 64-bit.msi](https://aka.ms/documentdb-odbc-64x64) para Windows de 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32x64-bit.msi](https://aka.ms/documentdb-odbc-32x64) para Windows de 32 bits en 64 bits
    * [Microsoft Azure Cosmos DB ODBC 32-bit.msi](https://aka.ms/documentdb-odbc-32x32) para Windows de 32 bits

    Hola ejecución msi archivo localmente, qué Hola inicia **Asistente de instalación del controlador de ODBC de Microsoft Azure Cosmos DB**. 
2. Complete el Asistente para la instalación Hola utilizando el controlador ODBC Hola de hello predeterminado tooinstall entrada.
3. Abra hello **Administrador de origen de datos ODBC** aplicación en el equipo, puede hacerlo escribir **orígenes de datos ODBC** cuadro de búsqueda de Windows hello. 
    Puede confirmar que se instaló el controlador de hello haciendo clic en hello **controladores** ficha y asegurarse de **controlador ODBC de Microsoft Azure Cosmos DB** aparece.

    ![Administrador de orígenes de datos ODBC de Azure Cosmos DB](./media/odbc-driver/odbc-driver.png)

## <a id="connect"></a>Paso 2: Conectar la base de datos de base de datos de Azure Cosmos tooyour

1. Después de [controlador de ODBC de base de datos de Azure Cosmos Hola instalar](#install), Hola **Administrador de orígenes de datos ODBC** ventana, haga clic en **agregar**. Puede crear un DSN de usuario o de sistema. En este ejemplo, vamos a crear un DSN de usuario.
2. Hola **Create New Data Source** ventana, seleccione **controlador ODBC de Microsoft Azure Cosmos DB**y, a continuación, haga clic en **finalizar**.
3. Hola **el programa de instalación de Azure Cosmos DB ODBC Driver SDN** ventana, rellene siguiente hello: 

    ![Ventana Azure Cosmos DB ODBC Driver DSN Setup (Configuración de DSN del controlador ODBC de Azure Cosmos DB)](./media/odbc-driver/odbc-driver-dsn-setup.png)
    - **Nombre del origen de datos**: su propio nombre descriptivo para hello DSN de ODBC. Este nombre es la cuenta de base de datos de Azure Cosmos tooyour único, por lo que asígnele el nombre correctamente si tiene varias cuentas.
    - **Descripción**: una breve descripción del origen de datos de Hola.
    - **Host**: URI de la cuenta de Azure Cosmos DB. Puede recuperar de la hoja de claves de base de datos de Azure Cosmos Hola Hola portal de Azure, como se muestra en la siguiente captura de pantalla de Hola. 
    - **Clave de acceso**: Hola clave principal o secundaria, lectura y escritura o de sólo lectura de la hoja de claves de base de datos de Azure Cosmos Hola Hola portal de Azure como se muestra en la siguiente captura de pantalla de Hola. Se recomienda que usar clave de solo lectura de hello si Hola DSN se utiliza para procesamiento de datos de solo lectura y los informes.
    ![Hoja Claves de Azure Cosmos DB](./media/odbc-driver/odbc-driver-keys.png)
    - **Cifrar la clave de acceso de**: seleccione la mejor opción de hello en función de los usuarios de Hola de esta máquina. 
4. Haga clic en hello **prueba** toomake de botón que se pueda conectar la cuenta de base de datos de Azure Cosmos tooyour. 
5. Haga clic en **opciones avanzadas** y conjunto Hola siguientes valores:
    - **Consultar coherencia**: Hola seleccione [nivel de coherencia](consistency-levels.md) para las operaciones. valor predeterminado de Hello es sesión.
    - **Número de reintentos**: escriba Hola número de veces que una operación si no se completa la solicitud inicial de hello debido a la limitación de tooservice tooretry.
    - **Archivo de esquema**: dispone de varias opciones.
        - De forma predeterminada, dejando esta entrada tal cual (en blanco), controlador de hello examina Hola primera datos de la página para todos los esquemas de hello toodetermine de colecciones de cada colección. Esto se conoce como asignación de colección. Sin un archivo de esquema que se definen, el controlador de hello tiene tooperform Hola examen para cada sesión de controlador y podría dar lugar a un tiempo de una aplicación con hello DSN de inicio mayor. Se recomienda asociar siempre un archivo de esquema para un DSN.
        - Si ya tiene un archivo de esquema (posiblemente uno que creó mediante hello [Editor de esquemas](#schema-editor)), puede hacer clic en **examinar**, navegue tooyour archivo, haga clic en **guardar**y, a continuación, haga clic en **Aceptar**.
        - Si desea toocreate un nuevo esquema, haga clic en **Aceptar**y, a continuación, haga clic en **Editor de esquemas** en la ventana principal de Hola. A continuación, continuar toohello [Editor de esquemas](#schema-editor) información. Al crear el nuevo archivo de esquema hello, recuerde toogo atrás toohello **opciones avanzadas** archivo de esquema de ventana tooinclude Hola recién creado.

6. Una vez que se complete y cierre hello **el programa de instalación de Azure Cosmos DB ODBC Driver DSN** ventana, Hola nuevo DSN de usuario es agrega ficha DSN de usuario de toohello.

    ![Nuevo Azure Cosmos DB DSN de ODBC en la ficha DSN de usuario de Hola](./media/odbc-driver/odbc-driver-user-dsn.png)

## <a id="#collection-mapping"></a>Paso 3: Crear una definición de esquema mediante el método de asignación de la colección de Hola

Hay dos tipos de métodos de muestreo que puede usar: **asignación de colección** o **delimitadores de tabla**. Una sesión de muestreo puede utilizar ambos métodos de muestreo, pero cada colección solo puede usar un método de muestreo específico. pasos de Hello siguiente crea un esquema para los datos de Hola en una o varias recopilaciones mediante el método de asignación de la colección de Hola. Este método de muestreo recupera datos de hello en la página de Hola de una estructura de hello toodetermine de recopilación de datos de Hola. Lo transpone una tabla de tooa de colección en hello lado ODBC. Este método de muestreo es rápido y eficaz cuando los datos de hello en un conjunto homogéneos. Si una colección contiene heterogénea tipo de datos, se recomienda usar hello [delimitadores de la tabla de asignación de método](#table-mapping) ya que proporciona un método de muestreo más robusto estructuras de datos de hello toodetermine en colección Hola. 

1. Después de completar los pasos 1 a 4 en [base de datos de base de datos de Azure Cosmos de conectar tooyour](#connect), haga clic en **Editor de esquemas** en hello **el programa de instalación de Azure Cosmos DB ODBC Driver DSN** ventana.

    ![Botón de editor de esquema en la ventana de configuración de DSN del controlador de ODBC de Azure Cosmos DB hello](./media/odbc-driver/odbc-driver-schema-editor.png)
2. Hola **Editor de esquemas** ventana, haga clic en **crear nuevo**.
    Hola **generar esquema** ventana muestra todas las colecciones de Hola Hola cuenta de base de datos de Azure Cosmos. 
3. Seleccione uno o más toosample de colecciones y, a continuación, haga clic en **ejemplo**. 
4. Hola **la vista Diseño** se representan las tabulaciones, base de datos de hello, esquema y tabla. En la vista de tabla de hello, análisis de hello muestra conjunto Hola de propiedades asociadas con los nombres de columna de hello (nombre de SQL, nombre de origen, etcetera).
    Para cada columna, puede modificar el nombre de la columna SQL hello, tipo de SQL de hello, longitud SQL (si procede), escala (si procede), precisión (si procede) y acepta valores NULL.
    - Puede establecer **Ocultar columna** demasiado**true** si desea tooexclude esa columna de resultados de la consulta. Las columnas marcadas como Ocultar columna = true no se devuelven para la selección y proyección, aunque siguen formando parte del esquema de Hola. Por ejemplo, puede ocultar todas propiedades de sistema que necesita de base de datos de Azure Cosmos Hola comenzando por "_".
    - Hola **identificador** columna es Hola único campo que no se puede ocultar tal como se utiliza como clave principal de hello en esquema normalizado Hola. 
5. Cuando haya terminado de definir el esquema de hello, haga clic en **archivo** | **guardar**, navegar por el esquema de toohello directory toosave hello y, a continuación, haga clic en **guardar**.

    Si en hello futuro desea toouse este esquema con un DSN, abrir ventana de configuración DSN de controlador de ODBC de base de datos de Azure Cosmos hello (a través de Hola Administrador de orígenes de datos ODBC), haga clic en Opciones avanzadas y, a continuación, en el cuadro del archivo de esquema de hello, navegue toohello guardó esquema. Guardar un tooan del archivo de esquema DSN existente modifica datos de saludo DSN conexión tooscope toohello y estructura definida por el esquema.

## <a id="table-mapping"></a>Paso 4: Crear una definición de esquema utilizando los delimitadores de tabla Hola asignación (método)

Hay dos tipos de métodos de muestreo que puede usar: **asignación de colección** o **delimitadores de tabla**. Una sesión de muestreo puede utilizar ambos métodos de muestreo, pero cada colección solo puede usar un método de muestreo específico. 

Hello pasos siguientes crea un esquema para los datos de hello en una o varias recopilaciones con hello **tabla delimitadores** método de asignación. Se recomienda usar este método de muestreo cuando las colecciones contengan un tipo heterogéneo de datos. Puede usar este Hola de tooscope método de muestreo tooa conjunto de atributos y sus valores correspondientes. Por ejemplo, si un documento contiene una propiedad "Tipo", puede definir el ámbito de los valores de hello muestreo toohello de esta propiedad. resultado final de Hola de muestreo de hello sería un conjunto de tablas para cada uno de los valores de hello para el tipo especificado. Por ejemplo, Tipo = Vehículo generará una tabla de vehículos, mientras que Tipo = Plano generaría una tabla de planos.

1. Después de completar los pasos 1 a 4 en [base de datos de base de datos de Azure Cosmos de conectar tooyour](#connect), haga clic en **Editor de esquemas** en la ventana de configuración de DSN del controlador de ODBC de Azure Cosmos DB hello.
2. Hola **Editor de esquemas** ventana, haga clic en **crear nuevo**.
    Hola **generar esquema** ventana muestra todas las colecciones de Hola Hola cuenta de base de datos de Azure Cosmos. 
3. Seleccione una colección en hello **vista de ejemplo** ficha Hola **definición de asignación** columna para la recopilación de hello, haga clic en **editar**. A continuación, en hello **definición asignación** ventana, seleccione **delimitadores de tabla** método. A continuación, Hola siguientes:

    a. Hola **atributos** cuadro, escriba un nombre Hola de una propiedad de delimitador. Se trata de una propiedad en el documento que desee tooscope Hola muestreo, por ejemplo, City y presione ENTRAR. 

    b. Si sólo desea los valores de toocertain tooscope Hola muestreo para el atributo de Hola que acaba de escribir, seleccione el atributo de hello en el cuadro de selección de hello, a continuación, escriba un valor en hello **valor** cuadro, por ejemplo, Seattle y presione ENTRAR. Puede continuar tooadd varios valores para los atributos. Sólo tiene que comprobar que Hola correcto se selecciona el atributo al que se están escribiendo valores.

    Por ejemplo, si incluye un **atributos** valor de ciudad y desea toolimit tooonly de la tabla incluye las filas con un valor de ciudad de Nueva York y Dubai, tendría que escribir ciudad en el cuadro de atributos de hello y Nueva York y, a continuación, Dubai en hello  **Valores** cuadro.
4. Haga clic en **Aceptar**. 
5. Después de completar las definiciones de asignación de Hola para colecciones de hello desea toosample Hola **Editor de esquemas** ventana, haga clic en **ejemplo**.
     Para cada columna, puede modificar el nombre de la columna SQL hello, tipo de SQL de hello, longitud SQL (si procede), escala (si procede), precisión (si procede) y acepta valores NULL.
    - Puede establecer **Ocultar columna** demasiado**true** si desea tooexclude esa columna de resultados de la consulta. Las columnas marcadas como Ocultar columna = true no se devuelven para la selección y proyección, aunque siguen formando parte del esquema de Hola. Por ejemplo, puede ocultar todas las propiedades de sistema que necesita de base de datos de Azure Cosmos Hola comenzando por "_".
    - Hola **identificador** columna es Hola único campo que no se puede ocultar tal como se utiliza como clave principal de hello en esquema normalizado Hola. 
6. Cuando haya terminado de definir el esquema de hello, haga clic en **archivo** | **guardar**, navegar por el esquema de toohello directory toosave hello y, a continuación, haga clic en **guardar**.
7. Nuevo en hello **el programa de instalación de Azure Cosmos DB ODBC Driver DSN** ventana, haga clic en ** Opciones avanzadas **. A continuación, en hello **archivo de esquema** , navegue toohello Guardar archivo de esquema y haga clic en **Aceptar**. Haga clic en **Aceptar** nuevo toosave Hola DSN. Este esquema de hello guarda creaste toohello DSN. 

## <a name="optional-creating-views"></a>(Opcional) Creación de vistas
Puede definir y crear vistas como parte del proceso de muestreo de Hola. Estas vistas son tooSQL equivalente. Se trata de solo lectura y son selecciones de Hola de ámbito y las proyecciones de hello definido por la base de datos SQL de Azure Cosmos. 

toocreate una vista para los datos, de hello **Editor de esquemas** ventana, en hello **definiciones de vistas** columna, haga clic en **agregar** en fila Hola de hello colección toosample. A continuación, en hello **definiciones de vista** ventana, Hola siguientes:
1. Haga clic en **New**, escriba un nombre para la vista de hello, por ejemplo, EmployeesfromSeattleView y, a continuación, haga clic en **Aceptar**.
2. Hola **Editar vista** ventana, escriba una consulta de base de datos de Azure Cosmos. Debe tratarse de una consulta SQL de Azure Cosmos DB, por ejemplo`SELECT c.City, c.EmployeeName, c.Level, c.Age, c.Gender, c.Manager FROM c WHERE c.City = “Seattle”` y, luego, haga clic en **Aceptar**.

Puede crear tantas vistas como desee. Una vez que haya terminado de definir vistas de hello, se pueden, a continuación, datos de ejemplo Hola. 

## <a name="step-5-view-your-data-in-bi-tools-such-as-power-bi-desktop"></a>Paso 5: Visualización de los datos en herramientas de BI como Power BI Desktop

Puede usar la nueva tooconnect DSN DocumentADB con cualquier herramienta compatible con ODBC - este paso solo muestra cómo tooconnect tooPower BI Desktop y crear una visualización de Power BI.

1. Abra Power BI Desktop.
2. Haga clic en **Obtener datos**.
3. Hola **obtener datos** ventana, haga clic en **otros** | **ODBC** | **conectar**.
4. Hola **de ODBC** (ventana), nombre de origen de datos seleccione Hola que creó y, a continuación, haga clic en **Aceptar**. Puede dejar hello **opciones avanzadas** entradas en blanco.
5. Hola **acceso a un origen de datos mediante un controlador ODBC** ventana, seleccione **predeterminado o personalizado** y, a continuación, haga clic en **conectar**. No es necesario hello tooinclude **propiedades de la cadena de conexión de credencial**.
6. Hola **navegador** ventana, en el panel izquierdo de hello, expanda la base de datos de hello, esquema de Hola y Hola, a continuación, seleccione tabla. panel de resultados de Hello incluye datos de hello mediante el esquema de Hola que ha creado.
7. toovisualize Hola datos en Power BI desktop, casilla Hola delante del nombre de la tabla de hello y, a continuación, haga clic en **carga**.
8. En Power BI Desktop, Hola izquierda, seleccione ficha de datos de Hola ![Pestaña Datos en Power BI Desktop](./media/odbc-driver/odbc-driver-data-tab.png) tooconfirm que se importaron los datos.
9. Ahora puede crear objetos visuales con Power BI, haga clic en la ficha Informes de hello ![ficha informe en Power BI Desktop](./media/odbc-driver/odbc-driver-report-tab.png), haga clic en **nuevo Visual**y, a continuación, personalizar el icono. Para más información sobre cómo crear visualizaciones en Power BI Desktop, consulte [Tipos de visualización en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-visualization-types-for-reports-and-q-and-a/).

## <a name="troubleshooting"></a>Solución de problemas

Si recibe Hola tras error, asegúrese de hello **Host** y **clave de acceso** valores copió Hola portal de Azure en [paso 2](#connect) son correctos y, a continuación, vuelva a intentarlo. Usar Hola copia botones toohello derecha de hello **Host** y **clave de acceso** valores de hello toocopy portal Azure Hola valores errores.

    [HY000]: [Microsoft][Azure Cosmos DB] (401) HTTP 401 Authentication Error: {"code":"Unauthorized","message":"hello input authorization token can't serve hello request. Please check that hello expected payload is built as per hello protocol, and check hello key being used. Server used hello following payload toosign: 'get\ndbs\n\nfri, 20 jan 2017 03:43:55 gmt\n\n'\r\nActivityId: 9acb3c0d-cb31-4b78-ac0a-413c8d33e373"}`

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de la base de datos de Cosmos de Azure, consulte [¿qué es la base de datos de Azure Cosmos?](introduction.md).
