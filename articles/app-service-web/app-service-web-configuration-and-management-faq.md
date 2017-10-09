---
title: "aaaConfiguration preguntas más frecuentes para aplicaciones web de Azure | Documentos de Microsoft"
description: "Obtener toofrequently respuestas preguntas más frecuentes sobre problemas de administración y configuración para la característica de las aplicaciones Web de Hola de servicio de aplicaciones de Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Preguntas más frecuentes sobre la configuración y administración de Web Apps en Azure

Este artículo tiene toofrequently respuestas preguntas frecuentes (P+f) sobre los problemas de configuración y administración de hello [característica de las aplicaciones Web de servicio de aplicaciones de Azure](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>¿Existen limitaciones que debo tener en cuenta si deseo usar recursos de servicio de aplicaciones de toomove?

Si tiene previsto toomove servicio de aplicaciones recursos tooa nuevo grupo de recursos o suscripción, hay algunas de las limitaciones toobe en cuenta. Para más información, consulte [Limitaciones de App Service](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>¿Cómo se usa un nombre de dominio personalizado para una aplicación web?

Para respuestas toocommon preguntas sobre el uso de un nombre de dominio personalizado con la aplicación web de Azure, vea nuestro vídeo siete minutos [agregar un nombre de dominio personalizado](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Hola vídeo ofrece un tutorial sobre cómo tooadd un nombre de dominio personalizado. Describe cómo toouse su propia dirección URL en lugar de Hola *. azurewebsites.net URL con la aplicación de servicio de aplicaciones web. También puede ver un tutorial detallado de [cómo toomap un nombre de dominio personalizado](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>¿Cómo se compra un nuevo dominio personalizado para una aplicación web?

toolearn toopurchase y configurar un dominio personalizado para la aplicación de servicio de aplicaciones web, vea [comprar y configurar un nombre de dominio personalizado en el servicio de aplicaciones](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>¿Cómo se carga y configura un certificado SSL existente para una aplicación web?

toolearn tooupload y configurar un certificado SSL personalizado existente, vea [enlazar una aplicación existente de personalizado SSL certificado tooan web de Azure](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>¿Cómo se compra y configura un nuevo certificado SSL en Azure para una aplicación web?

toolearn toopurchase y configurar un certificado SSL para la aplicación de servicio de aplicaciones web, vea [agregar un tooyour de certificado SSL aplicación de servicio de aplicaciones](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>¿Cómo se mueven los recursos de Application Insights?

Actualmente, visión de la aplicación de Azure no admite la operación de movimiento de Hola. Si su grupo de recursos original incluye un recurso de Application Insights, no puede mover ese recurso. Si incluye recursos de Application Insights de hello cuando intente toomove una aplicación de servicio de aplicaciones, Hola todo Mover operación provocará un error. Sin embargo, hello plan no es necesario toobe en el servicio de aplicaciones y Application Insights Hola mismo grupo de recursos como aplicación hello para hello aplicación toofunction correctamente.

Para más información, consulte [Limitaciones de App Service](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>¿Dónde puedo encontrar una lista de comprobación guía y aprender más sobre las operaciones de movimiento de recursos?

[Limitaciones de servicio de aplicaciones](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) muestra cómo toomove recursos tooeither un nuevo recurso nueva suscripción o tooa grupo Hola misma suscripción. Puede obtener información acerca de la lista de comprobación de movimiento de recursos de hello, obtenga información acerca de los servicios que admiten la operación de movimiento de Hola y obtener más información sobre las limitaciones del servicio de aplicaciones y otros temas relacionados.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>¿Cómo se puede establecer zona horaria del servidor hello para mi aplicación web?

zona de horaria del servidor de hello tooset para la aplicación web:

1. En el portal de Azure, en su suscripción de servicio de aplicaciones, Hola vaya toohello **configuración de la aplicación** menú.
2. En **Configuración de la aplicación**, agregue este valor:
    * Clave = WEBSITE_TIME_ZONE
    * Valor = *zona horaria de Hola que desee*
3. Seleccione **Guardar**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>¿Por qué mis trabajos web continuos en ocasiones dan error?

De forma predeterminada, las aplicaciones web se descargan si están inactivas durante algún tiempo. Esto permite que el sistema de hello conservar los recursos. En los planes de básico y estándar, puede activar hello **Always On** configuración de aplicación web de tookeep hello cargado todo el tiempo Hola. Si la aplicación web ejecuta trabajos Web continuos, debe activar **Always On**, u Hola trabajos Web no puede ejecutarse de forma confiable. Para más información, consulte [Creación de un trabajo web de ejecución continua](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>¿Cómo se puede obtener dirección IP de la salida Hola para mi aplicación web?

lista de hello tooget de salida de direcciones IP de la aplicación web:

1. Hola portal de Azure, en la hoja de la aplicación web, ir toohello **propiedades** menú.
2. Busque **direcciones ip de salida**.

aparece en la lista de Hola de direcciones IP salientes.

Si su sitio Web se hospeda en el entorno del servicio de aplicación para PowerApps, toolearn cómo tooget la dirección IP de salida, consulte [direcciones de red saliente](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>¿Cómo se obtiene una dirección IP de entrada reservada o dedicada para una aplicación web?

tooset una dirección IP dedicada o reservados para las llamadas entrantes realizadas sitio Web de aplicación de Azure de tooyour, instalar y configurar un certificado SSL basado en IP.

Tenga en cuenta que toouse dedicada o una dirección IP reservada para las llamadas entrantes, el plan de servicio de aplicaciones debe estar en un plan de servicio básico o superior.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>¿Puedo exportar mi toouse de certificado de servicio de aplicaciones fuera de Azure, como el caso de un sitio Web hospedado en otro lugar? 

Los certificados de App Service se consideran recursos de Azure. No están previsto toouse fuera de los servicios de Azure. No se puede exportarlos toouse fuera de Azure. Para más información, consulte las [preguntas más frecuentes sobre los dominios personalizados y los certificados de App Service](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>¿Se pueden exportar mi toouse de certificado de servicio de aplicaciones con otros servicios de nube de Azure?

portal de Hello proporciona una experiencia de primera clase para implementar un certificado de servicio de aplicaciones a través de aplicaciones de servicio de almacén de claves de Azure tooApp. Sin embargo, nos hemos haya recibido las solicitudes de clientes toouse estos certificados fuera Hola plataforma de servicio de aplicaciones, por ejemplo, con máquinas virtuales de Azure. toolearn cómo toocreate una copia local de PFX del servicio en la aplicación de certificado para que pueda usar el certificado de hello con otros recursos de Azure, consulte [crear una copia local de PFX de un certificado de servicio de aplicaciones](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Para más información, consulte las [preguntas más frecuentes sobre los dominios personalizados y los certificados de App Service](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>¿Por qué veo mensajes de bienvenida "Parcialmente correcta" cuando intento tooback seguridad de mi aplicación web?

Una causa común de errores de copia de seguridad es que algunos archivos están en uso por la aplicación hello. Archivos que están en uso se bloquean mientras se realiza la copia de seguridad de Hola. Como consecuencia, no se puede hacer una copia de seguridad de ellos y podría aparecer el estado "Realizado parcialmente". Puede potencialmente evitar que esto suceda si excluye archivos del proceso de copia de seguridad de Hola. Puede elegir tooback seguridad solo lo necesario. Para obtener más información, consulte [simplemente Hola partes importantes de su sitio con aplicaciones web de Azure de copia de seguridad](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>¿Cómo se puede quitar un encabezado de respuesta HTTP Hola?

encabezados de hello tooremove de hello respuesta HTTP, actualizar el archivo web.config de sitio. Para más información, consulte [Remove standard server headers on your Azure websites](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/) (Eliminación de encabezados de servidor estándar en los sitios web de Azure).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>¿Es compatible App Service con el Estándar de PCI 3.0 y 3.1?

Actualmente, características de las aplicaciones Web de Hola de servicio de aplicaciones de Azure es conforme a la versión de seguridad estándar de PCI datos (DSS) 3.0 de nivel 1. La versión 3.1 de PCI DSS está en nuestros planes. Planificación ya está en curso para la adopción del estándar más reciente de hello continuará.

Para la certificación de la versión 3.1 de PCI DSS es necesario deshabilitar la versión 1.0 del protocolo Seguridad de la capa de transporte (TLS). En la actualidad, la deshabilitación de TLS 1.0 no es una opción en la mayoría de los planes de App Service. Sin embargo, si usa el entorno del servicio de aplicación o están dispuesto toomigrate su entorno de servicio de carga de trabajo tooApp, puede obtener un mayor control de su entorno. Para ello, es necesario deshabilitar TLS 1.0 con la ayuda del soporte técnico de Azure. Hola futuro próximo, tenemos previsto toomake estos toousers accesible de configuración.

Para más información, consulte el artículo sobre el [cumplimiento de las aplicaciones web de Microsoft Azure App Service con el Estándar de PCI 3.0 y 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>¿Cómo se usa Hola entorno y ranuras de implementación de ensayo?

En los planes Standard y Premium servicio de aplicaciones, cuando se implementa la tooApp de aplicación web servicio, puede implementar tooa ranura de implementación independiente en lugar de la ranura de producción de toohello predeterminada. Los espacios de implementación son aplicaciones web activas que tienen sus propios nombres de host. Elementos de contenido y la configuración de aplicación Web se pueden intercambiar entre dos ranuras de implementación, incluida la zona de producción de hello.

Para más información sobre el uso de las ranuras de implementación, consulte [Configuración de entornos de ensayo en Azure App Service](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>¿Cómo se accede y se revisan registros de WebJob?

registros de trabajo Web de tooreview:

1. Inicie sesión en tooyour [sitio Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Seleccione Hola trabajo Web.
3. Seleccione hello **alternar salida** botón.
4. archivo de salida de hello toodownload, seleccione hello **descargar** vínculo.
5. Para ejecuciones individuales, seleccione **Individual Invoke** (Invocación individual).
6. Seleccione hello **alternar salida** botón.
7. Vínculo de descarga de hello SELECT.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Estoy tratando de toouse híbrida conexiones con SQL Server. ¿Por qué veo un mensaje de saludo "System.OverflowException: operación aritmética ha provocado un desbordamiento"?

Si utiliza conexiones híbridas tooaccess SQL Server, una actualización de Microsoft .NET de 10 de mayo de 2016, puede producir conexiones toofail. Puede que aparezca este mensaje:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Resolución

Estamos trabajando tooupdate toofix de administrador de conexiones híbridas este problema. Si desea conocer soluciones alternativas, consulte [Hybrid Connections error with SQL Server: System.OverflowException: Arithmetic operation resulted in an overflow](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/) (Error de conexiones híbridas con SQL Server: System.OverflowException: la operación aritmética ha provocado un desbordamiento).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>¿Cómo se agrega o edita una regla de reescritura de direcciones URL?

tooadd o editar una regla de reescritura de direcciones URL:

1. Configurar el Administrador de Internet Information Services (IIS) para que se conecte tooyour aplicación de servicio de aplicaciones web. toolearn tooconnect servicio tooApp el Administrador de IIS, vea [administración remota de sitios Web de Azure mediante el Administrador de IIS](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. En el Administrador de IIS, agregue o edite una regla de reescritura de direcciones URL. toolearn cómo tooadd o vuelva a escribir una dirección URL de editar regla, consulte [módulo de reescritura para crear reglas de reescritura de dirección URL de hello](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>¿Cómo se puede controlar el tráfico entrante tooApp servicio?

En el nivel de sitio de hello, tienes dos opciones para controlar el tráfico entrante tooApp servicio:

* Activar las restricciones de IP dinámicas. toolearn tooturn en restricciones de IP dinámicas, vea [restricciones de IP y dominio para sitios Web de Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Active Module Security. toolearn tooturn en el módulo de seguridad, vea [ModSecurity firewall de aplicación web en sitios Web de Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Si usa App Service Environment, puede emplear el [firewall de Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>¿Cómo se bloquean los puertos en una aplicación web de App Service?

Hola servicio de aplicaciones compartidas entorno inquilinos, no es posible tooblock determinados puertos debido a la naturaleza de saludo de la infraestructura de Hola. Los puertos TCP 4016, 4018 y 4020 podrían estar también abiertos para la depuración remota de Visual Studio.

En App Service Environment, dispone de control total sobre el tráfico de entrada y de salida. Puede usar puertos específicos de grupos de seguridad de red toorestrict o bloque. Para más información sobre App Service Environment, consulte [Introducing App Service Environment](https://azure.microsoft.com/blog/introducing-app-service-environment/) (Introducción a App Service Environment).

## <a name="how-do-i-capture-an-f12-trace"></a>¿Cómo se captura un seguimiento F12?

Para capturar un seguimiento F12, tiene dos opciones:

* Seguimiento HTTP de F12
* Salida de consola de F12

### <a name="f12-http-trace"></a>Seguimiento HTTP de F12

1. En Internet Explorer, vaya el sitio Web de tooyour. Es importante toosign antes de Hola pasos siguientes. En caso contrario, Hola F12 seguimiento captura datos confidenciales en el inicio de sesión.
2. Presione F12.
3. Compruebe que hello **red** ficha está seleccionada y, a continuación, seleccione Hola verde **reproducir** botón.
4. Hola pasos que reproducen el problema de Hola.
5. Seleccione Hola rojo **detener** botón.
6. Seleccione hello **guardar** botón (icono de disco) y guarde el archivo HAR de hello (en Internet Explorer y borde) *o* (ratón) en el archivo HAR de hello y, a continuación, seleccione **Guardar como HAR con contenido** () en Chrome).

### <a name="f12-console-output"></a>Salida de consola de F12

1. Seleccione hello **consola** ficha.
2. De cada pestaña que contiene elementos de mayor que cero, seleccione tabulador de hello (**Error**, **advertencia**, o **información**). Si no está seleccionada la ficha de hello, icono de pestaña hello es gris o en negro cuando se mueve el cursor de hello fuera de él.
3. Haga clic en el área de mensajes de Hola del panel de hello y, a continuación, seleccione **copiar todo**.
4. Hola pegar copiar texto en un archivo y, a continuación, guarde el archivo hello.

un archivo HAR tooview, puede usar hello [Visor HAR](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>¿Por qué obtengo un error cuando intento tooconnect un servicio de aplicación web aplicación tooa red virtual que esté conectado tooExpressRoute?

Si se trata de una red virtual de tooa de aplicación de web de Azure que se ha conectado tooAzure ExpressRoute tooconnect, se produce un error. aparece Hello siguiente mensaje: "Puerta de enlace no es una puerta de enlace VPN".

Actualmente, no puede tener point-to-site VPN conexiones tooa red virtual que esté conectado tooExpressRoute. Point-to-site VPN y ExpressRoute no pueden coexistir para hello misma red virtual. Para más información, consulte [Límites y limitaciones de ExpressRoute y las conexiones VPN de sitio a sitio](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>¿Cómo se puede conectar una servicio de aplicaciones web app tooa red virtual que tiene un enrutamiento (basada en directivas) puerta de enlace estática?

Actualmente, no se admite la conexión a una servicio de aplicaciones web app tooa red virtual que tiene un enrutamiento (basada en directivas) puerta de enlace estática. Si la red virtual de destino ya existe, debe tener VPN de sitio a punto habilitada, con una puerta de enlace de enrutamiento dinámico, antes de que puede ser aplicación tooan conectado. Si la puerta de enlace se establece toostatic enrutamiento, no se puede habilitar una VPN de sitio a punto. 

Para más información, consulte [Integración de su aplicación con una red virtual de Azure](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>En App Service Environment, ¿por qué solo se puede crear un plan de App Service si tengo dos trabajos disponibles?

tooprovide tolerancia a errores, el entorno del servicio de aplicaciones requiere que cada grupo de trabajo necesita al menos un recurso de proceso adicional. recurso de proceso adicional de Hello no se puede asignar una carga de trabajo.

Para obtener más información, consulte [cómo toocreate un entorno de servicio de aplicaciones](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>¿Por qué veo los tiempos de espera cuando intento toocreate un entorno de servicio de aplicaciones?

En ocasiones, la creación de una instancia de App Service Environment produce error. En ese caso, vea Hola tras error en hello que registros de actividad:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve esto, asegúrese de que ninguno de hello condiciones siguientes son ciertas:
* subred de Hello es demasiado pequeño.
* Hola subred no está vacía.
* ExpressRoute evita que los requisitos de conectividad de red de Hola de un entorno de servicio de aplicaciones.
* Un grupo de seguridad de red incorrecta evita que los requisitos de conectividad de red de Hola de un entorno de servicio de aplicaciones.
* La tunelización forzada esté activada.

Para más información, consulte [Frequent issues when deploying (creating) a new Azure App Service Environment](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/) (Problemas frecuentes al implementar [crear] una nueva instancia de Azure App Service Environment).

## <a name="why-cant-i-delete-my-app-service-plan"></a>¿Por qué no puedo eliminar mi plan de App Service?

No se puede eliminar un plan de servicio de aplicaciones si las aplicaciones de servicio de aplicaciones están asociadas con hello plan de servicio de aplicaciones. Antes de eliminar un plan de servicio de aplicaciones, quite todas las aplicaciones de servicio de aplicaciones asociadas de hello plan de servicio de aplicaciones.

## <a name="how-do-i-schedule-a-webjob"></a>¿Cómo se programa un trabajo web?

Puede crear un trabajo web programado mediante expresiones Cron:

1. Cree un archivo settings.job.
2. En este archivo JSON, incluya una propiedad de programación mediante una expresión Cron: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Para más información sobre los trabajos web programados, consulte [Creación de un trabajo web programado utilizando una expresión CRON](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>¿Cómo se realizan pruebas de penetración para una aplicación de App Service?

pruebas de penetración tooperform, [enviar una solicitud de](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>¿Cómo se configura un nombre de dominio personalizado para una aplicación web de App Service que usa Traffic Manager?

toolearn toouse un nombre de dominio personalizado con una aplicación de servicio de aplicaciones que utiliza Azure Traffic Manager para el equilibrio de carga, vea [configurar un nombre de dominio personalizado para una aplicación web de Azure con el Administrador de tráfico](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>El certificado de App Service está marcado como fraudulento. ¿Cómo se resuelve este problema?

Durante la comprobación del dominio Hola de una compra de certificado de servicio de aplicaciones, puede aparecer el siguiente mensaje de Hola:

"Su certificado se ha marcado por posible fraude. solicitud de Hello está actualmente en proceso de revisión. Si el certificado de hello no queda utilizable dentro de 24 horas, póngase en contacto con soporte técnico de Azure."

Como indica el mensaje de bienvenida, este proceso de comprobación de fraude podría tardar hasta too24 horas toocomplete. Durante este tiempo, continuará toosee mensaje de saludo.

Si el certificado de servicio de aplicaciones continúa tooshow este mensaje después de 24 horas, vuelva a ejecutar Hola siguiente script de PowerShell. Hola de contactos de script de Hola [proveedor de certificados](https://www.godaddy.com/) directamente el problema de hello tooresolve.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>¿Cómo funciona la autenticación y la autorización en App Service?

Para obtener documentación detallada sobre la autenticación y la autorización en App Service, consulte [Seguridad de App Service](../app-service/app-service-security-readme.md). documentación de Hello también encontrará información acerca de cómo configurar el servicio de aplicaciones toouse distintos identifican los inicios de sesión de proveedor:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Cuenta Microsoft](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>¿Cómo se puede redirigir predeterminado Hola *. dominio personalizado de la aplicación de azurewebsites.net dominio toomy web de Azure?

Cuando se crea un nuevo sitio Web mediante el uso de aplicaciones Web en Azure, el valor predeterminado es *sitename*. azurewebsites.net se asigna tooyour sitio. Si agrega un sitio de tooyour de nombre de host personalizado y no desea que los usuarios toobe capaz de tooaccess predeterminado *. dominio azurewebsites.net, puede redirigir la dirección URL predeterminada de Hola. toolearn cómo tooredirect todo el tráfico procedente predeterminado dominio tooyour dominio personalizado de su sitio Web, consulte [redirección Hola predeterminado dominio tooyour dominio personalizado en aplicaciones web de Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>¿Cómo se determina qué versión de .NET está instalada en App Service?

Hola más rápida forma toofind Hola versión de Microsoft .NET que está instalado en el servicio de aplicación es mediante la consola de Kudu Hola. Puede tener acceso a consola de hello Kudu desde el portal de Hola o mediante el uso de la dirección URL de saludo de la aplicación de servicio de aplicaciones. Para obtener instrucciones detalladas, consulte [determinar la versión de .NET Hola instalado en el servicio de aplicaciones](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>¿Por qué no funciona el escalado automático según lo previsto?

Si no se ha escalado escalado automático de Azure en o escalar horizontalmente la instancia de aplicación web de hello según lo esperado, es posible que esté ejecutando en un escenario en el que intencionadamente elegimos no tooscale tooavoid un bucle infinito debido demasiado "oscilante". Esto suele suceder cuando no hay un margen suficiente entre los umbrales de escalado horizontal y escalado en Hola. toolearn tooavoid "oscilante" y tooread sobre otras prácticas recomendadas de escalado automático, vea [prácticas recomendadas de escalado automático](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>¿Por qué a veces el escalado automático solo escala parcialmente?

El escalado automático se desencadena cuando las métricas superan los límites previamente configurados. En ocasiones, puede observar que capacidad Hola se rellena solo parcialmente toowhat comparado que esperaba. Esto puede ocurrir cuando el número de Hola de instancias que desea no está disponible. En ese caso, escalado automático parcialmente se rellena con número disponibles de Hola de instancias. Escalado automático, a continuación, ejecuta Hola equilibra lógica tooget más capacidad. Asigna Hola restantes instancias. Tenga en cuenta que esta operación puede tardar unos minutos.

Si no ve el número esperado de Hola de instancias después de unos minutos, es posible que el relleno parcial Hola era suficiente métricas de hello toobring dentro de los límites de Hola. O bien, escalado automático puede haber reducida porque ha alcanzado el límite inferior de las métricas de Hola.

Si ninguna de estas condiciones se aplican y Hola problema persiste, envíe una solicitud de soporte técnico.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>¿Cómo se activa la compresión HTTP para el contenido?

tooturn de compresión para los tipos de contenido estáticos y dinámicos, agregue Hola el archivo web.config de nivel de aplicación de código toohello siguiente:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

También puede especificar dinámicas específicas de Hola y tipos de MIME estático que desea toocompress. Para obtener más información, consulte la pregunta de foro de respuesta tooa de [httpCompression configuración en un sitio Web de Azure simple](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>¿Cómo migrar desde una tooApp del entorno local servicio?

toomigrate sitios de Windows y Linux tooApp de servidores web servicio, puede usar Azure aplicación servicio Migration Assistant. herramienta de migración de Hello crea aplicaciones web y bases de datos de Azure según sea necesario y, a continuación, publica contenido Hola. Para más información, consulte [Azure App Service Migration Assistant](https://www.movemetothecloud.net/).
