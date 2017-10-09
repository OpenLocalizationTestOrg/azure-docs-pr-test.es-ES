---
title: "integración de aaaDirectory entre Active Directory y la autenticación multifactor Azure"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo toointegrate Hola servidor Azure Multi-factor Authentication con Active Directory para poder sincronizar los directorios de Hola."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Integración de directorios entre Servidor Azure MFA y Active Directory
Utilice la sección de integración de directorios de Hola de hello servidor Azure MFA toointegrate con Active Directory u otro directorio LDAP. Puede configurar el esquema de directorio de atributos toomatch hello y configurar la sincronización automática de usuarios.

## <a name="settings"></a>Settings
De forma predeterminada, Hola servidor Azure Multi-factor Authentication (MFA) es tooimport configurado o sincronizar usuarios desde Active Directory.  pestaña de integración de directorios de Hello permite toooverride Hola comportamiento predeterminado y toobind tooa otro directorio LDAP, un directorio ADAM o controlador de dominio de Active Directory específico.  También se proporciona para su uso de Hola de autenticación LDAP tooproxy LDAP o enlazar LDAP como destino RADIUS, autenticación previa para la autenticación de IIS o la autenticación principal para el Portal de usuarios.  Hello en la tabla siguiente describe opciones de configuración individuales de Hola.

