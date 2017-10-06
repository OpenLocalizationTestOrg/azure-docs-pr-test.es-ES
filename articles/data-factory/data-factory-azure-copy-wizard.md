---
title: aaaData Asistente para copiar de generador de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola datos toocopy de Asistente para copia de Azure de factoría de datos de toosinks de orígenes de datos admitidos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 0974eb40-db98-4149-a50d-48db46817076
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: 188b3ae15f937b84a58aec1b979347ac8090abf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory-copy-wizard"></a>Asistente para copia de Azure Data Factory
Hola Asistente para copiar de factoría de datos de Azure facilita proceso Hola de ingesta datos, que normalmente es un primer paso en un escenario de integración de datos to-end. Cuando vaya a través de hello Asistente para copiar de factoría de datos de Azure, no es necesario toounderstand ninguna definición de JSON para servicios vinculados, conjuntos de datos y las canalizaciones. Asistente de Hello crea automáticamente una toocopy de datos de canalización de hello origen toohello seleccionado destino seleccionado. Además, Hola Asistente para copiar ayuda a datos de hello toovalidate se ingestión en tiempo de Hola de creación. Esto le permite ahorrar tiempo, especialmente cuando se están introducción de datos para hello primera vez desde el origen de datos de Hola. Hola toostart Asistente para copiar, haga clic en hello **copiar datos** de mosaico en la página principal de saludo de la factoría de datos.

![Asistente para copia](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="designed-for-big-data"></a>Diseñado para macrodatos
Este asistente le permite mover datos desde una gran variedad de orígenes toodestinations de tooeasily en minutos. Después de que vaya a través del Asistente de hello, una canalización con una actividad de copia se crea automáticamente para usted, junto con las entidades de factoría de datos dependientes (servicios vinculados y conjuntos de datos). No hay pasos adicionales son canalización de hello toocreate necesarios.   

![Selección de origen de datos](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Para obtener instrucciones paso a paso toocreate datos toocopy de canalización muestra de una tabla de base de datos de SQL Azure tooan de blobs de Azure, vea hello [tutorial del Asistente para copiar](data-factory-copy-data-wizard-tutorial.md).
>
>

Hola asistente está diseñado con grandes cantidades de datos en la cuenta de inicio hello, con compatibilidad para diversos datos y tipos de objeto. Puede crear canalizaciones de Data Factory que trasladen cientos de carpetas, archivos o tablas. Asistente de Hello es compatible con la vista previa de datos automática, captura de esquema y la asignación ni filtrado de datos.

## <a name="automatic-data-preview"></a>Vista previa de datos automática
Puede obtener una vista previa parte de datos de Hola Hola origen de datos seleccionado en orden toovalidate si los datos de hello están lo que desea toocopy. Además, si los datos de origen de hello están en un archivo de texto, hello Asistente para copiar analiza fila de Hola de toolearn del archivo de texto de Hola y los delimitadores de columna y esquema automáticamente.

![Configuración del formato de archivo](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Captura y asignación de esquema
esquema Hola de datos de entrada no puede coincidir con el esquema de Hola de datos de salida en algunos casos. En este escenario, necesita las columnas de toomap de hello toocolumns de esquema de origen del esquema de destino de Hola.

> [!TIP]
> Cuando copia de datos de SQL Server o base de datos de SQL de Azure en almacenamiento de datos de SQL Azure, si no existe la tabla de hello en el almacén de destino de hello, factoría de datos admite la creación de tabla automáticamente mediante el esquema de origen. Obtener más información en [mover tooand de datos de almacenamiento de datos de SQL Azure mediante Data Factory de Azure](./data-factory-azure-sql-data-warehouse-connector.md).
>

Utilice un tooselect de lista desplegable muestra una columna de la columna tooa toomap esquema de origen de Hola Hola esquema de destino. Hola Asistente para copiar intenta toounderstand el patrón de asignación de columnas. Se aplica Hola mismo toohello de patrón de rest de columnas de hello, por lo que no es necesario tooselect de columnas de hello individualmente asignación del esquema toocomplete Hola. Si lo prefiere, puede invalidar estas asignaciones mediante Hola listas desplegables toomap Hola columnas uno por uno. patrón de Hello pasa a ser más precisa como asignar más columnas. Hola Asistente para copiar actualiza constantemente patrón de Hola y en última instancia alcanza Hola derecho patrón para la asignación de columnas de hello desea tooachieve.     

![Asignación de esquemas](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrado de datos
Puede filtrar datos tooselect solo Hola datos de origen que necesita el almacén de datos de copia de toobe toohello receptor. Filtrado reduce el volumen de Hola de toohello copiada receptor de hello datos toobe, por tanto, mejora el rendimiento de Hola de operación de copia de Hola y almacén de datos. Proporciona un forma flexible que toofilter los datos en una base de datos relacional mediante el lenguaje de consulta SQL de Hola o archivos en una carpeta de blobs de Azure mediante el uso de [funciones de factoría de datos y variables](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrado de datos de una base de datos
Hello captura de pantalla siguiente muestra una consulta SQL con hello `Text.Format` función y `WindowStart` variable.

![Validación de expresiones](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrar datos en una carpeta de blobs de Azure
Puede usar variables en datos toocopy de la ruta de acceso de la carpeta Hola desde una carpeta que se determina en tiempo de ejecución según [las variables del sistema](data-factory-functions-variables.md#data-factory-system-variables). las variables de Hello admitido son: **{year}**, **{month}**, **{day}**, **{hora}**, **{minuto}**, y **{personalizado}**. Por ejemplo: carpetaDeEntrada/{year}/{month}/{day}.

Supongamos que ha escrito carpetas Hola siguiendo el formato:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Haga clic en hello **examinar** botón **archivo o carpeta**, examinar tooone de estas carpetas (por ejemplo, 2016 -> 03 -> 01 -> 02) y haga clic en **elegir**. Debería ver `2016/03/01/02` en el cuadro de texto de Hola. Ahora, reemplace **2016** con **{year}**, **03** con **{month}**, **01** con **{day}** , y **02** con **{hora}**, presione hello y **ficha** clave. Debería ver el formato de hello tooselect de listas desplegables para estos cuatro variables:

![Uso de variables del sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Como se muestra en la siguiente captura de pantalla de hello, también puede usar un **personalizado** variable y cualquier [admite cadenas de formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). una carpeta con esa estructura, utilice hello tooselect **examinar** botón primero. A continuación, reemplazar un valor con **{personalizado}**, presione hello y **ficha** cuadro de texto hello toosee clave donde puede escribir la cadena de formato de Hola.     

![Uso de la variable personalizada](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="scheduling-options"></a>Opciones de programación
Puede ejecutar la operación de copia de hello una sola vez o según una programación (cada hora, diariamente, y así sucesivamente). Ambos de estas opciones se pueden usar para amplitud Hola de conectores de Hola a través de entornos, como local, de nube y de copia de escritorio local.

Una operación de copia única permite el movimiento de datos desde un origen tooa destino solo una vez. Se aplica toodata de cualquier tamaño y en cualquier formato admitido. Hola programado copiar permite toocopy datos en una periodicidad prescrita. Puede usar la configuración enriquecidos (por ejemplo, Reintentar, tiempo de espera y las alertas) tooconfigure Hola programado de copia.

![Propiedades de programación](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Pasos siguientes
Para ver un tutorial rápido de usar Asistente para copiar de factoría de datos de hello toocreate una canalización con actividad de copia, consulte [Tutorial: crear una canalización mediante el Asistente para copiar Hola](data-factory-copy-data-wizard-tutorial.md).
