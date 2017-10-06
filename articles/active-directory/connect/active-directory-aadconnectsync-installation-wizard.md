---
title: "Volver a ejecutar Asistente de instalación de Connect de hello Azure AD | Documentos de Microsoft"
description: "Explica cómo el Asistente para instalación de hello funciona Hola segunda vez que se ejecuta."
keywords: "Asistente para la instalación de Hello AD Azure Connect permite configurar Hola de configuración de mantenimiento segunda vez que se ejecuta"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a>Azure AD Connect sync: ejecutando el Asistente para la instalación de hello otra vez
Hello primera vez que ejecute el Asistente para la instalación de hello Azure AD Connect, le explicamos cómo tooconfigure la instalación. Si ejecuta el Asistente para la instalación de Hola de nuevo, ofrece opciones para el mantenimiento.

Puede encontrar el Asistente para la instalación de hello en el menú de inicio de hello denominado **Azure AD Connect**.

![Menú Inicio](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

Cuando se inicia el Asistente para la instalación de hello, verá una página con estas opciones:

![Página con una lista de tareas adicionales](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

Si ha instalado ADFS con Azure AD Connect podrá ver incluso más opciones. Hola opciones adicionales que tenga por AD FS se documentan en [administración de ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).

Seleccione una de las tareas de Hola y haga clic en **siguiente** toocontinue.

> [!IMPORTANT]
> Mientras tiene abierto el Asistente para la instalación de hello, se suspenden todas las operaciones de motor de sincronización de Hola. Asegúrese de que cerrar el Asistente para la instalación de hello tan pronto como haya completado sus cambios de configuración.
>
>

## <a name="view-current-configuration"></a>Visualización de la configuración actual.
Esta opción le proporciona una vista rápida de las opciones configuradas en ese momento.

![Página con una lista de todas las opciones y su estado](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

Haga clic en **anterior** toogo back. Si selecciona **Exit**, cierre el Asistente para la instalación de Hola.

## <a name="customize-synchronization-options"></a>Personalización de las opciones de sincronización
Esta opción es la configuración de sincronización de toohello de cambios de toomake usado. Vea un subconjunto de opciones de ruta de acceso de instalación de configuración personalizada de Hola. Incluso si ha utilizado la instalación rápida inicialmente verá estas opciones.

* [Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories)(Agregar más directorios). Para quitar un directorio, consulte la sección sobre cómo [eliminar un conector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).
* [Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)(Cambiar filtrado por dominio y unidad organizativa).
* Remove Group filtering (Quitar filtrado de grupo).
* [Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features)(Cambiar las características opcionales).

Hola otras opciones de instalación inicial de hello no se puede cambiar y no están disponibles. Estas opciones son:

* Cambiar Hola atributo toouse para userPrincipalName y sourceAnchor.
* Cambiar Hola unir método para los objetos de otro bosque.
* Habilitación del filtrado basado en grupo.

## <a name="refresh-directory-schema"></a>Actualización del esquema de directorio
Esta opción se utiliza si ha cambiado el esquema de hello en uno de sus instalaciones en bosques de AD DS. Por ejemplo, puede que haya instalado Exchange o actualizar el esquema de tooa Windows Server 2012 con objetos de dispositivo. En este caso, se necesita tooinstruct Azure AD Connect tooread Hola esquema nuevo de AD DS y actualizar su caché. Esta acción también vuelve a generar reglas de sincronización de Hola. Si agrega el esquema de Exchange de hello, como ejemplo, reglas de sincronización de hello para el intercambio se agregan toohello configuración.

Cuando se selecciona esta opción, se muestran todos los directorios de hello en la configuración. Puede conservar la configuración predeterminada de Hola y actualizar todos los bosques o anule la selección de algunas de ellas.

![Página con una lista de todos los directorios en el entorno de Hola](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a>Configurar modo de almacenamiento provisional
Esta opción permite tooenable y deshabilitar el modo de almacenamiento provisional en el servidor de Hola. Puede encontrar más información acerca del modo de almacenamiento provisional y cómo se utiliza en [Sincronización de Azure AD Connect: tareas y consideraciones operativas](active-directory-aadconnectsync-operations.md#staging-mode).

opción de Hello muestra si almacenamiento provisional está habilitado o deshabilitado:  
![Opción que también se muestra el estado actual de Hola de modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

toochange Hola estado, seleccione esta opción y la casilla de verificación de hello seleccione o anule la selección.  
![Opción que también se muestra el estado actual de Hola de modo de almacenamiento provisional](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a>Cambiar inicio de sesión de usuario
Esta opción permite toochange de toofederation de sincronización de contraseña o hello revés. No se puede cambiar demasiado**no configure**.

Para más información sobre esta opción, consulte [Opciones para el inicio de sesión de los usuarios en Azure AD Connect](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).

## <a name="next-steps"></a>Pasos siguientes
* Obtener más información sobre el modelo de configuración de hello utilizado por la sincronización de Azure AD Connect en [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).

**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
