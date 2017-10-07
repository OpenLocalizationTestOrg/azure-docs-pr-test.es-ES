---
title: "supervisión de aaaSecurity en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este artículo le ayuda a tooget a trabajar con las funciones en el centro de seguridad de Azure de seguimiento."
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
ms.openlocfilehash: 43c2a8864d5fe27ba44b0d7bc979db970305ec17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="security-health-monitoring-in-azure-security-center"></a>Supervisión del estado de seguridad en el Centro de seguridad de Azure
En este artículo le ayuda a usar hello las capacidades de seguimiento en las directivas de cumplimiento de toomonitor centro de seguridad de Azure.

## <a name="what-is-security-health-monitoring"></a>¿Qué es la supervisión del estado de seguridad?
Creemos que a menudo de supervisión como observan y espera que un evento toooccur que podamos reaccionar toohello situación. Supervisión de la seguridad refiere toohaving una estrategia proactiva que audita los sistemas de tooidentify de recursos que no cumplen los estándares de la organización o los procedimientos recomendados.

## <a name="monitoring-security-health"></a>Supervisión del estado de seguridad
Después de habilitar [las directivas de seguridad](security-center-policies.md) para obtener recursos de una suscripción, el centro de seguridad analiza la seguridad de Hola de sus tooidentify posibles vulnerabilidades de recursos. La información acerca de la configuración de la red está disponible de inmediato. Puede tardar una hora o para obtener información acerca de la configuración de máquina virtual, como la seguridad de la actualización de estado y configuración del sistema operativo, toobecome disponible. Puede ver el estado de los recursos y de los problemas de seguridad de Hola Hola **prevención** sección. También puede ver una lista de los problemas en hello **recomendaciones** icono.

Para obtener más información acerca de cómo obtener recomendaciones tooapply, leer [implementar recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md).

En hello **prevención** sección, puede supervisar el estado de seguridad de Hola de los recursos. En el siguiente ejemplo de Hola, puede ver que en el mosaico de cada recurso (proceso, redes, almacenamiento de & datos y aplicaciones) tiene Hola número total de problemas que se identificaron.

![Icono de estado de seguridad de los recursos](./media/security-center-monitoring/security-center-monitoring-fig1-newUI-2017.png)


### <a name="monitor-compute"></a>Supervisión de proceso
Al hacer clic en **proceso** icono, hello **proceso** hoja que se abre muestra tres fichas:

- **Overview** (Información general): recomendaciones de supervisión y de la máquina virtual.
- **Virtual Machines** (Máquinas virtuales): lista de todas las máquinas virtuales y su estado de seguridad actual.
- **Cloud Services** (Servicios en la nube): lista de todos los roles web y de trabajo que supervisa Security Center.

![Actualizaciones de sistema que faltan por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new002-2017.png)

En cada pestaña puede tener varias secciones, y en cada sección, puede seleccionar una opción individual toosee más detalles sobre Hola recomienda pasos tooaddress este problema. 

#### <a name="monitoring-recommendations"></a>Supervisión de las recomendaciones
Esta sección muestra el número total de Hola de máquinas virtuales que se han inicializado para la recopilación de datos y sus estados actuales. Una vez todas las máquinas virtuales que inicializa la recopilación de datos, estará listo tooreceive directivas de seguridad del centro de seguridad. Al hacer clic en esta entrada, Hola **agente de máquina virtual es falta o no responde** abre la hoja. 

![Actualizaciones de sistema que faltan por máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig1-new003-2017.png)


#### <a name="virtual-machine-recommendations"></a>Recomendaciones sobre máquinas virtuales
Esta sección contiene un conjunto de [recomendaciones para cada máquina virtual](security-center-virtual-machine-recommendations.md) supervisadas por Azure Security Center. Hola primera columna muestra recomendación Hola. Hola segunda columna muestra número total de Hola de máquinas virtuales que se ven afectados por dicha recomendación. Hola tercera columna muestra gravedad Hola de problema de hello como se muestra en la siguiente captura de pantalla de Hola.

![Recomendaciones sobre máquinas virtuales](./media/security-center-monitoring/security-center-monitoring-fig1-new004-2017.png)

> [!NOTE]
> Se muestran solo las máquinas virtuales que tienen al menos un punto de conexión público en hello **redes mantenimiento** hoja en hello **topología de red** lista.
>
>

Cada recomendación tiene un conjunto de acciones que se podrán realizar una vez que haga clic en ella. Por ejemplo, si hace clic en **que les faltan actualizaciones de sistema**, hello **que les faltan actualizaciones de sistema** abre la hoja. Muestra máquinas virtuales de Hola que faltan revisiones y Hola gravedad de actualización que falta Hola tal y como se muestra en hello siguiente captura de pantalla.

