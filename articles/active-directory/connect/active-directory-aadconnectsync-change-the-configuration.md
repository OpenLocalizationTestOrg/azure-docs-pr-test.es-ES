---
title: "Sincronización de Azure AD Connect: cambio en la configuración de la sincronización de Azure AD Connect | Microsoft Docs"
description: "Le guía a través de toomake una toohello cambiar la configuración en Azure AD Connect de la sincronización."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 7b9df836-e8a5-4228-97da-2faec9238b31
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 78e96d9166831a668439c2b8aa6a0022bc472da4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomake-a-change-toohello-default-configuration"></a>Azure AD Connect sync: cómo toomake una toohello de cambio de configuración predeterminados
Hola de este tema sirve toowalk mostrarle cómo toomake cambia la configuración predeterminada de toohello en la sincronización de Azure AD Connect. Proporciona las instrucciones para algunos escenarios comunes. Con este conocimiento, debe ser capaz de toomake algunos cambios sencillos tooyour posee configuración basada en sus propias reglas de negocios.

## <a name="synchronization-rules-editor"></a>Editor de reglas de sincronización
Hola Editor de reglas de sincronización es usado toosee y cambio Hola configuración predeterminada que. Puede encontrarla en hello menú Inicio en hello **Azure AD Connect** grupo.  
![Menú Inicio con el Editor de reglas de sincronización](./media/active-directory-aadconnectsync-change-the-configuration/startmenu2.png)

Cuando lo abra, vea las reglas de hello predeterminadas out-of-box.

![Editor de reglas de sincronización](./media/active-directory-aadconnectsync-change-the-configuration/sre2.png)

### <a name="navigating-in-hello-editor"></a>Navegar en el editor de Hola
Hola listas desplegables en parte superior de hello del editor de hello le permiten buscar tooquickly una regla determinada. Por ejemplo, si desea que las reglas de hello toosee donde se incluye Hola atributo proxyAddresses, cambiaría Hola listas desplegables toohello a continuación:  
![Filtrado SRE](./media/active-directory-aadconnectsync-change-the-configuration/filtering.png)  
filtrado de tooreset y carga una configuración nueva, presione **F5** teclado Hola.

toohello superior derecha, tiene un botón **agregar nueva regla**. Este botón está toocreate usa su propia regla personalizada.

En la parte inferior de hello, tiene botones para actuar en una regla de sincronización seleccionado. Los botones **Edit** (Editar) y **Delete** (Eliminar) hacen lo que espera de ellos. **Exportar** genera un script de PowerShell para volver a crear la regla de sincronización Hola. Este procedimiento permite toomove una regla de sincronización de tooanother de un servidor.

## <a name="create-your-first-custom-rule"></a>Creación de su primera regla personalizada
cambio más frecuente de Hello es flujos de atributo de toohello de cambios. datos de Hello en el directorio de origen podrían no ser como en Azure AD. En el ejemplo de Hola en esta sección, desea toomake seguro Hola dado nombre de un usuario siempre está en **mayúsculas o minúsculas**.

### <a name="disable-hello-scheduler"></a>Deshabilite al programador de Hola
Hola [programador](active-directory-aadconnectsync-feature-scheduler.md) se ejecuta cada 30 minutos de forma predeterminada. Desea toomake seguro de que no se está iniciando mientras está realizando cambios y solucionar problemas de las reglas de nuevo. tootemporarily deshabilitar programador hello, inicie PowerShell y ejecute`Set-ADSyncScheduler -SyncCycleEnabled $false`

![Deshabilite al programador de Hola](./media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)  

### <a name="create-hello-rule"></a>Crear regla de Hola
1. Haga clic en **Agregar nueva regla**.
2. En hello **descripción** página escriba siguiente de hello:  
   ![Regla de filtrado de entrada](./media/active-directory-aadconnectsync-change-the-configuration/description2.png)  
   * Nombre: Escriba un nombre descriptivo de regla de Hola.
   * Descripción: Alguna aclaración para que otra persona puede sepan qué regla hello es para.
   * Conectado sistema: objeto de Hola Hola sistema se encuentra en. En este caso, seleccione Hola conector de Active Directory.
   * Connected System/Metaverse Object Type (Sistema conectado/Tipo de objeto de metaverso): seleccione **User** y **Person**, respectivamente.
   * Tipo de vínculo: Cambiar este valor también**unir**.
   * Prioridad: Proporcionar un valor que sea único en el sistema de Hola. Un valor numérico inferior indica una mayor prioridad.
   * Tag (Etiqueta): deje este campo en blanco. Solo las reglas de serie de Microsoft tienen esta casilla rellena con un valor.
