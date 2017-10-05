---
title: "Enlaces de tablas externas de Azure Functions (versión preliminar) | Microsoft Docs"
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
ms.openlocfilehash: 716438e5ea490f6716999813112305499dbe61a8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-external-table-binding-preview"></a><span data-ttu-id="2d1b9-103">Enlaces de tablas externas de Azure Functions (versión preliminar)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-103">Azure Functions External Table binding (Preview)</span></span>
<span data-ttu-id="2d1b9-104">Este artículo muestra cómo manipular los datos tabulares de proveedores de SaaS (por ejemplo, Sharepoint y Dynamics) dentro de la función con enlaces integrados.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-104">This article shows how to manipulate tabular data on SaaS providers (e.g. Sharepoint, Dynamics) within your function with built-in bindings.</span></span> <span data-ttu-id="2d1b9-105">Azure Functions admite enlaces de entrada y salida para tablas externas.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-105">Azure Functions supports input, and output bindings for external tables.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="api-connections"></a><span data-ttu-id="2d1b9-106">Conexiones de API</span><span class="sxs-lookup"><span data-stu-id="2d1b9-106">API Connections</span></span>

<span data-ttu-id="2d1b9-107">Los enlaces de tabla aprovechan las conexiones externas de API para autenticarse con proveedores de SaaS de terceros.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-107">Table bindings leverage external API connections to authenticate with 3rd party SaaS providers.</span></span> 

<span data-ttu-id="2d1b9-108">Al asignar un enlace, puede crear una nueva conexión de API o usar una conexión de API existente dentro del mismo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2d1b9-108">When assigning a binding you can either create a new API connection or use an existing API connection within the same resource group</span></span>

### <a name="supported-api-connections-tables"></a><span data-ttu-id="2d1b9-109">Conexiones de API compatibles (tablas)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-109">Supported API Connections (Table)s</span></span>