![Actualizaciones de sistema que faltan para las máquinas virtuales](./media/security-center-monitoring/security-center-monitoring-fig5-ga.png)

Hola **que les faltan actualizaciones de sistema** hoja muestra una tabla con hello siguiente información:

* **MÁQUINA VIRTUAL**: nombre de Hola de máquina virtual de Hola que faltan actualizaciones.
* **ACTUALIZACIONES del sistema**: Hola número de actualizaciones del sistema que faltan.
* **HORA del último RECORRIDO**: tiempo de presentación que el centro de seguridad último análisis de máquina virtual de Hola para las actualizaciones.
* **ESTADO**: Hola estado actual de la recomendación de hello:
  * **Abra**: recomendación de hello no se haya tratado todavía.
  * **En curso**: recomendación de saludo se está aplicada toothose recursos y no se requiere ninguna acción por parte del usuario.
  * **Resolver**: recomendación de hello ya ha terminado. (Cuando se ha resuelto el problema de hello, aparece atenuado entrada hello).
* **GRAVEDAD**: describe la gravedad de Hola de esa recomendación determinada:
  * **Alta**: existe una vulnerabilidad en un recurso importante (aplicación, máquina virtual o grupo de seguridad de red) y requiere atención.
  * **Medio**: pasos adicionales o no críticos son toocomplete requiere un proceso o eliminar una vulnerabilidad.
  * **Baja**: es preciso abordar una vulnerabilidad, pero esta no requiere una atención inmediata. (De forma predeterminada, no se presentan recomendaciones bajas, pero puede filtrar según las recomendaciones bajas si desea que tooview les.)

detalles de recomendación de hello tooview, haga clic en nombre de Hola de máquina virtual de Hola. Una nueva hoja de esa máquina virtual se abre con la lista Hola de actualizaciones tal y como se muestra en la siguiente captura de pantalla de Hola.

![Actualizaciones de sistema que faltan para una máquina virtual concreta](./media/security-center-monitoring/security-center-monitoring-fig6-ga.png)

> [!NOTE]
> Hello las recomendaciones de seguridad aquí son Hola igual que los de hello **recomendaciones** hoja. Vea hello [implementar recomendaciones de seguridad en Azure Security Center](security-center-recommendations.md) artículo para obtener más información acerca de cómo tooresolve recomendaciones. Esto es aplicable no solo para máquinas virtuales sino también para todos los recursos que están disponibles en hello **estado de los recursos** icono.
>
>

#### <a name="virtual-machines-section"></a>Sección Máquinas virtuales
sección de máquinas virtuales de Hello ofrece una visión general de todas las máquinas virtuales y las recomendaciones. Cada columna representa un conjunto de recomendaciones tal y como se muestra en la siguiente captura de pantalla de hello:

![Información general de todas las máquinas virtuales y recomendaciones](./media/security-center-monitoring/security-center-monitoring-fig1-new005-2017.png)

icono de Hola que aparece debajo de cada recomendación, le ayuda a tooquickly identificar máquinas virtuales de Hola que necesitan atención y tipo de la recomendación de Hola.

En el ejemplo anterior de hello, una máquina virtual tiene una recomendación relativa a la protección de extremos crítica. tooget obtener más información acerca de la máquina virtual de hello, haga clic en él. Una nueva hoja que se abre representa esta máquina virtual tal como se muestra en la siguiente captura de pantalla de Hola.

![Detalles sobre la seguridad de máquina virtual](./media/security-center-monitoring/security-center-monitoring-fig8-ga.png)

Esta hoja con información detallada de la seguridad de hello para la máquina virtual de Hola. De hello parte inferior de esta hoja, puede ver Hola recomienda acción y la gravedad de Hola de cada problema.

#### <a name="cloud-services-section"></a>Sección de servicios en la nube
Servicios de nube, se crea una recomendación cuando la versión del sistema operativo Hola está anticuada tal y como se muestra en la siguiente captura de pantalla de hello:

![Estado de mantenimiento de los servicios en la nube](./media/security-center-monitoring/security-center-monitoring-fig1-new006-2017.png)

En un escenario donde haya recomendación (que no es así de hello en hello ejemplo anterior), deberá toofollow pasos de hello en la versión de sistema operativo de hello recomendación tooupdate Hola. Cuando hay disponible una actualización, tendrá una alerta (de color rojo o naranja - depende Hola gravedad del problema de hello). Al hacer clic en esta alerta en filas de hello WebRole1 (se ejecuta Windows Server con su tooIIS de aplicación que se implementan de forma automática de web) o WorkerRole1 (se ejecuta Windows Server con su tooIIS de aplicación que se implementan automáticamente web), se abre una nueva hoja con más detalles sobre esto recomendación tal y como se muestra en la siguiente captura de pantalla de hello:

![Detalles del servicio en la nube](./media/security-center-monitoring/security-center-monitoring-fig8-new3.png)

