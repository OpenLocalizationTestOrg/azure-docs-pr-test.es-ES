---
title: Azure AD Connect Health con AD FS aaaUsing | Documentos de Microsoft
description: "Se trata hello Azure AD Connect Health página cómo toomonitor local infraestructura de AD FS."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
editor: curtand
ms.assetid: dc0e53d8-403e-462a-9543-164eaa7dd8b3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0cd26e8762be65e09d22e1f113e5165c4f131715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-ad-fs-using-azure-ad-connect-health"></a>Supervisión de AD FS mediante Azure AD Connect Health
Hola después de documentación es toomonitoring específico de la infraestructura de AD FS con Azure AD Connect Health. Para más información sobre la supervisión de Azure AD Connect (Sync) con Azure AD Connect Health, consulte [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md). Para obtener información adicional sobre la supervisión de los Servicios de dominio de Active Directory con Azure AD Connect Health, consulte [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md)(Uso de Azure AD Connect Health con AD DS).

## <a name="alerts-for-ad-fs"></a>Alertas de AD FS
Hola sección de alertas de Azure AD Connect Health proporciona que Hola lista de alertas activas. Cada alerta incluye información relevante, pasos de resolución así como documentación de toorelated de vínculos.

Haga doble clic en un tooopen alerta, activo o resuelto una nueva hoja con información adicional, los pasos que puede seguir tooresolve Hola alerta y vínculos toorelevant documentación. También puede ver datos históricos sobre las alertas que se resolvieron en hello anterior.

![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health/alert2.png)

## <a name="usage-analytics-for-ad-fs"></a>Análisis de uso de AD FS
Análisis Azure AD Connect Health uso analiza el tráfico de autenticación de Hola de los servidores de federación. Hacer doble clic en cuadro de análisis de uso de hello, tooopen Hola uso hoja de análisis, que muestra varias métricas y agrupaciones.

