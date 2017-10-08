---
title: "Tutorial: Integración de Azure Active Directory con Benefitsolver | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse Benefitsolver con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a>Tutorial: Integración de Azure Active Directory con Benefitsolver
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y Benefitsolver.  

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una suscripción habilitada para el inicio de sesión único (SSO) en Benefitsolver

Después de completar este tutorial, los usuarios de hello Azure AD que haya asignado tooBenefitsolver será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para Benefitsolver
2. Configuración del inicio de sesión único (SSO)
3. Configuración del aprovisionamiento de usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Escenario")

## <a name="enabling-hello-application-integration-for-benefitsolver"></a>Habilitar la integración de aplicación Hola para Benefitsolver
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para Benefitsolver.

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a>integración de aplicaciones de hello tooenable para Benefitsolver, lleve a cabo Hola pasos:
1. Hola portal de Azure clásico, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
   ![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
   ![Aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
   ![Agregar aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
   ![Agregar una aplicación de la galería](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **Benefitsolver**.
   
   ![Galería de aplicaciones](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **Benefitsolver**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
   ![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooBenefitsolver con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.  

La aplicación de Benefitsolver espera las aserciones de SAML de hello en un formato específico, lo que requiere tooyour de asignaciones de atributo personalizado de tooadd **atributos de token saml** configuración. 

Hola siguiente captura de pantalla muestra un ejemplo de esto.

![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **Benefitsolver** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que los usuarios toosign en tooBenefitsolver** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configurar inicio de sesión único")
3. En hello **configurar opciones de aplicación** , siga los pasos de hello:
   
   ![Configurar las opciones de la aplicación](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configurar las opciones de la aplicación")
   
   1. Hola **dirección URL de inicio de sesión** cuadro de texto, tipo **http://azure.benefitsolver.com**.
   2. Hola **dirección URL de respuesta** cuadro de texto, tipo **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.  
   3. Haga clic en **Siguiente**.
4. En hello **configurar inicio de sesión único en Benefitsolver** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde el archivo de metadatos de hello localmente en el equipo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configurar inicio de sesión único")
5. Enviar el equipo de soporte técnico de hello descargar metadatos archivo tooyour Benefitsolver.
   
   >[!NOTE]
   >El equipo de soporte de Benefitsolver tiene la configuración real del SSO toodo Hola. Cuando SSO se haya habilitado en su suscripción recibirá una notificación.
   >

6. En hello portal de Azure clásico, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar** tooclose hello **configurar inicio de sesión único** cuadro de diálogo.
   
   ![Configurar inicio de sesión único](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configurar inicio de sesión único")
7. En el menú de hello en la parte superior de hello, haga clic en **atributos** tooopen hello **atributos de Token SAML** cuadro de diálogo.
   
   ![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Atributos")
8. asignaciones de atributos de tooadd Hola necesario, lleve a cabo Hola pasos:
   
   ![Atributos](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Atributos")
   
   | Nombre del atributo | Valor de atributo |
   | --- | --- |
   | ClientID |Debe tooget este valor desde el equipo de soporte de Benefitsolver. |
   | ClientKey |Debe tooget este valor desde el equipo de soporte de Benefitsolver. |
   | LogoutURL |Debe tooget este valor desde el equipo de soporte de Benefitsolver. |
   | EmployeeID |Debe tooget este valor desde el equipo de soporte de Benefitsolver. |
   
   1. Para cada fila de datos de tabla de hello anterior, haga clic en **Agregar atributo de usuario**.
   2. Hola **nombre del atributo** cuadro de texto, nombre de atributo de tipo hello se muestra para esa fila.
   3. Hola **valor del atributo** cuadro de texto, valor de atributo seleccione Hola se muestra para esa fila.
   4. Haga clic en **Completo**.
9. Haga clic en **Aplicar cambios**.

## <a name="configure-user-provisioning"></a>Configurar aprovisionamiento de usuarios
En orden tooenable toolog de los usuarios de Azure AD en Benefitsolver, se les deben aprovisionar en Benefitsolver.  

En caso de hello de Benefitsolver, los datos del empleado están en la aplicación que se rellenan a través de un archivo del censo desde el sistema HRIS (normalmente por la noche).  

>[!NOTE]
>Puede usar cualquier otra Benefitsolver usuario cuenta herramienta de creación o las API proporcionadas por Benefitsolver tooprovision cuentas de usuario AAD. 
> 

## <a name="assigning-users"></a>Asignación de usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a>tooassign tooBenefitsolver de los usuarios, realizar Hola pasos:
1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En Hola ** Benefitsolver ** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Sí")

Si desea tootest las opciones de inicio de sesión único, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

