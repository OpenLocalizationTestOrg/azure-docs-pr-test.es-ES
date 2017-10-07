---
title: "esquemas definidos por el aaaUser en el almacén de datos de SQL | Documentos de Microsoft"
description: Sugerencias para usar los esquemas Transact-SQL en el Almacenamiento de datos SQL Azure para desarrollar soluciones.
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a>Esquemas definidos por el usuario en el Almacenamiento de datos SQL
Almacenamientos de datos tradicionales suelen usar bases de datos independientes toocreate los límites de aplicación en función de la carga de trabajo, dominio o seguridad. Por ejemplo, un almacenamiento de datos de SQL Server tradicional podría incluir una base de datos provisional, una base de datos de almacenamiento de datos y algunas bases de datos data mart. En esta topología, cada base de datos funciona como una carga de trabajo y el límite de seguridad de la arquitectura de Hola.

Por el contrario, el almacenamiento de datos SQL se ejecuta como carga de trabajo del almacenamiento de datos todo de hello dentro de una base de datos. No se permiten las combinaciones entre bases de datos. Por lo tanto, almacenamiento de datos de SQL espera que todas las tablas utilizadas por hello toobe de almacenamiento almacenado en una base de datos de Hola.

> [!NOTE]
> El Almacenamiento de datos SQL no admite consultas entre bases de datos de cualquier tipo. Por lo tanto, las implementaciones de almacenamiento de datos que aprovechan este patrón deberá toobe revisado.
> 
> 

## <a name="recommendations"></a>Recomendaciones
Se trata de recomendaciones para consolidar los límites de cargas de trabajo, seguridad, dominio y funcionales con esquemas definidos por el usuario.

1. Usar la carga de trabajo de almacenamiento de datos completo de toorun de base de datos de un almacén de datos SQL
2. Consolidar los datos almacenamiento entorno toouse un almacenamiento de datos SQL base de datos existente
3. Aproveche **esquemas definidos por el usuario** límites de hello tooprovide previamente implementado mediante bases de datos.

Si los esquemas definidos por el usuario no se han utilizado anteriormente, tendrá una pizarra limpia. Basta con usar nombre de base de datos anterior de hello como base de Hola para los esquemas definidos por el usuario de base de datos de almacenamiento de datos SQL de Hola.

Si ya se han utilizado los esquemas, tienen algunas opciones:

1. Quitar los nombres de esquema heredado de Hola y empezar de cero
2. Conservar los nombres de esquema heredado de Hola por nombre de tabla de hello previamente pendiente esquema heredado nombre toohello
3. Conservar los nombres de esquema heredado de hello mediante la implementación de vistas de tabla de hello en un esquema adicional toore-crear la estructura de esquema antigua Hola.

> [!NOTE]
> En la primera inspección opción 3 puede parecer opción más atractiva Hola. Sin embargo, el demonio de hello es detalladamente Hola. Las vistas son de solo lectura en el Almacenamiento de datos SQL. Cualquier modificación de datos o tabla tendría toobe realizada en la tabla de base de Hola. La opción 3 también introduce una capa de vistas en el sistema. Conviene toogive este algunas consideraciones adicionales si se utilizan vistas ya parte de la arquitectura.
> 
> 

### <a name="examples"></a>Ejemplos:
Implementar los esquemas definidos por el usuario en función de los nombres de base de datos.

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

Conservar esquema heredado les da un nombre por previamente pendiente toohello nombre de la tabla. Utilizar esquemas para límite de carga de trabajo de Hola.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

Conservar los nombres de esquemas heredados con vistas.

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> Cualquier cambio en la estrategia de esquema necesita una revisión del modelo de seguridad de Hola para base de datos de Hola. En muchos casos es posible que el modelo de seguridad de hello toosimplify capaz de mediante la asignación de permisos en el nivel del esquema de Hola. Si se requieren permisos más granulares, puede utilizar funciones de base de datos.
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Para más sugerencias sobre desarrollo, consulte la [información general sobre desarrollo][development overview].

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
