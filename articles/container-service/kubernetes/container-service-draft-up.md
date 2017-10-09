---
title: aaaUse borrador con registro de contenedor de Azure y el servicio de contenedor de Azure | Documentos de Microsoft
description: "Crear un clúster de ACS Kubernetes y un registro de contenedor de Azure toocreate su primera aplicación en Azure con Borrador."
services: container-service
documentationcenter: 
author: squillace
manager: gamonroy
editor: 
tags: draft, helm, acs, azure-container-service
keywords: Docker, contenedores, microservicios, Kubernetes, Draft, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: rasquill
ms.custom: mvc
ms.openlocfilehash: f5e21cda01e5e8452bf86a5c8fa458904d89f451
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-draft-with-azure-container-service-and-azure-container-registry-toobuild-and-deploy-an-application-tookubernetes"></a>Usar borrador con toobuild de servicio de contenedor de Azure y el registro de contenedor de Azure e implementar una aplicación tooKubernetes

[Borrador](https://aka.ms/draft) es una nueva herramienta de código abierto que hace más fácil toodevelop aplicaciones contenedor e implementarlas tooKubernetes clústeres sin saber mucho sobre Docker y Kubernetes--o incluso su instalación. Con herramientas como borrador permite a su enfoque de los equipos compilación aplicación hello con Kubernetes, no se presta tanta tooinfrastructure atención.

Puede usar Draft con cualquier registro de imágenes de Docker y cualquier clúster de Kubernetes, incluidos los locales. Este tutorial muestra cómo toouse ACS con toocreate Kubernetes, ACR y DNS de Azure, un desarrollador de CI/CD en vivo de canalización con Borrador.


## <a name="create-an-azure-container-registry"></a>Creación de una instancia de Azure Container Registry
Le resultará muy fácil [crear un nuevo registro de contenedor de Azure](../../container-registry/container-registry-get-started-azure-cli.md), pero Hola pasos son los siguientes:

1. Crear un toomanage de grupo de recursos de Azure en el clúster de Kubernetes de hello y del registro ACR en ACS.
      ```azurecli
      az group create --name draft --location eastus
      ```

2. Cree un registro de imagen ACR con [az acr create](/cli/azure/acr#create)
      ```azurecli
      az acr create -g draft -n draftacs --sku Basic --admin-enabled true -l eastus
      ```


## <a name="create-an-azure-container-service-with-kubernetes"></a>Creación de Azure Container Service mediante Kubernetes

Ahora está listo toouse [az acs crear](/cli/azure/acs#create) clúster toocreate un ACS utilizando Kubernetes como hello `--orchestrator-type` valor.
```azurecli
az acs create --resource-group draft --name draft-kube-acs --dns-prefix draft-cluster --orchestrator-type kubernetes
```

> [!NOTE]
> Porque Kubernetes no tiene tipos de orchestrator de hello predeterminado, asegúrese de usar hello `--orchestrator-type kubernetes` cambiar.

salida de Hello cuando se realiza correctamente es similar a continuación toohello.

```json
waiting for AAD role toopropagate.done
{
  "id": "/subscriptions/<guid>/resourceGroups/draft/providers/Microsoft.Resources/deployments/azurecli14904.93snip09",
  "name": "azurecli1496227204.9323909",
  "properties": {
    "correlationId": "<guid>",
    "debugSetting": null,
    "dependencies": [],
    "mode": "Incremental",
    "outputs": null,
    "parameters": {
      "clientSecret": {
        "type": "SecureString"
      }
    },
    "parametersLink": null,
    "providers": [
      {
        "id": null,
        "namespace": "Microsoft.ContainerService",
        "registrationState": null,
        "resourceTypes": [
          {
            "aliases": null,
            "apiVersions": null,
            "locations": [
              "westus"
            ],
            "properties": null,
            "resourceType": "containerServices"
          }
        ]
      }
    ],
    "provisioningState": "Succeeded",
    "template": null,
    "templateLink": null,
    "timestamp": "2017-05-31T10:46:29.434095+00:00"
  },
  "resourceGroup": "draft"
}
```

Ahora que tiene un clúster, puede importar las credenciales de hello mediante hello [az kubernetes get-credenciales de acs](/cli/azure/acs/kubernetes#get-credentials) comando. Ahora tiene un archivo de configuración local para el clúster, que es qué timón y un borrador necesitan tooget su trabajo.

## <a name="install-and-configure-draft"></a>Instalación y configuración de Draft
instrucciones de instalación de Hola de borrador que se encuentran en hello [repositorio de borrador](https://github.com/Azure/draft/blob/master/docs/install.md). Son relativamente simples, pero requiere cierta configuración, ya que depende de [timón](https://aka.ms/helm) toocreate e implementar un gráfico de timón en clúster de Kubernetes Hola.

1. [Descarga e instalación de Helm](https://aka.ms/helm#install).
2. Utilice toosearch timón para e instale `stable/traefik`y entrada controlador tooenable las solicitudes para las compilaciones de entrada.
    ```bash
    $ helm search traefik
    NAME            VERSION DESCRIPTION
    stable/traefik  1.3.0   A Traefik based Kubernetes ingress controller w...

    $ helm install stable/traefik --name ingress
    ```
    Ahora se establece una inspección en hello `ingress` controlador toocapture Hola IP valor externo cuando se implementa. Esta dirección IP será Hola uno [asignado tooyour implementación dominio](#wire-up-deployment-domain) en la sección siguiente Hola.

    ```bash
    kubectl get svc -w
    NAME                          CLUSTER-IP     EXTERNAL-IP     PORT(S)                      AGE
    ingress-traefik               10.0.248.104   13.64.108.240   80:31046/TCP,443:32556/TCP   1h
    kubernetes                    10.0.0.1       <none>          443/TCP                      7h
    ```

    En este caso, Hola direcciones IP externas de dominio de la implementación de hello es `13.64.108.240`. Ahora puede asignar la IP de toothat de dominio.

## <a name="wire-up-deployment-domain"></a>Conexión del dominio de implementación

Draft crea una versión para cada gráfico de Helm que crea: cada aplicación en la que esté trabajando. Cada uno obtiene un nombre generado que se usa por borrador como un _subdominio_ encima de la raíz de hello _dominio implementación_ que usted controla. (En este ejemplo, utilizamos `squillace.io` como dominio de implementación de hello.) tooenable este comportamiento subdominio, debe crear un registro a para `'*'` las entradas de DNS para el dominio de la implementación, para que cada uno de ellos genere subdominio es enrutado toohello Kubernetes controlador de entrada del clúster.

Su propio proveedor de dominio tiene sus propios servidores DNS de manera tooassign; demasiado[delegar su tooAzure de servidores de nombres de dominio DNS](../../dns/dns-delegate-domain-azure-dns.md), tomar Hola pasos:

1. Cree un grupo de recursos para su zona.
    ```azurecli
    az group create --name squillace.io --location eastus
    {
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io",
      "location": "eastus",
      "managedBy": null,
      "name": "zones",
      "properties": {
        "provisioningState": "Succeeded"
      },
      "tags": null
    }
    ```

2. Cree una zona DNS para su dominio.
Hola de uso [crear zona de dns de red az](/cli/azure/network/dns/zone#create) comando tooobtain Hola servidores de nombres toodelegate DNS controlar tooAzure DNS para su dominio.
    ```azurecli
    az network dns zone create --resource-group squillace.io --name squillace.io
    {
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/zones/providers/Microsoft.Network/dnszones/squillace.io",
      "location": "global",
      "maxNumberOfRecordSets": 5000,
      "name": "squillace.io",
      "nameServers": [
        "ns1-09.azure-dns.com.",
        "ns2-09.azure-dns.net.",
        "ns3-09.azure-dns.org.",
        "ns4-09.azure-dns.info."
      ],
      "numberOfRecordSets": 2,
      "resourceGroup": "squillace.io",
      "tags": {},
      "type": "Microsoft.Network/dnszones"
    }
    ```
3. Agregar servidores DNS de hello que tendrá toohello los proveedores de dominio para el dominio de la implementación, lo que permite toorepoint DNS de Azure toouse su dominio como desee.
4. Crear una entrada de conjunto de registros A para su toohello de asignación de dominio de implementación `ingress` IP del paso 2 de la sección anterior de Hola.
    ```azurecli
    az network dns record-set a add-record --ipv4-address 13.64.108.240 --record-set-name '*' -g squillace.io -z squillace.io
    ```
salida de Hello es similar:
    ```json
    {
      "arecords": [
        {
          "ipv4Address": "13.64.108.240"
        }
      ],
      "etag": "<guid>",
      "id": "/subscriptions/<guid>/resourceGroups/squillace.io/providers/Microsoft.Network/dnszones/squillace.io/A/*",
      "metadata": null,
      "name": "*",
      "resourceGroup": "squillace.io",
      "ttl": 3600,
      "type": "Microsoft.Network/dnszones/A"
    }
    ```

5. Configurar el registro de borrador toouse y crear subdominios para cada gráfico timón crea. tooconfigure borrador, se necesita:
  - el nombre de Azure Container Registry (en este ejemplo, `draft`)
  - la clave del registro, o la contraseña, de `az acr credential show -n <registry name> --output tsv --query "passwords[0].value"`.
  - dominio de implementación de Hello raíz que ha configurado la dirección IP externa de toomap toohello Kubernetes entrada (en este caso, `squillace.io`)

  Llame a `draft init` y proceso de configuración de hello solicita valores de hello indicados anteriormente. proceso de Hello parece algo siguiente Hola Hola primera vez que se ejecuta.
 ```bash
    $ draft init
    Creating pack ruby...
    Creating pack node...
    Creating pack gradle...
    Creating pack maven...
    Creating pack php...
    Creating pack python...
    Creating pack dotnetcore...
    Creating pack golang...
    $DRAFT_HOME has been configured at /Users/ralphsquillace/.draft.

    In order tooinstall Draft, we need a bit more information...

    1. Enter your Docker registry URL (e.g. docker.io, quay.io, myregistry.azurecr.io): draft.azurecr.io
    2. Enter your username: draft
    3. Enter your password:
    4. Enter your org where Draft will push images [draft]: draft
    5. Enter your top-level domain for ingress (e.g. draft.example.com): squillace.io
    Draft has been installed into your Kubernetes Cluster.
    Happy Sailing!
    ```

Ahora está listo toodeploy una aplicación.


## <a name="build-and-deploy-an-application"></a>Compilación e implementación de una aplicación

En el repositorio de borrador de hello son [seis de las aplicaciones de ejemplo simple](https://github.com/Azure/draft/tree/master/examples). Clonar el repositorio de Hola y vamos a usar hello [ejemplo de Python](https://github.com/Azure/draft/tree/master/examples/python). Cambiar en el directorio de ejemplos/Python hello y escriba `draft create` aplicación de hello toobuild. Debería ser similar el siguiente ejemplo de Hola.
```bash
$ draft create
--> Python app detected
--> Ready toosail
```

salida de Hello incluye un archivo Dockerfile y un gráfico de timón. toobuild e implementar, simplemente escriba `draft up`. salida de Hello es extensa, pero se inicia como el siguiente ejemplo de Hola.
```bash
$ draft up
--> Building Dockerfile
Step 1 : FROM python:onbuild
onbuild: Pulling from library/python
10a267c67f42: Pulling fs layer
fb5937da9414: Pulling fs layer
9021b2326a1e: Pulling fs layer
dbed9b09434e: Pulling fs layer
ea8a37f15161: Pulling fs layer
<snip>
```

y cuando finaliza correctamente con algo similar toohello siguiente ejemplo.
```bash
ab68189731eb: Pushed
53c0ab0341bee12d01be3d3c192fbd63562af7f1: digest: sha256:bb0450ec37acf67ed461c1512ef21f58a500ff9326ce3ec623ce1e4427df9765 size: 2841
--> Deploying tooKubernetes
--> Status: DEPLOYED
--> Notes:

  http://gangly-bronco.squillace.io tooaccess your application

Watching local files for changes...
```

Lo que es el nombre de su gráfico, ahora puede `curl http://gangly-bronco.squillace.io` tooreceive respuesta de hello, `Hello World!`.

## <a name="next-steps"></a>Pasos siguientes

Ahora que tiene un clúster de ACS Kubernetes, puede investigar mediante [registro de contenedor de Azure](../../container-registry/container-registry-intro.md) toocreate más y diferentes implementaciones de este escenario. Por ejemplo, puede crear un conjunto de registros DNS de dominios draft._basedomain.toplevel_ que controle aspectos de un subdominio más profundo para implementaciones de ACS específicas.






