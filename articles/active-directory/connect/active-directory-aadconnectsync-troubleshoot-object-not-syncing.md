---
title: un objeto que no se han sincronizado tooAzure AD aaaTroubleshoot | Documentos de Microsoft
description: "Solucionar problemas de por qué un objeto no se han sincronizado tooAzure AD."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 81e0a0793a1d5ec76cfcaec6e974726d7854f58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-object-that-is-not-synchronizing-tooazure-ad"></a>Solucionar problemas de un objeto que no se han sincronizado tooAzure AD

Si un objeto no se han sincronizado como se esperaba tooAzure AD, puede ser debido a varias razones. Si ha recibido un mensaje de error de Azure AD o si ven errores de hello en Azure AD Connect Health, a continuación, leer [solucionar errores de exportación](active-directory-aadconnect-troubleshoot-sync-errors.md) en su lugar. Pero si está solucionando un problema donde objeto hello no está en Azure AD, a continuación, en este tema es para usted. Describe cómo sincronización los errores de toofind en el componente de local de hello Azure AD Connect.

errores de hello toofind, va toolook en varios sitios en hello siguiendo el orden:

1. Hola [registros de operaciones](#operations) para buscar errores identificados por el motor de sincronización de Hola durante la importación y sincronización.
2. Hola [espacio conector](#connector-space-object-properties) para buscar objetos que faltan y errores de sincronización.
3. Hola [metaverso](#metaverse-object-properties) para buscar problemas relacionados con los datos.

Inicie [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md) antes de comenzar a realizar estos pasos.

## <a name="operations"></a>Operaciones
ficha de operaciones de Hello en hello Synchronization Service Manager es donde debe comenzar la solución de problemas. ficha de operaciones de Hello muestra los resultados de Hola de operaciones más recientes de Hola.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/operations.png)  

mitad superior de Hello muestra todas las ejecuciones en orden crónica. De forma predeterminada, registro de operaciones de hello mantiene información acerca de hello últimos siete días, pero se puede cambiar esta configuración con hello [programador](active-directory-aadconnectsync-feature-scheduler.md). Desea toolook para cualquier serie que no se muestren el estado correcto. Puede cambiar Hola ordenar haciendo clic en los encabezados de Hola.

Hola **estado** columna es la información más importante de Hola y muestra Hola problema más grave para una ejecución. Este es un breve resumen de los estados más comunes de hello en orden de prioridad tooinvestigate (donde * indicar varias cadenas de error posibles).

| Estado | Comentario |
| --- | --- |
| stopped-* |no se pudo completar Hola ejecutar. Por ejemplo, si hello sistema remoto está inactivo y no se puede contactar. |
| stopped-error-limit |Se han generado más de 5000 errores. Hola ejecutar automáticamente se detuvo debido toohello gran número de errores. |
| completed-\*-errors |Hola ejecución se completó, pero existen errores (menos de 5000) que deben investigarse. |
| completed-\*-warnings |Hola ejecutar completó, pero algunos datos no están en estado de espera de Hola. Si se producen errores, es posible que se trate únicamente de un síntoma. Le recomendamos que primero resuelva los errores y que luego investigue las advertencias. |
| Correcto |No hay ningún problema. |

Cuando se selecciona una fila, inferior Hola actualiza los detalles de hello tooshow de que se ejecutan. toohello extremo izquierdo de la parte inferior de hello, es posible que tenga un hablados lista **paso #**. Solo aparecerá si tiene varios dominios en el bosque; cada dominio estará representado por un paso. nombre de dominio de Hello puede encontrarse bajo el encabezado de hello **partición**. En **las estadísticas de sincronización**, también puede encontrar más información acerca del número de Hola de cambios que se han procesado. Puede hacer clic en hello vínculos tooget una lista de objetos de hello cambiado. Si hay objetos con errores, estos se mostrarán en **Errores de sincronización**.

### <a name="troubleshoot-errors-in-operations-tab"></a>Solución de problemas en la pestaña Operaciones
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorsync.png)  
Cuando se producen errores, ambos objetos Hola de error y el propio error Hola son vínculos que proporcionan más información.

Inicio haciendo clic en la cadena de error de hello (**sincronización regla-error-función-desencadenada** en la imagen de hello). Se le presentará una descripción general del objeto de Hola. toosee Hola error real, haga clic en el botón de hello **seguimiento de la pila**. Este seguimiento proporciona información de nivel de depuración para el error de Hola.

Puede hacer clic en hello **información de la pila de llamadas** cuadro, elija **seleccionar todo**, y **copia**. Luego puede copiar pila hello y examine el error de hello en su editor favorito, como el Bloc de notas.

* Si procede error hello **SyncRulesEngine**, a continuación, en primer lugar, información de pila de llamadas de hello tiene una lista de todos los atributos en el objeto de Hola. Desplácese hacia abajo hasta que vea el encabezado de hello **InnerException = >**.  
  ![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/errorinnerexception.png)  
  línea de Hello después muestra Hola error. En la imagen anterior de hello, error de hello es de un Fabrikam de regla de sincronización personalizado creado.

Si el propio error hello no proporcionan suficiente información, es toolook de tiempo en los propios datos Hola. Puede hacer clic Hola vínculo con el identificador de objeto de Hola y continuar solucionando hello [objeto importado de espacio de conector](#cs-import).

## <a name="connector-space-object-properties"></a>Propiedades de objeto del espacio del conector
Si no tiene todos los errores encontrados en hello [operations](#operations) ficha, a continuación, el paso siguiente de hello es toofollow Hola el objeto de espacio de conector de Active Directory, toohello metaverso y tooAzure AD. En esta ruta de acceso, debe encontrar dónde está el problema de Hola.

### <a name="search-for-an-object-in-hello-cs"></a>Buscar un objeto en hello CS

En **Synchronization Service Manager**, haga clic en **conectores**, seleccione Hola conector de Active Directory, y **espacio de conector de búsqueda**.

En **ámbito**, seleccione **RDN** (cuando desee toosearch en el atributo de hello CN) o **DN o delimitador** (cuando desee toosearch en el atributo de hello distinguishedName). Escriba un valor y haga clic en **Buscar**.  
![Búsqueda del espacio conector](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearch.png)  

Si no encuentra el objeto de Hola que está buscando, a continuación, puede que se han filtrado con [filtrado basado en dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) o [filtrado basado en la unidad organizativa](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering). Hola de lectura [configurar el filtrado de](active-directory-aadconnectsync-configure-filtering.md) tooverify de tema que Hola filtrado se configura según lo esperado.

Otra búsqueda útil es tooselect Hola conector de Azure AD, en **ámbito** seleccione **importación pendiente**, seleccione hello y **agregar** casilla de verificación. Esta búsqueda proporciona todos los objetos sincronizados con Azure AD que no se pueden asociar con un objeto local.  
![Búsqueda de objetos huérfanos del espacio de conector](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssearchorphan.png)  
Esos objetos lo han creado otro motor de sincronización o un motor de sincronización con una configuración de filtrado diferente. Esta vista es una lista de objetos **huérfanos** no administrados. Revise esta lista y considere la posibilidad de quitar estos objetos mediante hello [PowerShell de Azure AD](http://aka.ms/aadposh) cmdlets.

### <a name="cs-import"></a>Importación del servidor de configuración
Cuando se abre un objeto cs, hay varias pestañas en la parte superior de Hola. Hola **importar** ficha muestra datos Hola intermedia después de una importación.  
![Objeto del servidor de configuración](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/csobject.png)    
Hola **valor antiguo** muestra lo que se almacena en Connect y hello **nuevo valor** lo que se ha recibido de sistema de origen de hello y no se ha aplicado todavía. Si se produce un error en el objeto de hello, los cambios no se procesan.

**Error**  
![Objeto del servidor de configuración](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cssyncerror.png)  
Hola **Error de sincronización** ficha solo está visible si hay un problema con objeto de Hola. Para obtener más información, consulte el artículo sobre cómo [solucionar errores de sincronización](#troubleshoot-errors-in-operations-tab).

### <a name="cs-lineage"></a>Linaje del servidor de configuración
pestaña de linaje de Hello muestra cómo objeto de espacio de conector de hello es objeto de metaverso toohello relacionados. Puede ver cuando Hola conector última importa un cambio de Hola sistema conectado y qué datos de toopopulate de reglas que se aplican en Hola metaverso.  
![Linaje del servidor de configuración](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineage.png)  
Hola **acción** columna, puede ver hay uno **entrada** la regla de sincronización con la acción de hello **aprovisionar**. Valor que indica que siempre que este objeto de espacio de conector está presente, objeto de metaverso Hola permanece. Si lista Hola de reglas de sincronización en su lugar, muestra una regla de sincronización con la dirección de **saliente** y **aprovisionar**, indica que este objeto se elimina cuando se elimina el objeto de metaverso Hola.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/cslineageout.png)  
También puede ver en hello **PasswordSync** columna que Hola espacio de conector de entrada puede contribuir contraseña toohello de cambios ya que una regla de sincronización con el valor de hello **True**. Esta contraseña se envía tooAzure AD a través de la regla de salida de hello.

Desde la pestaña de linaje de hello, se puede obtener toohello metaverso haciendo clic en [propiedades del objeto de metaverso](#mv-attributes).

En parte inferior de Hola de todas las fichas, hay dos botones: **vista previa** y **registro**.

### <a name="preview"></a>Vista previa
página de vista previa de Hello es toosynchronize usa un único objeto. Resulta útil si está solucionando algunas reglas de sincronización personalizada y desea toosee Hola efecto de un cambio en un único objeto. Puede seleccionar entre **Sincronización completa** y **Sincronización diferencial**. También puede seleccionar entre **generar vista previa**, que mantiene solo cambio de hello en la memoria, y **confirmar Preview**, que actualiza Hola metaverso y todas las fases cambia tootarget espacios de conectores.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/preview.png)  
Puede inspeccionar el objeto de Hola y aplica la regla para un flujo de atributo concreto.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/previewresult.png)

### <a name="log"></a>Registro
página de registro de Hello es historial y estado de sincronización de contraseña de hello toosee usado. Para obtener más información, consulte el artículo sobre la [sincronización de contraseñas](active-directory-aadconnectsync-troubleshoot-password-synchronization.md).

## <a name="metaverse-object-properties"></a>Propiedades de objetos del metaverso
Es mejor toostart realizar búsquedas desde Active Directory de origen de hello [espacio conector](#connector-space). Pero también puede iniciar la búsqueda de metaverso Hola.

### <a name="search-for-an-object-in-hello-mv"></a>Buscar un objeto en hello MV
En **Synchronization Service Manager**, haga clic en **Búsqueda de metaverso**. Crear una consulta que sabe busca Hola usuario. Puede buscar atributos comunes, como accountName (sAMAccountName) y userPrincipalName. Para obtener más información, consulte [Búsqueda de metaverso](active-directory-aadconnectsync-service-manager-ui-mvsearch.md).
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvsearch.png)  

Hola **resultados de la búsqueda** ventana, haga clic en el objeto de Hola.

Si no se encontró el objeto de hello, a continuación, aún no ha llegado Hola metaverso. Continuar toosearch para el objeto de Hola Hola Active Directory [espacio conector](#connector-space-object-properties). Podría haber un error de sincronización que está bloqueando el objeto Hola de metaverso de toohello próximos o podrían haber aplicado un filtro.

### <a name="mv-attributes"></a>Atributos del metaverso
En la ficha de atributos de hello, puede ver los valores de hello y el conector que han contribuido a él.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvobject.png)  

Si un objeto no se han sincronizado, mire Hola siguientes atributos en el metaverso hello:
- ¿Es el atributo de hello **cloudFiltered** presentes y establecidas demasiado**true**? Si es, a continuación, se ha filtrado según los pasos de toohello de [filtrado basado en atributos](active-directory-aadconnectsync-configure-filtering.md#attribute-based-filtering).
- ¿Es el atributo de hello **sourceAnchor** presente? En caso negativo, ¿tiene una topología de bosque de cuenta-recurso? Si un objeto se identifica como un buzón vinculado (atributo Hola **msExchRecipientTypeDetails** posee el valor 2 de Hola), a continuación, hello sourceAnchor es aportado por bosque Hola con una cuenta de Active Directory habilitada. Asegúrese de que cuenta maestra Hola se ha importado y sincronizan correctamente. cuenta maestra Hola debe estar incluido en hello [conectores](#mv-connectors) para el objeto de Hola.

### <a name="mv-connectors"></a>Conectores del metaverso
ficha de conectores de Hello muestra todos los espacios conectores que tienen una representación de objeto de Hola.  
![Sync Service Manager](./media/active-directory-aadconnectsync-troubleshoot-object-not-syncing/mvconnectors.png)  
Debe tener un conector para los siguientes elementos:

- Cada usuario de Hola de bosque de Active Directory se representa en. Esta representación puede incluir foreignSecurityPrincipals y objetos de contacto.
- Un conector de Azure AD.

Si faltan Hola conector tooAzure AD, a continuación, leer [atributos MV](#MV-attributes) criterios de hello tooverify para que se va a aprovisionan tooAzure AD.

Esta pestaña también le permite toonavigate toohello [objeto del espacio del conector](#connector-space-object-properties). Seleccione una fila y haga clic en **Propiedades**.

## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
