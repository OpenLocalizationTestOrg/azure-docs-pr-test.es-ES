---
title: aaaHow toouse hello Azure Active Directory Power BI Content Pack | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse hello Azure Active Directory Power BI Content Pack"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>¿Cómo toouse hello Azure Active Directory Power BI Content Pack

Comprender cómo los usuarios adoptan y usan las características de Azure Active Directory es fundamental para un administrador de TI. Permite el uso de tooincrease de comunicación y la infraestructura de TI y tooget Hola más partido de las características AAD de tooplan. Paquete de contenido de Power BI para Azure Active Directory proporciona Hola capacidad toofurther analizar su toounderstand datos cómo puede usar esta toogather transmite información sobre los datos en que está sucediendo con su Azure Active Directory para hello varias funciones, muy se basan en.  Con la integración de Hola de API de Azure Active Directory en Power BI, puede descargar los paquetes de contenido pregenerado Hola fácilmente y obtener información de las actividades de hello tooall dentro de su Azure Active Directory con experiencia de visualización enriquecida de que Power BI ofrece. Puede crear su propio panel y compartirlo fácilmente con cualquier persona de su organización. 

Este tema se proporciona con instrucciones paso a paso sobre cómo tooinstall y uso Hola contenido módulo en su entorno.

## <a name="installation"></a>Instalación  

**Hola tooinstall paquete de contenido de Power BI:**

