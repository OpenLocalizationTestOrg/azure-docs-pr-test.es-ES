---
title: aaaWork existente local servidores proxy y Azure AD | Documentos de Microsoft
description: "Explica cómo toowork existente local servidores proxy."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: kgremban
ms.openlocfilehash: 7f8cec4f676f99bead5211bcbcf23056bd7f211f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="work-with-existing-on-premises-proxy-servers"></a>Trabajo con servidores proxy locales existentes

Este artículo se explica cómo tooconfigure toowork de conectores de Proxy de aplicación de Azure Active Directory (Azure AD) con los servidores proxy de salida. Está destinado a clientes con entornos de red que tienen servidores proxy en la actualidad.

Empezaremos examinando estos escenarios de implementación principales:
* Configure conectores toobypass el proxy de salida local.
* Configure conectores toouse un Proxy de aplicación de Azure AD tooaccess de proxy de salida.

Para más información sobre cómo funcionan los conectores, consulte [Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md).

## <a name="configure-hello-outbound-proxy"></a>Configurar el proxy de salida de hello

Si tiene un proxy de salida en su entorno, use una cuenta con proxy de salida de los permisos adecuados tooconfigure Hola. Como instalador de Hola se ejecuta en el contexto de Hola Hola del usuario de que está realizando la instalación de hello, puede comprobar configuración hello mediante Microsoft Edge u otro explorador de Internet.

configuración de proxy de hello tooconfigure con Microsoft Edge:

1. Vaya demasiado**configuración** > **configuración de vista avanzada** > **abrir la configuración de Proxy** > **Manual de instalación del Proxy** .
2. Establecer **utilizar un servidor proxy** demasiado**en**, seleccione hello **no usar servidor proxy de Hola para direcciones locales (intranet)** casilla de verificación y, a continuación, tooreflect de dirección y el puerto de Hola de cambio el servidor proxy local.
3. Rellene la configuración de proxy necesaria de Hola.

   ![Cuadro de diálogo de configuración del proxy](./media/application-proxy-working-with-proxy-servers/proxy-bypass-local-addresses.png)

## <a name="bypass-outbound-proxies"></a>Omisión de servidores proxy de salida

Los conectores tienen componentes del sistema operativo subyacentes que realizan solicitudes salientes. Estos componentes intentan automáticamente toolocate un servidor proxy de red de Hola. Usan la detección automática de Proxy Web (WPAD), si está habilitado en el entorno de Hola.

componentes del sistema operativo Hola intenten toolocate un servidor proxy llevando a cabo una búsqueda de DNS para wpad.domainsuffix. Si esto se resuelve en DNS, una solicitud HTTP, a continuación, se realiza toohello IP dirección wpad.dat. Esta solicitud se convierte en el script de configuración de proxy de hello en su entorno. Conector de Hello usa este tooselect script un servidor proxy de salida. Sin embargo, tráfico de conector es posible que todavía no vaya a través, debido a una configuración adicionales necesaria en el proxy de Hola.

Puede configurar Hola conector toobypass su tooensure de proxy local que usa dirigir conectividad toohello Azure servicios. Se recomienda este enfoque (si lo permite la directiva de red para él), ya que significa que tiene una menor toomaintain de configuración.

toodisable uso de proxy de salida para conector de hello, Editar archivo C:\Program Files\Microsoft AAD aplicación Proxy Connector\ApplicationProxyConnectorService.exe.config de hello y agregue hello *system.net* sección se muestra en este ejemplo de código :

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>
    <defaultProxy enabled="false"></defaultProxy>
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```
tooensure que el servicio de conector actualizador de hello también omite proxy hello, cree un archivo de ApplicationProxyConnectorUpdaterService.exe.config de toohello de cambio similar situado actualizador del conector del Proxy de aplicación C:\Program Files\Microsoft AAD.

Ser seguro toomake copias de archivos originales de hello, por si necesita archivos .config de toorevert toohello de forma predeterminada.

## <a name="use-hello-outbound-proxy-server"></a>Utilizar un servidor proxy saliente Hola

Algunos entornos requieren que todos los toogo el tráfico saliente a través de un proxy de salida, sin excepción. Como resultado, la omisión de proxy de hello no es una opción.

Puede configurar Hola conector tráfico toogo a través de proxy de salida de hello, como se muestra en hello siguiente diagrama:

 ![Configuración de conector toogo de tráfico a través de un tooAzure de proxy de salida AD Proxy de aplicación](./media/application-proxy-working-with-proxy-servers/configure-proxy-settings.png)

Como resultado de tener solo el tráfico saliente, no hay ninguna necesidad de tooconfigure acceso a través de los firewalls de entrada.

### <a name="step-1-configure-hello-connector-and-related-services-toogo-through-hello-outbound-proxy"></a>Paso 1: Configurar el conector de Hola y relacionados con servicios toogo a través de proxy de salida de hello

Tal como se explicó anteriormente, si está habilitado en el entorno de Hola y configurada correctamente WPAD, conector Hola detecta automáticamente toouse de servidor y el intento de proxy de salida Hola se. Sin embargo, puede configurar explícitamente Hola conector toogo a través de un proxy de salida.

toodo por lo tanto, edite el C:\Program Files\Microsoft AAD aplicación Proxy Connector\ApplicationProxyConnectorService.exe.config hello y agregue hello *system.net* sección se muestra en este ejemplo de código. Cambio *proxyserver:8080* tooreflect el nombre del servidor proxy local o dirección IP, hello y el puerto que está escuchando en.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.net>  
    <defaultProxy>   
      <proxy proxyaddress="http://proxyserver:8080" bypassonlocal="True" usesystemdefault="True"/>   
    </defaultProxy>  
  </system.net>
  <runtime>
    <gcServer enabled="true"/>
  </runtime>
  <appSettings>
    <add key="TraceFilename" value="AadAppProxyConnector.log" />
  </appSettings>
</configuration>
```

