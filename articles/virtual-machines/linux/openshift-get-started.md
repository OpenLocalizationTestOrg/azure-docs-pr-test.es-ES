---
title: aaaDeploy origen OpenShift tooAzure | Documentos de Microsoft
description: "Obtenga información acerca de las máquinas virtuales tooAzure toodeploy OpenShift origen."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: jbinder
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 
ms.author: jbinder
ms.openlocfilehash: a67450c46da41134a5f6c669a9e54e14773ac5b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-openshift-origin-tooazure-virtual-machines"></a>Implementar OpenShift origen tooAzure máquinas virtuales 

[OpenShift Origin](https://www.openshift.org/) es una plataforma de contenedor de código abierto basada en [Kubernetes](https://kubernetes.io/). Simplifica el proceso de Hola de implementar, ajuste de escala y utilizar aplicaciones de varios inquilinos. 

Esta guía describe cómo toodeploy OpenShift origen sobre el uso de máquinas virtuales de Azure Hola CLI de Azure y las plantillas de administrador de recursos de Azure. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Crear un toomanage KeyVault claves SSH para clúster de OpenShift Hola.
> * Implementar un clúster de OpenShift en máquinas virtuales de Azure. 
> * Instalar y configurar hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) clúster de hello toomanage.
> * Personalizar la implementación de OpenShift Hola.

