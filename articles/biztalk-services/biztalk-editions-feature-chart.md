---
title: "aaaLearn sobre las características de las ediciones de servicios de BizTalk | Documentos de Microsoft"
description: 'Se comparan las capacidades de Hola de ediciones de servicios de BizTalk de hello: liberar, Developer, Basic, Standard y Premium. MABS, WABS.'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: c589629f-06b1-44bb-b8ca-1db71826ea59
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 81626fa743a7190e7c78a0fd90b3054a08982b02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-editions-chart"></a>Servicios de BizTalk: gráfico de ediciones

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Servicios de BizTalk de Azure ofrece varias ediciones. Utilice este toodetermine artículo qué edición es la adecuada para sus escenario y las necesidades empresariales.

## <a name="compare-hello-editions"></a>Comparar las ediciones de Hola
**Free (Vista previa)**

Permite crear y administrar conexiones híbridas. Una conexión híbrida es un tooconnect de manera sencilla un sitio Web de Azure tooan sistema, como SQL Server local.

**Developer**

Incluye conexiones híbridas y procesamiento de mensajes de EAI y EDI con un portal de administración fácil de utilizar para socios comerciales, además de compatibilidad con esquemas EDI y procesamiento enriquecido EDI sobre X12 y AS2. Puede crear escenarios comunes de EAI conectar servicios en la nube de hello con cualquier tooread de protocolos HTTP/S, REST, FTP, SFTP y WCF y escribir los mensajes.  Usar sistemas LOB tooon local de conectividad con los adaptadores SAP, Oracle eBusiness, base de datos de Oracle, Siebel y SQL Server listos para usar. Utilice un entorno centrado en el desarrollador con herramientas de Visual Studio para desarrollo e implementación simples. Limitado toodevelopment fines y pruebas solo con ningún contrato de nivel de servicio (SLA).

**Básico**

Incluye la mayoría de las funciones para desarrolladores Hola con aumentos en las conexiones de conexiones híbridas, puentes EAI, acuerdos de EDI y BizTalk Adapter Pack. También ofrece alta disponibilidad y Hola opción tooscale con un contrato de nivel de servicio (SLA).

**Standard**

Incluye todas las capacidades básicas de hello con aumentos en las conexiones de conexiones híbridas, puentes EAI, acuerdos de EDI y BizTalk Adapter Pack. También ofrece alta disponibilidad y Hola opción tooscale con un contrato de nivel de servicio (SLA).

**Premium**

Incluye todas las funcionalidades de hello estándar con aumentos en las conexiones de conexiones híbridas, puentes EAI, acuerdos de EDI y BizTalk Adapter Pack. También incluye archivado, alta disponibilidad y Hola opción tooscale con un contrato de nivel de servicio (SLA).

## <a name="editions-chart"></a>Gráfico de ediciones
Hello tabla siguiente enumeran las diferencias de Hola.

<table border="1">
<tr bgcolor="FAF9F9">
        <th></th>
        <th>Free (Vista previa)</th>
        <th>Developer</th>
        <th>Básica</th>
        <th>Standard</th>
        <th>Premium</th>
</tr>

