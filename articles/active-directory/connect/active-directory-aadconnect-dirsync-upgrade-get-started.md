---
title: "Azure AD Connect: actualización desde DirSync | Microsoft Docs"
description: "Obtenga información acerca de cómo tooupgrade desde DirSync tooAzure AD Connect. En este artículo se describen los pasos de Hola de actualización de DirSync tooAzure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: baf52da7-76a8-44c9-8e72-33245790001c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 05572af410698deaa1392c8837bfcb749efc69e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-upgrade-from-dirsync"></a>Azure AD Connect: Actualización desde DirSync
Azure AD Connect es Hola sucesor tooDirSync. Buscar formas de hello que actualizar desde DirSync en este tema. Estos pasos no funcionan para la actualización desde otra versión de Azure AD Connect ni desde Sincronización de Azure AD.

Antes de empezar a instalar Azure AD Connect, asegúrese de que demasiado[descargar Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771) y los pasos de requisitos previos de hello completa de [Azure AD Connect: Hardware y los requisitos previos](active-directory-aadconnect-prerequisites.md). En concreto, desea tooread sobre siguientes hello, ya que estas áreas son diferentes de sincronización de directorios:

* versión requerida de Hola de .net y PowerShell. Las versiones más recientes son toobe necesario en el servidor de Hola que lo que necesita sincronización de directorios.
* configuración del servidor proxy Hola. Si utiliza un tooreach de servidor proxy Hola internet, este valor debe configurarse antes de actualizar. DirSync siempre utiliza el servidor de proxy de hello configurada para el usuario de hello instalarla, pero Azure AD Connect usa la configuración del equipo en su lugar.
* Hola las direcciones URL necesaria toobe abrir en el servidor de proxy de Hola. Para los escenarios básicos, esos escenarios también compatibles con la sincronización de directorios, los requisitos de hello son Hola igual. Si desea toouse de hello características nuevas incluidas con Azure AD Connect, debe abrirse algunas nuevas direcciones URL.

> [!NOTE]
> Una vez que se ha habilitado el nuevo Azure AD Connect server toostart sincronizar cambios tooAzure AD, debe volver a la versión toousing DirSync o sincronización de Azure AD. Degradar de Azure AD Connect toolegacy clientes como DirSync y Azure AD Sync no se admite y puede provocar tooissues, como la pérdida de datos en Azure AD.

