---
title: "Azure AD Connect sync: descripción de la arquitectura de hello | Documentos de Microsoft"
description: "En este tema se describe la arquitectura de Hola de sincronización de Azure AD Connect y explica Hola términos que se usan."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Azure AD Connect sync: descripción de la arquitectura de Hola
Este tema trata la arquitectura básica de hello sincronización de Azure AD Connect. En muchos aspectos, es similar predecesores de tooits MIIS 2003, 2007 de ILM y FIM 2010. Azure AD Connect sync es la evolución de Hola de estas tecnologías. Si está familiarizado con cualquiera de estas tecnologías anteriores, el contenido de Hola de este tema estará familiarizado tooyou así. Si está toosynchronization nuevo, este tema es para usted. Sin embargo no es un detalles de hello tooknow los requisitos de este toobe tema correcta para realizar personalizaciones tooAzure AD Connect sync (motor de sincronización llamado en este tema).

## <a name="architecture"></a>Arquitectura
motor de sincronización de Hello crea una vista integrada de objetos que se almacenan en varios orígenes de datos conectados y administra información de identidad en los orígenes de datos. Esta vista integrada viene determinada por la información de identidad de hello recuperada de orígenes de datos conectados y un conjunto de reglas que determinan cómo tooprocess esta información.

### <a name="connected-data-sources-and-connectors"></a>Orígenes de datos conectados y conectores
motor de sincronización de Hello procesa la información de identidad desde repositorios de datos diferentes, como Active Directory o una base de datos de SQL Server. Cada repositorio de datos que organiza sus datos en un formato de base de datos y que proporciona métodos de acceso a datos estándar es un candidato potencial de origen de datos de motor de sincronización de Hola. los repositorios de Hello datos que se sincronizan mediante el motor de sincronización se denominan **orígenes de datos conectados** o **conectado directorios** (CD).

motor de sincronización de Hello encapsula la interacción con un origen de datos conectado dentro de un módulo denominado un **conector**. Cada tipo de origen de datos conectado posee un conector específico. Hola conector traduce una operación necesaria en formato Hola Hola datos conectados se entiende origen.

Los conectores hacen llamadas API tooexchange información de identidad (de lectura y escritura) con un origen de datos conectado. También es posible tooadd un conector personalizado mediante el marco de trabajo de hello conectividad extensible. Hello en la ilustración siguiente se muestra cómo un conector conecta a un motor de sincronización de toohello de origen de datos conectado.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Los datos pueden fluir en ambas direcciones, pero no simultáneamente. En otras palabras, un conector puede ser configurado tooallow tooflow de datos de motor de toosync de origen de datos conectado de Hola o de origen de datos conectado de toohello de motor de sincronización, pero solo una de esas operaciones puede producirse en cualquier momento para un objeto y atributo. dirección de Hello puede ser diferente para los distintos objetos y para diferentes atributos.

tooconfigure un conector, especificar tipos de objeto de Hola que desea toosynchronize. Especificar los tipos de objeto de hello define el ámbito de Hola de objetos que se incluyen en el proceso de sincronización de Hola. Hola siguiente paso es tooselect Hola atributos toosynchronize, lo que se conoce como una lista de inclusión del atributo. Esta configuración se puede cambiar en cualquier momento en las reglas de negocios de respuesta toochanges tooyour. Cuando se utiliza el Asistente para la instalación de Azure AD Connect de hello, estas opciones se configuran automáticamente.

origen de datos conectado de tooexport objetos tooa, lista de inclusión del atributo de hello debe incluir al menos Hola mínimo atributos toocreate requiere un objeto específico que se escriba en un origen de datos conectado. Por ejemplo, hello **sAMAccountName** atributo se debe incluir en tooexport de lista de inclusión de atributo de hello un objeto user para tooActive directorio porque todos los objetos de usuario en Active Directory deben tener un **sAMAccountName**  atributo definido. Una vez más, Asistente para la instalación de hello realiza esta configuración automáticamente.