<tr>
<td><strong>Precio de salida</strong></td>
<td colspan="5"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Precios de Azure BizTalk Services</a> <br/><br/> <a HREF="http://azure.microsoft.com/pricing/calculator/?scenario=full">Calculadora de precios de Azure</a></td>
</tr>
<tr>
<td><strong>Configuración mínima predeterminada</strong></td>
<td>1 unidad gratis</td>
<td>1 unidad Developer</td>
<td>1 unidad Basic</td>
<td>1 unidad Standard</td>
<td>1 unidad Premium</td>
</tr>
<tr>
<td><strong>Escala</strong></td>
<td>Sin escala</td>
<td>Sin escala</td>
<td>Sí, en incrementos de 1 unidad Basic</td>
<td>Sí, en incrementos de una unidad Standard</td>
<td>Sí, en incrementos de una unidad Premium</td>
</tr>
<tr>
<td><strong>Escalado horizontal máximo permitido</strong></td>
<td>Sin escala</td>
<td>Sin escala</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
<td>Unidades de too8</td>
</tr>
<tr>
<td><strong>Puentes EAI por unidad</strong></td>
<td>No se incluye</td>
<td>25</td>
<td>25</td>
<td>125</td>
<td>500</td>
</tr>
<tr>
<td><strong>EDI, AS2</strong>
<br/><br/>
Incluye contratos TPM</td>
<td>No se incluye</td>
<td>Se incluye. 10 contratos por unidad.</td>
<td>Se incluye. 50 contratos por unidad.</td>
<td>Se incluye. 250 contratos por unidad.</td>
<td>Se incluye. 1000 contratos por unidad.</td>
</tr>
<tr>
<td><strong>Conexiones híbridas por unidad</strong></td>
<td>5</td>
<td>5</td>
<td>10</td>
<td>50</td>
<td>100</td>
</tr>
<tr>
<td><strong>Transferencia de datos de conexiones híbridas (GB) por unidad</strong></td>
<td>5</td>
<td>5</td>
<td>50</td>
<td>250</td>
<td>500</td>
</tr>
<tr>
<td><strong>Sistemas LOB de tooon locales de las conexiones de servicio de adaptador de BizTalk</strong></td>
<td>No se incluye</td>
<td>1 conexión</td>
<td>2 conexiones</td>
<td>5 conexiones</td>
<td>25 conexiones</td>
</tr>
<tr>
<td align="left"><strong>Sistemas/protocolos compatibles:</strong>
<ul>
<li>http</li>
<li>HTTPS</li>
<li>FTP</li>
<li>SFTP</li>
<li>WCF</li>
<li>Bus de servicio</li>
<li>Blob de Azure</li>
<li>API de REST</li>
</ul>
</td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Alta disponibilidad</strong>
<br/><br/>
Para ver el Acuerdo de Nivel de Servicio, consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=304011">Detalles de precios de Azure BizTalk Services</a>.
</td>
<td>No se incluye</td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Copia de seguridad y restauración</strong></td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Seguimiento</strong></td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Archivado</strong><br/><br/>
Incluye la recepción sin rechazo (NRR) y la descarga de mensajes controlados</td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>No se incluye</td>
<td>No se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Uso de código personalizado</strong></td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
<tr>
<td><strong>Uso de transformaciones, lo que incluye XSLT personalizado</strong></td>
<td>No se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
<td>Se incluye</td>
</tr>
</table>

> [!NOTE]
> Para la resistencia frente a los errores de hardware, la Alta disponibilidad implica disponer de varias máquinas virtuales en una sola unidad BizTalk.
> 
> 

## <a name="faqs"></a>Preguntas más frecuentes
#### <a name="what-is-a-biztalk-unit"></a>¿Qué es una unidad BizTalk?
Una "unidad" es el nivel atómica de Hola de una implementación de servicios de BizTalk de Azure. Cada edición incluye una unidad con distinta memoria y capacidad de proceso. Por ejemplo, una unidad Basic tiene más proceso que Developer, Standard tiene más proceso que Basic, etc. Cuando escala un servicio de BizTalk, se escala en términos de unidades.

#### <a name="what-is-hello-difference-between-biztalk-services-and-azure-biztalk-vm"></a>¿Cuál es la diferencia de hello entre los servicios de BizTalk y la máquina virtual de BizTalk de Azure?
Servicios de BizTalk proporciona una arquitectura de plataforma como-servicio (PaaS) true para generar soluciones de integración en nube Hola. Con el modelo de PaaS de hello, por completo y centrarse en la lógica de la aplicación hello deje todas tooMicrosoft de administración de infraestructura de hello, incluidos:

* No hay necesidad de toomanage o revisión de máquinas virtuales.
* Microsoft garantiza la disponibilidad.
* Controlar la escala a petición simplemente solicitando más o menos capacidad a través de hello portal de Azure.

BizTalk Server en Máquinas virtuales de Azure proporciona una arquitectura de infraestructura como servicio (IaaS). Crear máquinas virtuales y configurar exactamente igual que su entorno local, lo que sea más fácil toorun las aplicaciones existentes en la nube de hello sin realizar ningún cambio en el código. Con IaaS, son sigue siendo responsable de configurar las máquinas virtuales de hello, la administración de máquinas virtuales de hello (por ejemplo, instalar software y revisiones del sistema operativo) y la arquitectura de aplicación Hola para alta disponibilidad.

Si busca crear nuevas soluciones de integración que minimicen su esfuerzo de administración de la infraestructura, utilice Servicios de BizTalk. Si desea tooquickly migrar las soluciones de BizTalk existentes o para un entorno de petición toodevelop y probar el servidor BizTalk Server para examinar las aplicaciones, usar BizTalk Server en una máquina Virtual de Azure.

#### <a name="what-is-hello-difference-between-biztalk-adapter-service-and-hybrid-connections"></a>¿Cuál es la diferencia de hello entre el servicio de adaptador de BizTalk y las conexiones híbridas?
Hola servicio del adaptador de BizTalk se utiliza un servicio de BizTalk de Azure. Hola servicio del adaptador de BizTalk utiliza un sistema de línea de negocio (LOB) de hello BizTalk Adapter Pack tooconnect tooan local. Una conexión híbrida proporciona una manera fácil y cómodo tooconnect aplicaciones de Azure, como característica de las aplicaciones Web de hello en el servicio de aplicación de Azure y servicios móviles de Azure, tooan recursos locales.

