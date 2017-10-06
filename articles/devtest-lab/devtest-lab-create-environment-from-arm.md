---
title: aaaCreate entornos de varias VM y los recursos de PaaS con plantillas del Administrador de recursos de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate entornos de varias VM y recursos de PaaS en Azure los laboratorios de desarrollo y pruebas de una plantilla de Azure Resource Manager"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2017
ms.author: tarcher
ms.openlocfilehash: ab8628f6cb5a666435258efb93921ec69ad3a13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-multi-vm-environments-and-paas-resources-with-azure-resource-manager-templates"></a>Creación de entornos de varias máquinas virtuales y recursos de PaaS con plantillas de Azure Resource Manager

Hola [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) permite tooeasily [crear y agregar un laboratorio VM tooa](https://docs.microsoft.com/en-us/azure/devtest-lab/devtest-lab-add-vm). Esto funciona bien para crear una máquina virtual a la vez. Sin embargo, si el entorno de hello contiene varias máquinas virtuales, cada máquina virtual tiene toobe creada de forma individual. En escenarios como una aplicación Web de varios nivel o una granja de SharePoint, un mecanismo es tooallow necesario para la creación de hello de varias máquinas virtuales en un solo paso. Mediante el uso de plantillas del Administrador de recursos de Azure, puede definir ahora infraestructura hello y la configuración de la solución de Azure y repetidamente implementar varias máquinas virtuales en un estado coherente. Esta característica proporciona Hola siguientes ventajas:

- Las plantillas de Azure Resource Manager se cargan directamente desde el repositorio de control de código fuente (GitHub o Git de Team Services).
- Una vez configurado, los usuarios pueden crear un entorno seleccionando una plantilla de Azure Resource Manager desde el portal de Azure como lo pueden hacer con otros tipos de hello [VM bases](./devtest-lab-comparing-vm-base-image-types.md).
- En un entorno a partir de una plantilla de Azure Resource Manager en suma tooIaaS máquinas virtuales se pueden aprovisionar recursos de PaaS de Azure.
- puede realizar el seguimiento de costo de Hola de entornos de laboratorio hello en suma tooindividual máquinas virtuales creadas por otros tipos de bases de.
- Recursos de PaaS se crean y se mostrarán en el costo de seguimiento; Sin embargo, cierre automático de máquina virtual no aplica tooPaaS recursos.
- Los usuarios tienen Hola mismo control de directiva de máquina virtual para entornos tengan para las máquinas virtuales del laboratorio único.

Obtener más información acerca de hello muchas [ventajas del uso de plantillas de administrador de recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#the-benefits-of-using-resource-manager) toodeploy, actualizar o eliminar todos los recursos de laboratorio en una sola operación.

> [!NOTE]
> Cuando se usa una plantilla de administrador de recursos como un toocreate base laboratorio más máquinas virtuales, hay algunas diferencias tookeep en cuenta si va a crear varias VM o VM único. En la plantilla de máquina virtual de Azure Resource Manager se explican estas diferencias con mayor detalle.
>
>

## <a name="configure-azure-resource-manager-template-repositories"></a>Configuración de los repositorios de plantillas de Azure Resource Manager

Como uno de los procedimientos recomendados de hello con infraestructura como código y configuración como código, plantillas de entorno debe administrarse en control de código fuente. Azure DevTest Labs sigue este procedimiento y carga todas las plantillas de Azure Resource Manager directamente desde los repositorios de GitHub o VSTS Git. Como resultado, las plantillas de administrador de recursos pueden usarse en el ciclo de versiones completo de hello, de hello prueba toohello entorno de producción.

Hay un par de reglas toofollow tooorganize sus plantillas de Azure Resource Manager en un repositorio:

- archivo de plantilla principal Hola debe denominarse `azuredeploy.json`. 

    ![Archivos de plantilla principal de Azure Resource Manager](./media/devtest-lab-create-environment-from-arm/master-template.png)

- Si desea que los valores de parámetro toouse definidos en un archivo de parámetros, archivo de parámetros de hello debe denominarse `azuredeploy.parameters.json`.
- Puede usar parámetros de hello `_artifactsLocation` y `_artifactsLocationSasToken` tooconstruct hello parametersLink valor del URI, lo que permite los laboratorios de desarrollo y pruebas tooautomatically administrar plantillas anidadas. Vea [How Azure DevTest Labs makes nested Resource Manager template deployments easier for testing environments](https://blogs.msdn.microsoft.com/devtestlab/2017/05/23/how-azure-devtest-labs-makes-nested-arm-template-deployments-easier-for-testing-environments/) Cómo Azure DevTest Labs facilita la implementación de las plantillas de Resource Manager anidadas para los entornos de prueba) para más información.
- Metadatos pueden ser descripción y nombre para mostrar plantilla hello toospecify definido. Estos metadatos deben estar en un archivo denominado `metadata.json`. Hello archivo de metadatos de ejemplo siguiente muestra cómo toospecify Hola Mostrar nombre y una descripción: 

```json
{
 
"itemDisplayName": "<your template name>",
 
"description": "<description of hello template>"
 
}
```

Hello siguientes pasos le guiarán agregando un laboratorio de tooyour de repositorio mediante Hola portal de Azure. 

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.   
1. En la hoja del laboratorio de hello, seleccione **directivas y configuración**.

    ![Directivas y configuración](./media/devtest-lab-create-environment-from-arm/configuration-and-policies-menu.png)

1. De hello **directivas y configuración** lista de configuración, seleccione **repositorios**. Hola **repositorios** hoja enumera los repositorios de Hola que se han agregado toohello laboratorio. Un repositorio denominado `Public Repo` se genera automáticamente para todas las prácticas y se conecta toohello [repositorio de GitHub de laboratorios de desarrollo y pruebas](https://github.com/Azure/azure-devtestlab) que contiene varios artefactos de máquina virtual para su uso.

    ![Repositorio público](./media/devtest-lab-create-environment-from-arm/public-repo.png)

1. Seleccione **agregar +** tooadd el repositorio de plantilla de Azure Resource Manager.
1. Al segundo Hola **repositorios** hoja se abre, escriba la información necesaria de hello como sigue:
    - **Nombre** : escriba el nombre de repositorio de Hola que se usa en el laboratorio de Hola.
    - **Dirección URL de clonación de GIT** -escriba la dirección URL de clonación GIT HTTPS Hola de GitHub o Visual Studio Team Services.  
    - **Rama** -escriba tooaccess de nombre de bifurcación de hello las definiciones de plantilla de Azure Resource Manager. 
    - **Token de acceso personal** -se utiliza el token de acceso personal hello toosecurely tener acceso a su repositorio. tooget el símbolo (token) de Visual Studio Team Services, seleccione  **&lt;YourName >> Mi perfil > seguridad > símbolo (token) de acceso público**. tooget su token de GitHub, seleccione su avatar seguido seleccionando **configuración > símbolo (token) de acceso público**. 
    - **Las rutas de acceso de carpeta** : mediante uno de los campos de entrada de hello dos, escriba la ruta de carpeta de Hola que empieza con una barra diagonal - / - y es relativa tooyour Git clone URI tooeither sus definiciones de artefacto (primer campo de entrada) o la plantilla de Azure Resource Manager definiciones.   
    
        ![Repositorio público](./media/devtest-lab-create-environment-from-arm/repo-values.png)

1. Una vez que todos los campos de hello necesaria se introducen y pasan la validación de hello, seleccione **guardar**.

Hola siguiente sección le guiará a través de crear entornos a partir de una plantilla de Azure Resource Manager.

## <a name="create-an-environment-from-an-azure-resource-manager-template"></a>Creación de un entorno a partir de una plantilla de Azure Resource Manager

Una vez que un repositorio de la plantilla de Azure Resource Manager se ha configurado en el laboratorio de hello, los usuarios de laboratorio pueden crear un entorno mediante el portal de Azure con hello pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
1. Seleccione **más servicios**y, a continuación, seleccione **laboratorios de desarrollo y pruebas** de lista de Hola.
1. En lista de Hola de laboratorios, seleccione laboratorio deseado Hola.   
1. En la hoja del laboratorio de hello, seleccione **agregar +**.
1. Hola **elegir una base de** hoja muestra imágenes base Hola se pueden usar con plantillas de Azure Resource Manager Hola aparece en primer lugar. Seleccione Hola había deseado plantilla del Administrador de recursos de Azure.

    ![Elegir base de datos](./media/devtest-lab-create-environment-from-arm/choose-a-base.png)
  
1. En hello **agregar** hoja, escriba Hola **nombre del entorno** valor. nombre del entorno de Hello es lo que los usuarios tooyour mostrado en el laboratorio de Hola. campos de entrada restantes Hola se definen en la plantilla de hello Azure Resource Manager. Si los valores predeterminados se definen en la plantilla de Hola o hello `azuredeploy.parameter.json` archivo está presente, se muestran los valores predeterminados en los campos de entrada. Para los parámetros de tipo *cadena segura*, puede usar los secretos de hello almacenados en laboratorio de hello [almacén secreto personal](https://azure.microsoft.com/en-us/updates/azure-devtest-labs-keep-your-secrets-safe-and-easy-to-use-with-the-new-personal-secret-store).

    ![Hoja Add (Agregar)](./media/devtest-lab-create-environment-from-arm/add.png)

    > [!NOTE]
    > Hay varios valores de parámetro que, aunque se especifiquen, aparecen vacíos. Por lo tanto, si los usuarios asignar esos tooparameters valores en una plantilla de Azure Resource Manager, laboratorios de desarrollo y pruebas no muestra valores de hello; en su lugar, que muestra los campos de entrada en blanco donde los usuarios del laboratorio Hola necesitan tooenter un valor al crear el entorno de Hola.
    > 
    > - GEN-UNIQUE
    > - GEN-UNIQUE-[N]
    > - GEN-SSH-PUB-KEY
    > - GEN-PASSWORD 
 
1. Seleccione **agregar** entorno de hello toocreate. entorno de Hello inicia aprovisionamiento inmediatamente con el estado de hello mostrar en hello **mis equipos virtuales** lista. Se crea automáticamente un nuevo grupo de recursos por hello laboratorio tooprovision todos los recursos de hello definidos en la plantilla de Azure Resource Manager Hola.
1. Una vez creado el entorno de hello, seleccione el entorno de Hola Hola **mis equipos virtuales** lista hoja de grupo de recursos de tooopen hello y examinar todos los recursos de hello aprovisionados en el entorno de Hola.
    
    ![Lista My virtual machines (Mis máquinas virtuales)](./media/devtest-lab-create-environment-from-arm/all-environment-resources.png)
   
   También puede expandir la lista de hello simplemente tooview Hola de entorno de máquinas virtuales que se aprovisionan en el entorno de Hola.
    
    ![Lista My virtual machines (Mis máquinas virtuales)](./media/devtest-lab-create-environment-from-arm/my-vm-list.png)

1. Haga clic en cualquiera de hello entornos tooview hello las acciones disponibles - como la aplicación de artefactos, adjuntar discos de datos, cambiar tiempo de cierre automático y mucho más.

    ![Acciones de entorno](./media/devtest-lab-create-environment-from-arm/environment-actions.png)

## <a name="next-steps"></a>Pasos siguientes
* Una vez creada una máquina virtual, puede conectarse toohello VM seleccionando **conectar** en la hoja de la máquina virtual de Hola.
* Ver y administrar recursos en un entorno seleccionando entorno Hola Hola **mis equipos virtuales** lista en el laboratorio. 
* Explorar hello [plantillas del Administrador de recursos de Azure desde la Galería de plantillas de inicio rápido de Azure](https://github.com/Azure/azure-quickstart-templates)
