---
title: aaaInteract con informes utilizando la API de JavaScript de hello | Documentos de Microsoft
description: Power BI Embedded, interactuar con informes utilizando Hola API de JavaScript
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interactuar con informes de Power BI con hello API de JavaScript
habilita la API de JavaScript de Power BI Hola se tooeasily incrustar informes de Power BI en sus aplicaciones. Con hello API, las aplicaciones pueden interactuar mediante programación con elementos de informe diferente como páginas y filtros. Esta interactividad hace que los informes Power BI se integren mejor en las aplicaciones.

Incrustar un informe de Power BI en su aplicación mediante un iframe en el que se hospeda como parte de la aplicación hello. Hola iframe actúa como un límite entre la aplicación y el informe de hello, como puede ver en hello después de la imagen. 

![iframe de Power BI Embedded sin la API de Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hola iframe hace Hola incrustar proceso mucho más sencillo, pero sin Hola Hola de API de JavaScript informes y la aplicación no pueden interactuar entre sí. Esta falta de interacción puede hacer que la sensación de que el informe de hello no es realmente parte de la aplicación hello. informe de Hola y de aplicación sea realmente necesitan toocommunicate y hacia atrás, como en hello después de la imagen.

![iframe de Power BI Embedded con la API de Javascript](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Hola API de JavaScript de Power BI permite código toowrite que puede pasar de manera segura a través de límites de iframe Hola. Esto permite que su aplicación tooprogrammatically realizar una acción en un informe y toolisten para eventos de acciones que realizan los usuarios en el informe de Hola.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>¿Qué puede hacer con hello API de JavaScript de Power BI?
Con hello API de JavaScript puede administrar informes, navegue toopages en un informe, filtrar un informe y controlar los eventos de incrustación. Hello siguiente diagrama muestra la estructura de Hola de hello API.

![Diagrama de la API de JavaScript de Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Administración de informes
Hola API de Javascript habilita el comportamiento de toomanage a nivel de página y el informe de hello:

* Incrustar un informe de BI de energía específico de forma segura en la aplicación: intente hello [incrustar la aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Establecer un token de acceso
* Configurar informes de Hola
  * Habilitar y deshabilitar el panel de filtro de Hola y el panel de navegación de página; intente hello [actualizar configuración de la aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Establecer valores predeterminados para las páginas y los filtros - intente hello [demostración de conjunto de valores predeterminados](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* Entrar y salir de modo de pantalla completa

[Más información acerca de cómo insertar informes](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Navegue toopages en un informe
Hola API JavaScript enbales toodiscover todas las páginas de un informe y tooset Hola actual una página. Intente hello [aplicación de demostración de navegación](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Más información acerca de la navegación por la página](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Filtro de un informe
Hola API de JavaScript proporciona básicas y avanzadas capacidades de filtrado de informes incrustados y páginas del informe. Intente hello [filtrado de aplicación de demostración](http://azure-samples.github.io/powerbi-angular-client/#/scenario4)y revise el código introducción aquí.  

#### <a name="basic-filters"></a>Filtros básicos
Un filtro básico se coloca en un nivel de jerarquía o de columna y contiene una lista de valores tooinclude o exclude.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Filtros avanzados
Filtros avanzados utilizan el operador lógico de Hola y OR y aceptar uno o dos condiciones, cada uno con su propio operador y valor. Estas son las condiciones que se admiten:

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contains
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Más información acerca de los filtros](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Control de eventos
Además toosending información en hello iframe, la aplicación puede también recibe información de hello después de eventos procedentes de hello iframe:

* Insertar
  * loaded
  * error
* Informes
  * pageChanged
  * dataSelected (próximamente)

[Más información sobre el control de eventos](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información acerca de la API de JavaScript de Power BI Hola, consulte Hola siguientes vínculos:

* [Wiki de API de JavaScript](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Referencia de modelo de objeto](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Muestras
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Demostración en directo](https://microsoft.github.io/PowerBI-JavaScript/demo/)

