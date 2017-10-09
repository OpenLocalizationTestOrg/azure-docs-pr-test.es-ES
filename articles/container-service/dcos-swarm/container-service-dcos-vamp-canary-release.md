---
title: "versión de aaaCanary con Vamp en clúster de Azure DC/OS | Documentos de Microsoft"
description: "Cómo toouse Vamp toocanary servicios de lanzamiento y aplicar el filtrado en un clúster de servicio de contenedor de Azure DC/OS inteligente del tráfico"
services: container-service
author: gggina
manager: rasquill
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/17/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: e7b8658a161a7cddcf718e3e1c12a889a330d3d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="canary-release-microservices-with-vamp-on-an-azure-container-service-dcos-cluster"></a>Lanzamiento controlado de microservicios con Vamp en un clúster de DC/OS de Azure Container Service

En este tutorial, se configura Vamp en Azure Container Service con un clúster de DC/OS. Publicamos canary servicio de demostración de hello Vamp "sava" y, a continuación, resolver una incompatibilidad de servicio de hello con Firefox aplicando el filtrado de tráfico inteligente. 

> [!TIP] 
> En este tutorial Vamp se ejecuta en un clúster de DC/OS, pero también se puede utilizar Vamp con Kubernetes como orchestrator Hola.
>

## <a name="about-canary-releases-and-vamp"></a>Acerca de los lanzamientos controlados y Vamp