3. En hello **filtro de ámbito** escriba **givenName ISNOTNULL**.  
   ![Filtro del ámbito de la regla entrada](./media/active-directory-aadconnectsync-change-the-configuration/scopingfilter.png)  
   Esta sección es toodefine utilizado debería aplicarse qué regla Hola de objetos. Si se deja vacío, regla de hello aplicaría tooall objetos de usuario. Pero también incluiría a salas de conferencias, cuentas de servicio y otros objetos de usuario que no son personas.
4. En hello **reglas de unión**, déjelo en blanco.
5. En hello **transformaciones** página, cambie hello FlowType demasiado**expresión**. Seleccione Hola atributo Target **givenName**y en el código fuente escriba `PCase([givenName])`.
   ![Transformaciones de la regla de entrada](./media/active-directory-aadconnectsync-change-the-configuration/transformations.png)  
   motor de sincronización de Hello distingue mayúsculas de minúsculas tanto en el nombre de hello del atributo de Hola y nombre de la función de Hola. Si escribe algún error, verá una advertencia al agregar regla de Hola. editor de Hello permite toosave y continuar, por lo que deberá tooreopen regla de Hola y regla de hello correcto.
6. Haga clic en **agregar** regla de toosave Hola.

La nueva regla personalizada debe estar visible con hello otra reglas de sincronización en el sistema de Hola.

### <a name="verify-hello-change"></a>Comprobar el cambio de Hola
Con este cambio nuevo, se desea toomake seguro de funciona según lo previsto y no está produciendo errores. Función número de Hola de objetos que tiene, hay toodo de dos maneras diferentes este paso.

1. Ejecute una sincronización completa en todos los objetos.
2. Ejecute una vista previa y una sincronización completa en un solo objeto.

Iniciar **servicio de sincronización de** desde el menú de inicio de Hola. pasos de Hello en esta sección están en esta herramienta.

1. **Sincronización completa en todos los objetos**  
   Seleccione **conectores** en la parte superior de Hola. Identificar Hola conector que ha realizado una sección anterior de cambio tooin hello, en este caso Hola los servicios de dominio de Active Directory y selecciónelo. Seleccione **Ejecutar** en Acciones y seleccione **Sincronización completa** y **Aceptar**.
   ![Sincronización completa](./media/active-directory-aadconnectsync-change-the-configuration/fullsync.png)  
   objetos de Hello ahora se actualizan en el metaverso Hola. Ahora desea toolook objeto Hola Hola metaverso.
2. **Vista previa y sincronización completa en un solo objeto**  
   Seleccione **conectores** en la parte superior de Hola. Identificar Hola conector que ha realizado una sección anterior de cambio tooin hello, en este caso Hola los servicios de dominio de Active Directory y selecciónelo. Seleccione **Search Connector Space**(Buscar espacio de conector). Use el ámbito toofind un objeto que desea cambiar de toouse tootest Hola. Seleccione el objeto de Hola y haga clic en **vista previa**. En la nueva pantalla de bienvenida, seleccione **confirmar Preview**.  
   ![Commit preview](./media/active-directory-aadconnectsync-change-the-configuration/commitpreview.png)  
   cambio de Hello ahora es confirmada toohello metaverso.

**Ver objeto Hola Hola metaverso**  
Ahora desea toopick que se espera unos ejemplo objetos toomake que Hola el valor y aplique esa regla Hola. Seleccione **búsqueda de metaverso** desde la parte superior de Hola. Agregue cualquier filtro que necesita objetos relevantes de toofind Hola. Hola resultados de búsqueda, abra un objeto. Ver valores de atributo de Hola y compruebe también en hello **reglas de sincronización** columna que Hola regla aplicada según lo previsto.  
![Metaverse search](./media/active-directory-aadconnectsync-change-the-configuration/mvsearch.png)  

