---
title: problemas de Data Management Gateway aaaTroubleshoot | Documentos de Microsoft
description: Proporciona sugerencias tootroubleshoot problemas relacionados tooData Management Gateway.
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a>Solución de problemas con Data Management Gateway
En este artículo se ofrece información sobre la solución de problemas con Data Management Gateway.

> [!NOTE]
> Vea hello [Data Management Gateway](data-factory-data-management-gateway.md) artículo para obtener información detallada acerca de la puerta de enlace de Hola. Vea hello [mover datos entre local y nube](data-factory-move-data-between-onprem-and-cloud.md) artículo para ver un tutorial de mover datos desde una base de datos de SQL Server local tooMicrosoft almacenamiento de blobs de Azure mediante el uso de la puerta de enlace de Hola.
>
>

## <a name="failed-tooinstall-or-register-gateway"></a>Puerta de enlace tooinstall o registrar errores
### <a name="1-problem"></a>1. Problema
Verá este mensaje de error al instalar y registrar una puerta de enlace, en concreto, al descargar el archivo de instalación de puerta de enlace de Hola.

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a>Causa
máquina de Hello en el que está tratando de puerta de enlace de hello tooinstall error en archivo de instalación puerta de enlace más reciente de toodownload de hello desde centro de descarga de hello debido tooa problema de red.

