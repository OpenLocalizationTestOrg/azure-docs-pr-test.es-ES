---
title: Conector de Domino aaaLotus | Documentos de Microsoft
description: "Este artículo se describe cómo Lotus Domino conector tooconfigure Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Referencia técnica del conector de Lotus Domino
Este artículo describe Hola conector para Lotus Domino. artículo de Hola aplica toohello siguientes productos:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Debe usar la revisión 4.1.3671.0 o posterior ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Para MIM2016 y FIM2010R2, está disponible como una descarga de Hola Hola conector [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Información general de hello conector para Lotus Domino
Hola conector para Lotus Domino le permite el servicio de sincronización de hello toointegrate con el servidor de Lotus Domino de IBM.

Desde una perspectiva de alto nivel, Hola siguientes características es compatibles con la versión actual de Hola de conector de hello:

| Característica | Soporte técnico |
| --- | --- |
| Origen de datos conectado |Servidor:  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Cliente:<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Escenarios |<li>Administración del ciclo de vida de objetos</li><li>Administración de grupos</li><li>Administración de contraseñas</li> |
| Operaciones |<li>Importación completa y diferencial</li><li>Exportación</li><li>Establecer y cambiar la contraseña en Contraseña de HTTP</li> |
| Esquema |<li>Persona (usuario móvil, contacto (personas sin certificado))</li><li>Grupo</li><li>Recurso (recurso, sala, reunión en línea)</li><li>Base de datos de correo de entrada</li><li>Detección dinámica de atributos para los objetos admitidos</li> |

Conector de Lotus Domino de Hello usa toocommunicate de cliente de Lotus Notes Hola con Lotus Domino Server. Como consecuencia de esta dependencia, un cliente de Lotus Notes compatible debe instalarse en el servidor de sincronización de Hola. Hola la comunicación entre el cliente de Hola y el servidor de Hola se implementa a través de la interfaz de interoperabilidad de .NET de Lotus Notes (Interop.domino.dll) Hola. Esta interfaz facilita la comunicación de hello entre el cliente de Lotus Notes y la plataforma de Microsoft.NET de Hola y admite acceso tooLotus Domino documentos y vistas. Para la importación de delta, también es posible que se utiliza esa interfaz nativo Hola C++ (según el método de importación de delta de hello seleccionado).

### <a name="prerequisites"></a>Requisitos previos
Antes de usar Hola conector, asegúrese de que tiene Hola siguiendo los requisitos previos en el servidor de sincronización de hello:

* Microsoft .NET 4.5.2 Framework o posterior
* cliente de Lotus Notes Hola debe instalarse en el servidor de sincronización
* Hola conector para Lotus Domino requiere Hola predeterminado Lotus Domino LDAP esquema (schema.nsf) de la base de datos toobe existe en el servidor de directorio de Domino de Hola. Si no está presente, puede instalarlo ejecutando o reiniciar el servicio LDAP de hello en el servidor de Domino de Hola.

### <a name="connected-data-source-permissions"></a>Permisos del origen de datos conectado
tooperform admite cualquiera de hello tareas en el conector de Lotus Domino, debe ser miembro de los grupos siguientes:

* Administradores de acceso total
* Administradores
* Administradores de bases de datos

Hello tabla siguiente enumeran los permisos de Hola que son necesarios para cada operación:

| Operación | Derechos de acceso |
| --- | --- |
| Importar |<li>Leer documentos públicos</li><li> Administrador de acceso total (cuando son miembros del grupo de administradores de acceso completo, automáticamente tiene acceso efectivo de hello tooin ACL.)</li> |
| Exportación y establecimiento de contraseña |Acceso efectivo:  <li>Creación de documentos</li><li>Eliminar documentos</li><li>Leer documentos públicos</li><li>Escribir documentos públicos</li><li>Replicar o copiar documentos</li>Para las operaciones de exportación, también necesita Hola siguientes roles: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Operaciones directas y AdminP
Operaciones de ir directamente a toohello Domino directory o a través de hello AdminP procesan. Hello siguientes tablas enumeran todos los objetos admitidos, las operaciones y, si procede, Hola relacionados con el método de implementación:

**Libreta de direcciones principal**

| Objeto | Crear | Actualizar | Eliminar |
| --- | --- | --- | --- |
| Persona |AdminP |Directo |AdminP |
| Grupo |AdminP |Directo |AdminP |
| MailInDB |Directo |Directo |Directo |
| Recurso |AdminP |Directo |AdminP |

**Libreta de direcciones secundaria**

| Objeto | Crear | Actualizar | Eliminar |
| --- | --- | --- | --- |
| Persona |N/D |Directo |Directo |
| Grupo |Directo |Directo |Directo |
| MailInDB |Directo |Directo |Directo |
| Recurso |N/D |N/D |N/D |

Cuando se cree un recurso, se crea un documento de Notes. De forma similar, cuando se elimina un recurso, se elimina el documento de notas de Hola.

### <a name="ports-and-protocols"></a>Puertos y protocolos
El cliente de IBM Lotus Notes y los servidores de Domino se comunican mediante una llamada a procedimiento remoto de Notes (NRPC) en la que NRPC debe usar TCP/IP. número de puerto predeterminado de Hello es 1352, pero puede cambiarse mediante el Administrador de Domino de Hola.

### <a name="not-supported"></a>No compatible
Hola las siguientes operaciones no es compatibles con la versión actual de Hola de conector de Lotus Domino de hello:

* Mover un buzón entre servidores.

## <a name="create-a-new-connector"></a>Creación de un nuevo conector
### <a name="client-software-installation-and-configuration"></a>Instalación y configuración del software de cliente
Lotus Notes deben estar instalado en el servidor de hello **antes de** Hola conector está instalado.

Durante la instalación, asegúrese de realizar una **instalación para un solo usuario (Single User Install)**. Hola predeterminado **instalar multiusuario** no funciona.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

En la página de características de hello, instalar solo Hola requiere características de Lotus Notes y **inicio de sesión único de cliente**. Inicio de sesión único se requiere para hello conector toobe puede toolog en el servidor de Domino de toohello.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Nota:** inicio Lotus Notes una vez con un usuario que se encuentra en hello mismo servidor que Hola cuenta se usa como cuenta de servicio del conector de Hola. También asegúrese de cliente de Lotus Notes de hello tooclose seguro en el servidor de Hola. No se puede ejecutar en Hola Hola de tiempo mismo conector intenta tooconnect toohello Domino server.

### <a name="create-connector"></a>Creación del conector
tooCreate un conector de Lotus Domino, en **servicio de sincronización de** seleccione **Management Agent** y **crear**. Seleccione hello **Lotus Domino (Microsoft)** conector.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Si la versión del servicio de sincronización ofrece Hola capacidad tooconfigure **arquitectura**, asegúrese de que el conector Hola se ha establecido tooits predeterminado valor toorun **proceso**.

### <a name="connectivity"></a>Conectividad
En la página de conectividad de hello, debe especificar el nombre del servidor de Lotus Domino de Hola y escriba las credenciales de inicio de sesión de Hola.  
![Conectividad](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Hola propiedad del servidor de Domino admite dos formatos para el nombre del servidor de hello:

* nombreDeServidor
* nombreDeServidor/nombreDeDirectorio

Hola **ServerName/DirectoryName** formato es Hola preferido para este atributo porque proporciona una respuesta más rápida cuando contactos de conector de Hola Hola servidor Domino.

Hola proporciona UserID archivo se almacena en la base de datos de configuración de hello del servicio de sincronización de Hola.

Para **Importación diferencial** , tiene estas opciones:

* **Ninguna**. Hola conector no lleva a cabo las importaciones de delta.
* **Adición y actualización**. Hola conector hace delta import agregar y las operaciones de actualización. Para las de eliminación, se necesita una operación **Importación completa** . Esta operación es mediante la interoperabilidad de .net de Hola.
* **Adición, actualización y eliminación**. Hola conector hace delta import agregar, actualizar y eliminar operaciones. Esta operación es mediante interfaces de C++ nativo de Hola.

En **opciones de esquema** tiene Hola siguientes opciones:

* **Esquema predeterminado**. Hola conector detecta esquema Hola desde el servidor de Domino de Hola. Esta selección es la opción predeterminada de Hola.
* **Esquema DSML**. Solo se usa si servidor de Domino de hello no expone el esquema de Hola. A continuación, puede crear un archivo DSML con el esquema de Hola e importarlo en su lugar. Para más información sobre DSML, consulte [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Al hacer clic en siguiente, se comprueban Hola UserID y parámetros de configuración de contraseña.

### <a name="global-parameters"></a>Parámetros globales
En la página de parámetros globales de hello, configurar la zona de horaria de Hola y la importación de Hola y opción de operación de exportación.  
![Parámetros globales](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Hola **zona horaria del servidor Domino** parámetro define la ubicación de Hola de su servidor de Domino.

Esta opción de configuración es necesario toosupport **importación diferencial** operaciones porque permite que el servicio de sincronización de hello determinar los cambios entre las dos últimas importaciones de Hola.

>[!Note]
A partir de la pantalla de bienvenida marzo de 2017 actualización Hola parámetros globales incluye la base de datos de correo electrónico del usuario de hello opción toodelete Hola durante la eliminación del usuario de Hola.

![Eliminación del buzón del usuario](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Configuración de importación: método
Hola **realizar la importación completa por** tiene estas opciones:

* Search
* Vista (recomendada)

**Búsqueda** está utilizando la indización en Domino, pero es habitual que no se actualizan los índices de hello en tiempo real y datos de hello devueltas por el servidor hello no siempre son correctos. Para un sistema con muchos cambios, esta opción normalmente no funciona bien y proporciona eliminaciones falsas en algunas situaciones. Sin embargo, la **búsqueda** es más rápida que la **vista**.

**Vista** se recomienda opción Hola puesto que ofrece un estado correcto Hola de datos. Es ligeramente más lenta que la búsqueda.

#### <a name="creation-of-virtual-contact-objects"></a>Creación de objetos _Contact virtuales
Hola **habilitar la creación de \_objeto contacto** tiene estas opciones:

* None
* Valores sin referencia
* Valores de referencia y sin referencia

En Domino, atributos de referencia pueden contener muchos tooreference diferentes formatos otros objetos. toobe toorepresent capaz de distintas variaciones, Hola implementa conector \_póngase en contacto con objetos, también conocido como **contactos Virtual** (VC). Estos objetos se crean para que puedan unirse tooexisting MV objetos o se proyecta como nuevos objetos. De esta forma, se conservan las referencias de atributo.

Al habilitar esta opción y si el contenido de Hola de un atributo de referencia no es un formato DN, un \_se crea el objeto de contacto. Por ejemplo, un atributo member de un grupo puede contener direcciones SMTP. También es posible toohave shortName y otros atributos presentes en los atributos de referencia. En este escenario, seleccione **Valores sin referencia**. Esta configuración es la configuración más común de Hola para las implementaciones de Domino.

Lotus Domino una vez configurado toohave dirección independiente libros con diferentes nombres completos que representa Hola mismo objeto, crear su posible tooalso \_objetos de contacto para todos los valores de referencia que se encuentran en una libreta de direcciones. En este escenario, seleccione hello **referencia y los valores de referencia no** opción.

Si tiene varios valores de atributo de hello **FullName** Domino, a continuación, desea también creación de hello tooenable de contactos Virtual por lo que se pueden resolver las referencias. Por ejemplo, este atributo puede poseer varios valores después de un cambio de nombre. Seleccione la casilla de verificación de hello **habilitar... objeto _Contact cuando "FullName" tenga varios valores para una persona** para este escenario.

Mediante la combinación de atributos correctos de hello, Hola \_objetos de contacto sería MV de toohello Unidos a un objeto.

Estos objetos tienen VC =\_contacto agregado tootheir DN.

#### <a name="import-settings-conflict-object"></a>Configuración de importación: objeto de conflicto
**Excluir objeto de conflicto**

En una implementación mayor de Domino, es posible que varios objetos han Hola mismo DN debido a problemas de tooreplication. En estos casos, el conector de hello vería dos objetos con UniversalIDs diferentes pero mismo DN. Este conflicto hará que un objeto temporal se crea en el espacio de conector de Hola. Hola conector puede omitir los objetos de Hola que se han seleccionado en el Domino como sujetos de replicación. recomendación de Hello es tookeep activa esta casilla.

#### <a name="export-settings"></a>Exportar configuración
Si hello opción **AdminP usar para actualizar referencias** está seleccionada, la exportación de los atributos de referencia, como miembro, es una llamada directa y no utiliza el proceso de AdminP Hola. Use esta opción solo si AdminP no ha sido configurado toomaintain la integridad referencial.

#### <a name="routing-information"></a>Información de enrutamiento
En Domino, es posible que un atributo de referencia tiene información de enrutamiento incrusta como un toohello sufijo DN. Por ejemplo, podría contener el atributo de miembro de hello en un grupo de **CN =example/organization@ABC**. sufijo de Hello @ABC es información de enrutamiento de Hola. información de enrutamiento de Hola se usa por Domino toosend mensajes de correo electrónico toohello Domino sistema correcto, que puede ser un sistema en otra organización. En el campo de información de enrutamiento de hello, puede especificar usado en la organización de hello en el ámbito de hello conector de enrutamiento de sufijos de Hola. Si uno de estos valores se encuentra en un atributo de referencia como sufijo, información de enrutamiento de Hola se quita de la referencia de Hola. Si el sufijo de enrutamiento de hello en un valor de referencia no puede ser tooone coincidente de los valores especificados, un \_se crea el objeto de contacto. Estos \_objetos de contacto se crean con **RO = @<RoutingSuffix>**  inserta Hola DN. Para estos \_objetos de póngase en contacto con hello siguientes atributos es también agregan tooallow unir objeto real tooa si es necesario: \_routingName, \_contactName, \_displayName y UniversalID.

#### <a name="additional-address-books"></a>Libretas de direcciones adicionales
Si no tiene **guía telefónica** instalado, que proporciona el nombre de Hola de libretas de direcciones secundarias, a continuación, puede escribir manualmente estas libretas de direcciones.

#### <a name="multivalued-transformation"></a>Transformación multivalor
Muchos de los atributos de Lotus Domino son multivalor. Hello correspondiente metaverso atributos son normalmente solo con valores. Mediante la configuración de importación hello y opción de operación de exportación de hello, habilitar Hola conector toohelp con traducción de hello necesario de atributos de hello afectado.

**Exportarar**  
opción de operación de exportación de Hello admite dos modos:

* Anexar elemento
* Reemplazar elemento

**Reemplace el elemento** : al seleccionar esta opción, el conector de hello siempre remove Hola valores actuales del atributo de hello en Domino y sustituirlos por otros valores de hello proporcionado. Hola proporcionada con valores puede ser un valor único o con varios valores.

Ejemplo: atributo de Asistente de Hola de un objeto person tiene Hola siguientes valores:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Si un asistente de nueva denominado **David Alexander** está asignado el objeto de la persona de toothis, resultado de hello es:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**Anexar elemento** : cuando se selecciona esta opción, conector Hola conserva los valores existentes en el atributo de hello Domino e insertar nuevos valores en parte superior de Hola de lista de datos de Hola Hola.

Ejemplo: atributo de Asistente de Hola de un objeto person tiene Hola siguientes valores:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Si un asistente de nueva denominado **David Alexander** está asignado el objeto de la persona de toothis, resultado de hello es:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**Importaciónación**  
opción de la operación de importación de Hello admite dos modos:

* Valor predeterminado
* Valor de tooSingle con varios valores

**Predeterminado** : cuando se seleccione la opción predeterminada de hello, todos los valores del programa Hola a todos los atributos se importan.

**Valor de varios valores tooSingle** : cuando se selecciona esta opción, un atributo multivalor se convierte en un atributo de valor único. Si existe más de un valor, se utiliza el valor de hello en la parte superior de hello (este valor es normalmente también hello más reciente).

Ejemplo: atributo de Asistente de Hola de un objeto person tiene Hola siguientes valores:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Hola atributo de toothis de actualización más reciente es **David Alexander**. Puesto Hola opción de la operación de importación se establece tooMultivalued tooSingle valor, solo importa conector **David Alexander** hasta el espacio del conector de Hola.

tooconvert de atributos con varios valores en atributos de valor único para la lógica Hello no hay ningún atributo de miembro del grupo de toohello y atributo de toohello persona fullname.

Lo tooconfigure posible importar y exportar reglas de transformación para los atributos con varios valores por atributo, como una regla de excepción de toohello global. tooconfigure esta opción, escriba [objecttype]. [NombreAtributo] Hola **importar la lista de atributos de exclusión** y **exportar la lista de atributos de exclusión** cuadros de texto. Por ejemplo, si escribes Person.Assistant y marca global de Hola se establece tooimport se importa del Asistente de Hola para todos los valores, el único valor primera Hola.

#### <a name="certifiers"></a>Certificadores
Se muestran todas las unidades de organización/organización por conector Hola. toobe tooexport capaz de persona objetos toohello principal libreta de direcciones un certificador con su contraseña es necesario.

Si dispone de todos los certificadores Hola misma contraseña, hello **contraseña para todos los Certifers** puede utilizarse. A continuación, puede introducir aquí la contraseña de Hola y solo especificar archivo de certificador hello.

Si solo se importa, no tendrá toospecify cualquier los certificadores.

### <a name="configure-provisioning-hierarchy"></a>Configurar la jerarquía de aprovisionamiento
Cuando se configura el conector de Lotus Domino de hello, omitir esta página del cuadro de diálogo. el conector de Lotus Domino de Hello no admite la jerarquía de aprovisionamiento.  
![Jerarquía de aprovisionamiento](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurar particiones y jerarquías
Al configurar particiones y jerarquías, debe seleccionar la libreta de direcciones principal de hello denominado NAB=names.nsf. Además toohello libreta de dirección principal, puede seleccionar libretas de direcciones secundarias si existen.  
![Particiones](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Seleccionar atributos
Cuando configure los atributos, debe seleccionar todos aquellos con el prefijo **\_MMS\_**. Estos atributos son obligatorios al aprovisionar nuevos objetos tooLotus Domino

![Attributes](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Administración del ciclo de vida de objetos
Esta sección proporciona información general sobre los distintos objetos de Hola de Domino.

### <a name="person-objects"></a>Objetos de persona
objeto de Hello person representa a los usuarios en la organización y las unidades de organización. Además los atributos predeterminados toohello, Administrador de Domino de hello pueden agregar objeto Person de tooa de atributos personalizados. Como mínimo, un objeto de persona debe incluir todos los atributos obligatorios. Para obtener una lista completa de los atributos obligatorios, consulte [Propiedades de Lotus Notes](#lotus-notes-properties). debe cumplirse tooregister un objeto person, Hola siguiendo los requisitos previos:

* Libreta de direcciones de Hello (names.nsf) se debe haber definido y debe ser libreta de direcciones principal de Hola.
* Debe tener Hola O/OU tooregister de certificador hello y el Id. de contraseña un usuario determinado en hello organización o unidad organizativa.
* Debe establecer un conjunto específico de propiedades de Lotus Notes para un objeto de persona. Estas propiedades se utilizan para el aprovisionamiento de objeto de hello person. Para obtener más información, vea la sección Hola denominada [Lotus Notes Properties](#lotus-notes-properties) más adelante en este documento.
* Hola de contraseña HTTP inicial para una persona es un atributo y un conjunto durante el aprovisionamiento.
* objeto person de Hello debe ser uno de los siguientes tres tipos admitidos de hello:
  1. Usuario normal que tiene un archivo de correo y un archivo de identificación de usuario
  2. Usuario móvil (un usuario normal que incluye todos los archivos de base de datos móvil)
  3. Contactos (usuarios sin archivo de identificación)

Personas (excepto los contactos) más pueden agruparse en los usuarios nos e internacional tal como se define por valor de Hola de hello \_MMS\_IDRegType propiedad. Estas personas usar Hola cliente Notes tooaccess servidores Lotus Domino, tiene un identificador de notas y un documento de la persona. Si usan el correo de Notes, también tienen un archivo de correo. usuario de Hello debe ser registrado toobecome active. Para más información, consulte:

* [Setting up Notes users](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [User Registration](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Administración de usuarios](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Renaming users](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Todas estas operaciones se realizan en Lotus Domino y, a continuación, se importan en el servicio de sincronización de Hola.

### <a name="resources-and-rooms"></a>Recursos y salas
Un recurso es otro tipo de base de datos de Lotus Domino. Los recursos pueden ser las salas de conferencia con varios tipos de equipos como proyectores. Hay subtipos de recursos admitidos por el conector de Lotus Domino que se definen mediante el atributo de tipo de recurso de hello:

| Tipo de recurso | Atributo de tipo de recurso |
| --- | --- |
| Sala |1 |
| Recurso (otros) |2 |
| Reunión en línea |3 |

Para toowork de tipo de objeto de recurso de hello, se requiere lo siguiente hello:

* Base de datos de reserva de recursos ya debe existir en el servidor de Domino de hello conectado
* Hola sitio ya está definido para hello recursos

base de datos de reserva de recursos de Hello contiene tres tipos de documentos:

* Perfil de sitio
* Recurso
* Reserva

Para obtener más información sobre la configuración de base de datos de reserva de recursos, consulte [Configurar base de datos de las reservas de recursos de hello](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Crear, actualizar y eliminar recursos**  
Hola se realizan las operaciones Create, Update y Delete mediante el conector de Lotus Domino de hello en la base de datos de reserva de recursos de Hola. Los recursos se crean como documentos en Names.nsf (es decir, libreta de direcciones principal de hello). Para obtener más información sobre cómo modificar y eliminar recursos, consulte [Editing and deleting Resource documents](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html) (Edición y eliminación de documentos de recursos).

**Operación de importación y exportación para recursos**  
Hola recursos puede ser importado tooand exportada desde el servicio de sincronización de hello, como cualquier otro tipo de objeto. Tipo de objeto seleccione hello como recurso durante la configuración. Para que la operación de exportación se realice correctamente, debería tener información sobre el tipo de recurso, la base de datos de conferencias y el nombre del sitio.

### <a name="mail-in-databases"></a>Bases de datos de correo de entrada
Una base de datos de correo electrónico es una base de datos que está diseñada tooreceive correos. Es un buzón de Lotus Domino que no está asociado a ninguna cuenta de usuario de Lotus Domino específica (es decir, no tiene archivo de identificación ni contraseña propios). Una base de datos de correo de entrada tiene un valor UserId único ("nombre corto") asociado y su propia dirección de correo electrónico.

Si se necesita un buzón independiente con su propia dirección de correo electrónico que se pueda compartir entre distintos usuarios (por ejemplo: group@contoso.com), se crea una base de datos de correo de entrada. el buzón de correo de Hello acceso toothis se controla a través de su lista de Control de acceso (ACL), que contiene los nombres de Hola de usuarios de notas de Hola que se permiten los buzones de correo de tooopen Hola.

Para obtener una lista de atributos de hello necesario, consulte sección Hola denominada [atributos obligatorios](#mandatory-attributes) más adelante en este artículo.

Cuando una base de datos está diseñada tooreceive un correo electrónico, se crea un documento de correo electrónico de base de datos de Lotus Domino. Este documento debe existir en el directorio de Domino de todos los servidores que almacenan una copia de base de datos de Hola. Para ver una descripción detallada de cómo crear un documento de base de datos de correo de entrada, consulte [Creating a Mail-In Database document](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)(Creación de un documento de base de datos de correo de entrada).

Antes de crear una base de datos de correo electrónico, ya debe existir la base de datos de hello (deben se han creado por el Administrador de Lotus) en el servidor de Domino de Hola.

### <a name="group-management"></a>Administración de grupos
Puede obtener una descripción detallada de administración de grupos de Lotus Domino Hola de hello recursos siguientes:

* [Using groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Creating a group](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Creating and modifying groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Managing groups](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Renaming a group](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Administración de contraseñas
Para un usuario registrado de Lotus Domino, existen dos tipos de contraseñas:

1. Contraseña de usuario (se almacena en el archivo User.id)
2. Contraseña HTTP/Internet

Conector de Lotus Domino Hola solo admite operaciones con contraseña HTTP.

administración de contraseñas de tooperform, debe habilitar la administración de contraseñas para el conector de hello en hello diseñador del agente de administración. administración de contraseñas tooenable, seleccione **habilitar la administración de contraseñas** en hello **configurar extensiones** página de diálogo.  
![Configurar extensiones](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

soporte de conector de Lotus Domino de Hello las siguientes operaciones en la contraseña de Internet:

* Establecer contraseña: Contraseña del conjunto establece una nueva contraseña HTTP de Internet en usuario de hello en Domino. De forma predeterminada la cuenta de hello también está desbloqueada. Hola desbloquear marca se expone en la interfaz WMI de Hola de hello motor de sincronización.
* Cambiar la contraseña: En este escenario, un usuario conviene toochange contraseña de Hola o toochange solicitadas contraseña después de una hora especificada. Para este sitio de tootake operación, tanto (Hola antigua y nueva contraseña de hello) son obligatorios. Una vez cambiada, Hola nueva contraseña se actualiza en Lotus Domino.

Para más información, consulte:

* [Utilizando la característica de bloqueo de Internet de Hola](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Managing Internet passwords](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Información de referencia
Esta sección se enumeran como requisitos de los atributos para el conector de Lotus Domino de Hola y descripciones de atributo.

### <a name="lotus-notes-properties"></a>Propiedades de Lotus Notes
Al aprovisionamiento de directorio de Lotus Domino de Person objetos tooyour, los objetos deben tener un conjunto específico de propiedades con valores específicos que se rellena. Estos valores solo son necesarios para las operaciones de creación.

Hola tabla siguiente enumera estas propiedades y proporciona una descripción de ellos.

| Propiedad | Descripción |
| --- | --- |
| \_MMS_AltFullName |Hola alternativo nombre completo del usuario. |
| \_MMS_AltFullNameLanguage |Hola toobe de lenguaje utilizado para especificar el nombre completo alternativo de saludo del usuario. |
| \_MMS_CertDaysToExpire |número de Hola de días a partir de hello fecha actual antes de certificado de hello expira. Si no se especifica, fecha de hello predeterminada es de dos años de hello fecha actual. |
| \_MMS_Certifier |Propiedad que contiene el nombre de jerarquía organizativa de Hola de certificador Hola. Por ejemplo: OU=OrganizationUnit,O=Org,C=Country. |
| \_MMS_IDPath |Si Hola propiedad está vacía, ningún archivo de identificación de usuario se crea localmente en el servidor de sincronización de Hola. Si la propiedad de hello contiene un nombre de archivo, un archivo de Id. de usuario se crea en la carpeta de madata Hola. propiedad Hello también puede contener una ruta de acceso completa. |
| \_MMS_IDRegType |Las personas se pueden clasificar como contactos, usuarios de Estados Unidos y usuarios de fuera de Estados Unidos. Hello tabla siguiente enumeran los valores posibles de hello: <li>0 - Contacto</li><li>1 - Usuario Estados Unidos</li><li>2 - Usuario internacional</li> |
| \_MMS_IDStoreType |Propiedad obligatoria para los usuarios de Estados Unidos y de fuera de Estados Unidos. propiedad Hello contiene un valor entero que especifica si la identificación de usuario de Hola se almacena como datos adjuntos en la libreta de direcciones de hello notas o en el archivo de correo electrónico de la persona de Hola. Si el archivo de Id. de usuario de hello es un archivo adjunto en la libreta de direcciones de hello, opcionalmente, se puede crear como un archivo con \_MMS_IDPath. <li>Almacenar el archivo de identificación en el almacén de identificaciones, sin archivo de identificación (se usa para contactos).</li><li> 1 - attachment en Libreta de direcciones de hello notas. Hola \_MMS_Password propiedad debe establecerse para los archivos de identificación de usuario que son los datos adjuntos</li><li>2: almacenar la identificación en el archivo de correo de la persona. Hola \_MMS_UseAdminP debe establecerse correo de hello toolet toofalse archivo se crea durante Hola registro de la persona. Hola \_MMS_Password propiedad debe establecerse para los archivos de identificación de usuario.</li> |
| \_MMS_MailQuotaSizeLimit |número de Hola de megabytes que se permiten para la base de datos de archivo de correo electrónico de Hola. |
| \_MMS_MailQuotaWarningThreshold |número de Hola de megabytes que se permiten para la base de datos de archivo de correo electrónico de hello antes de que se emite una advertencia. |
| \_MMS_MailTemplateName |archivo de la plantilla de correo electrónico Hola que es el archivo de correo electrónico del usuario de hello toocreate usado. Si se especifica una plantilla, archivo de correo electrónico de hello se crea utilizando la plantilla Hola especificados. Si no se especifica ninguna plantilla, archivo de plantilla predeterminado de hello es el archivo de Hola de toocreate usado. |
| \_MMS_OU |Propiedad opcional que es nombre de unidad organizativa de hello en certificador Hola. Esta propiedad debe estar vacía para los contactos. |
| \_MMS_Password |Propiedad obligatoria para los usuarios. propiedad Hello contiene la contraseña de hello para el archivo de identificación de Hola de objeto Hola. |
| \_MMS_UseAdminP |Propiedad debe ser conjunto tootrue si se debe crear el archivo de correo electrónico de hello por proceso de AdminP hello en el servidor de Domino de hello (proceso de exportación de toohello asincrónica). Si la propiedad está establecida en toofalse, archivo de correo electrónico de hello se crea con hello usuario de Domino (sincrónico en el proceso de exportación de hello). |

Para un usuario con un archivo de identificación asociados, Hola \_MMS_Password propiedad debe contener un valor. Para el acceso de correo electrónico a través del cliente de Lotus Notes hello, servidor de correo electrónico de Hola y MailFile propiedades de un usuario deben contener un valor.

tooaccess de correo electrónico a través de un explorador Web, Hola propiedades siguientes debe contener valores:

* MailFile - propiedad necesaria que contiene la ruta de acceso de hello en servidor de Lotus Domino Hola donde se almacena el archivo de correo electrónico de hello.
* Servidor de correo electrónico - propiedad necesaria que contiene Hola nombre del servidor de Lotus Domino Hola. Este valor es Hola nombre toouse cuando se creó el archivo de correo electrónico de Lotus hello en el servidor de Domino de Hola.
* HTTPPassword - propiedad opcional que contiene la contraseña de acceso Web de hello para el objeto de Hola.

tooaccess Hola servidor Domino sin la funcionalidad de correo electrónico, hello HTTPPassword propiedad debe contener un valor. propiedad MailFile de Hola y Hola propiedad de servidor de correo electrónico puede estar vacío.

Con \_MMS_ IDStoreType = 2 (identificador de almacén en el archivo de correo electrónico), Hola propiedad MailSystem de NotesRegistrationclass se establece tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Atributos obligatorios
Conector de Lotus Domino de Hello principalmente admite estos tipos de objetos (tipos de documento):

* Grupo
* Base de datos de correo de entrada
* Persona
* Contacto (persona sin certificador)
* Recurso

En esta sección se enumera los atributos de Hola que son obligatorios para cada servidor de Domino de objeto compatible tooexport tooa.

| Tipo de objeto | Atributos obligatorios |
| --- | --- |
| Grupo |<li>ListName</li> |
| Base de datos de correo de entrada |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Persona |<li>Apellidos</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Contacto (persona sin certificador) |<li>\_MMS_IDRegType</li> |
| Recurso |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Sitio</li><li>DisplayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Problemas y preguntas comunes
### <a name="schema-detection-does-not-work"></a>La detección de esquema no funciona
esquema de toobe toodetect capaz de hello, es necesario que schema.nsf Hola el archivo esté presente en el servidor de Domino de Hola. Este archivo solo aparece si LDAP está instalado en el servidor de Hola. Si el esquema de hello no es detectable, compruebe Hola siguiente:

* Hola archivo schema.nsf está presente en la carpeta raíz de Hola de hello servidor Domino
* usuario de Hello tiene archivo de permisos toosee hello schema.nsf.
* Forzar un reinicio del servidor LDAP de Hola. Abra **Lotus Domino consola** y usar **saber LDAP ReloadSchema** esquema de comando tooreload Hola.

### <a name="not-all-secondary-address-books-are-visible"></a>No todas las libretas de direcciones secundarias son visibles
Hello Domino conector se basa en la característica de hello **Directory asistencia** toobe toofind capaz de hello secundaria libretas. Si faltan libretas de direcciones secundarias de hello, compruebe si [Directory asistencia](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) se ha habilitado y configurado en hello servidor Domino.

### <a name="custom-attributes-in-domino"></a>Atributos personalizados de Domino
Hay varias maneras de esquema de Domino tooextend Hola por lo que aparece como un atributo personalizado que se pueden utilizar por hello conector.

**Enfoque 1: Extender el esquema de Lotus Domino**

1. Crear una copia de la plantilla del directorio de Domino {PUBNAMES. NTF} siguiendo [estos pasos](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (no debe personalizar directorio de IBM Lotus Domino predeterminado de hello plantilla):
2. Plantilla de directorio de copia de Domino de abrir Hola {CONTOSO. Plantilla NTF} que se creó en el Diseñador de Domino y siga estos pasos:
   * Haga clic en Shared Elements (Elementos compartidos) y expanda Subforms (Subformularios).
   * Haga doble clic en subformulario de ${nombreDeObjeto} InheritableSchema (donde {nombreDeObjeto} es nombre Hola de clase de objeto estructural de hello de forma predeterminada, por ejemplo: persona).
   * Nombre de atributo de Hola que quiera tooadd en esquema {MyPersonAtrribute} y atributo toothat correspondiente. Crear un campo seleccione hello **crear** menú y, a continuación, seleccione **campo** de menú.
   * En campo agregado de hello, establecer sus propiedades, seleccione su tipo, estilo, tamaño, fuente y otros parámetros relacionados en la ventana de propiedades de campo.
   * Atributo de hello mantener mismo valor predeterminado como nombre de hello proporcionado para ese atributo (por ejemplo, si el nombre del atributo es MyPersonAttribute, mantener el valor predeterminado de hello con hello mismo nombre).
   * Guardar subformulario de hello ${nombreDeObjeto} InheritableSchema con valores actualizados.
3. Reemplace Hola Domino Directory plantilla {PUBNAMES. NTF} con plantilla personalizada nueva de Hola {CONTOSO. NTF} siguiendo [estos pasos](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Cierre el Administrador de Domino y abra hello de la consola de Domino toorestart servicio LDAP y tooReload Hola esquema LDAP:
   * En la consola de Domino, insert, comando hello en **Domino comando** texto presentado servicio LDAP de toorestart Hola - [reiniciar tarea LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * esquema de LDAP de tooreload utilizar comandos LDAP indicar - indicar ReloadSchema de LDAP
5. Abra Administrador de Domino y seleccione toosee pestaña usuarios y grupos agrega el atributo se refleja en el domino agregar una persona.
6. Abra Schema.nsf en la pestaña **Files** (Archivos) y compruebe que el atributo agregado se refleja en la clase de objeto de LDAP dominoPerson.

**Método 2: Crear un auxClass con el atributo personalizado y asociar a la clase de objeto de hello**

1. Crear una copia de la plantilla del directorio de Domino {PUBNAMES. NTF} siguiendo [estos pasos](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (nunca Personalizar directorio de IBM Lotus Domino predeterminado de hello plantilla):
2. Plantilla de directorio de copia de Domino de abrir Hola {CONTOSO. Plantilla NTF} que se creó en el Diseñador de Domino.
3. En el panel izquierdo de hello, seleccione el código compartido y, a continuación, subformularios.
4. Haga clic en New Subform (Nuevo subformulario).
5. Hola siguientes toospecify Hola propiedades subformulario nueva hello:
   * Con subformulario nueva Hola abierto, seleccione diseño - propiedades de subformulario
   * Toohello siguiente propiedad de nombre, escriba un nombre para la clase de objeto auxiliar de hello: por ejemplo, TestSubform.
   * Mantener la propiedad Options de Hola "Incluyen subformulario Insert... cuadro de diálogo" seleccionado
   * Anule la selección de propiedades de opciones de Hola "Representación pasan a través de HTML en notas."
   * Deje Hola otras propiedades Hola igual y cerrar Hola subformulario propiedades cuadro.
   * Guarde y cierre subformulario nueva Hola.
6. Hola después de una clase de objeto auxiliar de campo toodefine Hola tooadd:
   * Abrir subformulario Hola que creó.
   * Elija Create - Field (Crear - Campo).
   * Siguiente tooName en ficha de conceptos básicos de Hola Hola campo del cuadro de diálogo, especifique cualquier nombre, por ejemplo: {MyPersonTestAttribute}.
   * En campo agregado de hello, establecer sus propiedades, seleccione su tipo, estilo, tamaño, fuente y propiedades relacionadas.
   * Atributo de hello mantener mismo valor predeterminado como nombre de hello proporcionado para ese atributo (por ejemplo, si el nombre del atributo es MyPersonTestAttribute, mantener el valor predeterminado de hello con hello mismo nombre).
   * Guardar subformulario Hola con valores actualizados y Hola siguientes:
     * En el panel izquierdo de hello, seleccione el código compartido y, a continuación, subformularios
     * Seleccione nuevo subformulario de Hola y elija Diseño - propiedades de diseño.
     * Haga clic en hello tercera ficha de hello izquierda y seleccione **propagar esta prohibición de cambio de diseño**.
7. Abrir subformulario de ExtensibleSchema ${nombreDeObjeto}, (donde {nombreDeObjeto} es nombre Hola de clase de objeto estructural de Hola de forma predeterminada, por ejemplo: persona).
8. Insertar recurso y seleccione Hola subformulario (que ha creado, por ejemplo: TestSubform) y guardar subformulario ExtensibleSchema de hello ${nombreDeObjeto}.
9. Reemplace Hola Domino Directory plantilla {PUBNAMES. NTF} con plantilla personalizada nueva de Hola {CONTOSO. NTF} siguiendo [estos pasos](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Cierre el Administrador de Domino y abra hello de la consola de Domino toorestart servicio LDAP y tooReload Hola esquema LDAP:
    * En la consola de Domino, insert, comando hello en **Domino comando** texto presentado servicio LDAP de toorestart Hola - [reiniciar tarea LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * esquema de LDAP de tooreload utilizar comandos LDAP indicar **saber LDAP ReloadSchema**.
11. Abra Administrador de Domino y seleccione toosee pestaña usuarios y grupos agrega el atributo se refleja en el domino agregar una persona (en otras personas de tabulación).
12. Abra Schema.nsf en la pestaña **Files** (Archivos) y compruebe que el atributo agregado se refleja en la clase auxiliar de objeto de LDAP subformularioDePrueba.

**Método 3: Agregar clase de hello atributo personalizado toohello ExtensibleObject**

1. Abrir archivo {Schema.nsf} que se coloca en el directorio raíz de Hola
2. Seleccione las clases de objeto LDAP de menú de la izquierda hello en **todos los documentos de esquema** y haga clic en **agregar Object (clase)** botón:
3. Proporcione el nombre de LDAP en forma de Hola de {zzzExtensibleSchema} (donde zzz es nombre Hola de clase de objeto estructural de Hola de forma predeterminada, por ejemplo persona). Por ejemplo, esquemas de hello tooextend para la clase de objeto de persona, proporcione el nombre LDAP {PersonExtensibleSchema}.
4. Proporcionar el nombre de clase de objeto Superior, que se desea esquema de hello tooextend. Por ejemplo, esquema de hello tooextend para la clase de objeto de persona, proporcionar el nombre de clase de objeto de una mejor opción {dominoPerson}:
5. Proporciona una clase de objeto toohello correspondiente de OID válida.
6. Seleccionar atributos extendidos/personalizados en campos obligatorio u opcional de los tipos de atributo según los requisitos de Hola:
7. Después de agregar requiere atributos toohello ExtensibleObjectClass, haga clic en **guardar y cerrar**.
8. Se crea un elemento ExtensibleObjectClass para la clase de objeto predeterminada respectiva con atributos extendidos.

## <a name="troubleshooting"></a>Solución de problemas
* Para obtener información sobre cómo registro tooenable tootroubleshoot Hola conector, vea hello [cómo tooEnable seguimiento de ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