### <a name="enable-hello-scheduler"></a>Habilitar el programador de Hola
Si todo está como se esperaba, puede habilitar al programador de Hola de nuevo. En PowerShell, ejecute `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="other-common-attribute-flow-changes"></a>Otros cambios de flujo de atributo comunes
sección de Hello anterior describe cómo toomake cambia el flujo de atributo tooan. En esta sección, se proporcionan algunos ejemplos adicionales. pasos de Hola para cómo se abrevia la regla de sincronización de hello toocreate, pero se pueden encontrar pasos completos de hello en la sección anterior de Hola.

### <a name="use-another-attribute-than-hello-default"></a>Usar otro atributo predeterminado de Hola
De Fabrikam, hay un bosque donde se usa el alfabeto local hello para el nombre especificado, el apellido y el nombre para mostrar. Hola representación de caracteres latinos de estos atributos se puede encontrar en atributos de extensión de Hola. Al generar la lista global de direcciones de hello en Azure AD y Office 365, Hola organización quiere que estas toobe de atributos que se usa en su lugar.

Con una configuración predeterminada, un objeto de bosque local hello tiene el siguiente aspecto:  
![Flujo de atributos 1](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp1.png)

Hola toocreate una regla con otros flujos de atributo siguientes:

* Iniciar **Editor de reglas de sincronización** desde el menú de inicio de Hola.
* Con **entrada** toohello aún seleccionado izquierdo, haga clic en el botón de hello **agregar nueva regla**.
* Asigne a Hola regla un nombre y una descripción. Seleccionar tipos de objeto pertinente hello y Active Directory local de Hola. En **Tipo de vínculo**, seleccione **Unir**. Para establecer la precedencia, seleccione un número que no se use en otra regla. reglas de out-of-box Hola iniciar con 100, para que el valor de hello 50 se puedan utilizar en este ejemplo.
  ![Flujo de atributos 2](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp2.png)
* Salga del ámbito vacía (es decir, debe aplicar tooall objetos de usuario en el bosque de hello).
* Deje las reglas de unión vacías (que es, permiten Hola cualquier combinación de identificador de regla de out-of-box).
* En las transformaciones, crear Hola después flujos:  
  ![Flujo de atributos 3](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp3.png)
* Haga clic en **agregar** regla de toosave Hola.
* Vaya demasiado**Synchronization Service Manager**. En **conectores**, seleccione Hola conector que agregamos regla Hola. Seleccione **Ejecutar** y **Sincronización completa**. Una sincronización completa vuelve a calcular todos los objetos mediante las reglas actuales de Hola.

Esto es resultado de hello para hello mismo objetos con esta regla personalizada:  
![Flujo de atributos 4](./media/active-directory-aadconnectsync-change-the-configuration/attributeflowjp4.png)

### <a name="length-of-attributes"></a>Longitud de los atributos
Atributos de la cadena son predeterminado conjunto toobe indizables y longitud máxima de hello es 448 caracteres. Si está trabajando con atributos de cadena que podrían contener más, a continuación, realice siguiente de hello tooinclude seguro en el flujo de atributo hello:  
`attributeName` <- `Left([attributeName],448)`

### <a name="changing-hello-userprincipalsuffix"></a>Cambiar userPrincipalSuffix Hola
atributo userPrincipalName de Hello en Active Directory no siempre se conoce por los usuarios de Hola y podría no ser adecuado tal y como Hola identificador de inicio de sesión. Hello Azure AD Connect Asistente para la instalación de sincronización permite seleccionar un atributo diferente, por ejemplo correo. Pero en algunos Hola casos debe calcularse el atributo. Por ejemplo, la empresa Hola Contoso tiene dos directorios de Azure AD, uno para producción y otro para las pruebas. Desean que los usuarios de hello en su prueba de inquilinos toouse otro sufijo Hola inicio de sesión del Id.  
`userPrincipalName` <- `Word([userPrincipalName],1,"@") & "@contosotest.com"`

En esta expresión, tienen todo lo que deja de hello primero @-sign (Word) y concatenar con una cadena fija.

### <a name="convert-a-multi-value-tooa-single-value"></a>Convertir un valor único de valores múltiples tooa
Algunos atributos de Active Directory son con varios valores en el esquema de hello Aunque parezcan únicos con valores en equipos y usuarios de Active Directory. Un ejemplo es el atributo de descripción de Hola.  
`description` <- `IIF(IsNullOrEmpty([description]),NULL,Left(Trim(Item([description],1)),448))`

En esta expresión en caso de atributo de hello tiene un valor, tomar Hola primer elemento () en el atributo hello, quite a la izquierda espacios iniciales y finales (Trim) y, a continuación, mantener Hola primeros 448 caracteres (izquierda) en la cadena de Hola.

### <a name="do-not-flow-an-attribute"></a>No pasar atributos
Para obtener información sobre el escenario de Hola para esta sección, vea [controlar el proceso de flujo de atributo de hello](active-directory-aadconnectsync-understanding-declarative-provisioning.md#control-the-attribute-flow-process).

Hay dos maneras de toonot flujo de un atributo. Hola en primer lugar está disponible en el Asistente para la instalación de Hola y permite demasiado[quitar atributos seleccionados](active-directory-aadconnect-get-started-custom.md#azure-ad-app-and-attribute-filtering). Esta opción funciona si nunca ha sincronizado atributo Hola antes. Sin embargo, si se han iniciado toosynchronize este atributo y eliminarlo más tarde con esta característica, motor de sincronización de hello deja de administrar atributo hello y se mantienen los valores existentes de hello en Azure AD.

Si desea tooremove Hola valor de un atributo y asegúrese de que no se extiende en hello futuras, necesita crear una regla personalizada en su lugar.

De Fabrikam, nos hemos dimos cuenta que algunos Hola atributos se sincronizar toohello en la nube no deberían estar allí. Queremos toomake seguro de que estos atributos se eliminan de Azure AD.  
![Atributos de extensión incorrecta](./media/active-directory-aadconnectsync-change-the-configuration/badextensionattribute.png)

* Crear una nueva regla de sincronización de entrada y rellenar descripción hello ![descripciones](./media/active-directory-aadconnectsync-change-the-configuration/syncruledescription.png)
* Crear flujos de atributo de tipo **expresión** y con el origen de hello **AuthoritativeNull**. Hola literal **AuthoritativeNull** indica que el valor de Hola debería estar vacía en hello MV incluso si el valor de hello toopopulate trata de una regla de sincronización de prioridad inferior.
  ![Transformación de atributos de extensión](./media/active-directory-aadconnectsync-change-the-configuration/syncruletransformations.png)
* Guardar Hola la regla de sincronización. Iniciar **servicio de sincronización de**, encontrar Hola conector, seleccione **ejecutar**, y **sincronización completa**. Este paso vuelve a calcular todos los flujos de atributo.
* Comprobar que Hola dirigido cambios va toobe exportado mediante la búsqueda de espacio de conector de Hola.
  ![Eliminación por fases](./media/active-directory-aadconnectsync-change-the-configuration/deletetobeexported.png)

## <a name="create-rules-with-powershell"></a>Creación de reglas con PowerShell
Usar el editor de reglas de sincronización de hello funciona bien si solo tiene unos toomake de cambios. Si necesita toomake muchos cambios, PowerShell podría ser una mejor opción. Algunas características avanzadas solo están disponibles con PowerShell.

### <a name="get-hello-powershell-script-for-an-out-of-box-rule"></a>Obtener script de PowerShell de Hola para una regla de out-of-box
Hola toosee script de PowerShell que ha creado una regla de out-of-box, una regla de hello select en la sincronización de Hola de reglas de editor y haga clic en **exportar**. Esto deja de acción Hola PowerShell script esa regla Hola creado.

### <a name="advanced-precedence"></a>Precedencia avanzada
las reglas de sincronización de out-of-box Hola comienzan con un valor de prioridad de 100. Si tiene varios bosques y necesita toomake muchos cambios personalizados, a continuación, reglas de sincronización 99 podrían no ser suficiente.

Puede indicar el motor de sincronización que desee reglas adicionales que se insertan antes que las reglas de out-of-box Hola Hola. tooget este comportamiento, siga estos pasos:

1. Marca Hola primera sincronización de out-of-box regla (esta regla es hello **en desde AD-User Join**) en el editor de reglas de sincronización de Hola y seleccione **exportar**. Copiar valor de identificador de SR Hola.  
![PowerShell antes del cambio](./media/active-directory-aadconnectsync-change-the-configuration/powershell1.png)  
2. Crear nueva regla de sincronización Hola. Puede utilizar toocreate de editor de reglas de sincronización de Hola. Exportar el script de PowerShell de hello regla tooa.
3. En la propiedad de hello **PrecedenceBefore**, insertar el valor de identificador de Hola de regla de out-of-box Hola. Conjunto hello **prioridad** demasiado**0**. Asegúrese de que el atributo del identificador hello es único y no se reutiliza un GUID a partir de otra regla. Asegúrese también de que ese hello **ImmutableTag** propiedad no está establecida; esta propiedad sólo debe establecerse para una regla de out-of-box. Guardar script de PowerShell de Hola y ejecútelo. resultado de Hello es que la regla personalizada se asigna el valor de prioridad de Hola de 100 y se incrementan las demás reglas de out-of-box.  
![PowerShell después del cambio](./media/active-directory-aadconnectsync-change-the-configuration/powershell2.png)  

Puede tener muchas reglas de sincronización personalizadas con Hola mismo **PrecedenceBefore** valor cuando sea necesario.


## <a name="enable-synchronization-of-preferreddatalocation"></a>Habilitar la sincronización de PreferredDataLocation
Connect de Azure AD admite la sincronización de hello **PreferredDataLocation** atributo **usuario** objetos en la versión 1.1.524.0 y después. Más concretamente, se introdujeron los cambios siguientes:

* esquema de Hola Hola del tipo de objeto **usuario** en hello conector de Azure AD se extiende tooinclude PreferredDataLocation atributo, que es de tipo cadena y tiene un solo valor.

* esquema de Hola Hola del tipo de objeto **persona** en hello metaverso se extiende tooinclude PreferredDataLocation atributo, que es de tipo cadena y tiene un solo valor.

De forma predeterminada, los hello PreferredDataLocation atributo no está habilitado para la sincronización porque no hay ningún atributo PreferredDataLocation correspondiente en la instancia local de Active Directory. Debe habilitar manualmente la sincronización.

> [!IMPORTANT]
> Actualmente, Azure AD permite atributo PreferredDataLocation de hello en los objetos de usuario y sin sincronizar nube toobe de objetos de usuario directamente configurado con Azure AD PowerShell. Una vez habilitada la sincronización del atributo de PreferredDataLocation hello, debe detener mediante PowerShell de Azure AD tooconfigure Hola atributo en **sincronizar objetos de usuario** como Azure AD Connect reemplazará a partir de valores de atributo de origen de Hello en local de Active Directory.

> [!IMPORTANT]
> En 1 de septiembre de 2017, Azure AD ya no permitirá atributo PreferredDataLocation de hello en **sincronizar objetos de usuario** toobe configurada directamente con Azure AD PowerShell. atributo de PreferredLocation tooconfigure en sincroniza objetos de usuario, debe usar Azure AD Connect solo.

Antes de habilitar la sincronización del atributo de PreferredDataLocation hello, debe:

 * En primer lugar, decida qué toobe de atributo de Active Directory local utilizado como atributo de origen de Hola. Debe ser de tipo **cadena** y **un solo valor**.

 * Si ha configurado previamente atributo PreferredDataLocation de hello en existente sincroniza objetos de usuario de Azure AD mediante Azure AD PowerShell, debe **Atrás** toohello correspondientes objetos de usuario de valores de atributo de Hola en Active Directory local.
 
    > [!IMPORTANT]
    > Si lo hace, no de atrás Hola atributo valores toohello correspondientes objetos de usuario en la instancia local de Active Directory, Azure AD Connect quitará los valores de atributo existentes de hello en Azure AD cuando la sincronización para el atributo de hello PreferredDataLocation es habilitado.

 * Se recomienda configurar el atributo de origen de hello en al menos un par de local AD los objetos de usuario ahora, que puede utilizarse para la comprobación posterior.
 
sincronización de Hello pasos tooenable del atributo de hello PreferredDataLocation se puede resumir como:

1. Deshabilitar el programador de sincronización y comprobar que no hay ninguna sincronización en curso

2. Agregar toohello de atributo de origen de hello conector AD local esquema

3. Agregar PreferredDataLocation toohello conector de Azure AD esquema

4. Crear un valor de atributo de sincronización de entrada regla tooflow Hola de local de Active Directory

5. Crear una sincronización de salida regla tooflow Hola atributo valor tooAzure AD

6. Iniciar el ciclo de sincronización completo

7. Habilitar el programador de sincronización

> [!NOTE]
> resto de Hola de esta sección trata estos pasos detalladamente. Se describen en el contexto de Hola de una implementación de Azure AD con topología de bosque único y sin reglas de sincronización personalizadas. Si tiene la topología de varios bosques, reglas de sincronización personalizadas configurada o tienen un servidor de ensayo, deberá pasos de hello tooadjust en consecuencia.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Paso 1: Deshabilitar el programador de sincronización y comprobar que no hay ninguna sincronización en curso
Asegúrese de que realiza ninguna sincronización mientras está en medio de Hola de sincronización de actualización cambia de tooavoid de reglas no deseada que se ha exportado tooAzure AD. Programador de sincronización integrada de Hola toodisable:

 1. Inicie sesión de PowerShell en el servidor de Azure AD Connect Hola.

 2. Deshabilite la sincronización programada mediante la ejecución del cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`
 
 3. Iniciar hello **Synchronization Service Manager** con va tooSTART → servicio de sincronización.
 
 4. Vaya toohello **Operations** pestaña y confirme que no hay ninguna operación cuyo estado sea *"en"curso.*

