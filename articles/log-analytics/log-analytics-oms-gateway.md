---
title: Hola a aaaConnect equipos tooOMS con puerta de enlace de OMS | Documentos de Microsoft
description: Conectar los dispositivos administrados por OMS y los equipos supervisados por Operations Manager con el servicio de OMS de hello puerta de enlace de OMS toosend datos toohello cuando no tiene acceso a Internet.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>Conectar equipos sin tooOMS de acceso a Internet mediante Hola puerta de enlace de OMS

Este documento describe cómo los administrados por OMS y System Center Operations Manager supervisa los equipos pueden enviar servicio OMS de toohello de datos cuando no tienen acceso a Internet. Hola puerta de enlace de OMS, que es un proxy de reenvío de HTTP que admite el protocolo de túnel de HTTP mediante el comando HTTP CONNECT hello, puede recopilar datos y enviarlo toohello servicio OMS en su nombre.  

Hello puerta de enlace de OMS es compatible con:

* Trabajos híbridos de runbook de Azure Automation  
* Equipos Windows con Microsoft Monitoring Agent hello directamente conectan tooan área de trabajo OMS
* Equipos de Linux con hello agente de OMS para Linux conectan directamente tooan área de trabajo OMS  
* System Center Operations Manager 2012 SP1 con UR7, Operations Manager 2012 R2 con UR3 o el grupo de administración de Operations Manager 2016 integrado en OMS.  

Si las directivas de seguridad de TI no permitir que los equipos en su toohello de tooconnect de red Internet, como punto de venta (POS) dispositivos o servidores que admiten servicios de TI, pero debe tooconnect tooOMS les toomanage y supervisarlos, se pueden configurar toocommunicate directamente con la configuración de tooreceive de puerta de enlace de OMS de Hola y reenviar datos en su nombre.  Si estos equipos están configurados con toodirectly de agente OMS Hola conectar tooan área de trabajo OMS, todos los equipos en su lugar se comunicarán con hello puerta de enlace de OMS.  puerta de enlace de Hello transfiere datos desde Hola agentes tooOMS directamente, no analiza los datos de hello en tránsito.

Cuando un grupo de administración de Operations Manager se integra con OMS, servidores de administración de hello pueden ser configurado tooconnect toohello información de configuración de puerta de enlace de OMS tooreceive y enviar los datos recopilados según solución Hola que ha habilitado.  Agentes de Operations Manager envían algunos datos, como alertas de Operations Manager, evaluación de la configuración, espacio de la instancia y servidor de administración de capacidad datos toohello. Otros datos de gran volumen, como los registros de IIS, el rendimiento y eventos de seguridad se envían directamente toohello puerta de enlace de OMS.  Si tiene uno o más servidores de puerta de enlace de Operations Manager implementan en una red Perimetral o en otro toomonitor de red aislada sistemas no es de confianza, no puede comunicarse con una puerta de enlace de OMS.  Servidores de puerta de enlace de administrador de operaciones pueden solo servidor de administración de informes tooa.  Cuando un grupo de administración de Operations Manager está configurado toocommunicate con hello puerta de enlace de OMS, información de configuración de proxy de hello es tooevery distribuirá automáticamente equipo administrado con agente que está configurado toocollect datos para análisis de registros, incluso si configuración de Hello está vacía.    

tooprovide alta disponibilidad para directamente conectado o grupos de administración de las operaciones que se comunican con OMS a través de puerta de enlace de hello, puede usar tooredirect de equilibrio de carga de red y distribución el tráfico de hello en varios servidores de puerta de enlace.  Si un servidor de puerta de enlace deja de funcionar, tráfico de hello es nodo disponible tooanother redirigida.  

Se recomienda que instale el agente de OMS de hello en equipo Hola ejecutando Hola de toomonitor de software de puerta de enlace de OMS de hello puerta de enlace de OMS y analizar los datos de rendimiento o el evento. Además, Hola agente ayuda a Hola puerta de enlace de OMS identificar Hola extremos del servicio que necesita toocommunicate con.

Cada agente debe tener la puerta de enlace de tooits de conectividad de red para que los agentes automáticamente pueden transferir datos tooand de puerta de enlace de Hola. No se recomienda instalar puerta de enlace de hello en un controlador de dominio.

Hola siguiente diagrama muestra flujo de datos de tooOMS agentes directa con el servidor de puerta de enlace de Hola.  Agentes deben tener su coincidencia de configuración de proxy Hola mismo puerto hello puerta de enlace de OMS es toocommunicate configurado con tooOMS.  

