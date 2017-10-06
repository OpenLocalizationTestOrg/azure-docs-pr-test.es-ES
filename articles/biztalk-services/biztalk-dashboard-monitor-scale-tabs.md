---
title: "aaaDashboard, Monitor, escala, configurar y las conexiones híbridas en servicios de BizTalk | Documentos de Microsoft"
description: "Obtenga información acerca de los controles de Hola y supervisar el rendimiento en las pestañas de portal clásico de hello de servicios de BizTalk: panel, Monitor, escala, configurar y las conexiones híbridas. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Revise las pestañas de panel, Monitor, escala, configurar y conexión híbrida de Hola

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Después de crear su BizTalk Service e implementar la aplicación, puede cambiar parte de configuración de servicio de BizTalk de Hola y supervisar el rendimiento de la aplicación hello. 

Cuando se abre Hola portal de Azure clásico, se colocan automáticamente en hello **todos los elementos** tooview de pestaña. su BizTalk Service, seleccione su BizTalk Service en hello **todos los elementos** tab o seleccione hello **Servicios de BIZTALK** pestaña; y, a continuación, seleccione el nombre de BizTalk Service.

Se abrirá una nueva ventana con hello después de pestañas. En el tema se describen estas pestañas.

## <a name="quickstart-quickstartquickstart"></a>Guía de inicio rápido![Guía de inicio rápido][Quickstart])
Función hello BizTalk Services Edition, todas las opciones enumeradas no estén disponibles. 

<table border="1">
    <tr>
        <td><strong>Obtener herramientas de Hola</strong></td>
        <td>Descargar plantillas de proyecto de Visual Studio hello tooinstall de SDK de servicios de BizTalk hello en el equipo de desarrollo local. Estas plantillas crean hello <strong>servicios de BizTalk</strong> (puente) hello y <strong>artefactos de servicios de BizTalk</strong> proyectos de Visual Studio de (transformación) que están implementado tooyour BizTalk Service.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure </a> y <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Hola instalar SDK de servicios de BizTalk de Azure</a> listas Hola tooget de pasos que se inició.
        </td>
    </tr>
    <tr>
        <td><strong>Crear acuerdos de asociados comerciales</strong></td>
        <td>Se abre Hola Portal de servicios de BizTalk de Azure hospedado en Azure donde agregar asociados y crear X12, AS2 y acuerdos EDIFACT EDI.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> listas Hola tooget de pasos que se inició.
        </td>
    </tr>

<tr>
        <td><strong>Más información sobre BizTalk Services</strong></td>
        <td>Vaya toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centro de aprendizaje</a> toolearn más información acerca de los servicios de BizTalk de Azure.</td>
</tr>
</table>


En la barra de tareas de hello en parte inferior de hello, puede:

<table border="1">

<tr>
<td><strong>Administrar</strong> la implementación de la aplicación</td>
<td>Abre el portal de servicios de BizTalk de Azure de Hola. Hola Portal de servicios de BizTalk es la configuración de tooEDI de entrada de hello, incluida la adición de asociados y crear X12, AS2 y acuerdos EDIFACT.
<br/><br/>
Esto es Hola igual <strong>crear acuerdos entre socios</strong> en hello <strong>inicio rápido</strong> ficha.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> proporciona más información sobre Hola Portal de servicios de BizTalk.</td>
</tr>

<tr>
<td><strong>Información de conexión</strong> de hello Namespace de Control de acceso</td>
<td>Cuando se selecciona información de conexión, a continuación, Hola Namespace de Control de acceso, emisor predeterminado, y se muestran clave predeterminada. Estos valores se pueden copiar.
<br/><br/>
También puede abrir Hola Portal de Control de acceso. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Crear un control de acceso Namespace</a> proporciona más información sobre Hola Portal de Control de acceso.</td>
</tr>

<tr>
<td><strong>Sincronizar las claves</strong> Hola cuenta de almacenamiento</td>
<td>Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria. Estas claves de cifrado controlan acceso tooyour cuenta de almacenamiento. Su BizTalk Service usa automáticamente Hola Primary Key. <strong>Sincronizar las claves</strong> habilitar usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.
<br/><br/>
Por ejemplo, desea Hola BizTalk Service toouse una nueva clave principal para hello cuenta de almacenamiento. toodo esto:
<br/><br/>
<ol>
<li>Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>. Seleccione Hola clave secundaria. Al hacerlo, Hola BizTalk Service inicia utilizando Hola clave secundaria.</li>
<li>Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola Primary Key. Recuerde que su BizTalk Service está usando Hola clave secundaria.</li>
<li>Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>. Ahora, seleccione Hola Primary Key. Esto es Hola nueva clave principal vuelve a generar.</li>
<li>Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola clave secundaria.</li>
</ol>
<br/>
Este proceso se llama "claves de sustitución". Hola sirve tooenable usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</td>
</tr>

