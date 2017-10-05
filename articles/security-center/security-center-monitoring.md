---
title: "Supervisión de la seguridad en Azure Security Center | Microsoft Docs"
description: "Este artículo le ayuda a comenzar a trabajar con las funcionalidades de supervisión en Azure Security Center."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 3bd5b122-1695-495f-ad9a-7c2a4cd1c808
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: yurid
ms.openlocfilehash: 93fff129afb04e3a1896d275551f585f45658d6d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Supervisión del estado de seguridad en el Centro de seguridad de Azure
Este artículo le ayuda a usar las funcionalidades de supervisión de Azure Security Center para supervisar el cumplimiento de las directivas.

## <a name="what-is-security-health-monitoring"></a>¿Qué es la supervisión del estado de seguridad?
Con frecuencia se piensa que supervisar es observar y esperar que se produzca un evento, para así poder reaccionar ante la situación. La supervisión de seguridad se refiere a contar con una estrategia proactiva que audita los recursos a fin de identificar los sistemas que no cumplen con los estándares o los procedimientos recomendados de la organización.

## <a name="monitoring-security-health"></a>Supervisión del estado de seguridad
Después de habilitar las [directivas de seguridad](security-center-policies.md) para los recursos de una suscripción, Security Center analizará la seguridad de los recursos para identificar vulnerabilidades potenciales. La información acerca de la configuración de la red está disponible de inmediato. Sin embargo, la información acerca de la configuración de las máquinas virtuales, como el estado de las actualizaciones de seguridad y la configuración del sistema operativo, puede tardar una hora, o más, en estar disponible. Puede ver el estado de seguridad de sus recursos, además de cualquier problema, en la sección **Prevención**. Una lista de dichos problemas también se puede encontrar en el icono **Recomendaciones**.

Para más información sobre cómo aplicar las recomendaciones, lea [Implementación de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md).

En la sección **Prevención**, puede supervisar el estado de seguridad de los recursos. En el ejemplo siguiente, puede ver que, en el icono de cada recurso (Proceso, Redes, Almacenamiento y datos, y Aplicación) tiene el número total de problemas que se han identificado.