Si el origen de datos conectado hello usa los componentes estructurales, como los objetos de tooorganize particiones o contenedores, puede limitar las áreas de hello en el origen de datos conectado de Hola que sirven para una solución dada.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Estructura interna del espacio de nombres del motor de sincronización de Hola
espacio de nombres del motor de sincronización completa de Hello consta de dos espacios de nombres que almacenan información de identidad de Hola. Hola dos espacios de nombres son:

* espacio de conector de Hello (CS)
* Hola metaverse (MV)

Hola **espacio conector** es un área de ensayo que contiene representaciones de hello designado objetos desde una atributos de hello y origen de datos conectado especificado en la lista de inclusión del atributo de Hola. motor de sincronización de Hello usa toodetermine de espacio de conector de hello qué ha cambiado en datos Hola conectado origen y toostage cambios entrantes. motor de sincronización de Hello también utiliza Hola conector espacio toostage cambios de origen de datos conectado toohello de exportación de salida. motor de sincronización de Hello mantiene un espacio de conector distintos como un área de ensayo para cada conector.

Mediante el uso de un área de almacenamiento provisional, motor de sincronización de hello permanece independiente Hola conectado de orígenes de datos y no se ve afectada por su disponibilidad y la accesibilidad. Como resultado, puede procesar la información de identidad en cualquier momento mediante datos de hello en el área de ensayo de Hola. motor de sincronización de Hello puede solicitar solo Hola cambios dentro de origen de datos conectado Hola desde Hola última sesión de comunicación terminado o inserción solo información de tooidentity de cambios de Hola que Hola origen de datos conectado aún no ha recibido, lo que reduce tráfico de red de Hello entre el motor de sincronización de Hola y el origen de datos conectado Hola.

Además, el motor de sincronización almacena información de estado sobre todos los objetos que cree etapas en el espacio del conector de Hola. Cuando se reciben nuevos datos, el motor de sincronización siempre evalúa si ya se ha sincronizado datos Hola.

Hola **metaverso** es un área de almacenamiento que contiene la información de identidad de hello agregado desde varios orígenes de datos conectado, proporcionar una sola vista integrada, global de todos los objetos combinados. Los objetos de metaverso se crean en función de la información de identidad de Hola que se recupera de hello conectado los orígenes de datos y un conjunto de reglas que permitan el proceso de sincronización de toocustomize Hola.

Hello mostramos aquí espacios de nombres de espacio de conector de Hola y Hola metaverso dentro de motor de sincronización de Hola.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Objetos de identidad del motor de sincronización
objetos de Hello en el motor de sincronización de hello son representaciones de objetos de origen de datos conectado de Hola o hello vista integrada que el motor de sincronización tiene de dichos objetos. Cada objeto de motor de sincronización debe tener un identificador único global (GUID). Los GUID proporcionan integridad a los datos y expresan relaciones entre objetos.

### <a name="connector-space-objects"></a>Objetos del espacio conector
Cuando el motor de sincronización se comunica con un origen de datos conectado, lee la información de identidad de hello en el origen de datos conectado de Hola y utiliza esa toocreate información una representación de objeto de identidad de hello en el espacio del conector de Hola. No se pueden crear ni eliminar estos objetos individualmente. Sin embargo, puede eliminar manualmente todos los objetos en un espacio conector.

Todos los objetos de espacio de conector de hello tienen dos atributos:

* Un identificador único global (GUID)
* Un nombre distintivo (también conocido como DN)

Si Hola conectado origen de datos asigna un objeto de atributo único toohello, objetos en el espacio de conector de hello también pueden tener un atributo de delimitador. atributo de delimitador de Hello identifica de forma única un objeto de origen de datos conectado Hola. motor de sincronización de Hello usa Hola delimitador toolocate Hola correspondiente representación de este objeto de origen de datos conectado Hola. Motor de sincronización se da por supuesto que fijan Hola de un objeto nunca cambios a través de la duración de Hola de objeto de Hola.

