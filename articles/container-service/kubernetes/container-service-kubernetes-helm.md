---
title: "contenedores de aaaDeploy con timón en Azure Kubernetes | Documentos de Microsoft"
description: "Utilizar contenedores de toodeploy de herramienta de hello timón empaquetado en un clúster de Kubernetes en el servicio de contenedor de Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a>Utilizar contenedores de toodeploy de timón en un clúster de Kubernetes 

[Timón](https://github.com/kubernetes/helm/) es una herramienta de empaquetado de código abierto que le ayuda a instalar y administrar el ciclo de vida de Hola de Kubernetes aplicaciones. Administradores de paquetes tooLinux similar como Apt get y Yum, timón es toomanage usado Kubernetes gráficos, que son paquetes de recursos de Kubernetes preconfigurados. Este artículo muestra cómo implementa toowork con timón en un clúster de Kubernetes en el servicio de contenedor de Azure.

Helm tiene dos componentes: 
* Hola **timón CLI** es un cliente que se ejecuta en el equipo local o en la nube de Hola  

* **Caña** es un servidor que se ejecuta en hello Kubernetes clúster y administra Hola del ciclo de vida de las aplicaciones Kubernetes 
 
## <a name="prerequisites"></a>Requisitos previos

* [Creación de un clúster de Kubernetes](container-service-kubernetes-walkthrough.md) en Azure Container Service

* [Instalación y configuración `kubectl`](../container-service-connect.md) en un equipo local

* [Instalación de Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) en un equipo local

## <a name="helm-basics"></a>Aspectos básicos de Helm 

tooview información sobre hello Kubernetes clúster que está instalando caña y la implementación de las aplicaciones, escriba el siguiente comando de hello:

```bash
kubectl cluster-info 
```
![kubectl cluster-info](./media/container-service-kubernetes-helm/clusterinfo.png)
 
Después de haber instalado timón, instalar caña en el clúster Kubernetes escribiendo el siguiente comando de hello:

```bash
helm init --upgrade
```
Cuando se complete correctamente, verá resultados similares a Hola siguientes:

![Instalación de Tiller](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
tooview de comandos de todos los Hola timón gráficos disponibles en el repositorio de hello, Hola de tipo siguientes:

```bash 
helm search 
```

Verá resultados similares a Hola siguientes:

![Búsqueda de Helm](./media/container-service-kubernetes-helm/helm-search.png)
 
tooupdate Hola gráficos tooget Hola versiones más recientes, escriba:

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a>Implementación de un gráfico de controlador de entrada de Nginx 
 
toodeploy un gráfico de controlador de entrada de Nginx, escriba un comando único:

```bash
helm install stable/nginx-ingress 
```
![Implementación del controlador de entrada](./media/container-service-kubernetes-helm/nginx-ingress.png)

Si escribe `kubectl get svc` tooview todos los servicios que se ejecutan en el clúster de hello, verá que se asigna una dirección IP toohello controlador de entrada. (Mientras asignación Hola está en curso, vea `<pending>`. Toma un par de minutos toocomplete). 

Una vez se asigna la dirección IP de hello, navegue toohello valo Hola externo IP dirección toosee hello Nginx back-end ejecuta. 
 
![Dirección IP de entrada](./media/container-service-kubernetes-helm/ingress-ip-address.png)


toosee una lista de gráficos instalado en el clúster, tipo:

```bash
helm list 
```

Se puede abreviar como comando hello demasiado`helm ls`.
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a>Implementación de un cliente y un gráfico de MariaDB

Implementar ahora un gráfico de MariaDB y una base de datos de MariaDB cliente tooconnect toohello.

gráfico de toodeploy hello MariaDB, Hola de tipo siguiente comando:

```bash
helm install --name v1 stable/mariadb
```

donde `--name` es una etiqueta que se usa para las versiones.

> [!TIP]
> Si se produce un error en la implementación de hello, ejecute `helm repo update` y vuelva a intentarlo.
>
 
 
tooview todos los gráficos de hello implementan en el clúster, tipo:

```bash 
helm list
```
 
tooview todas las implementaciones que se ejecutan en el clúster, escriba:

```bash
kubectl get deployments 
``` 
 
 
Por último, toorun un cliente de hello pod tooaccess, escriba:

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
tooconnect toohello cliente, Hola de tipo siguiente comando, reemplazando `v1-mariadb` con nombre hello de la implementación:

```bash
sudo mysql –h v1-mariadb
```
 
 
Ahora puede usar el estándares SQL comandos toocreate las bases de datos, tablas, etcetera. Por ejemplo, `Create DATABASE testdb1;` crea una base de datos vacía. 
 
 
 
## <a name="next-steps"></a>Pasos siguientes

* Para obtener más información acerca de cómo administrar Kubernetes gráficos, vea hello [timón documentación](https://github.com/kubernetes/helm/blob/master/docs/index.md). 