![Icono de estado de seguridad de los recursos](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Supervisión de proceso
Al hacer clic en el icono **Proceso**, se abre la hoja **Proceso**, que contiene tres pestañas:

- **Overview** (Información general): recomendaciones de supervisión y de la máquina virtual.
- **Virtual Machines** (Máquinas virtuales): lista de todas las máquinas virtuales y su estado de seguridad actual.
- **Cloud Services** (Servicios en la nube): lista de todos los roles web y de trabajo que supervisa Security Center.

![Actualizaciones de sistema que faltan por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

Todas las pestañas pueden tener varias secciones y en cada una de ella se puede seleccionar cualquiera de las opciones para ver más detalles acerca de los pasos recomendados para abordar un problema concreto. 

#### <a name="monitoring-recommendations"></a>Supervisión de las recomendaciones
En esta sección se muestra el número total de máquinas virtuales que se inicializaron para la recopilación de datos y su estado actual. Una vez que se haya inicializado la recopilación de datos en todas las máquinas virtuales, estarán listas para recibir las directivas de seguridad de Security Center. Al hacer clic en esta entrada, se abre la hoja **VM Agent is missing or not responding** (El agente de máquina virtual falta o no responde). 

![Actualizaciones de sistema que faltan por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Recomendaciones sobre máquinas virtuales
Esta sección contiene un conjunto de [recomendaciones para cada máquina virtual](security-center-virtual-machine-recommendations.md) supervisadas por Azure Security Center. La primera columna muestra la recomendación. La segunda columna muestra el número total de máquinas virtuales a las que afecta esa recomendación. La tercera columna muestra la gravedad del problema como se muestra en la captura de pantalla siguiente.

![Recomendaciones sobre máquinas virtuales](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Solo las máquinas virtuales con al menos un punto de conexión público se muestran en la hoja de **estado de red** en la lista de **topología de red**.
>
>

Cada recomendación tiene un conjunto de acciones que se podrán realizar una vez que haga clic en ella. Por ejemplo, si hace clic en **Actualizaciones del sistema que faltan**, se abrirá la hoja **Actualizaciones del sistema que faltan**. En dicha hoja se enumeran las máquinas virtuales a las que faltan revisiones y la gravedad de la actualización que falta, como se muestra en la siguiente captura de pantalla.

![Actualizaciones de sistema que faltan para las máquinas virtuales](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

La hoja **Actualizaciones del sistema que faltan** muestra una tabla con la siguiente información:

* **MÁQUINA VIRTUAL**: el nombre de la máquina virtual en la que faltan actualizaciones.
* **ACTUALIZACIONES DEL SISTEMA**: el número actualizaciones del sistema que faltan.
* **HORA DEL ÚLTIMO EXAMEN**: la hora en que Security Center realizó el último examen de la máquina virtual en busca de actualizaciones.
* **ESTADO**: el estado actual de la recomendación:
  * **Abierta**: la recomendación aún no se ha abordado.
  * **En curso**: la recomendación se está aplicando actualmente a esos recursos y no se requiere ninguna acción por su parte.
  * **Resuelta**: la recomendación ya terminó. (Si se ha resuelto el problema, la entrada aparecerá atenuada).
* **GRAVEDAD**: describe la gravedad de una recomendación concreta:
  * **Alta**: existe una vulnerabilidad en un recurso importante (aplicación, máquina virtual o grupo de seguridad de red) y requiere atención.
  * **Media**: para completar un proceso o eliminar una vulnerabilidad se requieren pasos adicionales o no críticos.
  * **Baja**: es preciso abordar una vulnerabilidad, pero esta no requiere una atención inmediata. (De manera predeterminada no se muestran las recomendaciones bajas, pero si desea verlas, puede filtrar por ellas).

Para ver los detalles de las recomendaciones, haga clic en el nombre de la máquina virtual. Aparecerá una nueva hoja para esa máquina virtual con la lista de actualizaciones tal y como se muestra en la siguiente captura de pantalla.

![Actualizaciones de sistema que faltan para una máquina virtual concreta](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Las recomendaciones de seguridad son las mismas que aparecen en la hoja **Recomendaciones**. Para más información sobre cómo resolver las recomendaciones, consulte [Implementación de recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md). Esto no se aplica solo a las máquinas virtuales, sino también a todos los recursos disponibles en el icono **Estado de los recursos**.
>
>

#### <a name="virtual-machines-section"></a>Sección Máquinas virtuales
La sección de máquinas virtuales ofrece una visión general de todas las máquinas virtuales y recomendaciones. Cada columna representa un conjunto de recomendaciones tal como se muestra en la siguiente captura de pantalla:

![Información general de todas las máquinas virtuales y recomendaciones](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

El icono que aparece en cada recomendación le ayuda a identificar rápidamente tanto las máquinas virtuales que necesitan atención como el tipo de recomendación que necesitan.

En el ejemplo anterior, una máquina virtual tiene una recomendación crítica sobre la protección del punto de conexión. Para más información acerca de la máquina virtual, haga clic en ella. Se abrirá una nueva hoja que representa a esta máquina virtual como se muestra en la captura de pantalla siguiente.

![Detalles sobre la seguridad de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Esta hoja tiene los detalles de seguridad de la máquina virtual. En la parte inferior de la hoja puede ver la acción recomendada y la gravedad de cada problema.

#### <a name="cloud-services-section"></a>Sección de servicios en la nube
En el caso de los servicios en la nube, se crea una recomendación cuando la versión del sistema operativo está obsoleta, como se muestra en la siguiente captura de pantalla:

![Estado de mantenimiento de los servicios en la nube](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

En un escenario en el que haya alguna recomendación (lo que no ocurre en el ejemplo anterior), es preciso seguir los pasos descritos en la recomendación para actualizar la versión del sistema operativo. Cuando haya alguna actualización disponible, aparecerá una alerta (su color, rojo o naranja, depende de la gravedad del problema). Al hacer clic en esta alerta en las filas WebRole1 (ejecuta Windows Server con la aplicación web implementada automáticamente en IIS) o WorkerRole1 (ejecuta Windows Server con la aplicación web implementada automáticamente en IIS), se abre una nueva hoja con más datos acerca de esta recomendación, como se muestra en la siguiente captura de pantalla:

![Detalles del servicio en la nube](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

Para ver una explicación más preceptiva con respecto a esta recomendación, haga clic en **Actualizar versión del SO** en la columna **DESCRIPCIÓN**. Se abrirá la hoja **Actualizar versión del SO (versión preliminar)** con más detalles.

![Recomendaciones de servicios en la nube](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Supervisión de redes virtuales
Al hacer clic en el icono **Redes**, se abre la hoja **Redes**, donde encontrará más información, como se muestra en la siguiente captura de pantalla:

![Hoja Redes](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Recomendaciones de redes
De manera similar a la información del estado de los recursos de las máquinas virtuales, esta hoja proporciona una lista resumida de los problemas en la parte superior de la hoja y una lista de las redes supervisadas en la parte inferior.

La sección de desglose del estado de las redes enumera los potenciales problemas de seguridad y ofrece [recomendaciones](security-center-network-recommendations.md). Entre los posibles problemas se pueden incluir:

* Firewall de próxima generación (NGFW) no instalado
* Grupos de seguridad de red en subredes no habilitados
* Grupos de seguridad de red en máquinas virtuales no habilitados
* Restringir el acceso externo por medio de puntos de conexión externos públicos
* Puntos de conexión con conexión a Internet correctos

Al hacer clic en una recomendación, se abre una hoja nueva con más detalles acerca de la recomendación, como se muestra en el ejemplo siguiente.

![Detalles de una recomendación en la hoja de redes](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

En este ejemplo, la hoja **Configurar los grupos de seguridad de red que faltan para las subredes** tiene una lista de subredes y máquinas virtuales que carecen de la protección de grupo de seguridad de red. Si hace clic en la subred a la que desea aplicar el grupo de seguridad de red, se abrirá otra hoja.

En la hoja **Elegir grupo de seguridad de red**, puede seleccionar el grupo de seguridad de red más adecuado para la subred o crear uno.

#### <a name="internet-facing-endpoints-section"></a>Sección Internet facing endpoints
En la sección **Puntos de conexión accesibles desde Internet**, podrá ver las máquinas virtuales que están configuradas con un punto de conexión accesible desde Internet y su estado actual.

![Máquinas virtuales configuradas con puntos de conexión accesibles desde Internet y su estado](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Esta tabla incluye el nombre del punto de conexión que representa la máquina virtual, la dirección IP accesible desde Internet, el estado de gravedad actual del grupo de seguridad de red y el NGFW. La tabla está ordenada por gravedad:

* Rojo (arriba): alta prioridad; se debe solucionar de inmediato.
* Naranja: prioridad media; se debe solucionar lo antes posible.
* Verde (al final): estado de mantenimiento.

#### <a name="networking-topology-section"></a>Sección Networking topology
En la sección **Topología de red**, se ofrece una vista jerárquica de los recursos, como se muestra en la siguiente captura de pantalla:

![Vista jerárquica de los recursos en la sección de topología de redes](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Esta tabla está ordenada (máquinas virtuales y subredes) por gravedad:

* Rojo (arriba): alta prioridad; se debe solucionar de inmediato.
* Naranja: prioridad media; se debe solucionar lo antes posible.
* Verde (al final): estado de mantenimiento.

En esta vista de topología, el primer nivel tiene [redes virtuales](../virtual-network/virtual-networks-overview.md), [puertas de enlace de red virtual](/vpn-gateway/vpn-gateway-site-to-site-create.md) y [redes virtuales (clásicas)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). El segundo nivel tiene subredes y el tercero, las máquinas virtuales que pertenecen a esas subredes. La columna derecha contiene el estado actual del grupo de seguridad de red para esos recursos, tal como se muestra en el ejemplo siguiente:

![Estado del grupo de seguridad de red en la sección de topología de redes](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

En la parte inferior de esta hoja, aparecerán las recomendaciones para esta máquina virtual, parecidas a las que se han descrito antes. Puede hacer clic en una recomendación para ver más información o aplicar la configuración o el control de seguridad necesario.

### <a name="monitor-storage--data"></a>Supervisión de Almacenamiento y datos

Al hacer clic en **Almacenamiento y datos** en la sección **Prevención**, se abre la hoja **Recursos de datos** con las recomendaciones para SQL y Storage. También tiene [recomendaciones](security-center-sql-service-recommendations.md) sobre el estado general de la base de datos. Para más información acerca del cifrado de almacenamiento, consulte [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md) (Habilitación del cifrado para la cuenta de almacenamiento de Azure en Azure Security Center).

![Recursos de datos](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

En **SQL Recommendations** (Recomendaciones de SQL) puede hacer clic en cualquier recomendación y obtener más detalles acerca de cómo realizar más acciones para resolver un problema. El ejemplo siguiente muestra la expansión de la recomendación **Auditoría de la base de datos y detección de amenazas en bases de datos de SQL**.

![Detalles acerca de una recomendación de SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

La hoja **Habilitar la auditoría y la detección de amenazas en bases de datos SQL** contiene la siguiente información:

* Una lista de bases de datos SQL.
* El servidor en el que se encuentran.
* Información sobre si esta configuración se heredó del servidor o si es única en la base de datos.
* El estado actual.
* La gravedad del problema.

Al hacer clic en la base de datos para abordar esta recomendación, se abrirá la hoja **Auditoría y detección de amenazas**, como se muestra en la siguiente pantalla.

![Hoja de auditoría y detección de amenazas](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

Para habilitar la auditoría, seleccione **Activar** en la opción **Auditoría**.

### <a name="monitor-applications"></a>Supervisión de aplicaciones

Si la carga de trabajo de Azure tiene aplicaciones en las [máquinas virtuales (creadas con Resource Manager)](../azure-resource-manager/resource-manager-deployment-model.md) con puertos web expuestos (puertos TCP 80 y 443), Security Center puede supervisarlas para identificar posibles problemas de seguridad y recomendar pasos para su corrección. Al hacer clic en el icono **Aplicaciones**, se abrirá la hoja **Aplicaciones** con una serie de recomendaciones en la sección de **Recomendaciones sobre aplicaciones**. También mostrará el desglose de la aplicación por host o IP virtual, tal como aparece en la siguiente captura de pantalla.

![Estado de la seguridad de las aplicaciones](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Al igual que en las restantes recomendaciones, puede hacer clic en ella para ver más información acerca del problema y cómo corregirlo. El ejemplo que se muestra en la ilustración siguiente es una aplicación que se identificó como aplicación web no segura. Cuando selecciona la aplicación que se consideró como no segura, se abre otra hoja con la siguiente opción disponible:

![Detalles acerca de una aplicación que no es segura](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Esta hoja tendrá una lista de todas las recomendaciones para esta aplicación. Al hacer clic en la recomendación **Agregar un firewall de aplicaciones web**, se abrirá la hoja **Agregar un firewall de aplicaciones web**, en la que encontrará las opciones necesarias para instalar un firewall de aplicaciones web (WAF) de un asociado, como se muestra en la siguiente captura de pantalla.

![Cuadro de diálogo Agregar un firewall de aplicaciones web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Consulte también
En este artículo, aprendió a usar las funcionalidades de supervisión en Azure Security Center. Para obtener más información sobre el Centro de seguridad de Azure, consulte los siguientes recursos:

* [Establecimiento de directivas de seguridad en Azure Security Center](security-center-policies.md): obtenga información sobre cómo configurar los ajustes de seguridad en Azure Security Center.
* [Administración y respuesta a las alertas de seguridad en Azure Security Center](security-center-managing-and-responding-alerts.md): obtenga información sobre cómo administrar y responder a alertas de seguridad.
* [Supervisión de las soluciones de asociados con Azure Security Center](security-center-partner-solutions.md): aprenda a supervisar el estado de mantenimiento de las soluciones de asociados.
* [Preguntas más frecuentes sobre Azure Security Center](security-center-faq.md): encuentre las preguntas más frecuentes sobre el uso del servicio.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