Muchos de los conectores de hello usan un toogenerate un delimitador de identificador único conocido automáticamente para cada objeto cuando se haya importado. Por ejemplo, hello conector de Active Directory utiliza hello **objectGUID** atributo para un delimitador. Para orígenes de datos conectados que no proporcionan un identificador único claramente definido, puede especificar generación delimitador como parte de la configuración del conector de Hola.

Caso, delimitador de Hola se crea a partir de uno o más atributos únicos de un objeto de tipo, ninguno de los cambios y que forma única que identifica el objeto de hello en el espacio de conector de hello (por ejemplo, un número de empleado o un identificador de usuario).

Un objeto de espacio de conector puede ser uno de hello siguientes:

* Un objeto de almacenamiento provisional
* Un marcador de posición

### <a name="staging-objects"></a>Objetos de almacenamiento provisional
Un objeto de almacenamiento provisional representa una instancia de hello designado tipos de objeto de origen de datos conectado Hola. Además toohello GUID y el nombre distintivo de hello, un objeto de almacenamiento provisional siempre tiene un valor que indica el tipo de objeto de Hola.

Objetos de almacenamiento provisional que se han importado siempre tienen un valor de atributo de delimitador de Hola. Objetos de almacenamiento provisional que recientemente se ha aprovisionado el motor de sincronización y están en proceso de Hola de que se creen en el origen de datos conectado de Hola no tienen un valor de atributo de delimitador de Hola.

Objetos de almacenamiento provisional también mantienen los valores actuales de los atributos de negocios y obtener información operativa necesaria para el proceso de sincronización de Hola de tooperform de motor de sincronización. Información operativa incluye marcas que indican el tipo de saludo de actualizaciones que se almacenan en el objeto de almacenamiento provisional de Hola. Si un objeto de almacenamiento provisional ha recibido la nueva información de identidad de origen de datos conectado de Hola que todavía no se han procesado, objeto de Hola se marca como **importación pendiente**. Si un objeto de almacenamiento provisional tiene nueva información de identidad que aún no se ha exportado toohello origen de datos conectado, se marca como **pendientes exportación**.

Un objeto de almacenamiento provisional puede ser un objeto de importación o de exportación. motor de sincronización de Hello crea un objeto de importación mediante el uso de información sobre los objetos recibido del origen de datos conectado Hola. Cuando el motor de sincronización recibe información sobre la existencia de Hola de un nuevo objeto que coincide con uno de los tipos de objeto de hello seleccionados en hello conector, crea un objeto de importación en el espacio del conector de Hola como una representación del objeto de hello en el origen de datos conectado de Hola.

Hola sigue en la ilustración muestra un objeto de importación que representa un objeto de origen de datos conectado Hola.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

motor de sincronización de Hello crea un objeto de exportación con información de objeto de metaverso Hola. Exportar los objetos son origen de datos conectado toohello exportados durante la siguiente sesión de comunicación de Hola. Desde la perspectiva de Hola de motor de sincronización de hello, exportar los objetos no existen en el origen de datos conectado Hola todavía. Por lo tanto, el atributo de delimitador de Hola para un objeto de exportación no está disponible. Después de recibir el objeto de Hola desde el motor de sincronización, origen de datos conectado Hola crea un valor único para el atributo de delimitador de hello del objeto de Hola.

Hello en la ilustración siguiente se muestra cómo se crea un objeto de la exportación mediante el uso de información de identidad en el metaverso Hola.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

motor de sincronización de Hello confirma la exportación Hola del objeto de Hola volviendo a importar objetos de Hola Hola origen de datos conectado. Exportar los objetos se convierten en objetos de importación al motor de sincronización los recibe durante la importación del siguiente Hola de ese origen de datos conectado.

### <a name="placeholders"></a>Marcadores de posición
motor de sincronización de Hello usa un espacio de nombres plano toostore los objetos. Sin embargo, algunos orígenes de datos conectados, como Active Directory, usan un espacio de nombres jerárquico. información de tootransform de espacio de nombres jerárquico en un espacio de nombres sin formato, motor de sincronización utiliza la jerarquía de Hola de toopreserve de marcadores de posición.

