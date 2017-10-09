---
title: aaaConnectors en hello Azure AD Synchronization Service Manager UI | Documentos de Microsoft
description: Conocer la ficha conectores Hola Hola Synchronization Service Manager para Azure AD Connect.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 60f1d979-8e6d-4460-aaab-747fffedfc1e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c0969630313178b1e299385b1289360c8f787cb5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-connectors-with-hello-azure-ad-connect-sync-service-manager"></a>Uso de conectores con hello Azure AD Connect Sync Service Manager

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectors.png)

ficha de conectores de Hello es usado toomanage motor de sincronización de todos los sistemas Hola está conectado a.

## <a name="connector-actions"></a>Acciones del conector
| Acción | Comentario |
| --- | --- |
| Crear |No usar. Para conectar los bosques de AD tooadditional, usar a Asistente para la instalación de Hola. |
| Propiedades |Se usa para el filtrado por dominio y unidad organizativa. |
| [Eliminar](#delete) |Tooeither usado eliminar datos de Hola Hola conector espacio o toodelete conexión tooa bosque. |
| [Configurar perfiles de ejecución](#configure-run-profiles) |Excepción de filtrado, nada de dominio tooconfigure aquí. Esta acción se puede utilizar perfiles de ejecución de toosee ya configurado. |
| Ejecute |Usar toostart ejecutar único de un perfil. |
| Detención |Detiene un conector que esté ejecutando un perfil. |
| Exportar conector |No usar. |
| Importar conector |No usar. |
| Actualizar conector |No usar. |
| Actualizar esquema |Actualiza el esquema en caché de Hola. Es toouse preferido Hola opción en el Asistente para la instalación de hello en su lugar, desde el que también las actualizaciones de sincronización las reglas. |
| [Espacio del conector de búsqueda](#search-connector-space) |Usar objetos de toofind y demasiado[siga un objeto y sus datos a través del sistema de hello](#follow-an-object-and-its-data-through-the-system). |

### <a name="delete"></a>Eliminar
acción de eliminación de Hello sirve para dos cosas distintas.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/connectordelete.png)

Hola opción **eliminar solo el espacio del conector** quita todos los datos, pero mantener Hola configuración.

Hola opción **espacio conector eliminar y el conector** quita los datos de Hola y configuración de Hola. Esta opción se usa cuando no desea tooconnect tooa bosque ya.

Ambas opciones sincronización todos los objetos y actualización los objetos de metaverso de Hola. Se trata de una operación de larga duración.

### <a name="configure-run-profiles"></a>Configurar perfiles de ejecución
Esta opción permite hello toosee configurados para un conector de perfiles de ejecución.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/configurerunprofiles.png)

### <a name="search-connector-space"></a>Espacio del conector de búsqueda
acción de espacio de conector de búsqueda de Hello es útil toofind objetos y solucionar problemas de datos.

![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearch.png)

Empiece seleccionando un **ámbito**. Puede buscar la base de datos (RDN, DN, delimitador, subárbol), o de estado del objeto de hello (todas las demás opciones).  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchscope.png)  
Por ejemplo, si hace una búsqueda de un subárbol, obtiene todos los objetos de una unidad organizativa.  
![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/cssearchsubtree.png)  
En esta cuadrícula puede seleccionar un objeto, seleccione **propiedades**, y [seguirlo](active-directory-aadconnectsync-troubleshoot-object-not-syncing.md) de espacio del conector de origen de hello, mediante el metaverso hello y el espacio de conector de destino toohello.

### <a name="changing-hello-ad-ds-account-password"></a>Cambiar la contraseña de la cuenta de hello AD DS
Si cambia la contraseña de la cuenta de hello, Hola servicio de sincronización ya no será capaz de tooimport y exportación de cambios tooon local AD.   Puede ver la siguiente hello:

- se produce un error en el paso de importación y exportación de Hola para hello conector AD con error de "credenciales de inicio no".
- En el Visor de eventos de Windows, registro de eventos de aplicación Hola contiene un error con 6000 de Id. de evento y el mensaje "hello toorun de agente"contoso.com"Error de administración porque las credenciales de hello no eran válidas."

Hola tooresolve emitir, cuenta de usuario de actualización Hola AD DS con hello siguientes:


1. Iniciar Hola Synchronization Service Manager (servicio de sincronización de inicio →).
</br>![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)
2. Vaya toohello **conectores** ficha.
3. Seleccione Hola conector de AD que es configurado toouse hello cuenta AD DS.
4. En Acciones, seleccione **Propiedades**.
5. En el cuadro de diálogo emergente de hello, seleccione Conectar tooActive directorio de bosque:
6. nombre de bosque de Hello indica Hola correspondiente local AD.
7. nombre de usuario de Hello indica la cuenta de hello AD DS usada para la sincronización.
8. Escriba Hola nueva contraseña de cuenta de hello AD DS en el cuadro de texto de contraseña de hello ![Azure AD conectarse sincronización de cifrado de clave de utilidad](media/active-directory-aadconnectsync-encryption-key/key6.png)
9. Haga clic en Aceptar toosave Hola nueva contraseña y reinicie Hola Synchronization Service tooremove Hola contraseña antigua de la memoria caché.



## <a name="next-steps"></a>Pasos siguientes
Obtener más información sobre hello [sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuración.

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
