---
title: "aaaUse agentes de máquina virtual de Azure para la integración continua con Jenkins."
description: "Agentes de máquina virtual de Azure como servidores subordinados de Jenkins."
services: multiple
documentationcenter: 
author: mlearned
manager: douge
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 6/7/2017
ms.author: mlearned
ms.custom: Jenkins
ms.openlocfilehash: 2388e6919d0280372166fbd325d80dafb00d7550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-vm-agents-for-continuous-integration-with-jenkins"></a>Use los agentes de máquina virtual de Azure para la integración continua con Jenkins.

Este tutorial rápido muestra cómo toouse Hola agentes de máquina virtual de Azure Jenkins complemento toocreate un agente de Linux (Ubuntu) a petición en Azure.

## <a name="prerequisites"></a>Requisitos previos

toocomplete este tutorial rápido:

* Si no dispone de un patrón Jenkins, puede empezar con hello [plantilla de solución](install-jenkins-solution-template.md) 
* Consulte demasiado[crear una entidad de seguridad de servicio de Azure con Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) si ya no dispone de una entidad de seguridad de servicio de Azure.

## <a name="install-azure-vm-agents-plugin"></a>Instalación del complemento de agentes de máquina virtual de Azure

Si inicia desde hello [plantilla de solución](install-jenkins-solution-template.md), complemento de hello Azure VM Agent está instalado en master de hello Jenkins.

En caso contrario, instalar hello **agentes de máquina virtual de Azure** complemento desde dentro del panel de hello Jenkins.

## <a name="configure-hello-plugin"></a>Configurar el complemento de Hola

* En el panel de Jenkins hello, haga clic en **Jenkins administrar -> configurar el sistema ->**. Desplácese toohello inferior de la página de Hola y busque la sección de hello con lista desplegable de hello **agregar nueva nube**. En el menú de hello, seleccione **agentes de máquina virtual de Microsoft Azure**
* Seleccione una cuenta existente de lista desplegable de hello las credenciales de Azure.  tooadd un nuevo **entidad de servicio de Microsoft Azure,** escriba Hola siguientes valores: Id. de suscripción, Id. de cliente, el secreto de cliente y extremo de Token de OAuth 2.0.

![Credenciales de Azure](./media/jenkins-azure-vm-agents/service-principal.png)

* Haga clic en **Compruebe la configuración de** toomake que esa configuración de perfil de hello es correcta.
* Guardar configuración de Hola y continuar toohello siguiente paso.

## <a name="template-configuration"></a>Configuración de plantilla

### <a name="general-configuration"></a>Configuración general
A continuación, configure una plantilla para uso toodefine un agente de máquina virtual de Azure. 

* Haga clic en **agregar** tooadd una plantilla. 
* Proporcione un nombre para la nueva plantilla. 
* Para la etiqueta de hello, escriba "ubuntu." Esta etiqueta se usa durante la configuración del trabajo de Hola.
* Seleccionar región deseada Hola de cuadro combinado de Hola.
* Seleccione Hola había deseado tamaño de máquina virtual.
* Especifique el nombre de cuenta de almacenamiento de Azure de Hola o dejarlo nombre predeterminado de hello toouse en blanco "jenkinsarmst."
* Especifique el tiempo de retención de hello en minutos. Esta opción define el número de Hola de minutos que Jenkins puede esperar antes de eliminar automáticamente un agente inactivo. Especifique 0 si no desea toobe agentes inactivo elimina automáticamente.

![Configuración general](./media/jenkins-azure-vm-agents/general-config.png)

### <a name="image-configuration"></a>Configuración de imagen

toocreate un agente de Linux (Ubuntu), seleccione **referencia de imagen** y use Hola siguiente configuración como ejemplo. Consulte demasiado[Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute?subcategories=virtual-machine-images&page=1) para hello Azure más reciente admite imágenes.

* Image Publisher (Publicador de imagen): Canonical
* Image Offer (Oferta de imagen): UbuntuServer
* Image Sku (SKU de imagen): 14.04.5-LTS
* Image version (Versión de imagen): la más reciente
* OS Type (Tipo de sistema operativo): Linux
* Launch method (Método de inicio): SSH
* Proporcione unas credenciales de administrador.
* Para el script de inicialización de la máquina virtual, escriba:
```
# Install Java
sudo apt-get -y update
sudo apt-get install -y openjdk-7-jdk
sudo apt-get -y update --fix-missing
sudo apt-get install -y openjdk-7-jdk
```
![Configuración de imagen](./media/jenkins-azure-vm-agents/image-config.png)

* Haga clic en **comprobar plantilla** configuración de tooverify Hola.
* Haga clic en **Guardar**.

## <a name="create-a-job-in-jenkins"></a>Creación de un trabajo en Jenkins

* En el panel de Jenkins hello, haga clic en **nuevo elemento**. 
* Escriba un nombre y seleccione **Freestyle project** (Proyecto de estilo libre) y haga clic en **OK** (Aceptar).
* Hola **General** ficha, seleccione "Restringir donde se puede ejecutar el proyecto" y escriba "ubuntu" en la expresión de etiqueta. Ahora verá "ubuntu" en la lista desplegable de Hola.
* Haga clic en **Guardar**.

![Configurar un proyecto](./media/jenkins-azure-vm-agents/job-config.png)

## <a name="build-your-new-project"></a>Compilación de un nuevo proyecto

* Volver atrás toohello Jenkins panel.
* Nuevo trabajo de Hola de menú contextual que ha creado, a continuación, haga clic en **compila ahora**. Se inicia una compilación. 
* Una vez completada la compilación de hello, vaya demasiado**salida de consola**. Verá que compilación Hola se realizó de forma remota en Azure.

![Salida de consola](./media/jenkins-azure-vm-agents/console-output.png)

## <a name="reference"></a>Referencia

* Vídeo de Azure Friday: [Continuous Integration with Jenkins using Azure VM agents](https://channel9.msdn.com/Shows/Azure-Friday/Continuous-Integration-with-Jenkins-Using-Azure-VM-Agents) (Integración continua con Jenkins mediante agentes de máquina virtual de Azure)
* Opciones de configuración e información de soporte técnico: [Azure VM Agent Jenkins Plugin Wiki](https://wiki.jenkins-ci.org/display/JENKINS/Azure+VM+Agents+Plugin) (Wiki del complemento Jenkins de agente de máquina virtual de Azure) 

