---
title: Conector LDAP aaaGeneric | Documentos de Microsoft
description: "Este artículo se describe cómo conector de LDAP genérico de Microsoft tooconfigure."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Referencia técnica del conector de LDAP genérico
Este artículo describe Hola conector LDAP genérico. artículo de Hola aplica toohello siguientes productos:

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Debe usar la revisión 4.1.3671.0 o posterior ( [KB3092178](https://support.microsoft.com/kb/3092178)).

Para MIM2016 y FIM2010R2, está disponible como una descarga de Hola Hola conector [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Cuando se hace referencia en RFC tooIETF, este documento con formato de hello (RFC [número RFC] / [section en el documento RFC]), por ejemplo (RFC 4512/4.3).
Puede encontrar más información en http://tools.ietf.org/html/rfc4500 (necesita tooreplace 4500 con el número correcto de RFC de hello).

## <a name="overview-of-hello-generic-ldap-connector"></a>Información general de hello conector LDAP genérico
Hola conector LDAP genérico permite toointegrate Hola servicio de sincronización con un servidor LDAP v3.

Ciertas operaciones y elementos de esquema, como las que sea necesario tooperform importación de delta, no se especifican en la RFC de IETF Hola. Para estas operaciones se admiten solo directorios LDAP especificados explícitamente.

Desde una perspectiva de alto nivel, Hola siguientes características es compatibles con la versión actual de Hola de conector de hello:

| Característica | Soporte técnico |
| --- | --- |
| Origen de datos conectado |Hola conector es compatible con todos los servidores de v3 LDAP (compatible con RFC 4510). Se ha probado con siguiente hello: <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Catálogo global de Microsoft Active Directory (AD GC)</li><li>389 Directory Server</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (anteriormente Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**Directorios importantes no admitidos:** <li>Microsoft Active Directory Domain Services (AD DS) [uso Hola integrados conector de Active Directory en su lugar]</li><li>Oracle Internet Directory (OID)</li> |
| Escenarios |<li>Administración del ciclo de vida de objetos</li><li>Administración de grupos</li><li>Administración de contraseñas</li> |
| Operaciones |Hola las siguientes operaciones se admite en todos los directorios LDAP: <li>Importación completa</li><li>Exportación</li>solo se admite las siguientes operaciones de Hello en los directorios especificados:<li>Importación diferencial</li><li>Establecer contraseña, cambiar contraseña</li> |
| Esquema |<li>Esquema se ha detectado en el esquema LDAP de hello (RFC3673 y RFC4512/4.2)</li><li>Admite clases estructurales, clases auxiliares y la clase de objeto extensibleObject (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Compatibilidad con importación diferencial y administración de contraseñas
Directorios compatibles con la importación diferencial y la administración de contraseñas:

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con la operación Establecer contraseña
* Catálogo global de Microsoft Active Directory (AD GC)
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con la operación Establecer contraseña
* 389 Directory Server
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Apache Directory Server
  * No es compatible con la importación diferencial ya que este directorio no tiene un registro de cambios persistente
  * Es compatible con la operación Establecer contraseña
* IBM Tivoli DS
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Isode Directory
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Novell eDirectory y NetIQ eDirectory
  * Compatible con las operaciones Agregar, Actualizar y Cambiar nombre de la importación diferencial
  * No es compatible con operaciones Eliminar para importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Open DJ
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Open DS
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Open LDAP (openldap.org)
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con la operación Establecer contraseña
  * No admite la operación Cambiar contraseña
* Oracle (anteriormente Sun) Directory Server Enterprise Edition
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* RadiantOne Virtual Directory Server (VDS)
  * Debe utilizar la versión 7.1.1 o superior
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña
* Sun One Directory Server
  * Es compatible con todas las operaciones de la importación diferencial
  * Es compatible con las operaciones Establecer contraseña y Cambiar contraseña

### <a name="prerequisites"></a>Requisitos previos
Antes de usar Hola conector, asegúrese de que tiene Hola siguientes en el servidor de sincronización de hello:

* Microsoft .NET 4.5.2 Framework o posterior

### <a name="detecting-hello-ldap-server"></a>Detectar el servidor LDAP de Hola
Hola conector se basa en diversas toodetect técnicas e identificar el servidor LDAP de Hola. usos de conector de Hola Hola DSE raíz, de nombre/versión del proveedor, e inspecciona objetos únicos de hello esquema toofind y atributos conocidos tooexist en determinados servidores LDAP. Estos datos, si se encuentra, es usado toopre-rellenar las opciones de configuración de Hola Hola conector.

### <a name="connected-data-source-permissions"></a>Permisos del origen de datos conectado
tooperform importar y exportar las operaciones en objetos de hello en el directorio conectado hello, cuenta de hello conector debe tener permisos suficientes. Conector de Hello necesita escribir permisos toobe capaz de tooexport y tooimport capaz de toobe de permisos de lectura. Configuración de permisos se realiza dentro de las experiencias de administración de Hola Hola del directorio de destino propio.

### <a name="ports-and-protocols"></a>Puertos y protocolos
Conector de Hello usa número de puerto de hello especificado en la configuración de hello, cuyo valor predeterminado es 389 para LDAP y 636 para LDAPS.

Para LDAPS, debe utilizar SSL 3.0 o TLS. SSL 2.0 no es compatible y no se puede activar.

### <a name="required-controls-and-features"></a>Características y controles necesarios
Hello LDAP controles y características siguientes deben estar disponibles en servidor LDAP de Hola para hello conector toowork correctamente:  
`1.3.6.1.4.1.4203.1.5.3` Filtros True/False

filtro de verdadero/falso Hola con frecuencia se notifica no compatible con directorios LDAP y podría aparecer en hello **página Global** en **obligatorio características no se encontró**. Es utilizado toocreate **o** filtros en las consultas LDAP, por ejemplo, al importar varios tipos de objeto. Si puede importar más de un tipo de objeto, eso significa que el servidor LDAP es compatible con esta característica.

Si utiliza un directorio donde es un identificador único siguiente de hello delimitador hello también debe estar disponible (para obtener más información, vea hello [configurar delimitadores](#configure-anchors) sección):  
`1.3.6.1.4.1.4203.1.5.1` Todos los atributos operativos

Si el directorio de hello tiene más objetos que el que cabe en un directorio de toohello de llamada, se recomienda toouse paginación. Para toowork de paginación, necesita uno de hello siguientes opciones:

**Opción 1:**  
`1.2.840.113556.1.4.319` pagedResultsControl

**Opción 2:**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

Si ambas opciones están habilitadas en la configuración del conector de hello, se utiliza pagedResultsControl.

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl solo se usa con objetos de hello USNChanged delta import método toobe toosee puede eliminar.

Conector de Hello intenta opciones de hello toodetect presentes en el servidor de Hola. Si no se detectan opciones hello, una advertencia está presente en página Global hello en Propiedades del conector Hola. No todos los servidores LDAP presentes todos los controles y características admiten e incluso si está presente, esta advertencia Hola conector funcionen sin problemas.

### <a name="delta-import"></a>Importación diferencial
La importación diferencial sólo está disponible cuando se ha detectado un directorio de soporte. Hola siguiendo métodos está en uso actualmente:

* Registro de accesos LDAP. Consulte [http://www.openldap.org/doc/admin24/overlays.html#Access Registro de ](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* Registro de cambios LDAP. Consulte [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* Marca de tiempo. Para NetIQ/Novell eDirectory, Hola conector utiliza última fecha y hora tooget había creado y actualiza objetos. NetIQ/Novell eDirectory no proporciona que un equivalente significa tooretrieve eliminar objetos. Esta opción también puede utilizarse si ningún otro método de importación delta está activo en el servidor LDAP de Hola. Esta opción no es capaz de tooimport eliminar objetos.
* USNChanged. Consulte: [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>No compatible
no se admite Hola siguientes características LDAP:

* Referencias LDAP entre servidores (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Creación de un nuevo conector
tooCreate un conector LDAP genérico, en **servicio de sincronización de** seleccione **Management Agent** y **crear**. Seleccione hello **(Microsoft) de LDAP genérico** conector.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Conectividad
En la página de conectividad de hello, debe especificar información de Host, el puerto y el enlace de Hola. Según cuál sea enlace seleccionado, adicionales información podría proporcionarse en hello las secciones siguientes.

![Conectividad](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* configuración de tiempo de espera de conexión de Hello sirve únicamente como primer servidor de toohello conexión Hola al detectar el esquema de Hola.
* Si el enlace es anónimo, no se utiliza ningún nombre de usuario o contraseña ni certificados.
* Para otros enlaces, escriba la información ya sea mediante nombre de usuario y contraseña o bien mediante la selección de un certificado.
* Si está utilizando Kerberos tooauthenticate, también proporcionan Hola dominio/dominio del usuario de Hola.

Hola **atributo alias** cuadro de texto se utiliza para los atributos definidos en el esquema de hello con sintaxis RFC4522. Estos atributos no se pueden detectar durante la detección de esquemas y Hola conector necesita ayuda tooidentify esos atributos. Por ejemplo Hola siguiente debe especificarse en hello atributo alias cuadro toocorrectly identificar atributo userCertificate de Hola como un atributo binario:

`userCertificate;binary`

Hola te mostramos un ejemplo de cómo esta configuración podría ser similar:

![Conectividad](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Seleccione hello **incluir atributos operativos en esquema** tooalso casilla incluir atributos creados por servidor hello. Éstos incluyen atributos como al objeto de Hola se creó y hora de última actualización.

Seleccione **incluir atributos extensibles en esquema** si se utilizan objetos extensibles (RFC4512/4.3) y si se habilita esta opción permite que cada toobe de atributo que se utiliza en todos los objetos. Al seleccionar esta opción realiza esquema Hola muy grande para que a menos que se está usando el directorio conectado Hola esta recomendación de hello característica es la opción de Hola de tookeep anular la selección.

### <a name="global-parameters"></a>Parámetros globales
En la página de parámetros globales de hello, configurar registro de cambios de hello DN toohello delta y características adicionales de LDAP. página de Hola se rellena automáticamente con información de hello proporcionada por servidor LDAP de Hola.

![Conectividad](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

la sección superior Hello muestra información proporcionada por servidor hello, como nombre de saludo del servidor de Hola. Hola conector también comprueba que controles obligatorio Hola se encuentran en hello DSE raíz. Si no se muestran, aparece una advertencia. Algunos directorios LDAP no enumerar todas las características de hello DSE raíz y es posible que Hola funciona conector sin problemas, incluso si hay una advertencia.

Hola **admite controles** casillas de verificación controlan el comportamiento de Hola de ciertas operaciones:

* Con la eliminación de árbol seleccionada, se elimina una jerarquía con una llamada LDAP. Con la eliminación de árbol no está seleccionada, el conector de hello realiza una eliminación recursiva si es necesario.
* Con resultados paginados seleccionados, Hola conector realiza una importación paginada con tamaño de hello especificado en los pasos de hello ejecutar.
* Hola VLVControl y SortControl es un alternativo toohello pagedResultsControl tooread de datos de directorio LDAP de Hola.
* Si las tres opciones (pagedResultsControl, VLVControl y SortControl) son no seleccionadas, a continuación, hello conector importa todos los objetos en una sola operación, lo que podría producir un error si es un directorio de gran tamaño.
* ShowDeletedControl solo se usa cuando el método de importación de hello Delta es USNChanged.

registro de cambios de Hello DN es utilizado por el registro de cambios de delta de hello, por ejemplo el contexto de nomenclatura de hello **cn = registro de cambios**. Este valor debe ser especifica la importación de toobe toodo capaz de delta.

Hola te mostramos una lista de registro de cambios de forma predeterminada DNs:

| Directorio | Registro de cambios diferencial |
| --- | --- |
| AD LDS y AD GC de Microsoft |Detectado automáticamente. USNChanged. |
| Apache Directory Server |No disponible. |
| Directory 389 |Registro de cambios. Predeterminado valor toouse: **cn = registro de cambios** |
| IBM Tivoli DS |Registro de cambios. Predeterminado valor toouse: **cn = registro de cambios** |
| Isode Directory |Registro de cambios. Predeterminado valor toouse: **cn = registro de cambios** |
| Novell / NetIQ eDirectory |No disponible. Marca de tiempo. Hola conector utiliza última fecha y hora actualizadas tooget se agrega y actualiza registros. |
| Open DJ/DS |Registro de cambios.  Predeterminado valor toouse: **cn = registro de cambios** |
| Open LDAP |Registro de accesos. Predeterminado valor toouse: **cn = accesslog** |
| Oracle DSEE |Registro de cambios. Predeterminado valor toouse: **cn = registro de cambios** |
| RadiantOne VDS |Directorio virtual. Depende de hello tooVDS de directorio conectado. |
| Sun One Directory Server |Registro de cambios. Predeterminado valor toouse: **cn = registro de cambios** |

atributo de la contraseña de Hello es nombre Hola de Hola Hola de atributo conector debe usar la contraseña de hello tooset en las operaciones de conjunto de contraseña y cambio de contraseña.
Este valor es por su valor predeterminado es demasiado**userPassword** pero puede cambiarse cuando sea necesario para un determinado sistema LDAP.

En la lista de particiones adicionales de hello, es posible tooadd otros espacios de nombres detectado automáticamente. Por ejemplo, esta opción puede usarse si varios servidores forman un clúster lógico, que debe importarse en hello mismo tiempo. Al igual que Active Directory puede tener varios dominios en un bosque, pero todos los dominios comparten un esquema, Hola mismo se pueden simular mediante la especificación de espacios de nombres adicionales de hello en este cuadro. Cada espacio de nombres puede importar desde distintos servidores y además está configurado en la página Configurar particiones y jerarquías de Hola. Utilice Ctrl + Entrar tooget una nueva línea.

### <a name="configure-provisioning-hierarchy"></a>Configurar la jerarquía de aprovisionamiento
Esta página es toomap usado Hola DN componente, por ejemplo, OU, toohello tipo de objeto que debe tener aprovisionado, por ejemplo organizationalUnit.

![Jerarquía de aprovisionamiento](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

Mediante la configuración de jerarquía de aprovisionamiento, puede configurar Hola conector tooautomatically crear una estructura cuando sea necesario. Por ejemplo, si hay un espacio de nombres dc = contoso, dc = com y una nueva objeto cn = Joe, ou = Seattle, c = US, dc = contoso, dc = com se aprovisiona y luego Hola conector puede crear un objeto de país de tipo para Estados Unidos y una organizationalUnit para Seattle si estos no están ya presente en el directorio de Hola.

### <a name="configure-partitions-and-hierarchies"></a>Configurar particiones y jerarquías
En la página de particiones y jerarquías de hello, seleccione todos los espacios de nombres con objetos piensa tooimport y exportación.

![Particiones](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Para cada espacio de nombres, también es tooconfigure posibles opciones de conectividad que reemplazar valores de hello especificados en la pantalla de bienvenida conectividad. Si estos valores se dejan tootheir valor en blanco, se utiliza información de Hola de pantalla de bienvenida conectividad.

También es posible tooselect qué contenedores y las unidades organizativas Hola conector debe importación y exportación para.

Al realizar una búsqueda que esto se realiza en todos los contenedores de partición de Hola. En casos donde hay un gran número de contenedores este comportamiento provoca tooperformance degradación.

>[!NOTE]
A partir de toohello de actualización de marzo de 2017 Hola LDAP genérico búsquedas de conector pueden verse limitadas en contenedores de ámbito tooonly Hola seleccionado. Puede hacerlo seleccionando la casilla hello 'Buscar sólo en los contenedores seleccionados' tal y como se muestra en la imagen de hello siguiente.

![Buscar solo en contenedores seleccionados](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Configuración de delimitadores
Esta página siempre tiene un valor preconfigurado y no se puede cambiar. Si se ha identificado el proveedor del servidor hello, delimitador Hola puede estar rellena con un atributo inmutable, para hello GUID de ejemplo de un objeto. Si no ha sido detectado o se conoce toonot tiene un atributo inmutable y luego conector de hello usa dn (nombre completo) como delimitador de Hola.

![delimitadores](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


Hola te mostramos una lista de servidores LDAP y el delimitador de Hola que se va a utilizar:

| Directorio | Atributo de delimitador |
| --- | --- |
| AD LDS y AD GC de Microsoft |objectGUID |
| 389 Directory Server |dn |
| Apache Directory |dn |
| IBM Tivoli DS |dn |
| Isode Directory |dn |
| Novell / NetIQ eDirectory |GUID |
| Open DJ/DS |dn |
| Open LDAP |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One Directory Server |dn |

## <a name="other-notes"></a>Otras notas
Esta sección proporciona información de aspectos específicos toothis conector o por otras razones tooknow importante.

### <a name="delta-import"></a>Importación diferencial
marca de agua de Hello delta en LDAP abierto es la fecha y hora UTC. Por este motivo, los relojes de hello entre hello LDAP abierto y el servicio de sincronización de FIM deben estar sincronizados. De lo contrario, es posible que se omitan algunas entradas de registro de cambios de hello delta.

Para Novell eDirectory, importación diferencial de hello no está detectando las eliminaciones de objetos. Por esta razón, es necesario toorun una completa periódicamente importar toofind de eliminar todos los objetos.

Para directorios con una diferencia de cambio de registro que se basa en la fecha y hora, es altamente recomendado toorun una importación completa en momentos periódicas. Este proceso permite toofind de motor de sincronización de Hola y diferencias entre el servidor LDAP de Hola y lo que está actualmente en el espacio de conector de Hola.

## <a name="troubleshooting"></a>Solución de problemas
* Para obtener información sobre cómo registro tooenable tootroubleshoot Hola conector, vea hello [cómo tooEnable seguimiento de ETW para conectores](http://go.microsoft.com/fwlink/?LinkId=335731).
