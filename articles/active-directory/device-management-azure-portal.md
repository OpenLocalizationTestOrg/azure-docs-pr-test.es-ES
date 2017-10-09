---
title: dispositivos de aaaManaging mediante Hola portal de Azure - vista previa | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse Hola dispositivos toomanage de portal de Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>Administrar los dispositivos con Hola portal de Azure: obtener una vista previa

>[!NOTE]
>Esta funcionalidad se encuentra actualmente en versión preliminar pública. Prepararán toorevert o quitar los cambios. Hola característica está disponible en ninguna suscripción de Azure Active Directory (Azure AD) durante la vista previa pública. Sin embargo, cuando característica Hola deja de estar disponible con carácter general, algunos aspectos de la característica de hello pueden requerir una suscripción premium a Azure Active Directory.


Con la administración de dispositivos en Azure Active Directory (Azure AD), puede asegurarse de que los usuarios tienen acceso a los recursos desde dispositivos que cumplen los estándares de seguridad y cumplimiento. 

En este tema:

- Se da por supuesto que está familiarizado con hello [administración toodevice de introducción en Azure Active Directory](device-management-introduction.md)

- Proporciona información acerca de cómo administrar los dispositivos con Hola portal de Azure


dispositivos de toomanage Hola portal de Azure, necesita tooclick **dispositivos** en hello **administrar** sección de Hola Hola **Azure Active Directory** hoja.

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Configuración de dispositivo

toomanage los dispositivos con hello portal de Azure, que necesitan toobe registrado o Unidos tooAzure AD. Como administrador, puede ajustar el proceso de Hola de registrar y al unir dispositivos al establecer la configuración de dispositivo de Hola.

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/22.png)


hoja de configuración de dispositivo de Hello permite tooconfigure:

- **Los usuarios pueden inscribir dispositivos tooAzure AD** : esta configuración permite a los usuarios de tooselect Hola que se pueden unir dispositivos tooAzure AD. valor predeterminado de Hello es **todos los**.

- **Dispositivos Unidos a los administradores locales adicionales de Azure AD** -puede seleccionar los usuarios de Hola que tienen derechos de administrador local en un dispositivo. Los usuarios agregados aquí se agregan toohello *administradores de dispositivos* rol en Azure AD. De forma predeterminada, a los administradores globales de Azure AD y a los propietarios de dispositivos se les conceden derechos de administrador local. Esta opción es una capacidad de edición premium disponible a través de productos como Azure AD Premium o hello Enterprise Mobility Suite (EMS). 

- **Los usuarios pueden registrar sus dispositivos con Azure AD** -necesita tooconfigure esta toobe de dispositivos de tooallow de configuración registrada con Azure AD. Si selecciona **ninguno**, no se admiten los dispositivos tooregister cuando no estén Unido de Azure AD ni híbrida unido Azure AD. La inscripción en Microsoft Intune o Administración de dispositivos móviles (MDM) para Office 365 exige registrarse. Si ha configurado alguno de estos servicios, se selecciona **TODOS** y **NINGUNO** no está disponible.