<tr>
<td><strong>Eliminar</strong> la aplicación</td>
<td>Cuando se selecciona eliminar su BizTalk Service y se quitan tooit de todos los elementos implementados.</td>
</tr>
</table>


## <a name="dashboard"></a>Panel
Función hello BizTalk Services Edition, todas las opciones enumeradas no estén disponibles. 

Cuando se selecciona el nombre de BizTalk Service, se muestra la pestaña panel Hola. En el Panel, existen las siguientes opciones:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Información general del uso: Muestra el número de Hola de conexiones híbridas usadas
También muestra el uso de datos de hello en GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Gráfico de métrica: muestra una lista fija de métricas de rendimiento
Estas métricas proporcionan valores en tiempo real con respecto a mantenimiento Hola de hello BizTalk Service. También puede elegir hello **relativa** o **absoluta** hello y valores de intervalo de tiempo **intervalo** de métricas de Hola que se muestran en el gráfico de Hola. 

Para obtener una descripción de estas métricas de rendimiento, vaya demasiado[métricas disponibles](#Metrics) en este tema.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Vista rápida: muestra las propiedades del servicio de BizTalk
<table border="1">

<tr>
<td><strong>Actualizar credenciales de la base de datos de seguimiento</strong></td>
<td>Hola de cambios de nombre de usuario y contraseña utilizados toolog en hello base de datos de seguimiento.</td>
</tr>
<tr>
<td><strong>Actualizar certificado SSL</strong></td>
<td>Puede actualizar Hola BizTalk Service toouse un certificado SSL diferente. Automáticamente se crea un certificado SSL autofirmado cuando se <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">crear hello BizTalk Service</a>.</td>
</tr>
<tr>
<td><strong>Descarga del certificado</strong></td>
<td>Puede descargar el certificado SSL de hello usado por el equipo local de BizTalk Service tooa.</td>
</tr>
<tr>
<td><strong>Estado</strong></td>
<td>Muestra el estado actual de Hola de su BizTalk Service. Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: gráfico del estado del servicio de BizTalk</a>. </td>
</tr>
<tr>
<td><strong>URL de servicio</strong></td>
<td>dirección URL de Hola para su BizTalk Service. Esto mismo es Hola como hello <strong>dirección URL del dominio</strong> especificado cuando se crea el BizTalk Service.</td>
</tr>
<tr>
<td><strong>Dirección IP virtual (VIP) pública</strong></td>
<td>dirección IP de Hello asignado tooyour BizTalk Service. Se utiliza para todos los extremos de entrada y es la dirección de origen de hello para el tráfico saliente. Esta dirección IP pertenece tooyour BizTalk Service siempre y cuando se crea. Si elimina Hola BizTalk Service, se asigna a dirección IP de hello tooanother BizTalk Service.</td>
</tr>
<tr>
<td><strong>ACS Namespace</strong></td>
<td>Se autentica con hello BizTalk Service.</td>
</tr>
<tr>
<td><strong>Edición</strong></td>
<td>Hola que Edition especificado cuando se crea Hola BizTalk Service se enumeran.</td>
</tr>
<tr>
<td><strong>Ubicación</strong></td>
<td>Muestra Hola región geográfica que hospeda su BizTalk Service.</td>
</tr>
<tr>
<td><strong>Created</strong></td>
<td>Hola de fecha y hora de hello muestra BizTalk Service se creó.</td>
</tr>
<tr>
<td><strong>Tracking Database</strong></td>
<td>nombre de base de datos de SQL Azure de Hola que almacena Hola utilizadas por su BizTalk Service de tablas de seguimiento. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos sobre</a> proporciona información detallada sobre Hola base de datos de seguimiento.</td>
</tr>
<tr>
<td><strong>Monitoring/Archiving Storage</strong></td>
<td>nombre de la cuenta de almacenamiento de Azure Hola que almacena Hola supervisando los resultados de su BizTalk Service.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requisitos sobre</a> proporciona información detallada sobre Hola cuenta de almacenamiento.</td>
</tr>
<tr>
<td><strong>Subscription Name</strong></td>
<td>Suscripción de Hola que hospeda su BizTalk Service se enumeran. suscripción de Hello rige acceso toohello portal de Azure clásico.</td>
</tr>
<tr>
<td><strong>Subscription ID</strong></td>
<td>Cuando se crea una suscripción, se genera automáticamente un identificador de suscripción. Al utilizar las API de REST, puede que necesite hello tooenter identificador de suscripción.</td>
</tr>
</table>

[Servicios de BizTalk: Aprovisionamiento portal clásico con Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) listas Hola pasos toocreate un BizTalk Service.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Administrar información de conexión, las claves de la sincronización y eliminar en la barra de tareas de hello:
<table border="1">

<tr>
<td><strong>Administrar</strong> la implementación de la aplicación</td>
<td>Se abre el Hola Portal de servicios de BizTalk de Azure. Hola Portal de servicios de BizTalk es la configuración de tooEDI de entrada de hello, incluida la adición de asociados y crear X12, AS2 y acuerdos EDIFACT.
<br/><br/>
Esto es Hola igual <strong>crear acuerdos entre socios</strong> en hello <strong>inicio rápido</strong> ficha.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configurar componentes de mensajería de EDI en BizTalk Services Portal</a> proporciona más información sobre Hola Portal de servicios de BizTalk.</td>
</tr>
<tr>
<td><strong>Información de conexión</strong> de hello Namespace de Control de acceso</td>
<td>Muestra Hola Namespace de Control de acceso, emisor predeterminado y valores de clave predeterminada; que se pueden copiar.
<br/><br/>
También puede abrir Hola Portal de Control de acceso. Este Portal de Control de acceso es Hola igual que con la opción de Active Directory de hello en el panel de navegación izquierdo de Hola.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Administrar su Namespace ACS</a> proporciona más información sobre Hola Portal de Control de acceso.</td>
</tr>
<tr>
<td><strong>Sincronizar las claves</strong> Hola cuenta de almacenamiento</td>
<td>Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria. Estas claves de cifrado controlan acceso tooyour cuenta de almacenamiento. Su BizTalk Service usa automáticamente Hola Primary Key. <strong>Sincronizar las claves</strong> habilitar usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.
<br/><br/>
Por ejemplo, desea Hola BizTalk Service toouse una nueva clave principal para hello cuenta de almacenamiento. toodo esto:
<br/><br/>
<ol>
<li>Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>. Seleccione Hola clave secundaria. Al hacerlo, Hola BizTalk Service inicia utilizando Hola clave secundaria.</li>
<li>Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola Primary Key. Recuerde que su BizTalk Service está usando Hola clave secundaria.</li>
<li>Seleccione el servicio de BizTalk y después <strong>Sincronizar claves</strong>. Ahora, seleccione Hola Primary Key. Esto es Hola nueva clave principal vuelve a generar.</li>
<li>Hola portal de Azure clásico, seleccione la cuenta de almacenamiento y volver a generar Hola clave secundaria.</li>
</ol>
<br/>
Este proceso se llama "claves de sustitución". Hola sirve tooenable usuarios tooswitch entre clave principal de Hola y Hola clave secundaria sin interrumpir Hola BizTalk Service.</td>
</tr>

<tr>
<td><strong>Eliminar</strong> la aplicación</td>
<td>Se quitan los BizTalk Service y tooit de todos los elementos implementados.</td>
</tr>
</table>


## <a name="monitor"></a>Supervisión
No hay ningún toohello edición gratuita.

Cuando se selecciona el nombre de BizTalk Service, la pestaña Monitor Hola está disponible y muestra hello siguiente:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Gráfico de métrica: Hola muestra seleccionado las métricas de rendimiento
Estas métricas proporcionan valores en tiempo real con respecto a mantenimiento Hola de hello BizTalk Service. Se pueden elegir las métricas de rendimiento que mostrar. Se pueden mostrar seis métricas de rendimiento a la vez como máximo. 

También puede elegir hello **relativa** o **absoluta** hello y valores de intervalo de tiempo **intervalo** de métricas de Hola que se muestran. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>métricas de tooremove o mostrar en gráfico de hello:
1. Seleccione hello **Monitor** ficha.
2. Seleccione **agregar métricas** en la barra de tareas de hello:  
   ![Seleccione Agregar métricas][AddMetrics]
3. Compruebe las métricas de rendimiento de hello desea toodisplay.
4. Seleccione Hola marca de verificación tooreturn toohello **Monitor** ficha.
5. Seleccione Hola círculo siguiente toohello métrica toodisplay valor del esa métrica gráfico de Hola.  
   
    Por ejemplo, hello **el uso de CPU** métrica está atenuada; no se muestra su salida en el gráfico de hello:  
   ![La métrica Uso de CPU está atenuada][GrayedMetric]  
   
    Seleccione hello en gris Hola de círculo tooenable **el uso de CPU** toodisplay métrica sus resultados en el gráfico de hello:  
   ![La métrica Uso de CPU está habilitada][EnabledMetric]
6. Seleccione una métrica del gráfico de visualización de Hola y lista de hello, tooremove **eliminar métrica** en la barra de tareas de Hola. lista de métricas toohello atrás de hello tooadd, seleccione **agregar métricas** en la barra de tareas de hello, compruebe la métrica de Hola y Hola seleccione marca de verificación tooreturn toohello **Monitor** ficha. Seleccione Hola gris métrica de círculo tooenable Hola.

## <a name="Metrics"></a>Métricas disponibles
Hola siguiendo los contadores de rendimiento y las métricas está disponible:

<table border="1">

<tr>
<td><strong>Latencia de recorrido de ida y vuelta</strong></td>
<td>Muestra el tiempo medio de hello realizada en milisegundos tooprocess (ms) que se recibe un mensaje de mensaje de saludo de hello tiempo hasta que el mensaje Hola se procese por completo por hello BizTalk Service a través de todos los puentes de. Solo se cuentan los mensajes correctamente procesados.<br/><br/>
Cuando se produce Hola después de eventos, se crea una marca de tiempo:
<ul>
<li>Mensaje entra en la puerta de enlace de Hola</li>
<li>Mensaje es destino toohello enrutado</li>
<li>Se recibe la respuesta del destino</li>
<li>Puerta de enlace toohello enviado respuesta de confirmación de destino</li>
</ul>
<br/>
Esta métrica muestra resultado de hello de hello siguiente cálculo:
<br/><br/>
[Destino acuse de recibo respuesta enviada toohello puerta de enlace] - [mensaje entra en puerta de enlace de hello]</td>
</tr>
<tr>
<td><strong>Errores en origen</strong></td>
<td>Muestra el número total de Hola de mensajes que no se pudo por BizTalk Service al extraer los mensajes desde los puntos de conexión de origen de Hola Hola.</td>
</tr>
<tr>
<td><strong>Uso de CPU</strong></td>
<td>Enumera Hola % promedio de tiempo de procesador de todas las instancias de rol.</td>
</tr>
<tr>
<td><strong>Latencia de procesamiento</strong></td>
<td>Muestra el tiempo medio de hello realizada en un mensaje Hola BizTalk Service a través de todos los puentes, excluido el tiempo de hello empleado en destinos de tooprocess de milisegundos (ms). Solo se cuentan los mensajes correctamente procesados.<br/><br/>
Cuando se producen cada uno de hello después de eventos, se crea una marca de tiempo:

<ul>
<li>Mensaje entra en la puerta de enlace de Hola</li>
<li>Mensaje es destino toohello enrutado</li>
<li>Se recibe la respuesta del destino</li>
<li>Puerta de enlace toohello enviado respuesta de confirmación de destino</li>
</ul>
<br/>Esta métrica muestra resultado de hello de hello siguiente cálculo:<br/><br/>
[Destino acuse de recibo respuesta enviada toohello puerta de enlace] - [mensaje entra en puerta de enlace de hello] - [se recibió la respuesta de destino] + [mensaje enrutado toohello destino]</td>
</tr>
<tr>
<td><strong>Errores en proceso</strong></td>
<td>Muestra el número total de Hola de mensajes con errores durante el procesamiento por hello BizTalk Service a través de todos los puentes de hello dentro de un intervalo de tiempo.</td>
</tr>
<tr>
<td><strong>Mensajes enviados</strong></td>
<td>Muestra hello el número total de mensajes enviados por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo. Esta métrica se incrementa cuando llegue a un mensaje enviado desde una canalización de destino de la ruta de Hola. Esta métrica no indica el correcto procesamiento del mensaje.<br/><br/>
En un escenario de solicitud y respuesta, métrica Hola se incrementa al destino de la ruta de hello envía una canalización de recepción confirmación toohello atrás.</td>
</tr>
<tr>
<td><strong>Mensajes recibidos</strong></td>
<td>Muestra hello el número total de mensajes recibidos por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo. Esta métrica se incrementa cuando se recibe un mensaje nuevo canalización Hola.</td>
</tr>
<tr>
<td><strong>Mensajes en proceso</strong></td>
<td>Muestra Hola número total de mensajes que está procesando actualmente Hola BizTalk Service dentro de un intervalo de tiempo.</td>
</tr>
<tr>
<td><strong>Mensajes procesados</strong></td>
<td>Muestra Hola número total de mensajes procesados correctamente por hello BizTalk Service a través de todos los puentes dentro de un intervalo de tiempo. Esta métrica se incrementa cuando un mensaje se recibe correctamente por la canalización de Hola y de destino de toohello enrutado correctamente.</td>
</tr>
</table>


## <a name="scale"></a>Escala
En la pestaña escalar de hello, puede agregar o restar Hola número de unidades utilizadas por su BizTalk Service. De forma predeterminada, hay una unidad configurada. Unidades adicionales pueden agregarse tooscale su BizTalk Service. Al aumentar la escala de hello, se aumenta el rendimiento. Hola de recursos también aumenta, incluidos los puentes implementados, contratos, las conexiones de LOB y capacidad de procesamiento. Por ejemplo, aumentar la escala Hola de unidades de 1 unidad too2. En esta situación, puede implementar Hola dobles número de puentes, double contratos hello, double Hola LOB conexiones y potencia de procesamiento de hello dobles.

Algunas ediciones de BizTalk no ofrecen la opción de escala. En esta situación, se admite una unidad. toodetermine cuántas unidades se puede escalar su edición, consulte demasiado[servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md).

Aumentar el número de Hola de unidades puede afectar el precio. Si aumenta las unidades de hello, seleccionar **guardar** muestra un mensaje que indica si se ve afectada la facturación. A continuación, elija toocontinue. Al aumentar el número de Hola de unidades, Hola estado BizTalk Service cambia de activo tooUpdating. En el estado de actualización de hello, su BizTalk Service continúa toorun.

[Servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md) define una unidad.

## <a name="configure"></a>Configuración
No hay ningún tooHybrid conexiones.

Establece tooNone de estado de copia de seguridad de Hola o automático. Cuando se establece tooNone, copias de seguridad no se crean automáticamente. Cuando se establece tooAutomatic, configurar la ubicación de copia de seguridad de hello, frecuencia de Hola de copia de seguridad de Hola y cuánto archivos de copia de seguridad de hello tookeep. 

[Servicios de BizTalk: Backup y Restore](biztalk-backup-restore.md) proporciona detalles de Hola. 

## <a name="HybridConnections"></a>Conexiones híbridas
Las conexiones híbridas conectan una aplicación de Azure, como las aplicaciones Web o aplicaciones móviles en el servicio de aplicación de Azure, recurso local de tooan que usa un puerto TCP estático, como SQL Server, MySQL, las API Web de HTTP y mayoría de los servicios Web personalizados. Las conexiones híbridas se administran en servicios de BizTalk en hello portal de Azure clásico.

toocreate las conexiones híbridas en el servicio de aplicación de Azure, consulte [acceder a recursos usando conexiones híbridas en el servicio de aplicación de Azure local](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate o administrar las conexiones híbridas en servicios de BizTalk de Azure, consulte [conexiones híbridas](integration-hybrid-connection-overview.md).

## <a name="next"></a>Pasos siguientes
Ahora que está familiarizado con las diferentes pestañas de hello, puede obtener más información acerca de las características de servicios de BizTalk de Azure de hello:

* [Servicios de BizTalk: limitaciones](biztalk-throttling-thresholds.md)  
* [Servicios de BizTalk: nombre del emisor y clave del emisor](biztalk-issuer-name-issuer-key.md)  
* [Servicios de BizTalk: copias de seguridad y restauración](biztalk-backup-restore.md)

## <a name="see-also"></a>Otras referencias
* [Conexiones híbridas](integration-hybrid-connection-overview.md)  
* [Servicios de BizTalk: gráfico de las ediciones Developer, Basic, Standard y Premium](biztalk-editions-feature-chart.md)  
* [Servicios de BizTalk: aprovisionamiento con el Portal de Azure clásico](biztalk-provision-services.md)  
* [Servicios de BizTalk: gráfico de estado del servicio de BizTalk](biztalk-service-state-chart.md)  
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