El [lanzamiento controlado](https://martinfowler.com/bliki/CanaryRelease.html) es una estrategia de implementación inteligente adoptada por organizaciones innovadoras como Netflix, Facebook y Spotify. Es un método que tiene sentido, ya que reduce los problemas, incluye redes de seguridad y aumenta la innovación. ¿Y por qué no se usa en todas las compañías? Extender una tooinclude de canalización de CI/CD estrategias canary agrega complejidad y requiere devops amplios conocimientos y experiencia. Que es suficiente tooblock pequeñas empresas y las empresas similares antes de que incluso empezar a trabajar. 

[Vamp](http://vamp.io/) es un sistema de código abierto diseñado tooease esta transición y poner canary liberando características tooyour preferido contenedor programador. La funcionalidad controlada de Vamp va más allá de las implementaciones basadas en porcentajes. El tráfico se puede filtrar y dividir en una amplia variedad de condiciones, por ejemplo tootarget determinados usuarios, intervalos de IP o dispositivos. Vamp realiza un seguimiento y un análisis de las métricas de rendimiento, lo que permite una automatización basada en datos reales. Puede configurar la reversión automática en caso de error o escalar variantes de servicios individuales en función de la carga o la latencia.

## <a name="set-up-azure-container-service-with-dcos"></a>Configuración de Azure Container Service con DC/OS



1. [Implemente un clúster de DC/OS](container-service-deployment.md) con un maestro y dos agentes de tamaño predeterminado. 

2. [Crear un túnel SSH](../container-service-connect.md) clúster de tooconnect toohello DC/OS. En este artículo se da por supuesto que tunelizar toohello clúster en el puerto local 80.


## <a name="set-up-vamp"></a>Configuración de Vamp

Ahora que tiene un clúster de DC/OS ejecución, puede instalar Vamp desde Hola interfaz de usuario del controlador de dominio/OS (http://localhost: 80). 

![Interfaz de usuario de DC/OS](./media/container-service-dcos-vamp-canary-release/01_set_up_vamp.png)

La instalación se lleva a cabo en dos fases:

1. **Implemente Elasticsearch**.

2. A continuación, **implementar Vamp** mediante la instalación de paquete de universo de hello Vamp DC/OS.

### <a name="deploy-elasticsearch"></a>Implementación de Elasticsearch

Vamp necesita Elasticsearch para recopilar y agregar métricas. Puede usar hello [magneticio Docker images](https://hub.docker.com/r/magneticio/elastic/) toodeploy una pila Vamp Elasticsearch compatible.

1. Hola de interfaz de usuario del controlador de dominio/OS, vaya demasiado**servicios** y haga clic en **implementar servicio**.

2. Seleccione **modo JSON** de hello **implementar nuevo servicio** emergente.

  ![Selección del modo JSON](./media/container-service-dcos-vamp-canary-release/02_deploy_service_json_mode.png)

3. Pegue en hello después de JSON. Esta configuración ejecuta el contenedor de hello con 1 GB de RAM y una comprobación básica del estado en el puerto de hello Elasticsearch.
  
  ```JSON
  {
    "id": "elasticsearch",
    "instances": 1,
    "cpus": 0.2,
    "mem": 1024.0,
    "container": {
      "docker": {
        "image": "magneticio/elastic:2.2",
        "network": "HOST",
        "forcePullImage": true
      }
    },
    "healthChecks": [
      {
        "protocol": "TCP",
        "gracePeriodSeconds": 30,
        "intervalSeconds": 10,
        "timeoutSeconds": 5,
        "port": 9200,
        "maxConsecutiveFailures": 0
      }
    ]
  }
  ```
  

3. Haga clic en **Implementar**.

  Controlador de dominio/OS implementa contenedor de hello Elasticsearch. Puede realizar el seguimiento del progreso en hello **servicios** página.  

  ![Implementación de Elasticsearch](./media/container-service-dcos-vamp-canary-release/03_deply_elasticsearch.png)

### <a name="deploy-vamp"></a>Implementación de Vamp

Una vez Elasticsearch notifica como **ejecuta**, puede agregar paquete de universo de DC/OS Vamp Hola. 

1. Vaya demasiado**universo** y busque **vamp**. 
  ![Vamp en el universo de DC/OS](./media/container-service-dcos-vamp-canary-release/04_universe_deploy_vamp.png)

2. Haga clic en **instalar** toohello siguiente vamp paquete y elija **instalación avanzada**.

3. Desplácese hacia abajo y escriba Hola después elasticsearch url: `http://elasticsearch.marathon.mesos:9200`. 

  ![Escriba la dirección URL de Elasticsearch](./media/container-service-dcos-vamp-canary-release/05_universe_elasticsearch_url.png)

4. Haga clic en **revise e instale**, a continuación, haga clic en **instalar** implementación de hello toostart.  

  DC/OS implementa todos los componentes de Vamp necesarios. Puede realizar el seguimiento del progreso en hello **servicios** página.
  
  ![Implementación de Vamp como paquete de universo](./media/container-service-dcos-vamp-canary-release/06_deploy_vamp.png)
  
5. Una vez completada la implementación, puede tener acceso a hello Vamp interfaz de usuario:

  ![Servicio de Vamp en DC/OS](./media/container-service-dcos-vamp-canary-release/07_deploy_vamp_complete.png)
  
  ![Interfaz de usuario de Vamp](./media/container-service-dcos-vamp-canary-release/08_vamp_ui.png)


## <a name="deploy-your-first-service"></a>Implementación de su primer servicio

Ahora que Vamp está en funcionamiento, implemente un servicio desde un plano. 

En su forma más simple, un [Vamp plano](http://vamp.io/documentation/using-vamp/blueprints/) describe Hola extremos (puertas de enlace), clústeres y toodeploy de servicios. Vamp usa clústeres toogroup diferentes variaciones de hello mismo servicio en grupos lógicos para liberar canary o A realizar pruebas A/b.  

Este escenario usa una aplicación monolítica de ejemplo denominada [**sava**](https://github.com/magneticio/sava), que se encuentra en la versión 1.0. monolito Hola se empaqueta en un contenedor de Docker, que se encuentra en Docker Hub en magneticio/sava:1.0.0. aplicación Hello normalmente se ejecuta en el puerto 8080, pero desea tooexpose en puerto 9050 en este caso. Implementar la aplicación hello a través de Vamp con un esquema simple.

1. Vaya demasiado**implementaciones**.

2. Haga clic en **Agregar**.

3. Pegar en hello después plano YAML. Este plano contiene un clúster con solo una variante de servicio, que se cambia en un paso posterior:

  ```YAML
  name: sava                        # deployment name
  gateways:
    9050: sava_cluster/webport      # stable endpoint
  clusters:
    sava_cluster:               # cluster toocreate
     services:
        -
          breed:
            name: sava:1.0.0        # service variant name
            deployable: magneticio/sava:1.0.0
            ports:
              webport: 8080/http # cluster endpoint, used for canary releasing
  ```

4. Haga clic en **Guardar**. Vamp inicia la implementación de Hola.

aparece la implementación de Hello en hello **implementaciones** página. Haga clic en hello implementación toomonitor su estado.

![Interfaz de usuario de Vamp: implementar sava](./media/container-service-dcos-vamp-canary-release/09_sava100.png)

![Servicio sava en la interfaz de usuario de Vamp](./media/container-service-dcos-vamp-canary-release/09a_sava100.png)

Se crean dos puertas de enlace, que se muestran en hello **puertas de enlace** página:

* un hello tooaccess de extremo estable ejecutando el servicio (puerto 9050) 
* una puerta de enlace interna administrada por Vamp (información sobre esta puerta de enlace más adelante). 

![Interfaz de usuario de Vamp: puertas de enlace de sava](./media/container-service-dcos-vamp-canary-release/10_vamp_sava_gateways.png)

Ahora ha implementado el servicio de Hello sava, pero no puede acceder externamente puesto Hola equilibrador de carga Azure desconoce tooforward tráfico tooit todavía. servicio de hello tooaccess, Hola de actualización de configuración de red de Azure.


## <a name="update-hello-azure-network-configuration"></a>Actualizar configuración de red de Azure Hola

Vamp implementa el servicio de sava de hello en nodos de agente de Hola DC/OS, exponer un extremo en el puerto 9050 estable. servicio de hello tooaccess del clúster de DC/OS Hola exterior, realizar las Hola siguiente configuración de red de Azure toohello de cambios en la implementación de clúster: 

1. **Configurar Hola equilibrador de carga Azure** para los agentes de hello (Hola recurso denominado **dcos-agent-lb-xxxx**) con un sondeo de estado y un tráfico de tooforward de regla en instancias de puerto 9050 toohello sava. 

2. **Grupo de seguridad de red de actualizaciones hello** para agentes pública hello (Hola recurso denominado **XXXX agente público nsg XXXX**) tooallow tráfico en el puerto 9050.

Para obtener pasos detallados toocomplete estas tareas con hello Azure portal, vea [habilitar la aplicación de servicio de contenedor de Azure de acceso público tooan](container-service-enable-public-access.md). Especifique el puerto 9050 en todas las configuraciones de puerto.


Una vez que todo se ha creado, vaya toohello **Introducción** hoja del equilibrador de carga de agente de Hola DC/OS (Hola recurso denominado **dcos-agent-lb-xxxx**). Buscar hello **dirección IP pública**y utilice Hola dirección tooaccess sava de puerto 9050.

![Azure Portal: obtener la dirección IP pública](./media/container-service-dcos-vamp-canary-release/18_public_ip_address.png)

![sava](./media/container-service-dcos-vamp-canary-release/19_sava100.png)


## <a name="run-a-canary-release"></a>Ejecución de un lanzamiento controlado

Suponga que tiene una nueva versión de esta aplicación que desea que la versión toocanary en producción. Tiene que incluir en contenedores como magneticio/sava:1.1.0 y toogo listo. Vamp le permite agregar fácilmente nuevos toohello de servicios ejecuta la implementación. Estos servicios "combinados" se implementan junto con los servicios existentes en clúster de Hola Hola y le asigna un peso de 0%. Tráfico no es servicio de tooa enrutado recién combinado hasta ajustar una distribución del tráfico Hola. control deslizante de peso de Hola Hola Vamp interfaz de usuario proporciona un control total sobre la distribución de hello, lo que permite ajustes incrementales (versión canary) o una reversión de la instantánea.

### <a name="merge-a-new-service-variant"></a>Combinación de una nueva variante de servicio

toomerge Hola nuevo sava 1.1 servicio con hello ejecutando implementación:

1. Hola Vamp interfaz de usuario, haga clic en **planos**.

2. Haga clic en **agregar** y pegar en hello después plano YAML: esta guía describe un nuevo toodeploy variante (sava: 1.1.0) de servicio en clúster existente de hello (sava_cluster).

  ```YAML
  name: sava:1.1.0      # blueprint name
  clusters:
    sava_cluster:       # cluster tooupdate
      services:
        -
          breed:
            name: sava:1.1.0    # service variant name
            deployable: magneticio/sava:1.1.0    
            ports:
              webport: 8080/http # cluster endpoint tooupdate
  ```
  
3. Haga clic en **Guardar**. plano técnico Hola se almacena y aparece en hello **planos** página.

4. Menú de acción de hello abierto en el plano de Hola sava: 1.1 y haga clic en **Merge para**.

  ![Interfaz de usuario de Vamp: planos](./media/container-service-dcos-vamp-canary-release/20_sava110_mergeto.png)

5. Seleccione hello **sava** implementación y haga clic en **mezcla**.

  ![Interfaz de usuario de vamp - combinar plano toodeployment](./media/container-service-dcos-vamp-canary-release/21_sava110_merge.png)

Vamp implementa Hola nueva sava: 1.1.0 variante de un servicio se describe en el plano de hello junto con sava: 1.0.0 Hola **sava_cluster** de hello ejecutando la implementación. 

![Interfaz de usuario de Vamp: implementación de sava actualizada](./media/container-service-dcos-vamp-canary-release/22_sava_cluster.png)

Hola **sava/sava_cluster/webport** (punto de conexión de clúster de hello) de la puerta de enlace también se actualiza, agregar una ruta toohello recién implementado sava: 1.1.0. En este momento, no el tráfico se enruta a continuación (hello **peso** se establece too0%).

![Interfaz de usuario de Vamp: puerta de enlace de clúster](./media/container-service-dcos-vamp-canary-release/23_sava_cluster_webport.png)

### <a name="canary-release"></a>Lanzamiento controlado

Con ambas versiones de sava implementado en hello mismo clúster, ajuste la distribución de Hola de tráfico entre ellas moviendo hello **peso** control deslizante.

1. Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) siguiente demasiado**peso**.

2. Establecer Hola peso distribución too50%/50% y haga clic en **guardar**.

  ![Interfaz de usuario de Vamp: control deslizante de peso de puerta de enlace](./media/container-service-dcos-vamp-canary-release/24_sava_cluster_webport_weight.png)

3. Retroceda tooyour explorador y actualizar página de hello sava varias veces. aplicación Hola sava cambia entre una página sava: 1.0 y una página sava: 1.1.

  ![Alternar entre los servicios sava1.0 y sava1.1](./media/container-service-dcos-vamp-canary-release/25_sava_100_101.png)


  > [!NOTE]
  > Este alternancia de página Hola funciona mejor con Hola "Incógnito" o "Anónimo" modo de su explorador debido a Hola almacenamiento en caché de activos estáticos.
  >

### <a name="filter-traffic"></a>Filtrado del tráfico

Suponga que, después de la implementación, detecta una incompatibilidad en sava:1.1.0 que causa problemas de visualización en los exploradores Firefox. Puede establecer Vamp toofilter el tráfico entrante y dirigir que toohello conocida estable sava: 1.0.0 hacer copia de todos los usuarios de Firefox. Este filtro al instante resuelve Hola interrupciones para los usuarios de Firefox, mientras los demás continúa tooenjoy ventajas de Hola de hello había mejorado sava: 1.1.0.

Vamp utiliza **condiciones** toofilter el tráfico entre las rutas en una puerta de enlace. El tráfico en primer lugar se filtra y dirige correspondiente toohello condiciones aplicadas tooeach ruta. Todo el tráfico restante se distribuye según la configuración de peso de puerta de enlace de toohello.

Puede crear una condición toofilter todos los usuarios de Firefox y dirigirlas toohello sava: 1.0.0 anterior:

1. En hello sava/sava_cluster/webport **puertas de enlace** página, haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) tooadd una **condición** toohello ruta sava/sava_cluster/sava:1.0.0/webport. 

2. Escriba la condición de hello **usuario-agente == Firefox** y haga clic en ![Vamp una interfaz de usuario: Guardar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png).

  Vamp agrega la condición de hello con la seguridad predeterminada de 0%. toostart filtrando el tráfico, deberá intensidad de condición de tooadjust Hola.

3. Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) toochange hello **intensidad** aplica toohello condición.
 
4. Conjunto hello **intensidad** too100% y haga clic en ![Vamp una interfaz de usuario: Guardar](./media/container-service-dcos-vamp-canary-release/vamp_ui_save.png) toosave.

  Vamp ahora envía todo el tráfico coincidente Hola condición (todos los usuarios de Firefox) toosava:1.0.0.

  ![Vamp la interfaz de usuario: aplicar la condición toogateway](./media/container-service-dcos-vamp-canary-release/26_apply_condition.png)

5. Por último, ajustar toosend de peso de puerta de enlace de hello todas las restantes tráfico (todos los usuarios de Firefox no) toohello nueva sava: 1.1.0. Haga clic en ![Vamp una interfaz de usuario: editar](./media/container-service-dcos-vamp-canary-release/vamp_ui_edit.png) siguiente demasiado**peso** y establecer la distribución de pesos de Hola por lo que es de 100% toohello dirigido ruta sava/sava_cluster/sava:1.1.0/webport.

  Todo el tráfico que no se filtran por la condición de hello ahora es dirigido toohello nueva sava: 1.1.0.

6. filtro de hello toosee en acción, abra dos distintos exploradores (uno Firefox y un otro explorador) y obtenga acceso a hello sava de ambos. Todas las solicitudes de Firefox se envían toosava:1.0.0, mientras que todos los demás exploradores son toosava:1.1.0 dirigido.

  ![Interfaz de usuario de Vamp: filtrar el tráfico](./media/container-service-dcos-vamp-canary-release/27_filter_traffic.png)

## <a name="summing-up"></a>Resumen

Este artículo es una tooVamp introducción rápida en un clúster de DC/OS. Para empezar, copiadas Vamp hasta y ejecuta en el servicio de contenedor de Azure DC/OS clúster, implementar un servicio con un plano Vamp y accedió a él en el punto de conexión de hello expone (puerta de enlace).

Hemos tratado también algunas características eficaces de Vamp: combinar una toohello variant de servicio nueva ejecución de implementación y presentación de forma incremental y, a continuación, filtrar tráfico tooresolve una incompatibilidad conocida.


## <a name="next-steps"></a>Pasos siguientes

* Obtenga información acerca de cómo administrar las acciones de Vamp a través de hello [Vamp API de REST](http://vamp.io/documentation/api/api-reference/).

* Cree scripts de automatización de Vamp en Node.js y ejecútelos como [flujos de trabajo de Vamp](http://vamp.io/documentation/tutorials/create-a-workflow/).

* Consulte más [tutoriales sobre VAMP](http://vamp.io/documentation/tutorials/overview/).