Si no va a realizar la actualización desde DirSync, consulte la [documentación relacionada](#related-documentation) sobre otros escenarios.

## <a name="upgrade-from-dirsync"></a>Actualización desde DirSync
Dependiendo de su implementación actual de la sincronización de directorios, hay diferentes opciones para la actualización de Hola. Si Hola espera el tiempo de actualización es inferior a tres horas, recomendación de hello es toodo una actualización en contexto. Si Hola espera el tiempo de actualización es de más de tres horas, recomendación de hello es toodo una implementación paralela en otro servidor. Se estima que si tiene más de 50.000 objetos tarda más de tres horas toodo Hola actualización.

| Escenario |
| --- | --- |
| [Actualización local](#in-place-upgrade) |
| [Implementación paralela](#parallel-deployment) |

> [!NOTE]
> Si prevé tooupgrade desde DirSync tooAzure AD Connect, no desinstale DirSync usted mismo antes de la actualización de Hola. Azure AD Connect leer y migrar la configuración de Hola desde DirSync y desinstalar después de inspeccionar servidor hello.

**Actualización local**  
Hola espera actualización de hello toocomplete de tiempo se muestra al Asistente de Hola. Esta estimación se basa en la suposición de Hola que toma tres horas toocomplete una actualización para una base de datos con 50.000 objetos (usuarios, contactos y grupos). Si el número de Hola de objetos de la base de datos es menor que 50.000, Azure AD Connect recomienda una actualización en contexto. Si decide toocontinue, su configuración actual se aplica automáticamente durante la actualización y el servidor reanuda automáticamente la sincronización de active.

Si desea toodo una migración de la configuración y realizar una implementación paralela, puede invalidar recomendación de actualización en contexto de Hola. Por ejemplo, podría tardar Hola oportunidad toorefresh Hola hardware y sistema operativo. Para obtener más información, vea hello [implementación en paralelo](#parallel-deployment) sección.

**Implementación paralela**  
Si tiene más de 50.000 objetos se recomienda usar una implementación paralela. Esta implementación evita que los usuarios sufran retrasos operativos. Hola instalación de Azure AD Connect intenta tiempo de inactividad de tooestimate hello para la actualización de hello, pero si ha actualizado DirSync en hello anterior, su propia experiencia es guía recomendados de toobe probable Hola.

### <a name="supported-dirsync-configurations-toobe-upgraded"></a>Compatible toobe de las configuraciones de sincronización de directorios actualizado
Hola después de los cambios de configuración es compatibles con DirSync actualizado:

* Filtrado por dominio y unidad organizativa
* Identificador alternativo (UPN)
* Sincronización de contraseñas y configuración híbrida de Exchange
* Configuración de bosque/dominio y Azure AD
* Filtrado basado en atributos de usuario

Hola siguiente cambio no se puede actualizar. Si tiene esta configuración, se bloquea la actualización hello:

* Cambios de DirSync no admitidos, como por ejemplo, los atributos eliminados y el uso de un archivo DLL de extensión personalizado

![Actualización bloqueada](./media/active-directory-aadconnect-dirsync-upgrade-get-started/analysisblocked.png)

En esos casos, recomendación de hello es tooinstall un nuevo servidor de Azure AD Connect en [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode) y compruebe Hola DirSync antigua y nueva configuración de Azure AD Connect. Vuelva a aplicar los cambios usando la configuración personalizada, como se describe en el artículo sobre la [configuración personalizada de la sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md).

las contraseñas de Hello utilizadas DirSync hello las cuentas de servicio no se puede recuperar y no se migran. Estas contraseñas se restablecen durante la actualización de Hola.

### <a name="high-level-steps-for-upgrading-from-dirsync-tooazure-ad-connect"></a>Pasos generales para actualizar desde DirSync tooAzure AD Connect
1. Página principal tooAzure AD Connect
2. Análisis de la configuración actual de DirSync
3. Recopilación de la contraseña de administrador global de Azure AD
4. Recopilar las credenciales para una cuenta de administrador de empresa (sólo se utiliza durante la instalación de Hola de Azure AD Connect)
5. Instalación de Azure AD Connect
   * Desinstalar DirSync (o deshabilitarlo temporalmente)
   * Instalación de Azure AD Connect
   * Opcionalmente, iniciar la sincronización

Se requieren pasos adicionales cuando:

* Actualmente usa una instalación completa de SQL Server (local o remota)
* Tiene más de 50.000 objetos en el ámbito para sincronización

## <a name="in-place-upgrade"></a>Actualización local
1. Inicie a hello Azure AD Connect instalador (MSI).
2. Revise y acepte los términos de toolicense y aviso de privacidad.  
   ![Página principal tooAzure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Welcome.png)
3. Haga clic en el siguiente análisis toobegin de la instalación existente de DirSync.  
   ![Análisis de la instalación de Directory Sync existente](./media/active-directory-aadconnect-dirsync-upgrade-get-started/Analyze.png)
4. Cuando se completa el análisis de hello, vea las recomendaciones de hello sobre cómo tooproceed.  
   * Si utiliza SQL Server Express y tiene menos de 50.000 objetos, se muestra hello después de pantalla:  
     ![El análisis completó tooupgrade listo de sincronización de directorios](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReady.png)
   * Si usa una instancia completa de SQL Server para DirSync, verá esta página en su lugar:  
     ![El análisis completó tooupgrade listo de sincronización de directorios](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisReadyFullSQL.png)  
     se muestra información de Hello sobre Hola existente la servidor de base de datos SQL Server que se va a usar DirSync. Si es necesario, realice los ajustes adecuados. Haga clic en **siguiente** instalación de hello toocontinue.
   * Si tiene más de 50 000 objetos, verá esta pantalla en su lugar:  
     ![El análisis completó tooupgrade listo de sincronización de directorios](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)  
     tooproceed con una actualización en contexto, haga clic en la casilla de verificación siguiente toothis mensaje de Hola: **continuar actualizando DirSync en este equipo.**
     toodo una [implementación en paralelo](#parallel-deployment) en su lugar, exportar la configuración de sincronización de directorios de Hola y mover Hola configuración toohello nuevo servidor.
5. Proporcione la contraseña de Hola para cuenta de hello que usa actualmente tooconnect tooAzure AD. Debe tratarse de cuenta de hello utilizado actualmente por la sincronización de directorios.  
   ![Escriba sus credenciales de Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToAzureAD.png)  
   Si aparece un error y tiene problemas de conectividad, consulte [Solución de problemas de conectividad](active-directory-aadconnect-troubleshoot-connectivity.md).
6. Proporcione una cuenta de administrador de empresa para Active Directory.  
   ![Escriba sus credenciales de ADDS](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ConnectToADDS.png)
7. Ahora está listo tooconfigure. Al hacer clic en **Actualizar**, se desinstala DirSync, se configura Azure AD Connect y comienza la sincronización.  
   ![Tooconfigure listo](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ReadyToConfigure.png)
8. Una vez finalizada la instalación de hello, la sesión e iníciela de nuevo tooWindows antes de usarlos Synchronization Service Manager, Editor de reglas de sincronización, o intente toomake cualquier otro cambio de configuración.

## <a name="parallel-deployment"></a>Implementación paralela
### <a name="export-hello-dirsync-configuration"></a>Exportar la configuración de sincronización de directorios de Hola
**Implementación paralela con más de 50.000 objetos**

Si tiene más de 50.000 objetos, Hola instalación de Azure AD Connect recomienda una implementación paralela.

Se muestra a continuación toohello similar de pantalla:  
![Análisis completo](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AnalysisRecommendParallel.png)

Si desea que tooproceed con la implementación paralela, necesita hello tooperform pasos:

* Haga clic en hello **exportar la configuración** botón. Al instalar Azure AD Connect en un servidor independiente, esta configuración se migra desde la actual tooyour de DirSync nueva instalación de Azure AD Connect.

Una vez que la configuración se ha exportado correctamente, puede salir del Asistente de Azure AD Connect de hello en el servidor de sincronización de directorios de Hola. Continúe con el paso siguiente de hello demasiado[instalar Azure AD Connect en un servidor independiente](#installation-of-azure-ad-connect-on-separate-server)

**Implementación paralela con menos de 50.000 objetos**

Si tiene menos de 50.000 objetos pero sigue deseando toodo una implementación en paralelo, a continuación, Hola siguientes:

1. Ejecute a hello Azure AD Connect installer (MSI).
2. Cuando vea hello **tooAzure bienvenida AD Connect** pantalla Asistente para la instalación de Hola de salida, haga clic en "X" hello en hello superior derecho de la ventana hello.
3. Abra el símbolo del sistema.
4. Ubicación de Azure AD Connect de instalación de hello (predeterminado: C:\Program Files\Microsoft Azure Active Directory Connect) ejecute el siguiente comando de hello: `AzureADConnect.exe /ForceExport`.
5. Haga clic en hello **exportar la configuración** botón. Al instalar Azure AD Connect en un servidor independiente, esta configuración se migra desde la actual tooyour de DirSync nueva instalación de Azure AD Connect.

![Análisis completo](./media/active-directory-aadconnect-dirsync-upgrade-get-started/forceexport.png)

Una vez que la configuración se ha exportado correctamente, puede salir del Asistente de Azure AD Connect de hello en el servidor de sincronización de directorios de Hola. Continúe con el paso siguiente de hello demasiado[instalar Azure AD Connect en un servidor independiente](#installation-of-azure-ad-connect-on-separate-server).

### <a name="install-azure-ad-connect-on-separate-server"></a>Instalación de Azure AD Connect en un servidor independiente
Al instalar Azure AD Connect en un servidor nuevo, Hola supone que desea tooperform una instalación limpia de Azure AD Connect. Dado que desee que la configuración de sincronización de directorios de hello toouse, hay algunos pasos adicionales tootake:

1. Ejecute a hello Azure AD Connect installer (MSI).
2. Cuando vea hello **tooAzure bienvenida AD Connect** pantalla Asistente para la instalación de Hola de salida, haga clic en "X" hello en hello superior derecho de la ventana hello.
3. Abra el símbolo del sistema.
4. Ubicación de Azure AD Connect de instalación de hello (predeterminado: C:\Program Files\Microsoft Azure Active Directory Connect) ejecute el siguiente comando de hello: `AzureADConnect.exe /migrate`.
   Asistente para la instalación de Hello Azure AD Connect se inicia y presenta con hello después de pantalla:  
   ![Escriba sus credenciales de Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/ImportSettings.png)
5. Seleccione el archivo de configuración de hello que exporta de la instalación de sincronización de directorios.
6. Configure las opciones avanzadas, que se incluyen:
   * Una ubicación de instalación personalizada para Azure AD Connect.
   * Una instancia existente de SQL Server (de forma predeterminada, Azure AD Connect instala SQL Server 2012 Express) No utilice Hola misma instancia de base de datos que el servidor de sincronización de directorios.
   * Una cuenta de servicio usa tooconnect tooSQL Server (si la base de datos de SQL Server es remoto, a continuación, esta cuenta debe ser una cuenta de servicio de dominio).
     Estas opciones se pueden ver en esta pantalla:   
     ![Escriba sus credenciales de Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/advancedsettings.png)
7. Haga clic en **Siguiente**.
8. En hello **tooconfigure listo** página, deje hello **iniciar el proceso de sincronización de hello tan pronto como finalice la configuración de hello** activada. servidor de Hello está ahora en [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode) por lo que los cambios no son exportado tooAzure AD.
9. Haga clic en **Instalar**.
10. Una vez finalizada la instalación de hello, la sesión e iníciela de nuevo tooWindows antes de usarlos Synchronization Service Manager, Editor de reglas de sincronización, o intente toomake cualquier otro cambio de configuración.

> [!NOTE]
> Comienza la sincronización entre Active Directory de Windows Server y Active Directory de Azure, pero ningún cambio es exportado tooAzure AD. Solo una herramienta de sincronización puede a exportar activamente los cambios de una vez. Este estado se denomina [modo provisional](active-directory-aadconnectsync-operations.md#staging-mode).

### <a name="verify-that-azure-ad-connect-is-ready-toobegin-synchronization"></a>Compruebe que Azure AD Connect es sincronización toobegin listo
tooverify que Azure AD Connect está listo tootake a través de DirSync, necesita tooopen **Synchronization Service Manager** en grupo de hello **Azure AD Connect** desde el menú de inicio de Hola.

En la aplicación hello, vaya toohello **Operations** ficha. En esta pestaña, confirme completado ese hello las siguientes operaciones:

* Importar en hello conector de AD
* Importar en hello conector de Azure AD
* Sincronización completa en hello conector de AD
* Sincronización completa en hello conector de Azure AD

![Importación y sincronización completadas](./media/active-directory-aadconnect-dirsync-upgrade-get-started/importsynccompleted.png)

Revise el resultado de hello de esas operaciones y asegúrese de que no hay errores.

Si desea toosee e inspeccionar cambios Hola sobre toobe exportar tooAzure AD, a continuación, lea cómo tooverify Hola configuración bajo [modo de almacenamiento provisional](active-directory-aadconnectsync-operations.md#staging-mode). Realice los cambios de configuración necesarios hasta que no vea nada inesperado.

Está listo tooswitch desde DirSync tooAzure AD cuando haya completado estos pasos y esté satisfecho con el resultado de hello.

### <a name="uninstall-dirsync-old-server"></a>Desinstalación de DirSync (servidor antiguo)
* En **Programas y características**, busque **Herramienta de sincronización de Microsoft Azure Active Directory**
* Desinstale la **Herramienta de sincronización de Microsoft Azure Active Directory**
* desinstalación de Hello podría tardar hasta too15 minutos toocomplete.

Si prefiere toouninstall DirSync más adelante, puede apagar el servidor de Hola temporalmente o deshabilitar el servicio de Hola. Si algo va mal, este método le permite habilitar toore lo. Sin embargo, no se espera que ese paso Hola se producirá un error por lo que esto no debería ser necesario.

Con DirSync ha desinstalado o deshabilitado, no hay ningún servidor de active exportar tooAzure AD. Hola siguiente paso tooenable Azure AD Connect se debe completar antes de que los cambios en su Active Directory local continuará toobe sincronizado tooAzure AD.

### <a name="enable-azure-ad-connect-new-server"></a>Apertura de Azure AD Connect (nuevo servidor)
Después de la instalación, volver a abrir Azure AD connect estará permitir cambios de configuración adicionales de toomake. Iniciar **Azure AD Connect** desde el menú de inicio de Hola o acceso directo de hello en el escritorio de Hola. Asegúrese de que no intente toorun Hola instalación MSI nuevo.

Debería ver Hola siguiente:  
![Tareas adicionales](./media/active-directory-aadconnect-dirsync-upgrade-get-started/AdditionalTasks.png)

* Seleccione **Configurar modo de almacenamiento provisional**.
* Desactivar el almacenamiento provisional, Hola desactivando **modo de almacenamiento provisional habilitado** casilla de verificación.

![Escriba sus credenciales de Azure AD](./media/active-directory-aadconnect-dirsync-upgrade-get-started/configurestaging.png)

* Haga clic en hello **siguiente** botón
* En la página de confirmación de hello, haga clic en hello **instalar** botón.

Azure AD Connect es ahora el servidor activo y no debe cambiar toousing espera del servidor de sincronización de directorios existente.

## <a name="next-steps"></a>Pasos siguientes
Ahora que tiene instalado de Azure AD Connect puede [comprobar la instalación de Hola y asignar licencias](active-directory-aadconnect-whats-next.md).

Obtener más información sobre estas nuevas características, que estaban habilitadas con la instalación de hello: [la actualización automática](active-directory-aadconnect-feature-automatic-upgrade.md), [evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md), y [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md).

Más información acerca de estos temas comunes: [programador y cómo sincronizar tootrigger](active-directory-aadconnectsync-feature-scheduler.md).

Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).
