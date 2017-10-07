---
title: "Sincronización de Azure AD Connect: evitar eliminaciones accidentales | Microsoft Docs"
description: "Este tema describe Hola evitar la característica de eliminaciones accidentales (evitar eliminaciones accidentales) en Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6b852cb4-2850-40a1-8280-8724081601f7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 159597f8354806fcaea1430e0ff84956338592a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-prevent-accidental-deletes"></a>Sincronización de Azure AD Connect: cómo evitar eliminaciones accidentales
Este tema describe Hola evitar la característica de eliminaciones accidentales (evitar eliminaciones accidentales) en Azure AD Connect.

Al instalar Azure AD Connect, evitar accidental eliminaciones está habilitada de forma predeterminada y toonot configurado permiten una exportación con más de 500 eliminaciones. Esta característica está diseñada tooprotect desde la configuración accidental cambia y cambia el directorio local de tooyour que afectaría a muchos usuarios y otros objetos.

## <a name="what-is-prevent-accidental-deletes"></a>Qué significa evitar eliminaciones accidentales
Algunos de los escenarios comunes en los que puede observar esto son los siguientes:

* También cambia[filtrado](active-directory-aadconnectsync-configure-filtering.md) donde toda una [OU](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering) o [dominio](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering) está seleccionada.
* Se eliminan todos los objetos de una unidad organizativa.
* Se cambia el nombre de una unidad organizativa para que todos los objetos se consideran toobe fuera del ámbito de sincronización.

valor predeterminado de Hola de 500 objetos puede cambiarse con PowerShell mediante `Enable-ADSyncExportDeletionThreshold`. Debe configurar este tamaño de hello toofit de valor de su organización. Puesto que el programador de sincronización de Hola ejecuta cada 30 minutos, el valor de hello es número de Hola de eliminaciones que se ve dentro de 30 minutos.

Si hay demasiados toobe eliminaciones provisionalmente exporta tooAzure AD, hello exportación se detendrá y recibir un correo electrónico similar al siguiente:

![Evitar eliminaciones accidentales del correo electrónico](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/email.png)

> *Hola (contacto técnico). En (tiempo) Hola servicio de sincronización de identidad ha detectado que número Hola de eliminaciones superado el umbral de eliminación configurado de Hola para (nombre de la organización). En esta sincronización de identidades, se envía un total de (número) objetos para su eliminación. Esto cumple o supera Hola configurado el valor del umbral de eliminación de objetos de (número). Necesitamos confirmación tooprovide que estas eliminaciones debe procesar antes de que se llevará a cabo. Vea Hola evitar eliminaciones accidentales para obtener más información acerca de Hola de error incluido en este mensaje de correo electrónico.*
>
> 

También puede ver el estado de hello `stopped-deletion-threshold-exceeded` cuando busque en hello **Synchronization Service Manager** interfaz de usuario para el perfil de exportación de Hola.
![Evitar eliminaciones accidentales: Interfaz de usuario de Synchronization Service Manager](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/syncservicemanager.png)

Si no es lo esperado, investigue y tome las medidas correctivas oportunas. toosee los objetos que son sobre toobe elimina, Hola siguientes:

1. Iniciar **servicio de sincronización de** de hello menú Inicio.
2. Vaya demasiado**conectores**.
3. Seleccione Hola conector con el tipo de **Azure Active Directory**.
4. En **acciones** toohello a la derecha, seleccione **espacio de conector de búsqueda**.
5. Hola emergente en **ámbito**, seleccione **desconectado desde** y elija una hora en hello anterior. Haga clic en **Buscar**. Esta página proporciona una vista de todos los objetos sobre toobe eliminado. Haciendo clic en cada elemento, puede obtener información adicional sobre el objeto de Hola. También puede hacer clic en **valor columnas** tooadd adicional atributos toobe visible en la cuadrícula de Hola.

![Espacio del conector de búsqueda](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/searchcs.png)

Si desea iniciar todas las eliminaciones de hello, a continuación, Hola siguientes:

1. tooretrieve Hola eliminación umbral actual, ejecute el cmdlet de PowerShell de hello `Get-ADSyncExportDeletionThreshold`. Proporcione una cuenta y una contraseña de administrador global de Azure AD. valor predeterminado de Hello es 500.
2. tootemporarily deshabilitar dicha protección y dejar que las eliminaciones recorrer, ejecute el cmdlet de PowerShell de hello: `Disable-ADSyncExportDeletionThreshold`. Proporcione una cuenta y una contraseña de administrador global de Azure AD.
   ![Credenciales](./media/active-directory-aadconnectsync-feature-prevent-accidental-deletes/credentials.png)
3. Con hello Azure Active Directory Connector aún seleccionado, Seleccionar acción de hello **ejecutar** y seleccione **exportar**.
4. toore-habilitar la protección hello, ejecute el cmdlet de PowerShell de hello: `Enable-ADSyncExportDeletionThreshold -DeletionThreshold 500`. Reemplace 500 por valor Hola observado al recuperar el umbral de eliminación actual de Hola. Proporcione una cuenta y una contraseña de administrador global de Azure AD.

## <a name="next-steps"></a>Pasos siguientes
**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