Cada marcador de posición representa un componente (por ejemplo, una unidad organizativa) de nombre jerárquico de un objeto que no se ha importado en el motor de sincronización, pero es necesario tooconstruct Hola jerárquica nombre. Se rellenan brechas creadas por referencias en tooobjects de origen de datos de hello conectado que no son objetos en el espacio de conector de Hola de ensayo.

motor de sincronización de Hello también utiliza objetos de toostore hace referencia a los marcadores de posición que aún no se ha importado. Por ejemplo, si la sincronización es atributo de administrador de hello tooinclude configurado para hello *Abbie Spencer* objeto y hello valor recibido es un objeto que no se ha importado aún, como *CN = Lee Sperry, CN = Users, DC = fabrikam, DC = com*, se almacena información del Administrador de hello como marcadores de posición en el espacio de conector de Hola. Si más adelante se importa el objeto de administrador de hello, objeto de marcador de posición de hello sobrescribe Hola objeto que representa el Administrador de Hola de almacenamiento provisional.

### <a name="metaverse-objects"></a>Objetos del metaverso
Un objeto de metaverso contiene Hola agregado vista tiene ese motor de sincronización del programa Hola a objetos en el espacio de conector de Hola de almacenamiento provisional. Motor de sincronización crea los objetos de metaverso con información de hello en Importar objetos. Varios objetos del espacio de conector pueden ser objeto de metaverso único tooa vinculado, pero un objeto de espacio de conector no puede ser toomore vinculado a un objeto de metaverso.

Los objetos de metaverso no se pueden crear ni eliminar manualmente. motor de sincronización de Hello elimina automáticamente los objetos de metaverso que no tienen un objeto de espacio de conector de tooany de vínculo en el espacio del conector de Hola.

toomap objetos dentro de un tipo de objeto correspondiente de tooa de origen de datos conectado dentro de metaverso de hello, el motor de sincronización proporciona un esquema extensible con un conjunto predefinido de tipos de objetos y atributos asociados. Puede crear nuevos tipos de objeto y atributos para los objetos de metaverso. Atributos pueden tener un valor único o varios valores y tipos de atributo de hello pueden ser cadenas, referencias, números y valores booleanos.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relaciones entre los objetos de almacenamiento provisional y los objetos de metaverso
En el espacio de nombres de motor de sincronización de hello, está habilitado el flujo de datos de Hola por relación de vínculo de hello entre los objetos de almacenamiento provisionales y los objetos de metaverso. Objeto de un almacenamiento provisional que se se denomina objeto de metaverso vinculado tooa una **Unidos a un objeto** (o **objeto conector**). Se llama a un objeto de almacenamiento provisional que no es objeto de metaverso vinculado tooa una **separado objeto** (o **objeto desconector**). términos de Hello Unido y toonot preferido separado se confunda con hello conectores responsables de importación y exportación de datos desde un directorio conectado.

Marcadores de posición nunca son objeto de metaverso tooa vinculado

Un objeto unido consta de un objeto de almacenamiento provisional y su objeto de metaverso único tooa relación vinculado. Objetos combinados son valores de atributo utilizados toosynchronize entre un objeto de espacio de conector y un objeto de metaverso.

Cuando un objeto de almacenamiento provisional se convierte en un objeto combinado durante la sincronización, los atributos pueden fluir entre Hola Hola metaverso objetos y almacenamiento provisional. El flujo de atributos es bidireccional y se configura mediante reglas de atributo de importación y de atributo de exportación.

Un objeto de espacio único conector puede ser objeto de metaverso una tooonly vinculado. Sin embargo, cada objeto de metaverso puede ser objetos del espacio de conector toomultiple vinculado en hello mismo o en espacios de conectores diferentes, como se muestra en hello siguiente ilustración.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Hola vinculada relación entre el objeto de almacenamiento provisional de Hola y un objeto de metaverso es persistente y se puede quitar únicamente por reglas que especifique.

