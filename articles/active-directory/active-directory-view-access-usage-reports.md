---
title: aaaView su acceso y uso de informes | Documentos de Microsoft
description: "Explica cómo la informes de uso y acceso tooview toogain visión Hola integridad y la seguridad del directorio de su organización."
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: a074bc4e-cf3f-4ad1-8cc6-4199d2e09ce4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 1c18fd2a327ae8b67f62ce2754f643bdb03514a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="view-your-access-and-usage-reports"></a>Visualización de los informes de acceso y uso
*Esta documentación forma parte del programa Hola a [Azure Active Directory Reporting guía](active-directory-reporting-guide.md).*

Puede usar el acceso de Active Directory de Azure y visibilidad de toogain de informes de uso de integridad de Hola y seguridad del directorio de su organización. Con esta información, administradores de directorios pueden determinar mejor dónde puede haber posibles riesgos de seguridad para que se pueden planificar adecuadamente toomitigate esos riesgos.

Hola Portal de administración de Azure, los informes se clasifican de hello siguientes maneras:

* Informes de anomalías: contienen inicio de sesión de eventos se encuentra toobe anómalos. Nuestro objetivo es toomake, tanto de dicha actividad y le permiten toobe capaz toomake una decisión sobre si un evento es sospechoso.
* Informes de aplicaciones integradas: proporciona información sobre cómo se usan en su organización aplicaciones en la nube. Azure Active Directory ofrece integración con miles de aplicaciones en la nube.
* Informes de errores: indican los errores que pueden surgir al aprovisionar las aplicaciones de tooexternal de cuentas.
* Informes específicos del usuario: muestran los datos de actividad de dispositivo/inicio de sesión para un usuario específico.
* Registros de actividad: contienen un registro de todos los eventos auditados en hello últimos 24 horas, últimos 7 días o últimos 30 días, así como cambios de la actividad de grupo y la actividad de registro y restablecimiento de contraseña.

