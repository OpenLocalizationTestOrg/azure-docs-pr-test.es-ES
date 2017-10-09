---
title: "aaaAzure multilingüe de búsqueda | Documentos de Microsoft"
description: "Búsqueda de Azure admite 56 idiomas y aprovecha los analizadores de idiomas Lucene y la tecnología de procesamiento de lenguaje natural de Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Creación de un índice para documentos en varios idiomas en Búsqueda de Azure
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing power Hola de analizadores de lenguaje es tan fácil como una propiedad de configuración en un campo de búsqueda en la definición del índice Hola. Ahora puede realizar este paso en el portal de Hola.

A continuación se muestran capturas de pantalla de hello hojas de Portal de Azure para la búsqueda de Azure que permiten a los usuarios toodefine un esquema de índice. Desde esta hoja, los usuarios pueden crear todos los campos de Hola y establecer la propiedad de analizador de Hola para cada uno de ellos.

> [!IMPORTANT]
> Solo puede establecer un analizador de lenguaje durante la definición del campo, como en cuando cree un nuevo índice de hello descárguese de corriente, o cuando se agrega un nuevo índice existente de tooan de campo. Asegúrese de que especificar completamente todos los atributos, como analizador de hello, al crear el campo de Hola. No ser capaz de tooedit atributos de Hola o cambiar el tipo de analizador de hello una vez que guarde los cambios.
>
>

## <a name="define-a-new-field-definition"></a>Definición de una nueva definición de campo
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) y hoja de servicio de hello abierto de su servicio de búsqueda.
2. Haga clic en **agregar índice** de comando de hello barra princip Hola de hello servicio panel toostart un nuevo índice, o abrir un tooset índice existente en nuevos campos que se va a agregar un analizador de índice existente tooan.
3. aparece la hoja de campos de Hello, lo que le ofrece opciones para definir el esquema de Hola de índice de hello, incluido tab del analizador de Hola utiliza para elegir un analizador de lenguaje.
4. En los campos, inicie una definición de campo proporcionar un nombre, Elegir tipo de datos de Hola y establecer campo de atributos toomark Hola como texto completo permite realizar búsquedas, puede recuperar en resultados de búsqueda, puede usar en las estructuras de navegación de faceta, que se puede ordenar y así sucesivamente.
5. Antes de continuar toohello siguiente campo, abra hello **analizador** ficha.

![][1]
*tooselect un analizador, haga clic en la ficha de analizador de hello en la hoja de campos de Hola*

## <a name="choose-an-analyzer"></a>Selección de un analizador
1. Campo de desplazamiento toofind Hola que se está definiendo.
2. Si no ha marcado el campo hello como búsqueda, haga clic en hello casilla ahora toomark como **Searchable**.
3. Haga clic en lista Hola analizador área toodisplay Hola de analizadores disponibles.
4. Elija el analizador de hello desea toouse.

![][2]
*Seleccione uno de los analizadores de hello admitido para cada campo*

De forma predeterminada, todos los campos que permiten búsqueda usan hello [analizador estándar Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que es independiente del idioma. admite la lista completa de hello tooview de analizadores, consulte [compatibilidad con idiomas en búsqueda de Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Una vez seleccionado el analizador de lenguaje de Hola para un campo, se utilizará con cada solicitud de búsqueda e indización para ese campo. Cuando se emite una consulta en varios campos mediante analizadores de diferentes, se procesarán independientemente consulta Hola analizadores de derecho de Hola para cada campo.

Muchas aplicaciones web y móviles atienden a usuarios mundo Hola con distintos idiomas. Es posible toodefine un índice para un escenario similar a éste mediante la creación de un campo para cada idioma admitido.

![][3]
*Definición de índice con un campo de descripción para cada idioma admitido*

Si se conoce el idioma de Hola del agente de hello emitir una consulta, una solicitud de búsqueda puede ser tooa ámbito campo específico mediante hello **searchFields** parámetro de consulta. Hello siguiente consulta se emitirá solo para descripción de hello en polaco:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Puede consultar el índice desde el portal de hello, con **buscar en el explorador** toopaste en un toohello similar de consulta se muestra anteriormente. Buscar en el explorador está disponible en la barra de comandos de hello en el módulo de servicio de Hola. Vea [consultar el índice de búsqueda de Azure en el portal de hello](search-explorer.md) para obtener más información.

A veces hello idioma del agente de hello emitir una consulta no se conoce en qué caso Hola consulta se puede emitir en todos los campos al mismo tiempo. Si es necesario, se pueden definir una preferencia de resultados en un determinado idioma mediante [perfiles de puntuación](https://msdn.microsoft.com/library/azure/dn798928.aspx). En el ejemplo de Hola siguiente, las coincidencias encontradas en la descripción de saludo en inglés será mayor toomatches relativa en polaco y francés:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Si es un desarrollador de .NET, tenga en cuenta que puede configurar los analizadores de lenguaje con hello [SDK de .NET de búsqueda de Azure](http://www.nuget.org/packages/Microsoft.Azure.Search). versión más reciente de Hello incluye compatibilidad para analizadores de lenguaje de Microsoft de hello así.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
