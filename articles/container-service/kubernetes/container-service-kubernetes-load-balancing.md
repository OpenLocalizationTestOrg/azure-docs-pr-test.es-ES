---
title: aaaLoad equilibrar Kubernetes contenedores en Azure | Documentos de Microsoft
description: "Conéctese externamente y equilibre la carga entre varios contenedores en un clúster de Kubernetes en Azure Container Service."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenedores, microservicios, Kubernetes, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8073c8d3a015a53a532c326749571cb2582e1bac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-containers-in-a-kubernetes-cluster-in-azure-container-service"></a>Equilibrio de carga de contenedores en un clúster de Kubernetes en Azure Container Service 
En este artículo se detalla el equilibrio de carga en un clúster de Kubernetes en Azure Container Service. Equilibrio de carga proporciona una dirección IP accesible desde el exterior para el servicio de Hola y distribuye el tráfico de red entre pod de Hola que se ejecuta en máquinas virtuales de agente.

Puede configurar un toouse de servicio de Kubernetes [equilibrador de carga Azure](../../load-balancer/load-balancer-overview.md) toomanage tráfico de red (TCP) externo. Con la configuración adicional, son posibles el equilibrio de carga y el enrutamiento del tráfico HTTP o HTTPS, así como escenarios más avanzados.

## <a name="prerequisites"></a>Requisitos previos
* [Implementar un clúster de Kubernetes](container-service-kubernetes-walkthrough.md) en Azure Container Service
* [Conectar el cliente](../container-service-connect.md) tooyour clúster

## <a name="azure-load-balancer"></a>Azure Load Balancer

De forma predeterminada, un clúster de Kubernetes implementado en el servicio de contenedor de Azure incluye un equilibrador de carga de Azure orientado a Internet para el agente de hello las máquinas virtuales. (Un recurso de equilibrador de carga independiente está configurado para master Hola máquinas virtuales). Azure Load Balancer es un equilibrador de carga de nivel 4. Actualmente, equilibrador de carga de hello solo admite el tráfico TCP en Kubernetes.

Al crear un servicio de Kubernetes, puede configurar automáticamente hello Azure tooallow acceso toohello servicio del equilibrador de. equilibrador de carga de hello tooconfigure, conjunto Hola servicio `type` demasiado`LoadBalancer`. equilibrador de carga de Hola crea una regla toomap una dirección IP pública y número de puerto de entrada servicio tráfico toohello las direcciones IP privadas y los números de puerto de pod hello en el agente de VM (y viceversa para el tráfico de respuesta). 

 Éstos son algunos ejemplos de dos que muestra cómo tooset Hola servicio Kubernetes `type` demasiado`LoadBalancer`. (Después de tratar de obtener ejemplos de hello, eliminar las implementaciones de hello aunque ya no los necesite.)

### <a name="example-use-hello-kubectl-expose-command"></a>Ejemplo: Hola de uso `kubectl expose` comando 
Hola [Kubernetes tutorial](container-service-kubernetes-walkthrough.md) incluye un ejemplo de cómo un servicio con hello tooexpose `kubectl expose` comando y su `--type=LoadBalancer` marca. Estos son los pasos de hello:

1. Inicie una nueva implementación de contenedor. Hola por ejemplo, el siguiente comando inicia una nueva implementación llama `mynginx`. implementación de Hello consta de tres contenedores basados en imagen de Docker de hello para el servidor de web Nginx Hola.

    ```console
    kubectl run mynginx --replicas=3 --image nginx
    ```
2. Compruebe que se están ejecutando los contenedores de Hola. Por ejemplo, si realiza una consulta para los contenedores de hello con `kubectl get pods`, ve resultados similares toohello siguiente:

    ![Obtención de contenedores de Nginx](./media/container-service-kubernetes-load-balancing/nginx-get-pods.png)

3. tooconfigure Hola carga equilibrador tooaccept tráfico externo toohello implementación, ejecute `kubectl expose` con `--type=LoadBalancer`. Hello siguiente comando expone hello Nginx servidor en el puerto 80:

    ```console
    kubectl expose deployments mynginx --port=80 --type=LoadBalancer
    ```

4. Tipo `kubectl get svc` toosee estado de hello de servicios de hello en clúster de Hola. Mientras el equilibrador de carga de hello configura reglas de hello, Hola `EXTERNAL-IP` de hello servicio aparece como `<pending>`. Después de unos minutos, se configura la dirección IP externa de hello: 

    ![Configurar Azure Load Balancer](./media/container-service-kubernetes-load-balancing/nginx-external-ip.png)

5. Compruebe que puede tener acceso a servicio de hello en la dirección IP externa de Hola. Por ejemplo, abra una dirección IP de toohello de explorador web que se muestra. Explorador de Hello muestra servidor web hello Nginx que ejecute en uno de los contenedores de Hola. O bien, hello ejecución `curl` o `wget` comando. Por ejemplo:

    ```
    curl 13.82.93.130
    ```

    Debería mostrarse una salida similar a esta:

    ![Acceder a Nginx con curl](./media/container-service-kubernetes-load-balancing/curl-output.png)