![diagrama de comunicación de agente directo con OMS](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

Hello siguiente diagrama muestra el flujo de datos desde un tooOMS de grupo de administración de Operations Manager.   

![Diagrama de comunicación de Operations Manager con OMS](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>Requisitos previos

Al designar un Hola de toorun equipo puerta de enlace de OMS, este equipo debe tener el siguiente de hello:

* Windows 10, Windows 8.1, Windows 7
* Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008
* .Net Framework 4.5
* Procesador de 4 núcleos y 8 GB de memoria como mínimo

### <a name="language-availability"></a>Disponibilidad de idiomas

Hola puerta de enlace de OMS está disponible en hello siguientes idiomas:

- Chino (simplificado)
- Chino (tradicional)
- Checo
- Neerlandés
- English
- Francés
- Alemán
- Húngaro
- Italiano
- Japonés
- Coreano
- Polaco
- Portugués (Brasil)
- Portugués (Portugal)
- Ruso
- Español (internacional)

## <a name="download-hello-oms-gateway"></a>Descargar Hola puerta de enlace de OMS

Hay tres maneras tooget Hola versión más reciente del archivo de instalación de puerta de enlace de OMS hello.

1. Descargar de hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443).

2. Descargar desde el portal de OMS Hola.  Después de iniciar sesión en el área de trabajo OMS tooyour, navegue demasiado**configuración** > **orígenes conectados** > **servidores Windows** y haga clic en **Descargar la puerta de enlace OMS**.

3. Descargar de hello [portal de Azure](https://portal.azure.com).  Después de conectarse:  

   1. Examinar la lista de hello de servicios y, a continuación, seleccione **análisis de registros**.  
   2. Seleccione un área de trabajo.
   3. En su hoja de área de trabajo, en **General**, haga clic en **Inicio rápido**.
   4. En **elegir un área de trabajo de datos origen tooconnect toohello**, haga clic en **equipos**.
   5. Hola **Direct Agent** hoja, haga clic en **descargar puerta de enlace de OMS**.<br><br> ![descargar OMS Gateway](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>Instalar Hola puerta de enlace de OMS

tooinstall una puerta de enlace, llevar a cabo pasos de Hola.  Si tiene instalada una versión anterior, anteriormente denominado *reenviador de análisis de registro*, estará actualizado toothis versión.  

1. Desde la carpeta de destino de hello, haga doble clic en **Gateway.msi OMS**.
2. En hello **bienvenida** página, haga clic en **siguiente**.<br><br> ![Asistente para la instalación de la puerta de enlace](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. En hello **contrato de licencia** página, seleccione **acepto los términos de hello en el contrato de licencia de hello** tooagree toohello términos de licencia y, a continuación, haga clic en **siguiente**.
4. En hello **dirección de proxy y puerto** página:
   1. Toobe de número de puerto de tipo hello TCP utilizado para puerta de enlace de Hola. El programa de instalación configura una regla de entrada con este número de puerto en el firewall de Windows.  valor de Hello predeterminado es 8080.
      intervalo válido de Hola de número de puerto de hello está comprendido entre 1 y 65535. Si la entrada de hello no está dentro de este intervalo, aparece un mensaje de error.
   2. Si lo desea, si hello servidor donde es la puerta de enlace de hello instalado necesidades toocommunicate a través de un servidor proxy, escriba la dirección de proxy de Hola donde debe puerta de enlace de hello tooconnect. Por ejemplo: `http://myorgname.corp.contoso.com:80`.  Si está en blanco, puerta de enlace de hello intentará tooconnect toohello Internet directamente.  Si el servidor proxy requiere autenticación, especifique el nombre de usuario y la contraseña.<br><br> ![Configuración del proxy en el Asistente de la puerta de enlace](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. Haga clic en **Siguiente**.
5. Si no tiene habilitado Microsoft Update, página de Microsoft Update de hello aparece donde puede elegir tooenable lo. Elija la opción que desee y haga clic en **Siguiente**. En caso contrario, continúe toohello siguiente paso.
6. En hello **carpeta de destino** página, deja Hola predeterminado puerta de enlace de C:\Program Files\OMS o tipo hello ubicación de la carpeta donde desee tooinstall puerta de enlace y, a continuación, haga clic en **siguiente**.
7. En hello **tooinstall listo** página, haga clic en **instalar**. Control de cuentas de usuario pueden aparecer tooinstall solicitud de permiso. Si aparece, haga clic en **Sí**.
8. Una vez completada la instalación, haga clic en **Finalizar**. Puede comprobar que el servicio Hola ejecutando abriendo complemento Hola services.msc y compruebe que **puerta de enlace de OMS** aparece en la lista de hello de servicios y estado es **ejecutando**.<br><br> ![Servicios: OMS Gateway](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>Configuración de equilibrio de carga de red
Puede configurar la puerta de enlace de Hola para lograr alta disponibilidad con equilibrio de carga de red (NLB) mediante Microsoft red equilibrio de carga (NLB) o equilibradores de carga basado en hardware.  Hello equilibrador de carga administra tráfico redirigiendo Hola soliciten conexiones de agentes de OMS de Hola o servidores de administración de Operations Manager a través de sus nodos. Si un servidor de puerta de enlace deja de funcionar, tráfico de hello obtiene nodos tooother redirigida.

toolearn cómo toodesign e implementar un clúster de equilibrio de carga de red de Windows Server 2016, consulte [equilibrio de carga de red](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing).  Hello pasos siguientes describen cómo tooconfigure una red de Microsoft clúster equilibrio de carga.  

1.  Inicie sesión en hello Windows server que es miembro del clúster NLB de hello con una cuenta administrativa.  
2.  Abra el Administrador de equilibrio de carga de red en el Administrador del servidor, haga clic en **Herramientas** y, luego, en **Administrador de equilibrio de carga de red**.
3. tooconnect un servidor de puerta de enlace de OMS con hello el agente de supervisión de Microsoft instalado, haga clic en dirección IP del clúster de hello y, a continuación, haga clic en **tooCluster agregar Host**.<br><br> ![Administrador de equilibrio de carga de red: agregar Host tooCluster](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. Escriba la dirección IP de hello del servidor de puerta de enlace de Hola que desea tooconnect.<br><br> ![Administrador de equilibrio de carga de red: agregar Host tooCluster: conectar](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>Configuración de agentes de OMS y de un grupo de administración de Operations Manager
Hello próxima sección incluye pasos sobre cómo tooconfigure directamente conectado Hybrid Runbook Worker de automatización de Azure, un grupo de administración de Operations Manager o agentes OMS con hello toocommunicate de puerta de enlace de OMS con OMS.  

toounderstand requisitos y pasos acerca de cómo tooinstall Hola agente de OMS en equipos de Windows que se conectan directamente a tooOMS, consulte [Windows conectar equipos tooOMS](log-analytics-windows-agents.md) o para Linux, vea equipos [equipos Linux conectarse tooOMS](log-analytics-linux-agents.md).

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>Configuración de agente de OMS de Hola y Operations Manager toouse Hola puerta de enlace de OMS como un servidor proxy

### <a name="configure-standalone-oms-agent"></a>Configuración de agentes de OMS de forma independiente
Vea [configurar ajustes del proxy y firewall con Microsoft Monitoring Agent hello](log-analytics-proxy-firewall.md) para obtener información acerca de cómo configurar un toouse agente un servidor proxy, que en este caso es la puerta de enlace de Hola.  Si ha implementado varios servidores de puerta de enlace detrás de un equilibrador de carga de red, la configuración de proxy de agente OMS de hello es Hola de dirección IP virtual de hello NLB:<br><br> ![Propiedades de Microsoft Monitoring Agent – Configuración del proxy](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>Configure Operations Manager: todos los agentes usan Hola mismo servidor proxy
Configurar el servidor de puerta de enlace de Operations Manager tooadd Hola.  Hola Operations Manager, configuración de proxy es automáticamente aplica a agentes tooall reporting tooOperations Manager, incluso aunque Hola configuración está vacía.

toouse Hola puerta de enlace toosupport Operations Manager, debe tener:

* Microsoft Monitoring Agent (versión del agente: **8.0.10900.0** y versiones posteriores) instalados en el servidor de puerta de enlace de Hola y configurados para áreas de trabajo OMS de hello con el que desea toocommunicate.
* puerta de enlace de Hello debe tener conectividad a Internet o ser tooa conectado servidor de proxy que realiza.

> [!NOTE]
> Si no especifica un valor para la puerta de enlace de hello, valores en blanco se insertan a tooall agentes.


1. Consola de Operations Manager Hola abierta y en **Operations Management Suite**, haga clic en **conexión** y, a continuación, haga clic en **configurar servidor Proxy**.<br><br> ![Operations Manager: Configurar servidor proxy](./media/log-analytics-oms-gateway/scom01.png)<br>
2. Seleccione **usar un tooaccess de servidor proxy hello Operations Management Suite** y a continuación, escriba la dirección IP de hello del servidor de puerta de enlace de OMS de Hola o dirección IP virtual de NLB de Hola. Asegúrese de que comience con hello `http://` prefijo.<br><br> ![Operations Manager: dirección de servidor proxy](./media/log-analytics-oms-gateway/scom02.png)<br>
3. Haga clic en **Finalizar** El servidor de Operations Manager está conectado tooyour área de trabajo OMS.

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>Configuración de Operations Manager: determinados agentes usan el servidor proxy
En entornos grandes o complejos, podría desear sólo específico servidores (o grupos) toouse Hola servidor de puerta de enlace de OMS.  En estos servidores, no se puede actualizar Hola agente directamente como este valor se sobrescribe con el valor global de Hola Hola grupo de administración de Operations Manager.  En su lugar debe toooverride Hola regla usada toopush estos valores.

> [!NOTE]
> Esta misma técnica de configuración puede ser utilizará tooallow Hola de varios servidores de puerta de enlace de OMS en su entorno.  Por ejemplo, puede requerir toobe específico de servidores de puerta de enlace de OMS especificado en cada región.

1. Consola de Operations Manager Hola abra y seleccione hello **Authoring** área de trabajo.  
2. En el área de trabajo de creación de hello, seleccione **reglas** y haga clic en hello **ámbito** botón de barra de herramientas de Operations Manager Hola. Si este botón no está disponible, compruebe que dispone de un objeto, no una carpeta seleccionado en el panel de supervisión de hello toomake. Hola **objetos de módulo de administración de ámbito** cuadro de diálogo muestra una lista de clases de destino comunes, grupos u objetos.
3. Tipo de **servicio de mantenimiento** en hello **buscar** del campo y selecciónelo en la lista de Hola.  Haga clic en **Aceptar**.  
4. Busque la regla de hello **regla de configuración de Proxy de Advisor** y en la barra de la consola de operaciones de hello, haga clic en **invalida** y, a continuación, elija demasiado**invalidación hello Rule\For un objeto de clase específico: mantenimiento Servicio** y seleccione un objeto específico de la lista de Hola.  Si lo desea, puede crear un grupo personalizado que contiene el objeto de servicio de mantenimiento de Hola de servidores de Hola que desea tooapply esta tooand de invalidación y luego aplicar Hola invalidación toothat grupo.
5. Hola **propiedades de invalidación** diálogo cuadro, haga clic en una marca de verificación en hello tooplace **invalidar** columna siguiente toohello **WebProxyAddress** parámetro.  Hola **valor de invalidación** , escriba la dirección URL de hello consistente en garantizar de servidor de puerta de enlace de OMS de Hola que comienzan con hello `http://` prefijo.
   >[!NOTE]
   > No es necesario regla de hello tooenable tal y como ya se administra automáticamente con una invalidación contenida en hello Microsoft System Center Advisor Secure Reference Override management pack destinatarios Hola grupo de servidor de supervisión de Microsoft System Center Advisor.
   >
6. Seleccione un módulo de administración de hello **Seleccionar módulo de administración de destino** lista o cree un nuevo módulo de administración sin sellar haciendo clic en **nuevo**.
7. Cuando haya completado los cambios, haga clic en **Aceptar**.

### <a name="configure-for-automation-hybrid-workers"></a>Configuración de Hybrid Workers de Automation
Si tienes automatización Hybrid Runbook Workers en su entorno, Hola pasos proporciona soluciones alternativas manual y temporal tooconfigure Hola puerta de enlace toosupport ellos.

Hola pasos, debe tooknow hello Azure región donde reside la cuenta de automatización de Hola. ubicación de Hola toolocate:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Seleccione servicio de automatización de Azure Hola.
3. Seleccionar cuenta de automatización de Azure adecuada de Hola.
4. Vea su región en **Ubicación**.<br><br> ![Azure Portal – Ubicación de la cuenta de Automation](./media/log-analytics-oms-gateway/location.png)  

Usar hello después tablas tooidentify Hola URL para cada ubicación:

**Direcciones URL del servicio de datos del tiempo de ejecución del trabajo**

| **ubicación** | **URL** |
| --- | --- |
| Centro-Norte de EE. UU |ncus-jobruntimedata-prod-su1.azure-automation.net |
| Europa occidental |we-jobruntimedata-prod-su1.azure-automation.net |
| Centro-Sur de EE. UU |scus-jobruntimedata-prod-su1.azure-automation.net |
| Este de EE. UU. 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| Canadá central |cc-jobruntimedata-prod-su1.azure-automation.net |
| Europa del Norte |ne-jobruntimedata-prod-su1.azure-automation.net |
| Sudeste de Asia |sea-jobruntimedata-prod-su1.azure-automation.net |
| India Central |cid-jobruntimedata-prod-su1.azure-automation.net |
| Japón |jpe-jobruntimedata-prod-su1.azure-automation.net |
| Australia |ase-jobruntimedata-prod-su1.azure-automation.net |

**Direcciones URL de servicio Agente**

| **ubicación** | **URL** |
| --- | --- |
| Centro-Norte de EE. UU |ncus-agentservice-prod-1.azure-automation.net |
| Europa occidental |we-agentservice-prod-1.azure-automation.net |
| Centro-Sur de EE. UU |scus-agentservice-prod-1.azure-automation.net |
| Este de EE. UU. 2 |eus2-agentservice-prod-1.azure-automation.net |
| Canadá central |cc-agentservice-prod-1.azure-automation.net |
| Europa del Norte |ne-agentservice-prod-1.azure-automation.net |
| Sudeste de Asia |sea-agentservice-prod-1.azure-automation.net |
| India Central |cid-agentservice-prod-1.azure-automation.net |
| Japón |jpe-agentservice-prod-1.azure-automation.net |
| Australia |ase-agentservice-prod-1.azure-automation.net |

Si el equipo se registra automáticamente como un Runbook Worker híbrido para aplicar las revisiones mediante la solución de administración de actualizaciones de hello, siga estos pasos:

1. Agregar lista Host permite de toohello de direcciones URL de servicio de hello datos en tiempo de ejecución del trabajo en hello puerta de enlace de OMS. Por ejemplo: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. Reinicie el servicio de puerta de enlace de OMS de hello mediante Hola siguiente cmdlet de PowerShell:`Restart-Service OMSGatewayService`

Si el equipo está integrada tooAzure automatización mediante el uso de cmdlet de registro de hello Hybrid Runbook Worker, siga estos pasos:

1. Agregar lista de hello agente servicio Registro URL toohello Host permitido en hello puerta de enlace de OMS. Por ejemplo: `Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Agregar lista Host permite de toohello de direcciones URL de servicio de hello datos en tiempo de ejecución del trabajo en hello puerta de enlace de OMS. Por ejemplo: `Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. Reinicie el servicio de puerta de enlace de OMS Hola.
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>Cmdlets de PowerShell útiles
Cmdlets puede ayudarle a completar las tareas que son valores de configuración necesario tooupdate Hola OMS la puerta de enlace. Antes de usarlos, asegúrese de:

1. Instalar Hola OMS puerta de enlace (MSI).
2. Abra una ventana de la consola de PowerShell.
3. módulo de hello tooimport, escriba el siguiente comando:`Import-Module OMSGateway`
4. Si se ha producido ningún error en el paso anterior de hello, módulo de Hola se importó correctamente y puede usar cmdlets de Hola. Escriba `Get-Module OMSGateway`
5. Después de realizar cambios mediante los cmdlets de hello, asegúrese de que se reinicie el servicio de puerta de enlace de Hola.

Si se produce un error en el paso 3, el módulo de hello no se importa. podría producirse el error de Hello cuando PowerShell es el módulo de hello toofind no se puede. Puede encontrarla en la ruta de instalación de la puerta de enlace de hello: *C:\Program Files\Microsoft OMS Gateway\PowerShell*.

| **Cmdlet** | **Parámetros** | **Descripción** | **Ejemplo** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Clave |Obtiene la configuración de hello del servicio de Hola |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |Clave (se requiere) <br> Valor |Hola de cambios de configuración del servicio de Hola |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |Obtiene la dirección Hola de proxy de retransmisión (ascendente) |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |Dirección<br> Nombre de usuario<br> Password |Establece dirección hello (y credenciales) del proxy de retransmisión (ascendente) |1. Establezca un proxy de retransmisión y la credencial:<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2. Establezca un proxy de retransmisión que no necesite autenticación: `Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3. La configuración de proxy retransmisión Hola clara:<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |Hola obtiene permitida host (solo hello host permitidos configurada localmente, no se incluyen automáticamente descargados hosts permitidos) |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |Host (obligatorio) |Agrega la lista de elementos permitido de hello host toohello |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |Host (obligatorio) |Quita el host de Hola Hola lista de elementos permitido |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |Asunto (obligatorio) |Agrega el certificado de cliente de hello sujeto toohello lista de elementos permitido |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |Asunto (obligatorio) |Quita el sujeto del certificado de cliente de Hola de hello lista de elementos permitido |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |Hola obtiene permitida cliente sujetos de los certificados (solo Hola localmente configurado asuntos permitidos, no se incluyen automáticamente descargados asuntos permitidos) |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>Solución de problemas
toocollect eventos registrados por la puerta de enlace de hello, necesita tooalso tienen instalado el agente de OMS de Hola.<br><br> ![Visor de eventos: registro de OMS Gateway](./media/log-analytics-oms-gateway/event-viewer.png)

**Identificadores de evento y descripciones de OMS Gateway**

Hello siguiente tabla se muestra hello Id. de evento y las descripciones de eventos de registro de puerta de enlace de OMS.

| **Id** | **Descripción** |
| --- | --- |
| 400 |Cualquier error de la aplicación que no tiene un identificador específico |
| 401 |Configuración errónea. Por ejemplo: listenPort = "text", en lugar de un entero |
| 402 |Excepción al analizar los mensajes de protocolo de enlace TLS |
| 403 |Error de red. Por ejemplo: no se puede conectar el servidor de tootarget |
| 100 |Información general |
| 101 |El servicio se ha iniciado |
| 102 |El servicio se ha detenido |
| 103 |Se ha recibido un comando HTTP CONNECT del cliente |
| 104 |No es un comando HTTP CONNECT |
| 105 |Servidor de destino no está en la lista de permitidos o puerto de destino de hello no es el puerto seguro (443) <br> <br> Asegúrese de que Hola MMA el agente en el servidor de puerta de enlace y agentes de hello comunicarse con hello puerta de enlace son toohello conectado misma área de trabajo de análisis de registros. |
| 105 |ERROR TcpConnection – Invalid Client certificate: CN=Gateway <br><br> Asegúrese de que: <br>    <br> &#149; Utiliza una puerta de enlace con el número de versión 1.0.395.0, o uno superior. <br> &#149; Hello MMA agente en el servidor de puerta de enlace y agentes de hello comunicarse con hello puerta de enlace están conectado toohello misma área de trabajo de análisis de registros. |
| 106 |Alguna razón esa sesión TLS hello es sospechoso y rechazados |
| 107 |se ha comprobado la sesión TLS Hola |

**Toocollect de contadores de rendimiento**

Hello siguiente tabla muestra contadores de rendimiento de hello disponibles para hello puerta de enlace de OMS. Puede agregar contadores de hello mediante Monitor de rendimiento.

| **Name** | **Descripción** |
| --- | --- |
| OMS Gateway/Conexión de cliente activa |Número de conexiones de red (TCP) de cliente activas |
| OMS Gateway/Recuento de errores |Número de errores |
| OMS Gateway/Cliente conectado |Número máximo de clientes conectados |
| OMS Gateway/Recuento de rechazos |Número de rechazos debido a error de validación de tooany TLS |

![Contadores de rendimiento de OMS Gateway](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>Obtención de ayuda
Cuando haya iniciado sesión en toohello portal de Azure, puede crear una solicitud de asistencia con hello puerta de enlace de OMS o cualquier otro servicio de Azure o característica de un servicio.
asistencia de toorequest, haga clic en el signo de interrogación de hello en hello superior derecho del portal de hello y, a continuación, haga clic en **nueva solicitud de soporte técnico**. A continuación, complete el nuevo formulario de solicitud de soporte técnico de Hola.

![Nueva solicitud de soporte](./media/log-analytics-oms-gateway/support.png)

También puede dejar comentarios sobre OMS o análisis de registros en hello [foro de comentarios de Microsoft Azure](https://feedback.azure.com/forums/267889).

## <a name="next-steps"></a>Pasos siguientes
* [Agregar orígenes de datos](log-analytics-data-sources.md) datos toocollect de Hola orígenes conectados en el área de trabajo OMS y almacenarlo en el repositorio de OMS de Hola.
