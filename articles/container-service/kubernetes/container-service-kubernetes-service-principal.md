---
title: "entidad de seguridad de aaaService de clúster de Azure Kubernetes | Documentos de Microsoft"
description: "Cree y administre una entidad de servicio de Azure Active Directory para un clúster de Kubernetes en Azure Container Service"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/08/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 7a01624c5ac3fa717dbcbd570e05ceb4d917c53a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-ad-service-principal-for-a-kubernetes-cluster-in-container-service"></a>Configuración de una entidad de servicio de Azure AD para un clúster de Kubernetes en Container Service


En el servicio de contenedor de Azure, se requiere un clúster de Kubernetes una [entidad de servicio de Azure Active Directory](../../active-directory/develop/active-directory-application-objects.md) toointeract con las API de Azure. Hello entidad de servicio es necesario toodynamically administran recursos como [rutas definidas por el usuario](../../virtual-network/virtual-networks-udr-overview.md) hello y [equilibrador de carga de Azure de capa 4](../../load-balancer/load-balancer-overview.md). 


Este artículo muestra diferentes opciones tooset configurar un servicio principal para el clúster de Kubernetes. Por ejemplo, si instalado y configurado hello [CLI de Azure 2.0](/cli/azure/install-az-cli2), puede ejecutar hello [ `az acs create` ](/cli/azure/acs#create) comando toocreate hello Kubernetes hello y clúster de entidad de servicio en hello mismo tiempo.


## <a name="requirements-for-hello-service-principal"></a>Requisitos para la entidad de servicio de Hola

Puede usar a una entidad de servicio de Azure AD existente que cumpla Hola según los requisitos, o cree uno nuevo.

* **Ámbito**: grupo de recursos de hello en la suscripción de hello usa clúster de toodeploy hello Kubernetes o (menos de manera restrictiva) suscripción Hola clúster de hello toodeploy.

* **Rol**: **colaborador**

* **Secreto de cliente**: debe ser una contraseña. Actualmente, no se puede usar a una entidad de servicio configurado para la autenticación de certificados.

> [!IMPORTANT] 
> toocreate una entidad de servicio, debe tener permisos tooregister una aplicación con el inquilino de Azure AD y rol de tooassign Hola aplicación tooa en su suscripción. toosee si tiene los permisos necesario de hello, [comprobar Hola Portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md#required-permissions). 
>

## <a name="option-1-create-a-service-principal-in-azure-ad"></a>Opción 1: Creación de una entidad de servicio en Azure AD

Si desea toocreate una entidad de seguridad de servicio de Azure AD antes de implementar el clúster Kubernetes, Azure proporciona varios métodos. 

Hola después de comandos de ejemplo muestra cómo toodo esto con hello [CLI de Azure 2.0](../../azure-resource-manager/resource-group-authenticate-service-principal-cli.md). O bien puede crear una entidad de seguridad de servicio mediante [Azure PowerShell](../../azure-resource-manager/resource-group-authenticate-service-principal.md), hello [portal](../../azure-resource-manager/resource-group-create-service-principal-portal.md), u otros métodos.

```azurecli
az login

az account set --subscription "mySubscriptionID"

az group create -n "myResourceGroupName" -l "westus"

az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/mySubscriptionID/resourceGroups/myResourceGroupName"
```

Salida es similar toohello siguiente (mostrado aquí redactado):

![Creación de una entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-creds.png)

Resalta son hello **Id. de cliente** (`appId`) hello y **secreto de cliente** (`password`) que se usan como parámetros de entidad de seguridad de servicio para la implementación del clúster.


### <a name="specify-service-principal-when-creating-hello-kubernetes-cluster"></a>Especifique la entidad de servicio al crear el clúster de hello Kubernetes

Proporcionar hello **Id. de cliente** (también llamado hello `appId`, para el Id. de aplicación) y **secreto de cliente** (`password`) de una entidad como parámetros al crear Hola de servicio existente Clúster de Kubernetes. Asegúrese de entidad de servicio de hello cumple los requisitos de hello en hello partir de este artículo.

Puede especificar estos parámetros al implementar el clúster de hello Kubernetes con hello [interfaz de línea de comandos (CLI) 2.0 de Azure](container-service-kubernetes-walkthrough.md), [portal de Azure](../dcos-swarm/container-service-deployment.md), u otros métodos.

>[!TIP] 
>Al especificar hello **Id. de cliente**, estar seguro de hello toouse `appId`, no Hola `ObjectId`, de entidad de servicio de Hola.
>

Hello en el ejemplo siguiente se muestra toopass unidireccional Hola parámetros con hello 2.0 de CLI de Azure. Este ejemplo utiliza hello [plantilla de inicio rápido de Kubernetes](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acs-kubernetes).

1. [Descargar](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.parameters.json) archivo de parámetros de plantilla de hello `azuredeploy.parameters.json` desde GitHub.

2. servicio de hello toospecify principal, especifique los valores de `servicePrincipalClientId` y `servicePrincipalClientSecret` en el archivo hello. (También necesita tooprovide sus propios valores para `dnsNamePrefix` y `sshRSAPublicKey`. Hola este último es clúster Hola de hello SSH tooaccess de clave pública). Guarde el archivo hello.

    ![Pasar los parámetros de la entidad de servicio](./media/container-service-kubernetes-service-principal/service-principal-params.png)

3. Hola ejecución siguiente comando, usando `--parameters` tooset Hola ruta toohello azuredeploy.parameters.json al archivo. Este comando implementa el clúster de hello en un grupo de recursos que se haya creado llamado `myResourceGroup` en la región del oeste de Estados Unidos de Hola.

    ```azurecli
    az login

    az account set --subscription "mySubscriptionID"

    az group create --name "myResourceGroup" --location "westus" 
    
    az group deployment create -g "myResourceGroup" --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-acs-kubernetes/azuredeploy.json" --parameters @azuredeploy.parameters.json
    ```


## <a name="option-2-generate-a-service-principal-when-creating-hello-cluster-with-az-acs-create"></a>Opción 2: Generar a una entidad de servicio al crear el clúster de hello con`az acs create`

Si ejecuta hello [ `az acs create` ](/cli/azure/acs#create) toocreate comando Hola Kubernetes clúster, tienes Hola opción toogenerate una entidad de servicio automáticamente.

Al igual que sucede con otras opciones de creación de clústeres de Kubernetes, al ejecutar `az acs create` se pueden especificar los parámetros de una entidad de servicio existente. Sin embargo, si se omiten estos parámetros, Hola CLI de Azure crea una automáticamente para su uso con el servicio de contenedor. Esto tiene lugar de forma transparente durante la implementación de Hola. 

Hello comando siguiente crea un clúster Kubernetes y genera claves de SSH y las credenciales de servicio principal:

```console
az acs create -n myClusterName -d myDNSPrefix -g myResourceGroup --generate-ssh-keys --orchestrator-type kubernetes
```

> [!IMPORTANT]
> Si su cuenta no tiene hello Azure AD y toocreate de permisos de suscripción en una entidad de servicio, el comando de hello genera un error similar demasiado`Insufficient privileges toocomplete hello operation.`
> 

## <a name="additional-considerations"></a>Consideraciones adicionales

* Si no tiene permisos toocreate una entidad de servicio en su suscripción, puede que tenga tooask Azure AD o suscripción administrador tooassign Hola permisos necesarios o pídale una toouse principal de servicio con el servicio de contenedor de Azure. 

* entidad de servicio Hola para Kubernetes es un elemento de configuración del clúster Hola. Sin embargo, no use clústeres de hello identidad toodeploy Hola.

* Cada entidad de servicio está asociada a una aplicación de Azure AD. Hello entidad de servicio para un clúster de Kubernetes puede asociarse con cualquier Azure válida nombre de la aplicación de AD (por ejemplo: `https://www.contoso.org/example`). dirección URL de Hello para la aplicación hello no tiene toobe un punto de conexión real.

* Cuando especifica la entidad de servicio de hello **Id. de cliente**, se puede utilizar el valor de Hola de hello `appId` (como se muestra en este artículo) o entidad de servicio correspondiente hello `name` (por ejemplo,`https://www.contoso.org/example`).

* En master de Hola y el agente máquinas virtuales en clúster de Kubernetes Hola, credenciales de entidad de seguridad de servicio de Hola se almacenan en hello archivo /etc/kubernetes/azure.json.

* Cuando usas hello `az acs create` comando entidad de servicio de hello toogenerate automáticamente, se escriben las credenciales de entidad de seguridad de servicio de hello toohello archivo ~/.azure/acsServicePrincipal.json en la máquina de hello usa comandos de hello toorun. 

* Cuando usas hello `az acs create` comando entidad de servicio de hello toogenerate automáticamente, también puede autenticar la entidad de servicio de Hola con un [registro de contenedor de Azure](../../container-registry/container-registry-intro.md) creadas en hello mismo suscripción.




## <a name="next-steps"></a>Pasos siguientes

* [Introducción a Kubernetes](container-service-kubernetes-walkthrough.md) en el clúster de Container Service.

* entidad de servicio de tootroubleshoot Hola para Kubernetes, vea hello [documentación del motor de ACS](https://github.com/Azure/acs-engine/blob/master/docs/kubernetes.md#troubleshooting).


