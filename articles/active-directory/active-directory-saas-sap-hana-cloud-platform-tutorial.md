---
title: "Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform | Microsoft Docs"
description: "¡Obtenga información acerca de cómo toouse plataforma en la nube SAP HANA con Azure Active Directory tooenable único inicio de sesión, aprovisionamiento automático y mucho más!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a>Tutorial: Integración de Azure Active Directory con SAP HANA Cloud Platform
objetivo de Hola de este tutorial es la integración de hello tooshow de Azure y plataforma en la nube SAP HANA.

escenario de Hello descrito en este tutorial se da por supuesto que ya tiene Hola siguientes elementos:

* Una suscripción de Azure válida
* Una cuenta de SAP HANA Cloud Platform

Después de completar este tutorial, Hola usuarios de Azure AD que haya asignado tooSAP plataforma de nube de HANA será capaz de toosingle inicio de sesión en la aplicación hello mediante hello [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

>[!IMPORTANT]
>Necesita toodeploy su propia aplicación o suscribirse tooan aplicación en la plataforma de nube SAP HANA tootest de cuenta único inicio de sesión. En este tutorial, una aplicación se implementa en la cuenta de hello.
> 
> 

escenario de Hello descrito en este tutorial consta de hello después de bloques de creación:

1. Habilitar la integración de aplicación Hola para plataforma en la nube SAP HANA
2. Configuración del inicio de sesión único (SSO)
3. Asignar un rol tooa a un usuario
4. Asignación de usuarios

![Escenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Escenario")

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a>Habilitar la integración de aplicación Hola para plataforma en la nube SAP HANA
objetivo de Hola de esta sección es toooutline la integración de aplicaciones de hello tooenable para plataforma en la nube SAP HANA.

**integración de aplicaciones de hello tooenable para la plataforma de nube de SAP HANA, lleve a cabo Hola pasos:**

1. Hola Portal de administración de Azure, en el panel de navegación izquierdo de hello, haga clic en **Active Directory**.
   
    ![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")
2. De hello **Directory** lista, directorio de Hola select para la que desee tooenable integración de directorios.
3. Haga clic en vista de aplicaciones de hello tooopen, en la vista de directorio de hello, **aplicaciones** en el menú superior Hola.
   
    ![Aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Aplicaciones")
4. Haga clic en **agregar** final Hola de página Hola.
   
    ![Agregar aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Agregar aplicaciones")
5. En hello **especifique qué desea toodo** cuadro de diálogo, haga clic en **agregar una aplicación de la Galería de hello**.
   
    ![Agregar una aplicación de la galería](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Agregar una aplicación de la galería")
6. Hola **cuadro de búsqueda**, tipo **plataforma en la nube SAP HANA**.
   
    ![Galería de aplicaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Galería de aplicaciones")
7. En el panel de resultados de hello, seleccione **plataforma en la nube SAP HANA**y, a continuación, haga clic en **completar** aplicación de hello tooadd.
   
    ![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")
   
## <a name="configure-single-sign-on"></a>Configurar inicio de sesión único

objetivo de Hola de esta sección es toooutline cómo tooenable usuarios tooauthenticate tooSAP plataforma de nube de HANA con su cuenta de Azure AD utilizando federación basada en protocolo SAML de Hola.

Como parte de este procedimiento, se le tooupload requiere un inquilino de plataforma en la nube SAP HANA tooyour certificado codificado en base 64.  

Si no está familiarizado con este procedimiento, vea [cómo tooconvert certificado de un archivo binario en un archivo de texto](http://youtu.be/PlgrzUZ-Y1o)

**tooconfigure inicio de sesión único, lleve a cabo Hola pasos:**

1. En el portal de Azure clásico en Hola Hola **plataforma en la nube SAP HANA** página de integración de aplicaciones, haga clic en **configurar inicio de sesión único** tooopen hello **configurar inicio de sesión único**cuadro de diálogo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configurar inicio de sesión único")
2. En hello **¿cómo desea que toosign a los usuarios en la plataforma de nube de HANA tooSAP** página, seleccione **Microsoft Azure AD Single Sign-On**y, a continuación, haga clic en **siguiente**.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configurar inicio de sesión único")
3. En una ventana del explorador web diferente, inicie sesión en toohello cabina de plataforma de nube SAP HANA en https://account. \<host horizontal\>.ondemand.com/cockpit (p. ej.: *https://account.hanatrial.ondemand.com/cockpit*).
4. Haga clic en hello **confianza** ficha.
   
    ![Confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Confianza")
5. En la sección de administración de confianza, siga Hola pasos:
   
    ![Obtención de metadatos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Obtención de metadatos")
   
   1. Haga clic en hello **proveedor de servicios Local** ficha.
   2. Hola toodownload archivo de metadatos de la plataforma en la nube SAP HANA, haga clic en **obtener metadatos**.
6. En hello Azure Active portal clásico en hello **configurar URL de aplicación** página realizar pasos de Hola y, a continuación, haga clic en **siguiente**.
   
    ![Configurar dirección URL de la aplicación](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configurar dirección URL de la aplicación")
   
   1. Hola **dirección URL de inicio de sesión** cuadro de texto, escriba Hola la dirección URL utilizada por su toosign a los usuarios en su **plataforma en la nube SAP HANA** aplicación. Se trata de una dirección URL específica de la cuenta de hello de un recurso protegido en la aplicación de la plataforma en la nube SAP HANA. Hello dirección URL se basa Hola siguiente patrón: *https://\<applicationName\>\<accountName\>.\< host horizontal\>.ondemand.com/\<ruta de acceso\_a\_protegido\_recursos\>*  (p. ej.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)
      
     >[!NOTE]
     >Se trata de dirección URL de hello en la aplicación de plataforma en la nube SAP HANA que requiere hello tooauthenticate de usuario.
     > 

   2. Abrir archivo de metadatos de plataforma en la nube SAP HANA Hola descargado y, a continuación, busque hello **NS3: assertionconsumerservice** etiqueta.
   3. Copiar valor de Hola de hello **ubicación** de atributo y, a continuación, péguelo en hello **URL de respuesta de plataforma de nube de SAP HANA** cuadro de texto.

7. En hello **configurar inicio de sesión único en plataforma en la nube SAP HANA** page, toodownload sus metadatos, haga clic en **descargar metadatos**y, a continuación, guarde el archivo hello en el equipo.
   
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configurar inicio de sesión único")
8. En hello cabina de plataforma de nube de SAP HANA, Hola **proveedor de servicios Local** sección, lleve a cabo Hola pasos:
   
    ![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Administración de confianza")
   
  1. Haga clic en **Editar**.
  2. En **Configuration Type** (Tipo de configuración), seleccione **Custom** (Personalizado).
  3. Como **nombre del proveedor Local**, deje el valor predeterminado de Hola.
  4. toogenerate una **clave de firma de** y un **certificado de firma de** par de claves, haga clic en **generar el par de claves**.
  5. En **Principal Propagation** (Propagación de entidad de seguridad), seleccione **Disabled** (Deshabilitada).
  6. En **Force Authentication** (Forzar autenticación), seleccione **Disabled** (Deshabilitado).
  7. Haga clic en **Guardar**.

9. Haga clic en hello **proveedor de identidad de confianza** ficha y, a continuación, haga clic en **Agregar proveedor de identidad de confianza**.
   
    ![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Administración de confianza")
   
    >[!NOTE]
    >lista de hello toomanage de proveedores de identidad de confianza, deberá toohave elegido Hola tipo de configuración personalizada en hello sección proveedor de servicio Local. Para el tipo de configuración predeterminado, tendrá un toohello de confianza implícita que no puede modificar el servicio de Id. de SAP. Para Ninguno, no tiene ninguna configuración de confianza.
    > 
    > 

10. Haga clic en hello **General** ficha y, a continuación, haga clic en **examinar** hello tooupload descargado el archivo de metadatos.
    
    ![Administración de confianza](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Administración de confianza")
    
    >[!NOTE]
    >Después de cargar el archivo de metadatos de hello, valores de hello para **dirección URL de inicio de sesión único**, **dirección URL de cierre de sesión único** y **certificado de firma de** se rellenan automáticamente.
    > 
    > 

11. Haga clic en hello **atributos** ficha.
12. En hello **atributos** , realice Hola siguiendo el paso:
    
    ![Atributos](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Atributos") 
  * Haga clic en **Agregar atributo**y, a continuación, agregue Hola siguientes atributos basados en aserción:
       
    | Atributo de aserción | Atributo de entidad de seguridad |
    | --- | --- |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname |firstname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname |Lastname |
    | http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress |email 
   
     >[!NOTE]
     >configuración de Hola de hello atributos depende de cómo Hola aplicaciones en HCP se desarrollan, es decir, qué atributos esperan en hello respuesta de SAML y con qué nombre (atributo de entidad de seguridad) tienen acceso a este atributo en el código de hello.
     > 
     >  

    1.  Hola **atributo Default** Hola captura de pantalla es solo para fines ilustrativos. No es necesario trabajo de escenario de toomake Hola.   
    2.  Hola nombres y valores de **atributo de entidad de seguridad** se muestra en hello captura de pantalla dependen de cómo se desarrolla la aplicación hello. Es posible que la aplicación requiera diferentes asignaciones.
     
13. En el portal de Azure clásico en Hola Hola **configurar inicio de sesión único en plataforma en la nube SAP HANA** página de diálogo, seleccione la confirmación de configuración de inicio de sesión único de hello y, a continuación, haga clic en **completar**.
    
    ![Configurar inicio de sesión único](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configurar inicio de sesión único")

###<a name="assertion-based-groups"></a>Grupos basados en aserción
Como paso opcional, puede configurar grupos basados en aserciones para su proveedor de identidades de Azure Active Directory.

Uso de grupos en plataforma en la nube SAP HANA permite asignar toodynamically uno o más tooone de los usuarios o más roles en las aplicaciones de la plataforma en la nube SAP HANA, determinado por los valores de los atributos de hello SAML 2.0 aserción. 

Por ejemplo, si hello la aserción contiene el atributo de Hola "*contrato = temporal*", puede que desee todos los grupos de usuarios afectados toobe toohello agregado"*temporal*". grupo de Hola "*temporal*" puede contener uno o varios roles de una o varias de las aplicaciones implementadas en su cuenta de plataforma en la nube SAP HANA.
 
Utilice grupos basados en aserción cuando desee asignar toosimultaneously tooone muchos de los usuarios o más roles de las aplicaciones en su cuenta de plataforma en la nube SAP HANA. Si desea que solo un número único o pequeño de usuarios toospecific funciones tooassign, recomendamos asignarlos directamente en hello "**autorizaciones**" pestaña de cabina de plataforma en la nube SAP HANA Hola.

## <a name="assign-a-role-tooa-user"></a>Asignar a un usuario de tooa de rol
En orden tooenable toolog de los usuarios de Azure AD en plataforma en la nube SAP HANA, debe asignar roles de hello toothem de plataforma en la nube SAP HANA.

**tooassign un usuario de tooa rol, lleve a cabo Hola pasos:**

1. Inicie sesión en tooyour **plataforma en la nube SAP HANA** cabina.
2. Realice Hola siguiente:
   
   ![Autorizaciones](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Autorizaciones")
   
  1. Haga clic en **Authorization**(Autorización).
  2. Haga clic en hello **usuarios** ficha.
  3. Hola **usuario** cuadro de texto, dirección de correo electrónico del usuario de tipo hello.
  4. Haga clic en **asignar** rol tooa de tooassign Hola usuario.
  5. Haga clic en **Guardar**.

## <a name="assign-users"></a>Asignar usuarios
tootest la configuración, debe toogrant los usuarios de hello Azure AD que desee tooallow con su tooit de acceso de la aplicación mediante la asignación de ellos.

**tooassign usuarios tooSAP plataforma de nube de HANA, lleve a cabo Hola pasos:**

1. Hola portal de Azure clásico, cree una cuenta de prueba.
2. En hello **plataforma en la nube SAP HANA** página de integración de aplicaciones, haga clic en **asignar usuarios**.
   
   ![Asignar usuarios](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Asignar usuarios")
3. Seleccione el usuario de prueba, haga clic en **asignar**y, a continuación, haga clic en **Sí** tooconfirm su asignación.
   
   ![Sí](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Sí")

Si desea tootest la configuración de SSO, abra Hola Panel de acceso. Para obtener más información acerca de hello Panel de acceso, consulte [Introducción toohello Panel de acceso](active-directory-saas-access-panel-introduction.md).

