---
title: "aaaInstall o configurar las máquinas virtuales de Terraform tooprovision y otras infraestructuras de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configurar Terraform toocreate Azure recursos"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a>Instalar y configurar las máquinas virtuales de Terraform tooprovision y otras infraestructuras en Azure 
Este artículo describe tooinstall de pasos necesarios de Hola y configure Terraform tooprovision recursos como máquinas virtuales en Azure. Obtendrá información sobre cómo toocreate y use Azure credenciales tooenable Terraform tooprovision recursos en la nube de forma segura.

HashiCorp Terraform proporciona una manera sencilla de toodefine e implementar la infraestructura de nube mediante un lenguaje de plantillas personalizadas denominado lenguaje de configuración de HashiCorp (HCL). Este lenguaje personalizado es [toowrite sencillo y fácil toounderstand](terraform-create-complete-vm.md). Además, mediante el uso de hello `terraform plan` de comandos, puede visualizar tooyour infraestructura de hello cambios antes de confirmarlos. Siga estos toostart pasos mediante Terraform con Azure.

## <a name="install-terraform"></a>Instalar Terraform
tooinstall Terraform, [descargar](https://www.terraform.io/downloads.html) paquete Hola adecuado para su sistema operativo en un directorio de instalación independiente. descarga de Hello contiene un solo archivo ejecutable para el que también debe definir una ruta de acceso global. Para obtener instrucciones sobre cómo tooset Hola ruta de acceso en Linux y Mac, vaya demasiado[esta página Web](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux). Para obtener instrucciones sobre cómo tooset Hola ruta de acceso en Windows, vaya demasiado[esta página Web](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows). tooverify la instalación, ejecute hello `terraform` comando. Debería ver una lista de opciones disponibles de Terraform como salida.

A continuación, deberá tooallow Terraform acceso tooyour suscripción de Azure tooperform aprovisionamiento de la infraestructura.

## <a name="set-up-terraform-access-tooazure"></a>Configurar Terraform acceso tooAzure
tooenable Terraform tooprovision recursos en Azure, necesita toocreate dos entidades en Azure Active Directory (Azure AD): una aplicación de Azure AD y una entidad de seguridad de servicio de Azure AD. Seguidamente, los identificadores de estas entidades se usan en los scripts de Terraform. La entidad de servicio es una instancia local de una aplicación de Azure AD global. Una entidad de servicio permite recursos de tooglobal de control de acceso local específico.

Hay varias toocreate formas una aplicación de Azure AD y una entidad de seguridad de servicio de Azure AD. Hola más rápido y sencillo cierto hoy en día es toouse 2.0 de CLI de Azure, que [puede descargar e instalar en Windows, Linux o Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). También puede utilizar la infraestructura de seguridad necesarios de hello toocreate PowerShell o CLI de Azure 1.0. instrucciones de Hello siguientes muestran cómo tooconfigure Terraform de Azure mediante el uso de todos estos enfoques.

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a>Usar la CLI de Azure 2.0 (para usuarios de Windows, Linux o Mac) 
Después de descargar e instalar hello [CLI de Azure 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), inicie sesión en tooadminister su suscripción de Azure mediante la emisión de hello siguiente comando:

```
az login
```

>[!NOTE]
>Si usas Hola China, Azure en Alemania o nubes de Azure Government, necesita toofirst configurar hello Azure CLI toowork con esa nube. Puede hacerlo ejecutando Hola siguiente:

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

Si tiene varias suscripciones de Azure, se devuelven sus detalles por hello `az login` comando. Conjunto hello `SUBSCRIPTION_ID` devuelve el valor de hello toohold variables de entorno del programa Hola a `id` campo de la suscripción de hello desea toouse. 

Establecer la suscripción de Hola que quiere toouse de esta sesión.

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

Id. de suscripción de hello cuenta tooget Hola de consulta y valores de Id. de inquilino.

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

A continuación, cree credenciales separadas para Terraform.

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

Se devuelven el valor de appId, password, sp_name y tenant. Tome nota de appId de hello y una contraseña.

tooconfirm sus credenciales (entidad de servicio), abra un nuevo shell y ejecute hello siga los comandos. Hola de sustitución devuelve valores para sp_name, la contraseña y el inquilino:

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a>Usar PowerShell (para usuarios de Windows) 
toouse Windows toowrite del equipo y ejecutar su Terraform secuencias de comandos y toouse PowerShell para tareas de configuración, configurar la máquina con herramientas de PowerShell de hello adecuadas. 

1. Instalar herramientas de PowerShell siguiendo los pasos de hello en [instalar y configurar Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps). 

2. Descargar y ejecutar hello [secuencia de comandos de azure setup.ps1](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) desde la consola de PowerShell de Hola.

3. secuencia de comandos toorun hello setup.ps1 de azure, descargarla y ejecutar hello `./azure-setup.ps1 setup` comando desde la consola de PowerShell de Hola. A continuación, inicie sesión en tooyour suscripción de Azure con privilegios administrativos.

4. Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite. Opcionalmente, proporcione una contraseña segura cuando se le solicite. Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a>Usar la CLI de Azure 1.0 (para usuarios de Linux o Mac)
tooget iniciados con Terraform en máquinas de Linux o Mac con 1.0 de CLI de Azure, instale Hola bibliotecas adecuadas en su equipo.  

1. Instalar las herramientas CLI de Azure xPlat siguiendo los pasos de hello en [instalar Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). 

2. Descargar e instalar un procesador JSON siguiendo las instrucciones de hello en [descargar jq](https://stedolan.github.io/jq/download/).

3. Descargar y ejecutar hello [secuencia de comandos de azure setup.sh](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script desde la consola de Hola.

4. secuencia de comandos toorun hello setup.sh de azure, descargarla y ejecutar hello `./azure-setup setup` comando desde la consola de Hola. A continuación, inicie sesión en tooyour suscripción de Azure con privilegios administrativos.
 
5. Proporcione un nombre de aplicación (una cadena arbitraria, obligatoria) cuando se le solicite. Opcionalmente, proporcione una contraseña segura cuando se le solicite. Si no proporciona una contraseña, se genera una contraseña segura automáticamente con las bibliotecas de seguridad de .NET.

Todos los scripts anteriores Hola crean una aplicación de Azure AD y el servicio principal. Hola service principal obtiene un colaborador o acceso de nivel de propietario de la suscripción de Hola. Debido a Hola alto nivel de acceso concedido, siempre debería proteger la información de seguridad de hello generado por los scripts. Anote los cuatro elementos de información de seguridad que proporcionan los scripts: appId, password, subscription_id y tenant_id.

## <a name="set-environment-variables"></a>Establecimiento de variables de entorno
Después de crear y configurar una entidad de seguridad de servicio de Azure AD, necesita toolet Terraform saber Id. de inquilino de hello, Id. de suscripción, Id. de cliente y toouse secreto de cliente. Para ello, inserte esos valores en los scripts de Terraform, tal y como se describe en [Creación de una infraestructura básica de Azure mediante Terraform](terraform-create-complete-vm.md). Como alternativa, puede establecer Hola después de las variables de entorno (y, por tanto, evitar accidentalmente proteger o compartir sus credenciales):

- ARM_SUBSCRIPTION_ID
- ARM_CLIENT_ID
- ARM_CLIENT_SECRET
- ARM_TENANT_ID

Puede usar este tooset de secuencia de comandos de shell de ejemplo esas variables:

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

Además, si utiliza Terraform con Azure en China, o bien administración pública de Azure o Azure en Alemania, deberá variable de entorno tooset Hola adecuadamente.

## <a name="next-steps"></a>Pasos siguientes
Ya ha instalado Terraform y configurado las credenciales de Azure para poder iniciar la implementación de la infraestructura en su suscripción de Azure. A continuación, obtenga información acerca de cómo demasiado[crear infraestructura con Terraform](terraform-create-complete-vm.md).
