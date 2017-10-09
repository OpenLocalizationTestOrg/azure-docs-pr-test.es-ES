---
title: "datos de aaaCopy fácilmente con el Asistente para copiar - Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola datos toocopy de Asistente para copiar de factoría de datos de toosinks de orígenes de datos admitidos."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: f904972f-cd33-48db-9755-2b3196ae4168
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 99437ec16facf3b94c8be18487ec89e9f13acc9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="copy-or-move-data-easily-with-azure-data-factory-copy-wizard"></a>Copia o movimiento sencillos de datos con el Asistente para copia de Azure Data Factory
Hola Asistente para copiar de factoría de datos de Azure es el proceso de Hola de tooease de ingesta datos, que normalmente es un primer paso en un escenario de integración de datos to-end. Cuando vaya a través de hello Asistente para copiar de factoría de datos de Azure, no es necesario toounderstand ninguna definición de JSON para las canalizaciones, los conjuntos de datos y servicios vinculados. Sin embargo, después de completar todos los pasos de hello en el Asistente de hello, Hola asistente crea automáticamente un toocopy de datos de canalización de hello origen toohello seleccionado destino seleccionado. Además, Hola copia asistente le ayudará a datos de hello toovalidate se ingestión en tiempo de Hola de creación, lo que ahorra gran parte del tiempo, especialmente cuando se se introducción de datos para hello primera vez desde el origen de datos de Hola. Hola toostart Asistente para copiar, haga clic en hello **copiar datos** de mosaico en la página principal de saludo de la factoría de datos.

![Asistente para copia](./media/data-factory-copy-wizard/copy-data-wizard.png)

## <a name="an-intuitive-wizard-for-copying-data"></a>Un asistente intuitivo para copiar datos
Este asistente le permite mover datos desde una gran variedad de orígenes toodestinations de tooeasily en minutos. Después de pasar por el Asistente de hello, una canalización con una actividad de copia se crea automáticamente junto con las entidades de factoría de datos dependientes (servicios vinculados y los conjuntos de datos). No hay pasos adicionales son canalización de hello toocreate necesarios.   

![Selección de origen de datos](./media/data-factory-copy-wizard/select-data-source-page.png)

> [!NOTE]
> Vea [tutorial del Asistente para copiar](data-factory-copy-data-wizard-tutorial.md) artículo para obtener instrucciones paso a paso toocreate datos toocopy de canalización muestra de una tabla de base de datos de SQL Azure tooan de blobs de Azure. 
> 
> 

Hola asistente está diseñado con grandes cantidades de datos en la cuenta de inicio de Hola. Es canalizaciones de factoría de datos de tooauthor simple y eficiente que mover cientos de carpetas, archivos o tablas mediante el Asistente para copiar los datos de Hola. Hello asistente admite Hola siguientes tres características: vista previa de datos automática, la captura de esquema y asignación y filtrar datos. 

## <a name="automatic-data-preview"></a>Vista previa de datos automática
Asistente para copiar de Hello permite tooreview una parte de datos de Hola de hello seleccionada origen de datos para toovalidate si los datos Hola Hola haga datos que desea toocopy. Además, si los datos de origen de hello están en un archivo de texto, Asistente para copiar de hello analiza fila de toolearn del archivo de texto de Hola y los delimitadores de columna y esquema automáticamente. 

![Configuración del formato de archivo](./media/data-factory-copy-wizard/file-format-settings.png)

## <a name="schema-capture-and-mapping"></a>Captura y asignación de esquema
esquema Hola de datos de entrada no puede coincidir con el esquema de Hola de datos de salida en algunos casos. En este escenario, necesita las columnas de toomap de hello toocolumns de esquema de origen del esquema de destino de Hola. 

Asistente para copiar de Hello asigna automáticamente las columnas en toocolumns de esquema de origen de Hola Hola esquema de destino. Puede invalidar las asignaciones de hello mediante el uso de listas desplegables de hello (o) especifican si éste necesita una columna toobe omitió durante la copia de datos de Hola.   

![Asignación de esquemas](./media/data-factory-copy-wizard/schema-mapping.png)

