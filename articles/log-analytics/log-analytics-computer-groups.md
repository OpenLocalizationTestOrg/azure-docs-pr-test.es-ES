---
title: "búsquedas de registro de grupos de aaaComputer de análisis de registros | Documentos de Microsoft"
description: "Grupos de equipos de análisis de registros permiten tooscope registro búsquedas tooa conjunto determinado de equipos.  Este artículo describen métodos diferentes de Hola que puede usar grupos de equipos de toocreate y cómo toouse en un registro de búsqueda."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Grupos de equipos en búsquedas de registros en Log Analytics

>[!NOTE]
> Este artículo describe el uso de Hola de grupos de equipos mediante el lenguaje de consulta de registro Anayltics actual Hola.    Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, grupos de equipos funcionan de manera diferente.  Notas se proporcionan en este artículo con una sintaxis diferente Hola y el comportamiento de lenguaje de consultas nuevo Hola.  


Grupos de equipos de análisis de registros le permiten tooscope [búsquedas de registro](log-analytics-log-searches.md) tooa conjunto determinado de equipos.  Cada grupo se rellena con equipos mediante una consulta que defina o a través de la importación de grupos de diferentes orígenes.  Cuando Hola está incluido en una búsqueda de registros, resultados de hello son toorecords limitado que coinciden con los equipos de hello en el grupo de Hola.

## <a name="creating-a-computer-group"></a>Creación de un grupo de equipos
Puede crear un grupo de equipos en los análisis de registros mediante cualquiera de los métodos de hello en hello en la tabla siguiente.  En secciones de hello siguientes se proporcionan detalles sobre cada método. 

| Método | Descripción |
|:--- |:--- |
| Búsqueda de registros |Crear una búsqueda de registros que devuelve una lista de equipos y guardar los resultados de Hola como un grupo de equipos. |
| API de búsqueda de registros |Use Hola API de búsqueda de registros tooprogrammatically crear un grupo de equipos basado en hello los resultados de una búsqueda de registros. |
| Active Directory |Realizar la detección de pertenencia a grupos de Hola de los equipos de agente que son miembros de un dominio de Active Directory y cree un grupo de análisis de registros para cada grupo de seguridad. |
| WSUS |Analice automáticamente clientes o servidores WSUS para grupos de destino y cree un grupo en Log Analytics para cada uno. |

### <a name="log-search"></a>Búsqueda de registros
Grupos de equipos creados a partir de una búsqueda de registros contienen todos los equipos de hello devueltos por una consulta de búsqueda que haya definido.  Esta consulta se ejecuta cada vez que se usa el grupo de equipos de Hola para que se refleje los cambios desde que se creó el grupo de Hola.

Usar hello siguiendo el procedimiento toocreate un grupo de equipos de una búsqueda de registros.

1. [Cree una búsqueda de registros](log-analytics-log-searches.md) que devuelva una lista de equipos.  Hello búsqueda debe devolver un conjunto distinto de equipos mediante el uso de algo parecido a **equipo distintivo** o **measure count() by Computer** en consulta Hola.  
2. Haga clic en hello **guardar** situado en la parte superior de Hola de pantalla de bienvenida.
3. Seleccione **Sí** demasiado**guardar esta consulta como un grupo de equipos**.
4. Escriba un **nombre** y un **categoría** para el grupo de Hola.  Si una búsqueda con Hola mismo nombre y la categoría ya existe, entonces se pueden toooverwrite solicitada se.  Puede tener varias búsquedas con el mismo nombre en distintas categorías de Hola. 

A continuación se incluyen ejemplos de búsquedas que puede guardar como un grupo de equipos.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md) hello cambios siguientes son realizadas toohello procedimiento toocreate un nuevo grupo de equipos.
>  
> - Hola toocreate de consulta debe incluir un grupo de equipos `distinct Computer`.  Aquí te mostramos un ejemplo de un toocreate consulta un grupo de equipos.<br>`Heartbeat | where Computer contains "srv" `
> - Cuando se crea un nuevo grupo de equipos, debe especificar un alias de nombre de toohello de adición.  Usar alias de hello cuando se usa el grupo de equipos de hello en una consulta tal y como se describe a continuación.  

### <a name="log-search-api"></a>API de búsqueda de registros
Grupos de equipos creados con hello API de búsqueda de registros son igual Hola como búsquedas creadas con una búsqueda de registros.

