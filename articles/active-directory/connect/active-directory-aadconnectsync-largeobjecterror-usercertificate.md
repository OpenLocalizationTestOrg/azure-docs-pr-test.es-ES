---
title: 'Azure AD Connect Sync: control de errores LargeObject causados por el atributo userCertificate | Microsoft Docs'
description: "Este tema proporciona pasos de corrección de Hola para errores de LargeObject producidos por atributo userCertificate."
services: active-directory
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 146ad5b3-74d9-4a83-b9e8-0973a19828d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e547fb5f601b92f6f5154de9997651b1f28c51b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-handling-largeobject-errors-caused-by-usercertificate-attribute"></a>Azure AD Connect Sync: control de errores LargeObject causados por el atributo userCertificate

Azure AD impone un límite máximo de **15** certificado valores en hello **userCertificate** atributo. Si Azure AD Connect exporta un objeto con más de 15 valores tooAzure AD, Azure AD devuelve un **LargeObject** error con el mensaje:

>*"objeto aprovisionado hello es demasiado grande. Recorte el número de Hola de valores de atributo en este objeto. operación de Hola se reintentará en hello próximo ciclo de sincronización …"*

Hola LargeObject error puede deberse a otros atributos de AD. tooconfirm realmente está provocada por atributo userCertificate de hello, deberá tooverify con objeto de hello en AD local o en hello [búsqueda de metaverso Synchronization Service Manager](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-mvsearch).