Un objeto separado es un objeto de almacenamiento provisional que no es objeto de metaverso tooany vinculado. atributo Hola valores de un objeto separado no son procesados irá más allá de metaverso Hola. Hola atributo no se actualizan los valores de objeto correspondiente de hello en el origen de datos conectado Hola por el motor de sincronización.

Mediante el uso de objetos separados, puede almacenar información de identidad en el motor de sincronización y procesarla más adelante. Mantener un objeto de almacenamiento provisional como un objeto separado en el espacio de conector de hello tiene muchas ventajas. Dado que system Hola ya ha almacenado provisionalmente información Hola necesario sobre este objeto, no es necesario toocreate a continuación importar una representación de este objeto durante Hola Hola origen de datos conectado. De esta manera, el motor de sincronización siempre tiene una instantánea completa del origen de datos conectado hello, incluso si no hay ningún origen de datos conectado de toohello de conexión actual. Objetos separados se pueden convertir en objetos combinados y viceversa, según las reglas de Hola que especifique.

Un objeto de importación se crea como objeto separado. A cambio, un objeto de exportación debe ser un objeto unido. lógica del sistema Hola aplica esta regla y elimina todos los objetos de exportación no es un objeto combinado.

## <a name="sync-engine-identity-management-process"></a>Proceso de administración de identidad del motor de sincronización
proceso de administración de identidades de Hello controla cómo se actualiza la información de identidad entre orígenes de datos conectados diferentes. La administración de identidad se produce en tres procesos:

* Importación
* Sincronización
* Exportación

Durante el proceso de importación de hello, el motor de sincronización se evalúa como Hola entrantes información de identidad para un origen de datos conectado. Cuando se detectan cambios, crea nuevos objetos de almacenamiento provisionales o actualiza los objetos de almacenamiento provisionales existentes en el espacio de conector de hello para la sincronización.

Durante el proceso de sincronización de hello, motor de sincronización actualiza Hola metaverso tooreflect cambios que se han producido en el espacio del conector de Hola y actualiza Hola conector espacio tooreflect cambios que se han producido en el metaverso Hola.

Durante el proceso de exportación de hello, motor de sincronización se inserta los cambios que se almacenan en objetos de almacenamiento provisional y que se marcan como pendientes de exportación.

Hola sigue en la ilustración muestra donde cada uno de los procesos de Hola se produce cuando los flujos de información de identidad de tooanother de origen de datos conectado.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Proceso de importación
Durante el proceso de importación de hello, motor de sincronización, se evalúa como tooidentity se actualiza la información. Motor de sincronización compara la información de identidad de hello recibida del origen de datos conectado Hola con información de identidad de hello sobre un objeto de almacenamiento provisional y determina si Hola ensayo objeto requiere que las actualizaciones. Si es hello tooupdate necesarios objeto con los nuevos datos de almacenamiento provisional, Hola objeto de almacenamiento provisional se marca como pendiente de importación.

Organizando los objetos en el espacio de conector de hello antes de la sincronización, el motor de sincronización puede procesar únicamente información de identidad de Hola que ha cambiado. Este proceso proporciona Hola siguientes ventajas:

* **Sincronización eficiente**. se minimiza la cantidad de Hola de datos procesadas durante la sincronización.
* **Resincronización eficiente**. Puede cambiar cómo el motor de sincronización procesa la información de identidad sin origen de datos de toohello de motor de sincronización de reconexión Hola.
* **Sincronización de oportunidad toopreview**. Puede obtener una vista previa de tooverify de sincronización que sus suposiciones sobre el proceso de administración de identidades de hello son correctos.

Para cada objeto especificado en hello conector, motor de sincronización de hello trate toolocate una representación del objeto de hello en el espacio de conector de Hola de hello conector. Motor de sincronización examina todos los objetos de almacenamiento provisionales en el espacio del conector de Hola y trata de toofind un objeto de almacenamiento provisional correspondiente que tiene un atributo delimitador coincidente. Si ningún objeto de almacenamiento provisional existente tiene una coincidencia delimitar atributo, sincronizar motor intentos toofind un objeto de almacenamiento provisional correspondiente con hello igual nombre distintivo.