## <a name="filtering-data"></a>Filtrado de datos
Hola asistente permite toofilter datos tooselect solo Hola datos de origen que necesita el almacén de datos de destino/receptor toobe copiar toohello. Filtrado reduce el volumen de Hola de toohello copiada receptor de hello datos toobe, por tanto, mejora el rendimiento de Hola de operación de copia de Hola y almacén de datos. Proporciona un forma flexible que toofilter los datos en una base de datos relacional mediante SQL query language (o) archivos en una carpeta de blobs de Azure a través [funciones de factoría de datos y variables](data-factory-functions-variables.md).   

### <a name="filtering-of-data-in-a-database"></a>Filtrado de datos de una base de datos
En el ejemplo de Hola, consulta SQL de hello usa hello `Text.Format` función y `WindowStart` variable. 

![Validación de expresiones](./media/data-factory-copy-wizard/validate-expressions.png)

### <a name="filtering-of-data-in-an-azure-blob-folder"></a>Filtrar datos en una carpeta de blobs de Azure
Puede usar variables en datos toocopy de la ruta de acceso de la carpeta Hola desde una carpeta que se determina en tiempo de ejecución según [las variables del sistema](data-factory-functions-variables.md#data-factory-system-variables). las variables de Hello admitido son: **{year}**, **{month}**, **{day}**, **{hora}**, **{minuto}**, y **{personalizado}**. Ejemplo: carpetaDeEntrada/{year}/{month}/{day}.

Supongamos que ha escrito carpetas Hola siguiendo el formato:

    2016/03/01/01
    2016/03/01/02
    2016/03/01/03
    ...

Haga clic en hello **examinar** botón **archivo o carpeta**, examinar tooone de estas carpetas (por ejemplo, 2016 -> 03 -> 01 -> 02) y haga clic en **elegir**. Debería ver `2016/03/01/02` en el cuadro de texto de Hola. Sustituya **2016** por **{year}**, **03** por **{month}**, **01** por **{day}** y **02** por **{hour}** y presione la tecla TAB. Debería ver el formato de hello tooselect de listas desplegables para estos cuatro variables:

![Uso de variables del sistema](./media/data-factory-copy-wizard/blob-standard-variables-in-folder-path.png)   

Como se muestra en la siguiente captura de pantalla de hello, también puede usar un **personalizado** variable y cualquier [admite cadenas de formato](https://msdn.microsoft.com/library/8kb3ddd4.aspx). una carpeta con esa estructura, utilice hello tooselect **examinar** botón primero. A continuación, reemplazar un valor con **{personalizado}**y presione el cuadro de texto de pestaña toosee Hola donde puede escribir la cadena de formato de Hola.     

![Uso de la variable personalizada](./media/data-factory-copy-wizard/blob-custom-variables-in-folder-path.png)

## <a name="support-for-diverse-data-and-object-types"></a>Compatibilidad con distintos tipos de objetos y datos
Mediante el uso de hello Asistente para copiar, puede mover eficazmente cientos de carpetas, archivos o tablas.

![Seleccionar las tablas de los datos que se toocopy](./media/data-factory-copy-wizard/select-tables-to-copy-data.png)

## <a name="scheduling-options"></a>Opciones de programación
Puede ejecutar la operación de copia de hello una sola vez o según una programación (cada hora, diariamente, y así sucesivamente). Ambos de estas opciones se pueden usar para amplitud Hola de conectores de Hola en local, en la nube y copia de escritorio local.

Una operación de copia única permite el movimiento de datos desde un origen tooa destino solo una vez. Se aplica toodata de cualquier tamaño y en cualquier formato admitido. Hola programado copiar permite toocopy datos en una periodicidad prescrita. Puede usar la configuración enriquecidos (por ejemplo, Reintentar, tiempo de espera y las alertas) tooconfigure Hola programado de copia.

![Propiedades de programación](./media/data-factory-copy-wizard/scheduling-properties.png)

## <a name="next-steps"></a>Pasos siguientes
Para ver un tutorial rápido de usar Asistente para copiar de factoría de datos de hello toocreate una canalización con actividad de copia, consulte [Tutorial: crear una canalización mediante el Asistente para copiar Hola](data-factory-copy-data-wizard-tutorial.md).