> [!NOTE]
> toouse análisis de uso con AD FS, debe asegurarse de que está habilitada la auditoría de AD FS. Para obtener más información, consulte [Habilitación de la auditoría para AD FS](active-directory-aadconnect-health-agent-install.md#enable-auditing-for-ad-fs).
>
>

![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health/report1.png)

tooselect otras métricas, especifique un intervalo de tiempo o la agrupación de hello toochange, haga doble clic en el gráfico de análisis de uso de Hola y seleccione Editar gráfico. A continuación, puede especificar el intervalo de tiempo de hello, seleccione una métrica diferente y cambiar la agrupación de Hola. Puede ver la distribución de Hola Hola de tráfico de autenticación según diferentes "métricas" y agrupar cada métrica con los parámetros pertinentes "Agrupar por" descritos en hello pasos de la sección:

**Métrica: número total de solicitudes**: el número total de solicitudes procesadas por los servidores de AD FS.

|Agrupar por | ¿Significado de agrupación de Hola y por qué resulta útil? |
| --- | --- |
| Todo | Muestra el recuento de hello del número total de solicitudes procesadas por todos los servidores de AD FS.|
| Application | Grupos de Hola Nº total de solicitudes en función de usuario de confianza de Hola de destino. Esta agrupación es útil toounderstand qué aplicación está recibiendo qué porcentaje del total de tráfico que Hola. |
|  Server |Número total de solicitudes en función de servidor de Hola que procesa la solicitud de Hola Hola a grupos. Esta agrupación es la distribución de la carga útil toounderstand Hola del tráfico total de Hola.
| Unión al área de trabajo |Grupos de Hola Nº total de solicitudes en función de si proceden de los dispositivos que están unido al área de trabajo (conocidos). Esta agrupación es útil toounderstand si los recursos son accesibles mediante dispositivos de infraestructura de identidad de toohello desconocido. |
|  Método de autenticación | Grupos de Hola Nº total de solicitudes en función de método de autenticación de hello utilizado para la autenticación. Esta agrupación es útil toounderstand Hola método de autenticación común que se utiliza para la autenticación. Siguientes son los métodos de autenticación posibles Hola <ol> <li>Autenticación integrada de Windows (Windows)</li> <li>Autenticación basada en formularios (formularios)</li> <li>SSO (inicio de sesión único)</li> <li>Autenticación de certificados X509 (certificado)</li> <br>Si los servidores de federación Hola reciban solicitud de hello con una Cookie de SSO, dicha solicitud se cuenta como SSO (inicio de sesión único). En estos casos, si Hola cookie es válida, el usuario de hello no se le pedirá las credenciales de tooprovide y obtiene un acceso ininterrumpido toohello aplicación. Este comportamiento es habitual si tiene varios usuarios de confianza protegidos por servidores de federación de Hola. |
| Ubicación de red | Número total de solicitudes en función de la ubicación de red de saludo del usuario de Hola Hola a grupos. Puede ser intranet o extranet. Esta agrupación es útil tooknow qué porcentaje de tráfico de hello procede de intranet de hello frente a extranet. |


**Métrica: Total solicitudes con error** -número total de hello solicitudes con error procesadas por el servicio de federación de Hola. (Esta métrica solo está disponible en AD FS para Windows Server 2012 R2)

|Agrupar por | ¿Significado de agrupación de Hola y por qué resulta útil? |
| --- | --- |
| Tipo de error | Muestra el número de Hola de errores en función de los tipos de error predefinidas. Esta agrupación es útil toounderstand Hola tipos de errores comunes. <ul><li>Nombre de usuario o la contraseña incorrecta: errores debidos tooincorrect username o password.</li> <li>"Bloqueo de la extranet": errores debido a las solicitudes de toohello recibidas de un usuario que se bloqueó de extranet </li><li> "Caducado la contraseña": errores debido a toousers que inicie sesión con una contraseña caducada.</li><li>"Cuenta deshabilitada": errores de vencimiento toousers registro con una cuenta deshabilitada.</li><li>"Autenticación de dispositivos": errores debido a tooauthenticate toousers errores mediante la autenticación de dispositivo.</li><li>"Autenticación de certificado de usuario": errores debido a errores de toousers tooauthenticate debido a un certificado no válido.</li><li>"MFA": errores debido a tooauthenticate toouser errores usando la autenticación multifactor.</li><li>"Otra credencial": "Autorización de emisión": errores debido a errores de tooauthorization.</li><li>"Delegación de emisión": errores debido a errores de delegación de tooissuance.</li><li>"Aceptación de tokens": errores debido a rechazar tooADFS Hola símbolo (token) de un proveedor de identidades de terceros.</li><li>"Protocolo": error debido a errores de tooprotocol.</li><li>"Desconocido": detectar todas. Otros errores que no caben en hello definido por categorías.</li> |
| Server | Grupos de Hola errores basados en servidor hello. Esta agrupación es la distribución de error de hello toounderstand útil entre servidores. Una distribución desigual podría indicar que un servidor presenta un estado defectuoso. |
| Ubicación de red | Grupos de Hola errores basados en la ubicación de red de Hola de solicitudes de hello (intranet frente a extranet). Esta agrupación es útil toounderstand tipo de Hola de solicitudes que se producen errores. |
|  Application | Grupos de Hola errores basadas en aplicación Hola destinada (usuario de confianza). Esta agrupación es útil toounderstand qué aplicación de destino está viendo el número de errores. |

**Métrica: recuento de usuarios**: el número medio de usuarios únicos que se autentican activamente mediante AD FS.

|Agrupar por | ¿Significado de agrupación de Hola y por qué resulta útil? |
| --- | --- |
|Todo |Esta métrica proporciona un recuento del número promedio de usuarios con el servicio de federación de hello en intervalo de tiempo seleccionado de Hola. los usuarios de Hello no están agrupados. <br>promedio de Hello depende de hello intervalo de tiempo seleccionado. |
| Application |Número promedio de Hola de grupos de usuarios en función de Hola dirigió a la aplicación (usuario de confianza). Esta agrupación es útil toounderstand cuántos usuarios usa la aplicación. |

## <a name="performance-monitoring-for-ad-fs"></a>Supervisión del rendimiento de AD FS
Supervisión de rendimiento de Azure AD Connect Health proporciona información de supervisión sobre métricas. Activar la casilla de la supervisión de hello, se abre una nueva hoja con información detallada sobre las métricas de Hola.

![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health/perf1.png)

Si selecciona la opción de filtro de hello en parte superior de Hola de hoja de hello, puede filtrar por servidor toosee métricas de un servidor individual. métrica de toochange, haga doble clic en el gráfico en hello supervisión hoja de supervisión de Hola y seleccione Editar gráfico (o botón Editar gráfico de hello select). De hello nueva hoja que se abre, puede seleccionar métricas adicionales en la lista desplegable de Hola y especificar un intervalo de tiempo para ver los datos de rendimiento de saludo.

## <a name="reports-for-ad-fs"></a>Informes de AD FS
Azure AD Connect Health proporciona informes sobre la actividad y el rendimiento de AD FS. Estos informes ayudan a los administradores a comprender mejor las actividades en sus servidores de AD FS.

### <a name="top-50-users-with-failed-usernamepassword-logins"></a>Primeros 50 usuarios con errores de inicio de sesión por nombre de usuario y contraseña no válidos
Uno de los motivos comunes de Hola para una solicitud de autenticación con errores en un servidor de AD FS es una solicitud con credenciales válidas, es decir, un nombre de usuario incorrecto o una contraseña. Suele suceder toousers debido toocomplex contraseñas, contraseñas olvidadas o errores tipográficos.

Pero hay otras razones por las que pueden dar lugar a un número inesperado de solicitudes está siendo procesado por los servidores de AD FS, como por ejemplo: una aplicación que expiran las credenciales de usuario de las memorias caché y las credenciales de Hola o un usuario malintencionado intente toosign en una cuenta con una serie de contraseñas que conocido. Los dos ejemplos siguientes son motivos válidos que pudieron provocar la sobrecarga de tooa en las solicitudes.

Azure AD Connect Health para AD FS proporciona un informe acerca de los usuarios de 50 primeras con intentos de inicio de sesión fallidos debido tooinvalid username o password. Este informe se logra mediante el procesamiento de eventos de auditoría de hello generados por todos los servidores de AD FS de hello en granjas de servidores de Hola

![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report1a.png)

En este informe tiene toohello un acceso sencillo siguientes fragmentos de información:

* Número total de solicitudes erróneas con el nombre de usuario/contraseña incorrecta en hello últimos 30 días
* Número promedio de usuarios con error de inicio de sesión por nombre de usuario o contraseña incorrectos por día.

Al hacer clic en esta parte, se le toohello hoja de informe principal que se proporciona más detalles. Esta hoja incluye un gráfico con tendencias información toohelp establecer una línea base sobre las solicitudes con el nombre de usuario incorrecto. Además, proporciona Hola lista de los usuarios principales 50 con número de Hola de intentos fallidos.

gráfico de Hello proporciona Hola siguiente información:

* Hola Nº total de inicios de sesión erróneos debido tooa nombre de usuario/contraseña incorrecta en base al día.
* Hola Nº total de usuarios únicos que no se pudo inicios de sesión en base al día.
* Dirección IP del cliente de la última solicitud

![portal de Azure AD Connect Health](./media/active-directory-aadconnect-health-adfs/report3a.png)

informe de Hello proporciona Hola siguiente información:

| Elemento de informe | Description |
| --- | --- |
| Id. de usuario |Muestra el Id. de usuario de Hola que se utilizó. Este valor es qué hello usuario escrito, que en algunos casos es Hola Id. de usuario incorrecto que se va a usar. |
| Intentos con error |Muestra Hola Nº total de intentos con error para dicho Id. de usuario específico Hola tabla está ordenada por hello más número de intentos fallidos en orden descendente. |
| Último error |Muestra la marca de tiempo de hello cuando se produjo el último error de Hola. |
| Última IP con error |Muestra la dirección de IP del cliente de Hola de solicitud incorrecta de hello más reciente. |

> [!NOTE]
> Este informe se actualiza automáticamente después de cada dos horas con hello nueva información recopilada durante este periodo. Como resultado, los intentos de inicio de sesión en hello últimas dos horas no se incluyen en el informe de Hola.
>
>

## <a name="related-links"></a>Vínculos relacionados
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalación del agente de Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operaciones de Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Uso de Azure AD Connect Health para sincronización](active-directory-aadconnect-health-sync.md)
* [Uso de Azure AD Connect Health con AD DS](active-directory-aadconnect-health-adds.md)
* [Preguntas más frecuentes de Azure AD Connect Health](active-directory-aadconnect-health-faq.md)
* [Historial de versiones de Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)