![Settings](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| Característica | Description |
| --- | --- |
| Usar Active Directory |Seleccione toouse de opción de uso de Active Directory de hello Active Directory para la importación y sincronización.  Se trata de una configuración predeterminada de Hola. <br>Nota: Para Active Directory integration toowork correctamente, unirse a dominio tooa de hello equipo e inicie sesión con una cuenta de dominio. |
| Incluir dominios de confianza |Comprobar **incluir dominios de confianza** toohave Hola agente intento tooconnect toodomains de confianza para Hola dominio actual, otro dominio en el bosque de Hola o dominios implicados en una relación de confianza de bosque.  Cuando no importar o sincronizar usuarios desde cualquiera de hello dominios de confianza, desactive la opción de rendimiento de tooimprove de casilla de verificación de Hola.  se comprueba el valor predeterminado de Hola. |
| Usar la configuración LDAP específica |Seleccione Hola usar LDAP opción toouse Hola configuración LDAP especificada para la importación y sincronización. Nota: Cuando se selecciona usar LDAP, interfaz de usuario de hello cambia las referencias de tooLDAP de Active Directory. |
| Botón Editar |botón de edición de Hello permite toomodified de configuración de LDAP actual de hello configuración. |
| Usar consultas de ámbito de atributo |Indica si se deben usar consultas de ámbito de atributo.  Las consultas de ámbito de atributo permiten búsquedas de directorio eficientes que califiquen registros basados en las entradas de hello en otros atributos de registro.  Hola servidor Azure Multi-factor Authentication utiliza el atributo ámbito consultas tooefficiently consultar Hola a los usuarios que sean miembros de un grupo de seguridad.   <br>Nota: existen algunos casos donde se admiten las consultas de ámbito de atributo pero no deberían usarse.  Por ejemplo, Active Directory puede tener problemas con las consultas de ámbito de atributo cuando un grupo de seguridad contiene miembros de más de un dominio. En este caso, anule la selección de casilla de verificación de Hola. |

Hello en la tabla siguiente describe opciones de configuración de LDAP de Hola.

| Característica | Description |
| --- | --- |
| Server |Escriba el nombre de host de Hola o dirección IP del servidor de hello ejecutan el directorio LDAP de Hola.  También puede especificar un servidor de copia de seguridad separado por un punto y coma. <br>Nota: Cuando Tipo de enlace es SSL, se requiere un nombre de host completo. |
| DN base |Escriba el nombre distintivo de Hola Hola base del objeto de directorio desde el que se iniciarán todas las consultas de directorio.  Por ejemplo, dc=abc,dc=com. |
| Tipo de enlace - Consultas |Seleccione el tipo de enlace apropiado de Hola para su uso cuando se enlaza el directorio LDAP de toosearch Hola.  Se utiliza para importaciones, sincronización y resolución de nombres de usuario. <br><br>  Anónimo: se realiza un enlace anónimo.  No se utilizan el DN ni la contraseña de enlace.  Esto solo funciona si el directorio LDAP de hello permite el enlace anónimo y los permisos permiten Hola consulta de atributos y los registros adecuados de Hola.  <br><br> Simple - DN de enlace y la contraseña de enlace se pasan como directorio de texto sin formato toobind toohello LDAP.  Esto es para fines de prueba, tooverify que Hola servidor es alcanzable y esa cuenta de enlace de hello tenga acceso adecuado de Hola. Después de que se ha instalado el certificado adecuado de hello, use SSL en su lugar.  <br><br> SSL - DN de enlace y la contraseña de enlace se cifra mediante SSL toobind toohello LDAP directory.  Instalar un certificado localmente que Hola confianzas de directorio LDAP.  <br><br> Windows: nombre de usuario y contraseña de enlace se usa toosecurely conectar tooan controlador de dominio de Active Directory o directorio ADAM.  Si el enlace se deja en blanco, Hola ha iniciado la sesión de cuenta de usuario es toobind usado. |
| Tipo de enlace: autenticaciones |Seleccione el tipo de enlace apropiado de Hola para su uso al realizar la autenticación de enlace LDAP.  Ver una descripción de tipo de enlace de hello en tipo de enlace - consultas.  Por ejemplo, esto permite toobe enlace anónimo utilizado para las consultas durante el enlace SSL es las autenticaciones de enlace LDAP de toosecure usado. |
| DN de enlace o Nombre de usuario de enlace |Escriba nombre distintivo Hola de registro de usuario de Hola para hello cuenta toouse al enlazar toohello directorio LDAP.<br><br>nombre distintivo del enlace Hola sólo se utiliza cuando el tipo de enlace es Simple o SSL.  <br><br>Escriba el nombre de usuario de Hola de toouse de cuenta de Windows hello al enlazar el directorio LDAP de toohello cuando el tipo de enlace es Windows.  Si se deja en blanco, Hola ha iniciado la sesión de cuenta de usuario es toobind usado. |
| Contraseña de enlace |Escriba la contraseña de enlace de Hola para hello DN de enlace o nombre de usuario que se va a directorio LDAP de toohello de toobind usado.  contraseña tooconfigure Hola Hola servicio Multi-factor Auth Server AdSync, habilitar la sincronización y asegúrese de que el servicio de hello está ejecutando en el equipo local de Hola.  se guardó la contraseña de Hello en hello Windows nombres y contraseñas en Hola Hola de cuenta que se ejecuta el servicio Multi-factor Auth Server AdSync como.  También se guarda la contraseña de Hello en Hola Hola de cuenta se está ejecutando como interfaz de usuario se ejecuta como y en Hola Hola de cuenta servicio de servidor de autenticación multifactor de servidor de Multi-factor Auth.  <br><br>Puesto que la contraseña de hello solo se almacena en los nombres de usuario de Windows almacena y las contraseñas del servidor local de hello, repita este paso en cada servidor de autenticación multifactor que necesita acceso toohello contraseña. |
| Límite de tamaño de consulta |Especificar el límite de tamaño de hello para el número máximo de Hola de usuarios que se devuelve de una búsqueda en directorios.  Este límite debe coincidir con la configuración de hello en el directorio LDAP de Hola.  Para búsquedas grandes donde no se admite la paginación, importación y sincronización intenta tooretrieve a los usuarios en lotes.  Si el límite de tamaño de hello especificado aquí es mayor que el límite de hello configurado en el directorio LDAP de hello, pueden faltar algunos usuarios. |
| Botón Probar |Haga clic en **prueba** servidor LDAP de tootest enlace toohello.  <br><br>No es necesario hello tooselect **usar LDAP** opción tootest enlace. Esto permite Hola enlace toobe probado antes de usar la configuración de LDAP de Hola. |

## <a name="filters"></a>Filtros
Los filtros permiten registros tooqualify de tooset criterios al realizar una búsqueda en directorios.  Establecer filtro de hello, puede restringir el ámbito Hola objetos desea toosynchronize.  

![Filtros](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

La autenticación multifactor Azure tiene Hola tres opciones de filtro siguientes:

* **Filtro de contenedor** -especifique criterios de filtro de hello utilizan registros de contenedor de tooqualify al realizar una búsqueda en directorios.  Para Active Directory y ADAM, se suele usar (|(objectClass=organizationalUnit)(objectClass=container)).  Para otros directorios LDAP, utilice criterios de filtro que califiquen cada tipo de objeto de contenedor, según el esquema de directorio de Hola.  <br>Nota: Si se deja en blanco, se usará ((objectClass=organizationalUnit)(objectClass=container)) de forma predeterminada.
* **Filtro de grupo de seguridad** -especifique criterios de filtro de hello utilizan registros de grupo de seguridad de tooqualify al realizar una búsqueda en directorios.  Para Active Directory y ADAM, se suele usar (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)).  Para otros directorios LDAP, utilice criterios de filtro que califiquen cada tipo de objeto de grupo de seguridad, según el esquema de directorio de Hola.  <br>Nota: Si se deja en blanco, se usa (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648)) de forma predeterminada.
* **Filtro de usuarios** -especifique criterios de filtro de hello utilizan registros de usuario de tooqualify al realizar una búsqueda en directorios.  Para Active Directory y ADAM, se suele utilizar (&(objectClass=user)(objectCategory=person)).  Para otros directorios LDAP, use (objectClass = inetOrgPerson) o algo similar, según el esquema de directorio de Hola. <br>Nota: Si se deja en blanco, se usa (&(objectCategory=person)(objectClass=user)) de forma predeterminada.