|<span data-ttu-id="2d1b9-110">Conector</span><span class="sxs-lookup"><span data-stu-id="2d1b9-110">Connector</span></span>|<span data-ttu-id="2d1b9-111">Desencadenador</span><span class="sxs-lookup"><span data-stu-id="2d1b9-111">Trigger</span></span>|<span data-ttu-id="2d1b9-112">Entrada</span><span class="sxs-lookup"><span data-stu-id="2d1b9-112">Input</span></span>|<span data-ttu-id="2d1b9-113">Salida</span><span class="sxs-lookup"><span data-stu-id="2d1b9-113">Output</span></span>|
|:-----|:---:|:---:|:---:|
|[<span data-ttu-id="2d1b9-114">DB2</span><span class="sxs-lookup"><span data-stu-id="2d1b9-114">DB2</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-db2)||<span data-ttu-id="2d1b9-115">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-115">x</span></span>|<span data-ttu-id="2d1b9-116">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-116">x</span></span>
|[<span data-ttu-id="2d1b9-117">Dynamics 365 for Operations</span><span class="sxs-lookup"><span data-stu-id="2d1b9-117">Dynamics 365 for Operations</span></span>](https://ax.help.dynamics.com/wiki/install-and-configure-dynamics-365-for-operations-warehousing/)||<span data-ttu-id="2d1b9-118">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-118">x</span></span>|<span data-ttu-id="2d1b9-119">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-119">x</span></span>
|[<span data-ttu-id="2d1b9-120">Dynamics 365</span><span class="sxs-lookup"><span data-stu-id="2d1b9-120">Dynamics 365</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="2d1b9-121">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-121">x</span></span>|<span data-ttu-id="2d1b9-122">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-122">x</span></span>
|[<span data-ttu-id="2d1b9-123">Dynamics NAV</span><span class="sxs-lookup"><span data-stu-id="2d1b9-123">Dynamics NAV</span></span>](https://msdn.microsoft.com/library/gg481835.aspx)||<span data-ttu-id="2d1b9-124">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-124">x</span></span>|<span data-ttu-id="2d1b9-125">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-125">x</span></span>
|[<span data-ttu-id="2d1b9-126">Google Sheets</span><span class="sxs-lookup"><span data-stu-id="2d1b9-126">Google Sheets</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-googledrive)||<span data-ttu-id="2d1b9-127">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-127">x</span></span>|<span data-ttu-id="2d1b9-128">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-128">x</span></span>
|[<span data-ttu-id="2d1b9-129">Informix</span><span class="sxs-lookup"><span data-stu-id="2d1b9-129">Informix</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-informix)||<span data-ttu-id="2d1b9-130">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-130">x</span></span>|<span data-ttu-id="2d1b9-131">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-131">x</span></span>
|[<span data-ttu-id="2d1b9-132">Dynamics 365 for Financials</span><span class="sxs-lookup"><span data-stu-id="2d1b9-132">Dynamics 365 for Financials</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-crmonline)||<span data-ttu-id="2d1b9-133">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-133">x</span></span>|<span data-ttu-id="2d1b9-134">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-134">x</span></span>
|[<span data-ttu-id="2d1b9-135">MySQL</span><span class="sxs-lookup"><span data-stu-id="2d1b9-135">MySQL</span></span>](https://docs.microsoft.com/azure/store-php-create-mysql-database)||<span data-ttu-id="2d1b9-136">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-136">x</span></span>|<span data-ttu-id="2d1b9-137">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-137">x</span></span>
|[<span data-ttu-id="2d1b9-138">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="2d1b9-138">Oracle Database</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-oracledatabase)||<span data-ttu-id="2d1b9-139">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-139">x</span></span>|<span data-ttu-id="2d1b9-140">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-140">x</span></span>
|[<span data-ttu-id="2d1b9-141">Common Data Service</span><span class="sxs-lookup"><span data-stu-id="2d1b9-141">Common Data Service</span></span>](https://docs.microsoft.com/common-data-service/entity-reference/introduction)||<span data-ttu-id="2d1b9-142">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-142">x</span></span>|<span data-ttu-id="2d1b9-143">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-143">x</span></span>
|[<span data-ttu-id="2d1b9-144">Salesforce</span><span class="sxs-lookup"><span data-stu-id="2d1b9-144">Salesforce</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-salesforce)||<span data-ttu-id="2d1b9-145">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-145">x</span></span>|<span data-ttu-id="2d1b9-146">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-146">x</span></span>
|[<span data-ttu-id="2d1b9-147">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d1b9-147">SharePoint</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sharepointonline)||<span data-ttu-id="2d1b9-148">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-148">x</span></span>|<span data-ttu-id="2d1b9-149">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-149">x</span></span>
|[<span data-ttu-id="2d1b9-150">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2d1b9-150">SQL Server</span></span>](https://docs.microsoft.com/azure/connectors/connectors-create-api-sqlazure)||<span data-ttu-id="2d1b9-151">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-151">x</span></span>|<span data-ttu-id="2d1b9-152">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-152">x</span></span>
|[<span data-ttu-id="2d1b9-153">Teradata</span><span class="sxs-lookup"><span data-stu-id="2d1b9-153">Teradata</span></span>](http://www.teradata.com/products-and-services/azure/products/)||<span data-ttu-id="2d1b9-154">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-154">x</span></span>|<span data-ttu-id="2d1b9-155">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-155">x</span></span>
|<span data-ttu-id="2d1b9-156">UserVoice</span><span class="sxs-lookup"><span data-stu-id="2d1b9-156">UserVoice</span></span>||<span data-ttu-id="2d1b9-157">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-157">x</span></span>|<span data-ttu-id="2d1b9-158">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-158">x</span></span>
|<span data-ttu-id="2d1b9-159">Zendesk</span><span class="sxs-lookup"><span data-stu-id="2d1b9-159">Zendesk</span></span>||<span data-ttu-id="2d1b9-160">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-160">x</span></span>|<span data-ttu-id="2d1b9-161">x</span><span class="sxs-lookup"><span data-stu-id="2d1b9-161">x</span></span>


> [!NOTE]
> <span data-ttu-id="2d1b9-162">También se pueden utilizar conexiones de tablas externas en [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="2d1b9-162">External Table connections can also be used in [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)</span></span>

### <a name="creating-an-api-connection-step-by-step"></a><span data-ttu-id="2d1b9-163">Creación de conexión de API: paso a paso</span><span class="sxs-lookup"><span data-stu-id="2d1b9-163">Creating an API connection: step by step</span></span>

1. <span data-ttu-id="2d1b9-164">Creación de una función > función personalizada ![Creación de una función personalizada](./media/functions-bindings-storage-table/create-custom-function.jpg)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-164">Create a function > custom function ![Create a custom function](./media/functions-bindings-storage-table/create-custom-function.jpg)</span></span>
1. <span data-ttu-id="2d1b9-165">Escenario `Experimental`  >  `ExternalTable-CSharp` plantilla > Creación de una nueva `External Table connection` 
 ![Elección de una plantilla d entrada de tabla](./media/functions-bindings-storage-table/create-template-table.jpg)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-165">Scenario `Experimental` > `ExternalTable-CSharp` template > Create a new `External Table connection`
![Choose table input template](./media/functions-bindings-storage-table/create-template-table.jpg)</span></span>
1. <span data-ttu-id="2d1b9-166">Elección del proveedor de SaaS > elección/creación de una conexión ![Configuración de la conexión de SaaS](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-166">Choose your SaaS provider > choose/create a connection ![Configure SaaS connection](./media/functions-bindings-storage-table/authorize-API-connection.jpg)</span></span>
1. <span data-ttu-id="2d1b9-167">Selección de la conexión de API > creación de la función ![Creación de la función de tabla](./media/functions-bindings-storage-table/table-template-options.jpg)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-167">Select your API connection > create the function ![Create table function](./media/functions-bindings-storage-table/table-template-options.jpg)</span></span>
1. <span data-ttu-id="2d1b9-168">Selección de `Integrate` > `External Table`</span><span class="sxs-lookup"><span data-stu-id="2d1b9-168">Select `Integrate` > `External Table`</span></span>
    1. <span data-ttu-id="2d1b9-169">Configure la conexión para utilizar la tabla de destino.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-169">Configure the connection to use your target table.</span></span> <span data-ttu-id="2d1b9-170">Esta configuración dependerá en gran parte de los proveedores de SaaS.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-170">These settings will very between SaaS providers.</span></span> <span data-ttu-id="2d1b9-171">Se señalan a continuación en [configuración del origen de datos](#datasourcesettings)
![Configurar tabla](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span><span class="sxs-lookup"><span data-stu-id="2d1b9-171">They are outline below in [data source settings](#datasourcesettings)
![Configure table](./media/functions-bindings-storage-table/configure-API-connection.jpg)</span></span>

## <a name="usage"></a><span data-ttu-id="2d1b9-172">Uso</span><span class="sxs-lookup"><span data-stu-id="2d1b9-172">Usage</span></span>

<span data-ttu-id="2d1b9-173">En este ejemplo, se conecta a una tabla denominada "Contacto" con columnas Id, LastName y FirstName.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-173">This example connects to a table named "Contact" with Id, LastName, and FirstName columns.</span></span> <span data-ttu-id="2d1b9-174">El código muestra las entidades de contacto en la tabla y registra los nombres y apellidos.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-174">The code lists the Contact entities in the table and logs the first and last names.</span></span>

### <a name="bindings"></a><span data-ttu-id="2d1b9-175">Enlaces</span><span class="sxs-lookup"><span data-stu-id="2d1b9-175">Bindings</span></span>
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
<span data-ttu-id="2d1b9-176">`entityId` debe estar vacío para los enlaces de tabla.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-176">`entityId` must be empty for table bindings.</span></span>

<span data-ttu-id="2d1b9-177">`ConnectionAppSettingsKey` identifica la configuración de aplicación que almacena la cadena de conexión de API.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-177">`ConnectionAppSettingsKey` identifies the app setting that stores the API connection string.</span></span> <span data-ttu-id="2d1b9-178">La configuración de la aplicación se crea automáticamente cuando se agrega una conexión de API en la interfaz de usuario integrada.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-178">The app setting is created automatically when you add an API connection in the integrate UI.</span></span>

<span data-ttu-id="2d1b9-179">Un conector tabular proporciona conjuntos de datos, y cada conjunto de datos contiene tablas.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-179">A tabular connector provides data sets, and each data set contains tables.</span></span> <span data-ttu-id="2d1b9-180">El nombre del conjunto de datos predeterminado es "default".</span><span class="sxs-lookup"><span data-stu-id="2d1b9-180">The name of the default data set is “default.”</span></span> <span data-ttu-id="2d1b9-181">Los títulos de un conjunto de datos y una tabla en varios proveedores de SaaS se enumeran a continuación:</span><span class="sxs-lookup"><span data-stu-id="2d1b9-181">The titles for a dataset and a table in various SaaS providers are listed below:</span></span>

|<span data-ttu-id="2d1b9-182">Conector</span><span class="sxs-lookup"><span data-stu-id="2d1b9-182">Connector</span></span>|<span data-ttu-id="2d1b9-183">Dataset</span><span class="sxs-lookup"><span data-stu-id="2d1b9-183">Dataset</span></span>|<span data-ttu-id="2d1b9-184">Tabla</span><span class="sxs-lookup"><span data-stu-id="2d1b9-184">Table</span></span>|
|:-----|:---|:---| 
|<span data-ttu-id="2d1b9-185">**SharePoint**</span><span class="sxs-lookup"><span data-stu-id="2d1b9-185">**SharePoint**</span></span>|<span data-ttu-id="2d1b9-186">Sitio</span><span class="sxs-lookup"><span data-stu-id="2d1b9-186">Site</span></span>|<span data-ttu-id="2d1b9-187">Lista de SharePoint</span><span class="sxs-lookup"><span data-stu-id="2d1b9-187">SharePoint List</span></span>
|<span data-ttu-id="2d1b9-188">**SQL**</span><span class="sxs-lookup"><span data-stu-id="2d1b9-188">**SQL**</span></span>|<span data-ttu-id="2d1b9-189">Base de datos</span><span class="sxs-lookup"><span data-stu-id="2d1b9-189">Database</span></span>|<span data-ttu-id="2d1b9-190">Tabla</span><span class="sxs-lookup"><span data-stu-id="2d1b9-190">Table</span></span> 
|<span data-ttu-id="2d1b9-191">**Hoja de cálculo de Google**</span><span class="sxs-lookup"><span data-stu-id="2d1b9-191">**Google Sheet**</span></span>|<span data-ttu-id="2d1b9-192">Hoja de cálculo</span><span class="sxs-lookup"><span data-stu-id="2d1b9-192">Spreadsheet</span></span>|<span data-ttu-id="2d1b9-193">Hoja de cálculo</span><span class="sxs-lookup"><span data-stu-id="2d1b9-193">Worksheet</span></span> 
|<span data-ttu-id="2d1b9-194">**Excel**</span><span class="sxs-lookup"><span data-stu-id="2d1b9-194">**Excel**</span></span>|<span data-ttu-id="2d1b9-195">Archivo de Excel</span><span class="sxs-lookup"><span data-stu-id="2d1b9-195">Excel file</span></span>|<span data-ttu-id="2d1b9-196">Hoja</span><span class="sxs-lookup"><span data-stu-id="2d1b9-196">Sheet</span></span> 

<!--
See the language-specific sample that copies the input file to the output file.

* [C#](#incsharp)
* [Node.js](#innodejs)

-->
<a name="incsharp"></a>

### <a name="usage-in-c"></a><span data-ttu-id="2d1b9-197">Uso en C#</span><span class="sxs-lookup"><span data-stu-id="2d1b9-197">Usage in C#</span></span> #

```cs
#r "Microsoft.Azure.ApiHub.Sdk"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.ApiHub;

//Variable name must match column type
//Variable type is dynamically bound to the incoming data
public class Contact
{
    public string Id { get; set; }
    public string LastName { get; set; }
    public string FirstName { get; set; }
}

public static async Task Run(string input, ITable<Contact> table, TraceWriter log)
{
    //Iterate over every value in the source table
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

<span data-ttu-id="2d1b9-198"><!--
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
## Configuración de origen de datos</span><span class="sxs-lookup"><span data-stu-id="2d1b9-198"><!--
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

### <a name="sql-server"></a><span data-ttu-id="2d1b9-199">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2d1b9-199">SQL Server</span></span>

<span data-ttu-id="2d1b9-200">El script para crear y rellenar la tabla Contact se encuentra a continuación.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-200">The script to create and populate the Contact table is below.</span></span> <span data-ttu-id="2d1b9-201">dataSetName es el "valor predeterminado".</span><span class="sxs-lookup"><span data-stu-id="2d1b9-201">dataSetName is “default.”</span></span>

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

### <a name="google-sheets"></a><span data-ttu-id="2d1b9-202">Hojas de cálculo de Google</span><span class="sxs-lookup"><span data-stu-id="2d1b9-202">Google Sheets</span></span>
<span data-ttu-id="2d1b9-203">En Google Docs, cree una hoja de cálculo con una hoja de cálculo denominada `Contact`.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-203">In Google Docs, create a spreadsheet with a worksheet named `Contact`.</span></span> <span data-ttu-id="2d1b9-204">El conector no puede usar el nombre para mostrar de la hoja de cálculo.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-204">The connector cannot use the spreadsheet display name.</span></span> <span data-ttu-id="2d1b9-205">El nombre interno (en negrita) tiene que usarse como dataSetName, por ejemplo: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Agregar los nombres de columna `Id`, `LastName`, `FirstName` a la primera fila, y luego completar los datos en las filas siguientes.</span><span class="sxs-lookup"><span data-stu-id="2d1b9-205">The internal name (in bold) needs to be used as dataSetName, for example: `docs.google.com/spreadsheets/d/`**`1UIz545JF_cx6Chm_5HpSPVOenU4DZh4bDxbFgJOSMz0`** Add the column names `Id`, `LastName`, `FirstName` to the first row, then populate data on subsequent rows.</span></span>

### <a name="salesforce"></a><span data-ttu-id="2d1b9-206">Salesforce</span><span class="sxs-lookup"><span data-stu-id="2d1b9-206">Salesforce</span></span>
<span data-ttu-id="2d1b9-207">dataSetName es el "valor predeterminado".</span><span class="sxs-lookup"><span data-stu-id="2d1b9-207">dataSetName is “default.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d1b9-208">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2d1b9-208">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
