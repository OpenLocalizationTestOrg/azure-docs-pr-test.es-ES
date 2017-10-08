---
title: "Configuración de filtrado de sincronización de Azure AD Connect | Microsoft Docs"
description: "Explica cómo tooconfigure filtrado en la sincronización de Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 880facf6-1192-40e9-8181-544c0759d506
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 97979b508c560a6de6cb091b1b621bc1d51b25c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-configure-filtering"></a>Azure AD Connect Sync: configuración del filtrado
Con el filtrado puede controlar qué objetos aparecen en Azure Active Directory (Azure AD) desde el directorio local. configuración predeterminada de Hello toma todos los objetos en todos los dominios de bosques de hello configurado. En general, se trata de hello configuración recomendada. Los usuarios con cargas de trabajo de Office 365, como Exchange Online y Skype Empresarial, se benefician de una lista global de direcciones completa para poder enviar correo electrónico y llamar a todos los integrantes. Con la configuración predeterminada de hello, tendrían Hola que misma experiencia que tienen con una implementación local de Exchange o Lync.

Sin embargo, en algunos casos está requiere realizar alguna configuración predeterminada de toohello de cambios. Estos son algunos ejemplos:

* Planear hello toouse [topología de directorio de AD Azure varias](active-directory-aadconnect-topologies.md#each-object-only-once-in-an-azure-ad-tenant). A continuación, deberá tooapply un toocontrol filtro qué objetos están sincronizados tooa AD de Azure determinado directorio.
* Va a ejecutar un piloto para Azure u Office 365 y desea solo un subconjunto de usuarios en Azure AD. En hello pequeña prueba piloto no es importante toohave una lista Global de direcciones toodemonstrate Hola una funcionalidad completa.
* Tiene numerosas cuentas de servicio y otras de carácter no personal que no desea en Azure AD.
* Por motivos de cumplimiento, no elimina ninguna cuenta de usuario local. Solo las deshabilita. Pero en Azure AD, sólo desea que las cuentas de active toobe presente.

Este artículo trata cómo tooconfigure Hola diferentes métodos de filtrado.

> [!IMPORTANT]
> No es compatible con Microsoft modificar u operando sincronización de Azure AD Connect fuera de las acciones de Hola que están documentadas formalmente. Cualquiera de estas acciones pueden provocar un estado incoherente o incompatible de sincronización de Azure AD Connect. Como resultado, Microsoft no ofrece soporte técnico para estas implementaciones.

## <a name="basics-and-important-notes"></a>Conceptos básicos y notas importantes
En Azure AD Connect Sync, puede habilitar el filtrado en cualquier momento. Si comienza con una configuración predeterminada de sincronización de directorios y, a continuación, configurar el filtrado, los objetos de Hola que se filtran ya no están sincronizado tooAzure AD. Por este cambio, en Azure AD se eliminan los objetos de Azure AD que se sincronizaran previamente pero que se filtraran después.

Antes de empezar a realizar cambios toofiltering, asegúrese de que se [deshabilitar la tarea programada de hello](#disable-scheduled-task) para no exportar accidentalmente cambios que aún no ha comprobado toobe correcto.

Ya puede eliminar muchos objetos en hello el filtrado mismo tiempo, desea toomake seguro de que los nuevos filtros son correctos antes de empezar cualquier exportación cambia tooAzure AD. Después de haber completado los pasos de configuración de hello, se recomienda que siga hello [pasos de comprobación](#apply-and-verify-changes) para exportar y hacer cambios tooAzure AD.

característica tooprotect desde eliminar muchos objetos por accidente, hello "[evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" está activada de forma predeterminada. Si se eliminan muchos objetos debido a toofiltering (500 de forma predeterminada), necesita conocer pasos de hello toofollow este Hola de tooallow artículo elimina toogo a través de tooAzure AD.

Si usa una compilación antes de noviembre de 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)), realice una configuración de filtro de cambio tooa y utilizar la sincronización de contraseña, deberá tootrigger una sincronización completa de todas las contraseñas después de haber completado la configuración de Hola. Para conocer los pasos en la sincronización de completa de tootrigger una contraseña, vea [desencadenar una sincronización completa de todas las contraseñas](active-directory-aadconnectsync-troubleshoot-password-synchronization.md#trigger-a-full-sync-of-all-passwords). Si está en la compilación 1.0.9125 o una versión posterior, a continuación, Hola regular **sincronización completa** acción también calcula si se deben sincronizar las contraseñas y si este paso adicional ya no es necesario.

Si **usuario** se han eliminado objetos por accidente en Azure AD debido a un error de filtrado, puede volver a crear objetos de usuario de hello en Azure AD mediante la eliminación de las configuraciones de filtrado. A continuación, podrá volver a sincronizar los directorios. Esta acción restaura los usuarios de Hola de Papelera de reciclaje de hello en Azure AD. Sin embargo, no se pueden recuperar otros tipos de objeto. Por ejemplo, si elimina un grupo de seguridad y era tooACL usa un recurso, grupo de Hola y su ACL no se puede recuperar.

Azure AD Connect sólo elimina los objetos que una vez que considera toobe en el ámbito. Si hay objetos en Azure AD que se crearon con otro motor de sincronización y que no estén dentro del ámbito, no se quitarán al agregar el filtrado. Por ejemplo, si empieza con un servidor de sincronización de directorios que crea una copia completa de todo el directorio en Azure AD e instalar a un nuevo servidor de sincronización de Azure AD Connect en paralelo con el filtrado habilitado desde el principio de hello, Azure AD Connect no quita Hola adicional objetos que se crean mediante la sincronización de directorios.

configuración del filtrado de Hola se conserva al instalar o actualizar la versión más reciente de tooa de Azure AD Connect. Es siempre un tooverify prácticas recomendada que Hola configuración no se cambió por accidente después una versión más reciente de actualización tooa antes de ejecutar Hola primer ciclo de sincronización.

Si tiene más de un bosque y, a continuación, debe aplicar Hola filtrado configuraciones que se describen en este bosque tooevery de tema (suponiendo que desea Hola misma configuración para todas ellas).

### <a name="disable-hello-scheduled-task"></a>Deshabilitar la tarea programada de Hola
programador integrados de toodisable Hola que desencadena un ciclo de sincronización cada 30 minutos, siga estos pasos:

1. Vaya el símbolo del sistema de PowerShell de tooa.
2. Ejecutar `Set-ADSyncScheduler -SyncCycleEnabled $False` programador de hello toodisable.
3. Realice los cambios de Hola que se documentan en este artículo.
4. Ejecutar `Set-ADSyncScheduler -SyncCycleEnabled $True` tooenable nuevo programador de Hola.

**Si usa una compilación de Azure AD Connect anterior a 1.1.105.0**  
tarea programada de toodisable Hola que desencadena un ciclo de sincronización cada tres horas, siga estos pasos:

1. Iniciar **programador de tareas** de hello **iniciar** menú.
2. Directamente en **biblioteca del programador de tareas**, tarea de Hola de búsqueda denominada **Azure AD Sync Scheduler**, menú contextual y seleccione **deshabilitar**.  
   ![Programador de tareas](./media/active-directory-aadconnectsync-configure-filtering/taskscheduler.png)  
3. Ahora puede realizar cambios de configuración y ejecutar el motor de sincronización de hello manualmente de hello **Synchronization Service Manager** consola.

Después de haber completado todos los cambios de filtrado, no olvide volver toocome y **habilitar** tarea hello nuevo.

## <a name="filtering-options"></a>Opciones de filtrado
Puede aplicar Hola después de la herramienta de sincronización de directorio toohello de tipos de configuración filtrado:

* [**Basado en grupos**](#group-based-filtering): filtrado basado en un único grupo sólo puede configurarse en la instalación inicial usando el Asistente para la instalación de Hola.
* [**Basado en dominio**](#domain-based-filtering): con esta opción, puede seleccionar qué dominios sincronización tooAzure AD. También puede agregar y quitar dominios de configuración del motor de sincronización de hello cuando se realiza la infraestructura local de cambios tooyour después de instalar sincronización de Azure AD Connect.
* [**Unidad organizativa (OU) – según**](#organizational-unitbased-filtering): con esta opción, puede seleccionar qué OU sincronizar tooAzure AD. Esta opción está en todos los tipos de objeto de las unidades organizativas seleccionadas.
* [**Basado en atributos**](#attribute-based-filtering): con esta opción, puede filtrar los objetos basados en valores de atributo en objetos de Hola. También puede tener filtros diferentes para distintos tipos de objetos.

Puede utilizar varias opciones de filtrado en hello mismo tiempo. Por ejemplo, puede usar el filtrado basado en la unidad organizativa tooonly incluir objetos en una unidad organizativa. Hola al mismo tiempo, puede usar basado en atributos objetos de hello toofilter filtrado aún más. Cuando se usan varios métodos de filtrado, los filtros de hello utilizan un operador lógico "AND" entre los filtros de Hola.

## <a name="domain-based-filtering"></a>Filtrado basado en dominios
Esta sección proporciona Hola pasos tooconfigure el filtro de dominios. Si agrega o quitar dominios del bosque después de instalar Azure AD Connect, también tiene hello tooupdate configuración del filtrado.

Hola preferido toochange basado en dominio filtrado está ejecutando el Asistente para la instalación de Hola y cambiar de manera [dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Asistente para la instalación de Hello automatiza todas las tareas de Hola que se documentan en este tema.

Solo deben seguir estos pasos si eres un Asistente para la instalación no se puede toorun Hola por algún motivo.

La configuración del filtrado basado en dominios consta de estos pasos:

1. [Seleccione los dominios de hello](#select-domains-to-be-synchronized) que desea tooinclude en la sincronización de Hola.
2. Para cada uno de ellos se agregan y se quitan de dominio, ajuste hello [perfiles de ejecución](#update-run-profiles).
3. [Aplicación y comprobación de los cambios](#apply-and-verify-changes).

### <a name="select-hello-domains-toobe-synchronized"></a>Seleccione Hola dominios toobe sincronizado
dominio de hello tooset filtrar, Hola lo siguiente:

1. Inicie sesión en el servidor de toohello que se ejecuta la sincronización de Azure AD Connect con una cuenta que sea miembro del programa Hola a **ADSyncAdmins** grupo de seguridad.
2. Iniciar **servicio de sincronización de** de hello **iniciar** menú.
3. Seleccione **conectores**y en hello **conectores** seleccione Hola conector con el tipo de hello **los servicios de dominio de Active Directory**. En **Acciones**, seleccione **Propiedades**.  
   ![Propiedades del conector](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Haga clic en **Configurar particiones de directorio**.
5. Hola **seleccionar particiones de directorio** lista, seleccione y anule la selección de dominios según sea necesario. Compruebe que están seleccionadas solo las particiones de Hola que desea toosynchronize.  
   ![Particiones](./media/active-directory-aadconnectsync-configure-filtering/connectorpartitions.png)  
   Si ha cambiado la infraestructura de Active Directory local y agregar o quitar dominios del bosque de hello, a continuación, haga clic en hello **actualizar** tooget una lista actualizada de botón. Al actualizar, se le pedirán las credenciales. Proporcionar las credenciales con acceso de lectura tooWindows Server Active Directory. No tiene usuarios de hello toobe que se rellena previamente en el cuadro de diálogo de Hola.  
   ![Actualización necesaria](./media/active-directory-aadconnectsync-configure-filtering/refreshneeded.png)  
6. Cuando haya terminado, cierre hello **propiedades** haciendo clic en el cuadro de diálogo **Aceptar**. Si quita dominios del bosque de hello, un mensaje emergente indica que se ha quitado un dominio y que la configuración se limpiarán.
7. Continuar hello tooadjust [perfiles de ejecución](#update-run-profiles).

### <a name="update-hello-run-profiles"></a>Actualizar los perfiles de hello ejecutar
Si ha actualizado el filtro de dominios, debe también perfiles de hello ejecutar tooupdate.

1. Hola **conectores** lista, asegúrese de que ese Hola conector que cambió en el paso anterior de hello está seleccionada. En **Acciones**, seleccione **Configure Run Profiles** (Configurar perfiles de ejecución).  
   ![Perfiles de ejecución de conector 1](./media/active-directory-aadconnectsync-configure-filtering/connectorrunprofiles1.png)  
2. Busque e identifique Hola siguientes perfiles:
    * Importación completa
    * sincronización completa
    * Importación delta
    * Sincronización delta
    * Exportación
3. Para cada perfil, ajustar hello **agregado** y **quitado** dominios.
    1. Para cada uno de los perfiles de hello cinco, Hola lo siguiente para cada **agregado** dominio:
        1. Seleccione el perfil de hello ejecutar y haga clic en **nuevo paso**.
        2. En hello **configurar paso** página Hola **tipo** menú desplegable, seleccione Hola el tipo de paso con hello mismo nombre hello perfiles que se va a configurar. A continuación, haga clic en **Siguiente**.  
        ![Perfiles de ejecución de conector 2](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep1.png)  
        3. En hello **configuración del conector** página Hola **partición** menú desplegable, el nombre de hello seleccione del dominio de Hola que ha agregado el filtro de dominios tooyour.  
        ![Perfiles de ejecución de conector 3](./media/active-directory-aadconnectsync-configure-filtering/runprofilesnewstep2.png)  
        4. Hola tooclose **configurar perfiles de ejecución** cuadro de diálogo, haga clic en **finalizar**.
    2. Para cada uno de los perfiles de hello cinco, Hola lo siguiente para cada **quitado** dominio:
        1. Seleccione el perfil de hello ejecutar.
        2. Si hello **valor** de hello **partición** atributo es un GUID, seleccione Hola ejecutar paso y haga clic en **eliminar paso**.  
        ![Perfiles de ejecución de conector 4](./media/active-directory-aadconnectsync-configure-filtering/runprofilesdeletestep.png)  
    3. Compruebe el cambio. Cada dominio que desea toosynchronize debe aparecer como un paso en cada perfil de ejecución.
4. Hola tooclose **configurar perfiles de ejecución** cuadro de diálogo, haga clic en **Aceptar**.
5.  configuración de hello toocomplete, deberá toorun un **importación completa** y un **sincronización diferencial**. Continúe leyendo Hola sección [aplicar y comprobar los cambios](#apply-and-verify-changes).

## <a name="organizational-unitbased-filtering"></a>Filtrado por unidad organizativa
Hola preferido toochange OU filtrado está ejecutando el Asistente para la instalación de Hola y cambiar de manera [dominio y unidad organizativa filtrado](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering). Asistente para la instalación de Hello automatiza todas las tareas de Hola que se documentan en este tema.

Solo deben seguir estos pasos si eres un Asistente para la instalación no se puede toorun Hola por algún motivo.

tooconfigure organizativa unidad filtrado basado en, Hola lo siguiente:

1. Inicie sesión en el servidor de toohello que se ejecuta la sincronización de Azure AD Connect con una cuenta que sea miembro del programa Hola a **ADSyncAdmins** grupo de seguridad.
2. Iniciar **servicio de sincronización de** de hello **iniciar** menú.
3. Seleccione **conectores**y en hello **conectores** seleccione Hola conector con el tipo de hello **los servicios de dominio de Active Directory**. En **Acciones**, seleccione **Propiedades**.  
   ![Propiedades del conector](./media/active-directory-aadconnectsync-configure-filtering/connectorproperties.png)  
4. Haga clic en **configurar particiones de directorio**, seleccione dominio de Hola que desee tooconfigure y, a continuación, haga clic en **contenedores**.
5. Cuando se le pida, proporcione las credenciales con acceso de lectura tooyour en Active Directory local. No tiene usuarios de hello toobe que se rellena previamente en el cuadro de diálogo de Hola.
6. Hola **seleccionar contenedores** cuadro de diálogo, desactive hello las unidades organizativas que no desee toosynchronize con el directorio de la nube de hello y, a continuación, haga clic en **Aceptar**.  
   ![Unidades organizativas en el cuadro de diálogo Seleccionar contenedores de Hola](./media/active-directory-aadconnectsync-configure-filtering/ou.png)  
   * Hola **equipos** contenedor debe seleccionarse para su toobe de equipos de Windows 10 sincronizado correctamente tooAzure AD. Si los equipos unidos a un dominio se encuentran en otras unidades organizativas, asegúrese de que estén seleccionadas.
   * Hola **ForeignSecurityPrincipals** contenedor debe seleccionarse si tiene varios bosques con relaciones de confianza. Este contenedor permite toobe de pertenencia a grupo de seguridad entre bosques resuelto.
   * Hola **RegisteredDevices** unidad organizativa debe seleccionarse si habilitó la característica de reescritura de dispositivos de Hola. Si usa otra característica de reescritura, como la de grupos, asegúrese de que estas ubicaciones estén seleccionadas.
   * Seleccione cualquier otra unidad organizativa donde se encuentren usuarios, objetos InetOrgPerson, grupos, contactos y equipos. En la imagen de hello, todas estas unidades organizativas se encuentran en hello ManagedObjects OU.
   * Si usa el filtrado basado en el grupo, se debe incluir Hola unidad organizativa donde se encuentra el grupo de Hola.
   * Tenga en cuenta que puede configurar si unidades organizativas nuevas que se agregan una vez finalizada la configuración del filtrado de Hola se sincronizado o no. Vea la siguiente sección de Hola para obtener más información.
7. Cuando haya terminado, cierre hello **propiedades** haciendo clic en el cuadro de diálogo **Aceptar**.
8. configuración de hello toocomplete, deberá toorun un **importación completa** y un **sincronización diferencial**. Continúe leyendo Hola sección [aplicar y comprobar los cambios](#apply-and-verify-changes).

### <a name="synchronize-new-ous"></a>Sincronización de unidades organizativas nuevas
Las unidades organizativas nuevas creadas una vez que se ha configurado el filtrado se sincronizan de forma predeterminada. Esto se indica mediante una marca en la casilla. También se puede anular la selección de algunas subunidades organizativas. tooget este comportamiento, haga clic en el cuadro de hello hasta que esté en blanco y una marca de verificación azul (su estado predeterminado). A continuación, anule la selección de las subunidades que no desea toosynchronize.

Si no se sincronizan todas las subunidades organizativas, cuadro de hello es blanca con una marca de verificación azul.  
![Unidad organizativa con todas las casillas activadas](./media/active-directory-aadconnectsync-configure-filtering/ousyncnewall.png)

Si algunos subunidades ha anulado la selección, cuadro de hello es gris con una marca de verificación blanca.  
![Unidad organizativa con la selección de algunas subunidades organizativas anulada](./media/active-directory-aadconnectsync-configure-filtering/ousyncnew.png)

Con esta configuración, se sincronizará la nueva unidad organizativa que se creó en ManagedObjects.

Asistente para la instalación de Hello Azure AD Connect siempre crea esta configuración.

### <a name="dont-synchronize-new-ous"></a>No sincronizar unidades organizativas nuevas
Puede configurar la sincronización de hello motor toonot sincronizar unidades organizativas nuevas una vez finalizada la configuración del filtrado de Hola. Este estado se indica en la interfaz de usuario que aparecen de color gris sólido con ninguna marca de verificación de cuadro de Hola Hola. tooget este comportamiento, haga clic en el cuadro de hello hasta que esté en blanco y sin marca de verificación. A continuación, seleccione Hola subunidades organizativas que desea toosynchronize.

![Unidad organizativa con la raíz de hello anular la selección](./media/active-directory-aadconnectsync-configure-filtering/oudonotsyncnew.png)

Con esta configuración, no se sincronizará la nueva unidad organizativa que se creó en ManagedObjects.

## <a name="attribute-based-filtering"></a>Filtrado basado en atributos
Asegúrese de que está usando Hola de noviembre de 2015 ([1.0.9125](active-directory-aadconnect-version-history.md#1091250)) o una compilación posterior para estos pasos toowork.

Filtrado basado en atributos es objetos de toofilter de manera más flexibles de Hola. Puede usar power Hola de [aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning.md) toocontrol prácticamente todos los aspectos de cuando un objeto se encuentra sincronizan tooAzure AD.

Puede aplicar [entrada](#inbound-filtering) filtrado de metaverso de toohello de Active Directory, y [saliente](#outbound-filtering) filtrado de hello metaverso tooAzure AD. Se recomienda aplicar filtrado entrante, ya es más fácil toomaintain de Hola. Solo se debe utilizar el filtrado de salida si se requiere toojoin objetos de más de un bosque antes de que puede tener lugar la evaluación de Hola.

### <a name="inbound-filtering"></a>Filtrado entrante
Filtrado de entrada usa configuración predeterminada de hello, donde objetos tooAzure AD deben establecerse Hola metaverso atributo cloudFiltered no tooa valor toobe sincronizado. Si el valor de este atributo se establece demasiado**True**, a continuación, el objeto de hello no está sincronizado. No debería establecerse demasiado**False**, por diseño. toomake que otras reglas tienen Hola capacidad toocontribute un valor, este atributo solo se supone que los valores de hello toohave **True** o **NULL** (ausente).

En el filtrado de entrada, use power Hola de **ámbito** toodetermine que objetos toosynchronize o no se sincronice. Aquí es donde realizar ajustes toofit los requisitos de su propia organización. módulo de ámbito de Hello tiene un **grupo** y un **cláusula** toodetermine cuando una regla de sincronización está en ámbito. Un grupo contiene una o varias cláusulas. Existe un operador lógico AND entre varias cláusulas y un operador lógico OR entre varios grupos.

Veamos un ejemplo:   
![Ámbito](./media/active-directory-aadconnectsync-configure-filtering/scope.png)  
Se debe leer como **(departamento = TI) O BIEN (departamento = Ventas Y c = Estados Unidos)**.

En hello después de ejemplos y los pasos, utilice el objeto de usuario de hello como ejemplo, pero se puede usar para todos los tipos de objetos.

En los siguientes ejemplos de hello, valor de prioridad de hello empieza con 50. Puede ser cualquier número no usado, pero debe ser menor que 100.

#### <a name="negative-filtering-do-not-sync-these"></a>Filtrado negativo: "no sincronizar estos"
En el siguiente ejemplo de Hola, filtra (no sincronizar) todos los usuarios que **extensionAttribute15** tiene el valor de hello **NoSync**.

1. Inicie sesión en el servidor de toohello que se ejecuta la sincronización de Azure AD Connect con una cuenta que sea miembro del programa Hola a **ADSyncAdmins** grupo de seguridad.
2. Iniciar **Editor de reglas de sincronización** de hello **iniciar** menú.
3. Asegúrese de que **Entrante** esté seleccionado y haga clic en **Agregar nueva regla**.
4. Asigne a Hola regla un nombre descriptivo, como "*en desde AD – User DoNotSyncFilter*". Bosque correcto de hello seleccione, seleccione **usuario** como hello **tipo de objeto CS**y seleccione **persona** como hello **tipo de objeto MV**. En **Tipo de vínculo**, seleccione **Unir**. En **Precedencia**, escriba un valor que no use actualmente ninguna otra regla de sincronización (por ejemplo, 50) y haga clic en **Siguiente**.  
   ![Descripción de entrante 1](./media/active-directory-aadconnectsync-configure-filtering/inbound1.png)  
5. En **Scoping filter** (Filtro de ámbito), haga clic en **Agregar grupo** y en **Agregar cláusula**. En **Atributo**, seleccione **ExtensionAttribute15**. Asegúrese de que **operador** se establece demasiado**igual**y escriba el valor de hello **NoSync** en hello **valor** cuadro. Haga clic en **Siguiente**.  
   ![Ámbito de entrante 2](./media/active-directory-aadconnectsync-configure-filtering/inbound2.png)  
6. Deje hello **unir** reglas vacío y, a continuación, haga clic en **siguiente**.
7. Haga clic en **Agregar transformación**, seleccione hello **FlowType** como **constante**y seleccione **cloudFiltered** como hello  **Atributo de destino**. Hola **origen** cuadro de texto, escriba **True**. Haga clic en **agregar** regla de toosave Hola.  
   ![Transformación de entrante 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)
8. configuración de hello toocomplete, deberá toorun un **sincronización completa**. Continúe leyendo Hola sección [aplicar y comprobar los cambios](#apply-and-verify-changes).

#### <a name="positive-filtering-only-sync-these"></a>Filtrado positivo: "solo sincronizar estos"
Cuando se expresan filtrado positivo puede ser más difícil porque también tiene tooconsider objetos que no son evidente toobe sincronizada, como salas de conferencias. También son filtro predeterminado de curso toooverride Hola regla de out-of-box hello **en desde AD - User Join**. Cuando se crea el filtro personalizado, asegúrese de que toonot incluyen objetos críticos del sistema, objetos de conflictos de replicación, los buzones especiales y las cuentas de servicio de Hola para Azure AD Connect.

opción de filtrado positivo Hola requiere dos reglas de sincronización. Necesitará una regla (o varios) con ámbito correcto de Hola de toosynchronize de objetos. También necesita una segunda regla de sincronización general que filtre todos los objetos que aún no se hayan identificado como objeto para sincronizar.

En el siguiente ejemplo de Hola, sólo sincronizar objetos de usuario donde el atributo del departamento de hello tiene valor hello **ventas**.

1. Inicie sesión en el servidor de toohello que se ejecuta la sincronización de Azure AD Connect con una cuenta que sea miembro del programa Hola a **ADSyncAdmins** grupo de seguridad.
2. Iniciar **Editor de reglas de sincronización** de hello **iniciar** menú.
3. Asegúrese de que **Entrante** esté seleccionado y haga clic en **Agregar nueva regla**.
4. Asigne a Hola regla un nombre descriptivo, como "*en desde AD – usuario ventas sincronizar*". Bosque correcto de hello seleccione, seleccione **usuario** como hello **tipo de objeto CS**y seleccione **persona** como hello **tipo de objeto MV**. En **Tipo de vínculo**, seleccione **Unir**. En **Precedencia**, escriba un valor que no use actualmente ninguna otra regla de sincronización (por ejemplo, 51) y haga clic en **Siguiente**.  
   ![Descripción de entrante 4](./media/active-directory-aadconnectsync-configure-filtering/inbound4.png)  
5. En **Scoping filter** (Filtro de ámbito), haga clic en **Agregar grupo** y en **Agregar cláusula**. En **Atributo**, seleccione **department**. Asegúrese de que el operador está establecido demasiado**igual**y escriba el valor de hello **ventas** en hello **valor** cuadro. Haga clic en **Siguiente**.  
   ![Ámbito de entrante 5](./media/active-directory-aadconnectsync-configure-filtering/inbound5.png)  
6. Deje hello **unir** reglas vacío y, a continuación, haga clic en **siguiente**.
7. Haga clic en **Agregar transformación**, seleccione **constante** como hello **FlowType**, seleccione hello y **cloudFiltered** como hello  **Atributo de destino**. Hola **origen** , escriba **False**. Haga clic en **agregar** regla de toosave Hola.  
   ![Transformación de entrante 6](./media/active-directory-aadconnectsync-configure-filtering/inbound6.png)  
   Se trata de un caso especial que se establece explícitamente cloudFiltered demasiado**False**.
8. Ahora tenemos la regla de sincronización de catch-all de hello toocreate. Asigne a Hola regla un nombre descriptivo, como "*en de AD: el filtro de usuario general*". Bosque correcto de hello seleccione, seleccione **usuario** como hello **tipo de objeto CS**y seleccione **persona** como hello **tipo de objeto MV**. En **Tipo de vínculo**, seleccione **Unir**. En **Precedencia**, escriba un valor que no use actualmente ninguna otra regla de sincronización (por ejemplo, 99). Ha seleccionado un valor de prioridad que es la prioridad más alta (inferior) que la regla de sincronización anterior Hola. Pero también se ha dejado algo de espacio para que pueda agregar más reglas de filtrado de sincronización más tarde cuando se desea toostart sincronizar departamentos adicionales. Haga clic en **Siguiente**.  
   ![Descripción de entrante 7](./media/active-directory-aadconnectsync-configure-filtering/inbound7.png)  
9. Deje **Scoping filter** (Filtro de ámbito) vacío y haga clic en **Siguiente**. Un filtro vacío indica que esa regla hello es toobe aplica tooall objetos.
10. Deje hello **unir** reglas vacío y, a continuación, haga clic en **siguiente**.
11. Haga clic en **Agregar transformación**, seleccione **constante** como hello **FlowType**y seleccione **cloudFiltered** como hello  **Atributo de destino**. Hola **origen** , escriba **True**. Haga clic en **agregar** regla de toosave Hola.  
    ![Transformación de entrante 3](./media/active-directory-aadconnectsync-configure-filtering/inbound3.png)  
12. configuración de hello toocomplete, deberá toorun un **sincronización completa**. Continúe leyendo Hola sección [aplicar y comprobar los cambios](#apply-and-verify-changes).

Si necesita, puede crear más reglas de tipo primera Hola donde incluyen más objetos en la sincronización de Hola.

### <a name="outbound-filtering"></a>Filtrado saliente
En algunos casos, resulta hello toodo necesarios filtrado después de hello objetos se hayan unido Hola metaverso. Por ejemplo, sería necesario toolook al atributo de correo electrónico de Hola Hola bosque de recursos y al atributo userPrincipalName de Hola Hola bosque de cuenta, toodetermine si se debe sincronizar un objeto. En estos casos, crear Hola filtrado en la regla de salida de hello.

En este ejemplo, cambiar Hola filtrado para que solo los usuarios que tengan su correo electrónico y el userPrincipalName que terminen en @contoso.com se sincronizan:

1. Inicie sesión en el servidor de toohello que se ejecuta la sincronización de Azure AD Connect con una cuenta que sea miembro del programa Hola a **ADSyncAdmins** grupo de seguridad.
2. Iniciar **Editor de reglas de sincronización** de hello **iniciar** menú.
3. En **Rules Type** (Tipo de reglas), haga clic en **Saliente**.
4. Regla de Hola de búsqueda con el nombre **Out tooAAD – User Join**y haga clic en **editar**.
5. En el menú emergente de hello, responder **Sí** toocreate una copia de la regla de Hola.
6. En hello **descripción** página, cambie **prioridad** tooan valor sin usar, como 50.
7. Haga clic en **filtro de ámbito** en Hola de navegación izquierdo y, a continuación, haga clic en **Agregar cláusula**. En **Atributo**, seleccione **mail**. En **Operador**, seleccione **ENDSWITH**. En **Valor**, escriba **@contoso.com** y haga clic en **Agregar cláusula**. En **Atributo**, seleccione **userPrincipalName**. En **Operador**, seleccione **ENDSWITH**. En **Valor**, escriba **@contoso.com**.
8. Haga clic en **Guardar**.
9. configuración de hello toocomplete, deberá toorun un **sincronización completa**. Continúe leyendo Hola sección [aplicar y comprobar los cambios](#apply-and-verify-changes).

## <a name="apply-and-verify-changes"></a>Aplicación y comprobación de los cambios
Después de realizar los cambios de configuración, debe aplicarlos toohello objetos que ya están presentes en los sistemas de Hola. También es posible que los objetos de Hola que no están actualmente en el motor de sincronización de hello deben procesarse (y motor de sincronización de Hola necesita el sistema de origen de hello tooread nuevo tooverify su contenido).

Si se cambió la configuración de hello mediante el uso de **dominio** o **unidad organizativa** filtrado, deberá toodo un **importación completa**, seguido de **Delta sincronización**.

Si se cambió la configuración de hello mediante el uso de **atributo** filtrado, deberá toodo un **sincronización completa**.

Hola lo siguiente:

1. Iniciar **servicio de sincronización de** de hello **iniciar** menú.
2. Seleccione **Conectores**. Hola **conectores** seleccione Hola conector donde se realizó una cambio de configuración anteriormente. En **Acciones**, seleccione **Ejecutar**.  
   ![Ejecución de conector](./media/active-directory-aadconnectsync-configure-filtering/connectorrun.png)  
3. En **perfiles de ejecución**, seleccione Hola operación que se mencionó en la sección anterior de Hola. Si necesita toorun dos acciones, ha terminado de primera ejecución hello en segundo lugar después de hello. (hello **estado** columna es **inactivo** para conector de hello seleccionado.)

Después de la sincronización de hello, todos los cambios están almacenados provisionalmente toobe exportado. Antes de implementar cambios de hello en Azure AD, desea tooverify que todos estos cambios son correctos.

1. Inicie un símbolo del sistema y vaya demasiado`%Program Files%\Microsoft Azure AD Sync\bin`.
2. Ejecute `csexport "Name of Connector" %temp%\export.xml /f:x`.  
   nombre de Hola de hello conector está en el servicio de sincronización. Tiene un too"contoso.com similar nombre – AAD" para Azure AD.
3. Ejecute `CSExportAnalyzer %temp%\export.xml > %temp%\export.csv`.
4. Ahora tiene un archivo en %temp% denominado export.csv que se puede examinar en Microsoft Excel. Este archivo contiene todos los cambios de hello sobre toobe exportado.
5. Realice los cambios necesarios de hello toohello datos o configuración y ejecute estos pasos nuevo (importación, sincronizar y compruebe) hasta Hola cambios que tienen aproximadamente toobe exportar son los esperados.

Cuando esté satisfecho, exportar Hola cambios tooAzure AD.

1. Seleccione **Conectores**. Hola **conectores** seleccione Hola conector de Azure AD. En **Acciones**, seleccione **Ejecutar**.
2. En **Run profiles** (Perfiles de ejecución), seleccione **Exportar**.
3. Si eliminan muchos objetos a los cambios de configuración, a continuación, verá un error en la exportación de hello al número hello es mayor que el umbral de hello configurado (de forma predeterminada en 500). Si ve este error, deberá tootemporarily disable Hola "[evitar eliminaciones accidentales](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)" característica.

Ahora es el nuevo programador de hello tooenable de tiempo.

1. Iniciar **programador de tareas** de hello **iniciar** menú.
2. Directamente en **biblioteca del programador de tareas**, tarea de Hola de búsqueda denominada **Azure AD Sync Scheduler**, menú contextual y seleccione **habilitar**.

## <a name="group-based-filtering"></a>Filtrado basado en grupo
Puede configurar Hola filtrado basado en grupos de primera vez que se instala Azure AD Connect con [instalación personalizada](active-directory-aadconnect-get-started-custom.md#sync-filtering-based-on-groups). Su destinados a una implementación piloto donde desea que solo un pequeño conjunto de toobe objetos sincronizado. Cuando deshabilite el filtrado por grupo, no lo podrá volver a habilitar. Tiene *no admite* toouse filtrado en una configuración personalizada basada en grupos. Solo ha admite tooconfigure esta característica utilizando el Asistente para la instalación de Hola. Cuando haya completado la prueba piloto, a continuación, utilice uno de hello otras opciones de filtrado en este tema. Cuando se utiliza OU filtrado junto con el filtrado basado en grupos, se debe incluir Hola unidades organizativas donde se encuentran grupo hello y sus miembros.

Al sincronizar varios bosques de AD, puede configurar el filtrado basado en grupos mediante la especificación de un grupo diferente para cada conector de AD. Si desea toosynchronize un usuario en un bosque de AD y hello mismo usuario tiene uno o más correspondiente FSP (entidad de seguridad externa) objetos en otros bosques de AD, debe asegurarse de ese objeto de usuario de Hola y sus correspondientes objetos FSP están dentro de basado en grupos filtrar el ámbito. Si uno o varios objetos FSP Hola se excluyen mediante el filtrado basado en el grupo, el objeto de usuario de hello no estará sincronizada tooAzure AD.

## <a name="next-steps"></a>Pasos siguientes
- Más información sobre la configuración de la [Sincronización de Azure AD Connect](active-directory-aadconnectsync-whatis.md).
- Más información sobre la [integración de las identidades locales con Azure AD](active-directory-aadconnect.md).