Cuando el motor de sincronización encuentra un objeto de almacenamiento provisional que coincide con nombre distintivo, pero no por delimitador, hello especial ocurre siguiente:

* Si objeto Hola ubicado en el espacio de conector de hello no tiene ningún delimitador, a continuación, motor de sincronización quita este objeto de espacio de conector de Hola y marcas Hola objeto de metaverso es vinculado tooas **reintentará el aprovisionamiento en la siguiente sincronización ejecutar**. A continuación, crea Hola nuevo objeto de importación.
* Si el objeto Hola ubicado en el espacio de conector de hello tiene un anclaje, motor de sincronización se supone que este objeto se ha cambiado el nombre o eliminado en el directorio conectado Hola. Asigna un nombre distintivo temporal, nueva para el objeto de espacio de conector de Hola para que puede realizar copias intermedias de objeto de Hola entrantes. Hello objeto anterior, a continuación, se convierte en **transitorio**, esperando Hola conector tooimport Hola cambiarle el nombre o eliminación tooresolve Hola situación.

Si el motor de sincronización encuentra un objeto de almacenamiento provisional que corresponde el objeto toohello especificado en hello conector, determina qué tipo de cambios tooapply. Por ejemplo, motor de sincronización podría cambiar el nombre o eliminar objetos de hello en el origen de datos conectado de hello, o solo pueden actualizar los valores de atributo del objeto de Hola.

Los objetos de almacenamiento provisional con datos actualizados se marcan como pendientes de importación. Existen distintos tipos de importación pendiente. Según el resultado de hello de proceso de importación de hello, un objeto de almacenamiento provisional en el espacio del conector de hello tiene uno de los siguientes tipos de importación pendiente de hello:

* **Ninguna**. No tooany de cambios de los atributos de Hola de objeto de almacenamiento provisional de hello están disponibles. El motor de sincronización no marca este tipo como pendiente de importación.
* **Agregar**. Hola, objeto de almacenamiento provisional es un nuevo objeto de importación en el espacio de conector de Hola. Motor de sincronización marca este tipo como pendientes de importación para su procesamiento adicional en el metaverso Hola.
* **Actualizar**. Motor de sincronización encuentra un objeto de almacenamiento provisional correspondiente en el espacio de conector de Hola y marcas de este tipo como importación pendiente para que las actualizaciones toohello atributos se pueden procesar en hello metaverso. Entre las actualizaciones, se incluye el cambio de nombre del objeto.
* **Eliminar**. Motor de sincronización encuentra un objeto de almacenamiento provisional correspondiente en el espacio de conector de Hola y marcas de este tipo como importación pendiente para que hello Unidos a un objeto se puede eliminar.
* **Eliminar o agregar**. Motor de sincronización encuentra un objeto de almacenamiento provisional correspondiente en el espacio del conector de hello, pero los tipos de objeto de hello no coinciden. En este caso, se almacena provisionalmente una modificación de tipo Eliminar o agregar. Agregar por delete A modificación indica toohello motor de sincronización que debe realizarse una resincronización completa de este objeto porque diferentes conjuntos de reglas aplican toothis objeto cuando cambia el tipo de objeto de Hola.

Al establecer Hola pendiente de estado de la importación de un objeto de almacenamiento provisional, es posible tooreduce Hola significativamente la cantidad de datos procesadas durante la sincronización porque si lo hace, Hola sistema tooprocess solo aquellos objetos que se han actualizado los datos.

### <a name="synchronization-process"></a>Proceso de sincronización
La sincronización consta de dos procesos relacionados:

* Sincronización de entrada, cuando se actualizó el contenido de Hola de metaverso de hello mediante datos de Hola de espacio de conector de Hola.
* Sincronización de salida, cuando se actualizó el contenido de Hola de espacio de conector de hello mediante datos de metaverso de Hola.

