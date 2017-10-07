---
title: aaaSetting el acceso condicional local mediante el registro de dispositivos de Azure Active Directory | Documentos de Microsoft
description: "Una guía paso a paso tooenabling acceso condicional local tooon las aplicaciones mediante el uso de los servicios de federación de Active Directory (AD FS) en Windows Server 2012 R2."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6ae9df8b-31fe-4d72-9181-cf50cfebbf05
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 808e3b96873102aebae667153f588dcdb205e884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-on-premises-conditional-access-by-using-azure-active-directory-device-registration"></a>Configuración del acceso condicional local mediante el registro de dispositivos de Azure Active Directory
Cuando necesite usuarios tooworkplace-recombinar su servicio de registro de dispositivo de Azure Active Directory (Azure AD) toohello de dispositivos personales, sus dispositivos se pueden marcar como organización tooyour conocidos. Aquí te mostramos una guía paso a paso para permitir que las aplicaciones de acceso condicional tooon local mediante el uso de los servicios de federación de Active Directory (AD FS) en Windows Server 2012 R2.

> [!NOTE]
> Se requiere una licencia de Azure AD Premium o de Office 365 al usar dispositivos que están registrados en directivas de acceso condicional del servicio de registros de dispositivos de Azure Active Directory. Estas incluyen directivas que AD FS aplica en recursos locales.
> 
> Para obtener más información sobre los escenarios de acceso condicional de Hola de recursos locales, consulte [unirse tooworkplace desde cualquier dispositivo para SSO y autenticación de segundo factor sin problemas en todas las aplicaciones de empresa](https://technet.microsoft.com/library/dn280945.aspx).

Estas capacidades están disponibles toocustomers que adquirir una licencia de Azure Active Directory Premium.

## <a name="supported-devices"></a>Dispositivos compatibles
* Dispositivos Windows 7 unidos a un dominio
* Dispositivos Windows 8.1 personales y unidos a un dominio
* iOS 6 y versiones posteriores del explorador Safari Hola
* Android 4.0 o versiones posteriores, teléfonos Samsung GS3 o versiones posteriores, tabletas Samsung Galaxy Note 2 o versiones posteriores

## <a name="scenario-prerequisites"></a>Requisitos previos de escenario
* Suscripción tooOffice 365 o Azure Active Directory Premium
* Un inquilino de Azure Active Directory
* Windows Server Active Directory (Windows Server 2008 o versiones posteriores)
* Esquema actualizado en Windows Server 2012 R2
* Licencia de Azure Active Directory Premium
* Windows Server 2012 R2 servicios de federación, configurados para SSO tooAzure AD
* Proxy de aplicación web de Windows Server 2012 R2 
* Microsoft Azure Active Directory Connect (Azure AD Connect) [(descargue Azure AD Connect)](http://www.microsoft.com/en-us/download/details.aspx?id=47594)
* Dominio comprobado

## <a name="known-issues-in-this-release"></a>Problemas conocidos en esta versión
* Directivas de acceso condicional basado en dispositivos requieren tooActive de reescritura de dispositivos objeto Directory de Azure Active Directory. Pueden tardar horas toothree toobe de objetos de dispositivo reescrito tooActive Directory.
* dispositivos con iOS 7 siempre le preguntará Hola usuario tooselect un certificado durante la autenticación de certificado de cliente.
* Algunas versiones de iOS 8 anteriores a iOS 8.3 no funcionan.

## <a name="scenario-assumptions"></a>Escenarios hipotéticos
En este escenario se asume que tiene un entorno híbrido que consta de un inquilino de Azure AD y una versión local de Active Directory. Estos inquilinos deben conectarse mediante Azure AD Connect, con un dominio comprobado, y con AD FS para SSO. Usar hello después de configurar su entorno según los requisitos de toohello de toohelp de lista de comprobación.

## <a name="checklist-prerequisites-for-conditional-access-scenario"></a>Lista de comprobación: requisitos previos para un escenario de acceso condicional
Conecte su inquilino de Azure AD a la instancia local de Active Directory.

## <a name="configure-azure-active-directory-device-registration-service"></a>Configuración del servicio de registro de dispositivos de Azure Active Directory
Use esta guía toodeploy y configurar el servicio de registro de dispositivos de hello Azure Active Directory para su organización.

Esta guía se da por supuesto que ha configurado Active Directory de Windows Server y ha suscrito tooMicrosoft Azure Active Directory. Consulte los requisitos previos de Hola que se ha descrito anteriormente.

Hola toodeploy servicio de registro de dispositivos de Azure Active Directory con Azure Active Directory de inquilinos, tareas de hello completa en hello después de la lista de comprobación en orden. Cuando un vínculo de referencia le lleve tooa de tema conceptual, devolver lista de comprobación de toothis posteriormente, para que puedas seguir con las tareas restantes de hello. Algunas tareas incluyen un paso de validación de escenario que te ayudará a confirmar si el paso de Hola se completó correctamente.

## <a name="part-1-enable-azure-active-directory-device-registration"></a>Paso 1: habilitación del registro de dispositivos de Azure Active Directory
Siga los pasos de hello en tooenable de lista de comprobación de Hola y configurar el servicio de registro de dispositivos de hello Azure Active Directory.

| Tarea | Referencia | 
| --- | --- |
| Habilite el registro de dispositivo en su Azure Active Directory inquilino tooallow dispositivos toojoin Hola al área de trabajo. De forma predeterminada, la autenticación multifactor Azure no está habilitada para el servicio de Hola. Sin embargo, se recomienda que lo uso cuando registre un dispositivo. Antes de habilitar Multi-Factor Authentication en el servicio de registro de Active Directory, asegúrese de que AD FS está configurado para un proveedor de Multi-Factor Authentication. |[Habilitación del registro de dispositivos de Azure Active Directory](active-directory-device-registration-get-started.md)| 
|Los dispositivos detectan el servicio de registro de dispositivos de Azure Active Directory buscando registros DNS conocidos. Configure el DNS de la empresa para que los dispositivos puedan detectar el servicio de registro de dispositivos de Azure Active Directory. |[Configuración de la detección del registro de dispositivos de Azure Active Directory](active-directory-device-registration-get-started.md)| 


## <a name="part-2-deploy-and-configure-windows-server-2012-r2-active-directory-federation-services-and-set-up-a-federation-relationship-with-azure-ad"></a>Parte 2: implementación de Servicios de federación de Active Directory Windows Server 2012 R2 y configuración de una relación de federación con Azure AD.

| Tarea | Referencia |
| --- | --- |
| Implementar los servicios de dominio de Active Directory con extensiones de esquema de Windows Server 2012 R2 Hola. No es necesario tooupgrade cualquiera de sus tooWindows de controladores de dominio Server 2012 R2. actualización del esquema de Hello es el único requisito de Hola. |[Actualización del esquema de Active Directory Domain Services](#upgrade-your-active-directory-domain-services-schema) |
| Los dispositivos detectan el servicio de registro de dispositivos de Azure Active Directory buscando registros DNS conocidos. Configure el DNS de la empresa para que los dispositivos puedan detectar el servicio de registro de dispositivos de Azure Active Directory. |[Preparación de los dispositivos para la compatibilidad con Active Directory](#prepare-your-active-directory-to-support-devices) |

## <a name="part-3-enable-device-writeback-in-azure-ad"></a>Parte 3: habilitación de reescritura de dispositivos en Azure AD
| Tarea | Referencia |
| --- | --- |
| Complete la parte 2 de "Habilitación de escritura diferida de dispositivos en Azure AD Connect". Cuando termine de él, Guía de toothis devuelto. |[Habilitación de escritura diferida de dispositivos en Azure AD Connect](#upgrade-your-active-directory-domain-services-schema) |

## <a name="optional-part-4-enable-multi-factor-authentication"></a>[Opcional] Parte 4: habilitación de Multi-Factor Authentication
Se recomienda encarecidamente que deberá configurar uno de hello varias opciones para la autenticación multifactor. Si desea que toorequire la autenticación multifactor, consulte [elegir la solución de seguridad de la autenticación multifactor de hello automáticamente](../multi-factor-authentication/multi-factor-authentication-get-started.md). Se incluye una descripción de cada solución y vincula toohelp configurar solución Hola de su elección.

## <a name="part-5-verification"></a>Parte 5: verificación
implementación de Hello ahora se ha completado y puede probar algunos escenarios. Usar hello siguiente vincula tooexperiment con el servicio de Hola y se familiarice con sus características.

| Tarea | Referencia |
| --- | --- |
| Unirse al área de trabajo de algunos tooyour de dispositivos mediante el servicio de registro de dispositivo de Azure Active Directory. Puede conectar dispositivos iOS, Windows y Android. |[Unirse al área de trabajo tooyour de dispositivos con el servicio de registro de dispositivos de Azure Active Directory](#join-devices-to-your-workplace-using-azure-active-directory-device-registration) |
| Ver y habilitar o deshabilitar dispositivos registrados mediante el portal de administración de Hola. En esta tarea, verá algunos dispositivos registrados mediante el uso de portal de administración de Hola. |[Introducción al servicio de registro de dispositivos de Azure Active Directory](active-directory-device-registration-get-started.md) |
| Compruebe que los objetos de dispositivo se reescriben desde Azure Active Directory tooWindows Server Active Directory. |[Comprobar dispositivos registrados se reescriben tooActive Directory](#verify-registered-devices-are-written-back-to-active-directory) |
| Ahora que los usuarios pueden registrar sus dispositivos, puede crear en AD FS directivas de acceso a la aplicación que solo permitan dispositivos registrados. En esta tarea, creará una regla de acceso a la aplicación y un mensaje de acceso denegado personalizado. |[Creación de una directiva de acceso a aplicaciones y un mensaje personalizado de acceso denegado](#create-an-application-access-policy-and-custom-access-denied-message) |

## <a name="integrate-azure-active-directory-with-on-premises-active-directory"></a>Integración de Azure Active Directory con una versión local de Active Directory
Este paso le ayuda a integrar el inquilino de Azure AD con la instancia local de Active Directory mediante Azure AD Connect. Aunque los pasos de hello están disponibles en hello portal de Azure clásico, tome nota de las instrucciones especiales que se enumeran en esta sección.

1. Inicie sesión en toohello portal de Azure clásico mediante una cuenta que sea un administrador global de Azure AD.
2. En el panel izquierdo de hello, seleccione **Active Directory**.
3. En hello **Directory** ficha, seleccione el directorio.
4. Seleccione hello **integración de directorios** ficha.
5. En hello **implementar y administrar** sección, siga los pasos del 1 al 3 toointegrate Azure Active Directory con su directorio local.
   
   1. Adición de dominios.
   2. Instalar y ejecutar Azure AD Connect con instrucciones de hello en [instalación personalizada de Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).
   3. Comprobación y administración de la sincronización de directorios. Las instrucciones de inicio de sesión único están disponibles en este paso.
   
   Además, configure la federación con AD FS tal como se describe en [Instalación personalizada de Azure AD Connect](connect/active-directory-aadconnect-get-started-custom.md).

## <a name="upgrade-your-active-directory-domain-services-schema"></a>Actualización del esquema de Servicios de dominio de Active Directory
> [!NOTE]
> Después de actualizar el esquema de Active Directory, no se puede revertir el proceso de Hola. Se recomienda realizar primero la actualización hello en un entorno de prueba.
> 

1. Inicie sesión en el controlador de dominio de tooyour con una cuenta que tiene derechos de administrador de esquema y Administrador de organización.
2. Hola copia **[media] \support\adprep** tooone de directorio y subdirectorios de los controladores de dominio de Active Directory (donde **[media]** es el medio de instalación de Windows Server 2012 R2 de hello ruta de acceso toohello ).
4. Desde un símbolo del sistema, vaya toohello **adprep** directorio y ejecución **adprep.exe /forestprep**. Siga la actualización del esquema de hello instrucciones en pantalla toocomplete Hola.

## <a name="prepare-your-active-directory-toosupport-devices"></a>Preparar los dispositivos de toosupport de Active Directory
> [!NOTE]
> Se trata de una operación única que debe ejecutar tooprepare los dispositivos de toosupport de bosque de Active Directory. toocomplete este procedimiento, debe haber iniciado sesión con permisos de administrador de empresa y el bosque de Active Directory debe tener esquema de Windows Server 2012 R2 Hola.
> 


### <a name="prepare-your-active-directory-forest"></a>Preparación del bosque de Active Directory
1. En el servidor de federación, abra una ventana Comandos de Windows PowerShell y escriba **Initialize-ADDeviceRegistration**. 
2. Cuando se le solicite **ServiceAccountName**, escriba Hola nombre de cuenta de servicio de Hola que seleccionó como cuenta de servicio de Hola para AD FS. Si es una cuenta de gMSA, escriba la cuenta de hello en hello **dominio\nombreDeCuenta$** formato. Para una cuenta de dominio, use el formato de hello **dominio\nombreDeCuenta**.

### <a name="enable-device-authentication-in-ad-fs"></a>Habilitación de la autenticación del dispositivo en AD FS
1. En el servidor de federación, abra la consola de administración de AD FS de Hola y vaya demasiado**AD FS** > **las directivas de autenticación**.
2. En hello **acciones** panel, seleccione **Editar autenticación principal Global**.
3. Active **Habilitar autenticación de dispositivo** y, luego, seleccione **Aceptar**.
4. De manera predeterminada, AD FS quitará periódicamente los dispositivos no usados de Active Directory. Deshabilite esta tarea cuando use el servicio de registro de dispositivos de Azure Active Directory para que los dispositivos se puedan administrar en Azure.

### <a name="disable-unused-device-cleanup"></a>Deshabilitación de la limpieza de dispositivos no usados
En el servidor de federación, abra una ventana Comandos de Windows PowerShell y, luego, escriba **Set-AdfsDeviceRegistration -MaximumInactiveDays 0**.

### <a name="prepare-azure-ad-connect-for-device-writeback"></a>Preparación de Azure AD Connect para la reescritura de dispositivos
Complete la parte 1: preparación de Azure AD Connect.

## <a name="join-devices-tooyour-workplace-by-using-azure-active-directory-device-registration-service"></a>Unirse al área de trabajo tooyour de dispositivos mediante el servicio de registro de dispositivo de Azure Active Directory

### <a name="join-an-ios-device-by-using-azure-active-directory-device-registration"></a>Unión de un dispositivo iOS mediante el registro de dispositivos de Azure Active Directory
Registro de dispositivos de Azure Active Directory usa el proceso de inscripción de perfil por aire Hola para dispositivos iOS. Este proceso comienza cuando el usuario de Hola conecta URL de inscripción de perfil toohello con Safari. formato de dirección URL de Hello es como sigue:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/"yourdomainname"

En este caso, `yourdomainname` es nombre de dominio de Hola que ha configurado con Azure Active Directory. Por ejemplo, si el nombre de dominio es contoso.com, dirección URL de hello es:

    https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com

Hay toocommunicate de muchas maneras diferentes de los usuarios de este tooyour de dirección URL. Por ejemplo, un método que se recomienda es publicar esta dirección URL en un mensaje de acceso denegado a la aplicación personalizado en AD FS. Esta información se trata en la siguiente sección de hello [crear una directiva de acceso de la aplicación y el mensaje acceso denegado personalizado](#create-an-application-access-policy-and-custom-access-denied-message).

### <a name="join-a-windows-81-device-by-using-azure-active-directory-device-registration"></a>Unión de un dispositivo Windows 8.1 mediante el registro de dispositivos de Azure Active Directory
1. En el dispositivo Windows 8.1, seleccione **Configuración de PC** > **Red** > **Área de trabajo**.
2. Escriba el nombre de usuario en formato UPN, por ejemplo, **dan@contoso.com**.
3. Seleccione **Combinar**.
4. Cuando se lo pidan, inicie sesión con sus credenciales. Ahora se une el dispositivo de Hola.

### <a name="join-a-windows-7-device-by-using-azure-active-directory-device-registration"></a>Unión de un dispositivo Windows 7 mediante el registro de dispositivos de Azure Active Directory
tooregister Windows 7 dispositivos Unidos a dominio, debe paquete de software de registro de dispositivos de toodeploy Hola. Hello paquete de software se denomina Workplace Join for Windows 7 y sus disponible para su descarga en hello [sitio Web de Microsoft Connect](https://connect.microsoft.com/site1164). 

Las instrucciones sobre cómo toouse Hola paquete están disponibles en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).

## <a name="verify-that-registered-devices-are-written-back-tooactive-directory"></a>Compruebe que los dispositivos registrados se reescriben tooActive Directory
Puede ver y comprobar que los objetos de dispositivo se ha reescrito tooyour Active Directory con LDP.exe o ADSI Edit. Ambos están disponibles con las herramientas de administrador de Active Directory de Hola.

De forma predeterminada, los objetos de dispositivo que se reescriben desde Azure Active Directory se colocan en hello mismo dominio que la granja de servidores de AD FS.

    CN=RegisteredDevices,defaultNamingContext

## <a name="create-an-application-access-policy-and-custom-access-denied-message"></a>Creación de una directiva de acceso a aplicaciones y un mensaje personalizado de acceso denegado
Considere la posibilidad de hello siguiendo escenario: crear una aplicación de confianza para usuario autenticado en AD FS y configurar una regla de autorización de emisión que permita solamente dispositivos registrados. Ahora sólo los dispositivos que están registrados se permiten aplicaciones de hello tooaccess. 

toomake más sencilla para la aplicación de toohello de acceso de los usuarios toogain, configurará un mensaje personalizado al acceso denegado que se incluye instrucciones sobre cómo toojoin su dispositivo. Ahora los usuarios tienen un tooregister de manera transparente sus dispositivos para que pueden acceder a una aplicación.

Hello pasos siguientes muestran cómo tooimplement este escenario.

> [!NOTE]
> En esta sección se supone que ya configuró una relación de confianza para usuario autenticado para la aplicación en AD FS.
> 

1. Abra Hola herramienta MMC de AD FS y, a continuación, seleccione **AD FS** > **relaciones de confianza** > **Veracidades**.
2. Busque toowhich de aplicación Hola que se aplica esta regla de acceso nuevo. Haga clic en aplicación hello y, a continuación, seleccione **editar reglas de notificación**.
3. Seleccione hello **las reglas de autorización de emisión** pestaña y, a continuación, seleccione **Agregar regla**.
4. De hello **regla de notificación** lista desplegable de plantillas, seleccione **permitir o denegar a los usuarios según una notificación entrante**. Luego, seleccione **Siguiente**.
5. Hola **nombre de la regla de notificación** , escriba **permitir el acceso desde dispositivos registrados**.
6. De hello **tipo de notificación entrante** lista desplegable, seleccione **Is Registered User**.
7. Hola **valor de notificación entrante** , escriba **true**.
8. Seleccione hello **toousers de permiso de acceso con esta notificación entrante** botón de radio.
9. Seleccione **Finalizar** y, luego, **Aplicar**.
10. Quite las reglas que sean más permisivas que la regla de Hola que ha creado. Por ejemplo, quitar la regla predeterminada de hello **tooall de permitir el acceso a los usuarios**.

La aplicación está ahora configurado tooallow acceso solo cuando el usuario de hello procede de un dispositivo que registró y unió al área de trabajo toohello. Para ver directivas de acceso más avanzadas, consulte [Administrar el riesgo con la autenticación multifactor adicional para aplicaciones con información confidencial](https://technet.microsoft.com/library/dn280949.aspx).

A continuación, se configura un mensaje de error personalizado para la aplicación. mensaje de error de Hello permite a los usuarios saber que debe unirse al área de trabajo de su toohello de dispositivo antes de que puede tener acceso a la aplicación hello. Puede usar PowerShell y HTML personalizado para crear un mensaje personalizado de acceso denegado a la aplicación.

En el servidor de federación, abra una ventana de comandos de PowerShell y, a continuación, escriba el siguiente comando de Hola. Reemplazar partes del comando hello con elementos que el sistema tooyour específica:

    Set-AdfsRelyingPartyWebContent -Name "relying party trust name" -ErrorPageAuthorizationErrorMessage
Para poder acceder a esta aplicación, debe registrar el dispositivo.

**Si está utilizando un dispositivo iOS, seleccione este vínculo toojoin su dispositivo**:

    a href='https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/yourdomain.com

Únase a esta área de trabajo de tooyour de dispositivo de iOS.

Si usa un dispositivo Windows 8.1, puede conectarlo si selecciona **Configuración de PC**> **Red** > **Área de trabajo**.

Hola anterior comandos, **nombre de confianza de relación de confianza** es Hola nombre del objeto de relación de confianza de la aplicación en AD FS.
Y **dominio.com** es nombre de dominio de Hola que ha configurado con Azure Active Directory (por ejemplo, contoso.com).
Ser tooremove seguro de que los saltos de línea (si existe) de hello HTML contenido que pasar toohello **Set-AdfsRelyingPartyWebContent** cmdlet.

Ahora cuando los usuarios tener acceso a la aplicación desde un dispositivo que no está registrado con el servicio de registro de dispositivos de Azure Active Directory de hello, verán una página que busca la siguiente captura de pantalla de toohello similar.

![Captura de pantalla de un error cuando los usuarios no han registrado su dispositivo con Azure AD](./media/active-directory-conditional-access/error-azureDRS-device-not-registered.gif)