![Synchronization Service Manager: comprobar que no hay ninguna operación en curso](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step1.png)

### <a name="step-2-add-hello-source-attribute-toohello-on-premises-ad-connector-schema"></a>Paso 2: Agregar toohello de atributo de origen de hello conector AD local esquema
No todos los atributos de AD se importan en hello espacio de conector de AD local. tooadd Hola origen toohello lista de atributos Hola importado atributos:

 1. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.
 
 2. Haga doble clic en hello **conector de AD local** y seleccione **propiedades**.
 
 3. En el cuadro de diálogo emergente de hello, vaya toohello **seleccionar los atributos** ficha.
 
 4. Asegúrese de que el atributo de origen de Hola se comprueba en la lista de atributos de Hola.
 
 5. Haga clic en **Aceptar** toosave.

![Agregar origen de atributo tooon local esquema del conector de AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step2.png)

### <a name="step-3-add-preferreddatalocation-toohello-azure-ad-connector-schema"></a>Paso 3: Agregar esquema de PreferredDataLocation toohello conector de Azure AD
De forma predeterminada, el atributo de hello PreferredDataLocation no se importa en hello Azure AD Connect espacio. tooadd hello PreferredDataLocation atributo toohello lista de atributos importadas:

 1. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.

 2. Haga doble clic en hello **conector de Azure AD** y seleccione **propiedades**.

 3. En el cuadro de diálogo emergente de hello, vaya toohello **seleccionar los atributos** ficha.

 4. Asegúrese de que el atributo de hello PreferredDataLocation está activada en la lista de atributos de Hola.

 5. Haga clic en **Aceptar** toosave.