toosee una explicación más descriptiva acerca de esta recomendación, haga clic en **versión del sistema operativo de la actualización** en hello **descripción** columna. Hola **versión del sistema operativo de la actualización (vista previa)** hoja se abre con más detalles.

![Recomendaciones de servicios en la nube](./media/security-center-monitoring/security-center-monitoring-fig8-new4.png)  

### <a name="monitor-virtual-networks"></a>Supervisión de redes virtuales
Al hacer clic en **red** icono, hello **red** hoja se abre con más detalles, como se muestra en la siguiente captura de pantalla de Hola:

![Hoja Redes](./media/security-center-monitoring/security-center-monitoring-fig9-new3.png)

#### <a name="networking-recommendations"></a>Recomendaciones de redes
Al igual que hello información de estado del recurso de la máquina virtual, esta hoja proporciona una lista resumida de los problemas en la parte superior de Hola de hoja de hello y una lista de redes supervisadas en la parte inferior de Hola.

Hola sección de clasificación de estado de red se enumeran los posibles problemas de seguridad y ofrece [recomendaciones](security-center-network-recommendations.md). Entre los posibles problemas se pueden incluir:

* Firewall de próxima generación (NGFW) no instalado
* Grupos de seguridad de red en subredes no habilitados
* Grupos de seguridad de red en máquinas virtuales no habilitados
* Restringir el acceso externo por medio de puntos de conexión externos públicos
* Puntos de conexión con conexión a Internet correctos

Al hacer clic en una recomendación, se abre una nueva hoja con más detalles acerca de la recomendación de Hola tal y como se muestra en el siguiente ejemplo de Hola.

![Detalles de una recomendación en la hoja de redes de Hola](./media/security-center-monitoring/security-center-monitoring-fig9-ga.png)

En este ejemplo, Hola **configurar falta red grupos de seguridad para las subredes** hoja tiene una lista de subredes y protección del grupo de seguridad de red de máquinas virtuales que faltan. Si hace clic en hello subred toowhich desea que el grupo de seguridad de red de tooapply hello, se abre otra hoja.

Hola **elegir grupo de seguridad de red** hoja, puede seleccionar grupo de seguridad de red más adecuada de hello para la subred de hello, o puede crear un nuevo grupo de seguridad de red.

#### <a name="internet-facing-endpoints-section"></a>Sección Internet facing endpoints
Hola **con conexión a puntos de conexión de Internet** sección, puede ver máquinas virtuales de Hola que están actualmente configuradas con un orientada hacia el extremo y el estado actual de Internet.

![Máquinas virtuales configuradas con puntos de conexión accesibles desde Internet y su estado](./media/security-center-monitoring/security-center-monitoring-fig10-ga.png)

Esta tabla tiene el nombre de extremo de Hola que representa máquina virtual de hello, hello orientado a la dirección IP, Internet y Hola estado actual de gravedad del grupo de seguridad de red de Hola y Hola NGFW. Hola tabla está ordenada por gravedad:

* Rojo (arriba): alta prioridad; se debe solucionar de inmediato.
* Naranja: prioridad media; se debe solucionar lo antes posible.
* Verde (al final): estado de mantenimiento.

#### <a name="networking-topology-section"></a>Sección Networking topology
Hola **topología de red** sección tiene una vista jerárquica de los recursos de hello tal y como se muestra en la siguiente captura de pantalla de hello:

![Vista jerárquica de los recursos en la sección de topología de redes](./media/security-center-monitoring/security-center-monitoring-fig121-new4.png)

Esta tabla está ordenada (máquinas virtuales y subredes) por gravedad:

* Rojo (arriba): alta prioridad; se debe solucionar de inmediato.
* Naranja: prioridad media; se debe solucionar lo antes posible.
* Verde (al final): estado de mantenimiento.

En esta vista de topología, tiene el primer nivel de hello [redes virtuales](../virtual-network/virtual-networks-overview.md), [puertas de enlace de red virtual](/vpn-gateway/vpn-gateway-site-to-site-create.md), y [redes virtuales (clásicas)](/virtual-network/virtual-networks-create-vnet-classic-pportal.md). segundo nivel de Hello tiene subredes y tercer nivel de hello tiene máquinas virtuales de Hola que pertenecen toothose subredes. columna derecha de Hello tiene el estado actual de hello del grupo de seguridad de red de Hola para esos recursos, como se muestra en el siguiente ejemplo de Hola:

![Estado del grupo de seguridad de red de hello en la sección de topología de red](./media/security-center-monitoring/security-center-monitoring-fig12-ga.png)

Hello parte inferior de esta hoja contiene recomendaciones para esta máquina virtual, que es similar el Hola toowhat se ha descrito anteriormente. Puede hacer clic una toolearn recomendación más o aplicar Hola necesitado un control de seguridad o configuración.