Mediante la información de hello provisionalmente en el espacio del conector de hello, hello proceso de sincronización de entrada crea en Hola metaverso Hola integrado vista de datos de Hola que se almacenan en orígenes de datos de hello conectado. Dependiendo de cómo se configuran las reglas de hello, se agregan todos los objetos de almacenamiento provisionales o sólo aquellos que tengan una información de importación pendiente.

las actualizaciones de proceso de sincronización de salida de Hello exportación objetos cuando cambian los objetos de metaverso.

Sincronización de entrada crea la vista de hello integrado en el metaverso Hola Hola de información de identidad que se recibe desde orígenes de datos de hello conectado. Motor de sincronización puede procesar la información de identidad en cualquier momento mediante Hola la información de identidad más reciente que ha de hello origen de datos conectado.

**Sincronización de entrada**

Sincronización de entrada incluye Hola siguientes procesos:

* **Aprovisionar** (también denominada **proyección** si es importante toodistinguish este proceso de aprovisionamiento de sincronización de salida). motor de sincronización de Hello crea un nuevo objeto de metaverso basándose en un objeto de almacenamiento provisional y vínculos a ellos. El aprovisionamiento es una operación de nivel de objeto.
* **Unión**. motor de sincronización de Hello vincula un ensayo objeto tooan existente objeto de metaverso. La unión es una operación de nivel de objeto.
* **Flujo de atributos de importación**. Motor de sincronización actualiza los valores de atributo de hello, denominados flujo de atributo, del objeto de Hola Hola metaverso. El flujo de atributos de importación es una operación de nivel de atributo que requiere un vínculo entre un objeto de almacenamiento provisional y un objeto de metaverso.

El aprovisionamiento es Hola único proceso que crea objetos de metaverso Hola. afecta solamente a los objetos de importación que sean objetos separados. Durante el aprovisionamiento, motor de sincronización crea un objeto de metaverso correspondiente toohello tipo de objeto de la importación de Hola y establece un vínculo entre los objetos, lo que crea un objeto combinado.

proceso de combinación de Hello también establece un vínculo entre los objetos de importación y un objeto de metaverso. diferencia de Hello entre join y aprovisionar es que el proceso de incorporación de Hola requiere ese objeto de importación de hello son objeto de metaverso existente tooan vinculado, donde el proceso de aprovisionamiento de hello crea un nuevo objeto de metaverso.

Motor de sincronización intenta toojoin un objeto de metaverso de importación objeto tooa mediante criterios que se especifica en configuración de la regla de sincronización de Hola.

Durante el aprovisionamiento de Hola y los procesos de combinación, el motor de sincronización vincula un objeto de metaverso de tooa objeto separados, haciéndolos unido. Después de que se completen estas operaciones de nivel de objeto, el motor de sincronización puede actualizar valores de atributo de hello del objeto de metaverso asociado Hola. Este proceso se denomina flujo de atributos de importación.

Flujo de atributos de importación se produce en todos los objetos de importación que transportan datos nuevos y son objeto de metaverso tooa vinculado.

**Sincronización de salida**

La sincronización de salida actualiza los objetos de exportación cuando un objeto de metaverso cambia pero no se elimina. objetivo de Hola de sincronización de salida es tooevaluate si los objetos de toometaverse cambios requieren actualizaciones toostaging objetos en espacios de conectores de Hola. En algunos casos, se actualizará Hola cambios pueden requerir que los objetos de almacenamiento provisional en todos los espacios conectores. Los objetos de almacenamiento provisional que se cambian se marcan como pendientes de exportación, lo que los convierte en objetos de exportación. Estos objetos más adelante se resaltan los origen de datos conectado toohello durante el proceso de exportación de Hola de exportación.

La sincronización de salida consta de tres procesos:

* **Aprovisionamiento**
* **Desaprovisionamiento**
* **Flujo de atributos de exportación**

Tanto el aprovisionamiento como el desaprovisionamiento son operaciones de nivel de objeto. El desaprovisionamiento depende del aprovisionamiento porque solo lo puede iniciar este último. Desaprovisionamiento se desencadena cuando se aprovisionen quita Hola vínculo entre un objeto de metaverso y un objeto de la exportación.

