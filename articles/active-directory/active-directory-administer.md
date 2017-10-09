---
title: "aaaHow toouse una introducción a Azure Active Direcory inquilino directory | Documentos de Microsoft"
description: "Explica qué es un inquilino de Azure AD y cómo toomanage Azure con Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Administración del directorio de Azure AD

## <a name="what-is-an-azure-ad-tenant"></a>¿Qué es un inquilino de Azure AD?
En Azure Active Directory (Azure AD), un inquilino es una instancia dedicada de un directorio de Azure AD que su organización recibe cuando se suscribe a un servicio en la nube de Microsoft, como Azure u Office 365. Cada directorio de Azure AD es distinto e independiente de otros directorios de Azure AD. Al igual que un edificio de oficinas corporativos es un tooonly específico activo seguro su organización, un directorio de Azure AD también fue diseñado toobe un activo seguro para su uso únicamente por su organización. Hola arquitectura de Azure AD aísla la información de datos y la identidad del cliente para que los usuarios y administradores de un directorio de Azure AD no accidental o malintencionada tener acceso a datos en otro directorio.

![Administración de Azure Active Directory](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>¿Cómo puedo obtener un directorio de Azure AD?
Azure AD proporciona identidad y directorio principal de hello capacidades de administración detrás de la mayoría de servicios de nube de Microsoft, incluidos:

* Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Al suscribirse en cualquiera de estos servicios en la nube de Microsoft, obtiene un directorio de Azure AD. Puede crear directorios adicionales según sea necesario. Por ejemplo, puede mantener el primer directorio como directorio de producción y, a continuación, crear otro directorio para pruebas o ensayos.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>Utilizando el directorio de Azure AD de Hola que viene con una nueva suscripción de Azure

Se recomienda utilizar cuenta de administrador de Hola que usó para su primer servicio al registrarse para obtener otros servicios de Microsoft. información que proporcione Hola Hola primera vez que se registra para un servicio de Microsoft es toocreate usa un nuevo Azure instancia de directorio de AD para su organización. Si usas que el inicio de sesión de directory tooauthenticate intentos cuando se suscriben a los servicios de Microsoft tooother, pueden utilizar Hola cuentas de usuario existentes, las directivas, las configuraciones o integración de directorio local que configure en el directorio predeterminado.

Por ejemplo, si el inicio de sesión para una suscripción de Microsoft Intune y, después, sincronizar su Active Directory local con su directorio Azure AD, puede suscribirse a otro servicio de Microsoft como Office 365 y lograr fácilmente Hola mismo directorio ventajas de integración que tenga con Microsoft Intune.

Para más información acerca de cómo integrar su directorio local con Azure AD, consulte [Integración de directorios con Azure AD Connect](active-directory-aadconnect.md).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Asociación de un directorio existente de Azure AD con una nueva suscripción de Azure
Puede asociar una nueva suscripción a Azure con hello mismo directorio que autentica el inicio de sesión de para una suscripción de Office 365 o Microsoft Intune existente. Para obtener más información sobre ese escenario, consulte [transferir la propiedad de una cuenta de tooanother de suscripción de Azure](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Creación de un directorio de Azure AD mediante una suscripción a un servicio en la nube de Microsoft como una organización
Si aún no tiene un servicio de nube de Microsoft tooa de suscripción, puede usar uno de hello seguimiento vínculos toosign una. Con la suscripción a su primer servicio se crea un directorio de Azure AD automáticamente.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>¿Cómo toochange Hola directorio predeterminado para una suscripción

1. Inicie sesión en toohello [centro de cuentas de Azure](https://account.windowsazure.com/Home/Index) con una cuenta que es administrador de la cuenta de la propiedad de la suscripción para la suscripción hello tootransfer hello.
2. Asegúrese de ese usuario Hola que quieran toobe propietario de la suscripción de Hola se encuentra en el directorio de Hola de destino.
3. Haga clic en **Transferir suscripción**.
4. Especifica al destinatario de Hola. destinatario de Hello recibe automáticamente un correo electrónico con un vínculo de aceptación.
5. destinatario de Hello hace clic en el vínculo de Hola y sigue las instrucciones de hello, incluidos introducir su información de pago. Cuando el destinatario de Hola se realiza correctamente, se transfiere suscripción Hola. 
6. Hello directorio predeterminado de suscripción de Hola se cambia el directorio toohello que Hola usuario tiene si la transferencia de propiedad de suscripción de hello es correcta.

### <a name="manage-hello-default-directory-in-azure"></a>Administrar el directorio predeterminado de hello en Azure
Al suscribirse a Azure, se asocia un directorio de Azure AD predeterminado a su suscripción. No hay ningún costo por el uso de Azure AD y los directorios son un recurso gratuito. Hay servicios de Azure AD de pago que se conceden bajo licencia aparte y proporcionan funcionalidad adicional, como la personalización de marca de empresa en el inicio de sesión y el restablecimiento de contraseña en modo autoservicio. También puede crear un dominio personalizado mediante un nombre DNS que usted posee en lugar del valor predeterminado de Hola *. dominio onmicrosoft.com.

## <a name="how-can-i-manage-directory-data"></a>¿Cómo puedo administrar datos de directorios?
tooadminister uno o más suscripciones de servicio de nube de Microsoft, puede usar hello [centro de administración de Azure AD](https://aad.portal.azure.com), Hola portal de cuentas de Microsoft Intune u Hola [centro de administración de Office 365](https://portal.office.com/) toomanage su datos de directorio de la organización. También puede usar [cmdlets de PowerShell de Azure Active Directory](https://docs.microsoft.com/powershell/azure/active-directory) toohelp administrar los datos almacenados en Azure AD.

Desde cualquiera de estos portales (o cmdlets), puede:

* Crear y administrar cuentas de usuario y grupo
* Administración de servicios en la nube relacionados para las suscripciones de su organización
* Configuración de la integración local con los servicios de autenticación e identidad de Azure AD

Centro de administración de Azure AD de Hello, centro de administración de Office 365, portal de cuentas de Microsoft Intune y Hola cmdlets de Azure AD leen y escriben tooa una sola instancia compartida de Azure AD que está asociado con el directorio de su organización. Cada una de esas herramientas actúa como una interfaz front-end que extrae o cambia la información del directorio.

Si cambia los datos de su organización mediante cualquiera de los portales de Hola o cmdlets mientras la sesión iniciada en el contexto de Hola de uno de estos servicios, cambios de hello también se muestran en hello otros portales Hola la próxima vez que inicie sesión. Estos datos se comparten a través de servicios de nube de hello Microsoft toowhich que suscribirse.

Por ejemplo, si utiliza Hola centro de administración de Office 365 tooblock inicio de sesión, un usuario que los bloques de acción Hola usuario iniciar sesión en tooany otro toowhich servicio suscrito su organización es actualmente. Si ve Hola misma cuenta de usuario en el portal de cuentas de Microsoft Intune hello, también verá dicho usuario Hola está bloqueado.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>¿Cómo puedo agregar y administrar varios directorios?
También puede [agregar un directorio de Azure AD en el portal de Azure hello](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Rellene la información de Hola y seleccione **crear**.

Puede administrar cada directorio como un recurso totalmente independiente: cada directorio es un recurso del mismo nivel con características completas y lógicamente independiente de otros directorios que administre; no hay ninguna relación principal-secundario entre los directorios. Esta independencia entre directorios incluye la independencia de recursos, la independencia administrativa y la independencia de sincronización.

* **Independencia de recursos**. Si crear o eliminar un recurso en un directorio, no tiene ningún impacto en los recursos en otro directorio, con la excepción parcial de Hola de usuarios externos. Si utiliza un dominio personalizado “contoso.com” con un directorio, este no se puede utilizar con ningún otro directorio. 
* **Independencia administrativa**.  Si un usuario no administrador del directorio "Contoso", crea un directorio de prueba denominado "Prueba":
  
  * los administradores de Hello del directorio "Contoso" no tienen ningún toodirectory privilegios administrativos directos 'Test' a menos que un administrador de "Prueba" específicamente les otorgue estos privilegios. Los administradores de "Contoso" pueden controlar acceso toodirectory 'Test' en virtud de su control de cuenta de usuario de Hola que creó "Prueba".
    
  * Si asigna o quitar un rol de administrador para un usuario en un directorio, cambio de hello no afecta a ningún rol de administrador que pueda tener en otro directorio.
* **Independencia de sincronización**. Puede configurar cada Azure AD independientemente inquilino datos tooget sincronizadas desde una herramienta de sincronización de directorio de instancia única hello Azure AD Connect.

A diferencia de otros recursos de Azure, los directorios no son recursos secundarios de una suscripción a Azure. Por lo que si se cancela o permite la tooexpire de suscripción de Azure, es posible tener acceso los datos de directorio mediante PowerShell de Azure AD, Hola API Graph de Azure u otras interfaces, como el centro de administración de hello Office 365. También puede asociar otra suscripción directory Hola.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Cómo tooprepare toodelete un directorio de Azure AD
Un administrador global puede eliminar un directorio de Azure AD desde el portal de Hola. Cuando se elimina un directorio, también se eliminan todos los recursos que se encuentran en el directorio de Hola. Compruebe que se no necesita Hola a directorio antes de eliminarlo.

> [!NOTE]
> Si el usuario de hello ha iniciado sesión con una cuenta profesional o educativa, usuario de hello no deben tratar de toodelete su directorio particular. Por ejemplo, si hello usuario ha iniciado sesión como joe@contoso.onmicrosoft.com, ese usuario no puede eliminar el directorio de Hola que tiene contoso.onmicrosoft.com como dominio predeterminado.

Azure AD necesita que ciertas condiciones son toodelete cumpla un directorio. Esto reduce el riesgo de que la eliminación de un directorio negativamente afecta a los usuarios o aplicaciones, como la capacidad de Hola de usuarios toosign en tooOffice 365 o tener acceso a recursos en Azure. Por ejemplo, si accidentalmente se elimina un directorio para una suscripción, a continuación, los usuarios no podrán acceder Hola recursos de Azure para esa suscripción.

se comprueba Hola condiciones siguientes:

* Hello solo usuario en el directorio de hello debe ser administrador global de hello, que es toodelete Hola directorio. Los demás usuarios deben eliminarse antes de poder eliminar el directorio de Hola. Si los usuarios se sincronizan de forma local, sincronización debe estar desactivada y los usuarios de hello deben eliminarse en el directorio en la nube hello mediante el uso de Hola portal de Azure o cmdlets de PowerShell de Azure. Hay no hay grupos de toodelete de requisito o contactos como contactos agregados desde el centro de administración de hello Office 365.
* No puede haber ninguna aplicación en el directorio de Hola. Todas las aplicaciones deben eliminarse antes de poder eliminar el directorio de Hola.
* Ningún proveedor de autenticación multifactor puede directory toohello vinculado.
* No puede haber ninguna suscripción para los servicios en línea de Microsoft, como Microsoft Azure, Office 365, o directorio Hola asociada a Azure AD Premium. Por ejemplo, si se ha creado un directorio predeterminado en Azure en su nombre, no puede eliminar este directorio si la suscripción a Azure aún se basa en este directorio para la autenticación. De igual forma, no puede eliminar un directorio si otro usuario le ha asociado una suscripción. 


## <a name="next-steps"></a>Pasos siguientes
* [Foro de Azure AD](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Foro de Multi-Factor Authentication de Azure](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Preguntas sobre Azure publicadas en Stack Overflow](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Asignación de roles de administrador en Azure AD](active-directory-assign-admin-roles.md)
