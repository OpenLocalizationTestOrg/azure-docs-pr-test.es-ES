---
title: "aaaManage análisis de Data Lake de Azure mediante el uso de Hola portal de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage cuentas de análisis de Data Lake, datos de orígenes, los usuarios y trabajos."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: f63ccdfae79772c92e92462194e8cdc636a73dc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-by-using-hello-azure-portal"></a>Administrar el análisis de Azure Data Lake mediante Hola portal de Azure
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Obtenga información acerca de cómo las cuentas de análisis de Azure Data Lake toomanage, orígenes de datos de cuenta, los usuarios y trabajos mediante el uso de Hola portal de Azure. temas de administración de toosee sobre el uso de otras herramientas, haga clic en una pestaña de la parte superior de Hola de página de Hola.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-lake-analytics-accounts"></a>Administración de cuentas de Data Lake Analytics

### <a name="create-an-account"></a>Crear una cuenta

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** > **Inteligencia y análisis** > **Data Lake Analytics**.
3. Seleccione los valores de hello siguientes elementos: 
   1. **Nombre**: nombre de Hola de hello cuenta de análisis de Data Lake.
   2. **Suscripción**: Hola suscripción de Azure usada para la cuenta de hello.
   3. **Grupo de recursos**: grupo de recursos de Azure de hello en qué cuenta de hello toocreate. 
   4. **Ubicación**: Hola centro de datos de Azure para la cuenta de análisis de Data Lake Hola. 
   5. **Almacén de Data Lake**: Hola toobe de almacén predeterminado utilizado por cuenta de análisis de Data Lake Hola. cuenta de almacén de Azure Data Lake de Hola y Hola cuenta debe estar en el análisis de Data Lake Hola misma ubicación.
4. Haga clic en **Crear**. 

### <a name="delete-a-data-lake-analytics-account"></a>Eliminar una cuenta de Data Lake Analytics

Para eliminar una cuenta de Data Lake Analytics, elimine la cuenta de Data Lake Store predeterminada.

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Hacer clic en **Eliminar**.
3. Nombre de cuenta de hello de tipo.
4. Hacer clic en **Eliminar**.

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-data-sources"></a>Administración de orígenes de datos

Análisis de Data Lake admite Hola siguientes orígenes de datos:

* Data Lake Store
* Azure Storage

Puede usar orígenes de datos de toobrowse de explorador de datos y realizar operaciones de administración básica de archivos. 

### <a name="add-a-data-source"></a>Agregar un origen de datos

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Orígenes de datos**.
3. Haga clic en **Agregar origen de datos**.
    
   * tooadd una cuenta de almacén de Data Lake, necesita cuenta de hello toohello de acceso y nombre de la cuenta tooquery de toobe capaz de él.
   * tooadd almacenamiento de blobs de Azure, necesitará cuenta de almacenamiento de Hola y clave de la cuenta de hello. toofind toohello de éstos, vaya cuenta de almacenamiento en el portal de Hola.

## <a name="set-up-firewall-rules"></a>Configurar reglas de firewall

Puede usar análisis de Data Lake toofurther bloquear acceso tooyour cuenta de análisis de Data Lake Hola a nivel de red. Puede habilitar un firewall, especificar una dirección IP o definir un intervalo de direcciones IP para los clientes de confianza. Después de habilitar estas medidas, solo los clientes que tengan direcciones IP de hello en el intervalo de hello definido pueden conectarse toohello almacén.

Si otros servicios de Azure, como Data Factory de Azure o máquinas virtuales, conectan la cuenta de análisis de Data Lake toohello, asegúrese de que **permitir servicios de Azure** está activado **en**. 

### <a name="set-up-a-firewall-rule"></a>Configurar una regla de firewall

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. En el menú de Hola Hola izquierda, haga clic en **Firewall**.

## <a name="add-a-new-user"></a>Agregar un nuevo usuario