Aprovisionamiento siempre se desencadena cuando los cambios son tooobjects aplicados en el metaverso Hola. Cuando se realizan cambios toometaverse objetos, motor de sincronización puede realizar cualquiera de hello siguiente las tareas como parte del proceso de aprovisionamiento de hello:

* Crear objetos combinados, donde un objeto de metaverso es objeto de la exportación de vinculado tooa recién creado.
* Cambiar el nombre de un objeto unido.
* Separar los vínculos entre un objeto de metaverso y objetos de almacenamiento provisional, lo que crea un objeto separado.

Si aprovisionamiento requiere el motor de sincronización toocreate un nuevo objeto de conector, hello objeto de metaverso de hello toowhich de objeto de almacenamiento provisional es vinculado siempre es un objeto de la exportación, porque aún no existe en el origen de datos conectado Hola objeto Hola.

Si el aprovisionamiento de requiere el motor de sincronización toodisjoin un objeto combinado, crea un objeto separado, se desencadena el desaprovisionamiento. proceso de desaprovisionamiento de Hello elimina el objeto de Hola.

Durante la cancelación, la eliminación de un objeto de exportación no elimina físicamente objeto Hola. Hello objeto tiene una marca que **eliminar**, lo que significa que esa operación de eliminación de Hola se almacenan provisionalmente en objeto Hola.

Flujo de atributos de exportación también se produce durante el proceso de sincronización de salida de hello, manera toohello similar que Importar flujo de atributo que se produce durante la sincronización de entrada. El flujo de atributos de exportación se produce solamente entre los objetos de metaverso y de exportación que están unidos.

### <a name="export-process"></a>Proceso de exportación
Durante el proceso de exportación de hello, motor de sincronización examina todos los objetos de exportación que están marcados como pendientes de exportación en el espacio del conector de hello y, a continuación, envía las actualizaciones toohello conecta el origen de datos.

motor de sincronización de Hello puede determinar el éxito de Hola de una exportación pero suficientemente no puede determinar que el proceso de administración de identidades de hello está completa. Objetos de origen de datos conectado Hola siempre se pueden cambiar por otros procesos. Porque el motor de sincronización no tiene un origen de datos conectado toohello conexión persistente, no es suficiente suposiciones toomake acerca de las propiedades de un objeto de origen de datos conectado Hola basándose únicamente en una notificación de exportación correcta Hola.

Por ejemplo, un proceso en hello origen de datos conectado pudieron atributos del objeto de cambio Hola hacer copia de los valores originales de tootheir (es decir, origen de datos conectado Hola podría sobrescribir los valores de hello inmediatamente después de que se insertan datos de hello alejar el motor de sincronización y correctamente se aplica en el origen de datos conectado hello).

almacenes de motor de sincronización de Hello exportación e importación información de estado acerca de cada objeto de almacenamiento provisional. Si los valores de atributos de Hola que se especifican en la lista de inclusión del atributo de hello han cambiado desde la última exportación de hello, Hola almacenamiento de importación y exportación tooreact de motor de sincronización de estado habilita adecuadamente. Motor de sincronización utiliza Hola importación proceso tooconfirm valores de atributo que se han exportado toohello origen de datos conectado. Una comparación entre Hola importado y la información exportada, como se muestra en hello después de ilustración, permite toodetermine de motor de sincronización si la exportación de hello tuvo éxito o si necesita toobe repetido.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Por ejemplo, si el motor de sincronización exporta atributo C, que tiene un valor de 5, tooa de origen de datos conectado, C = 5 almacena en su memoria de estado de exportación. Cada exportación adicional en este objeto da como resultado un origen de datos conectado intento tooexport C = 5 toohello nuevo porque el motor de sincronización se da por supuesto que este valor no ha sido objeto de forma persistente aplicada toohello (es decir, a menos que un valor diferente se importó recientemente de hello origen de datos conectado). memoria de exportación de Hola se borra cuando C = 5 se recibe durante una operación de importación en el objeto de Hola.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