lista de hello tooobtain de objetos en el inquilino con errores LargeObject, utilice uno de los siguientes métodos de hello:

 * Si está habilitado el inquilino de Azure AD Connect Health para la sincronización, puede consultar toohello [informe de errores de sincronización](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-sync#object-level-synchronization-error-report-preview) proporcionado.
 
 * Hola correo electrónico de notificación para los errores de sincronización de directorios que se envía al final de Hola de cada ciclo de sincronización tiene lista Hola de objetos con errores de LargeObject. 
 * Hola [ficha operaciones Synchronization Service Manager](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-service-manager-ui-operations) muestra la lista de Hola de objetos con errores de LargeObject si hace clic en la operación de hello más reciente exportación tooAzure AD.
 
## <a name="mitigation-options"></a>Opciones de mitigación
Hasta que se resuelva el error de hello LargeObject, otro toohello de cambios de atributo no puede ser el mismo objeto exportado tooAzure AD. error de hello tooresolve, puede considerar Hola siguientes opciones:

 * Actualizar Azure AD Connect toobuild 1.1.524.0 o después. En Azure AD Connect compilación 1.1.524.0, reglas de sincronización de out-of-box Hola han sido actualizados toonot exportación atributos userCertificate y userSMIMECertificate si los atributos de hello tienen más de 15 valores. Para obtener más información acerca de cómo tooupgrade Azure AD Connect, consulte tooarticle [Azure AD Connect: actualización de un toohello de versión anterior más reciente](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-upgrade-previous-version).

 * Implemente un **regla de sincronización de salida** en Azure AD Connect que exporta un **null el valor en lugar de valores reales de Hola para los objetos con valores de certificado de más de 15**. Esta opción es adecuada si no es necesario que cualquiera de hello certificado valores toobe exportar tooAzure AD objetos con valores de más de 15. Para obtener más información acerca de cómo tooimplement regla esta sincronización, consulte la sección toonext [exportación de toolimit de regla de sincronización de implementación del atributo userCertificate](#implementing-sync-rule-to-limit-export-of-usercertificate-attribute).

 * Reducir el número de Hola de valores de certificado en hello local objeto de AD (15 o menos) mediante la eliminación de los valores que ya no están en uso por su organización. Esto es conveniente si inundación de atributo Hola está causado por los certificados expirados o sin usar. Puede usar hello [aquí disponible del script de PowerShell](https://gallery.technet.microsoft.com/Remove-Expired-Certificates-0517e34f) buscar toohelp, copia de seguridad y eliminar certificados caducados en sus instalaciones en AD. Antes de eliminar los certificados de hello, se recomienda que compruebe con los administradores de infraestructura de clave pública de hello en su organización.

 * Configurar Azure AD Connect tooexclude Hola userCertificate atributo que se va a exporta tooAzure AD. En general, no se recomienda esta opción ya que pueden utilizar el atributo de hello escenarios específicos de Microsoft Online Services tooenable. En particular:
    * atributo userCertificate de Hola Hola objeto de usuario se usa por clientes de Outlook y Exchange Online para cifrado y firma de mensajes. toolearn más información acerca de esta característica, consulte tooarticle [S/MIME para firmar mensajes y cifrado](https://technet.microsoft.com/library/dn626158(v=exchg.150).aspx).

    * atributo userCertificate de Hello en objetos de equipo de Hola se usa por dispositivos Unidos a dominio tooconnect tooAzure AD de Azure AD tooallow 10 de Windows local. toolearn más información acerca de esta característica, consulte tooarticle [conectar dispositivos Unidos a dominio tooAzure AD para Windows 10 experimenta](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy).

## <a name="implementing-sync-rule-toolimit-export-of-usercertificate-attribute"></a>Implementación de exportación de toolimit de regla de sincronización del atributo userCertificate
tooresolve hello LargeObject error por un atributo userCertificate de hello, puede implementar una regla de sincronización de salida en Azure AD Connect que exporta un **un valor en lugar de valores reales de Hola para los objetos con valores de certificado de más de 15nulo**. Esta sección describe la regla de sincronización de Hola Hola pasos tooimplement necesarios para **usuario** objetos. Hello pasos se pueden adaptados para **póngase en contacto con** y **equipo** objetos.

> [!IMPORTANT]
> Exportar valor null quita certificado valores exportan previamente correctamente tooAzure AD.

Hola pasos se pueden resumir como:

1. Deshabilitar el programador de sincronización y comprobar que no hay ninguna sincronización en curso.
3. Buscar la regla de sincronización de salida existente de hello para el atributo userCertificate.
4. Crear regla de sincronización de salida de hello requerida.
5. Compruebe la nueva regla de sincronización hello en un objeto existente con el error LargeObject.
6. Aplicar Hola nueva regla tooremaining objetos de sincronización con el error LargeObject.
7. Comprobar que no hay ningún cambio inesperado espera toobe exportar tooAzure AD.
8. Exportar Hola cambios tooAzure AD.
9. Volver a habilitar el programador de sincronización.

### <a name="step-1-disable-sync-scheduler-and-verify-there-is-no-synchronization-in-progress"></a>Paso 1. Deshabilitar el programador de sincronización y comprobar que no hay ninguna sincronización en curso
Asegúrese de que realiza ninguna sincronización mientras está en medio de Hola de implementar una nueva sincronización cambia de regla tooavoid no deseada que se ha exportado tooAzure AD. Programador de sincronización integrada de Hola toodisable:
1. Inicie sesión de PowerShell en el servidor de Azure AD Connect Hola.

2. Deshabilite la sincronización programada mediante la ejecución del cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $false`

> [!Note]
> Hello pasos anteriores son sólo aplicables toonewer versiones (1.1.xxx.x) de Azure AD Connect con el programador integrado Hola. Si usa versiones anteriores (1.0.xxx.x) de Azure AD Connect que usa el programador de tareas de Windows, o que usa su propia sincronización periódica de tootrigger programador personalizado (no es común), necesita toodisable ellos según corresponda.

3. Iniciar hello **Synchronization Service Manager** con va tooSTART → servicio de sincronización.

4. Vaya toohello **Operations** pestaña y confirme que no hay ninguna operación cuyo estado sea *"en"curso.*

### <a name="step-2-find-hello-existing-outbound-sync-rule-for-usercertificate-attribute"></a>Paso 2: Buscar la regla de sincronización de salida existente de hello para el atributo userCertificate
Debería haber una regla de sincronización existente que está habilitada y configurada del atributo userCertificate tooexport tooAzure de objetos de usuario AD. Busque este toofind de regla de sincronización fuera su **prioridad** y **filtro de ámbito** configuración:

1. Iniciar hello **Editor de reglas de sincronización** con va tooSTART → Editor de reglas de sincronización.

2. Configurar filtros de búsqueda de hello con hello siguientes valores:

    | Atributo | Valor |
    | --- | --- |
    | Dirección |**Outbound** |
    | Tipo de objeto del metaverso |**Person** |
    | Conector |*nombre de su conector de Azure AD* |
    | Tipo de objeto de conector |**user** |
    | Atributos del metaverso |**userCertificate** |

3. Si usas el atributo OOB (out-of-box) sincronización rules tooAzure AD conector tooexport userCertficiate para objetos de usuario, debe regresar hello *"Out tooAAD – usuario ExchangeOnline"* regla.
4. Tome nota de hello **prioridad** valor de esta regla de sincronización.
5. Seleccione la regla de sincronización hello y haga clic en **editar**.
6. Hola *"Editar reservada Confirmation regla"* cuadro de diálogo emergente, haga clic en **No**. (No se preocupe, no vamos a toomake cualquier cambio de la regla de sincronización toothis).
7. En la pantalla de edición de bienvenida, seleccione hello **filtro de ámbito** ficha.
8. Anote la configuración del filtro de ámbito de Hola. Si usas la regla de sincronización OOB hello, debería exactamente haber **un grupo de filtro ámbito que contiene dos cláusulas**, incluido:

    | Atributo | operador | Valor |
    | --- | --- | --- |
    | sourceObjectType | EQUAL | Usuario |
    | cloudMastered | NOTEQUAL | True |

### <a name="step-3-create-hello-outbound-sync-rule-required"></a>Paso 3: Crear regla de sincronización de salida de hello requerida
Hello nueva regla de sincronización debe haber Hola mismo **filtro de ámbito** y **mayor precedencia** de Hola la regla de sincronización existente. Esto garantiza que esa nueva regla de sincronización Hola aplica toohello al mismo conjunto de objetos como regla de sincronización existente de Hola e invalidaciones Hola existente la regla de sincronización para el atributo userCertificate de Hola. regla de sincronización de Hola toocreate:
1. Hola Editor de reglas de sincronización, haga clic en hello **agregar nueva regla** botón.
2. En hello **ficha Descripción**, proporcionar Hola siguiente configuración:

    | Atributo | Valor | Detalles |
    | --- | --- | --- |
    | Nombre | *Proporcione un nombre*. | Por ejemplo, *"Out tooAAD – personalizado invalidar para userCertificate"* |
    | Descripción | *Proporcione una descripción* | Por ejemplo, *"Si el atributo userCertificate tiene más de 15 valores, la exportación es NULL".* |
    | Sistema conectado | *Seleccione Hola conector de Azure AD* |
    | Tipo de objeto de sistema conectado | **user** | |
    | Propiedades de objeto de metaverso | **person** | |
    | Tipo de vínculo | **Join** | |
    | Prioridad | *Elija un número entre 1 y 99* | no se debe usar en cualquier regla de sincronización existente Hello número elegido y tiene un valor inferior (y por lo tanto, mayor prioridad) de Hola la regla de sincronización existente. |

3. Vaya toohello **filtro de ámbito** pestaña e implementar Hola está usando el mismo ámbito filtro Hola sincronización regla existente.
4. Hola SKIP **reglas de unión** ficha.
5. Vaya toohello **transformaciones** ficha tooadd una nueva transformación realizada utilizando después de configuración:

    | Atributo | Valor |
    | --- | --- |
    | Tipo de flujo |**Expression** |
    | Atributo de destino |**userCertificate** |
    | Atributo de origen |*Hola de uso siguiente expresión*:`IIF(IsNullOrEmpty([userCertificate]), NULL, IIF((Count([userCertificate])> 15),AuthoritativeNull,[userCertificate]))` |
    
6. Haga clic en hello **agregar** regla de sincronización de botón toocreate Hola.

### <a name="step-4-verify-hello-new-sync-rule-on-an-existing-object-with-largeobject-error"></a>Paso 4 Comprobar la nueva regla de sincronización hello en un objeto existente con el error LargeObject
Se trata de tooverify que Hola sincronización regla creada funciona correctamente en un objeto de AD existente con el error LargeObject antes de aplicarla tooother objetos:
1. Vaya toohello **Operations** ficha Hola Synchronization Service Manager.
2. Seleccione hello más reciente exportación tooAzure AD operación y haga clic en uno de los objetos de hello con errores de LargeObject.
3.  En la pantalla emergente de propiedades de objeto del espacio de conector de bienvenida, haga clic en hello **vista previa** botón.
4. En la pantalla emergente de vista previa de bienvenida, seleccione **sincronización completa** y haga clic en **confirmar Preview**.
5. Cierre la pantalla de vista previa de bienvenida y la pantalla de propiedades del objeto de espacio de conector de bienvenida.
6. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.
7. Haga doble clic en hello **Azure AD** conector y seleccione **ejecutar...**
8. En el menú emergente de hello ejecutar conector, seleccione **exportar** paso a paso y haga clic en **Aceptar**.
9. Espere durante la exportación tooAzure AD toocomplete y confirmar que no hay ningún error LargeObject más en este objeto específico.

### <a name="step-5-apply-hello-new-sync-rule-tooremaining-objects-with-largeobject-error"></a>Paso 5. Aplicar Hola nueva regla tooremaining objetos de sincronización con el error LargeObject
Una vez que se ha agregado la regla de sincronización hello, deberá toorun un paso de sincronización completa en hello conector AD:
1. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.
2. Haga doble clic en hello **AD** conector y seleccione **ejecutar...**
3. En el menú emergente de hello ejecutar conector, seleccione **sincronización completa** paso a paso y haga clic en **Aceptar**.
4. Espere a que toocomplete de paso de sincronización completa de Hola.
5. Repita Hola por encima de los pasos para hello restantes conectores AD si tiene más de una conectores de AD. Normalmente, se necesitan varios conectores si tiene varios directorios locales.

### <a name="step-6-verify-there-are-no-unexpected-changes-waiting-toobe-exported-tooazure-ad"></a>Paso 6. Compruebe que no hay cambios inesperados toobe exportar tooAzure AD
1. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.
2. Haga doble clic en hello **Azure AD** conector y seleccione **espacio de conector de búsqueda**.
3. En la ventana emergente del espacio de conector de búsqueda de hello:
    1. Establecer el ámbito demasiado**exportar pendiente**.
    2. Active las tres casillas, incluidas **Add** (Agregar), **Modify** (Modificar) y **Delete** (Eliminar).
    3. Haga clic en **búsqueda** botón tooreturn todos los objetos que tienen cambios que esperan toobe exportar tooAzure AD.
    4. Compruebe que no hay cambios inesperados. cambios de hello tooexamine para un objeto determinado, haga doble clic en el objeto de Hola.

### <a name="step-7-export-hello-changes-tooazure-ad"></a>Paso 7. Exportar Hola cambios tooAzure AD
tooexport Hola cambios tooAzure AD:
1. Vaya toohello **conectores** ficha Hola Synchronization Service Manager.
2. Haga doble clic en hello **Azure AD** conector y seleccione **ejecutar...**
4. En el menú emergente de hello ejecutar conector, seleccione **exportar** paso a paso y haga clic en **Aceptar**.
5. Espere exportación tooAzure AD toocomplete y confirmar que no existen errores LargeObject más.

### <a name="step-8-re-enable-sync-scheduler"></a>Paso 8. Volver a habilitar el programador de sincronización
Ahora que se resuelve el problema de hello, volver a habilitar el programador de sincronización integrada de hello:
1. Inicie la sesión de PowerShell.
2. Vuelva a habilitar la sincronización programada mediante la ejecución del cmdlet: `Set-ADSyncScheduler -SyncCycleEnabled $true`

> [!Note]
> Hello pasos anteriores son sólo aplicables toonewer versiones (1.1.xxx.x) de Azure AD Connect con el programador integrado Hola. Si usa versiones anteriores (1.0.xxx.x) de Azure AD Connect que usa el programador de tareas de Windows, o que usa su propia sincronización periódica de tootrigger programador personalizado (no es común), necesita toodisable ellos según corresponda.

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre la [Integración de las identidades locales con Azure Active Directory](active-directory-aadconnect.md).

