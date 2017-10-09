---
title: "aaaConstructing cadenas de filtro para el Diseñador de tablas de hello | Documentos de Microsoft"
description: "Crear cadenas de filtro para el Diseñador de tablas de Hola"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: a1a10ea1-687a-4ee1-a952-6b24c2fe1a22
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 48b38d27b97936064daa875e41881d51546bc11f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="constructing-filter-strings-for-hello-table-designer"></a>Crear cadenas de filtro para hello Diseñador de tablas
## <a name="overview"></a>Información general
Hola a toofilter datos en una tabla de Azure que se muestra en Visual Studio **Diseñador de tablas**, construir una cadena de filtro y escríbala en el campo de filtro de Hola. sintaxis de cadena de filtro de Hola Hola WCF Data Services define y es similar tooa cláusula WHERE de SQL, pero se envían toohello servicio tabla a través de una solicitud HTTP. Hola **Diseñador de tablas** identificadores Hola la codificación adecuada para usted, por lo que toofilter en un valor de propiedad, sólo necesita escribir el nombre de propiedad hello, operador de comparación, el valor de criterios, y si lo desea, filtre operador booleano en hello campo. No es necesario tooinclude opción de consulta de hello $filter como si estuviese creando una tabla de hello tooquery de dirección URL a través de hello [referencia de API de REST de servicios de almacenamiento](http://go.microsoft.com/fwlink/p/?LinkId=400447).

Hola WCF Data Services se basan en hello [Open Data Protocol](http://go.microsoft.com/fwlink/p/?LinkId=214805) (OData). Para obtener más información sobre la opción de consulta de sistema de hello filter (**$filter**), vea hello [especificación OData URI Conventions](http://go.microsoft.com/fwlink/p/?LinkId=214806).

## <a name="comparison-operators"></a>Operadores de comparación
Hola se admiten los operadores lógicos siguientes para todos los tipos de propiedad:

| Operador lógico | Description | Ejemplo de cadena de filtro |
| --- | --- | --- |
| eq |Igual |Ciudad eq "Redmond" |
| gt |Mayor que |Precio gt 20 |
| ge |Mayor o igual demasiado|Precio ge 10 |
| lt |Menor que |Precio lt 20 |
| le |Menor o igual que |Precio le 100 |
| ne |No igual |Ciudad ne 'Londres' |
| y |y |Precio le 200 and Precio gt 3,5 |
| o |o |Precio 3,5 or Precio gt 200 |
| not |not |not isAvailable |

Al construir una cadena de filtro, hello las reglas siguientes son importantes:

* Usar operadores lógicos de hello toocompare un valor de propiedad tooa. Tenga en cuenta que no es posible toocompare un valor dinámico de propiedad tooa; un lado de la expresión de hello debe ser una constante.
* Todas las partes de la cadena de filtro de hello distinguen mayúsculas de minúsculas.
* valor constante de Hello debe ser de hello como propiedad Hola para resultados válidos de hello filtro tooreturn de tipo de datos mismas. Para obtener más información acerca de los tipos de propiedad admitidos, consulte [Hola de entender el modelo de datos del servicio de tabla](http://go.microsoft.com/fwlink/p/?LinkId=400448).

## <a name="filtering-on-string-properties"></a>Filtro por propiedades de cadena
Cuando se filtra según las propiedades de cadena, encierre constante de cadena de hello en comillas simples.

Hola siguiente filtros de ejemplo de Hola **PartitionKey** y **RowKey** propiedades; adicional que no son de clave propiedades también podrían agregarse toohello la cadena de filtro:

    PartitionKey eq 'Partition1' and RowKey eq '00001'

Las expresiones de filtro se pueden escribir entre paréntesis, aunque no es obligatorio:

    (PartitionKey eq 'Partition1') and (RowKey eq '00001')

Tenga en cuenta que Hola servicio tabla no admite consultas con caracteres comodín y no se admiten en el Diseñador de tablas de Hola o. Sin embargo, puede realizar mediante el uso de operadores de comparación en el prefijo que desees Hola de coincidencia de prefijos. Hello en el ejemplo siguiente se devuelve entidades que tienen una propiedad LastName empieza con la letra "A" de hello:

    LastName ge 'A' and LastName lt 'B'

## <a name="filtering-on-numeric-properties"></a>Filtro por propiedades numéricas
toofilter en un entero o un número de punto flotante, especifique número Hola sin comillas.

Este ejemplo devuelve todas las entidades con una propiedad Age cuyo valor es mayor que 30:

    Age gt 30

Este ejemplo devuelve todas las entidades con una propiedad AmountDue cuyo valor es menor que o igual a too100.25:

    AmountDue le 100.25

## <a name="filtering-on-boolean-properties"></a>Filtro por propiedades booleanas
toofilter en un valor booleano, especifique **true** o **false** sin comillas.

Hello en el ejemplo siguiente se devuelve todas las entidades donde IsActive propiedad Hola se establece demasiado**true**:

    IsActive eq true

También puede escribir esta expresión de filtro sin el operador lógico Hola. En el siguiente ejemplo de Hola Hola servicio tabla también devolverá todas las entidades donde IsActive sea **true**:

    IsActive

tooreturn todas las entidades donde IsActive sea false, puede usar Hola no operador:

    not IsActive

## <a name="filtering-on-datetime-properties"></a>Filtro por propiedades de fecha y hora
toofilter en un valor de fecha y hora, especifique hello **datetime** (palabra clave), seguida de hello constante de fecha y hora entre comillas simples. constante de fecha y hora de Hello debe estar en formato UTC combinado, tal y como se describe en [dar formato a valores de propiedad de fecha y hora](http://go.microsoft.com/fwlink/p/?LinkId=400449).

Hola siguiente ejemplo devuelve las entidades donde hello cuya propiedad CustomerSince es igual tooJuly 10, 2008:

    CustomerSince eq datetime'2008-07-10T00:00:00Z'
