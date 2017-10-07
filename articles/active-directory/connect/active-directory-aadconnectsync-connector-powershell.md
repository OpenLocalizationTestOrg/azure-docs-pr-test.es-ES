---
title: aaaPowerShell conector | Documentos de Microsoft
description: "Este artículo se describe cómo conector de Microsoft tooconfigure de Windows PowerShell."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Referencia técnica del conector de Windows PowerShell
Este artículo describe Hola conector de Windows PowerShell. artículo de Hola aplica toohello siguientes productos:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Debe usar la revisión 4.1.3671.0 o posterior ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Para MIM2016 y FIM2010R2, está disponible como una descarga de Hola Hola conector [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Información general de hello conector de PowerShell
Hola PowerShell conector permite servicio de sincronización de hello toointegrate con sistemas externos que proporcionan API basadas en Windows PowerShell. Conector de Hello proporciona un puente entre las capacidades de hello del agente de administración de conectividad extensible basada en llamadas de hello 2 framework (ECMA2) y Windows PowerShell. Para obtener más información sobre el marco de trabajo de hello ECMA, vea hello [Extensible referencia de agente de administración de conectividad 2.2](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Requisitos previos
Antes de usar Hola conector, asegúrese de que tiene Hola siguientes en el servidor de sincronización de hello:

* Microsoft .NET 4.5.2 Framework o posterior
* Windows PowerShell 2.0, 3.0 o 4.0

Directiva de ejecución de Hello en el servidor del servicio de sincronización de hello debe ser configurado tooallow Hola conector toorun scripts de Windows PowerShell. A menos que la ejecución del conector de hello scripts Hola está firmados digitalmente, configurar Directiva de ejecución de hello, ejecute este comando:  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Creación de un nuevo conector
toocreate un conector de Windows PowerShell en el servicio de sincronización de hello, debe proporcionar una serie de secuencias de comandos de Windows PowerShell que se ejecutan pasos de hello solicitados por el servicio de sincronización de Hola. Según se conecta la funcionalidad de hello tooand que se necesita el origen de datos de hello, secuencias de comandos de hello debe implementar varía. En esta sección se describe cada una de las secuencias de comandos de Hola que puedan implementarse y cuando sea necesarios.

Hola de Windows PowerShell es conector diseñado toostore de scripts de hello dentro de la base de datos de servicio de sincronización de Hola. Aunque es posible toorun scripts que están almacenados en el sistema de archivos de hello, resulta más fácil de cuerpo de hello tooinsert de cada secuencia de comandos directamente en la configuración del conector toohello.

tooCreate un conector de PowerShell, en **servicio de sincronización de** seleccione **Management Agent** y **crear**. Seleccione hello **PowerShell (Microsoft)** conector.

![Creación del conector](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Conectividad
Proporcionar parámetros de configuración para conectar el sistema remoto tooa. Estos valores segura se almacenan por el servicio de sincronización de Hola y realizados los scripts de Windows PowerShell tooyour disponibles cuando se ejecuta el conector de Hola.

![Conectividad](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Puede configurar Hola conectividad parámetros siguientes:

**Conectividad**

| Parámetro | Valor predeterminado | Propósito |
| --- | --- | --- |
| Server |<Blank> |Nombre del servidor que Hola conector debe conectarse a. |
| Dominio |<Blank> |Dominio de hello credencial toostore para su uso cuando se ejecuta el conector de Hola. |
| Usuario |<Blank> |Nombre de usuario de hello credencial toostore para su uso cuando se ejecuta el conector de Hola. |
| Password |<Blank> |Contraseña de hello credencial toostore para su uso cuando se ejecuta el conector de Hola. |
| Suplantación de la cuenta del conector |False |Cuando sea true, el servicio de sincronización de Hola ejecuta scripts de Windows PowerShell de hello en contexto de Hola de las credenciales de hello proporcionadas. Cuando sea posible, se recomienda que hello **$Credentials** parámetro se pasa tooeach script se utiliza en lugar de suplantación. Para obtener más información sobre los permisos adicionales que son necesarios toouse esta opción, consulte [configuración adicional para la suplantación](#additional-configuration-for-impersonation). |
| Carga del perfil de usuario al suplantar |False |Indica el perfil de usuario de Windows tooload Hola de credenciales del conector de Hola durante la suplantación. Si el usuario suplantado hello tiene un perfil móvil, conector hello no carga el perfil móvil de Hola. Para obtener más información sobre los permisos adicionales que son necesarios toouse este parámetro, consulte [configuración adicional para la suplantación](#additional-configuration-for-impersonation). |
| Tipo de inicio de sesión al suplantar |None |Tipo de inicio de sesión durante la suplantación Para obtener más información, vea hello [dwLogonType] [ dw] documentación. |
| Solo scripts firmados |False |Si es true, el conector de Windows PowerShell de hello valida que cada script tiene una firma digital válida. Si es false, asegúrese de que la directiva de ejecución de Windows PowerShell del servidor del servicio de sincronización de hello es RemoteSigned o sin restricción. |

**Módulo común**  
Conector de Hello permite toostore compartido módulo de Windows PowerShell en la configuración de Hola. Cuando el conector de Hola ejecuta una secuencia de comandos, hello de Windows PowerShell es el módulo extrae toohello sistema de archivos para que pueda importarse por cada secuencia de comandos.

Para las secuencias de comandos de importación, exportación y la sincronización de contraseña, módulo común de hello es la carpeta de MAData del conector toohello extraídos. Para los scripts de detección de esquemas, validación, jerarquía y partición, módulo común de hello es carpeta toohello extraídos % TEMP %. En ambos casos, Hola extrae comunes módulo de script se denomina según la configuración de nombre de secuencia de comandos de módulo común toohello.

tooload un módulo denominado FIMPowerShellConnectorModule.psm1 desde la carpeta de MAData hello, use Hola siguiente instrucción:`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload un módulo denominado FIMPowerShellConnectorModule.psm1 desde la carpeta % TEMP % de hello, use Hola siguiente instrucción:`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Validación de parámetros**  
Hola Script de validación es un script de Windows PowerShell opcional que puede ser usado tooensure que los parámetros de configuración de conector proporcionados por el Administrador de hello son válidos. Servidor de validación, las credenciales de conexión y los parámetros de conectividad son usos comunes de script de validación de Hola. Hello secuencia de comandos de validación se llama después de hello siguientes fichas y cuadros de diálogo se han modificado:

* Conectividad
* Parámetros globales
* Configuración de la partición

script de validación de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |ficha de configuración de Hola o cuadro de diálogo que desencadena la solicitud de validación de Hola. |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |

script de validación de Hello debe devolver una sola canalización de toohello de objeto ParameterValidationResult.

**Detección de esquema**  
Hola script de detección de esquemas es obligatorio. Esta secuencia de comandos devuelve los tipos de objeto de hello, atributos y las restricciones de atributo que Hola servicio de sincronización que se utiliza al configurar reglas de flujo de atributos. Hola script de detección de esquemas se ejecuta durante la creación del conector y rellena el esquema del conector de Hola. También se usa por hello acción Actualizar esquema Hola Synchronization Service Manager.

script de detección de esquemas de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |

script de Hola debe devolver una sola [esquema] [ schema] canalización toohello de objetos. objeto de esquema de Hola se compone de [SchemaType] [ schemaT] objetos que representan los tipos de objeto (por ejemplo: usuarios y grupos). objeto de tipo de esquema de Hello contiene una colección de [SchemaAttribute] [ schemaA] objetos que representan atributos de hello (por ejemplo: nombre, apellido y dirección postal) de tipo hello.

**Parámetros adicionales**  
Además toohello configuración estándar, puede definir personalizado configuración adicional que las instancias toohello específico de hello conector. Estos parámetros se pueden especificar en el conector de hello, partición, o los niveles de paso de ejecución y son accesibles desde script de Windows PowerShell relevante de Hola. Opciones de configuración personalizadas pueden almacenarse en la base de datos de servicio de sincronización de hello en texto sin formato o se pueden cifrar. Hola servicio de sincronización automáticamente cifra y descifra la configuración de una configuración segura cuando sea necesario.

Opciones de configuración personalizada de toospecify, nombre de hello independientes de cada parámetro con una coma (,).

tooaccess configuración personalizada de una secuencia de comandos, debe sufijo nombre hello con un carácter de subrayado ( \_ ) y el ámbito de Hola de parámetro de hello (Global, partición o RunStep). Por ejemplo, tooaccess Hola parámetro FileName Global, use este fragmento de código:`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Capacidades
pestaña de capacidades de Hola de hello diseñador del agente de administración define Hola comportamiento y la funcionalidad de conector de Hola. no se puede modificar las selecciones de Hello realizadas en esta pestaña cuando se ha creado el conector de Hola. Esta tabla enumera la configuración de capacidad de Hola.

![Capacidades](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Capacidad | Descripción |
| --- | --- |
| [Estilo de nombre distintivo][dnstyle] |Indica si el conector de hello es compatible con nombres distintivos y si es así, ¿qué estilo. |
| [Tipo de exportación][exportT] |Determina el tipo de saludo de objetos que se presentan toohello script de exportación. <li>AttributeReplace: incluye el conjunto completo de Hola de valores para un atributo con varios valores cuando cambia el atributo de Hola.</li><li>AttributeUpdate: incluye solo atributo multivalor de hello deltas tooa cuando cambia el atributo de Hola.</li><li>MultivaluedReferenceAttributeUpdate: incluye un conjunto completo de valores de atributos de varios valores sin referencia y diferencias solo para atributos de referencia de varios valores.</li><li>ObjectReplace: incluye todos los atributos de un objeto cuando no cambia ningún atributo.</li> |
| [Normalización de datos][DataNorm] |Indica los atributos de delimitador de toonormalize de servicio de sincronización de hello antes de que se proporcionaron tooscripts. |
| [Confirmación de objeto][oconf] |Configura Hola pendiente de comportamiento de la importación de hello servicio de sincronización. <li>Normal: comportamiento predeterminado que se espera que exporta todas toobe cambios confirmado mediante la importación</li><li>NoDeleteConfirmation: cuando se elimina un objeto, no hay ninguna importación pendiente generada.</li><li>NoAddAndDeleteConfirmation: cuando se crea o se elimina un objeto, no hay ninguna importación pendiente generada.</li> |
| Usar el nombre distintivo como delimitador |Si hello estilo de nombre distintivo se establece tooLDAP, atributo de delimitador de hello para el espacio de conector de hello también es nombre distintivo de Hola. |
| Operaciones simultáneas de varios conectores |Cuando está activada, se pueden ejecutar simultáneamente varios conectores de Windows PowerShell. |
| Particiones |Al activar esta opción, el conector de hello admite varias particiones y detección de partición. |
| Jerarquía |Al activar esta opción, conector hello es compatible con una estructura jerárquica de estilo LDAP. |
| Habilitar importación |Al activar esta opción, el conector de hello importa datos a través de las secuencias de comandos de importación. |
| Habilitar importación diferencial |Al activar esta opción, puede solicitar conector Hola deltas de hello importación secuencias de comandos. |
| Habilitar exportación |Al activar esta opción, el conector de hello exporta los datos a través de scripts de exportación. |
| Habilitar exportación completa |Al activar esta opción, Hola exportar soporte técnico de las secuencias de comandos exportar el espacio de conector por completo de Hola. toouse que esta opción, Habilitar exportación también debe comprobarse. |
| No hay valores de referencia en el primer paso de exportación |Cuando está activada, se exportan los atributos de referencia en un segundo paso de exportación. |
| Habilitar cambio de nombre de objeto |Cuando está activada, se pueden modificar los nombres distintivos. |
| Eliminar-agregar al reemplazar |Cuando se activa, las operaciones de eliminar-agregar se exportan como un único reemplazo. |
| Habilitar operaciones de contraseña |Cuando está activada, se admiten los scripts de sincronización de contraseña. |
| Habilitar contraseña de exportación en el primer paso |Cuando está activada, las contraseñas que se establece durante el aprovisionamiento se exportan cuando se crea el objeto de Hola. |

### <a name="global-parameters"></a>Parámetros globales
pestaña de parámetros globales de Hola Hola diseñador del agente de administración permite scripts de Windows PowerShell de hello tooconfigure que se ejecutan mediante el conector de Hola. También puede configurar valores globales para los valores de configuración personalizados definidos en la ficha de conectividad de Hola.

**Detección de particiones**  
Una partición es un espacio de nombres independiente dentro de un esquema compartido. Por ejemplo, en Active Directory, cada dominio es una partición dentro de un bosque. Una partición es agrupación lógica de hello para la importación y exportación de las operaciones. La importación y exportación tienen particiones como contexto y todas las operaciones tienen lugar en este contexto. Las particiones se supone que toorepresent una jerarquía en LDAP. nombre distintivo de Hola de una partición se usa en tooverify de importación que todas devuelven objetos están dentro del ámbito de Hola de una partición. También se utiliza el nombre distintivo de la partición de Hola durante el aprovisionamiento de hello metaverso toohello conector espacio toodetermine Hola partición que debe asociar con un objeto durante la exportación.

script de detección de partición de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |

Hello secuencia de comandos debe devolver un una sola [partición] [ part] objeto o una lista [T] de la canalización de toohello de objetos de partición.

**Detección de jerarquía**  
script de detección de jerarquía de Hello sólo se utiliza cuando es de hello funcionalidad de estilo de nombre distintivo LDAP. script de Hola es tooallow usado se toobrowse y seleccione un conjunto de contenedores que se considera dentro o fuera de ámbito para importa y exportar las operaciones. script de Hola solo debe proporcionar una lista de nodos que son elementos secundarios directos del nodo proporcionado toohello script de Hola raíz.

script de detección de jerarquía de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| ParentNode |[HierarchyNode][hn] |nodo raíz de Hola de jerarquía de hello en qué Hola script debería devolver a elementos secundarios directos. |

script de Hola debe devolver una un objeto de HierarchyNode secundario único o una lista [T] de canalización de secundarios HierarchyNode objetos toohello.

#### <a name="import"></a>Importación
Los conectores que admiten operaciones de importación deben implementar tres scripts.

**Begin Import**  
Hola Iniciar importación script se ejecuta al principio de Hola de un paso de importación que se ejecute. Durante este paso, puede establecer un sistema de origen de conexión toohello y realice los pasos preparatorios antes de importar los datos de hello conectado el sistema.

Hola Iniciar importación script recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa a script de Hola sobre tipo hello de importación ejecutar (delta o full), partición, jerarquía, marca de agua y el tamaño de página esperado. |
| Tipos |[Schema][schema] |Esquema para el espacio de conector de Hola que se importa. |

script de Hola debe devolver una sola [OpenImportConnectionResults] [ oicres] objeto canalización toohello, por ejemplo:`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Import Data**  
Conector de Hola llama Hola importar datos script hasta que el script de Hola indica que no hay ningún tooimport datos más. Conector de Windows PowerShell de Hello tiene un tamaño de página de 9.999 objetos. Si el script devuelve más de 9999 objetos para importar, debe admitir la paginación. expone de conector de Hola se llama a una propiedad de datos personalizados que puede usar el almacén de tooa una marca de agua para que cada Hola tiempo Importar secuencia de comandos de datos, el script reanuda la importación de objetos donde se quedó.

script de importación de datos de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Contiene Hola marca de agua (CustomData) que puede usarse durante paginadas importaciones y las importaciones de delta. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa a script de Hola sobre tipo hello de importación ejecutar (delta o full), partición, jerarquía, marca de agua y el tamaño de página esperado. |
| Tipos |[Schema][schema] |Esquema para el espacio de conector de Hola que se importa. |

Hello secuencia de comandos de datos de importación debe escribir una lista [[CSEntryChange][csec]] canalización toohello de objetos. Esta colección se compone de atributos de CSEntryChange que representan cada objeto que se va a importar. Durante una ejecución de importación completa, esta colección debe tener un conjunto completo de objetos CSEntryChange que tengan todos los atributos para cada objeto. Durante una importación Delta, objeto de hello CSEntryChange debe contener deltas de nivel de atributo de Hola para cada objeto tooimport o una representación completa de los objetos de Hola que han cambiado (modo de reemplazo).

**End Import**  
Al finalizar de Hola de importación de hello ejecutar, Hola final Importar script se ejecuta. Esta secuencia de comandos debe realizar las tareas de limpieza necesarias (por ejemplo, toofailures de cerrar conexiones toosystems y responder).

script de importación de Hello final recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Informa a script de Hola sobre tipo hello de importación ejecutar (delta o full), partición, jerarquía, marca de agua y el tamaño de página esperado. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Informa de script de Hola motivo Hola finalizó la importación de Hola. |

script de Hola debe devolver una sola [CloseImportConnectionResults] [ cicres] objeto canalización toohello, por ejemplo:`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Exportación
Toohello idénticos importación arquitectura de conector de hello, los conectores que admiten la exportación deben implementar tres secuencias de comandos.

**Begin Export**  
Hola iniciar exportación script se ejecutará al principio de Hola de un paso de ejecución de exportación. Durante este paso, puede establecer un sistema de origen de conexión toohello y llevar a cabo los pasos previos antes de exportar datos toohello conectado el sistema.

Hola iniciar exportación script recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa a script de Hola sobre tipo hello de ejecución de exportación (delta o full), partición, jerarquía y el tamaño de página esperado. |
| Tipos |[Schema][schema] |Esquema para el espacio de conector de Hola que se exporta. |

script de Hola no debería devolver cualquier canalización toohello de salida.

**Export Data**  
Hola servicio de sincronización llama a secuencias de comandos de exportar datos de hello como tantas veces como sea necesario tooprocess todas las exportaciones pendientes. Si el espacio del conector de hello tiene más exportaciones pendientes de Hola a tamaño de página del conector, secuencia de comandos de datos puede recibir varias llamadas de exportación de Hola y posiblemente varias veces para Hola mismo objeto.

script de exportación de datos de Hello recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| CSEntries |IList[CSEntryChange][csec] |Lista de cambiar todos los objetos del espacio de conector Hola con pendiente toobe exportaciones procesadas durante esta fase. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa a script de Hola sobre tipo hello de ejecución de exportación (delta o full), partición, jerarquía y el tamaño de página esperado. |
| Tipos |[Schema][schema] |Esquema para el espacio de conector de Hola que se exporta. |

Hello script de exportación de datos debe devolver un [PutExportEntriesResults] [ peeres] canalización toohello de objetos. Este objeto no necesita información sobre los resultados tooinclude por cada conector exportado a menos que se produce un error o un atributo de delimitador de toohello de cambio. Por ejemplo, tooreturn una canalización de toohello PutExportEntriesResults objeto:`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**End Export**  
Al finalizar de Hola de exportación de hello ejecutar, Hola toorun exportar de final de secuencia de comandos. Esta secuencia de comandos debe realizar las tareas de limpieza necesarias (por ejemplo, toofailures de cerrar conexiones toosystems y responder).

script de exportación de Hello final recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Informa a script de Hola sobre tipo hello de ejecución de exportación (delta o full), partición, jerarquía y el tamaño de página esperado. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Informa de script de Hola motivo Hola finalizó la exportación de Hola. |

script de Hola no debería devolver cualquier canalización toohello de salida.

#### <a name="password-synchronization"></a>Sincronización de contraseñas
Se pueden usar los conectores de Windows PowerShell como destino para los cambios o restablecimientos de contraseña.

secuencia de comandos de Hello contraseña recibe Hola siguientes parámetros de conector de hello:

| Nombre | Tipo de datos | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tabla de parámetros de configuración para el conector de Hola. |
| Credential: |[PSCredential][pscred] |Contiene las credenciales especificadas por administrador de hello en la ficha de conectividad de Hola. |
| Partition |[Partición][part] |Partición de directorio que Hola CSEntry está en. |
| CSEntry |[CSEntry][cse] |Entrada de espacio del conector para objeto Hola que recibió un cambio de contraseña o se restablece. |
| OperationType |String |Indica si la operación de hello es un restablecimiento (**SetPassword**) o un cambio (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Marcas que especifican Hola diseñado el comportamiento de restablecimiento de contraseña. Este parámetro solo está disponible si OperationType es **SetPassword**. |
| OldPassword |String |Rellena con la contraseña antigua del objeto de Hola para cambios de contraseña. Este parámetro solo está disponible si OperationType es **ChangePassword**. |
| NewPassword |String |Se rellena con la contraseña nueva del objeto de Hola que debe establecer el script de Hola. |

Hola script de contraseña es tooreturn no esperado cualquier canalización de Windows PowerShell de toohello de resultados. Si se produce un error en la secuencia de comandos de contraseña de hello, script de Hola debe producir una de hello después excepciones tooinform Hola servicio de sincronización sobre el problema de hello:

* [PasswordPolicyViolationException] [ pwdex1] : se produce si Hola contraseña no cumple los directiva de contraseñas de hello en el sistema de hello conectado.
* [PasswordIllFormedException] [ pwdex2] : se produce si Hola contraseña no es aceptable para el sistema de hello conectado.
* [PasswordExtension] [ pwdex3] – produce para todos los demás errores en la secuencia de comandos de hello contraseña.

## <a name="sample-connectors"></a>Conectores de ejemplo
Para obtener información general completa de los conectores de ejemplo disponibles de hello, consulte [colección de conector de Windows PowerShell conector ejemplo][samp].

## <a name="other-notes"></a>Otras notas
### <a name="additional-configuration-for-impersonation"></a>Configuración adicional para la suplantación
Usuario de Hola de concesión es suplantada hello siguientes permisos en el servidor del servicio de sincronización de hello:

Acceso de lectura toohello siguiendo las claves del registro:

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

Hola toodetermine identificador de seguridad (SID) de cuenta de servicio del servicio de sincronización hello, ejecute hello siga los comandos de PowerShell:

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Carpetas del sistema de archivos de acceso de lectura toohello siguiente:

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Sustituya el nombre de hello del conector de Windows PowerShell de Hola de marcador de posición de Hola {ConnectorName}.

## <a name="troubleshooting"></a>Solución de problemas
* Para obtener información sobre cómo registro tooenable tootroubleshoot Hola conector, vea hello [cómo tooEnable seguimiento de ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