![Agregar el atributo de origen tooAzure esquema del conector de AD](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step3.png)

### <a name="step-4-create-an-inbound-synchronization-rule-tooflow-hello-attribute-value-from-on-premises-active-directory"></a>Paso 4: Crear un valor de atributo de sincronización de entrada regla tooflow Hola desde local de Active Directory
regla de sincronización de entrada de Hello permite tooflow de valor de atributo de Hola de atributo de origen de Hola de toohello de Active Directory local metaverso:

1. Iniciar hello **Editor de reglas de sincronización** con va tooSTART → Editor de reglas de sincronización.

2. Establecer filtro de búsqueda de hello **dirección** toobe **entrada**.

3. Haga clic en **agregar nueva regla** botón toocreate una nueva regla de entrada.

4. En hello **descripción** pestaña, proporcione la siguiente configuración de hello:
 
    | Atributo | Valor | Detalles |
    | --- | --- | --- |
    | Nombre | *Proporcione un nombre*. | Por ejemplo, *"In from AD – User PreferredDataLocation"* |
    | Descripción | *Proporcione una descripción* |  |
    | Sistema conectado | *Elegir Hola local conector de AD* |  |
    | Tipo de objeto de sistema conectado | **User** |  |
    | Propiedades de objeto de metaverso | **Person** |  |
    | Tipo de vínculo | **Join** |  |
    | Prioridad | *Elija un número entre 1 y 99* | El intervalo de 1 a 99 se reserva para las reglas de sincronización personalizadas. No elija ningún valor que use otra regla de sincronización. |