### <a name="monitor-storage--data"></a>Supervisión de Almacenamiento y datos

Al hacer clic en **almacenamiento & datos** en hello **prevención** sección hello **los recursos de datos** hoja se abre con las recomendaciones para SQL y almacenamiento. También tiene [recomendaciones](security-center-sql-service-recommendations.md) Hola general estado de mantenimiento de base de datos de Hola. Para más información acerca del cifrado de almacenamiento, consulte [Enable encryption for Azure storage account in Azure Security Center](security-center-enable-encryption-for-storage-account.md) (Habilitación del cifrado para la cuenta de almacenamiento de Azure en Azure Security Center).

![Recursos de datos](./media/security-center-monitoring/security-center-monitoring-fig13-newUI-2017.png)

En **recomendaciones de SQL**, puede hacer clic en cualquier recomendación y obtener más detalles sobre tooresolve de acción más un problema. Hello en el ejemplo siguiente se muestra expansión Hola de hello **detección de auditoría de base de datos y amenazas en las bases de datos SQL** recomendación.

![Detalles acerca de una recomendación de SQL](./media/security-center-monitoring/security-center-monitoring-fig14-ga-new.png)

Hola **habilitar auditoría y amenaza para la detección en las bases de datos SQL** hoja tiene Hola siguiente información:

* Una lista de bases de datos SQL.
* servidor de Hello en el que se encuentran
* Información sobre si esta configuración se ha heredado del servidor de Hola o si es único en esta base de datos
* estado actual de Hola
* gravedad de Hola de problema de Hola

Al hacer clic en hello tooaddress de base de datos de esta recomendación, Hola **detección de auditoría y amenaza** hoja se abre como se muestra en hello después de la pantalla.

![Hoja de auditoría y detección de amenazas](./media/security-center-monitoring/security-center-monitoring-fig15-ga.png)

auditoría de tooenable, seleccione **ON** en hello **auditoría** opción.

### <a name="monitor-applications"></a>Supervisión de aplicaciones

Si la carga de trabajo de Azure tiene aplicaciones ubicadas en [máquinas virtuales (creadas mediante el Administrador de recursos de Azure)](../azure-resource-manager/resource-manager-deployment-model.md) con puertos web expuestos (puertos TCP 80 y 443), el centro de seguridad puede supervisar los posibles problemas de seguridad tooidentify y recomienda los pasos de corrección. Al hacer clic en hello **aplicaciones** icono, hello **aplicaciones** hoja se abre con una serie de recomendaciones de hello **las recomendaciones de aplicaciones** sección. También se muestra el desglose de la aplicación hello por dirección IP virtual/host tal y como se muestra en la siguiente captura de pantalla de Hola.

![Estado de la seguridad de las aplicaciones](./media/security-center-monitoring/security-center-monitoring-fig16-ga.png)

Al igual que con hello otras recomendaciones, puede hacer clic en una recomendación toosee más detalles sobre el problema de Hola y cómo tooremediate. ejemplo de Hola Hola figura siguiente es una aplicación que se identificó como una aplicación web no segura. Cuando se selecciona la aplicación hello que se considera no seguro, abre otra hoja con hello después de la opción disponible:

![Detalles acerca de una aplicación que no es segura](./media/security-center-monitoring/security-center-monitoring-fig17-ga.png)

Esta hoja tendrá una lista de todas las recomendaciones para esta aplicación. Al hacer clic en hello **agregar un servidor de seguridad de la aplicación web** recomendación, hello **agregar un servidor de seguridad de la aplicación Web** hoja abre con opciones para tooinstall un servidor de aplicaciones web (WAFS) de un socio comercial como se muestra en la siguiente captura de pantalla de Hola.

![Cuadro de diálogo Agregar un firewall de aplicaciones web](./media/security-center-monitoring/security-center-monitoring-fig18-ga.png)

## <a name="see-also"></a>Otras referencias
En este artículo, se habrá aprendido cómo toouse capacidades en el centro de seguridad de Azure de supervisión. toolearn más información acerca del centro de seguridad de Azure, vea Hola recursos siguientes:

* [Configuración de directivas de seguridad de Azure Security Center](security-center-policies.md): Obtenga información acerca de cómo tooconfigure configuración de seguridad en el centro de seguridad de Azure.
* [Toosecurity responde y administrar las alertas en Azure Security Center](security-center-managing-and-responding-alerts.md): Obtenga información acerca de cómo las alertas de toosecurity toomanage y que responden.
* [Supervisión de soluciones de socios comerciales con Azure Security Center](security-center-partner-solutions.md): Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
* [Preguntas más frecuentes de Azure Security Center](security-center-faq.md): preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
* [Blog de seguridad de Azure](http://blogs.msdn.com/b/azuresecurity/): encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.
