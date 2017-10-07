---
title: Conector de SQL aaaGeneric | Documentos de Microsoft
description: "Este artículo se describe cómo conector de SQL genérico de Microsoft tooconfigure."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Referencia técnica del conector de SQL genérico
Este artículo describe Hola conector de SQL genérico. artículo de Hola aplica toohello siguientes productos:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Debe usar la revisión 4.1.3671.0 o posterior ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Para MIM2016 y FIM2010R2, está disponible como una descarga de Hola Hola conector [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee este conector en acción, vea hello [paso a paso de conector de SQL genérico](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) artículo.

## <a name="overview-of-hello-generic-sql-connector"></a>Información general de hello conector de SQL genérico
Hola conector de SQL genérico permite servicio de sincronización de hello toointegrate con un sistema de base de datos que ofrece conectividad ODBC.  

Desde una perspectiva de alto nivel, Hola siguientes características es compatibles con la versión actual de Hola de conector de hello:

| Característica | Soporte técnico |
| --- | --- |
| Origen de datos conectado |Hola conector es compatible con todos los controladores ODBC de 64 bits. Se ha probado con siguiente hello: <li>Microsoft SQL Server y SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 y 11g</li><li>MySQL 5.x</li> |
| Escenarios |<li>Administración del ciclo de vida de objetos</li><li>Administración de contraseñas</li> |
| Operaciones |<li>Importación completa e importación diferencial, exportación</li><li>Para la exportación: agregar, eliminar, actualizar y reemplazar</li><li>Establecer contraseña, cambiar contraseña</li> |
| Esquema |<li>Detección dinámica de objetos y atributos</li> |

### <a name="prerequisites"></a>Requisitos previos
Antes de usar Hola conector, asegúrese de que tiene Hola siguientes en el servidor de sincronización de hello:

* Microsoft .NET 4.5.2 Framework o posterior
* Controladores cliente ODBC de 64 bits

### <a name="permissions-in-connected-data-source"></a>Permisos en origen de datos conectado
toocreate o para realizar cualquiera de las tareas de hello admite en Conector de SQL genérico, debe tener:

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Puertos y protocolos
Para puertos de hello necesarios para hello ODBC driver toowork, consulte la documentación del proveedor de la base de datos de Hola.

## <a name="create-a-new-connector"></a>Creación de un nuevo conector
tooCreate un conector de SQL genérico, en **servicio de sincronización de** seleccione **Management Agent** y **crear**. Seleccione hello **(Microsoft) de SQL genérico** conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Conectividad
Hola conector usa un archivo de DSN de ODBC para la conectividad. Crear archivo DSN de hello mediante **orígenes de datos ODBC** se encuentra en el menú Inicio, hello en **herramientas administrativas**. En la herramienta administrativa de hello, cree un **DSN de archivo** por lo que puede proporcionarse toohello conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

pantalla de bienvenida conectividad es hello en primer lugar cuando se crea un nuevo conector de SQL genérico. Primero debe hello tooprovide siguiente información:

* Ruta de acceso de archivo DSN
* Autenticación
  * User Name
  * Password

base de datos de Hello debe admitir uno de estos métodos de autenticación:

* **Autenticación de Windows**: Hola autenticación de base de datos utiliza credenciales de Windows de hello tooverify usuario de Hola. Hola nombre de usuario/contraseña especificada es tooauthenticate utilizado con la base de datos de Hola. Esta cuenta necesita la base de datos de toohello de permisos.
* **Autenticación de SQL**: Hola autenticar el nombre de usuario de Hola de base de datos utiliza/contraseña definida una Hola conectividad pantalla tooconnect toohello base de datos. Si almacena Hola nombre de usuario/contraseña en archivo DSN de Hola, credenciales de hello proporcionadas en la pantalla de bienvenida conectividad tienen prioridad.
* **Autenticación de base de datos de SQL Azure**: para obtener más información, consulte [conectar tooSQL base de datos mediante Active Directory autenticación de Azure](../../sql-database/sql-database-aad-authentication.md).

**DN es delimitador**: Si selecciona esta opción, Hola DN también se usa como atributo de delimitador de Hola. Puede usarse para una implementación sencilla pero también tiene Hola siguiente limitación:

* El conector solo admite un tipo de objeto. Por lo tanto, cualquier referencia solo pueden hacer referencia a atributos Hola mismo tipo de objeto.

**Tipo de exportación: Objeto reemplazar**: durante la exportación, cuando han cambiado sólo algunos atributos, se exporta el objeto completo de Hola a todos los atributos y reemplaza Hola objeto existente.

### <a name="schema-1-detect-object-types"></a>Esquema 1 (Detectar tipos de objeto)
En esta página, que va tooconfigure cómo hello conector es continuo toofind Hola distintos tipos de objetos de base de datos de Hola.

Cada tipo de objeto se presenta como una partición y se configura más adelante en **Configurar particiones y jerarquías**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Método de detección de tipo de objeto**: Hola conector es compatible con estos métodos de detección del tipo de objeto.

* **Valor fijo**: deberá proporcionar Hola lista de tipos de objeto con una lista separada por comas. Por ejemplo: `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Tabla/vista/Stored Procedure**: proporcionar nombre de Hola de hello tabla/procedimiento almacenado/vista y, a continuación, en nombre de la columna de Hola que proporciona la lista de Hola de tipos de objeto. Si utiliza un procedimiento almacenado, a continuación, también proporcionan parámetros para él en formato de hello **[nombre]: [dirección]: [valor]**. Proporcionar cada parámetro en una línea independiente (use Ctrl + Entrar tooget una nueva línea).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **Consulta SQL**: esta opción le permite tooprovide una consulta SQL que devuelve una sola columna con tipos de objeto, por ejemplo `SELECT [Column Name] FROM TABLENAME`. Hola devuelve la columna debe ser de tipo cadena (varchar).

### <a name="schema-2-detect-attribute-types"></a>Esquema 2 (Detectar tipos de atributo)
En esta página, va tooconfigure cómo Hola nombres de atributos y tipos va toobe detectado. Opciones de configuración de Hola se muestran para cada tipo de objeto detectado en la página anterior de Hola.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Método de detección de tipo de atributo**: Hola conector es compatible con estos métodos de detección del tipo de atributo con cada tipo de objeto detectado en la pantalla 1 del esquema.

* **Tabla/vista/Stored Procedure**: proporcionar nombre Hola de hello tabla/procedimiento almacenado/vista que debe tener nombres de atributo de hello toofind usado. Si utiliza un procedimiento almacenado, a continuación, también proporcionan parámetros para él en formato de hello **[nombre]: [dirección]: [valor]**. Proporcionar cada parámetro en una línea independiente (use Ctrl + Entrar tooget una nueva línea). nombres de atributo de hello toodetect en un atributo con varios valores, proporcionar una lista separada por comas de tablas o vistas. No se admiten escenarios multivalor si la tabla primaria y secundaria tienen los mismos nombres de columna.
* **Consulta SQL**: esta opción le permite tooprovide una consulta SQL que devuelve una sola columna con nombres de atributo, por ejemplo `SELECT [Column Name] FROM TABLENAME`. Hola devuelve la columna debe ser de tipo cadena (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Esquema 3 (Definir delimitador y DN)
Esta página permite el delimitador de tooconfigure y atributo DN para cada tipo de objeto detectado. Puede seleccionar varios delimitador de hello atributos toomake único.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* No se enumeran los atributos multivalor y booleanos.
* Mismo atributo no se puede utilizar para DN y delimitador, a menos que **DN es delimitador** está seleccionado en la página de conectividad de Hola.
* Si **DN es delimitador** está seleccionada en página de conectividad de hello, esta página requiere único atributo Hola DN. Este atributo también se utilizaría como atributo de delimitador de Hola.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Esquema 4 (Definir tipo de atributo, referencia y dirección)
Esta página permite el tipo de atributo de hello tooconfigure, por ejemplo, entero, binario, o un valor booleano y dirección para cada atributo. Se muestran todos los atributos de la página **Esquema 2** , incluidos los atributos multivalor.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Tipo de datos**: toomap Hola atributo tipo toothose tipos conocidos por el motor de sincronización de Hola de uso. predeterminado de Hello es hello toouse mismo tipo detectado en el esquema SQL de hello, pero referencia y la fecha y hora no son detectables fácilmente. En esos casos, deberá toospecify **DateTime** o **referencia**.
* **Dirección**: puede establecer Hola atributo dirección tooImport, exportar o ImportExport. ImportExport es el valor predeterminado.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Notas:

* Si un tipo de atributo no es detectable mediante el conector de hello, usa el tipo de datos de cadena de Hola.
* **Tablas anidadas** se pueden considerar tablas de base de datos con una única columna. Oracle almacena filas Hola de una tabla anidada sin ningún orden determinado. Sin embargo, al recuperar la tabla anidada hello en una variable de PL/SQL, Hola filas reciben subíndices consecutivos comenzando por 1. Que proporciona las filas de tooindividual de acceso de la matriz.
* **VARRYS** no se admiten en Conector de Hola.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Esquema 5 (Definir partición para atributos de referencia)
En esta página, puede configurar en todos los atributos de referencia a qué partición (tipo de objeto) hace referencia un atributo.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Si usa **DN es delimitador**, a continuación, debe usar Hola al mismo tipo de objeto como Hola uno para hacer referencia desde. No se puede hacer referencia a otro tipo de objeto.

>[!NOTE]
A partir de la actualización de marzo de 2017 Hola ahora hay una opción para "*" cuando esta opción está seleccionada, a continuación, todos los tipos de miembro posibles se importará.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 A partir de mayo de 2017 Hola "*" también conocido como **cualquier opción** ha cambiado toosupport de importación y exportación de flujo. Si desea toouse esta opción la tabla o vista con varios valores deben tener un atributo que contiene el tipo de objeto de Hola.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Si "*" está seleccionada, a continuación, también debe especificarse el nombre de Hola de columna de hello con el tipo de objeto de Hola.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Después de la importación verá algo similar imagen toohello siguiente:

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Parámetros globales
página de parámetros globales Hello es usado tooconfigure importación diferencial, formato de fecha y hora y un método de contraseña.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Hola genérico conector de SQL admite Hola siguientes métodos para la importación de diferencias:

* **Trigger**: consulte [Generating Delta Views Using Triggers](https://technet.microsoft.com/library/cc708665.aspx).
* **Watermark**: un enfoque genérico que se puede utilizar con cualquier base de datos. consulta de marca de agua de Hola se rellena previamente en función de proveedor de base de datos de Hola. En cada tabla/vista que se utiliza, debe estar presente una columna de marca de agua. Esta columna debe realizar un seguimiento de inserciones y actualizaciones de tablas de toohello como y sus dependientes (con varios valores o secundarios) tablas. relojes de Hello entre el servidor de base de datos de Hola y el servicio de sincronización deben estar sincronizados. De lo contrario, es posible que se omitan algunas entradas de importación de hello diferencial.  
  Limitación:
  * La estrategia de marca de agua no admite objetos eliminados.
* **Snapshot**: (solo funciona con Microsoft SQL Server) [Generating Delta Views Using Snapshots](https://technet.microsoft.com/library/cc720640.aspx)
* **ChangeTracking**: (solo funciona con Microsoft SQL Server) [About ChangeTracking](https://msdn.microsoft.com/library/bb933875.aspx)  
  Limitaciones:
  * Delimitador & atributo DN deben formar parte de clave principal para el objeto seleccionado de hello en tabla Hola.
  * No se admite la consulta SQL durante la importación y exportación con seguimiento de cambios.

**Parámetros adicionales**: especificar Hola la zona de horaria del servidor de base de datos que indica dónde se encuentra el servidor de base de datos. Este valor se utiliza toosupport Hola diversos formatos de fecha y hora de atributos.

Hola conector siempre almacena fecha y la fecha y hora en formato UTC. toocorrectly de toobe capaz de convertir horas y fecha de hello, se debe especificar la zona horaria de Hola de servidor de base de datos de Hola y el formato de hello usa. formato de Hola se debe expresar en formato. NET.

Durante la exportación se debe proporcionar a cada atributo de tiempo de fecha toohello conector en formato de hora UTC.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Configuración de la contraseña**: conector de hello proporciona capacidades de sincronización de contraseña admite establece y cambia la contraseña.

Hola conector proporciona dos métodos de sincronización de contraseña de toosupport:

* **Procedimiento almacenado**: este método requiere dos procedimientos almacenados toosupport conjunto & Cambiar contraseña. Escriba todos los parámetros para agregar y cambiar la operación de contraseña de hello en **establecer contraseña SP** y **cambiar contraseña SP** parámetros respectivamente como por ejemplo siguiente.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Extensión de la contraseña**: este método requiere el archivo DLL de extensión de contraseña (debe hello tooprovide nombre de la DLL de extensión que está implementando hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interfaz). Ensamblado de la extensión de contraseña se debe colocar en la carpeta de extensión para que el conector de hello pueda cargar Hola DLL en tiempo de ejecución.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

También tiene tooenable Hola administración de contraseñas en hello **configurar extensión** página.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurar particiones y jerarquías
En la página de particiones y jerarquías de hello, seleccione todos los tipos de objeto. Cada tipo de objeto está en su propia partición.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

También puede invalidar los valores de hello definido en hello **conectividad** o **parámetros globales** página.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Configuración de delimitadores
Esta página es de solo lectura porque ya se ha definido el delimitador de Hola. Hello atributo de delimitador seleccionado siempre se anexa con tooensure de tipo de objeto de hello permanece único entre los tipos de objeto.

![delimitadores](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Configuración del parámetro de paso de ejecución
Estos pasos se configuran en hello perfiles de ejecución en hello conector. Estas configuraciones Hola trabajo real de importación y exportación de datos.

### <a name="full-and-delta-import"></a>Importación completa y diferencial
El conector de SQL genérico admite la importación completa y diferencial mediante estos métodos:

* Tabla
* Ver
* Procedimiento almacenado
* Consulta SQL

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Tabla/Vista**  
atributos multivalor tooimport de un objeto, tiene nombre de tabla o vista separada por comas de hello tooprovide en **vistas de la tabla nombre de multivalor** y condiciones de combinación correspondiente en hello **decondicióndecombinación**con la tabla primaria de Hola.

Ejemplo: Supongamos que desea objeto Employee de tooimport hello y todos sus atributos con varios valores. Hay dos tablas con el nombre Employee (tabla principal) y Department (multivalor).
Hola siguientes:

* Escriba **Employee** en **Tabla/Vista/PA**.
* Indique Department en **Nombre de tabla/vistas multivalor**.
* Escriba la condición de combinación de hello entre empleado y el departamento de **condición de combinación**, por ejemplo `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Procedimientos almacenados**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Si tiene muchos datos, se recomienda la paginación tooimplement con los procedimientos almacenados.
* Para la paginación de toosupport del procedimiento almacenado, necesitará tooprovide índice inicial y el índice final. Consulte: [Tutorial 25: Efficiently Paging Through Large Amounts of Data](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndex y @EndIndex se reemplazan en tiempo de ejecución por el valor del tamaño de página correspondiente establecido en la página **Configurar paso**. Por ejemplo, el cuando conector Hola recupera la primera página y el tamaño de página de Hola se establece en esta situación 500, @StartIndex sería 1 y @EndIndex 500. Estos valores aumentar al conector recupera las páginas siguientes y cambiar hello @StartIndex & @EndIndex valor.
* tooexecute parámetros de procedimiento almacenado, proporcionar parámetros de hello en `[Name]:[Direction]:[Value]` formato. Escriba cada parámetro en una línea independiente (Use Ctrl + Entrar tooget una nueva línea).
* El conector SQL genérico también admite la operación de importación desde los servidores vinculados de Microsoft SQL Server. Si se debe recuperar información de una tabla en el servidor vinculado, tabla debe proporcionarse en formato de hello:`[ServerName].[Database].[Schema].[TableName]`
* El conector de SQL genérico admite únicamente los objetos que tienen una estructura similar (tanto nombre de alias como tipo de datos) entre la información de pasos de ejecución y la detección del esquema. Si selecciona Hola objeto de esquema y la información proporcionada en el paso de ejecución es diferente, el conector de SQL es toosupport no se puede este tipo de escenarios.

**Consulta SQL**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* No se admiten consultas de conjuntos de resultados múltiples.
* Consulta SQL admite paginación de Hola y proporcione inicio índice y el índice final como una variable toosupport la paginación.

### <a name="delta-import"></a>Importación delta
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

La configuración de importación condicional requiere algo más de configuración si se compara con la importación completa.

* Si decide enfoque de desencadenador o una instantánea de hello cambios diferenciales de tootrack, a continuación, proporcione tabla de historial o instantánea de base de datos en **nombre de base de datos de tabla de historial o instantánea** cuadro.
* También necesita tooprovide condición de combinación entre la tabla de historial y la tabla primaria, por ejemplo`Employee.ID=History.EmployeeID`
* tootrack transacciones de hello en tabla de hello primaria de la tabla de historial de hello, debe proporcionar el nombre de la columna de Hola que contiene información de la operación de hello (agregar/actualizar/eliminar).
* Si elige cambios diferenciales de la marca de agua tootrack, a continuación, proporcionar nombre de columna de Hola que contiene información de la operación de hello en **nombre de columna de marca de agua**.
* Hola **cambiar el atributo de tipo** columna es necesaria para cambiar el tipo de saludo. Esta columna asigna un cambio que se produce en la tabla principal de Hola o tabla multivalor tooa cambiar tipo en la vista de diferencias de Hola. Esta columna puede contener el tipo de cambio de hello Modify_Attribute de cambio de nivel de atributo o una agregar, modificar o eliminar cambiar tipo de un tipo de cambio de nivel de objeto. Si es un valor distinto de valor de hello agregar, modificar, o eliminar; a continuación, puede definir los valores mediante esta opción.

### <a name="export"></a>Exportación
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

El conector de SQL genérico admite la exportación mediante cuatro métodos compatibles como:

* Tabla
* Ver
* Procedimiento almacenado
* Consulta SQL

**Tabla/Vista**  
Si elige Hola opción de tabla o vista, conector Hola genera Hola respectivas consultas toodo Hola exportación.

**Procedimientos almacenados**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Si elige la opción de procedimiento almacenado Hola, exportación requiere tres diferentes almacenado procedimientos tooperform Insert/Update/Delete operaciones.

* **Agregar nombre de SP**: This SP se ejecuta si vuelve a cualquier objeto tooconnector de inserción en la tabla respectiva de Hola.
* **Actualizar nombre de SP**: This SP se ejecuta si vuelve a cualquier objeto tooconnector de actualización en la tabla respectiva de Hola.
* **Eliminar nombre SP**: This SP se ejecuta si vuelve a cualquier objeto tooconnector para su eliminación en la tabla respectiva de Hola.
* Atributo seleccionado en el esquema de hello usado como un procedimiento de toohello almacenado del valor de parámetro. Por ejemplo, `EmployeeName: INPUT: @EmployeeName` (EmployeeName está seleccionado en el esquema del conector de Hola y conector Hola reemplaza el valor respectivo de hello mientras realiza la exportación)
* toorun parámetros de procedimiento almacenado, proporcione los parámetros en `[Name]:[Direction]:[Value]` formato. Escriba cada parámetro en una línea independiente (Use Ctrl + Entrar tooget una nueva línea).

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Si elige la opción de consulta SQL de hello, exportación requiere que tres diferentes consultas operaciones Insert, Update o Delete de tooperform.

* **Consulta Insert**: se ejecuta esta consulta si vuelve a cualquier objeto tooconnector de inserción en la tabla respectiva de Hola.
* **Actualizar consulta**: se ejecuta esta consulta si vuelve a cualquier objeto tooconnector de actualización en la tabla respectiva de Hola.
* **Eliminar consultas**: se ejecuta esta consulta si vuelve a cualquier objeto tooconnector para su eliminación en la tabla respectiva de Hola.
* Atributo seleccionado del esquema de hello usará como una consulta de toohello del valor de parámetro, por ejemplo`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Solución de problemas
* Para obtener información sobre cómo registro tooenable tootroubleshoot Hola conector, vea hello [cómo tooEnable seguimiento de ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