5. Vaya toohello **filtro de ámbito** pestaña y agregar un **grupo de filtro de ámbito único con hello tras cláusula**:
 
    | Atributo | operador | Valor |
    | --- | --- | --- |
    | adminDescription | NOTSTARTWITH | Usuario\_ | 
 
    El filtro de ámbito determina a qué objetos de AD locales se aplica esta regla de sincronización de entrada. En este ejemplo, utilizamos Hola mismo filtro de ámbito se usa como *"en desde AD – usuario Common"* regla de sincronización de OOB, lo que impide que la regla de sincronización de Hola que se va a aplicar los objetos de tooUser creados mediante la reescritura de usuarios de Azure AD característica. Puede que necesite los filtro de ámbito de Hola de tootweak según tooyour implementación de Azure AD Connect.

6. Vaya toohello **ficha transformación** e implementar Hola siguiendo la regla de transformación:
 
    | Tipo de flujo | Atributo de destino | Origen | Aplicar una vez | Tipo de combinación |
    | --- | --- | --- | --- | --- |
    | Directo | PreferredDataLocation | Elegir el atributo de origen de Hola | No activado | Actualizar |

7. Haga clic en **agregar** regla de entrada de toocreate Hola.

![Crear regla de sincronización de entrada](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step4.png)

### <a name="step-5-create-an-outbound-synchronization-rule-tooflow-hello-attribute-value-tooazure-ad"></a>Paso 5: Crear una sincronización de salida regla tooflow Hola atributo valor tooAzure AD
regla de sincronización de salida de Hello permite tooflow de valor de atributo de hello del atributo de hello metaverso toohello PreferredDataLocation en Azure AD:

1. Vaya toohello **reglas de sincronización** Editor.

2. Establecer filtro de búsqueda de hello **dirección** toobe **saliente**.

3. Haga clic en el botón **Agregar nueva regla**.

4. En hello **descripción** pestaña, proporcione la siguiente configuración de hello:

    | Atributo | Valor | Detalles |
    | --- | --- | --- |
    | Nombre | *Proporcione un nombre*. | Por ejemplo, "Out" tooAAD: PreferredDataLocation de usuario" |
    | Descripción | *Proporcione una descripción* |
    | Sistema conectado | *Seleccione el conector AAD Hola* |
    | Tipo de objeto de sistema conectado | Usuario ||
    | Propiedades de objeto de metaverso | **Person** ||
    | Tipo de vínculo | **Join** ||
    | Prioridad | *Elija un número entre 1 y 99* | El intervalo de 1 a 99 se reserva para las reglas de sincronización personalizadas. No elija ningún valor que use otra regla de sincronización. |

5. Vaya toohello **filtro de ámbito** pestaña y agregar un **único grupo de ámbito de filtro con dos cláusulas**:
 
    | Atributo | operador | Valor |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Usuario |
    | cloudMastered | NOTEQUAL | True |

    El filtro de ámbito determina a qué objetos de Azure AD se aplica esta regla de sincronización de salida. En este ejemplo, utilizamos Hola mismo filtro de ámbito de "Out tooAD: identidad de usuario" regla de sincronización de OOB. Impide regla de sincronización de hello tooUser aplicado objetos que no se sincronizan desde la instancia local de Active Directory. Puede que necesite los filtro de ámbito de Hola de tootweak según tooyour implementación de Azure AD Connect.
    
6. Vaya toohello **transformación** pestaña e implementar Hola siguiendo la regla de transformación:

    | Tipo de flujo | Atributo de destino | Origen | Aplicar una vez | Tipo de combinación |
    | --- | --- | --- | --- | --- |
    | Directo | PreferredDataLocation | PreferredDataLocation | No activado | Actualizar |

7. Cerrar **agregar** regla de salida de hello toocreate.

![Crear regla de sincronización de salida](./media/active-directory-aadconnectsync-change-the-configuration/preferredDataLocation-step5.png)

### <a name="step-6-run-full-synchronization-cycle"></a>Paso 6: Ejecutar el ciclo de sincronización completo
En general, el ciclo de sincronización completa es necesario ya hemos agregado nuevas Hola de tooboth atributos AD y el esquema de conector de Azure AD e introdujo reglas de sincronización personalizadas. Se recomienda que compruebe los cambios de hello antes de exportarlos a tooAzure AD. Puede usar Hola tras cambios de pasos tooverify Hola mientras la ejecución manual de los pasos de Hola que forman un ciclo de sincronización completa. 

