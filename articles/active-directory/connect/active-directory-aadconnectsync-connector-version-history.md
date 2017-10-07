---
title: Historial de versiones aaaConnector | Documentos de Microsoft
description: En este tema se enumera todas las versiones de conectores de Hola para Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM)
services: active-directory
documentationcenter: 
author: fimguy
manager: femila
editor: 
ms.assetid: 6a0c66ab-55df-4669-a0c7-1fe1a091a7f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: fimguy
ms.openlocfilehash: 3522f17c30e46542eaa367ecdefdfd2fc47f71a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connector-version-release-history"></a>Historial de versiones de conectores
Conectores de Hola para Forefront Identity Manager (FIM) y Microsoft Identity Manager (MIM) se actualizan con frecuencia.

> [!NOTE]
> Este tema solo está disponible en FIM y MIM. No se admite la instalación de estos conectores en Azure AD Connect. Conectores de lanzamiento se preinstalado en AADConnect al actualizar toospecified compilación.

En este tema se enumeran todas las versiones de hello conectores que se han liberado.

Vínculos relacionados:

* [Descargar los últimos conectores](http://go.microsoft.com/fwlink/?LinkId=717495)
* [conector LDAP genérico](active-directory-aadconnectsync-connector-genericldap.md)
* [conector SQL genérico](active-directory-aadconnectsync-connector-genericsql.md)
* [conector de servicios web](http://go.microsoft.com/fwlink/?LinkID=226245)
* [conector PowerShell](active-directory-aadconnectsync-connector-powershell.md)
* [conector Lotus Domino](active-directory-aadconnectsync-connector-domino.md)


## <a name="116040-aadconnect-pending-release"></a>1.1.604.0 (AADConnect pendiente de publicación)


### <a name="fixed-issues"></a>Problemas corregidos:

* Servicios Web genéricos:
  * Se corrigió un problema que impedía la creación de un proyecto SOAP cuando había dos o más puntos de conexión.
* SQL genérico:
  * En la operación de Hola de importación hello GSQL no se convertir la hora correctamente, cuando guarda tooconnector espacio. Hello formato de fecha y hora predeterminado para el espacio de conector de hello GSQL cambió de 'aaaa-MM-dd ssZ' too'yyyy-MM-dd ssZ '.

## <a name="115510-aadconnect-115530"></a>1.1.551.0 (AADConnect 1.1.553.0)

### <a name="fixed-issues"></a>Problemas corregidos:

* Servicios Web genéricos:
  * herramienta de Hello Wsconfig no convirtió correctamente matriz Json de Hola de "solicitud de ejemplo" para el método de servicio REST de Hola. Esto causaba problemas con la serialización de esta matriz Json de solicitud REST de Hola.
  * La herramienta de configuración del conector de servicio web no admite el uso de espacios en nombres de atributo JSON 
    * Un patrón de sustitución se puede agregar manualmente archivos de WSConfigTool.exe.config de toohello, p. ej.```<appSettings> <add key=”JSONSpaceNamePattern” value="__" /> </appSettings>```

* Lotus Notes:
  * Hola cuando la opción **permitir los certificadores personalizados para las unidades de organización/organización** está deshabilitado Hola conector se produce un error durante la exportación (actualización) después de exportación de hello fluir todos los atributos son tooDomino exportado, pero en tiempo de presentación de exportar un KeyNotFoundException se devuelve tooSync. 
    * Esto sucede porque Hola cambiar el nombre de operación se produce un error cuando intente toochange DN (atributo de nombre de usuario) cambiando uno de los atributos de hello siguientes:  
      - Apellidos
      - Nombre
      - MiddleInitial
      - AltFullName
      - AltFullNameLanguage
      - ou
      - altcommonname

  * Cuando la opción **Allow custom certifiers for Organization/Organizational Units** (Permitir certificadores personalizados para la organización/unidades organizativas) está habilitada pero los certificadores necesarios siguen vacíos, se produce una excepción KeyNotFoundException.

### <a name="enhancements"></a>Mejoras:

* SQL genérico:
  * **Escenario: rediseñado implementado:** característica "*"
  * **Descripción de la solución:** se cambió el enfoque para el [control de los atributos de referencia multivalor](active-directory-aadconnectsync-connector-genericsql.md).


### <a name="fixed-issues"></a>Problemas corregidos:

* Servicios Web genéricos:
  * No se puede importar la configuración del servidor si está presente el conector de WebService
  * El conector de WebService no funciona con varios servicios web

* SQL genérico:
  * No hay tipos de objeto para atributos de referencia de un único valor
  * La importación diferencial en la estrategia de Change Tracking elimina el objeto cuando se quita el valor de la tabla multivalor
  * OverflowException en conector GSQL con DB2 en AS/400

Lotus:
  * Tooenable\disable ha agregado la opción Buscar las unidades organizativas antes de abrir la página de GlobalParameters

## <a name="114430"></a>1.1.443.0

Publicación: marzo de 2017

### <a name="enhancements"></a>Mejoras

* SQL genérico:</br>
  **Síntomas de escenario:** es una limitación conocida con hello conector de SQL donde sólo permiten un tipo de objeto de referencia tooone y requieren una referencia cruzada con los miembros. </br>
  **Descripción de la solución:** en el paso de procesamiento de Hola para las referencias eran "*" se elige la opción, se devolverán todas las combinaciones de tipos de objeto toohello atrás motor de sincronización.

>[!Important]
- Con esto se crearán muchos marcadores de posición
- Es necesario toomake seguro Hola de nomenclatura es único entre los tipos de objeto.


* LDAP genérico:</br>
 **Escenario:** cuando se seleccionan sólo algunos contenedores de partición específica, a continuación, búsqueda de hello todavía se realizará en toda partición. El servicio de sincronización filtrará la partición específica, pero MA no lo hará, lo que podría provocar una degradación del rendimiento. </br>

 **Descripción de la solución:** toomake de código del conector GLDAP cambiado se pueden pasar por todos los contenedores y buscar objetos en cada uno de ellos, en lugar de buscar en toda partición de Hola.


* Lotus Domino:

  **Escenario:** compatibilidad de la eliminación de correo de Domino para la eliminación de una persona durante una exportación. </br>
  **Solución:** configuración de eliminación de correo configurable para la eliminación de una persona durante una exportación.

### <a name="fixed-issues"></a>Problemas corregidos:
* Servicios Web genéricos:
 * Al cambiar la dirección URL del servicio de Hola de forma predeterminada en los proyectos wsconfig SAP a través de la herramienta de configuración de servicio Web, a continuación, Hola tras error ocurre: no se encontró una parte de la ruta de acceso de Hola

      ``'C:\Users\cstpopovaz\AppData\Local\Temp\2\e2c9d9b0-0d8a-4409-b059-dceeb900a2b3\b9bedcc0-88ac-454c-8c69-7d6ea1c41d17\cfg.config\cloneconfig.xml'. ``

* LDAP genérico:
 * Conector GLDAP no ve todos los atributos en AD LDS
 * Asistente para saltos cuando ningún atributo UPN se ha detectado en el esquema de directorio LDAP de Hola
 * Error de importaciones diferenciales cuando no hay errores de detección durante la importación completa, cuando no se selecciona el atributo "objectclass"
 * Una página de configuración "Configurar particiones y jerarquías", no muestra ningún objeto de qué tipo es la partición de toohello igual para los servidores Novel Hola genérico  
genérico. Solo se muestran objetos desde la partición RootDSE.


* SQL genérico:
 * Corrección para el error en que el atributo multivalor de importación diferencial de límite de SQL genérico no se puede importar
 * Cuando se exportan valores eliminados o agregados del atributo multivalor, no se eliminan ni agregan en el origen de datos.  


* Lotus Notes:
 * Un campo específico "Nombre completo" se muestra en el metaverso Hola correctamente sin embargo cuando tooNotes exportar Hola valor de atributo de hello es nulo o está vacío.
 * Corrección para error de certificador duplicado
 * Cuando se selecciona Hola objeto sin ningún dato en hello conector para Lotus Domino con otros objetos que recibimos error de detección de hello al realizar la importación completa.
 * Una vez importación diferencial que se ejecuta en hello conector para Lotus Domino, final Hola de esa ejecución, hello Microsoft.IdentityManagement.MA.LotusDomino.Service.exe servicio a veces devuelve un Error de aplicación.
 * La pertenencia al grupo global funciona correctamente y se mantiene, excepto cuando se ejecuta Hola exportación tootry tooremove un usuario de pertenencia se muestra como correcto con una actualización, pero usuario Hola realmente no se quitan de la pertenencia a Lotus Notes.
 * Un modo de toochoose oportunidad de exportación como "Anexado el elemento final" se agregó en configuración del agente de administración de GUI de Lotus tooappend nuevos elementos en parte inferior durante la exportación de Hola para los atributos con varios valores.
 * Conector agregará Hola necesita Id. de almacén y del archivo de Hola de toodelete de lógica de hello carpeta de correo electrónico.
 * La eliminación de pertenencias no funciona entre los miembros de NAB.
 * Los valores se deben eliminar correctamente del atributo multivalor

## <a name="111170"></a>1.1.117.0
Publicación: marzo de 2016

**Nuevo conector**  
Versión de hello inicial [conector de SQL genérico](active-directory-aadconnectsync-connector-genericsql.md).

**Nuevas características:**

* Conector LDAP genérico:
  * Se agregó compatibilidad para la importación diferencial con Isode.
* Conector de servicios web:
  * Hola actualizada csEntryChangeResult actividad y setImportErrorCode actividad tooallow objeto errores en el nivel toobe toohello atrás devuelto motor de sincronización.
  * Hola actualizada SAP6 y SAP6User plantillas toouse Hola nuevo error nivel funcionalidad del objeto.
* Conector Lotus Domino:
  * Al exportar, necesita un certificador por cada libreta de direcciones. Puede ahora use Hola misma contraseña para todos los certificadores toomake Hola la administración sea más fácil.

**Problemas corregidos:**

* Conector LDAP genérico:
  * En el caso de IBM Tivoli DS, no se detectaban correctamente algunos atributos de referencia.
  * Para LDAP abierto durante una importación delta, se truncan los espacios en blanco al principio de Hola y al final de cadenas.
  * Para Novell y NetIQ, una exportación que mueve un objeto entre las unidades organizativas o contenedores y en hello mismo tiempo objeto Hola cuyo nombre ha cambiado.
* Conector de servicios web:
  * Si el servicio web de hello tuviera varios extremos para el mismo enlace, a continuación, hello conector no correctamente detectó estos extremos.
* Conector Lotus Domino:
  * Una exportación de hello fullName atributo tooa correo electrónico de base de datos no funcionaron.
  * Una exportación que tanto agregar y quitar a miembros de un grupo solo Hola exportado había agregado a los miembros.
  * Si un documento de notas no es válido (Hola atributo isValid establecido toofalse), Hola, a continuación, se produce un error de conector.

## <a name="older-releases"></a>Versiones anteriores
Antes de marzo de 2016, Hola conectores se publicaron como temas de soporte técnico.

**LDAP genérico**

* [KB3078617](https://support.microsoft.com/kb/3078617) : 1.0.0597, septiembre de 2015
* [KB3044896](https://support.microsoft.com/kb/3044896) : 1.0.0549, marzo de 2015
* [KB3031009](https://support.microsoft.com/kb/3031009) : 1.0.0534, enero de 2015
* [KB3008177](https://support.microsoft.com/kb/3008177) : 1.0.0419, septiembre de 2014
* [KB2936070](https://support.microsoft.com/kb/2936070) : 4.3.1082, marzo de 2014

**Servicios web**

* [KB3008178](https://support.microsoft.com/kb/3008178) : 1.0.0419, septiembre de 2014

**PowerShell**

* [KB3008179](https://support.microsoft.com/kb/3008179) : 1.0.0419, septiembre de 2014

**Lotus Domino**

* [KB3096533](https://support.microsoft.com/kb/3096533) : 1.0.0597, septiembre de 2015
* [KB3044895](https://support.microsoft.com/kb/3044895) : 1.0.0549, marzo de 2015
* [KB2977286](https://support.microsoft.com/kb/2977286) : 5.3.0712, agosto de 2014
* [KB2932635](https://support.microsoft.com/kb/2932635) : 5.3.1003, febrero de 2014  
* [KB2899874](https://support.microsoft.com/kb/2899874) : 5.3.0721, octubre de 2013
* [KB2875551](https://support.microsoft.com/kb/2875551) : 5.3.0534, agosto de 2013

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
