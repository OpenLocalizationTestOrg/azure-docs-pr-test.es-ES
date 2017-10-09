---
title: "enlace de tabla externa de las funciones de aaaAzure (versión preliminar) | Documentos de Microsoft"
description: Uso de enlaces de tablas externas en Azure Functions
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: bf19d7d377232edc91087d5f4110602bb82c67ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-table-binding-preview"></a>Enlaces de tablas externas de Azure Functions (versión preliminar)
Este artículo se muestra cómo toomanipulate datos tabulares en proveedores de SaaS (por ejemplo, Sharepoint, Dynamics) dentro de la función con enlaces integrados. Azure Functions admite enlaces de entrada y salida para tablas externas.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a>Conexiones de API

Enlaces de tabla aprovechan externo tooauthenticate de conexiones de API con los proveedores de SaaS 3rd. 

Al asignar un enlace puede crear una nueva conexión de API o usar una conexión de API existente dentro de hello mismo grupo de recursos

### <a name="supported-api-connections-tables"></a>Conexiones de API compatibles (tablas)

|Conector|Desencadenador|Entrada|Salida|
|:-----|:---:|:---:|:---:|
|[DB2](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||x|x
|[Dynamics 365 for Operations](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||x|x
|[Dynamics 365](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[Dynamics NAV](https://msdn.microsoft.com/library/gg481835.aspx)||x|x
|[Google Sheets](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||x|x
|[Informix](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||x|x
|[Dynamics 365 for Financials](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||x|x
|[MySQL](https://docs.microsoft.com/azure/store-php-create-mysql-database)||x|x
|[Oracle Database](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||x|x
|[Common Data Service](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||x|x
|[Salesforce](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||x|x
|[SharePoint](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||x|x
|[SQL Server](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||x|x
|[Teradata](http://www.teradata.com/products-and-services/azure/products/)||x|x
|UserVoice||x|x
|Zendesk||x|x


> [!NOTE]
> También se pueden utilizar conexiones de tablas externas en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).

### <a name="creating-an-api-connection-step-by-step"></a>Creación de conexión de API: paso a paso

1. Creación de una función > función personalizada ![Creación de una función personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)
1. Escenario `Experimental`  >  `ExternalTable-CSharp` plantilla > Creación de una nueva `External Table connection` 
 ![Elección de una plantilla d entrada de tabla](./media/functions-bindings-storage-table/create-template-table.jpg)
1. Elección del proveedor de SaaS > elección/creación de una conexión ![Configuración de la conexión de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)
1. Seleccione la conexión de API > Crear función hello ![crear función de tabla](./media/functions-bindings-storage-table/table-template-options.jpg)
1. Selección de `Integrate` > `External Table`
    1. Configurar Hola conexión toouse la tabla de destino. Esta configuración dependerá en gran parte de los proveedores de SaaS. Se señalan a continuación en [configuración del origen de datos](#datasourcesettings)
![Configurar tabla](./media/functions-bindings-storage-table/configure-API-connection.jpg)

## <a name="usage"></a>Uso

En este ejemplo se conecta con el nombre "Contacto" con Id., LastName y FirstName columnas de tabla de tooa. código de Hello enumera las entidades de contacto de Hola de tabla de Hola y Hola de registros de nombres y apellidos.

### <a name="bindings"></a>Enlaces
```json
{
  "bindings": [
    {
      "type": "manualTrigger",
      "direction": "in",
      "name": "input"
    },
    {
      "type": "apiHubTable",
      "direction": "in",
      "name": "table",
      "connection": "ConnectionAppSettingsKey",
      "dataSetName": "default",
      "tableName": "Contact",
      "entityId": "",
    }
  ],
  "disabled": false
}
```
`entityId` debe estar vacío para los enlaces de tabla.

`ConnectionAppSettingsKey`identifica la configuración de la aplicación hello que almacena la cadena de conexión de API de Hola. Hello configuración de la aplicación se crea automáticamente cuando se agrega una API conexión Hola integrar la interfaz de usuario.

Un conector tabular proporciona conjuntos de datos, y cada conjunto de datos contiene tablas. Hola Hola predeterminada del conjunto de datos se denomina "predeterminado". títulos de Hola para un conjunto de datos y una tabla en varios proveedores de SaaS se enumeran a continuación:

|Conector|Dataset|Tabla|
|:-----|:---|:---| 
|**SharePoint**|Sitio|Lista de SharePoint
|**SQL**|Base de datos|Tabla 
|**Hoja de cálculo de Google**|Hoja de cálculo|Hoja de cálculo 
|**Excel**|Archivo de Excel|Hoja 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a>Uso en C# #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound toohello incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in hello source table
    ContinuationToken continuationToken = null;
    do
    {   
        //retreive table values
        var contactsSegment = await table.ListEntitiesAsync(
            continuationToken: continuationToken);

        foreach (var contact in contactsSegment.Items)
        {   
            log.Info(string.Format("{0} {1}", contact.FirstName, contact.LastName));
        }

        continuationToken = contactsSegment.ContinuationToken;
    }
    while (continuationToken != null);
}
```

<!--
<a name="innodejs"></a>

### Usage in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```
-->
<a name="datasourcesettings"></a>
## Configuración de origen de datos

### <a name="sql-server"></a>SQL Server

Hola toocreate de secuencia de comandos y rellenar tabla Contact de hello está por debajo. dataSetName es el "valor predeterminado".

```sql
CREATE TABLE Contact
(
    Id int NOT NULL,
    LastName varchar(20) NOT NULL,
    FirstName varchar(20) NOT NULL,
    CONSTRAINT PK_Contact_Id PRIMARY KEY (Id)
)
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (1, 'Bitt', 'Prad') 
GO
INSERT INTO Contact(Id, LastName, FirstName)
     VALUES (2, 'Glooney', 'Ceorge') 
GO
```

### <a name="google-sheets"></a>Hojas de cálculo de Google
En Google Docs, cree una hoja de cálculo con una hoja de cálculo denominada `Contact`. Conector de Hello no puede usar el nombre para mostrar hello hoja de cálculo. nombre interno de Hello (en negrita) necesita toobe usará como dataSetName, por ejemplo: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  agregar nombres de columna de hello `Id`, `LastName`, `FirstName` toohello primera fila, a continuación, rellenar los datos en filas siguientes.

### <a name="salesforce"></a>Salesforce
dataSetName es el "valor predeterminado".

## <a name="next-steps"></a>Pasos siguientes
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