> [!NOTE]
> * Algunos informes de uso de recursos y de anomalías avanzados solo están disponibles cuando se habilita [Azure Active Directory Premium](active-directory-get-started-premium.md). Informes avanzados le ayudan a mejorar la seguridad de acceso, responder a amenazas de toopotential y obtener acceso tooanalytics sobre el uso de acceso y la aplicación de dispositivo.
> * Azure Active Directory Premium y básicas ediciones están disponibles para los clientes de China mediante Hola instancia internacional de Azure Active Directory. Azure Active Directory Premium y las ediciones básicas no se admiten actualmente en el servicio de Microsoft Azure Hola operado por 21Vianet en China. Para obtener más información, póngase en contacto con nosotros en hello [foro de Azure Active Directory](https://feedback.azure.com/forums/169401-azure-active-directory/).
> 
> 

## <a name="reports"></a>Informes
| Informe | Description |
| --- | --- |
| **Informes de actividades anómalas** | |
| [Inicios de sesión desde orígenes desconocidos](active-directory-reporting-sign-ins-from-unknown-sources.md) |Puede indicar un toosign intento en sin seguimiento. |
| [Inicios de sesión tras varios errores](active-directory-reporting-sign-ins-after-multiple-failures.md) |Puede indicar un ataque por fuerza bruta realizado con éxito. |
| [Inicios de sesión desde varias ubicaciones geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md) |Puede indicar que varios usuarios están iniciando sesión con hello misma cuenta. |
| [Inicios de sesión desde direcciones IP con actividad sospechosa](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md) |Puede indicar un inicio de sesión correcto después de un intento de intrusión sostenido. |
| [Inicios de sesión desde dispositivos posiblemente infectados](active-directory-reporting-sign-ins-from-possibly-infected-devices.md) |Puede indicar un toosign intento en desde dispositivos posiblemente infectados. |
| [Actividad de inicio de sesión irregular](active-directory-reporting-irregular-sign-in-activity.md) |Puede indicar el inicio de sesión de toousers de eventos anómalos en los patrones. |
| [Usuarios con actividad de inicio de sesión erróneo.](active-directory-reporting-users-with-anomalous-sign-in-activity.md) |Indica los usuarios cuyas cuentas se han comprometido. |
| Usuarios con credenciales perdidas |Usuarios con credenciales perdidas |
| **Registros de actividad** | |
| Informe de auditoría |Eventos auditados en el directorio |
| Actividad de restablecimiento de contraseña |Proporciona una vista detallada de los restablecimientos de contraseña que se producen en su organización. |
| Actividad de registro de restablecimiento de contraseñas |Proporciona una vista detallada de los registros de restablecimiento de contraseña que se producen en su organización. |
| Actividad de los grupos de autoservicio |Proporciona un tooall de registro de actividad actividades de autoservicio en el directorio del grupo |
| **Aplicaciones integradas** | |
| Uso de la aplicación |Proporciona un resumen de uso para todas las aplicaciones de SaaS integradas con su directorio. |
| Actividad de aprovisionamiento de cuentas |Proporciona un historial de intentos de las aplicaciones de tooexternal de cuentas de tooprovision. |
| Estado de la sustitución de contraseña |Proporciona información detallada del estado de sustitución automática de contraseñas de aplicaciones SaaS. |
| Errores de aprovisionamiento de cuentas |Indica que las aplicaciones de tooexternal de acceso de toousers un impacto. |
| **Rights management** | |
| Uso de RMS |Proporciona un resumen de uso de Rights Management |
| Usuarios de RMS más activos |Enumera los 1.000 usuarios activos principales que han accedido a archivos protegidos mediante RMS |
| Uso de dispositivos RMS |Enumera los dispositivos utilizados para obtener acceso a los archivos protegidos mediante RMS |
| Uso de aplicaciones habilitadas para RMS |Permite usar aplicaciones habilitadas para RMS |

## <a name="report-editions"></a>Ediciones de los informes
| Informe | Gratuito | Básica | Premium |
| --- | --- | --- | --- |
| **Informes de actividades anómalas** | | | |
| Inicios de sesión desde orígenes desconocidos |✓ |✓  |✓ |
| Inicios de sesión tras varios errores |✓ |✓  |✓ |
| Inicios de sesión desde varias ubicaciones geográficas |✓ |✓  |✓ |
| Inicios de sesión desde direcciones IP con actividad sospechosa | | |✓ |
| Inicios de sesión desde dispositivos posiblemente infectados | | |✓ |
| Actividad de inicio de sesión irregular | | |✓ |
| Usuarios con actividad de inicio de sesión erróneo. | | |✓ |
| Usuarios con credenciales perdidas | | |✓ |
| **Registros de actividad** | | | |
| Informe de auditoría |✓ |✓  |✓ |
| Actividad de restablecimiento de contraseña | | |✓ |
| Actividad de registro de restablecimiento de contraseñas | | |✓ |
| Actividad de los grupos de autoservicio | | |✓ |
| **Aplicaciones integradas** | | | |
| Uso de la aplicación | | |✓ |
| Actividad de aprovisionamiento de cuentas |✓ |✓  |✓ |
| Estado de la sustitución de contraseña | | |✓ |
| Errores de aprovisionamiento de cuentas |✓ |✓  |✓ |
| **Administración de derechos** | | | |
| Uso de RMS | | |Solo RMS |
| Usuarios de RMS más activos | | |Solo RMS |
| Uso de dispositivos RMS | | |Solo RMS |
| Uso de aplicaciones habilitadas para RMS | | |Solo RMS |

## <a name="anomalous-activity-reports"></a>Informes de actividades anómalas
<p>Hola anómalo inicie sesión en los informes de actividad marca sospechosos de inicio de sesión tooOffice365 de actividad, el Portal de administración de Azure, el Panel de acceso de Azure AD, Sharepoint Online, Dynamics CRM Online y otros servicios en línea de Microsoft.</p>

<p>Todos estos informes, excepto Hola informes "Inicios de sesión tras varios errores", también marca sospechosa <i>federado</i> firmar toohello mencionados previamente los servicios ins, independientemente del proveedor de federación de Hola. </p>

<p>Hola siguientes informes está disponible: </p><ul>

<li>[Inicios de sesión desde orígenes desconocidos](active-directory-reporting-sign-ins-from-unknown-sources.md).</li>

<li>[Inicios de sesión tras varios errores](active-directory-reporting-sign-ins-after-multiple-failures.md).</li>

<li>[Inicios de sesión desde varias ubicaciones geográficas](active-directory-reporting-sign-ins-from-multiple-geographies.md).</li>

<li>[Inicios de sesión desde direcciones IP con actividad sospechosa](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md).</li>

<li>[Actividad de inicio de sesión irregular](active-directory-reporting-irregular-sign-in-activity.md).</li>

<li>[Inicios de sesión desde dispositivos posiblemente infectados](active-directory-reporting-sign-ins-from-possibly-infected-devices.md).</li>

<li><seg>
  [Usuarios con actividad de inicio de sesión erróneo](active-directory-reporting-users-with-anomalous-sign-in-activity.md).</seg></li>

<li>Usuarios con credenciales perdidas</li></ul>

## <a name="activity-logs"></a>Registros de actividad
### <a name="audit-report"></a>Informe de auditoría
| Description | Ubicación del informe |
|:--- |:--- |
| Muestra un registro de todos los eventos auditados en hello últimas 24 horas, los últimos 7 días o los últimos 30 días. <br /> Para obtener más información, consulte [Eventos del informe de auditoría de Azure Active Directory](active-directory-reporting-audit-events.md) |Directorio > pestaña Informes |

![Informe de auditoría](./media/active-directory-view-access-usage-reports/auditReport.PNG)

### <a name="password-reset-activity"></a>Actividad de restablecimiento de contraseña
| Description | Ubicación del informe |
|:--- |:--- |
| Muestra los intentos de restablecimiento de contraseña que se han producido en su organización. |Directorio > pestaña Informes |

![Actividad de restablecimiento de contraseña](./media/active-directory-view-access-usage-reports/passwordResetActivity.PNG)

### <a name="password-reset-registration-activity"></a>Actividad de registro de restablecimiento de contraseñas
| Description | Ubicación del informe |
|:--- |:--- |
| Muestra los registros de restablecimiento de contraseña que se han producido en su organización. |Directorio > pestaña Informes |

![Actividad de registro de restablecimiento de contraseñas](./media/active-directory-view-access-usage-reports/passwordResetRegistrationActivity.PNG)

### <a name="self-service-groups-activity"></a>Actividad de los grupos de autoservicio
| Description | Ubicación del informe |
|:--- |:--- |
| Muestra toda la actividad de los grupos administrados de autoservicio de hello en el directorio. |Directorio > Usuarios > <i>Usuario</i> > pestaña Dispositivos |

![Actividad de los grupos de autoservicio](./media/active-directory-view-access-usage-reports/selfServiceGroupsActivity.PNG)

## <a name="integrated-applications-reports"></a>Informes de aplicaciones integradas
### <a name="application-usage-summary"></a>Uso de la aplicación: resumen
| Description | Ubicación del informe |
|:--- |:--- |
| Utilice este informe cuando desee toosee uso para todas las aplicaciones de SaaS hello en el directorio. Este informe se basa en número de Hola de veces que los usuarios hacen clic en la aplicación Hola Hola Panel de acceso. |Directorio > pestaña Informes |

Este informe incluye inicios de sesión demasiado*todos los* acceder las aplicaciones que tiene su directorio, incluidas las aplicaciones previamente integradas de Microsoft.

Las aplicaciones previamente integradas de Microsoft incluyen Office 365, Sharepoint, Hola Portal de administración de Azure y otros usuarios.

![Resumen de uso de la aplicación](./media/active-directory-view-access-usage-reports/applicationUsage.PNG)

### <a name="application-usage-detailed"></a>Uso de la aplicación: detallado
| Description | Ubicación del informe |
|:--- |:--- |
| Utilice este informe cuando desee toosee cuánto una aplicación SaaS específica está usándola. Este informe se basa en número de Hola de veces que los usuarios hacen clic en la aplicación Hola Hola Panel de acceso. |Directorio > pestaña Informes |

### <a name="application-dashboard"></a>Panel de la aplicación
| Description | Ubicación del informe |
|:--- |:--- |
| Este informe indica la aplicación de toohello de inicios de sesión acumulativos por los usuarios de su organización, en un intervalo de tiempo seleccionado. gráfico de Hello en la página del panel Hola le ayudará a identificar las tendencias de uso general de la aplicación. |Directorio > Aplicación > pestaña Panel |

## <a name="error-reports"></a>Informes de errores
### <a name="account-provisioning-errors"></a>Errores de aprovisionamiento de cuentas
| Description | Ubicación del informe |
|:--- |:--- |
| Usar este toomonitor los errores que se producen durante la sincronización de Hola de cuentas desde las aplicaciones de SaaS tooAzure Active Directory. |Directorio > pestaña Informes |

![Errores de aprovisionamiento de cuentas](./media/active-directory-view-access-usage-reports/accountProvisioningErrors.PNG)

## <a name="user-specific-reports"></a>Informes específicos del usuario
### <a name="devices"></a>Dispositivos
| Description | Ubicación del informe |
|:--- |:--- |
| Utilice este informe cuando desee dirección IP de toosee hello y la ubicación geográfica de los dispositivos que un usuario determinado ha usado tooaccess Azure Active Directory. |Directorio > Usuarios > <i>Usuario</i> > pestaña Dispositivos |

### <a name="activity"></a>Actividad
| Description | Ubicación del informe |
|:--- |:--- |
| Muestra el inicio de sesión de hello en actividad para un usuario. Hola informe incluye información como la aplicación hello iniciado sesión en, dispositivo utilizado, dirección IP y ubicación. No recopilamos el historial de Hola para los usuarios que inician sesión con una cuenta de Microsoft. |Directorio > Usuarios > <i>Usuario</i> > pestaña Actividad |

#### <a name="sign-in-events-included-in-hello-user-activity-report"></a>Inicie sesión en los eventos incluidos en hello informe actividad del usuario
Solo determinados tipos de eventos de inicio de sesión aparecerá en hello informe actividad del usuario.

| Tipo de evento | ¿Se incluye? |
| --- | --- |
| Toohello de inicios de sesión [Panel de acceso](http://myapps.microsoft.com/) |Sí |
| Iniciar sesión ins toohello [Portal de administración de Azure](https://manage.windowsazure.com/) |Sí |
| Iniciar sesión ins toohello [Portal de Microsoft Azure](https://portal.azure.com/) |Sí |
| Iniciar sesión ins toohello [portal de Office 365](http://portal.office.com/) |Sí |
| Firmar ins aplicación nativa de tooa, como Outlook (consulte la excepción siguiente) |Sí |
| Firmar ins tooa federada de aprovisionar la aplicación a través del Panel de acceso, como Salesforce Hola |Sí |
| Firmar ins tooa basado en contraseña aplicación a través del Panel de acceso, como Twitter Hola |Sí |
| Inicio de sesión inicios tooa empresarial personalizada aplicación que se ha agregado toohello directory |No (próximamente) |
| Firmar la aplicación del Proxy de aplicación de Azure AD de tooan de complementos que se ha agregado toohello directory |No (próximamente) |

> Nota: cantidad de hello tooreduce de ruido en este informe, inicios de sesión por hello [Microsoft Online Services Sign-In Assistant](http://community.office365.com/en-us/w/sso/534.aspx) no se muestran.
> 
> 

## <a name="things-tooconsider-if-you-suspect-security-breach"></a>Cosas tooconsider si sospecha una infracción de seguridad
Si sospecha que una cuenta de usuario puede suponer un riesgo o cualquier tipo de actividad del usuario sospechosa que puede provocar tooa infracción de seguridad de los datos del directorio en la nube de hello, puede que desee tooconsider uno o más de hello siguientes acciones:

* Póngase en contacto con actividad de hello usuario tooverify Hola
* Restablecer la contraseña del usuario de Hola
* [Habilite Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md) para obtener seguridad adicional

## <a name="view-or-download-a-report"></a>Visualización o descarga de un informe
1. Hola portal de Azure clásico, haga clic en **Active Directory**, haga clic en nombre de hello del directorio de su organización y, a continuación, haga clic en **informes**.
2. En la página de informes de hello, haga clic en informe de Hola que desee tooview o descargar.
   
   > [!NOTE]
   > Si se trata de hello primera vez que usa Hola reporting característica de Azure Active Directory, verá un tooOpt de mensaje en. Si los acepta, haga clic en toocontinue de icono de marca de verificación de Hola.
   > 
   > 
3. Haga clic en tooInterval siguiente del menú desplegable de hello y, a continuación, seleccione uno de hello después los intervalos de tiempo que deben usarse para generar el informe:
   
   * Últimas 24 horas
   * Últimos 7 días
   * Últimos 30 días
4. Haga clic en informe de hello marca de verificación icono toorun Hola.
   * Seguridad too1000 eventos se mostrará en hello portal de Azure clásico.
5. Si procede, haga clic en **descargar** toodownload Hola informe tooa archivo comprimido en formato de valores separados por comas (CSV) para verlo sin conexión o con fines de archivado.
   * Seguridad too75, 000 eventos se incluirán en el archivo hello descargado.
   * Para obtener más datos, visite hello [API Reporting de Azure AD](active-directory-reporting-api-getting-started.md).

## <a name="ignore-an-event"></a>Ignorar un evento
Si está viendo informes de anomalías, observará que puede ignorar varios eventos que se muestran en informes relacionados. tooignore un evento, basta con resaltar eventos hello en el informe de hello y, a continuación, haga clic en **omitir**. Hola **omitir** botón quitará de forma permanente evento resaltado Hola de informe de Hola y solo puede usarse por los administradores globales con licencia.

## <a name="automatic-email-notifications"></a>Notificaciones de correo electrónico automáticas
Para obtener más información sobre las notificaciones de informes de Azure AD, consulte [Notificaciones de informes de Azure Active Directory](active-directory-reporting-notifications.md).

## <a name="whats-next"></a>Pasos siguientes
* [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Agregar marcas tooyour páginas de inicio de sesión y Panel de acceso de empresa](active-directory-add-company-branding.md)