#### <a name="resolution"></a>Resolución
Compruebe su toosee de configuración del servidor de proxy de firewall si configuración de hello bloquea la conexión de red de Hola de hello equipo toohello [centro de descarga de](https://download.microsoft.com/)y actualizar la configuración de hello en consecuencia.

Como alternativa, puede descargar archivo de instalación de hello para puerta de enlace más reciente de Hola de hello [centro de descarga de](https://www.microsoft.com/download/details.aspx?id=39717) en otros equipos que pueden tener acceso a centro de descarga de Hola. También puede, a continuación, puerta de enlace de copia Hola instalador archivo toohello equipo host y ejecutarlo manualmente puerta de enlace de hello tooinstall y actualización.

### <a name="2-problem"></a>2. Problema
Verá este error al tratar de tooinstall una puerta de enlace, haga clic en **instalar directamente en este equipo** Hola portal de Azure.

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a>Causa
Una puerta de enlace ya está instalado en el equipo de Hola.

#### <a name="resolution"></a>Resolución
Desinstalar Hola puerta de enlace existente en la máquina de Hola y haga clic en hello **instalar directamente en este equipo** volver a vincular.

### <a name="3-problem"></a>3. Problema
Puede que vea este error al registrar una nueva puerta de enlace.

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a>Causa
Podría aparecer este mensaje para uno de hello siguientes motivos:

* Hola formato de clave de puerta de enlace de hello no es válido.
* se ha invalidado la clave de puerta de enlace de Hola.
* se ha vuelto generar clave de puerta de enlace de Hola desde el portal de Hola.  

#### <a name="resolution"></a>Resolución
Compruebe si está utilizando la clave de puerta de enlace correcto de Hola desde el portal de Hola. Si es necesario, volver a generar una clave y usar puerta de enlace de hello tooregister clave Hola.

### <a name="4-problem"></a>4. Problema
Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Contenido o formato de la clave no son válidos](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a>Causa
Hello contenido o el formato de clave de puerta de enlace de entrada de hello es incorrecto. Uno de los motivos de hello puede ser que solo una parte de la clave de Hola que copió desde el portal de Hola o si está usando una clave no válida.

#### <a name="resolution"></a>Resolución
Generar una clave de puerta de enlace en el portal de Hola y usar Hola copia toocopy botón Hola clave todo. A continuación, péguelo en esta puerta de enlace de ventana tooregister Hola.

### <a name="5-problem"></a>5. Problema
Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a>Causa
se ha vuelto generar clave de puerta de enlace de Hola o se ha eliminado la puerta de enlace de Hola Hola portal de Azure. También puede ocurrir si el programa de instalación de Data Management Gateway de hello no es más reciente.

#### <a name="resolution"></a>Resolución
Compruebe si el programa de instalación de Data Management Gateway de hello es la versión más reciente de hello, puede encontrar la versión más reciente de Hola en hello Microsoft [centro de descarga de](https://go.microsoft.com/fwlink/p/?LinkId=271260).

Si el programa de instalación es actual / más reciente y puerta de enlace sigue existiendo en el Portal, regenerar la clave de puerta de enlace de Hola Hola portal de Azure y usar Hola copia toocopy botón Hola clave completa y, a continuación, péguelo en esta puerta de enlace de ventana tooregister Hola. En caso contrario, vuelva a crear la puerta de enlace de Hola y empezar de nuevo.

### <a name="6-problem"></a>6. Problema
Es posible que vea Hola siguiente mensaje de error cuando se está registrando una puerta de enlace.

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La clave de la puerta de enlace no es válida o está vacía](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a>Causa
Este error puede ocurrir porque se ha eliminado la puerta de enlace de Hola o se ha vuelto generar clave de puerta de enlace asociada Hola.

#### <a name="resolution"></a>Resolución
Si se ha eliminado la puerta de enlace de hello, volver a crear la puerta de enlace de Hola desde el portal de hello, haga clic en **registrar**, copie la clave de Hola desde el portal de hello, péguelo e intente puerta de enlace de tooregister Hola.

Si la puerta de enlace de hello sigue existiendo, pero se ha vuelto generar su clave, utilice Hola nueva clave tooregister Hola puerta de enlace. Si no tiene clave hello, Regenerar clave de hello nuevo desde el portal de Hola.

### <a name="7-problem"></a>7. Problema
Cuando se está registrando una puerta de enlace, podría necesitar tooenter ruta de acceso y una contraseña para un certificado.

![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a>Causa
se ha registrado la puerta de enlace de Hello en otras máquinas antes. Durante el registro inicial de Hola de una puerta de enlace, un certificado de cifrado se ha asociado con la puerta de enlace de Hola. certificado de Hello puede generado automáticamente por puerta de enlace de Hola o proporcionado por el usuario de Hola.  Este certificado es tooencrypt usa credenciales Hola del almacén de datos (servicio vinculado).  

![Exportación de certificado](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

Al restaurar puerta de enlace de hello en otra máquina, solicita el Asistente para registro de hello para este certificado toodecrypt credenciales previamente cifrado con este certificado.  Sin este certificado, no puede descifrar las credenciales de hello nueva puerta de enlace de Hola y se producirá un error en las ejecuciones de actividad de copia posteriores asociadas a esta nueva puerta de enlace.  

#### <a name="resolution"></a>Resolución
Si ha exportado certificado de credencial de Hola de máquina de puerta de enlace de hello original mediante el uso de hello **exportar** botón en hello **configuración** del Administrador de configuración de Data Management Gateway, utilice Hola certificado aquí.

No puede omitir esta fase al recuperar una puerta de enlace. Si falta el certificado de hello, puerta de enlace de toodelete Hola desde el portal de hello es necesario y volver a crear una nueva puerta de enlace.  Además, actualice todos los servicios vinculados que están relacionados toohello puerta de enlace, volver a escribir sus credenciales.

### <a name="8-problem"></a>8. Problema
Es posible que vea Hola siguiente mensaje de error.

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a>Causa
Este error se produce cuando la puerta de enlace está en un entorno que requiere una tooaccess de proxy HTTP recursos de Internet, o se cambia la contraseña de autenticación del servidor de proxy pero no se actualiza en consecuencia en la puerta de enlace.

#### <a name="resolution"></a>Resolución
Siga las instrucciones de Hola Hola [consideraciones acerca del servidor Proxy](#proxy-server-considerations) sección de este artículo y configurar el proxy del Administrador de configuración con Data Management Gateway.

## <a name="gateway-is-online-with-limited-functionality"></a>La puerta de enlace está en línea con funcionalidad limitada
### <a name="1-problem"></a>1. Problema
Ver estado de Hola de puerta de enlace de hello como en línea con una funcionalidad limitada.

#### <a name="cause"></a>Causa
Ver estado de Hola de puerta de enlace de hello en línea con una funcionalidad limitada para uno de hello siguientes motivos:

* Puerta de enlace no puede conectar toocloud servicio a través de Service Bus de Azure.
* Servicio de nube no puede conectar toogateway a través del Bus de servicio.

Cuando la puerta de enlace de hello está en línea con una funcionalidad limitada, no es posible que toouse pueda Hola Asistente para copiar de factoría de datos toocreate las canalizaciones de datos para copiar datos tooor de almacenes de datos local. Como alternativa, puede usar el Editor de generador de datos en el portal de hello, Visual Studio o PowerShell de Azure.

#### <a name="resolution"></a>Resolución
Resolución de este problema (en línea con una funcionalidad limitada) se basa en que no se puede conectar el servicio de nube toohello u Hola otra forma de puerta de enlace de Hola. Hola las secciones siguientes proporciona estas soluciones.

### <a name="2-problem"></a>2. Problema
Vea Hola siguiente error.

`Error: Gateway cannot connect toocloud service through service bus`

![Puerta de enlace no puede conectar el servicio de toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a>Causa
Puerta de enlace no puede conectar el servicio en la nube toohello a través del Bus de servicio.

#### <a name="resolution"></a>Resolución
Siga estos pasos tooget Hola puerta de enlace en línea:

1. Permitir que las reglas de salida en la máquina de puerta de enlace de Hola y el firewall corporativo de Hola de dirección IP. Puede encontrar direcciones IP de registro de eventos de Windows hello (Id. de == 401): fue un intento realizado tooaccess un socket de una manera prohibida por los permisos de acceso XX. XX. XX. XX:9350.
* Configurar el proxy de puerta de enlace de Hola. Vea hello [consideraciones acerca del servidor Proxy](#proxy-server-considerations) sección para obtener más información.
* Habilitar los puertos de salida 5671 y 9350-9354 en ambos Hola Firewall de Windows en la máquina de puerta de enlace de Hola y el firewall corporativo de Hola. Vea hello [puertos y firewall](#ports-and-firewall) sección para obtener más información. Este paso es opcional, pero se recomienda por motivos de rendimiento.

### <a name="3-problem"></a>3. Problema
Vea Hola siguiente error.

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a>Causa
Un error transitorio en la conectividad de red.

#### <a name="resolution"></a>Resolución
Siga estos pasos tooget Hola puerta de enlace en línea:

1. Espere unos minutos, conectividad de Hola se podrán recuperar automáticamente al error de hello ha desaparecido.
* Si Hola error persiste, reinicie el servicio de puerta de enlace de Hola.

## <a name="failed-tooauthor-linked-service"></a>Servicio de tooauthor errores vinculado
### <a name="problem"></a>Problema
Puede ver este error cuando intente toouse Administrador de credenciales en credenciales de hello tooinput portal para un nuevo servicio vinculado, o actualizar las credenciales para un servicio vinculado existente.

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

Cuando aparece este error, página de configuración de hello del Administrador de configuración de Data Management Gateway sería Hola siguiente captura de pantalla.

![No se puede establecer conexión con la base de datos](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a>Causa
certificado SSL de Hola se podría haber perdido en la máquina de puerta de enlace de Hola. equipo de puerta de enlace de Hello no puede cargar el certificado de hello actualmente que se usa para el cifrado SSL. También puede ver un mensaje de error en registro de eventos de hello es similar toohello siguiente mensaje.

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a>Resolución
Siga estos pasos toosolve problema de hello:

1. Inicie el Administrador de configuración de la puerta de enlace de administración de datos.
2. Cambiar toohello **configuración** ficha.  
3. Haga clic en hello **cambio** certificado SSL de botón toochange Hola.

   ![Botón Cambiar certificado](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. Seleccione un nuevo certificado como certificado SSL de Hola. Puede usar cualquier certificado SSL que haya generado por su cuenta o que haya generado una organización.

   ![Especificar certificado](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a>Error en la actividad de copia
### <a name="problem"></a>Problema
Quizás haya notado Hola después de un error "UserErrorFailedToConnectToSqlserver" después de configurar una canalización en el portal de Hola.

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a>Causa
Esto puede ocurrir por diferentes motivos y la mitigación varía según la causa.

#### <a name="resolution"></a>Resolución
Permitir las conexiones TCP salientes en el puerto TCP/1433 en hello cliente de Data Management Gateway antes de conectar la base de datos SQL tooan.

Si la base de datos de destino de hello es una base de datos de SQL Azure, comprobar SQL Server configuración de firewall de Azure también.

Vea Hola después de almacén de datos local de sección tootest Hola conexión toohello.

## <a name="data-store-connection-or-driver-related-errors"></a>Errores relacionados con la conexión al almacén de datos o con los controladores
Si ve datos almacenar conexión o errores relacionados con el controlador, complete Hola pasos:

1. Inicie el Administrador de configuración de Data Management Gateway en la máquina de puerta de enlace de Hola.
2. Cambiar toohello **diagnósticos** ficha.
3. En **Probar conexión**, agregar valores de grupo de puerta de enlace de Hola.
4. Haga clic en **prueba** toosee si se puede conectar toohello local origen de datos de la máquina de puerta de enlace de hello usando información de conexión de Hola y credenciales. Si la conexión de prueba de hello sigue sin funciona después de instalar un controlador, reinicio Hola puerta de enlace para el mismo toopick cambio más reciente de Hola.

![Prueba de conexión en la pestaña Diagnósticos](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a>Registros de puerta de enlace
### <a name="send-gateway-logs-toomicrosoft"></a>Enviar tooMicrosoft de registros de puerta de enlace
Cuando se comunique con Microsoft Support tooget ayuda para solucionar problemas de la puerta de enlace, que se le pida tooshare los registros de puerta de enlace. Con la versión de Hola de puerta de enlace de hello, puede compartir los registros de puerta de enlace necesaria con dos clics del botón del Administrador de configuración de Data Management Gateway.    

1. Cambiar toohello **diagnósticos** ficha del Administrador de configuración de Data Management Gateway.

    ![Pestaña Diagnóstico de la puerta de enlace de administración de datos](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. Haga clic en **enviar registros** hello toosee después el cuadro de diálogo.

    ![Puerta de enlace de administración de datos: Enviar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. (Opcional) Haga clic en **ver registros** tooreview inicia sesión en el Visor de eventos de Hola.
4. (Opcional) Haga clic en **privacidad** declaración de privacidad de los servicios web de Microsoft tooreview.
5. Cuando esté satisfecho con lo que está a punto de tooupload, haga clic en **enviar registros** tooactually enviar registros de Hola desde Hola últimos siete días tooMicrosoft para solucionar el problema. Debería ver estado de Hola de operación de registros de envío de hello tal y como se muestra en la siguiente captura de pantalla de Hola.

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. Una vez completada la operación de hello, verá un cuadro de diálogo como se muestra en la siguiente captura de pantalla de Hola.

    ![Puerta de enlace de administración de datos: Estado del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. Guardar hello **ID informe** y compartirlo con Microsoft Support. Id. de informe de Hello es registros de puerta de enlace de hello toolocate usado que ha cargado para solucionar el problema.  Id. de informe de Hello también se guarda en el Visor de eventos de Hola.  Puede buscar examinando Hola de Id. de evento "25" y comprobar Hola fecha y hora.

    ![Puerta de enlace de administración de datos: Identificador de informe del envío de registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a>Archivar registros de puerta de enlace en el equipo host de puerta de enlace
Hay veces en las que existen problemas con la puerta de enlace y no es posible compartir los registros de puerta de enlace de forma directa:

* Instalar puerta de enlace de Hola y registrar la puerta de enlace de hello manualmente.
* Intente puerta de enlace de hello tooregister con una nueva clave del Administrador de configuración de Data Management Gateway.
* Intente toosend registros y no se puede conectar el servicio de host de puerta de enlace de Hola.

Para estos escenarios, puede guardar los registros de puerta de enlace como un archivo ZIP y compartirlo cuando pueda ponerse en contacto con el equipo de soporte técnico de Microsoft. Por ejemplo, si recibe un error al registrar la puerta de enlace de hello como se muestra en la siguiente captura de pantalla de Hola.   

![Puerta de enlace de administración de datos: Error de registro](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

Haga clic en hello **almacene los registros de puerta de enlace** vinculan tooarchive y guardar los registros y, a continuación, compartir el archivo zip de hello con soporte técnico de Microsoft.

![Puerta de enlace de administración de datos: Archivar registros](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a>Buscar registros de puerta de enlace
Puede encontrar información de registro de puerta de enlace detallada en registros de eventos de Windows hello.

1. Inicie el **Visor de eventos** de Windows.
2. Buscar registros en hello **registros de aplicaciones y servicios** > **Data Management Gateway** carpeta.

 Cuando esté solucionando problemas relacionados con la puerta de enlace, busque eventos de nivel de error en el Visor de eventos de Hola.

![Puerta de enlace de administración de datos: Registros en el Visor de eventos](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