Puede usar hello **Asistente para agregar usuarios** tooeasily aprovisionar nuevos usuarios de Data Lake.

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. En hello izquierdo, bajo **Introducción**, haga clic en **Asistente para agregar usuarios**.
3. Seleccione un usuario y luego haga clic en **Seleccionar**.
4. Seleccione un rol y luego haga clic en **Seleccionar**. tooset seguridad un nuevo toouse de desarrollador Azure Data Lake, seleccione hello **para desarrolladores de análisis de datos Lake** rol.
5. Seleccione las listas de control de acceso (ACL) de Hola para bases de datos de SQL U Hola. Cuando esté satisfecho con las opciones seleccionadas, haga clic en **Seleccionar**.
6. Seleccione Hola ACL para los archivos. Para el almacén predeterminado de hello, no cambie las ACL de hello para la carpeta raíz de Hola "/" y para la carpeta de Hola/sistema. Haga clic en **Seleccionar**.
7. Revise todos los cambios seleccionados y luego haga clic en **Ejecutar**.
8. Cuando finalice el Asistente de hello, haga clic en **realiza**.

## <a name="manage-role-based-access-control"></a>Administrar el control de acceso basado en roles

Al igual que otros servicios de Azure, puede usar toocontrol de Control de acceso basado en roles (RBAC) cómo los usuarios interactúan con el servicio de Hola.

los roles RBAC estándares de Hello tienen Hola siguientes capacidades:
* **Propietario**: puede enviar trabajos, supervise los trabajos, Cancelar trabajos de todos los usuarios y configurar la cuenta de hello.
* **Colaborador**: puede enviar trabajos, supervise los trabajos, Cancelar trabajos de todos los usuarios y configurar la cuenta de hello.
* **Lector**: puede supervisar trabajos.

Usar Hola para desarrolladores de análisis de datos Lake tooenable U-SQL a los desarrolladores toouse Hola análisis de Data Lake servicio de función. Puede usar papel de los desarrolladores de análisis de datos Lake Hola para:
* Enviar trabajos.
* Supervisar el progreso del trabajo hello y estado de los trabajos enviados por cualquier usuario.
* Vea las secuencias de comandos SQL U Hola de trabajos enviados por cualquier usuario.
* Cancelar solo sus propios trabajos.

### <a name="add-users-or-security-groups-tooa-data-lake-analytics-account"></a>Agregar usuarios o grupos de seguridad tooa cuenta de análisis de Data Lake

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Control de acceso (IAM)** > **Agregar**.
3. Seleccione un rol.
4. Agregue un usuario.
5. Haga clic en **Aceptar**.

>[!NOTE]
>Si un usuario o un grupo de seguridad necesita toosubmit trabajos, también necesitan el permiso en la cuenta de la tienda de Hola. Para más información, vea [Secure data stored in Data Lake Store (Protección de datos almacenados en Data Lake Store)](../data-lake-store/data-lake-store-secure-data.md).
>

<!-- ################################ -->
<!-- ################################ -->

## <a name="manage-jobs"></a>Trabajos de administración

### <a name="submit-a-job"></a>Enviar un trabajo

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.

2. Haga clic en **Nuevo trabajo**. Para cada trabajo, configure:

    1. **Nombre del trabajo**: nombre de hello del trabajo de Hola.
    2. **Prioridad**: los números más bajos tienen mayor prioridad. Si se ponen en cola dos trabajos, Hola con un valor de prioridad inferior se ejecuta primero.
    3. **Paralelismo**: número máximo de Hola de cálculo procesa tooreserve para este trabajo.

3. Haga clic en **Enviar trabajo**.

### <a name="monitor-jobs"></a>Supervisión de trabajos

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Ver todos los trabajos**. Se muestra una lista de todos los trabajos activas y finalizadas recientemente de hello en la cuenta de hello.
3. Si lo desea, haga clic en **filtro** toohelp buscar trabajos Hola por **intervalo de tiempo**, **nombre del trabajo**, y **autor** valores. 

### <a name="monitoring-pipeline-jobs"></a>Supervisión de trabajos de canalización
Trabajos que forman parte de una canalización funcionan juntos, normalmente secuencialmente, tooaccomplish un escenario concreto. Por ejemplo, puede tener una canalización que limpia, extrae, transforma y agrega el uso para información del cliente. Trabajos de canalización se identifican mediante la propiedad de la "Canalización" hello cuando se envió el trabajo de Hola. En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática. 

tooview una lista de trabajos de SQL U que forman parte de las canalizaciones: 

1. Hola portal de Azure, vaya cuentas de análisis de Data Lake tooyour.
2. Haga clic en **Información de trabajos**. Hola que se establecerá pestaña "Todos los trabajos" que muestra una lista de ejecución, en cola y había finalizado trabajos.
3. Haga clic en hello **trabajos de canalización** ficha. Se muestra una lista de trabajos de canalización junto con estadísticas agregadas de cada canalización.

