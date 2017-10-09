---
title: "aaaSave búsquedas y pin datos activos en el catálogo de datos de Azure | Documentos de Microsoft"
description: "Cómo tooarticle capacidades resaltadas en el catálogo de datos para guardar los orígenes de datos y activos de datos para su uso posterior."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0ad0a31d4b84782fed9d80acc2734912eecd6d74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="save-searches-and-pin-data-assets-in-azure-data-catalog"></a>Guardar búsquedas y anclar recursos de datos en Azure Data Catalog
## <a name="introduction"></a>Introducción
Azure Data Catalog proporciona funciones de detección de orígenes de datos. Rápidamente puede buscar y filtrar los orígenes de datos de hello catálogo toolocate y conocer su finalidad prevista, lo que sea más fáciles datos correctos de Hola de toofind de trabajo de hello en cuestión.

Pero ¿qué ocurre si necesita tooregularly trabajar con hello mismos datos? Y ¿qué ocurre si usted y otros usuarios con regularidad aportar su toohello conocimiento mismos orígenes de datos en el catálogo de hello? En estas situaciones, tiene toorepeatedly problema Hola mismo búsquedas pueden ser ineficaces. Aquí es donde pueden ayudar las búsquedas guardadas y los recursos de datos anclados.

## <a name="saved-searches"></a>Búsquedas guardadas
Una búsqueda guardada en Data Catalog es una definición de búsqueda por usuario reutilizable. Puede definir una búsqueda, incluidos los términos, etiquetas y otros filtros de la búsqueda y, a continuación, guardarla. Puede volver a ejecutar definición de hello Guardar búsqueda posterior tooreturn los activos de datos que coinciden con sus criterios de búsqueda.

### <a name="create-a-saved-search"></a>Creación de una búsqueda guardada
toocreate una búsqueda guardada, Hola siguientes:
1. En portal del catálogo de datos de Azure hello, Hola **búsqueda actual** ventana, haga clic en **guardar**. 

    ![Vínculo Guardar en la configuración de Búsqueda actual](./media/data-catalog-how-to-save-pin/01-save-option.png) 

2. Especifique los criterios de búsqueda de Hola que desee tooreuse y, a continuación, haga clic en **guardar**.

    ![Nombre de la búsqueda guardada en la configuración de Búsqueda actual](./media/data-catalog-how-to-save-pin/02-name.png)

3. Cuando se le pida, escriba un nombre para la búsqueda guardada de Hola. Elija un nombre que sea significativo y que describe los activos de datos Hola devueltos por las búsquedas de Hola.

### <a name="manage-saved-searches"></a>Administración de búsquedas guardadas
Después de haber guardado búsquedas de uno o más, un **búsquedas guardadas** opción se muestra debajo de hello **búsqueda actual** cuadro. Cuando se expande la lista de hello, se muestran todas las búsquedas guardadas.

 ![Lista de búsquedas guardadas](./media/data-catalog-how-to-save-pin/03-list.png)

Realice cualquiera de hello siguientes:

* tooexecute una búsqueda, seleccione una búsqueda guardada en la lista de Hola.

* tooview una lista de opciones de administración de una búsqueda guardada, haga clic en hello hacia abajo la flecha siguiente toohello alias.

    ![Opción para administrar búsquedas guardadas](./media/data-catalog-how-to-save-pin/04-managing.png)

* tooenter un nuevo nombre para la búsqueda de hello guardado, seleccione **cambiar el nombre de**. no se cambia la definición de la búsqueda de Hola.

* búsqueda de tooremove Hola guardado en la lista, seleccione **eliminar**y, a continuación, confirme la eliminación de Hola.

* búsqueda de hello guarda toomark como la búsqueda de forma predeterminada, seleccione **Guardar como predeterminado**. Si realiza una búsqueda de "vacía" desde la página principal de hello el catálogo de datos, se ejecuta la búsqueda de forma predeterminada. Además, Hola búsqueda que se marca como búsqueda predeterminada de Hola se muestra en la parte superior de Hola de hello **búsquedas guardadas** lista.

### <a name="organizational-saved-searches"></a>Búsquedas guardadas de la organización
Todos los usuarios de la organización pueden guardar búsquedas para su propio uso. Los administradores del catálogo de datos también pueden guardar búsquedas para todos los usuarios dentro de la organización de Hola. Cuando los administradores guardar una búsqueda, le presentará una **recurso compartido de empresa de hello** opción. Si se selecciona este Hola de recursos compartidos de opción guarda búsqueda para todos los usuarios en la organización de Hola.

 ![Búsquedas guardadas de la organización](./media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Recursos de datos anclados
Las búsquedas guardadas le permiten guardar y volver a usar las definiciones de búsqueda. activos de datos de Hello devueltos por las búsquedas Hola podrían cambiar con el tiempo como contenido de Hola de cambio de catálogo de Hola. Al anclar activos de datos, puede identificar explícitamente toomake de activos de datos específicos les sea más fácil tooaccess sin necesidad de toouse una búsqueda.

Anclar un recurso de datos es sencillo. tooadd Hola datos activos tooyour anclado, simplemente haga clic en hello **pin** icono. icono de Hola se muestra en la esquina de Hola de hello asset mosaico en la vista en mosaico Hola y de columna del extremo izquierdo hello en la vista de lista de hello en el portal del catálogo de datos de Azure de Hola.

![icono de anclaje de Hello datos activos](./media/data-catalog-how-to-save-pin/05-pinning.png)

Desanclar un recurso de datos es igual de sencillo. Simplemente haga clic en hello **Desanclar** configuración de hello tootoggle de icono para el recurso seleccionado de Hola.

![recurso de datos Hola desanclar un icono](./media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="hello-my-assets-section"></a>Hola sección Mis activos
Hola catálogo de datos de página principal del portal incluye un **activos mi** sección que se muestra los activos del usuario actual de interés toohello. Esta sección incluye tanto recursos anclados como búsquedas guardadas.

![Hola sección Mis activos en la página de inicio de Hola](./media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Resumen
Catálogo de datos de Azure proporciona capacidades que hacen que sea más fácil toodiscover Hola los orígenes de datos que necesita, por lo que usted y otros miembros de la organización pueden dedicar menos tiempo buscando datos y más tiempo a trabajar con él. Las búsquedas guardadas y los recursos de datos anclados se basan en estas funciones centrales para que los usuarios puedan identificar fácilmente los orígenes de datos con los que trabajan repetidamente.