A continuación, configurar a proxy de Hola de hello actualizador del conector servicio toouse mediante la realización de un archivo de toohello cambio similar que se encuentra en C:\Program Files\Microsoft AAD aplicación Proxy conector Updater\ApplicationProxyConnectorUpdaterService.exe.config.

### <a name="step-2-configure-hello-proxy-tooallow-traffic-from-hello-connector-and-related-services-tooflow-through"></a>Paso 2: Configurar el tráfico de tooallow de hello proxy del conector de Hola y servicios relacionados tooflow a través de

Hay cuatro tooconsider aspectos en el proxy de salida de hello:
* Las reglas de salida del proxy
* La autenticación del proxy
* Los puertos del proxy
* La inspección de SSL

#### <a name="proxy-outbound-rules"></a>Las reglas de salida del proxy
Permitir toohello de acceso después de los puntos de conexión para el acceso del servicio de conector:

* *.msappproxy.net
* *.servicebus.windows.net

Para el registro inicial, permitir toohello de acceso después de los puntos de conexión:

* login.windows.net
* login.microsoftonline.com

Si no se permite una conectividad mediante el FQDN y necesita los intervalos IP toospecify en su lugar, utilice estas opciones:

* Permitir el acceso de salida de conector de hello tooall destinos.
* Permitir el acceso de salida de conector de hello demasiado[intervalos IP del centro de datos Azure](https://www.microsoft.com/en-gb/download/details.aspx?id=41653). desafío de Hello con el uso de la lista de Hola de intervalos IP de centro de datos de Azure es que se actualiza semanalmente. Deberá tooput un proceso en tooensure lugar que las reglas de acceso se actualizan en consecuencia.

#### <a name="proxy-authentication"></a>La autenticación del proxy

Actualmente no se admite la autenticación del proxy. Nuestra recomendación actual es destinos de Internet toohello de tooallow Hola conector acceso anónimo.

#### <a name="proxy-ports"></a>Los puertos del proxy

conector Hola hace las conexiones SSL salientes mediante el método CONNECT de Hola. Básicamente, este método establece un túnel a través de proxy de salida de hello. Configurar Hola proxy server tooallow túnel tooports 80 y 443.

>[!NOTE]
>Service Bus, si se ejecuta a través de HTTPS, usa el puerto 443. Sin embargo, de forma predeterminada, Service Bus intentará establecer conexiones directas de TCP y vuelve tooHTTPS solo si se produce un error en la conexión directa.

tooensure que Hola tráfico también se envía a través de servidor proxy de salida de hello de Bus de servicio, asegúrese de que dicho conector hello no puede conectar directamente toohello servicios de Azure para los puertos 9350, 9352 y 5671.

#### <a name="ssl-inspection"></a>La inspección de SSL
No utilice inspección de SSL para el tráfico de conector de hello, ya que causará problemas para el tráfico de conector de Hola.

## <a name="troubleshoot-connector-proxy-problems-and-service-connectivity-issues"></a>Solución de problemas del proxy del conector y de conectividad del servicio
Ahora debería ver todo el tráfico que fluye a través de proxy de Hola. Si sigue teniendo problemas, debe hacer Hola siguiendo la información para solucionar problemas.

Hola tooidentify de manera mejor y solucionar problemas de conectividad del conector de problemas es tootake una red de captura en el servicio de conector de hello al iniciar el servicio de conector de Hola. Esta tarea puede resultar desalentadora; así pues, veamos algunas breves sugerencias sobre cómo capturar y filtrar seguimientos de red.

Puede usar Hola herramienta de su elección de supervisión. Para fines de Hola de este artículo, hemos usado el Monitor de red 3.4 de Microsoft. Puede [descargarlo de Microsoft](https://www.microsoft.com/download/details.aspx?id=4865).

ejemplos de Hello y los filtros que se usan en las secciones siguientes de hello son específico tooNetwork Monitor, pero principios de hello pueden ser la herramienta de análisis de tooany aplicado.

### <a name="take-a-capture-by-using-network-monitor"></a>Realización de una captura mediante el Monitor de red

toostart una captura:

1. Abra el Monitor de red y haga clic en **New Capture** (Nueva captura).
2. Haga clic en hello **iniciar** botón.

   ![Ventana Monitor de red](./media/application-proxy-working-with-proxy-servers/network-capture.png)

Después de completar una captura, haga clic en hello **detener** tooend de botón.

### <a name="take-a-capture-of-connector-traffic"></a>Toma de una captura del tráfico de conector

Para solucionar el problema inicial, realizar Hola pasos:

1. Desde services.msc, detenga el servicio de conector del Proxy de aplicación de Azure AD de Hola.
2. Iniciar la captura de red de Hola.
3. Iniciar servicio de conector del Proxy de aplicación de Azure AD de Hola.
4. Detener la captura de red de Hola.

   ![Servicio de conector del Proxy de aplicación de Azure AD en services.msc](./media/application-proxy-working-with-proxy-servers/services-local.png)

### <a name="look-at-hello-requests-from-hello-connector-toohello-proxy-server"></a>Buscar en las solicitudes de Hola de servidor proxy de hello conector toohello

Ahora que tienes una captura de red, está listo toofilter lo. Hola toolooking clave en el seguimiento de hello es entender cómo capturar toofilter Hola.

Un filtro es el siguiente (donde 8080 es el puerto de servicio del proxy de hello):

**(http.Request o http.Response) y tcp.port==8080**

Si escribe este filtro en hello **Mostrar filtro** ventana y seleccione **aplicar**, filtra el tráfico de hello capturado en función de filtro de Hola.

Hello filtro anterior muestra solo Hola solicitudes y respuestas HTTP de puerto de proxy de Hola. Para un inicio de conector donde conector hello es toouse configurado un servidor proxy, filtro de hello mostraría algo parecido a esto:

 ![Ejemplo de lista de las solicitudes y respuestas HTTP filtradas](./media/application-proxy-working-with-proxy-servers/http-requests.png)

Está ahora específicamente buscando Hola que conectar solicita que muestran la comunicación con el servidor de proxy de Hola. Si se realiza correctamente, obtiene una respuesta HTTP OK (200).

Si ve otros códigos de respuesta, como 407 o 502, proxy de hello es requerir la autenticación o no permitir el tráfico de Hola por algún otro motivo. En este momento, póngase en contacto con el equipo de soporte técnico del servidor proxy.

### <a name="identify-failed-tcp-connection-attempts"></a>Identificación de los intentos de conexión de TCP con error

Hello otro escenario común que puede estar interesado resulta hello conector está tratando de tooconnect directamente, pero que se produzcan errores.

Otro filtro de Monitor de red que ayuda a tooeasily identificar este problema es:

**property.TCPSynRetransmit**

Un paquete SYN es envía de hello primer paquete tooestablish una conexión TCP. Si este paquete no devuelve una respuesta, se vuelve a intentar Hola SYN. Puede usar Hola anterior filtro toosee las solicitudes de SYN retransmitidos. A continuación, puede comprobar si estas solicitudes SYN corresponde tooany el tráfico relacionado con el conector.

Hello en el ejemplo siguiente se muestra un intento de conexión ha fallado puerto del Bus de tooService 9352:

 ![Ejemplo de respuesta para un intento de conexión con errores](./media/application-proxy-working-with-proxy-servers/failed-connection-attempt.png)

Si ve algo parecido a Hola anterior respuesta, conector Hola consiste en intentar toocommunicate directamente con hello service Bus de servicio de Azure. Si creas Hola conector toomake conexiones directas toohello Azure services, esta respuesta es una indicación clara de que haya un problema de red o firewall.

>[!NOTE]
>Si está configurado toouse un servidor proxy, esta respuesta podría significar que Service Bus intenta una conexión TCP directa antes de cambiar tooattempting una conexión a través de HTTPS.
>

El análisis de seguimiento de red no está indicado para todos los usuarios. Pero puede ser una valiosa herramienta tooget rápido más información sobre lo que ocurre con la red.

Si continúa toostruggle con problemas de conectividad del conector, crear un vale de nuestro equipo de soporte técnico. equipo de Hello le puede ayudar a solucionar el problema más.

Para más información sobre cómo resolver errores del conector del Proxy de aplicación, consulte [Solucionar problemas de Proxy de aplicación](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-troubleshoot).

## <a name="next-steps"></a>Pasos siguientes

[Descripción de los conectores del Proxy de aplicación de Azure AD](application-proxy-understand-connectors.md)<br>
[¿Cómo toosilently instalar Hola conector del Proxy de aplicación de Azure AD](active-directory-application-proxy-silent-installation.md)
