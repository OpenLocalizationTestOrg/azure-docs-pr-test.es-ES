---
title: "un clúster de Azure DC/OS - pila ELK aaaMonitor | Documentos de Microsoft"
description: "Supervisión de un clúster de DC/OS en un clúster de Azure Container Service con ELK (Elasticsearch, Logstash y Kibana)."
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Contenedores, DC/OS, supervisión, elk"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 8d81c5342616ec14880d38803cdf95f5845a669b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-elk"></a>Supervisión de un clúster de Azure Container Service con ELK
En este artículo, se muestra cómo la pila toodeploy Hola ELK (Elasticsearch, Logstash, Kibana) en un clúster de DC/OS en el servicio de contenedor de Azure. 

## <a name="prerequisites"></a>Requisitos previos
[Implemente](container-service-deployment.md) y [conecte](../container-service-connect.md) un clúster de DC/OS configurado por Azure Container Service. Explorar el panel de controlador de dominio/OS hello y servicios de maratón [aquí](container-service-mesos-marathon-ui.md). Instalar hello [equilibrador de carga de maratón](container-service-load-balancing.md).


## <a name="elk-elasticsearch-logstash-kibana"></a>ELK (Elasticsearch, Logstash, Kibana)
Pila ELK es una combinación de Elasticsearch, Logstash, y Kibana que proporciona una pila de tooend final que puede toomonitor usado y analizar los registros en el clúster.

## <a name="configure-hello-elk-stack-on-a-dcos-cluster"></a>Configurar la pila ELK hello en un clúster de DC/OS
Obtener acceso a la interfaz de usuario del controlador de dominio/OS a través de [http://localhost: 80 /](http://localhost:80/) una vez en hello navegar de interfaz de usuario del controlador de dominio/OS demasiado**universo**. Buscar e instalar Elasticsearch, Logstash y Kibana con hello universo de DC/OS y, en ese orden específico. Se puede obtener más información acerca de la configuración si va toohello **instalación avanzada** vínculo.

![ELK1](./media/container-service-monitoring-elk/elk1.PNG) ![ELK2](./media/container-service-monitoring-elk/elk2.PNG) ![ELK3](./media/container-service-monitoring-elk/elk3.PNG) 

Una vez Hola contenedores ELK y están activos y en funcionamiento, debe tooenable Kibana toobe tiene acceso a través de maratón LB. Navegue demasiado **servicios** > **kibana**y haga clic en **editar** tal y como se muestra a continuación.

![ELK4](./media/container-service-monitoring-elk/elk4.PNG)


Alternar demasiado**modo JSON** y desplácese hacia abajo de la sección de etiquetas toohello.
Necesita tooadd un `"HAPROXY_GROUP": "external"` entrada aquí tal como se muestra a continuación.
Una vez que haga clic en **Deploy changes** (Implementar cambios), se reinicia el contenedor.

![ELK5](./media/container-service-monitoring-elk/elk5.PNG)


Si desea que tooverify que Kibana está registrado como un servicio en el panel HAPROXY hello, deberá tooopen puerto 9090 en clúster de agente de hello tal y como HAPROXY se ejecuta en el puerto 9090.
De forma predeterminada, se abre los puertos 80, 8080 y Hola a 443 en el clúster de agente de DC/OS.
Instrucciones tooopen un puerto y proporcionar evaluar público se proporcionan [aquí](container-service-enable-public-access.md).

tooaccess Hola panel HAPROXY, interfaz de administración abierto Hola maratón LB en: `http://$PUBLIC_NODE_IP_ADDRESS:9090/haproxy?stats`.
Una vez que navegue toohello URL, debería ver el panel de hello HAPROXY tal y como se muestra a continuación y debería ver una entrada de servicio de Kibana.

![ELK6](./media/container-service-monitoring-elk/elk6.PNG)


panel de tooaccess hello Kibana, que se implementa en el puerto 5601, deberá tooopen puerto 5601. Siga las instrucciones que encontrará [aquí](container-service-enable-public-access.md). A continuación, abra el panel de Kibana hello en: `http://localhost:5601`.

## <a name="next-steps"></a>Pasos siguientes

* Con respecto al reenvío y configuración de registros de aplicaciones y sistemas, consulte [Log Management in DC/OS with ELK](https://docs.mesosphere.com/1.8/administration/logging/elk/) (Administración de registros en DC/OS con ELK).

* Consulte los registros de toofilter, [filtrar registros con ELK](https://docs.mesosphere.com/1.8/administration/logging/filter-elk/). 

 

