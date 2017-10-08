---
title: "Introducción a los informes de Azure Active Directory | Microsoft Docs"
description: Listas de Hola varios informes disponibles en los informes de Azure Active Directory
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Introducción a los informes de Azure Active Directory
## <a name="what-it-is"></a>¿Qué es?
Azure Active Directory (Azure AD) incluye informes de seguridad, actividad y auditoría para el directorio. Presentamos una lista de informes de hello incluidas:

### <a name="security-reports"></a>Informes de seguridad
* Inicios de sesión desde orígenes desconocidos
* Inicios de sesión tras varios errores
* Inicios de sesión desde varias ubicaciones geográficas
* Inicios de sesión desde direcciones IP con actividad sospechosa
* Actividad de inicio de sesión irregular
* Inicios de sesión desde dispositivos posiblemente infectados
* Usuarios con actividad de inicio de sesión anómala

### <a name="activity-reports"></a>Informes de actividad
* Uso de la aplicación: resumen
* Uso de la aplicación: detallado
* Panel de la aplicación
* Errores de aprovisionamiento de cuentas
* Dispositivos de usuario individuales
* Actividad de usuario individual
* Informe de actividad de grupos
* Informe de actividad de registro de restablecimiento de contraseña
* Actividad de restablecimiento de contraseña

### <a name="audit-reports"></a>Informes de auditoría
* Informe de auditoría de directorio

> [!TIP]
> Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Cómo funciona
### <a name="reporting-pipeline"></a>Canalización de informes
canalización informes de Hello consta de tres pasos principales. Cada vez que un usuario inicia sesión o se realiza una autenticación, ocurre lo siguiente de hello:

* En primer lugar, se autentica el usuario de hello (correcta o incorrectamente) y Hola resultado se almacena en las bases de datos del servicio de Azure Active Directory de Hola.
* En intervalos regulares, se procesan todos los inicios de sesión recientes. En este momento, la seguridad y los algoritmos de actividades anómalas buscan todos los inicios de sesión recientes en busca de actividad sospechosa.
* Después del procesamiento, Hola informes anota, almacenado en memoria caché y sirve de hello portal de Azure clásico.

### <a name="report-generation-times"></a>Tiempos de generación de informes
Pagar toohello gran volumen de autenticaciones y el inicio de sesión que inicios procesan por hello plataforma de Azure AD, hello más reciente inicios de sesión procesados son, por término medio, una hora anteriores. En raras ocasiones, puede llevar hasta too8 horas tooprocess hello más reciente inicios de sesión.

Puede encontrar iniciar sesión más reciente de hello procesado mediante el examen de texto de Ayuda de hello en parte superior de Hola de cada informe.

![Texto de ayuda en parte superior de Hola de cada informe](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Introducción
### <a name="sign-into-hello-azure-classic-portal"></a>Inicie sesión en hello portal de Azure clásico
En primer lugar, deberá toosign en hello [portal de Azure clásico](https://manage.windowsazure.com) como administrador global o de cumplimiento de normas. También debe ser un administrador de servicios de suscripción de Azure o Coadministrador o usar Hola "acceso tooAzure AD" suscripción de Azure.

### <a name="navigate-tooreports"></a>Navegue tooReports
tooview informes, navegue toohello ficha de informes en parte superior de Hola de su directorio.

Si se trata de la primera vez que ver los informes de hello, necesitará cuadro de diálogo de tooagree tooa para poder ver los informes de Hola. Se trata de tooensure que es aceptable para que los administradores de su organización tooview estos datos, lo cual pueden considerarse información privada en algunos países.

![Cuadro de diálogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Exploración de cada informe
Navegue a cada informe toosee Hola de datos que se recopilan y procesan Hola inicios de sesión. Puede encontrar un [lista de todos los informes de hello aquí](active-directory-reporting-guide.md).

![Todos los informes](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Descargar informes de hello como CSV
Cada informe se puede descargar como un archivo CSV (valores separados por comas). Puede utilizar estos archivos en Excel, Power BI o programas toofurther analizar los datos de análisis de terceros.

toodownload cualquier informe como CSV, navegar por toohello informe y haga clic en "Descargar" en la parte inferior de Hola.

![Botón Descargar](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Personalización de las alertas para la actividad de inicio de sesión anómala
Navegue toohello "Configurar" pestaña del directorio.

Desplácese toohello sección de "Notificaciones".

Habilitar o deshabilitar la sección "Notificaciones de correo electrónico de inicios de sesión anómalos" de Hola.

![Hola sección notificaciones](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Integrar con hello API Reporting de Azure AD
Vea [Introducción a Hola API Reporting](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Uso de Multi-Factor Authentication en usuarios
Seleccione un usuario en un informe.

Haga clic en el botón de "Habilitar MFA" de hello en parte inferior de Hola de pantalla de bienvenida.

![botón de la autenticación multifactor de Hello final Hola de pantalla de bienvenida](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Más información
### <a name="audit-events"></a>Eventos de auditoría
Obtenga información acerca de qué eventos se auditan en el directorio de hello en [Azure Active Directory informar de eventos de auditoría](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Integración de la API
Vea [Introducción a Hola API Reporting](active-directory-reporting-api-getting-started.md) hello y [documentación de referencia de API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Ponerse en contacto
Envíe un correo electrónico a [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) para trasmitir sus comentarios, solicitar ayuda o plantear las preguntas que tenga.

> [!TIP]
> Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).
> 
> 