6. configuración de hello toosee hello Azure del equilibrador de carga, vaya toohello [portal de Azure](https://portal.azure.com).

7. Busque el grupo de recursos de hello para el clúster de servicio de contenedor y seleccione el equilibrador de carga de hello para el agente de hello las máquinas virtuales. Su nombre debe ser Hola igual que el servicio de contenedor de Hola. (No elija equilibrador de carga de Hola de nodos maestros hello, Hola uno cuyo nombre incluya **lb master**.) 

    ![Equilibrador de carga en el grupo de recursos](./media/container-service-kubernetes-load-balancing/container-resource-group-portal.png)

8. toosee Hola detalles de configuración de equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga** y el nombre de Hola de regla de Hola que configuró.

    ![Reglas de equilibrador de carga](./media/container-service-kubernetes-load-balancing/load-balancing-rules.png) 

### <a name="example-specify-type-loadbalancer-in-hello-service-configuration-file"></a>Ejemplo: Especificar `type: LoadBalancer` en el archivo de configuración de servicio de Hola

Si se implementa una aplicación de contenedor de Kubernetes desde un YAML o JSON [archivo de configuración de servicio](https://kubernetes.io/docs/user-guide/services/operations/#service-configuration-file), especifique un equilibrador de carga externo mediante la adición de hello siguiendo la especificación del servicio toohello línea:

```YAML
 "type": "LoadBalancer"
``` 



pasos siguientes Hello utilizan hello Kubernetes [ejemplo de libro de visitas](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook). Este ejemplo es una aplicación web de varios niveles basada en imágenes de Redis y Docker PHP. Puede especificar en el archivo de configuración de servicio de hello que ese servidor PHP de front-end de hello usa el equilibrador de carga de Azure Hola.

1. Descargar archivo hello `guestbook-all-in-one.yaml` de [GitHub](https://github.com/kubernetes/kubernetes/tree/master/examples/guestbook/all-in-one). 
2. Busque hello `spec` para hello `frontend` servicio.
3. Quite el comentario de línea de hello `type: LoadBalancer`.

    ![Equilibrador de carga en configuración del servicio](./media/container-service-kubernetes-load-balancing/guestbook-frontend-loadbalance.png)

4. Guardar archivo hello e implementar la aplicación hello ejecutando el siguiente comando de hello:

    ```
    kubectl create -f guestbook-all-in-one.yaml
    ```

5. Tipo `kubectl get svc` toosee estado de hello de servicios de hello en clúster de Hola. Mientras el equilibrador de carga de hello configura reglas de hello, Hola `EXTERNAL-IP` de hello `frontend` servicio aparece como `<pending>`. Después de unos minutos, se configura la dirección IP externa de hello: 

    ![Configurar Azure Load Balancer](./media/container-service-kubernetes-load-balancing/guestbook-external-ip.png)

6. Compruebe que puede tener acceso a servicio de hello en la dirección IP externa de Hola. Por ejemplo, puede abrir una dirección IP externa de toohello de explorador de web del servicio de Hola.

    ![Acceder al libro de visitas externamente](./media/container-service-kubernetes-load-balancing/guestbook-web.png)

    Puede agregar entradas del libro de visitas.

7. configuración de hello toosee hello Azure del equilibrador de carga, buscar recursos de equilibrador de carga de Hola para clúster Hola Hola [portal de Azure](https://portal.azure.com). Vea Hola los pasos de ejemplo de Hola anterior.

### <a name="considerations"></a>Consideraciones

* Creación de regla de equilibrador de carga de Hola se realiza de forma asincrónica y la información sobre equilibrador de hello aprovisionado se publica en el servicio de hello `status.loadBalancer` campo.
* Todos los servicios se asignan automáticamente su propia dirección IP virtual en el equilibrador de carga de Hola.
* Si lo desea equilibrador de carga de hello tooreach mediante un nombre DNS, trabajar con su toocreate de proveedor de servicio de dominio un nombre DNS para la dirección IP de la regla de Hola.

## <a name="http-or-https-traffic"></a>Tráfico HTTP o HTTPS

saldo de tooload HTTP o HTTPS tráfico toocontainer aplicaciones web y administrar los certificados de seguridad de la capa de transporte (TLS), puede usar hello Kubernetes [entrada](https://kubernetes.io/docs/user-guide/ingress/) recursos. Una entrada es una colección de reglas que permiten las conexiones entrantes en servicios de cluster Server de tooreach Hola. Para una toowork de recursos de entrada, hello Kubernetes deben tener un [controlador de entrada](https://kubernetes.io/docs/user-guide/ingress/#ingress-controllers) ejecutando.

Azure Container Service no implementa un controlador Ingress de Kubernetes automáticamente. Hay varias implementaciones de controlador disponibles. Actualmente, Hola [controlador de entrada de Nginx](https://github.com/kubernetes/ingress/tree/master/examples/deployment/nginx) se recomienda tooconfigure reglas de entrada y equilibrio de carga de tráfico HTTP y HTTPS. 

Para obtener más información, vea hello [documentación del controlador de entrada de Nginx](https://github.com/kubernetes/ingress/tree/master/controllers/nginx/README.md).

> [!IMPORTANT]
> Al utilizar Hola controlador Nginx entrada en servicio de contenedor de Azure, debe exponer como un servicio con la implementación de controladores de hello `type: LoadBalancer`. Esto configura el controlador toohello de tráfico de tooroute de equilibrador de hello carga de Azure. Para obtener más información, vea la sección anterior de Hola.


## <a name="next-steps"></a>Pasos siguientes

* Vea hello [Kubernetes LoadBalancer documentación](https://kubernetes.io/docs/user-guide/load-balancer/)
* Obtener más información sobre los controladores [Ingress de Kubernetes](https://kubernetes.io/docs/user-guide/ingress/)
* Consultar [ejemplos de Kubernetes](https://github.com/kubernetes/kubernetes/tree/master/examples)

