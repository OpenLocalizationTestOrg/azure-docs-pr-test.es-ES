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
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="97327-103">Enlaces de tablas externas de Azure Functions (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="97327-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="97327-104">Este artículo se muestra cómo toomanipulate datos tabulares en proveedores de SaaS (por ejemplo, Sharepoint, Dynamics) dentro de la función con enlaces integrados.</span><span class="sxs-lookup"><span data-stu-id="97327-104">This article shows how toomanipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="97327-105">Azure Functions admite enlaces de entrada y salida para tablas externas.</span><span class="sxs-lookup"><span data-stu-id="97327-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="97327-106">Conexiones de API</span><span class="sxs-lookup"><span data-stu-id="97327-106">API Connections</span></span>

<span data-ttu-id="97327-107">Enlaces de tabla aprovechan externo tooauthenticate de conexiones de API con los proveedores de SaaS 3rd.</span><span class="sxs-lookup"><span data-stu-id="97327-107">Table bindings leverage external API connections tooauthenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="97327-108">Al asignar un enlace puede crear una nueva conexión de API o usar una conexión de API existente dentro de hello mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="97327-108">When assigning a binding you can either create a new API connection or use an existing API connection within hello same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="97327-109">Conexiones de API compatibles (tablas)</span><span class="sxs-lookup"><span data-stu-id="97327-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="97327-110">Conector</span><span class="sxs-lookup"><span data-stu-id="97327-110">Connector</span></span>|<span data-ttu-id="97327-111">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="97327-111">Trigger</span></span>|<span data-ttu-id="97327-112">Entrada</span><span class="sxs-lookup"><span data-stu-id="97327-112">Input</span></span>|<span data-ttu-id="97327-113">Salida</span><span class="sxs-lookup"><span data-stu-id="97327-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="97327-114">DB2</span><span class="sxs-lookup"><span data-stu-id="97327-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="97327-115">x</span><span class="sxs-lookup"><span data-stu-id="97327-115">x</span></span>|<span data-ttu-id="97327-116">x</span><span class="sxs-lookup"><span data-stu-id="97327-116">x</span></span>
|[<span data-ttu-id="97327-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="97327-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="97327-118">x</span><span class="sxs-lookup"><span data-stu-id="97327-118">x</span></span>|<span data-ttu-id="97327-119">x</span><span class="sxs-lookup"><span data-stu-id="97327-119">x</span></span>
|[<span data-ttu-id="97327-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="97327-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="97327-121">x</span><span class="sxs-lookup"><span data-stu-id="97327-121">x</span></span>|<span data-ttu-id="97327-122">x</span><span class="sxs-lookup"><span data-stu-id="97327-122">x</span></span>
|[<span data-ttu-id="97327-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="97327-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="97327-124">x</span><span class="sxs-lookup"><span data-stu-id="97327-124">x</span></span>|<span data-ttu-id="97327-125">x</span><span class="sxs-lookup"><span data-stu-id="97327-125">x</span></span>
|[<span data-ttu-id="97327-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="97327-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="97327-127">x</span><span class="sxs-lookup"><span data-stu-id="97327-127">x</span></span>|<span data-ttu-id="97327-128">x</span><span class="sxs-lookup"><span data-stu-id="97327-128">x</span></span>
|[<span data-ttu-id="97327-129">Informix</span><span class="sxs-lookup"><span data-stu-id="97327-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="97327-130">x</span><span class="sxs-lookup"><span data-stu-id="97327-130">x</span></span>|<span data-ttu-id="97327-131">x</span><span class="sxs-lookup"><span data-stu-id="97327-131">x</span></span>
|[<span data-ttu-id="97327-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="97327-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="97327-133">x</span><span class="sxs-lookup"><span data-stu-id="97327-133">x</span></span>|<span data-ttu-id="97327-134">x</span><span class="sxs-lookup"><span data-stu-id="97327-134">x</span></span>
|[<span data-ttu-id="97327-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="97327-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="97327-136">x</span><span class="sxs-lookup"><span data-stu-id="97327-136">x</span></span>|<span data-ttu-id="97327-137">x</span><span class="sxs-lookup"><span data-stu-id="97327-137">x</span></span>
|[<span data-ttu-id="97327-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="97327-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="97327-139">x</span><span class="sxs-lookup"><span data-stu-id="97327-139">x</span></span>|<span data-ttu-id="97327-140">x</span><span class="sxs-lookup"><span data-stu-id="97327-140">x</span></span>
|[<span data-ttu-id="97327-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="97327-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="97327-142">x</span><span class="sxs-lookup"><span data-stu-id="97327-142">x</span></span>|<span data-ttu-id="97327-143">x</span><span class="sxs-lookup"><span data-stu-id="97327-143">x</span></span>
|[<span data-ttu-id="97327-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="97327-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="97327-145">x</span><span class="sxs-lookup"><span data-stu-id="97327-145">x</span></span>|<span data-ttu-id="97327-146">x</span><span class="sxs-lookup"><span data-stu-id="97327-146">x</span></span>
|[<span data-ttu-id="97327-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="97327-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="97327-148">x</span><span class="sxs-lookup"><span data-stu-id="97327-148">x</span></span>|<span data-ttu-id="97327-149">x</span><span class="sxs-lookup"><span data-stu-id="97327-149">x</span></span>
|[<span data-ttu-id="97327-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="97327-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="97327-151">x</span><span class="sxs-lookup"><span data-stu-id="97327-151">x</span></span>|<span data-ttu-id="97327-152">x</span><span class="sxs-lookup"><span data-stu-id="97327-152">x</span></span>
|[<span data-ttu-id="97327-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="97327-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="97327-154">x</span><span class="sxs-lookup"><span data-stu-id="97327-154">x</span></span>|<span data-ttu-id="97327-155">x</span><span class="sxs-lookup"><span data-stu-id="97327-155">x</span></span>
|<span data-ttu-id="97327-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="97327-156">UserVoice</span></span>||<span data-ttu-id="97327-157">x</span><span class="sxs-lookup"><span data-stu-id="97327-157">x</span></span>|<span data-ttu-id="97327-158">x</span><span class="sxs-lookup"><span data-stu-id="97327-158">x</span></span>
|<span data-ttu-id="97327-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="97327-159">Zendesk</span></span>||<span data-ttu-id="97327-160">x</span><span class="sxs-lookup"><span data-stu-id="97327-160">x</span></span>|<span data-ttu-id="97327-161">x</span><span class="sxs-lookup"><span data-stu-id="97327-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="97327-162">También se pueden utilizar conexiones de tablas externas en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="97327-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="97327-163">Creación de conexión de API: paso a paso</span><span class="sxs-lookup"><span data-stu-id="97327-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="97327-164">Creación de una función > función personalizada ![Creación de una función personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="97327-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="97327-165">Escenario `Experimental`  >  `ExternalTable-CSharp` plantilla > Creación de una nueva `External Table connection` 
 ![Elección de una plantilla d entrada de tabla](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="97327-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="97327-166">Elección del proveedor de SaaS > elección/creación de una conexión ![Configuración de la conexión de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="97327-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="97327-167">Seleccione la conexión de API > Crear función hello ![crear función de tabla](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="97327-167">Select your API connection > create hello function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="97327-168">Selección de `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="97327-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="97327-169">Configurar Hola conexión toouse la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="97327-169">Configure hello connection toouse your target table.</span></span> <span data-ttu-id="97327-170">Esta configuración dependerá en gran parte de los proveedores de SaaS.</span><span class="sxs-lookup"><span data-stu-id="97327-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="97327-171">Se señalan a continuación en [configuración del origen de datos](#datasourcesettings)
![Configurar tabla](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="97327-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="97327-172">Uso</span><span class="sxs-lookup"><span data-stu-id="97327-172">Usage</span></span>

<span data-ttu-id="97327-173">En este ejemplo se conecta con el nombre "Contacto" con Id., LastName y FirstName columnas de tabla de tooa.</span><span class="sxs-lookup"><span data-stu-id="97327-173">This example connects tooa table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="97327-174">código de Hello enumera las entidades de contacto de Hola de tabla de Hola y Hola de registros de nombres y apellidos.</span><span class="sxs-lookup"><span data-stu-id="97327-174">hello code lists hello Contact entities in hello table and logs hello first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="97327-175">Enlaces</span><span class="sxs-lookup"><span data-stu-id="97327-175">Bindings</span></span>
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
<span data-ttu-id="97327-176">`entityId` debe estar vacío para los enlaces de tabla.</span><span class="sxs-lookup"><span data-stu-id="97327-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="97327-177">`ConnectionAppSettingsKey`identifica la configuración de la aplicación hello que almacena la cadena de conexión de API de Hola.</span><span class="sxs-lookup"><span data-stu-id="97327-177">`ConnectionAppSettingsKey` identifies hello app setting that stores hello API connection string.</span></span> <span data-ttu-id="97327-178">Hello configuración de la aplicación se crea automáticamente cuando se agrega una API conexión Hola integrar la interfaz de usuario.</span><span class="sxs-lookup"><span data-stu-id="97327-178">hello app setting is created automatically when you add an API connection in hello integrate UI.</span></span>

<span data-ttu-id="97327-179">Un conector tabular proporciona conjuntos de datos, y cada conjunto de datos contiene tablas.</span><span class="sxs-lookup"><span data-stu-id="97327-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="97327-180">Hola Hola predeterminada del conjunto de datos se denomina "predeterminado".</span><span class="sxs-lookup"><span data-stu-id="97327-180">hello name of hello default data set is “default.”</span></span> <span data-ttu-id="97327-181">títulos de Hola para un conjunto de datos y una tabla en varios proveedores de SaaS se enumeran a continuación:</span><span class="sxs-lookup"><span data-stu-id="97327-181">hello titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="97327-182">Conector</span><span class="sxs-lookup"><span data-stu-id="97327-182">Connector</span></span>|<span data-ttu-id="97327-183">Dataset</span><span class="sxs-lookup"><span data-stu-id="97327-183">Dataset</span></span>|<span data-ttu-id="97327-184">Tabla</span><span class="sxs-lookup"><span data-stu-id="97327-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="97327-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="97327-185">**SharePoint**</span></span>|<span data-ttu-id="97327-186">Sitio</span><span class="sxs-lookup"><span data-stu-id="97327-186">Site</span></span>|<span data-ttu-id="97327-187">Lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="97327-187">SharePoint List</span></span>
|<span data-ttu-id="97327-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="97327-188">**SQL**</span></span>|<span data-ttu-id="97327-189">Base de datos</span><span class="sxs-lookup"><span data-stu-id="97327-189">Database</span></span>|<span data-ttu-id="97327-190">Tabla</span><span class="sxs-lookup"><span data-stu-id="97327-190">Table</span></span> 
|<span data-ttu-id="97327-191">**Hoja de cálculo de Google**</span><span class="sxs-lookup"><span data-stu-id="97327-191">**Google Sheet**</span></span>|<span data-ttu-id="97327-192">Hoja de cálculo</span><span class="sxs-lookup"><span data-stu-id="97327-192">Spreadsheet</span></span>|<span data-ttu-id="97327-193">Hoja de cálculo</span><span class="sxs-lookup"><span data-stu-id="97327-193">Worksheet</span></span> 
|<span data-ttu-id="97327-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="97327-194">**Excel**</span></span>|<span data-ttu-id="97327-195">Archivo de Excel</span><span class="sxs-lookup"><span data-stu-id="97327-195">Excel file</span></span>|<span data-ttu-id="97327-196">Hoja</span><span class="sxs-lookup"><span data-stu-id="97327-196">Sheet</span></span> 

<!--
See hello language-specific sample that copies hello input file toohello output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="97327-197">Uso en C#</span><span class="sxs-lookup"><span data-stu-id="97327-197">Usage in C#</span></span> #

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

<span data-ttu-id="97327-198"><!--
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
## Configuración de origen de datos</span><span class="sxs-lookup"><span data-stu-id="97327-198"><!--
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
## Data Source Settings</span></span>

### <a name="sql-server"></a><span data-ttu-id="97327-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="97327-199">SQL Server</span></span>

<span data-ttu-id="97327-200">Hola toocreate de secuencia de comandos y rellenar tabla Contact de hello está por debajo.</span><span class="sxs-lookup"><span data-stu-id="97327-200">hello script toocreate and populate hello Contact table is below.</span></span> <span data-ttu-id="97327-201">dataSetName es el "valor predeterminado".</span><span class="sxs-lookup"><span data-stu-id="97327-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="97327-202">Hojas de cálculo de Google</span><span class="sxs-lookup"><span data-stu-id="97327-202">Google Sheets</span></span>
<span data-ttu-id="97327-203">En Google Docs, cree una hoja de cálculo con una hoja de cálculo denominada `Contact`.</span><span class="sxs-lookup"><span data-stu-id="97327-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="97327-204">Conector de Hello no puede usar el nombre para mostrar hello hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="97327-204">hello connector cannot use hello spreadsheet display name.</span></span> <span data-ttu-id="97327-205">nombre interno de Hello (en negrita) necesita toobe usará como dataSetName, por ejemplo: `docs.google.com/spreadsheets/d/`  **`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`**  agregar nombres de columna de hello `Id`, `LastName`, `FirstName` toohello primera fila, a continuación, rellenar los datos en filas siguientes.</span><span class="sxs-lookup"><span data-stu-id="97327-205">hello internal name (in bold) needs toobe used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add hello column names `Id`, `LastName`, `FirstName` toohello first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="97327-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="97327-206">Salesforce</span></span>
<span data-ttu-id="97327-207">dataSetName es el "valor predeterminado".</span><span class="sxs-lookup"><span data-stu-id="97327-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="97327-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="97327-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