- **Requiere que los dispositivos de la autenticación multifactor toojoin** -puede elegir si los usuarios son tooprovide necesaria una segunda autenticación factor toojoin su tooAzure dispositivo AD. valor predeterminado de Hello es **No**. Se recomienda exigir Multi-Factor Authentication al registrar un dispositivo. Antes de habilitar la autenticación multifactor para este servicio, debe asegurarse de que la autenticación multifactor está configurada para usuarios de Hola que registren sus dispositivos. Para más información sobre los distintos servicios de Azure Multi-Factor Authentication, vea [Introducción a Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Número máximo de dispositivos** -esta opción le permite el número máximo de hello tooselect de dispositivos que puede tener un usuario en Azure AD. Si un usuario alcanza esta cuota, que éstos no estén tooadd capaz de más dispositivos hasta que uno o varios de los dispositivos existentes Hola se quitan. oferta de dispositivo de Hola se cuenta para todos los dispositivos de Azure AD Unido o Azure AD registrado hoy en día. es el valor predeterminado de Hello **20**.

- **Los usuarios pueden sincronizar la configuración y los datos de aplicación en todos los dispositivos** : de forma predeterminada, esta opción se establece demasiado**NONE**. Selección de usuarios específicos o grupos o todos permite configuración del usuario de Hola y toosync de datos de aplicación a través de sus dispositivos Windows 10. Más información sobre cómo funciona la sincronización en Windows 10.
Esta opción es una capacidad de premium disponible a través de productos como Azure AD Premium o hello Enterprise Mobility Suite (EMS).
 
    ![Administración de un dispositivo de Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Búsqueda de dispositivos

Como administrador, Hola portal de Azure, tienes dos opciones toolocate registró y unió dispositivos:

- **Todos los dispositivos** en hello **administrar** sección de hello **dispositivos** hoja  

    ![Todos los dispositivos](./media/device-management-azure-portal/41.png)


- **Dispositivos** en hello **administrar** sección de un **usuario** hoja
 
    ![Todos los dispositivos](./media/device-management-azure-portal/43.png)



Con ambas opciones, puede obtener vista tooa:


- Le permite toosearch para dispositivos con nombre para mostrar hello como filtro.

- Proporciona información general detallada de los dispositivos registrados y unidos.

- Le permite tooperform tareas comunes de la administración de dispositivos
   

![Todos los dispositivos](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Tareas de administración de dispositivos

Como administrador, puede administrar Hola registrado o dispositivos Unidos a un. En esta sección se proporciona información sobre las tareas comunes de administración de dispositivos.


**Administrar un dispositivo de Intune**: si es administrador de Intune, puede administrar los dispositivos marcados como **Microsoft Intune**. Un administrador puede ver dispositivos adicionales 

![Administración de un dispositivo de Intune](./media/device-management-azure-portal/31.png)


**Habilitar o deshabilitar un dispositivo de Azure AD**

tooenable o deshabilitar un dispositivo, deberá toobe un administrador global en Azure AD. Al deshabilitar un dispositivo se evita que acceda a los recursos de Azure AD.  dispositivo de hello toodisable, puede hacer clic en *...* Haga clic en el dispositivo de Hola para obtener más detalles.

 
![Administración de un dispositivo de Intune](./media/device-management-azure-portal/33.png)

Al deshabilitar un dispositivo cambia el estado de Hola Hola **habilitado** columna demasiado**No**.

![Deshabilitación de un dispositivo](./media/device-management-azure-portal/32.png)


**Eliminar un dispositivo de Azure AD** -toodelete un dispositivo, deberá toobe un administrador global de Azure AD.  
La eliminación de un dispositivo:
 
- Evita que un dispositivo acceda a los recursos de Azure AD 

- Quita todos los detalles que se adjunta toohello dispositivo, por ejemplo, las claves de BitLocker para dispositivos Windows  

- Representa una actividad no recuperable y no se recomienda a menos que sea necesaria

Si un dispositivo está administrado por otra entidad de administración (por ejemplo, Microsoft Intune), asegúrese de que dicho dispositivo Hola se ha borrado / retirado antes de eliminar el dispositivo de hello en Azure AD.

Puede seleccionar "..." dispositivo de hello toodelete o haga clic en el dispositivo de Hola para obtener más detalles
 
![Eliminar un dispositivo](./media/device-management-azure-portal/34.png)


**Ver o copiar el Id. de dispositivo** : puede usar un detalles del Id. de dispositivo de dispositivo ID tooverify Hola de dispositivo de Hola o con PowerShell durante la solución de problemas. tooaccess Hola copia opción, haga clic en el dispositivo de Hola.

![Visualización de identificador de dispositivo](./media/device-management-azure-portal/35.png)
  

**Ver o copiar las claves de BitLocker** -si eres un administrador, puede ver y Hola copia BitLocker claves toohelp toorecover de los usuarios de su unidad cifrada. Estas claves solo están disponibles para dispositivos Windows cifrados y con las claves almacenadas en Azure AD. Puede copiar estas claves al tener acceso a los detalles del dispositivo de Hola.
 
![Visualización de claves de BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Registros de auditoría


Hola dispositivo actividades están disponibles a través de los registros de actividad de Hola. Esto incluye actividades desencadenadas por el servicio de registro de dispositivo de Hola o por el usuario de hello:

- Creación de dispositivos y agregar propietarios o los usuarios en el dispositivo de Hola

- Cambia la configuración de toodevice

- Operaciones de dispositivo como eliminar o actualizar un dispositivo
 
Es el toohello de punto de entrada, datos de auditoría **registros de auditoría** en hello **actividad** sección de hello **dispositivos* hoja.

![Registros de auditoría](./media/device-management-azure-portal/61.png)


Un registro de auditoría tiene una vista de lista predeterminada que muestra:

- Hola fecha y hora de aparición de Hola

- destinos de Hola

- Hola iniciador / actor (que) de una actividad

- actividad de Hello (¿qué)

![Registros de auditoría](./media/device-management-azure-portal/63.png)

Puede personalizar la vista de lista Hola haciendo clic en **columnas** en la barra de herramientas de Hola.
 
![Registros de auditoría](./media/device-management-azure-portal/64.png)


toonarrow hacia abajo Hola informó de un nivel de tooa de datos que funciona para usted, puede filtrar datos de auditoría de hello mediante Hola siguientes campos:

- Categoría
- Tipo de recurso de actividad
- Actividad
- Intervalo de fechas
- Destino
- Iniciado por (actor)

Además toohello filtros, puede buscar entradas específicas.

![Registros de auditoría](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Pasos siguientes

* [Administración de toodevice de introducción en Azure Active Directory](device-management-introduction.md)