Para obtener más información acerca de cómo crear un grupo de equipos con hello API de búsqueda de registros, vea [API de REST de búsqueda de grupos de equipos en el registro de análisis de registros](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Al configurar la pertenencia a grupos de Active Directory de tooimport de análisis de registros, analiza pertenencia Hola de los equipos unidos a un dominio con el agente OMS Hola.  Se crea un grupo de equipos en el análisis de registros para cada grupo de seguridad en Active Directory, y cada equipo se agrega grupos de equipos de toohello correspondientes son miembros de los grupos de seguridad toohello.  Esta pertenencia se actualiza continuamente cada 4 horas.  

Configurar grupos de seguridad de Active Directory de tooimport de análisis de registros de hello **grupos de equipos** menú análisis de registros **configuración**.  Seleccione **Automatización** y, a continuación, **Importar pertenencias a grupos de Active Directory desde los equipos**.  No es necesario realizar ninguna configuración más.

![Grupos de equipos de Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Cuando se han importado los grupos, hello menú listas Hola número de equipos con pertenencia a grupos detectó y Hola número de grupos de importados.  Puede hacer clic en cualquiera de estos Hola de vínculos tooreturn **ComputerGroup** registros con esta información.

### <a name="windows-server-update-service"></a>Windows Server Update Services
Al configurar las pertenencias de grupo de análisis de registros tooimport WSUS, analiza hello como destino la pertenencia a grupos de los equipos con agente de OMS Hola.  Si usas de cliente de destino, cualquier equipo que está conectado tooOMS y forma parte de los grupos de destino de WSUS se su pertenencia al grupo importado tooLog análisis. Si utilizas el servidor como destino, Hola agente de OMS debe instalarse en hello WSUS servidor para toobe de información de pertenencia de grupo de hello importado tooOMS.  Esta pertenencia se actualiza continuamente cada 4 horas. 

Configurar grupos de seguridad de Active Directory de tooimport de análisis de registros de hello **grupos de equipos** menú análisis de registros **configuración**.  Seleccione **Active Directory** y, a continuación, **Importar pertenencias a grupos de Active Directory desde los equipos**.  No es necesario realizar ninguna configuración más.

![Grupos de equipos de Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Cuando se han importado los grupos, hello menú listas Hola número de equipos con pertenencia a grupos detectó y Hola número de grupos de importados.  Puede hacer clic en cualquiera de estos Hola de vínculos tooreturn **ComputerGroup** registros con esta información.

## <a name="managing-computer-groups"></a>Administración de grupos de equipos
Puede ver los grupos de equipos que se crearon a partir de una búsqueda de registros u Hola API de búsqueda de registros de hello **grupos de equipos** menú análisis de registros **configuración**.  Haga clic en hello **x** en hello **quitar** grupo de equipos de columna toodelete Hola.  Haga clic en hello **ver miembros** icono de búsqueda de registros de grupo toorun Hola de un grupo que devuelve sus miembros. 

![Grupos de equipos guardados](media/log-analytics-computer-groups/configure-saved.png)

Hola toomodify grupo, cree un nuevo grupo con hello mismo **categoría** y **nombre** grupo original de toooverwrite Hola.

## <a name="using-a-computer-group-in-a-log-search"></a>Uso de un grupo de equipos de una búsqueda de registros
Utilice Hola después el grupo de equipos de sintaxis toorefer tooa en una búsqueda de registros.  Hola especificando **categoría** es opcional y solo si tiene grupos de equipos con el mismo nombre en distintas categorías de Hola que requieren. 

    $ComputerGroups[Category: Name]

Cuando se ejecuta una búsqueda, los miembros de Hola de los grupos de equipos incluidos en la búsqueda de Hola se resuelven en primer lugar.  Si el grupo de Hola se basa en una búsqueda de registros, que la búsqueda se ejecuta a los miembros de hello tooreturn del grupo de hello antes de realizar la búsqueda de registros de nivel superior de Hola.

Grupos de equipos se usan normalmente con hello **IN** cláusula en búsqueda de registros de hello como en el siguiente ejemplo de Hola:

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Si el área de trabajo se ha actualizado toohello [lenguaje de consulta de análisis de registros nueva](log-analytics-log-search-upgrade.md), a continuación, usar un grupo de equipos en una consulta por su alias se trata como una función como en el siguiente ejemplo de Hola:
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Registros de grupos de equipos
Se crea un registro en el repositorio OMS de Hola para cada pertenencia a grupos de equipo creado a partir de Active Directory o WSUS.  Estos registros tienen un tipo de **ComputerGroup** y que tienen propiedades de hello en hello en la tabla siguiente.  Para los grupos de equipos basados en búsquedas de registros no se crean registros.

| Propiedad | Descripción |
|:--- |:--- |
| Tipo |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Equipo |Nombre del equipo de miembro Hola. |
| Grupo |Nombre del grupo de Hola. |
| GroupFullName |Grupo de toohello de ruta de acceso completa como origen de Hola y el nombre de origen. |
| GroupSource |Origen desde el que se ha recopilado el grupo. <br><br>ActiveDirectory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nombre de origen de Hola que Hola grupo se recopilaron de.  Para Active Directory, se trata de nombre de dominio de Hola. |
| ManagementGroupName |Nombre del grupo de administración de Hola para agentes de SCOM.  En el caso de los otros agentes, es AOI-\<id. de área de trabajo\>. |
| TimeGenerated |Grupo de equipos de Hola de fecha y hora se creó o actualizó. |

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de [búsquedas de registro](log-analytics-log-searches.md) recopilan los datos de Hola de tooanalyze desde orígenes de datos y soluciones.  