1. Inicie sesión en [Power BI](https://app.powerbi.com/groups/me/getdata/services) con su cuenta de Power BI (Esto es hello la misma cuenta que la cuenta de AD de Azure u Office 365).

2. En hello parte inferior del panel de navegación izquierdo de hello, seleccione **obtener datos**.

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. Hola **servicios** cuadro, haga clic en **obtener**.
   
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Busque **Azure Active Directory**.

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Cuando se le solicite, escriba su identificador de inquilino de Azure AD y haga clic en **Siguiente**.

    > [!TIP] 
    > Hola de tooget de forma rápida Id. de inquilino para su inquilino de Office 365 o Azure AD es toologin toohello Portal de Azure AD, explorar en profundidad toohello directorio e Id. de Hola de copia de hello después de la dirección URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ Directorio/ActiveDirectoryExtension/<tenantid>/directoryQuickStart

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Haga clic en **Iniciar sesión**. 
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Escriba su nombre de usuario y contraseña, y haga clic en **Iniciar sesión**.
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  En el cuadro de diálogo de consentimiento de aplicación Hola, haga clic en **Accept**.
 
9.  Cuando se haya creado el panel de registros de actividad de Azure Active Directory, haga clic en él.
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>¿Qué puedo hacer con este paquete de contenido?

Antes de que pasamos lo que puede hacer con este paquete de contenido, obtener vista previa a continuación del Hola varios informes en el contenido de hello del módulo. Informe de datos van toohello **últimos 30 días**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Informes incluidos en esta versión del paquete de contenido de registros de Azure Active Directory

**Informes de uso de la aplicación y la tendencia**: Obtenga información sobre aplicaciones de Hola que se utilizan en su organización y cuáles se usan más Hola y cuándo. Puede usar este informe toogather visiones cómo se usa una aplicación recientemente implantado en su organización o averiguar qué aplicaciones son frecuentes. Al hacerlo, puede mejorar el uso si ve si no se usa aplicación Hola.

**Inicios de sesión por ubicación y los usuarios**: Obtenga información sobre todos los Hola inicios de sesión lleva a cabo con la identidad de Azure proporciona nuevas perspectivas en identidad Hola de usuarios de Hola. Con esto, puede profundizar en los inicios de sesión individuales y responder a preguntas como:

- ¿Desde dónde inició sesión este usuario?
- ¿Qué usuario tiene Hola mayoría de inicios de sesión y donde inicio de sesión de? 
- ¿Estaba en el inicio de sesión de hello correcta?  
 
Para profundizar en los detalles, haga clic en una fecha o ubicación concretas.

**Usuarios únicos por aplicación**: obtenga una vista de todos los usuarios únicos de una aplicación determinada. Esto incluye solo los usuarios que hayan iniciado sesión "*correctamente*" en una aplicación.

**Inicios de sesión de dispositivo**: obtener una vista del tipo hello del sistema operativo y exploradores están siendo utilizados por los usuarios de su organización con información detallada sobre los usuarios de hello incluidos:

- User Name
- Dirección IP
- Ubicación 
- Estado de inicio de sesión 

Con este informe, puede comprender Hola diversos perfiles de dispositivo usan dentro de su organización y determinan las directivas de dispositivo según lo que se usa

**Embudo de SSPR**: obtenga una descripción de cómo se llevan a cabo los restablecimientos de contraseña en su organización. Obtener un vistazo en contraseña cuántos restablecimientos se intentaron a través de la herramienta de Autoservicio de Hola y cuántos de ellos obtuvieron resultados satisfactorios. Profundizar en error de restablecimientos de contraseña de hello mediante embudo de Autoservicio de Hola y entender por qué se produjeron determinados errores. Este informe ofrece una visión más profunda de cómo se utilizan herramientas SSPR Hola dentro de su organización para que pueda tomar las decisiones adecuadas de Hola.

## <a name="customizing-azure-ad-activity-content-pack"></a>Personalización del paquete de contenido de actividad de Azure AD

**Cambiar la visualización**: puede cambiar la visualización de un informe, haga clic en **Editar informe** y seleccione la visualización de Hola que quiera.
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Incluir campos adicionales**: puede agregar un informe de toohello de campo o quitar seleccionando hello toowhich visual desea tooadd o quitar Hola campo. En el ejemplo de Hola a continuación, agregamos la vista de tabla de toohello de campo de "estado de inicio de sesión". 
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Panel de PIN visualizaciones tooyour**: puede personalizar el panel e incluir sus propios informes de toohello visualizaciones y anclar el panel de toohello. En el siguiente ejemplo de Hola, he agregado un filtro nuevo denominado "estado de inicio de sesión" y se incluyen en el informe de Hola. También cambia la visualización de Hola de gráfico de líneas de tooa de gráfico de barras y se puede anclar este nuevo panel toohello visual.

![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Compartir su panel**: una vez haya creado el contenido de Hola que desea, puede compartir panel Hola con usuarios de hello en su organización. Recuerde que una vez compartir informes de hello, pueden ver los campos de Hola que ha seleccionado en el informe de Hola.
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Programación de una actualización diaria de su informe de Power BI

tooschedule una actualización diaria de su informe de Power BI, vaya demasiado**conjuntos de datos > Configuración > Programar actualización** y configúrelo como se muestra a continuación.
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Actualizar versión de toonewer del paquete de contenido

Si desea que tooupdate el paquete de contenido de tooget una versión más reciente:

- Descargar el nuevo paquete de contenido de Hola y configurarla según las instrucciones enumeradas en este artículo.

- Una vez que haya configurado, vaya demasiado**origen de datos > Configuración > las credenciales del origen de datos** y vuelva a escribir sus credenciales, tal y como se muestra a continuación

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Tan pronto como nueva versión de paquete de contenido de Hola de hello está en funcionamiento, puede quitar la versión anterior de hello si es necesario mediante la eliminación de informes subyacentes de Hola y conjuntos de datos asociados con ese paquete de contenido.

## <a name="still-having-issues"></a>¿Sigue teniendo problemas? 

Consulte nuestra [guía de solución de problemas](active-directory-reporting-troubleshoot-content-pack.md). Para obtener ayuda general con Power BI, visite estos [artículos de Ayuda](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Pasos siguientes

Para obtener información general de informes, vea hello [reporting de Azure Active Directory](active-directory-reporting-azure-portal.md).