Si no tiene una suscripción a Azure, cree una [cuenta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de empezar.

Este inicio rápido requiere hello Azure CLI versión 2.0.8 o posterior. versión de hello toofind, ejecute `az --version`. Si necesita tooinstall o una actualización, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure 
Inicie sesión en la suscripción de Azure con hello tooyour [inicio de sesión de az](/cli/azure/#login) comando y siga hello en pantalla instrucciones o haga clic en **Pruébelo** toouse Shell en la nube.

```azurecli 
az login
```
## <a name="create-a-resource-group"></a>Crear un grupo de recursos

Crear un grupo de recursos con hello [crear grupo az](/cli/azure/group#create) comando. Un grupo de recursos de Azure es un contenedor lógico en el que se implementan y se administran los recursos de Azure. 

Hello en el ejemplo siguiente se crea un grupo de recursos denominado *myResourceGroup* en hello *eastus* ubicación.

```azurecli 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves
Crear un Hola de toostore KeyVault claves SSH para clúster Hola con hello [crear az keyvault](/cli/azure/keyvault#create) comando.  

```azurecli 
az keyvault create --resource-group myResourceGroup --name myKeyVault \
       --enabled-for-template-deployment true \
       --location eastus
```

## <a name="create-an-ssh-key"></a>Creación de una clave SSH 
Una clave SSH es necesario toosecure acceso toohello clúster OpenShift origen. Crear un par de claves SSH con hello `ssh-keygen` comando. 
 
 ```bash
ssh-keygen -f ~/.ssh/openshift_rsa -t rsa -N ''
```

> [!NOTE]
> Hola par de claves SSH que cree no debe tener una frase de contraseña.

Para obtener más información sobre las claves SSH en Windows, [cómo toocreate SSH teclas Windows](/azure/virtual-machines/linux/ssh-from-windows).

## <a name="store-ssh-private-key-in-key-vault"></a>Almacenamiento de la clave privada de SSH en Key Vault
Hola OpenShift implementación utiliza la clave SSH de hello creaste acceso toosecure toohello OpenShift master. tooenable Hola implementación toosecurely recuperar la clave SSH hello, almacenar la clave de hello en el almacén de claves mediante el siguiente comando de Hola.

# <a name="enabled-for-template-deployment"></a>Habilitación para la implementación de plantilla
```azurecli
az keyvault secret set --vault-name KeyVaultName --name OpenShiftKey --file ~/.ssh/openshift.rsa
```

## <a name="create-a-service-principal"></a>Creación de una entidad de servicio 
OpenShift se comunica con Azure mediante un nombre de usuario y una contraseña, o a través de una entidad de servicio. Las entidades de servicio de Azure son identidades de seguridad que pueden usarse con aplicaciones, servicios y herramientas de automatización como OpenShift. Controlar y definir permisos de hello como entidad de servicio de hello toowhat operaciones puede llevar a cabo en Azure. tooimprove seguridad a través de la que se proporcionen un nombre de usuario y una contraseña, este ejemplo crea un servicio básico principal.

Crear un servicio principal con [az ad sp crear-de-rbac](/cli/azure/ad/sp#create-for-rbac) y las credenciales de Hola de salida que necesita OpenShift:

```azurecli
az ad sp create-for-rbac --name openshiftsp \
          --role Contributor --password {strong password} \
          --scopes $(az group show --name myResourceGroup --query id)
```
Tome nota de la propiedad de appId Hola devuelta por el comando Hola.
```json
{
  "appId": "a487e0c1-82af-47d9-9a0b-af184eb87646d",
  "displayName": "openshiftsp",
  "name": "http://openshiftsp",
  "password": {strong password},
  "tenant": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX"
}
```
 > [!WARNING] 
 > No cree una contraseña que no sea segura.  Siga la guía de las [restricciones y reglas de contraseña de Azure AD](/azure/active-directory/active-directory-passwords-policy).

Para más información, sobre las entidades de servicio, consulte [Creación de una entidad de servicio de Azure con la CLI de Azure 2.0](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="deploy-hello-openshift-origin-template"></a>Implementar la plantilla de origen de OpenShift Hola
A continuación implemente OpenShift Origin mediante una plantilla de Azure Resource Manager. 

> [!NOTE] 
> el comando siguiente Hello requiere az CLI 2.0.8 o una versión posterior. Puede comprobar Hola az CLI versión con hello `az --version` comando. Hola tooupdate versión CLI, consulte [instalar Azure CLI 2.0]( /cli/azure/install-azure-cli).

Hola de uso `appId` valor de entidad de seguridad de servicio de Hola que creó anteriormente para hello `aadClientId` parámetro.

```azurecli 
az group deployment create --name myOpenShiftCluster \
      --template-uri https://raw.githubusercontent.com/Microsoft/openshift-origin/master/azuredeploy.json \
      --params \ 
        openshiftMasterPublicIpDnsLabel=myopenshiftmaster \
        infraLbPublicIpDnsLabel=myopenshiftlb \
        openshiftPassword=Pass@word!
        sshPublicKey=~/.ssh/openshift_rsa.pub \
        keyVaultResourceGroup=myResourceGroup \
        keyVaultName=myKeyVault \
        keyVaultSecret=OpenShiftKey \
        aadClientId={appId} \
        aadClientSecret={strong password} 
```
implementación de Hello puede tardar too20 minutos toocomplete. Hello dirección URL de la consola de OpenShift de Hola y el nombre DNS de hello OpenShift maestro está imprime toohello terminal cuando se completa la implementación de Hola.

```json
{
  "OpenShift Console Uri": "http://openshiftlb.cloudapp.azure.com:8443/console",
  "OpenShift Master SSH": "ocpadmin@myopenshiftmaster.cloudapp.azure.com"
}
```
## <a name="connect-toohello-openshift-cluster"></a>Conectar toohello OpenShift clúster
Cuando se haya completado la implementación de hello, conectar la consola de OpenShift toohello mediante explorador hello mediante hello `OpenShift Console Uri`. O bien, puede conectarse a toohello OpenShift maestra mediante el siguiente comando de Hola.

```bash
$ ssh ocpadmin@myopenshiftmaster.cloudapp.azure.com
```

## <a name="clean-up-resources"></a>Limpieza de recursos
Cuando ya no necesite, puede usar hello [eliminación del grupo az](/cli/azure/group#delete) comandos tooremove grupo de recursos de hello, OpenShift clúster y todos ellos relacionados con recursos.

```azurecli 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido cómo:
> [!div class="checklist"]
> * Crear un toomanage KeyVault claves SSH para clúster de OpenShift Hola.
> * Implementar un clúster de OpenShift en máquinas virtuales de Azure. 
> * Instalar y configurar hello [OpenShift CLI](https://docs.openshift.org/latest/cli_reference/index.html#cli-reference-index) clúster de hello toomanage.

Ahora el clúster de OpenShift Origin está implementado. Puede seguir OpenShift tutoriales toolearn cómo toodeploy su primera aplicación y utilice Hola OpenShift herramientas. Vea [introducción con el origen de OpenShift](https://docs.openshift.org/latest/getting_started/index.html) tooget iniciado. 