### <a name="monitoring-recurring-jobs"></a>Supervisión de trabajos periódicos
Un trabajo periódico es aquel que tiene Hola misma lógica de negocios pero usa los datos de entrada diferente cada vez que se ejecuta. Idealmente, los trabajos recurrentes deberían siempre correctamente y tener tiempo de ejecución relativamente estable; supervisión de estos comportamientos servirán para asegurarse del trabajo de hello es correcto. Los trabajos recurrentes se identifican mediante la propiedad de "Recurrence" Hola. En los trabajos programados con ADF V2 esta propiedad se rellena de forma automática.

tooview una lista de trabajos U SQL que son periódicos: 

1. Hola portal de Azure, vaya cuentas de análisis de Data Lake tooyour.
2. Haga clic en **Información de trabajos**. Hola que se establecerá pestaña "Todos los trabajos" que muestra una lista de ejecución, en cola y había finalizado trabajos.
3. Haga clic en hello **trabajos recurrentes** ficha. Se muestra una lista de trabajos periódicos junto con estadísticas agregadas de cada uno de ellos.

## <a name="manage-policies"></a>Administración de directivas

### <a name="account-level-policies"></a>Directivas de nivel de cuenta

Estas directivas aplican tooall trabajos en una cuenta de análisis de Data Lake.

#### <a name="maximum-number-of-aus-in-a-data-lake-analytics-account"></a>Número máximo de unidades de análisis en una cuenta de Data Lake Analytics
Una directiva controla el número total de Hola de unidades de análisis (AUs) puede usar su cuenta de análisis de Data Lake. De forma predeterminada, el valor de Hola se establece too250. Por ejemplo, si este valor se establece too250 AUs, puede tener un trabajo en ejecución con 250 tooit AUs asignados o 10 trabajos que se ejecutan con 25 AUs cada. Trabajos adicionales que se envían se ponen en cola hasta que finalicen los trabajos en ejecución Hola. Cuando haya terminado de trabajos en ejecución, AUs se liberen para hello en cola trabajos toorun.

número de hello toochange de AUs para su cuenta de análisis de Data Lake:

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Propiedades**.
3. En **AUs máximo**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola. 
4. Haga clic en **Guardar**.

> [!NOTE]
> Si necesita más de Hola predeterminado (250) AUs, en el portal de hello, haga clic en **+ compatibilidad con la Ayuda** toosubmit una solicitud de soporte técnico. puede aumentar el número de Hola de AUs disponibles en su cuenta de análisis de Data Lake.
>

#### <a name="maximum-number-of-jobs-that-can-run-simultaneously"></a>Número máximo de trabajos que se pueden ejecutar simultáneamente
Una directiva controla cuántos trabajos pueden ejecutar en hello mismo tiempo. De forma predeterminada, este valor se establece too20. Si el análisis de Data Lake tiene AUs disponibles, nuevos trabajos son toorun programada inmediatamente hasta el número total de Hola de trabajos en ejecución alcanza el valor de Hola de esta directiva. Cuando se alcanza el número máximo de Hola de trabajos que se pueden ejecutar simultáneamente, se ponen en cola en los trabajos posteriores en orden de prioridad hasta que se completen uno o varios trabajos en ejecución (según la disponibilidad de Australia).

número de hello toochange de trabajos que se pueden ejecutar simultáneamente:

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Propiedades**.
3. En **máximo el número de trabajos ejecuta**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola. 
4. Haga clic en **Guardar**.

> [!NOTE]
> Si necesita más de Hola predeterminada (20) número de trabajos, en el portal de hello, haga clic en el toorun **+ compatibilidad con la Ayuda** toosubmit una solicitud de soporte técnico. puede aumentar el número de Hola de trabajos que se pueden ejecutar simultáneamente en su cuenta de análisis de Data Lake.
>

#### <a name="how-long-tookeep-job-metadata-and-resources"></a>¿Cuánto tiempo tookeep metadatos de trabajo y recursos 
Cuando los usuarios ejecuten trabajos SQL U, Hola servicio de análisis de Data Lake conserva todos los archivos relacionados. Archivos relacionados incluyen script de Hola U-SQL, archivos DLL de hello hace referencia en el script de Hola U-SQL, recursos compilados y estadísticas. archivos de Hello están en carpeta de /system/ Hola de cuenta de almacenamiento de Azure datos Lake Hola predeterminada. Esta directiva controla cuánto tiempo se almacenan estos recursos antes de que se eliminen automáticamente (valor predeterminado de hello es 30 días). Puede utilizar estos archivos para la depuración y para la optimización de rendimiento de trabajos que podrá volver a ejecutar en hello futuras.