1. Ejecutar **importación completa** paso en hello **conector de AD local**:

   1. Vaya toohello **Operations** ficha Hola Synchronization Service Manager.

   2. Haga doble clic en hello **conector de AD local** y seleccione **ejecutar...**

   3. En el cuadro de diálogo emergente de hello, seleccione **importación completa** y haga clic en **Aceptar**.
    
   4. Espere a que toocomplete de operación.

    > [!NOTE]
    > Puede omitir la importación completa en hello AD conector local si el atributo de origen de hello ya está incluido en la lista de Hola de atributos importados. En otras palabras, no tenía toomake cualquier cambio durante la [paso 2: agregar toohello de atributo de origen de hello conector AD local esquema](#step-2-add-the-source-attribute-to-the-on-premises-ad-connector-schema).

2. Ejecutar **importación completa** paso en hello **conector de Azure AD**:

   1. Haga doble clic en hello **conector de Azure AD** y seleccione **ejecutar...**

   2. En el cuadro de diálogo emergente de hello, seleccione **importación completa** y haga clic en **Aceptar**.
   
   3. Espere a que toocomplete de operación.

3. Comprobar los cambios de regla de sincronización de hello en un objeto de usuario existente:

atributo de origen de Hola desde Active Directory y PreferredDataLocation de Azure AD se han importado en local Hola espacio de conector correspondiente. Antes de continuar con el paso de sincronización completa, se recomienda que realice un **vista previa** en un usuario existente objeto Hola local espacio de conector de AD. objeto Hola que ha seleccionado debe tener el atributo de origen de hello rellena. Una correcta **vista previa** con hello PreferredDataLocation rellenado en hello metaverso es un buen indicador que ha configurado correctamente las reglas de sincronización de Hola. Para obtener información acerca de cómo toodo una **vista previa**, consulte toosection [comprobar el cambio de hello](#verify-the-change).

4. Ejecutar **sincronización completa** paso en hello **conector de AD local**:

   1. Haga doble clic en hello **conector de AD local** y seleccione **ejecutar...**
  
   2. En el cuadro de diálogo emergente de hello, seleccione **sincronización completa** y haga clic en **Aceptar**.
   
   3. Espere a que toocomplete de operación.

5. Comprobar **exportaciones pendientes** tooAzure AD:

   1. Haga doble clic en hello **conector de Azure AD** y seleccione **espacio de conector de búsqueda**.

   2. En el cuadro de diálogo emergente de hello espacio de conector de búsqueda:

      1. Establecer **ámbito** demasiado**exportar pendiente**.
      
      2. Active las tres casillas, incluidas **Agregar, Modificar y Eliminar**.
      
      3. Haga clic en hello **búsqueda** lista de botones de hello tooget de objetos con toobe cambios exportado. cambios de hello tooexamine para un objeto determinado, haga doble clic en el objeto de Hola.
      
      4. Compruebe que se esperan que los cambios de Hola.

6. Ejecutar **exportar** paso en hello **conector de Azure AD**
      
   1. Menú contextual hello **conector de Azure AD** y seleccione **ejecutar...**
   
   2. En el cuadro de diálogo emergente de hello ejecutar conector, seleccione **exportar** y haga clic en **Aceptar**.
   
   3. Espere a que toocomplete tooAzure AD de exportación.

> [!NOTE]
> Puede que observe que Hola pasos no incluyen el paso de sincronización completa de Hola y el paso de exportación en hello conector de Azure AD. Hola pasos no son necesarios porque el fluyen de valores de atributo de Hola desde Active Directory tooAzure AD de local solo.

### <a name="step-7-re-enable-sync-scheduler"></a>Paso 7: Volver a habilitar el programador de sincronización
Volver a habilitar el programador de sincronización integrada de hello:

1. Inicie la sesión de PowerShell.

2. Vuelva a habilitar la sincronización programada mediante la ejecución del cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`



## <a name="next-steps"></a>Pasos siguientes
* Obtener más información acerca del modelo de configuración de hello en [aprovisionamiento declarativo de descripción](active-directory-aadconnectsync-understanding-declarative-provisioning.md).
* Obtener más información acerca del lenguaje de expresiones de hello en [descripción expresiones de aprovisionamiento declarativo](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md).

**Temas de introducción**

* [Sincronización de Azure AD Connect: comprender y personalizar la sincronización](active-directory-aadconnectsync-whatis.md)
* [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md)
