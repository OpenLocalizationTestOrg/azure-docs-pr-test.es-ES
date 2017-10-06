---
title: "Proxy de aplicación aaaTroubleshoot | Documentos de Microsoft"
description: "Cubre cómo tootroubleshoot errores en el Proxy de aplicación de Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 970caafb-40b8-483c-bb46-c8b032a4fb74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: d426708a2ee32da6674987b5794602ed984b06b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-application-proxy-problems-and-error-messages"></a>Solución de problemas y mensajes de error de Proxy de aplicación
Si se producen errores al obtener acceso a una aplicación publicada o al publicar aplicaciones, compruebe Hola después opciones toosee si el Proxy de aplicación de Microsoft Azure AD funciona correctamente:

* Hola abrir Servicios de Windows de la consola y compruebe que hello **conector del Proxy de aplicación de Microsoft AAD** servicio está habilitado y ejecutándose. Puede que también desee toolook en la página de propiedades de servicio de Proxy de aplicación hello, como se muestra en hello después de imagen:  
  ![Captura de pantalla de la ventana de propiedades del conector del proxy de aplicación de Microsoft AAD](./media/active-directory-application-proxy-troubleshoot/connectorproperties.png)
* Abra el Visor de eventos y busque eventos del conector del proxy de aplicación en **Registros de aplicaciones y servicios** > **Microsoft** >  **AadApplicationProxy** > **Conector** > **Administrador**.
* Si es necesario, registros más detallados están disponibles de manera [activar Hola registros de sesión de Proxy de aplicación conector](application-proxy-understand-connectors.md#under-the-hood).

Para obtener más información acerca de la herramienta de solución de problemas de hello Azure AD, consulte [solución de problemas de requisitos previos de herramienta toovalidate conector red](https://blogs.technet.microsoft.com/applicationproxyblog/2015/09/03/troubleshooting-tool-to-validate-connector-networking-prerequisites).

## <a name="hello-page-is-not-rendered-correctly"></a>página de Hello no se representa correctamente
Es posible que tenga problemas con la representación o el funcionamiento incorrecto de la aplicación, aunque no reciba ningún mensaje de error específico. Esto puede ocurrir si ha publicado la ruta de acceso de hello artículo, pero requiere la aplicación hello de contenido que existe fuera de dicha ruta de acceso.

Por ejemplo, si publica Hola ruta de acceso https://yourapp/app pero aplicación hello llama imágenes en https://yourapp/media, no representa. Asegúrese de que publica la aplicación hello mediante hello más alto nivel ruta de acceso necesita tooinclude todo el contenido relevante. En este ejemplo sería http://yourapp/.

Si cambia el contenido de tooinclude al que hace referencia de la ruta de acceso, pero sigue necesitando tooland de usuarios en un vínculo más profundo en la ruta de acceso de Hola, consulte Entrada de blog hello [vínculo derecho de Hola de configuración para las aplicaciones de Proxy de aplicación en el panel de acceso de hello Azure AD y aplicación de Office 365 Selector de](https://blogs.technet.microsoft.com/applicationproxyblog/2016/04/06/setting-the-right-link-for-application-proxy-applications-in-the-azure-ad-access-panel-and-office-365-app-launcher/).

## <a name="connector-errors"></a>Errores del conector

Hola de uso [herramienta de prueba de Azure AD aplicación Proxy conector puertos](https://aadap-portcheck.connectorporttest.msappproxy.net/) tooverify que el conector puede comunicarse con servicio de Proxy de aplicación Hola. Como mínimo, asegúrese de que región de EE. UU. Central de Hola y Hola región más cercana tooyou tienen todas las marcas de verificación verde. Además, cuantas más marcas de verificación verde haya, mayor resistencia habrá. 

Si se produce un error en el registro durante la instalación del Asistente para conector de hello, hay dos maneras de tooview motivo Hola error de Hola. Examine en el registro de eventos de hello en **aplicaciones y servicios Logs\Microsoft\AadApplicationProxy\Connector\Admin**, u Hola ejecución siguiente comando de Windows PowerShell:

    Get-EventLog application –source “Microsoft AAD Application Proxy Connector” –EntryType “Error” –Newest 1

Una vez que encuentre el error del conector de Hola Hola del registro de eventos, use esta tabla de problema de Hola de tooresolve errores comunes:

| Error | Pasos recomendados |
| ----- | ----------------- |
| Error de registro de conector: asegúrese de que ha habilitado el Proxy de aplicación Hola Portal de administración de Azure y que escribió correctamente el nombre de usuario de Active Directory y la contraseña. Error: 'Se han producido uno o más errores'. | Si cierra la ventana de registro de hello sin iniciar sesión en tooAzure AD, vuelva a ejecutar el Asistente del conector de Hola y registre Hola conector. <br><br> Si la ventana de registro de hello se abre y, a continuación, se cierra inmediatamente sin permitir toolog en, probablemente obtendrá este error. Este error se produce cuando hay un error de red en el sistema. Asegúrese de que es posible tooconnect desde un sitio Web público de explorador tooa y que Hola puertos estén abiertos como se especifica en [requisitos previos del Proxy de aplicación](active-directory-application-proxy-enable.md). |
| Borrar error se presenta en la ventana de registro de hello. No se puede continuar | Si ve este error y, a continuación, cierra la ventana hello, especificó Hola incorrecto username o password. Inténtelo de nuevo. |
| Error de registro de conector: asegúrese de que ha habilitado el Proxy de aplicación Hola Portal de administración de Azure y que escribió correctamente el nombre de usuario de Active Directory y la contraseña. Error: ' AADSTS50059: ninguna información de identificación del inquilino se encuentra en cualquier solicitud de Hola o implícita en ninguna proporcionado las credenciales y la búsqueda por servicio error URI principal. | Estamos toosign usando un Account de Microsoft y no a un dominio que forma parte del identificador de organización de hello del directorio de Hola que estamos tooaccess. Asegúrese de que dicho administrador hello es parte del programa Hola mismo nombre de dominio como dominio del inquilino hello, por ejemplo, si el dominio hello Azure AD es contoso.com, debe ser Hola, administrador admin@contoso.com. |
| No se pudo tooretrieve Hola directiva actual de ejecución para ejecutar scripts de PowerShell. | Si se produce un error en la instalación del conector de hello, compruebe toomake seguro de que la directiva de ejecución de PowerShell no está deshabilitado. <br><br>1. Hola abrir Editor de directivas de grupo.<br>2. Vaya demasiado**configuración del equipo** > **plantillas administrativas** > **componentes de Windows**  >   **Windows PowerShell** y haga doble clic en **activar la ejecución del Script**.<br>3. directiva de ejecución Hola se puede establecer tooeither **no configurado** o **habilitado**. Si establece demasiado**habilitado**, asegúrese de que en las opciones, Hola directiva de ejecución se establece tooeither **permitir scripts locales y scripts remotos firmados** o demasiado**permitir que todos los scripts**. |
| Conector no pudo configuración de hello toodownload. | certificado de cliente del conector de Hello, que se utiliza para la autenticación, expirado. También puede producirse si tiene Hola que conector instalado detrás de un proxy. En este caso, Hola conector no tiene acceso a Internet de hello y no será capaz de tooprovide aplicaciones tooremote a los usuarios. Renueve la confianza manualmente mediante hello `Register-AppProxyConnector` cmdlet de Windows PowerShell. Si el conector está detrás de un servidor proxy, es necesario toogrant Internet access toohello conector cuentas "servicios de red" y "sistema local". Esto puede realizarse mediante la concesión de acceso toohello Proxy o estableciendo ellos toobypass Hola proxy. |
| Error de registro de conector: asegúrese de que sea un administrador Global de su Hola de tooregister conector de Active Directory. Error: "solicitud de registro de hello se ha denegado." | alias de Hola que intentas toolog con no es un administrador en este dominio. Siempre se instala el conector para el directorio de Hola que posee el dominio del usuario de Hola. Asegúrese de que está tratando de toosign sesión con la cuenta de administrador de hello tiene inquilino de Azure AD toohello permisos globales. |

## <a name="kerberos-errors"></a>Errores de Kerberos

Esta tabla recogen hello más comunes errores que proceden de la configuración de Kerberos y la configuración y se incluyen sugerencias para la resolución.

| Error | Pasos recomendados |
| ----- | ----------------- |
| No se pudo tooretrieve Hola directiva actual de ejecución para ejecutar scripts de PowerShell. | Si se produce un error en la instalación del conector de hello, compruebe toomake seguro de que la directiva de ejecución de PowerShell no está deshabilitado.<br><br>1. Hola abrir Editor de directivas de grupo.<br>2. Vaya demasiado**configuración del equipo** > **plantillas administrativas** > **componentes de Windows**  >   **Windows PowerShell** y haga doble clic en **activar la ejecución del Script**.<br>3. directiva de ejecución Hola se puede establecer tooeither **no configurado** o **habilitado**. Si establece demasiado**habilitado**, asegúrese de que en las opciones, Hola directiva de ejecución se establece tooeither **permitir scripts locales y scripts remotos firmados** o demasiado**permitir que todos los scripts**. |
| 12008 - azure AD superado Hola número máximo de autenticación de Kerberos permitidos intentos toohello servidor de back-end. | Este error puede indicar una configuración incorrecta entre Azure AD y Hola back-end de servidor de aplicaciones o un problema en la configuración de fecha y hora en ambos equipos. servidor de back-end de Hello rechazó el vale de Kerberos de hello creado por Azure AD. Compruebe que Azure AD y servidor de aplicaciones back-end de hello están configurados correctamente. Asegúrese de que configuración de fecha y hora de hello en hello Azure AD y el servidor de aplicaciones back-end de hello están sincronizadas. |
| 13016 - azure AD no puede recuperar un vale de Kerberos en nombre de usuario de hello porque no hay ningún UPN en edge Hola token o en cookie de acceso de Hola. | Hay un problema con la configuración de STS Hola. Corregir Hola notificación de UPN configuración Hola STS. |
| 13019 - azure AD no puede recuperar un vale de Kerberos en nombre de usuario de hello debido a Hola tras error general de API. | Este evento puede indicar una configuración incorrecta entre Azure AD y servidor de controlador de dominio de hello, o un problema en la configuración de fecha y hora en ambos equipos. controlador de dominio de Hello rechazó el vale de Kerberos de hello creado por Azure AD. Compruebe que Azure AD y servidor de aplicaciones back-end de hello están configurados correctamente, especialmente Hola SPN configuración. Asegúrese de que hello Azure AD está unido a un dominio toohello mismo dominio como Hola tooensure de controlador de dominio que Hola de controlador de dominio establece la confianza con Azure AD. Asegúrese de que configuración de fecha y hora de hello en hello Azure AD y el controlador de dominio de hello están sincronizadas. |
| 13020 - azure AD no puede recuperar un vale de Kerberos en nombre de usuario de hello porque no está definido el SPN del servidor de back-end de Hola. | Este evento puede indicar una configuración incorrecta entre Azure AD y servidor de controlador de dominio de hello, o un problema en la configuración de fecha y hora en ambos equipos. controlador de dominio de Hello rechazó el vale de Kerberos de hello creado por Azure AD. Compruebe que Azure AD y servidor de aplicaciones back-end de hello están configurados correctamente, especialmente Hola SPN configuración. Asegúrese de que hello Azure AD está unido a un dominio toohello mismo dominio como Hola tooensure de controlador de dominio que Hola de controlador de dominio establece la confianza con Azure AD. Asegúrese de que configuración de fecha y hora de hello en hello Azure AD y el controlador de dominio de hello están sincronizadas. |
| 13022 - azure AD no puede autenticar el usuario de hello porque el servidor back-end de hello responde tooKerberos los intentos de autenticación con un error HTTP 401. | Este evento puede indicar una configuración incorrecta entre Azure AD y Hola back-end de servidor de aplicaciones o un problema en la configuración de fecha y hora en ambos equipos. servidor de back-end de Hello rechazó el vale de Kerberos de hello creado por Azure AD. Compruebe que Azure AD y servidor de aplicaciones back-end de hello están configurados correctamente. Asegúrese de que configuración de fecha y hora de hello en hello Azure AD y el servidor de aplicaciones back-end de hello están sincronizadas. |

## <a name="end-user-errors"></a>Errores del usuario final

Esta lista muestran los errores que los usuarios finales pueden surgir cuando intentan tooaccess Hola aplicación y se producirá un error. 

| Error | Pasos recomendados |
| ----- | ----------------- |
| sitio Web de Hello no puede mostrar la página de Hola. | El usuario puede obtener este error al tratar de tooaccess Hola aplicación publicada si la aplicación hello es una aplicación IWA. Hola define un SPN para esta aplicación puede ser incorrecta. Para las aplicaciones IWA, asegúrese de que ese Hola SPN configurado para esta aplicación es correcto. |
| sitio Web de Hello no puede mostrar la página de Hola. | El usuario puede obtener este error al tratar de tooaccess Hola aplicación publicada si la aplicación hello es una aplicación de OWA. La causa puede ser uno de hello siguientes:<br><li>Hola define un SPN para esta aplicación es incorrecta. Asegúrese de que ese Hola SPN configurado para esta aplicación es correcto.</li><li>usuario de Hola que intentó aplicación hello de tooaccess está utilizando una cuenta de Microsoft, en lugar de hello toosign cuenta corporativa adecuada en, o usuario hello es un usuario invitado. Asegúrese de que Hola usuario inicia sesión con su cuenta corporativa que coincide con Hola dominio del programa Hola a la aplicación publicada. Los usuarios de cuenta Microsoft y los invitados no pueden tener acceso a aplicaciones IWA.</li><li>Hola usuarios intentaron aplicación hello de tooaccess no es correctamente definido por el usuario para esta aplicación Hola local. Asegúrese de que este usuario tiene los permisos adecuados de hello tal como se define para esta aplicación back-end en el equipo local de Hola. |
| No se puede tener acceso a esta aplicación corporativa. Se están tooaccess no autorizado en esta aplicación. Error de autorización. Asegúrese de usuario de hello tooassign seguro con la aplicación de access toothis. | Los usuarios pueden obtener este error al intentar tooaccess Hola aplicación publicada si usan cuentas de Microsoft en lugar de su toosign cuenta corporativa en. Los usuarios invitados también pueden recibir este error. Los usuarios y los invitados de la Cuenta Microsoft no pueden tener acceso a aplicaciones IWA. Asegúrese de que Hola usuario inicia sesión con su cuenta corporativa que coincide con Hola dominio del programa Hola a la aplicación publicada.<br><br>Puede que no haya asignado a usuario Hola para esta aplicación. Vaya toohello **aplicación** ficha y en **usuarios y grupos**, asigne este usuario o grupo toothis aplicación de usuario. |
| No se puede tener acceso a esta aplicación corporativa en este momento. Vuelva a intentarlo más tarde... conector Hola agotado el tiempo. | Los usuarios pueden obtener este error al intentar tooaccess Hola aplicación publicada si no se han definido correctamente para esta aplicación Hola local. Asegúrese de que los usuarios tienen los permisos adecuados de hello tal como se define para esta aplicación back-end en el equipo local de Hola. |
| No se puede tener acceso a esta aplicación corporativa. Se están tooaccess no autorizado en esta aplicación. Error de autorización. Asegúrese de que el usuario hello tiene una licencia de Azure Active Directory Premium o Basic. | Los usuarios pueden obtener este error al intentar tooaccess Hola aplicación publicada si no asignadas explícitamente con una licencia Premium o Basic administrador del suscriptor Hola. Vaya a Active Directory del suscriptor toohello **licencias** pestaña y asegúrese de que este usuario o grupo de usuarios se haya asignado una licencia Premium o Basic. |

## <a name="my-error-wasnt-listed-here"></a>Mi error no aparece aquí.

Si se produce un error o un problema con el Proxy de aplicación de Azure AD que no aparece en esta guía de solución de problemas, nos gustaría toohear sobre él. Enviar un correo electrónico tooour [equipo comentarios](mailto:aadapfeedback@microsoft.com) con detalles de Hola de ha encontrado un error Hola.

## <a name="see-also"></a>Otras referencias
* [Habilitación del proxy de aplicación de Azure Active Directory](active-directory-application-proxy-enable.md)
* [Publicar aplicaciones con Proxy de aplicación](active-directory-application-proxy-publish.md)
* [Habilitar el inicio de sesión único](active-directory-application-proxy-sso-using-kcd.md)
* [Habilitar el acceso condicional](active-directory-application-proxy-conditional-access.md)


<!--Image references-->
[1]: ./media/active-directory-application-proxy-troubleshoot/connectorproperties.png
[2]: ./media/active-directory-application-proxy-troubleshoot/sessionlog.png
