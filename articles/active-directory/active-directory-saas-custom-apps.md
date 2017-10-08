---
title: aaaConfigure Azure AD SSO para aplicaciones | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooself servicio conectar aplicaciones tooAzure Active Directory mediante SAML y SSO basado en contraseña"
services: active-directory
author: asmalser-msft
documentationcenter: na
manager: femila
ms.assetid: 0d42eb0c-6d3f-4557-9030-e88e86709a19
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/20/2017
ms.author: asmalser
ms.reviewer: luleon
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 002a19a6c7ad25ea2f3b9c6a7c7874ed2be23cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-single-sign-on-tooapplications-that-are-not-in-hello-azure-active-directory-application-gallery"></a>Configurar tooapplications de inicio de sesión único que no están en la Galería de aplicaciones de Azure Active Directory Hola
Este artículo trata sobre una característica que permite a los administradores tooconfigure único inicio de sesión tooapplications no está en la Galería de aplicaciones de Azure Active Directory hello *sin escribir código*. Esta característica se ha publicado en Technical Preview el 18 de noviembre de 2015 y se incluye en [Azure Active Directory Premium](active-directory-editions.md). Si desea en su lugar para obtener una guía para desarrolladores sobre toointegrate aplicaciones personalizadas con Azure AD a través del código, consulte [escenarios de autenticación para Azure AD](active-directory-authentication-scenarios.md).

Hello Galería de aplicaciones de Azure Active Directory proporciona una lista de las aplicaciones que se conocen toosupport un formulario de inicio de sesión único con Azure Active Directory, como se describe en [este artículo](active-directory-appssoaccess-whatis.md). Una vez (como un TI especialista o integrador de sistemas de su organización) haya encontrado la aplicación hello desea tooconnect, puede empezar por siga Hola paso a paso las instrucciones presentadas en hello Azure management portal tooenable inicio de sesión único.

Los clientes con licencias [Azure Active Directory Premium](active-directory-editions.md) también obtienen estas funcionalidades adicionales:

* Integración de autoservicio de cualquier aplicación que admita proveedores de identidades SAML 2.0 (iniciado por el proveedor de servicios o por el proveedor de identidades)
* Integración de autoservicio de cualquier aplicación web que tenga una página de inicio de sesión basada en HTML que use [SSO basado en contraseña](active-directory-appssoaccess-whatis.md#password-based-single-sign-on)
* Conexión sin intervención del Administrador de aplicaciones que usan el protocolo SCIM hello para el aprovisionamiento de usuarios ([descritos aquí](active-directory-scim-provisioning.md))
* Capacidad tooadd vincula tooany aplicación Hola [iniciador de aplicaciones de Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) o hello [panel de acceso de Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)

Esto puede incluir no sólo aplicaciones de SaaS que usar pero aún no han sido integrada toohello Galería de aplicaciones de Azure AD, pero las aplicaciones web de terceros que su organización ha implementado tooservers que controlar, ya sea en la nube de Hola o de forma local.

Estas funcionalidades, también conocidas como *plantillas de integración de aplicaciones*, proporcionan puntos de conexión basados en estándares para aplicaciones que admiten SAML, SCIM o autenticación basada en formularios, e incluyen opciones y configuraciones flexibles para compatibilidad con un amplio número de aplicaciones. 

## <a name="adding-an-unlisted-application"></a>Adición de una aplicación que no figura en la lista
tooconnect una aplicación mediante una plantilla de integración de aplicación, inicie sesión en el portal de administración de Azure Hola con su cuenta de administrador de Active Directory de Azure y examinar toohello **Active Directory > [directorio] > aplicaciones**sección, seleccione **agregar**y, a continuación, **agregar una aplicación de la Galería de hello**. 

![][1]

En la Galería de aplicaciones de hello, puede agregar una aplicación que no figuran en con hello **personalizado** categoría a la izquierda de Hola o seleccionando Hola **agregar una aplicación que no figuran en** vínculo que se muestra en la búsqueda de hello resultados si la aplicación deseada no se encontró. Después de escribir un nombre para la aplicación, puede configurar opciones de inicio de sesión único de Hola y de comportamiento. 

**Sugerencia rápida**: como práctica recomendada, utilice Hola búsqueda función toocheck toosee si aplicación Hola ya existe en la Galería de aplicaciones de Hola. Si se encuentra la aplicación hello y su descripción menciona "inicio de sesión único" y luego la aplicación hello ya es compatible con un inicio de sesión único federado. 

![][2]

Agregar una aplicación de esta manera, proporciona un toohello experiencia muy similares está disponible para las aplicaciones previamente integradas. toostart, seleccione **configurar Single Sign-On**. pantalla de bienvenida siguiente presenta hello siguientes tres opciones para configurar el inicio de sesión único, que se describen en las secciones siguientes de Hola.

![][3]

## <a name="azure-ad-single-sign-on"></a>Inicio de sesión único de Azure AD 
Seleccione esta opción tooconfigure SAML autenticación para aplicación hello. Este método precisa que Hola compatibilidad con aplicaciones SAML 2.0 y debe recopilar información sobre cómo toouse Hola capacidades SAML de la aplicación hello antes de continuar. Después de seleccionar **siguiente**, podrá tooenter solicitadas tres direcciones URL diferentes correspondiente toohello extremos SAML para la aplicación hello. 

![][4]

Dichos componentes son:

* **Dirección URL de inicio de sesión (iniciado por el SP solo)** : cuando el usuario de hello siga toothis toosign de aplicación. Si se configura la aplicación hello único iniciado por el proveedor de servicio de tooperform iniciar sesión, a continuación, cuando un usuario navega toothis URL, proveedor de servicios de Hola se Hola redirección necesarios tooAzure AD tooauthenticate y usuario hello en el inicio de sesión. Si este campo se rellena, Azure AD usará esta aplicación de hello toolaunch de dirección URL de hello Panel de acceso de Azure AD y Office 365. Si este campo es ommited, Azure AD en su lugar realizará el proveedor de identidades-inicio de sesión iniciada cuando aplicación hello se inicia desde Office 365, Hola el Panel de acceso de Azure AD, o de hello Azure AD único inicio de sesión (copiable desde la pestaña panel hello) de la dirección URL.
* **Dirección URL del emisor** -Hola dirección URL del emisor debería identificar únicamente la aplicación hello para que solo inicio de sesión se está configurando. Se trata de valor de Hola que Azure AD envía tooapplication atrás como Hola **audiencia** parámetro de token SAML de Hola y aplicación hello es toovalidate esperado lo. Este valor también aparece como hello **Id. de entidad** en los metadatos SAML proporcionado por la aplicación hello. Compruebe la documentación de SAML de la aplicación de Hola para obtener más información sobre lo que este Id. de entidad o valor de audiencia es. A continuación se muestra un ejemplo de cómo Hola dirección URL de la audiencia aparece en aplicación de hello SAML token toohello devuelto:

```
    <Subject>
    <NameID Format="urn:oasis:names:tc:SAML:2.0:nameid-format:unspecificed">chad.smith@example.com</NameID>
        <SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer" />
      </Subject>
      <Conditions NotBefore="2014-12-19T01:03:14.278Z" NotOnOrAfter="2014-12-19T02:03:14.278Z">
        <AudienceRestriction>
          <Audience>https://tenant.example.com</Audience>
        </AudienceRestriction>
      </Conditions>
```

* **Dirección URL de respuesta** -URL de respuesta de hello es donde la aplicación hello espera token SAML de hello tooreceive. Esto también es que se hace referencia tooas hello **dirección URL del servicio de consumidor de aserción (ACS)**. Consulte la documentación de SAML de la aplicación hello para obtener más información sobre lo que es su dirección URL de respuesta de token de SAML o la dirección URL de ACS.
  Después de que se han introducido, haga clic en **siguiente** tooproceed toohello siguiente pantalla. Esta pantalla proporciona información sobre qué toobe necesidades configurarlo en hello aplicación lado tooenable tooaccept un token de SAML de Azure AD. 

![][5]

Los valores que son necesarios se varían en función de la aplicación hello, así que compruebe la documentación de SAML de la aplicación de Hola para obtener más información. Hola **Sign-On** y **cierre de sesión** dirección URL del servicio ambos resolver toohello mismo punto de conexión, que es el punto de conexión de control de la solicitud SAML de hello para la instancia de Azure AD. Hola dirección URL del emisor es valor de Hola que aparece como Hola "Emisor" dentro de hello aplicación toohello emitido token de SAML. 

Después de que se ha configurado la aplicación, haga clic en **siguiente** botón y, a continuación, Hola **completar** el cuadro de diálogo de tooclose Hola. 

## <a name="assigning-users-and-groups-tooyour-saml-application"></a>Asignar usuarios y aplicaciones de grupos tooyour SAML
Una vez que la aplicación ha sido configurado toouse Azure AD como proveedor de identidad basado en SAML, está casi listo tootest. Como un control de seguridad, Azure AD no emita un token permitiéndoles toosign en aplicación Hola a menos que se les ha concedido acceso mediante Azure AD. A los usuarios se les puede conceder acceso directamente o a través del grupo al que pertenecen. 

tooassign una aplicación de tooyour usuario o grupo, haga clic en hello **asignar usuarios** botón. Seleccione Hola usuario o grupo que desea tooassign y, a continuación, seleccione hello **asignar** botón. 

![][6]

Asignación de un usuario le permitirá tooissue de Azure AD un token de usuario hello, así como provocando un icono para este tooappear de aplicación en el Panel de acceso del usuario de Hola. Una ventana de aplicación también aparecerán en el iniciador de la aplicación de Office 365 Hola si el usuario de hello está usando Office 365. 

Puede cargar un logotipo del mosaico de aplicación hello mediante hello **Cargar logotipo** botón en hello **configurar** pestaña aplicación hello. 

### <a name="customizing-hello-claims-issued-in-hello-saml-token"></a>Personalizar las notificaciones de hello emitidas en el token SAML de Hola
Cuando un usuario autentica toohello aplicación, Azure AD emitirá una aplicación de toohello token de SAML que contiene información (o notificaciones) acerca del usuario de Hola que identifica de forma única a ellos. De forma predeterminada, esto incluye nombre de usuario, dirección de correo electrónico, nombre y apellido del usuario de Hola. 

Puede ver o editar notificaciones Hola enviados en hello aplicación toohello token de SAML en hello **atributos** ficha. 

![][7]

Hay dos razones posibles por las que puede necesitar notificaciones de hello tooedit emitidas en el token SAML de hello: •hello aplicación se ha escrito toorequire otro conjunto de URI de notificación o se ha implementado la aplicación de •Your de valores de una manera que requiere Hola de notificación NameIdentifier notificación toobe un valor distinto de hello username (nombre principal de usuario AKA) almacenados en Azure Active Directory. 

Para obtener información sobre cómo tooadd y editar las notificaciones para estos escenarios, consulte esta [artículo acerca de la personalización de notificaciones](active-directory-saml-claims-customization.md). 

### <a name="testing-hello-saml-application"></a>Probar la aplicación de SAML de hello
Una vez que las direcciones URL de SAML de Hola y el certificado se ha configurado en Azure AD y en la aplicación hello, usuarios o grupos se han asignado toohello aplicación en Azure y notificaciones de Hola se han revisado y editar si es necesario, entonces usuario hello es toosign listo en hello aplicación. 

tootest, simplemente inician sesión en Hola panel de acceso de Azure AD en https://myapps.microsoft.com con una cuenta de usuario asignada toohello aplicación y, a continuación, haga clic en el mosaico de Hola para hello aplicación tookick desactivar el proceso de inicio de sesión único de Hola. Como alternativa, puede examinar directamente toohello dirección URL de inicio de sesión para la aplicación hello e inicio de sesión a partir de ahí. 

Para sugerencias de depuración, vea este [artículo sobre cómo toodebug basado en SAML single sign-on tooapplications](active-directory-saml-debugging.md) 

## <a name="password-single-sign-on"></a>Inicio de sesión único con contraseña
Seleccione esta opción tooconfigure [basada en contraseña de inicio de sesión único](active-directory-appssoaccess-whatis.md) para una aplicación web que tiene una página de inicio de sesión de HTML. SSO basado en contraseña, también la contraseña del que se hace referencia tooas depósito, le permite toomanage acceso y las contraseñas tooweb aplicaciones de usuario que no son compatibles con la federación de identidades. También es útil en escenarios donde varios usuarios necesitan tooshare una sola cuenta, como las cuentas de aplicación de la organización tooyour medios sociales. 

Después de seleccionar **siguiente**, podrá tooenter solicitadas Hola URL de página de la aplicación hello basada en web de inicio de sesión. Tenga en cuenta que debe tratarse de página de Hola que incluya campos de entrada de hello username y password. Una vez escrita, Azure AD inicia una proceso tooparse Hola página de inicio para una entrada de nombre de usuario y una entrada de contraseña. Si el proceso de hello no es correcto, a continuación, le guía a través de un proceso alternativo de la instalación de una extensión de explorador (requiere Internet Explorer, Chrome o Firefox) que le permitirá campos de toomanually captura Hola.

Una vez que se captura la página de inicio de sesión de hello, pueden asignarse a los usuarios y grupos y directivas de credencial pueden establecerse como normal [aplicaciones SSO de contraseña](active-directory-appssoaccess-whatis.md).

Nota: Puede cargar un logotipo del mosaico de aplicación hello mediante hello **Cargar logotipo** botón en hello **configurar** pestaña aplicación hello. 

## <a name="existing-single-sign-on"></a>Inicio de sesión único existente
Seleccione esta opción tooadd un vínculo tooan aplicación tooyour portal de la organización Panel de acceso de Azure AD u Office 365. Puede usar este tooadd vínculos toocustom las aplicaciones web que actualmente la utilizan servicios de federación de Active Directory de Azure (u otro servicio de federación) en lugar de Azure AD para la autenticación. O bien, puede agregar páginas de SharePoint de vínculos profundos toospecific u otras páginas web que desea que solo tooappear sobre los paneles de acceso de sus usuarios. 

Después de seleccionar **siguiente**, podrá tooenter solicitadas Hola URL de toolink de aplicación Hola a. Una vez completado, los usuarios y grupos pueden asignarse toohello aplicación, lo que hace tooappear de aplicación Hola Hola que [iniciador de aplicaciones de Office 365](https://blogs.office.com/2014/10/16/organize-office-365-new-app-launcher-2/) o hello [panel de acceso de Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users) para los usuarios.

Nota: Puede cargar un logotipo del mosaico de aplicación hello mediante hello **Cargar logotipo** botón en hello **configurar** pestaña aplicación hello.

## <a name="related-articles"></a>Artículos relacionados
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)
* [Cómo se emiten las notificaciones tooCustomize en hello Token de SAML para aplicaciones Pre-Integrated](active-directory-saml-claims-customization.md)
* [Cómo depurar el inicio de sesión único basado en SAML en aplicaciones de Azure Active Directory](active-directory-saml-debugging.md)

<!--Image references-->
[1]: ./media/active-directory-saas-custom-apps/customapp1.png
[2]: ./media/active-directory-saas-custom-apps/customapp2.png
[3]: ./media/active-directory-saas-custom-apps/customapp3.png
[4]: ./media/active-directory-saas-custom-apps/customapp4.png
[5]: ./media/active-directory-saas-custom-apps/customapp5.png
[6]: ./media/active-directory-saas-custom-apps/customapp6.png
[7]: ./media/active-directory-saas-custom-apps/customapp7.png