#### <a name="what-does-hybrid-connection-data-transfer-gb-per-unit-mean-is-this-per-minutehourdayweekmonth-what-happens-when-hello-limit-is-reached"></a>Significado de la transferencia de datos de conexiones híbridas (GB) por unidad ¿Es por minuto/hora/día/semana/mes? ¿Qué ocurre cuando se alcanza el límite de hello?
Hola costo de conexión híbrida por unidad depende de la edición de servicios de BizTalk de Hola. En pocas palabras, los costos dependen de la cantidad de datos que transfiera. Por ejemplo, transferir 10 GB de datos al día cuesta menos que transferir 100 GB al día. Hola de uso [Calculadora de precios](https://azure.microsoft.com/pricing/calculator/?scenario=full) costos específicos de toodetermine de servicios de BizTalk. Normalmente, los límites de Hola se aplican diariamente. Si se supera el límite de hello, cualquier por encima del límite se cobra a velocidad de Hola de 1 USD por GB.

#### <a name="when-i-create-an-agreement-in-biztalk-services-why-does-hello-number-of-bridges-go-up-by-two-instead-of-just-one"></a>Al crear un acuerdo de servicios de BizTalk, ¿por qué número Hola de puentes Subir por dos en lugar de simplemente uno?
Cada contrato consta de dos puentes distintos: un puente de comunicación de envío y un puente de comunicación de recepción.

#### <a name="what-happens-when-i-hit-hello-quota-limit-on-hello-number-of-bridges-or-agreements"></a>¿Qué ocurre cuando alcanza el límite de cuota de hello en número de Hola de puentes o contratos de?
Está toodeploy no se pueden los puentes nuevos o crear los nuevos contratos. toodeploy más, es necesario tooscale toomore unidades de servicio de BizTalk de Hola o tooa actualización de edición superior.

#### <a name="how-do-i-migrate-from-one-tier-of-biztalk-services-tooanother"></a>¿Cómo migrar desde un nivel de servicios de BizTalk tooanother?
Edición gratuita de Hello no puede ser el nivel de migración o 'escalado vertical' tooanother y no se realizará copia de seguridad y restaura el nivel de tooanother. Si necesita otro nivel, cree un BizTalk Service nueva con el nuevo nivel de Hola. Los artefactos que se creó mediante la edición gratuita de hello, incluidas las conexiones híbridas, toobe necesidad de volver a crear en Hola nueva BizTalk Service. 

Para las ediciones restantes de hello, usar copia de seguridad de Hola y restauración para migrar los artefactos de tooanother de una capa. Por ejemplo, una copia de los artefactos en el nivel estándar de hello y, después, restaurarla nivel Premium de toohello. [Servicios de BizTalk: Backup y Restore](biztalk-backup-restore.md) se describen las rutas de migración de hello admitida y qué artefactos se copian. Tenga en cuenta que no se realiza copia de seguridad de las conexiones híbridas. Después de realizar copias de seguridad y restauración tooa nueva capa, se vuelva a crear las conexiones híbridas de Hola.  

#### <a name="is-hello-biztalk-adapter-service-included-in-hello-service-how-do-i-receive-hello-software"></a>¿Hola servicio del adaptador de BizTalk incluye servicio Hola? ¿Cómo se puede recibir software Hola?
Sí, se incluyen con hello SDK de servicios de BizTalk de Azure Hola servicio del adaptador de BizTalk con BizTalk Adapter Pack hello [descargar](http://www.microsoft.com/download/details.aspx?id=39087).

## <a name="next-steps"></a>Pasos siguientes
Hola toocreate servicios de BizTalk de Azure en Azure, vaya a demasiado[servicios de BizTalk: aprovisionamiento mediante Hola portal de Azure](biztalk-provision-services.md). toostart crear aplicaciones, vaya demasiado[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).

## <a name="additional-resources"></a>Recursos adicionales
* [Servicios de BizTalk: Aprovisionamiento mediante Hola portal de Azure](biztalk-provision-services.md)<br/>
* [Servicios de BizTalk: gráfico del estado de aprovisionamiento](biztalk-service-state-chart.md)<br/>
* [Servicios de BizTalk: pestañas Panel, Monitor y Escala](biztalk-dashboard-monitor-scale-tabs.md)<br/>
* [BizTalk Services: Backup and restore](biztalk-backup-restore.md)<br/>
* [Servicios de BizTalk: limitaciones](biztalk-throttling-thresholds.md)<br/>
* [Servicios de BizTalk: nombre del emisor y clave del emisor](biztalk-issuer-name-issuer-key.md)<br/>
* [¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>