## <a name="attributes"></a>Attributes
Puede personalizar los atributos según sea necesario para un determinado directorio.  Esto permite atributos personalizados tooadd y ajustar los atributos de Hola de tooonly de sincronización de Hola que necesita. Utilice el nombre de Hola de hello attricute tal como se define en el esquema de directorio de hello para el valor de Hola de cada campo de atributo. Hello tabla siguiente proporciona información adicional sobre cada característica.

Los atributos pueden introducirse manualmente y no son toomatch requiere un atributo en la lista de atributos de Hola.

![Attributes](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| Característica | Description |
| --- | --- |
| Identificador único |Escriba el nombre de atributo de hello del atributo de Hola que actúa como identificador único de Hola de contenedor, grupo de seguridad y registros de usuario.  En Active Directory, suele ser objectGUID. Otras implementaciones LDAP pueden usar entryUUID o similar.  valor predeterminado de Hello es objectGUID. |
| Tipo de identificador único |Seleccione el tipo de Hola de atributo del identificador único de Hola.  En Active Directory, el atributo objectGUID de hello es de tipo GUID. Otras implementaciones LDAP pueden usar el tipo Matriz de bytes ASCII o Cadena.  valor predeterminado de Hello es GUID. <br><br>Es importante tooset se hace referencia a este tipo de correctamente desde elementos de sincronización por su identificador único. Hola tipo de identificador único es objeto de Hola de toodirectly usa Buscar en el directorio de Hola.  Establecer este tipo tooString al directorio de hello almacena realmente el valor de hello como una matriz de bytes de caracteres ASCII impide que la sincronización funcione correctamente. |
| Nombre distintivo |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre distintivo de Hola para cada registro.  En Active Directory, suele ser distinguishedName. Otras implementaciones LDAP pueden usar entryDN o similar.  Hola predeterminada es distinguishedName. <br><br>Si no existe un atributo con hello nombre distintivo, puede utilizarse el atributo adspath de Hola.  Hola "LDAP: / /\<server\>/" parte de la ruta de acceso de Hola se extrae automáticamente desactivado, dejando sólo Hola nombre distintivo del objeto de Hola. |
| Nombre del contenedor |Escriba el nombre de atributo de hello del atributo de Hola que contiene el nombre de hello en un registro de contenedor.  valor de Hola de este atributo se muestra en la jerarquía de contenedores de hello al importar desde Active Directory o agregar elementos de sincronización.  Hola predeterminado es nombre. <br><br>Si varios contenedores usan distintos atributos para sus nombres, use punto y coma tooseparate varios atributos de nombre de contenedor.  primer atributo de nombre de contenedor Hola se encuentra en un objeto de contenedor es toodisplay usa su nombre. |
| Nombre de grupo de seguridad |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre de hello en un registro de grupo de seguridad.  valor de Hola de este atributo se muestra en la lista de grupos de seguridad de hello al importar desde Active Directory o agregar elementos de sincronización.  Hola predeterminado es nombre. |
| Nombre de usuario |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre de usuario de hello en un registro de usuario.  valor de Hola de este atributo se utiliza como nombre de usuario de servidor Multi-factor Auth Hola.  Puede especificar un segundo atributo como una copia de seguridad toohello en primer lugar.  atributo de segundo Hola solo se utiliza si Hola primer atributo no contiene un valor para el usuario de Hola.  Hola los valores predeterminados son userPrincipalName y sAMAccountName. |
| Nombre |Escriba el nombre de atributo de hello del atributo de Hola que contiene nombre hello en un registro de usuario.  valor predeterminado de Hello es givenName. |
| Apellidos |Escriba el nombre de atributo de hello del atributo de Hola que contiene el apellido de hello en un registro de usuario.  valor predeterminado de Hello es sn. |
| Dirección de correo electrónico |Escriba el nombre de atributo de Hola de atributo de Hola que contiene la dirección de correo electrónico de hello en un registro de usuario.  Dirección de correo electrónico es toosend usado bienvenida y actualización de usuario de toohello de mensajes de correo electrónico.  valor predeterminado de Hello es correo electrónico. |
| Grupo de usuarios |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el grupo de usuarios de hello en un registro de usuario.  Grupo de usuarios puede ser usuarios de toofilter usado en el agente de Hola y en informes del Portal de administración de servidor de autenticación multifactor Hola. |
| Descripción |Escriba el nombre de atributo de Hola de atributo de Hola que contiene la descripción de hello en un registro de usuario.  La descripción solo se utiliza para realizar búsquedas.  opción predeterminada de Hello es description. |
| Idioma de llamadas de teléfono |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre corto Hola de hello idioma toouse para llamadas de voz para el usuario de Hola. |
| Idioma de mensajes de texto |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre corto Hola de hello idioma toouse para mensajes de texto SMS para el usuario de Hola. |
| Idioma de aplicaciones móviles |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre corto Hola de hello idioma toouse para mensajes de texto de aplicación de teléfono para el usuario de Hola. |
| Idioma de token OATH |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el nombre corto Hola de hello toouse de idioma para los mensajes de texto de token OATH para el usuario de Hola. |
| Teléfono del trabajo |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de teléfono de negocio de hello en un registro de usuario.  valor predeterminado de Hello es telephoneNumber. |
| Teléfono particular |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de teléfono particular de hello en un registro de usuario.  valor predeterminado de Hello es homePhone. |
| Buscapersonas |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de buscapersonas de hello en un registro de usuario.  valor predeterminado de Hello es pager. |
| Teléfono móvil |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de teléfono móvil de hello en un registro de usuario.  valor predeterminado de Hello es móvil. |
| Fax |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de fax de hello en un registro de usuario.  Hola predeterminada es facsimileTelephoneNumber. |
| Teléfono IP |Escriba el nombre de atributo de Hola de atributo de Hola que contiene el número de teléfono IP de hello en un registro de usuario.  valor predeterminado de Hello es ipPhone. |
| Personalizado |Escriba el nombre de atributo de hello del atributo de Hola que contiene un número de teléfono personalizado en un registro de usuario.  valor predeterminado de Hello es en blanco. |
| Extensión |Escriba el nombre de atributo de Hola de atributo de Hola que contiene la extensión del número de teléfono hello en un registro de usuario.  valor de Hola de campo de extensión de Hola se utiliza como número de teléfono principal solo de hello extensión toohello.  valor predeterminado de Hello es en blanco. <br><br>Si no se especifica el atributo de extensión de hello, las extensiones se pueden incluidas como parte de atributo de teléfono de Hola. En este caso, preceden extensión Hola por una 'x' para que se obtiene analizar correctamente.  Por ejemplo, se crearán 555-123-4567 x890 555-123-4567 como número de teléfono de Hola y 890 como extensión de Hola. |
| Botón Restaurar valores predeterminados |Haga clic en **Restaurar valores predeterminados** tooreturn valor predeterminado de tootheir hacer copia de todos los atributos.  Hola los valores predeterminados deben funcionar correctamente con el esquema de Active Directory o ADAM normal Hola. |

atributos de tooedit, haga clic en **editar** en la ficha de atributos de Hola.  Se abrirá una ventana donde puede editar los atributos de Hola. Seleccione hello **...**  siguiente tooany atributo tooopen una ventana donde puede elegir qué toodisplay atributos.

![Editar atributos](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>Sincronización
La sincronización mantiene hello Azure MFA usuario base de datos sincronizada con los usuarios de hello en Active Directory o en otro directorio de Lightweight Directory Access Protocol (LDAP). proceso de Hello es similar usuarios tooimporting manualmente desde Active Directory, pero se sondea periódicamente para el usuario de Active Directory y grupo de seguridad cambia tooprocess.  También deshabilita o quita los usuarios que se quitaron de un contenedor, grupo de seguridad o Active Directory.

Hola servicio Multi-factor Auth ADSync es un servicio de Windows que realiza Hola periódica de sondeo de Active Directory.  Esto no es toobe confundirse con sincronización de Azure AD o Azure AD Connect.  Hola Multi-factor Auth ADSync, aunque se basa en un código base similar, es específico toohello servidor Azure Multi-factor Authentication.  Se instala en un estado detenido y se inicia con hello servicio del servidor Multi-factor Auth cuando está configurado toorun.  Si tiene una configuración de servidor de autenticación multifactor de varios servidores, hello Multi-factor Auth ADSync sólo puede ejecutarse en un único servidor.

Hola servicio Multifactorauthadsync usa Hola extensión del servidor LDAP DirSync proporcionada por sondeo tooefficiently de Microsoft para los cambios.  Este llamador de control DirSync debe tener Hola "directory get cambios" control extendido DS-Replication-Get-Changes y secundario derecho de acceso.  De forma predeterminada, estos derechos se asignan toohello las cuentas de administrador y LocalSystem en controladores de dominio.  Hola servicio Multifactorauthadsync está configurado toorun como LocalSystem de forma predeterminada.  Por lo tanto, es más sencillo servicio de hello toorun en un controlador de dominio.  Si configura Hola servicio tooalways realizar una sincronización completa, puede ejecutar como una cuenta con menos permisos.  Esto es menos eficaz, pero requiere menos privilegios de cuenta.

Si el directorio LDAP de hello es compatible y está configurado para la sincronización de directorios, a continuación, sondeo para que funcionen los cambios de grupo de seguridad de usuarios y Hola igual como lo hace con Active Directory.  Si el directorio LDAP de hello no admite Hola control DirSync, se realiza una sincronización completa durante cada ciclo.

![Sincronización](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

Hello tabla siguiente contiene información adicional sobre cada una de las opciones de pestañas de sincronización de Hola.

| Característica | Description |
| --- | --- |
| Habilitar sincronización con Active Directory |Al activar esta opción, Hola servicio servidor Multi-factor Auth sondea periódicamente Active Directory para los cambios. <br><br>Nota: debe agregarse al menos un elemento de sincronización y sincronizar ahora debe realizarse antes de hello servidor Multi-factor Auth servicio empiece a procesar cambios. |
| Sincronizar cada |Especifique Hola Hola de intervalo de tiempo servidor Multi-factor Auth servicio esperará entre el sondeo y procesamiento de cambios. <br><br> Nota: especificado el intervalo de saludo es tiempo de hello entre comienzo Hola de cada ciclo.  Si los cambios de procesamiento en tiempo de hello superan el intervalo de saludo, servicio de hello volverá a sondear inmediatamente. |
| Quitar usuarios que ya no estén en Active Directory  |Al activar esta opción, Hola servicio servidor Multi-factor Auth procesará los desechos de usuarios eliminados de Active Directory y quitar Hola relacionados con servidor Multi-factor Auth usuario. |
| Realizar siempre una sincronización completa |Al activar esta opción, Hola servicio servidor Multi-factor Auth siempre realizará una sincronización completa.  Si está desactivada, Hola servicio servidor Multi-factor Auth realizará una sincronización incremental consultando solo los usuarios que han cambiado.  Hola predeterminada no está marcada. <br><br>Si está desactivada, servidor Azure MFA realiza sincronización incremental solo cuando directory Hola admite el control de sincronización de directorios de Hola y el directorio de toohello de enlace de hello cuenta tiene consultas incrementales de DirSync de tooperform de permisos.  Si Hola cuenta no tiene los permisos adecuados de Hola o varios dominios implicados en la sincronización de hello, servidor de MFA de Azure realiza una sincronización completa. |
| Requerir autorización del administrador cuando se quiten o deshabiliten más de X usuarios |Elementos de sincronización pueden ser toodisable configurado o quitar los usuarios que ya no están miembro del grupo de seguridad o contenedor del elemento de Hola.  Como medida de seguridad, puede se requiera la aprobación del administrador cuando Hola número de usuarios toodisable o quitar supera un umbral.  Cuando está activado, se requiere autorización para el umbral especificado.  valor predeterminado de Hello es 5 y el intervalo de hello es 1 too999. <br><br> La aprobación se facilita enviando primero una tooadministrators de notificación de correo electrónico. notificación de correo electrónico de Hello proporciona instrucciones para revisar y aprobar Hola deshabilitación y eliminación de usuarios.  Cuando se inicia la interfaz de usuario de hello servidor Multi-factor Auth, solicitará su aprobación. |

Hola **sincronizar ahora** botón permite toorun una sincronización completa para la sincronización de hello elementos especificados.  Es necesaria una sincronización completa cuando se agregan, modifican, quitan o reordenan elementos de sincronización.  También es necesario antes de hello servicio Multifactorauthadsync está operativo, ya que establece Hola desde el que el servicio de hello realizará el sondeo de cambios incrementales de punto de partida.  Si se han realizado cambios toosynchronization elementos pero no se ha realizado una sincronización completa, es posible que tooSynchronize solicitada ahora.

Hola **quitar** botón permite Hola administrador toodelete uno o varios elementos de sincronización de la lista de elementos de sincronización de servidor Multi-factor Auth Hola.

> [!WARNING]
> Una vez quitado un registro de elemento de sincronización, no se puede recuperar. Necesitará sincronización de hello tooadd registro de elemento nuevo si lo eliminó por error.

elemento de sincronización de Hola o elementos de sincronización se eliminaron desde el servidor Multi-factor Auth.  Hola servicio servidor Multi-factor Auth ya no procesará los elementos de sincronización de Hola.

botones Subir y Bajar de Hello permiten a administrador Hola orden de hello toochange de elementos de sincronización de Hola.  Hello orden es importante porque hello mismo usuario puede ser un miembro de más de un elemento de sincronización (por ejemplo, un contenedor y un grupo de seguridad).  configuración de Hello usuario toohello aplicada durante la sincronización procederá del primer elemento de sincronización hello en hello lista toowhich Hola de usuario está asociado.  Por lo tanto, se deben colocar elementos de sincronización de hello en orden de prioridad.

> [!TIP]
> Se debe realizar una sincronización completa después de quitar elementos de sincronización.  Es necesario realizar una sincronización completa después de ordenar elementos de sincronización.  Haga clic en **sincronizar ahora** tooperform una sincronización completa.

## <a name="multi-factor-auth-servers"></a>Servidores Multi-Factor Authentication
Servidores adicionales de autenticación multifactor puede configurarse tooserve como un copia de seguridad proxy RADIUS, proxy LDAP, o para la autenticación de IIS. configuración de la sincronización de Hola se comparte entre todos los agentes de Hola. Sin embargo, sólo uno de estos agentes puede tener el servicio servidor Multi-factor Auth Hola que se ejecuta. Esta pestaña permite tooselect Hola servidor Multi-factor Auth debe habilitarse para la sincronización.

![Servidores Multi-Factor Authentication](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
