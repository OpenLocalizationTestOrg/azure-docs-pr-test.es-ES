---
title: "Azure AD Connect : habilitación de reescritura de dispositivos | Microsoft Azure"
description: "Este documento detalles cómo tooenable reescritura de dispositivos mediante Azure AD Connect"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c0ff679c-7ed5-4d6e-ac6c-b2b6392e7892
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 2566a514137fed85b21929207cf3230e6878ebbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-enabling-device-writeback"></a>Azure AD Connect: Habilitación de escritura diferida de dispositivos
> [!NOTE]
> Un tooAzure de suscripción AD Premium es necesario para la reescritura de dispositivos.
> 
> 

Hola siguiendo documentación proporciona información sobre cómo la característica tooenable Hola reescritura en dispositivos en Azure AD Connect. Reescritura de dispositivos se usa en hello los escenarios siguientes:

* Habilitar el acceso condicional basado en dispositivos tooADFS (2012 R2 o posterior) protegido de aplicaciones (usuario autenticado).

Esto proporciona seguridad adicional y garantía de que tienen acceso a tooapplications se le concede tootrusted solo los dispositivos. Para más información sobre el acceso condicional, consulte [Administración de riesgos con el acceso condicional](../active-directory-conditional-access.md) y [Configuración del acceso condicional local mediante el Registro de dispositivos de Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

> [!IMPORTANT]
> <li>Dispositivos deben estar ubicados en hello como usuarios de Hola del mismo bosque. Puesto que los dispositivos deben volver a escribir tooa solo bosque, esta característica no admite actualmente una implementación con varios bosques de usuarios.</li>
> <li>Objeto de configuración de registro de un solo dispositivo se puede agregar bosque de Active Directory local toohello. Esta característica no es compatible con una topología donde hello local Active Directory no se directorios sincronizados toomultiple Azure AD.</li>> 

## <a name="part-1-install-azure-ad-connect"></a>Parte 1: Instalación de Azure AD Connect
1. Instale Azure AD Connect mediante la configuración rápida o personalizada. Microsoft recomienda toostart con todos los usuarios y grupos se sincronizaron correctamente antes de habilitar la reescritura de dispositivos.

## <a name="part-2-prepare-active-directory"></a>Parte 2: Preparación de Active Directory
Usar hello siguiendo los pasos tooprepare para el uso de reescritura de dispositivos.

1. Desde el equipo de Hola donde está instalado Azure AD Connect, inicie PowerShell en modo elevado.
2. Si no está instalado el módulo de Active Directory PowerShell hello, instalarlo mediante Hola siguiente comando:
   
   `Add-WindowsFeature RSAT-AD-PowerShell`
3. Si no está instalado el módulo de PowerShell de Azure Active Directory de hello, a continuación, descargar e instalar desde [Azure módulo Active Directory para Windows PowerShell (versión de 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297). Este componente tiene una dependencia en hello Asistente para iniciar sesión, que se instala con Azure AD Connect.
4. Con credenciales de administrador de organización, ejecute hello siga los comandos y, a continuación, salga de PowerShell.
   
   `Import-Module 'C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1'`
   
   `Initialize-ADSyncDeviceWriteback {Optional:–DomainName [name] Optional:-AdConnectorAccount [account]}`

Dado que no se necesita espacio de nombres de configuración de toohello de cambios, se necesitan credenciales de administrador de Enterprise. Un administrador de dominio no tiene suficientes permisos.

![Powershell para habilitar la escritura diferida de dispositivos](./media/active-directory-aadconnect-feature-device-writeback/powershell.png)

Description:

* Si todavía no existen, se crean y configuran nuevos contenedores y objetos en CN=Device Registration Configuration,CN=Services,CN=Configuration,[forest-dn].
* Si todavía no existen, se crean y se configuran nuevos contenedores y objetos en CN=RegisteredDevices,[domain-dn]. Los objetos de dispositivo se crearán en este contenedor.
* Establece permisos necesarios en hello cuenta de conector de Azure AD, toomanage dispositivos en su Active Directory.
* Solo necesita toorun en un bosque, incluso si se instala Azure AD Connect en varios bosques.

Parámetros:

* DomainName: dominio de Active Directory donde se crearán los objetos de dispositivo. Nota: todos los dispositivos para un bosque de Active Directory determinado se creará en un dominio único.
* AdConnectorAccount: Cuenta de Active Directory que se usará en Azure AD Connect toomanage objetos en el directorio de Hola. Se trata de una cuenta de hello usada por Azure AD Connect sync tooconnect tooAD. Si ha instalado mediante la configuración rápida, se trata de cuenta de hello MSOL_ el prefijo.

## <a name="part-3-enable-device-writeback-in-azure-ad-connect"></a>Parte 3: Habilitación de la reescritura de dispositivos en Azure AD Connect
Usar hello siguiendo el procedimiento tooenable reescritura de dispositivos en Azure AD Connect.

1. Vuelva a ejecutar el Asistente para la instalación de Hola. Seleccione **personalizar las opciones de sincronización** de tareas adicionales de hello página y haga clic en **siguiente**.
   ![Instalación personalizada de las opciones de sincronización](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback2.png)
2. En la página de características opcionales de hello, reescritura de dispositivos, ya no aparecerá deshabilitada. Tenga en cuenta que si hello no se completan los pasos de preparación de Azure AD Connect reescritura de dispositivos se atenuará alejar en la página de características opcionales de Hola. Casilla de Hola para reescritura de dispositivos y haga clic en **siguiente**. Si todavía está deshabilitado casilla hello, vea hello [sección de solución de problemas](#the-writeback-checkbox-is-still-disabled).
   ![Instalación personalizada de características opcionales de escritura diferida de dispositivos](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback3.png)
3. En la página de la escritura diferida de hello, verá dominio Hola proporcionado como bosque de reescritura de dispositivos de hello predeterminado.
   ![Instalación personalizada del bosque de destino de escritura diferida de dispositivos](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback4.png)
4. Completar la instalación de Hola de hello asistente sin realizar ningún cambio de configuración adicional. Si es necesario, consulte demasiado[instalación personalizada de Azure AD Connect.](active-directory-aadconnect-get-started-custom.md)

## <a name="enable-conditional-access"></a>Habilitar el acceso condicional
Tooenable instrucciones detalladas están disponibles en este escenario [configuración del acceso condicional local mediante el registro del dispositivo de Azure Active Directory](../active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-devices-are-synchronized-tooactive-directory"></a>Comprobar que dispositivos están sincronizado tooActive Directory
La reescritura de dispositivos debería funcionar ahora correctamente. Tenga en cuenta que puede tardar horas too3 para dispositivo objetos toobe reescritos tooAD.  Hola tooverify que los dispositivos que se están sincronizados correctamente, siga después de completar reglas de sincronización de hello:

1. Inicie el Centro de administración de Active Directory.
2. Expanda RegisteredDevices, dentro de hello dominio que se está federado.
   ![Dispositivos registrados del centro de administración de Active Directory](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback5.png)
3. Los dispositivos registrados actuales aparecerá en la lista.
   ![Lista de dispositivos registrados del centro de administración de Active Directory](./media/active-directory-aadconnect-feature-device-writeback/devicewriteback6.png)

## <a name="troubleshooting"></a>Solución de problemas
### <a name="hello-writeback-checkbox-is-still-disabled"></a>casilla de reescritura de Hello todavía está deshabilitada
Si la casilla de verificación de Hola para reescritura de dispositivos no está habilitado incluso si ha seguido los pasos de hello anteriores, Hola pasos le guiará a través de la instalación de hello asistente consiste en comprobar antes de habilita el cuadro de Hola.

En primer lugar:

* Asegúrese de que al menos un bosque tenga Windows Server 2012 R2. tipo de objeto de dispositivo de Hello debe estar presente.
* Si ya está ejecutando el Asistente para la instalación de hello, no se detectarán los cambios. En este caso, complete el Asistente para la instalación de Hola y vuelva a ejecutarlo.
* Asegúrese de que cuenta de hello que proporcione en el script de inicialización de hello es realmente Hola usuario correctos utilizando Hola conector de Active Directory. tooverify, siga estos pasos:
  * En el menú de inicio de hello, abra **servicio de sincronización**.
  * Abra hello **conectores** ficha.
  * Buscar Hola conector con el tipo de los servicios de dominio de Active Directory y selecciónelo.
  * En **Acciones**, seleccione **Propiedades**.
  * Vaya demasiado**conectar tooActive Directory bosque**. Compruebe que Hola dominio y nombre de usuario especificado en esta secuencia de comandos de toohello de pantalla coincidencia Hola cuenta proporcionada.
    ![Cuenta de conector en Sync Service Manager](./media/active-directory-aadconnect-feature-device-writeback/connectoraccount.png)

Compruebe la configuración en Active Directory:

* Compruebe que Hola Device Registration Service se encuentra en la siguiente ubicación de hello (CN = DeviceRegistrationService, CN = Servicios de registro de dispositivos, CN = Configuración de registro de dispositivos, CN = Services, CN = Configuration) en el contexto de nomenclatura de configuración.

![Solución de problemas, DeviceRegistrationService en el espacio de nombres de configuración](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot1.png)

* Compruebe que hay solo un objeto de configuración mediante la búsqueda de espacio de nombres de configuración de Hola. Si hay más de uno, elimine Hola duplicado.

![Solucionar problemas, busque objetos duplicados Hola](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot2.png)

* En el objeto de servicio de registro de hello, asegúrese de que Hola atributo msDS-DeviceLocation está presente y tiene un valor. Búsqueda de esta ubicación y asegúrese de que está presente con hello objectType msDS-DeviceContainer.

![Solución de problemas, msDS-DeviceLocation](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot3.png)

![Solución de problemas, clase de objeto RegisteredDevices](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot4.png)

* Comprobar cuenta hello usa Hola que conector de Active Directory tiene los permisos necesarios en contenedor de los dispositivos registrados Hola encontrado por el paso anterior de Hola. Se trata de permisos de hello esperada en este contenedor:

![Solución de problemas, comprobar los permisos en el contenedor](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot5.png)

* Compruebe Hola cuenta de Active Directory tiene permisos en hello CN = Configuración de registro de dispositivos, CN = Services, CN = objeto de configuración.

![Solución de problemas, comprobar los permisos en la configuración del registro de dispositivos](./media/active-directory-aadconnect-feature-device-writeback/troubleshoot6.png)

## <a name="additional-information"></a>Información adicional
* [Administración de riesgos con el acceso condicional](../active-directory-conditional-access.md)
* [Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory](../active-directory-device-registration-on-premises-setup.md)

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

