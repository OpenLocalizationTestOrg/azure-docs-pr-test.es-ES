---
title: "acceso a la aplicación de servicio de aaaSelf y la administración delegada con Azure Active Directory | Documentos de Microsoft"
description: "Este artículo describe cómo tener acceso aplicaciones de autoservicio de tooenable y la administración delegada con Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 448a7fe8-a162-475e-9ba2-2e3ab59302bc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: asmalser
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 90bec3bd71796f22a782929b028db0d18c3aa1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="self-service-application-access-and-delegated-management-with-azure-active-directory"></a>Acceso a aplicaciones de autoservicio y administración delegada con Azure Active Directory
Habilitar las funcionalidades de autoservicio para los usuarios finales es un escenario común para TI empresarial. Una gran cantidad de usuarios, una gran cantidad de aplicaciones y persona hello best-informed acceso toomake concede decisiones no pueden ser administrador del directorio de Hola. Hola a menudo toodecide mejor persona que puede tener acceso a una aplicación es responsable de equipo u otro administrador delegado. Sin embargo, resulta Hola que usa la aplicación hello, usuario y que Hola sabe lo que necesitan toobe capaz de toodo su trabajo.

> [!IMPORTANT]
> Microsoft recomienda que administrar Azure AD utilizando hello [centro de administración de Azure AD](https://aad.portal.azure.com) Hola portal de Azure en lugar de usar Hola portal de Azure clásico que se hace referencia en este artículo. 

El acceso a la aplicación de autoservicio es una característica de las licencias [Azure Active Directory Premium](https://azure.microsoft.com/trial/get-started-active-directory/) P1 y P2 que permite a los administradores de directorio:

* Permitir el acceso de usuarios toorequest tooapplications con una opción "obtener más aplicaciones" disponer en mosaico en hello [Panel de acceso de Azure AD](active-directory-appssoaccess-whatis.md#deploying-azure-ad-integrated-applications-to-users)
* Establecer qué usuarios de las aplicaciones pueden solicitar acceso
* Establecer si o no es necesaria para la aplicación de tooan de acceso de los usuarios toobe asignar tooself capaz de aprobación
* Conjunto que se debe aprobar las solicitudes de Hola y administrar el acceso para cada aplicación

Hoy en día se admite esta capacidad para todas las aplicaciones previamente integradas y personalizadas que admiten federado o basada en contraseña de inicio de sesión único en hello [Galería de aplicaciones de Azure Active Directory](https://azure.microsoft.com/marketplace/active-directory/all/), incluidas las aplicaciones como Salesforce, Dropbox, Google Apps y mucho más.
En este artículo se describe cómo:

* Configurar el acceso a aplicaciones de autoservicio para usuarios finales, incluida la configuración de un flujo de trabajo de aprobación opcional. 
* Delegar la administración de acceso para las personas más adecuadas de toohello aplicaciones específicas de su organización y habilitarlos toouse hello Azure AD acceso panel tooapprove acceso a las solicitudes, asignar directamente el acceso a los usuarios de tooselected o establecer (opcionalmente) credenciales de acceso a la aplicación cuando se configura basada en contraseña de inicio de sesión único

## <a name="configuring-self-service-application-access"></a>Configuración del acceso de la aplicación de autoservicio
acceso a las aplicaciones de autoservicio tooenable y configurar las aplicaciones que pueden agregarse o solicitado por los usuarios finales, siguen estas instrucciones.

1. Inicio de sesión en hello [portal de Azure clásico](https://manage.windowsazure.com/).

2.   En hello **Active Directory** sección, seleccione el directorio y después seleccione hello **aplicaciones** ficha. 

3. Seleccione hello **agregar** botón y use tooselect de opción de la Galería de Hola y agregue una aplicación.

4. Una vez agregada la aplicación, obtendrá la página de inicio rápido de la aplicación hello. Haga clic en **configurar Single Sign-On**, seleccione Hola único inicio de sesión en modo deseado y guardar la configuración de Hola. 

5. A continuación, seleccione hello **configurar** ficha tooenable usuarios toorequest acceso toothis aplicación desde el panel de acceso de hello Azure AD, establecer **permitir acceso a la aplicación de autoservicio** demasiado**Sí**.
  
  ![][1]

6. toooptionally configurar un flujo de trabajo de aprobación para las solicitudes de acceso, establecer **requieren la aprobación antes de conceder acceso** demasiado**Sí**. A continuación, se pueden seleccionar uno o más aprobadores mediante hello **aprobadores** botón.

  Un aprobador puede ser cualquier usuario de la organización de hello con una cuenta de Azure AD y podría ser responsable de aprovisionamiento de cuentas, administración de licencias, o cualquier otro proceso de negocio de su organización requiere antes de conceder acceso tooan aplicación. aprobador Hola incluso podría ser propietario del grupo de Hola de uno o varios comparten grupos de cuentas y puede asignar Hola tooone de los usuarios de estos toogive grupos acceso a través de una cuenta compartida. 

  Si no se requiere ninguna aprobación, a continuación, los usuarios al instante, obtendrá panel de acceso de hello aplicación agregada tootheir Azure AD. Si se ha configurado la aplicación hello para [aprovisionamiento automático de usuarios](active-directory-saas-app-provisioning.md), o se ha configurado [modo SSO de contraseña "administradas por el usuario"](active-directory-appssoaccess-whatis.md#password-based-single-sign-on), usuario de hello ya debe tener un usuario de la cuenta y conocer la contraseña de Hola.

7. Si se ha configurado toouse aplicación hello basada en contraseña de inicio de sesión único, a continuación, una opción para permitir el aprobador hello tooset credenciales de SSO de hello en nombre de cada usuario también está disponible. Para obtener más información, vea la sección de hello en [delegar la administración de acceso](#delegated-application-access-management).

8. Por último, Hola **grupo para los usuarios de Self-Assigned** muestra Hola nombre del grupo de Hola que es usado toostore Hola que los usuarios se han concedido o acceso toohello aplicación asignada. aprobador de acceso de Hola se convierte en propietario de Hola de este grupo. Si no existe el nombre del grupo de Hola que se muestra, se crea automáticamente. Opcionalmente, se puede establecer nombre del grupo de hello toohello nombre de un grupo existente.

9. configuración de hello toosave, haga clic en **guardar** final Hola de pantalla de bienvenida. Ahora los usuarios pueden toorequest acceso toothis aplicación desde el panel de acceso de Hola.

10. experiencia del usuario final tootry hello, inicio de sesión en el panel de acceso de Azure AD de su organización en https://myapps.microsoft.com, preferiblemente con una cuenta diferente que no es un aprobador de la aplicación. 

11. En hello **aplicaciones** , haga clic en hello **obtener más aplicaciones** icono. Este icono muestra una galería de todas las aplicaciones de Hola que se han habilitado para el acceso a aplicaciones de autoservicio en directorio de hello, con toosearch de capacidad de Hola y filtrar por categoría de la aplicación hello izquierda. 

12. Al hacer clic en una aplicación inicia el proceso de solicitud de saludo. Si no hay ningún proceso de aprobación es necesaria, aplicación hello se agregarán inmediatamente debajo hello **aplicaciones** ficha después de una confirmación corta. Si se requiere la aprobación, a continuación, verá un cuadro de diálogo que indica esto y se envía un correo electrónico toohello aprobadores. Debe iniciar sesión en hello panel de acceso como un toosee no es aprobador de este proceso de solicitud.

13. correo electrónico de Hello dirige Hola aprobador toosign en el panel de acceso de Azure AD de Hola y aprobar la solicitud de Hola. Una vez que se aprueba la solicitud de hello (y que se hayan realizado los procesos especiales que se define por aprobador hello), Hola verá Hola aparecen bajo sus **aplicaciones** ficha donde puede iniciar sesión en él.

## <a name="delegated-application-access-management"></a>Administración de acceso a aplicaciones delegadas
Un aprobador de acceso de la aplicación puede ser cualquier usuario de su organización que sea tooapprove persona más adecuada de Hola o denegar acceso toohello aplicación en cuestión. Este usuario podría ser responsable de aprovisionamiento de cuentas, administración de licencias, o cualquier otro proceso de negocio de su organización requiere antes de conceder acceso tooan aplicación.

Al configurar el acceso a la aplicación de autoservicio se ha descrito anteriormente, cualquier aplicación asignada ven aprobadores adicionales **administrar aplicaciones** icono en el panel de acceso de hello Azure AD, que muestra las aplicaciones que están Administrador de acceso de Hola para. Al hacer clic en una aplicación, se muestra una pantalla con varias opciones.

![][2]

### <a name="approve-requests"></a>Aprobar solicitudes
Hola **aprobar solicitudes** icono permite aprobadores toosee pendiente aplicación toothat específico de aprobaciones y pestaña de aprobaciones toohello de redirecciones que solicita Hola puede confirmar o denegar. aprobador Hello también recibe mensajes de correo electrónico automatizadas siempre que se crea una solicitud que les indica qué toodo.

### <a name="add-users"></a>Agregar usuarios
Hola **agregar usuarios** icono permite aprobadores toodirectly seleccionado de conceder a los usuarios acceso toohello aplicación. Al hacer clic en este icono, aprobador Hola ve que un cuadro de diálogo permite tooview y búsqueda para los usuarios en su directorio. Al agregar un usuario aplicación Hola se muestran en paneles de acceso de Azure AD de esos usuarios u Office 365. Si se requiere cualquier proceso de aprovisionamiento manual del usuario en la aplicación hello antes de que el usuario de hello es capaz de toosign en, a continuación, aprobador Hola debe realizar este proceso antes de asignar el acceso.  

### <a name="manage-users"></a>Administrar usuarios
Hola **administrar usuarios** icono permite aprobadores toodirectly actualizar o quitar los usuarios que tienen acceso a aplicaciones de toohello. 

### <a name="configure-password-sso-credentials-if-applicable"></a>Configuración de credenciales de SSO con contraseña (si corresponde)
Hola **configurar** mosaico solo se muestra si aplicación hello configuró Hola TI Administrador toouse basado en contraseña inicio de sesión único, y concede al administrador de hello aprobador Hola credenciales de SSO de contraseña de hello capacidad tooset como se describió anteriormente. Cuando se selecciona, Hola aprobador se presenta con varias opciones para cómo credenciales Hola son tooassigned propagado a los usuarios:

![][3]

* **Los usuarios iniciar sesión con sus propias contraseñas** : en este modo, los usuarios de hello asignado sepan en qué sus nombres de usuario y contraseñas son para la aplicación hello y son tooenter solicitada usarlas en su primera aplicación de inicio de sesión toohello. Hello escenario corresponde caso SSO de contraseña toohello donde hello [a los usuarios administran credenciales](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Los usuarios inician sesión automáticamente en el uso de cuentas independientes que se administran** : en este modo, no se requiere tooenter o sepa cuáles son sus credenciales específico de la aplicación al iniciar sesión en la aplicación hello usuarios de hello asignado. En su lugar, aprobador Hola establece las credenciales de Hola para cada usuario después de asignar el acceso mediante hello **Agregar usuario** icono. Cuando hace clic en usuario de hello en la aplicación hello en su panel de acceso u Office 365, sesión automáticamente con credenciales de hello establecidas por aprobador Hola. Hello escenario corresponde caso SSO de contraseña toohello donde hello [los administradores administrar credenciales](active-directory-appssoaccess-whatis.md#password-based-single-sign-on).
* **Los usuarios inician sesión automáticamente en con una cuenta única que administrar** -un caso especial, en este caso es toouse adecuado cuando todos los usuarios asignados deben toobe concede acceso mediante una cuenta compartida única. Hola de caso de uso más común para esta característica es con aplicaciones de redes sociales, donde una organización tiene una cuenta de "company" único y varios usuarios deben toomake actualizaciones toothat cuenta. Hello escenario también corresponde caso SSO de contraseña toohello donde hello [los administradores administrar credenciales](active-directory-appssoaccess-whatis.md#password-based-single-sign-on). Sin embargo, después de seleccionar esta opción, aprobador Hola será el nombre de usuario de tooenter solicitadas hello y contraseña de una cuenta compartida única Hola. Una vez completado, todos los usuarios asignados han iniciado sesión con esta cuenta al hacer clic en la aplicación hello en sus paneles de acceso de Azure AD u Office 365.

## <a name="additional-resources"></a>Recursos adicionales
* [Índice de artículos sobre la administración de aplicaciones en Azure Active Directory](active-directory-apps-index.md)

<!--Image references-->
[1]: ./media/active-directory-self-service-application-access/ssaa_admin.PNG
[2]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app.PNG
[3]: ./media/active-directory-self-service-application-access/ssaa_ap_manage_app_config.PNG
