---
title: "orígenes de aaaData admitidos en los servicios de análisis de Azure | Documentos de Microsoft"
description: "Describe los orígenes de datos admitidos para los modelos de datos en Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 6ec63319-ff9b-4b01-a1cd-274481dc8995
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2902d7d3c3bcf086419822fa826193bd247bde61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="data-sources-supported-in-azure-analysis-services"></a>Orígenes de datos admitidos en Azure Analysis Services
Azure servidores de Analysis Services admiten orígenes de toodata conexión en la nube de Hola y de forma local en su organización. Orígenes de datos compatibles adicionales se agregan todo el tiempo Hola. por lo que se recomienda consultarlos con asiduidad. 

Hola siguientes orígenes de datos es compatibles actualmente:

| Nube  |
|---|
| Azure Blob Storage*  |
| Base de datos SQL de Azure  |
| Almacenamiento de datos de Azure |


| Local  |   |   |   |
|---|---|---|---|
| Base de datos de Access  | Carpeta* | Base de datos de Oracle  | Base de datos de Teradata |
| Active Directory*  | Documento JSON*  | Base de datos de Postgre SQL*  |Tabla XML* |
| Analysis Services  | Líneas de archivo binario*  | SAP HANA*  |
| Analytics Platform System  | Base de datos MySQL  | SAP Business Warehouse*  | |
| Dynamics CRM*  | Fuente OData*  | SharePoint*  |
| Libro de Excel  | Consulta ODBC  | SQL Database  |
| Exchange*  | OLE DB  | Base de datos de Sybase  |

\* Solo modelos tabulares 1400. 

> [!IMPORTANT]
> Conectar requieren orígenes de datos local tooon una [puerta de enlace de datos local](analysis-services-gateway.md) instalado en un equipo en su entorno.

## <a name="data-providers"></a>Proveedores de datos

Modelos de datos de Analysis Services de Azure pueden requerir distintos proveedores de datos al conectarse a orígenes de datos de toocertain. En algunos casos, los modelos tabulares conectar orígenes de toodata mediante proveedores nativos como SQL Server Native Client (SQLNCLI11) pueden devolver un error.

Para los modelos de datos que se conectan tooa datos en la nube de origen como base de datos de SQL Azure, si utiliza los proveedores nativos que no sea de SQLOLEDB, puede ver el mensaje de error: **"hello provider 'SQLNCLI11.1' no está registrado".** O bien, si tiene DirectQuery modelo orígenes de datos de conexión local tooon, si utiliza los proveedores nativos puede ver el mensaje de error: **"Error al crear el conjunto de filas OLE DB. Sintaxis incorrecta cerca de 'LIMIT'”**.

Hola después de los proveedores de origen de datos es compatibles con en memoria o los modelos de datos de DirectQuery cuando toodata conecta orígenes en la nube de Hola o de forma local:

### <a name="cloud"></a>Nube
| **Origen de datos** | **En memoria** | **DirectQuery** |
|  --- | --- | --- |
| Almacenamiento de datos SQL de Azure |Proveedor de datos .NET Framework para SQL Server |Proveedor de datos .NET Framework para SQL Server |
| Base de datos SQL de Azure |Proveedor de datos .NET Framework para SQL Server |Proveedor de datos .NET Framework para SQL Server | |

### <a name="on-premises-via-gateway"></a>Local (mediante una puerta de enlace)
|**Origen de datos** | **En memoria** | **DirectQuery** |
|  --- | --- | --- |
| SQL Server |SQL Server Native Client 11.0 |Proveedor de datos .NET Framework para SQL Server |
| SQL Server |Proveedor OLE DB de Microsoft para SQL Server |Proveedor de datos .NET Framework para SQL Server | |
| SQL Server |Proveedor de datos .NET Framework para SQL Server |Proveedor de datos .NET Framework para SQL Server | |
| Oracle |Proveedor OLE DB de Microsoft para Oracle |Proveedor de datos de Oracle para .NET | |
| Oracle |Proveedor de datos de Oracle para .NET |Proveedor de datos de Oracle para .NET | |
| Teradata |Proveedor OLE DB para Teradata |Proveedor de datos de Teradata para .NET | |
| Teradata |Proveedor de datos de Teradata para .NET |Proveedor de datos de Teradata para .NET | |
| Analytics Platform System |Proveedor de datos .NET Framework para SQL Server |Proveedor de datos .NET Framework para SQL Server | |

> [!NOTE]
> Asegúrese de que estén instalados proveedores de 64 bits cuando se use la puerta de enlace local.
> 
> 

Cuando se migra un modelo tabular de SQL Server Analysis Services local tooAzure Analysis Services, puede ser proveedor de hello toochange necesarios.

**toospecify un proveedor de origen de datos**

1. En SSDT > **Tabular Model Explorer**(Explorador de modelos tabulares) > **Orígenes de datos**, haga clic en una conexión de origen de datos y en **Editar origen de datos**.
2. En **Editar conexión**, haga clic en **avanzadas** ventana de propiedades de tooopen Hola por adelantado.
3. En **Set avanzadas Properties** > **proveedores**, a continuación, seleccione Hola proveedor adecuado.

## <a name="impersonation"></a>Suplantación
En algunos casos, puede ser necesario toospecify una cuenta de suplantación diferente. La cuenta de suplantación se puede especificar en SSDT o SSMS.

Para orígenes de datos locales:

* Si se utiliza la autenticación de SQL, la suplantación debe ser la Cuenta de servicio.
* Si se utiliza la autenticación de Windows, establezca la contraseña y el usuario de Windows. Para SQL Server, se admite la autenticación de Windows con una cuenta de suplantación específica solo para los modelos de datos en memoria.

Para orígenes de datos en la nube:

* Si se utiliza la autenticación de SQL, la suplantación debe ser la Cuenta de servicio.

## <a name="next-steps"></a>Pasos siguientes
Si tiene orígenes de datos locales, que seguro hello tooinstall [puerta de enlace local](analysis-services-gateway.md).   
vea toolearn más acerca de cómo administrar el servidor en SSMS, o de SSDT [administrar su servidor](analysis-services-manage.md).