toochange cuánto tookeep metadatos de trabajo y recursos:

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Propiedades**.
3. En **tooRetain días trabajo consulta**, mover el control deslizante de hello tooselect un valor o escriba el valor de hello en el cuadro de texto de Hola.  
4. Haga clic en **Guardar**.

### <a name="job-level-policies"></a>Directivas de nivel de trabajo
Con las directivas de nivel de trabajo, puede controlar Hola AUs máximos y Hola máxima prioridad que los usuarios individuales (o los miembros de grupos de seguridad específicos) pueden establecer en trabajos que envíen ellos mismos. Esto permite controlar los costos de hello producidos por los usuarios. También le permite podría tener efecto de Hola de control que los trabajos programados en alta prioridad los trabajos de producción que se ejecutan en Hola la misma cuenta de análisis de Data Lake.

Análisis de Data Lake tiene dos directivas que se pueden establecer en el nivel de trabajo de hello:

* **Límite de AU por trabajo**: los usuarios sólo pueden enviar los trabajos que tienen un número de toothis de Australia. De forma predeterminada, este límite es Hola mismo Hola Australia el límite máximo para la cuenta de hello.
* **Prioridad**: los usuarios sólo pueden enviar los trabajos que tienen un valor de prioridad toothis menores o iguales. Tenga en cuenta que un número mayor significa una prioridad más baja. De forma predeterminada, se establece too1, que es la prioridad más alta posible de Hola.

Hay una directiva predeterminada establecida en cada cuenta. directiva predeterminada de Hola aplica a los usuarios de tooall de cuenta de hello. Puede establecer directivas adicionales para usuarios y grupos concretos. 

> [!NOTE]
> Las directivas de nivel de cuenta y las directivas de nivel de trabajo se aplican de forma simultánea.
>

#### <a name="add-a-policy-for-a-specific-user-or-group"></a>Agregar una directiva para un usuario o grupo concreto

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Propiedades**.
3. En **límites de envío de trabajos**, haga clic en hello **Agregar directiva** botón. A continuación, seleccione o escriba Hola después de configuración:
    1. **Nombre de la directiva de proceso**: escriba un nombre de directiva, tooremind de propósito de Hola de directiva de Hola.
    2. **Seleccione usuario o grupo**: Seleccione usuario de Hola o grupo al que se aplica esta directiva.
    3. **Establecer Hola trabajo Australia límite**: conjunto Hola Australia se aplica un límite toohello selecciona usuario o grupo.
    4. **Establecer límite de prioridad de Hola**: conjunto Hola prioridad se aplica un límite toohello selecciona usuario o grupo.

4. Haga clic en **Aceptar**.

5. Hola nueva directiva se muestra en hello **predeterminado** en directiva de tabla **límites de envío de trabajos**. 

#### <a name="delete-or-edit-an-existing-policy"></a>Eliminar o editar una directiva existente

1. Hola portal de Azure, vaya tooyour cuenta de análisis de Data Lake.
2. Haga clic en **Propiedades**.
3. En **límites de envío de trabajos**, directiva de Hola de búsqueda que desee tooedit.
4.  Hola toosee **eliminar** y **editar** haga clic en Opciones, en la columna situada más a Hola de tabla de hello, **...** .

### <a name="additional-resources-for-job-policies"></a>Recursos adicionales para directivas de trabajo
* [Entrada de blog de información general sobre directivas](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-overview/)
* [Entrada de blog sobre directivas de nivel de cuenta](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-account-level-policy/)
* [Entrada de blog sobre directivas de nivel de trabajo](https://blogs.msdn.microsoft.com/azuredatalake/2017/06/08/managing-your-azure-data-lake-analytics-compute-resources-job-level-policy/)

## <a name="next-steps"></a>Pasos siguientes

* [Información general de Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Empezar a trabajar con análisis de Data Lake utilizando Hola portal de Azure](data-lake-analytics-get-started-portal.md)
* [Manage Azure Data Lake Analytics by using Azure PowerShell](data-lake-analytics-manage-use-powershell.md) (Administración de Azure Data Lake Analytics mediante Azure PowerShell)

