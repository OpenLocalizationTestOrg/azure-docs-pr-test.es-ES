---
title: "Preguntas más frecuentes de laboratorios de desarrollo y pruebas aaaAzure | Documentos de Microsoft"
description: Encuentre respuestas toocommon preguntas de laboratorios de desarrollo y pruebas de Azure
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: afe83109-b89f-4f18-bddd-b8b4a30f11b4
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: tarcher
ms.openlocfilehash: 07d4c870eca21856750a472ed503de4a2734a438
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-devtest-labs-faq"></a>Preguntas más frecuentes sobre Azure DevTest Labs
Este artículo ofrece respuestas a algunas preguntas más frecuentes de hello sobre laboratorios de desarrollo y pruebas de Azure.

**General**
## <a name="what-if-my-question-isnt-answered-here"></a>Mi pregunta no está respondida aquí. ¿Qué debo hacer?
Si su pregunta no aparece aquí, háganoslo saber para que podamos ayudarlo a encontrar una respuesta.

* Publicar una pregunta en hello [Disqus subproceso](#comments) final Hola de estas preguntas más frecuentes y ponerse en contacto con el equipo de la memoria caché de Azure de Hola y otros miembros de la Comunidad sobre este artículo.
* tooreach un público más amplio, publicar una pregunta en hello [foro de MSDN de laboratorios de desarrollo y pruebas de Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=AzureDevTestLabs)y ponerse en contacto con el equipo de laboratorios de desarrollo y pruebas de Azure de Hola y otros miembros de la Comunidad de Hola.
* toomake una solicitud de característica, envíe su solicitudes e ideas toohello [voz de usuario de laboratorios de desarrollo y pruebas de Azure](https://feedback.azure.com/forums/320373-azure-devtest-labs).

## <a name="why-should-i-use-azure-devtest-labs"></a>¿Por qué debería usar Azure DevTest Labs?
Azure DevTest Labs puede ahorrarle a su equipo tiempo y dinero. Los programadores pueden crear sus propios entornos con distintas varias bases y utilizar artefactos tooquickly implementar y configurar aplicaciones. Mediante imágenes personalizadas y fórmulas, las máquinas virtuales se pueden guardar como plantillas y reproducirse fácilmente. Además, los laboratorios ofrecen varias directivas configurables que permiten a los administradores de laboratorio tooreduce residuos y administrar entornos de un equipo. Estas directivas incluyen apagado automático, umbral de costos, número máximo de máquinas virtuales por usuario y tamaños máximos de máquinas virtuales. Para obtener una explicación más detallada de los laboratorios de desarrollo y pruebas de Azure, lea hello [Introducción](devtest-lab-overview.md) o inspección hello [vídeo de introducción](/documentation/videos/videos/what-is-azure-devtest-labs).

## <a name="what-does-worry-free-self-service-mean"></a>¿Qué significa "sin preocupaciones, autoservicio"?
"Autoservicio preocupaciones," significa que los desarrolladores y evaluadores crean sus propios entornos según sea necesario, y los administradores tienen la seguridad de Hola de saber que los laboratorios de desarrollo y pruebas de Azure ayuda a minimizar los residuos y controlar los costos. Los administradores pueden especificar qué tamaños de máquina virtual se permiten, número máximo de Hola de máquinas virtuales, y cuando se inician y apagar las máquinas virtuales. Azure laboratorios de desarrollo y pruebas también resulta fácil toomonitor costos y toostay de alertas de conjunto consciente de cómo se usan recursos de laboratorio Hola.

## <a name="how-can-i-use-azure-devtest-labs"></a>¿Cómo se usa Azure DevTest Labs?
Laboratorios de desarrollo y pruebas de Azure es útil en cualquier momento necesita desarrollo o entornos de prueba y desea tooreproduce ellos rápidamente o administrarlos con directivas de ahorro de costos.

Estos son algunos escenarios en los que nuestros clientes usan Azure DevTest Labs:

* Administración de entornos de desarrollo y pruebas en un solo lugar, utilizando las directivas tooreduce costo y tooshare imágenes personalizadas compilaciones de team Hola.
* Desarrollar una aplicación usando el estado de disco de imágenes personalizadas toosave Hola a lo largo de fases de desarrollo de Hola.
* Costo de hello en relación tooprogress de seguimiento.
* Creación de entornos de prueba masivos para pruebas de garantía de calidad.
* Mediante el tooeasily artefactos y fórmulas configure y reproducir una aplicación en varios entornos.
* Distribuir las máquinas virtuales para hackathons (trabajo de desarrollo o prueba colaboración) y, a continuación, fácilmente la cancelación del aprovisionamiento ellos cuando finaliza el evento Hola.

## <a name="how-am-i-billed-for-azure-devtest-labs"></a>¿Cómo se factura Azure DevTest Labs?
Laboratorios de desarrollo y pruebas de Azure es un servicio gratuito, lo que significa que los laboratorios de crear y configurar artefactos, las plantillas y directivas de hello estén disponible. Solo paga por hello Azure recursos que usa en sus laboratorios, como máquinas virtuales, las cuentas de almacenamiento y redes virtuales. Para obtener más información sobre el costo de Hola de recursos de laboratorio, obtenga información sobre [laboratorios de desarrollo y pruebas de Azure precios](https://azure.microsoft.com/pricing/details/devtest-lab/).


**Seguridad**
## <a name="what-are-hello-different-security-levels-in-azure-devtest-labs"></a>¿Qué Hola diferentes niveles de seguridad en los laboratorios de desarrollo y pruebas de Azure?
La seguridad del acceso viene determinada por el [Control de acceso basado en roles (RBAC) de Azure](../active-directory/role-based-access-built-in-roles.md). toounderstand cómo tener acceso a works, ayuda a las diferencias de hello toounderstand entre un permiso, un rol y un ámbito tal como se define por RBAC.

* **Permiso** -un permiso es una acción específica de tooa de acceso definido. Por ejemplo, un permiso puede ser máquinas virtuales de tooall de acceso de lectura.
* **Rol** -un rol es un conjunto de permisos que se pueden agrupar y tooa usuario asignado. Por ejemplo, un "propietario de la suscripción" tiene acceso a los recursos de tooall dentro de una suscripción.
* **Ámbito** -un ámbito es un nivel dentro de la jerarquía de Hola de recursos de Azure. Por ejemplo, un ámbito puede ser un grupo de recursos o una sola suscripción toda laboratorio u Hola.

En el ámbito de Hola de laboratorios de desarrollo y pruebas de Azure, hay dos tipos de permisos de usuario de roles toodefine: usuario de laboratorio y de propietario de laboratorio.

* **Propietario de laboratorio** -un propietario de laboratorio tiene Hola acceder a tooany los recursos de laboratorio Hola. Por lo tanto, puede modificar las directivas, leer y escribir todas las máquinas virtuales, cambiar la red virtual de Hola y así sucesivamente.
* **Usuario de laboratorio** : un usuario de laboratorio puede ver todos los recursos de laboratorio, como máquinas virtuales, directivas y redes virtuales, pero no puede modificar las directivas ni las máquinas virtuales creadas por otros usuarios. También es posible toocreate roles personalizados en los laboratorios de desarrollo y pruebas de Azure y aprenderá cómo toodo en el artículo de hello, [conceder permisos de usuario en las directivas de laboratorio toospecific](devtest-lab-grant-user-permissions-to-specific-lab-policies.md).

Puesto que los ámbitos son jerárquicos, cuando un usuario tiene permisos en un ámbito determinado, también se le conceden automáticamente en cada ámbito de nivel inferior que engloba. Por ejemplo, si se asigna a un usuario toohello rol de propietario de la suscripción, a continuación, tienen acceso a los recursos tooall en una suscripción. Estos recursos incluyen todas las máquinas virtuales, todas las redes virtuales y todos los laboratorios. Por lo tanto, un propietario de la suscripción hereda automáticamente el rol Hola del propietario de laboratorio. Sin embargo, no es cierto Hola opuesto. El propietario de un laboratorio tiene laboratorio tooa de acceso, que es un ámbito inferior al nivel de suscripción de Hola. Por lo tanto, un propietario de laboratorio no es capaz de toosee las máquinas virtuales o redes virtuales o todos los recursos que se encuentran fuera del laboratorio de Hola.

## <a name="how-do-i-create-a-role-tooallow-users-tooperform-a-specific-task"></a>¿Cómo creo un tooperform de los usuarios de rol tooallow una tarea específica?
Un artículo completo sobre cómo toocreate de roles personalizados y asignar permisos toothat rol pueden encontrarse aquí. Este es un ejemplo de un script que crea el rol de Hola "DevTest laboratorios avanzada User", que tiene permiso toostart y detener todas las máquinas virtuales en el laboratorio de hello:

    $policyRoleDef = Get-AzureRmRoleDefinition "DevTest Labs User"
    $policyRoleDef.Actions.Remove('Microsoft.DevTestLab/Environments/*')
    $policyRoleDef.Id = $null
    $policyRoleDef.Name = "DevTest Labs Advance User"
    $policyRoleDef.IsCustom = $true
    $policyRoleDef.AssignableScopes.Clear()
    $policyRoleDef.AssignableScopes.Add("subscriptions/<subscription Id>")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Start/action")
    $policyRoleDef.Actions.Add("Microsoft.DevTestLab/labs/virtualMachines/Stop/action")
    $policyRoleDef = New-AzureRmRoleDefinition -Role $policyRoleDef  


**Automatización e integración de CI/CD**
## <a name="does-azure-devtest-labs-integrate-with-my-cicd-toolchain"></a>¿Se integra Azure DevTest Labs con mi cadena de herramientas de CI/CD?
Si usas VSTS, hay un [extensión tareas de laboratorios de desarrollo y pruebas de Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) que le permite tooautomate la versión de canalización en los laboratorios de desarrollo y pruebas de Azure. Algunos de los usos de Hola de esta extensión incluyen:

* Crear e implementar automáticamente una máquina virtual y configurarlo con la compilación más reciente de hello con Azure File Copy o PowerShell VSTS tareas.
* Capturar automáticamente el estado de Hola de una máquina virtual después de probar tooreproduce un error en Hola la misma máquina virtual para que lo investiguen.
* Eliminar Hola VM final Hola de hello liberar canalización cuando ya no es necesario.

Hello entradas de blog siguientes proporcionan instrucciones e información sobre el uso de la extensión VSTS hello:

* [Azure DevTest Labs: extensión de VSTS](https://blogs.msdn.microsoft.com/devtestlab/2016/06/15/azure-devtest-labs-vsts-extension/)
* [Deploying a new VM in an existing AzureDevTestLab from VSTS (Implementación de una nueva máquina virtual en un laboratorio de AzureDevTestLab existente desde VSTS)](http://www.visualstudiogeeks.com/blog/DevOps/Deploy-New-VM-To-Existing-AzureDevTestLab-From-VSTS)
* [Uso de VSTS Release Management para implementaciones continua tooAzureDevTestLabs](http://www.visualstudiogeeks.com/blog/DevOps/Use-VSTS-ReleaseManagement-to-Deploy-and-Test-in-AzureDevTestLabs)

Para otros toolchains CI/CD, Hola todos los mencionados anteriormente escenarios que se pueden lograr a través de hello extensión VSTS tareas se puede lograr de forma similar a través de implementación [plantillas de Azure Resource Manager](https://aka.ms/dtlquickstarttemplate) con [ Cmdlets de PowerShell de Azure](../azure-resource-manager/resource-group-template-deploy.md) y [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Management.DevTestLabs/). También puede usar [API de REST para los laboratorios de desarrollo y pruebas](http://aka.ms/dtlrestapis) toointegrate con su cadena de herramientas.  


**Máquinas virtuales**
## <a name="why-cant-i-see-certain-vms-in-hello-azure-virtual-machines-blade-that-i-see-within-azure-devtest-labs"></a>¿Por qué no puedo ver determinadas máquinas virtuales en la hoja de máquinas virtuales de Azure de Hola que he visto en los laboratorios de desarrollo y pruebas de Azure?
Cuando se crea una máquina virtual en los laboratorios de desarrollo y pruebas de Azure, permiso está dado tooaccess esa máquina virtual. Es capaz de tooview, tanto en la hoja de laboratorios de Hola y Hola **máquinas virtuales** hoja. Los usuarios en función de los laboratorios de desarrollo y pruebas de hello pueden ver todas las máquinas virtuales que se creó en la práctica de Hola a través del laboratorio de hello **todas las máquinas virtuales** hoja. Sin embargo, los usuarios en función de los laboratorios de desarrollo y pruebas de hello no se conceden automáticamente los recursos de acceso de lectura tooVM creados por otros. Por lo tanto, esas máquinas virtuales no se muestran en hello **máquinas virtuales** hoja.

## <a name="what-is-hello-difference-between-custom-images-and-formulas"></a>¿Cuál es la diferencia de hello entre imágenes personalizadas y las fórmulas?
Una imagen personalizada es un disco duro virtual (VHD), mientras que una fórmula es una imagen que se puede configurar con opciones adicionales que se pueden guardar y reproducir. Una imagen personalizada puede ser preferible si desea tooquickly crear varios entornos con hello misma imagen básica, inmutable. Una fórmula puede ser mejor si desea tooreproduce Hola configuración de la máquina virtual con los bits más recientes de hello, una red/subred virtual o un tamaño específico. Para obtener una explicación más detallada, vea el artículo de hello [comparar imágenes personalizadas y las fórmulas en los laboratorios de desarrollo y pruebas](devtest-lab-comparing-vm-base-image-types.md).

## <a name="how-do-i-create-multiple-vms-from-hello-same-template-at-once"></a>¿Cómo crear varias máquinas virtuales de hello misma plantilla a la vez?
Puede usar hello [VSTS tareas extensión](https://marketplace.visualstudio.com/items?itemName=ms-azuredevtestlabs.tasks) o [generar una plantilla de Azure Resource Manager](devtest-lab-add-vm.md#save-azure-resource-manager-template) al crear una máquina virtual y [implementar la plantilla de Azure Resource Manager Hola desde Windows PowerShell ](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="how-do-i-move-my-existing-azure-vms-into-my-azure-devtest-labs-lab"></a>¿Cómo se pueden mover las máquinas virtuales de Azure existentes a mi laboratorio de Azure DevTest Labs?
Siga estos pasos hello toocopy su tooAzure de máquinas virtuales existente laboratorios de desarrollo y pruebas:

1. Copiar el archivo del disco duro virtual de hello de la máquina virtual existente con este [script de Windows PowerShell](https://github.com/Azure/azure-devtestlab/blob/master/Scripts/CopyVHDFromVMToLab.ps1)
2. [Crear imagen personalizada hello](devtest-lab-create-template.md) dentro del laboratorio de prácticas de desarrollo y pruebas de Azure.
3. Crear una máquina virtual en el laboratorio de saludo de la imagen personalizada

## <a name="can-i-attach-multiple-disks-toomy-vms"></a>¿Puedo conectar varios discos toomy máquinas virtuales?
Se admite adjuntar tooVMs de varios discos.  

## <a name="if-i-want-toouse-a-windows-os-image-for-my-testing-do-i-have-toopurchase-an-msdn-subscription"></a>Si desea toouse una imagen de sistema operativo Windows para mi prueba, ¿tengo toopurchase una suscripción a MSDN?
Si tiene imágenes de sistema operativo cliente de Windows toouse (Windows 7 o posterior) para el desarrollo o pruebas en Azure, a continuación, en Sí, debe:

- [Adquirir una suscripción a MSDN](https://www.visualstudio.com/products/how-to-buy-vs).
- Si tiene un contrato Enterprise, cree una suscripción de Azure con hello [oferta Enterprise para desarrollo/pruebas](https://azure.microsoft.com/en-us/offers/ms-azr-0148p).

Para obtener más información acerca de hello créditos de Azure para cada oferta de MSDN, consulte [crédito de Azure mensual para los suscriptores de Visual Studio](https://azure.microsoft.com/en-us/pricing/member-offers/msdn-benefits-details/).

## <a name="how-do-i-automate-hello-process-of-uploading-vhd-files-toocreate-custom-images"></a>¿Cómo se automatiza el proceso de Hola de carga de imágenes personalizadas de toocreate de archivos de disco duro virtual?
Hay dos opciones:

* [AzCopy Azure](../storage/common/storage-use-azcopy.md#blob-upload) pueden toocopy usado o cargar la cuenta de almacenamiento de disco duro virtual archivos toohello asociada laboratorio Hola.
* [Explorador de almacenamiento de Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente que se ejecuta en Windows, OSX y Linux.   

cuenta de almacenamiento de destino toofind Hola asociado con el laboratorio, siga estos pasos:

1. Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
2. Seleccione **grupos de recursos** desde el panel izquierdo de Hola.
3. Busque y seleccione el grupo de recursos de hello asociado con el laboratorio.
4. En hello **Introducción** hoja, seleccione una de las cuentas de almacenamiento de Hola.
5. Seleccione **Blobs**.
6. Busque cargas en lista de Hola. Si no existe ninguno, devolver tooStep #4 e intente otra cuenta de almacenamiento.
7. Hola de uso **URL** como destino en el comando de AzCopy.

## <a name="how-can-i-automate-hello-process-of-deleting-all-hello-vms-in-my-lab"></a>¿Cómo puedo automatizar el proceso de hello de la eliminación de todas las máquinas virtuales de hello en mi laboratorio?
Por otra parte toodeleting máquinas virtuales en el laboratorio de hello portal de Azure, puede eliminar todas las máquinas virtuales de hello en el laboratorio mediante un script de PowerShell. Hola siguiente ejemplo, modificar valores de parámetro de hello en hello **toochange valores** comentario. Puede recuperar hello `subscriptionId`, `labResourceGroup`, y `labName` valores de hoja de laboratorio Hola Hola portal de Azure.

    # Delete all hello VMs in a lab

    # Values toochange
    $subscriptionId = "<Enter Azure subscription ID here>"
    $labResourceGroup = "<Enter lab's resource group here>"
    $labName = "<Enter lab name here>"

    # Login tooyour Azure account
    Login-AzureRmAccount

    # Select hello Azure subscription that contains hello lab. This step is optional
    # if you have only one subscription.
    Select-AzureRmSubscription -SubscriptionId $subscriptionId

    # Get hello lab that contains hello VMs toodelete.
    $lab = Get-AzureRmResource -ResourceId ('subscriptions/' + $subscriptionId + '/resourceGroups/' + $labResourceGroup + '/providers/Microsoft.DevTestLab/labs/' + $labName)

    # Get hello VMs from that lab.
    $labVMs = Get-AzureRmResource | Where-Object {
              $_.ResourceType -eq 'microsoft.devtestlab/labs/virtualmachines' -and
              $_.ResourceName -like "$($lab.ResourceName)/*"}

    # Delete hello VMs.
    foreach($labVM in $labVMs)
    {
        Remove-AzureRmResource -ResourceId $labVM.ResourceId -Force
    }

**Artefactos**
## <a name="what-are-artifacts"></a>¿Qué son los artefactos?
Los artefactos son elementos personalizables que pueden ser utilizado toodeploy los bits más recientes o el desarrollo de las herramientas en una máquina virtual. Son tooyour adjunto VM durante la creación con unos pocos pasos sencillos, y cuando se aprovisiona Hola VM, artefactos de hello implementación y configurar la máquina virtual. Hay diversos artefactos ya existentes en el [repositorio público de GitHub](https://github.com/Azure/azure-devtestlab/tree/master/Artifacts), pero también puede [crear sus propios artefactos](devtest-lab-artifact-author.md) fácilmente.


**Configuración del laboratorio**
## <a name="how-do-i-create-a-lab-from-an-azure-resource-manager-template"></a>¿Cómo se crea un laboratorio a partir de una plantilla de Azure Resource Manager?
Hemos preparado una [repositorio de GitHub de plantillas de Azure Resource Manager de laboratorio](https://aka.ms/dtlquickstarttemplate) que se puede implementar como-es o modificar toocreate plantillas personalizadas para los laboratorios. Cada una de estas plantillas tiene un vínculo que puede hacer clic en laboratorio de hello toodeploy como-está por debajo de su propia suscripción de Azure, o puede personalizar la plantilla de Hola y [implementar con PowerShell o CLI de Azure](../azure-resource-manager/resource-group-template-deploy.md).

## <a name="why-are-my-vms-created-in-different-resource-groups-with-arbitrary-names-can-i-rename-or-modify-these-resource-groups"></a>¿Por qué mis máquinas virtuales se crean en distintos grupos de recursos con nombres arbitrarios? ¿Se pueden modificar estos grupos de recursos o cambiar su nombre?
Grupos de recursos se crean así en orden para los equipos de toovirtual de acceso y permisos de usuario de laboratorios de desarrollo y pruebas de Azure toomanage Hola. Aunque puede mover el grupo de recursos de hello VM tooanother con el nombre que desee, al hacerlo no es recomendable. Estamos trabajando en la mejora esta experiencia tooallow más flexibilidad.   

## <a name="how-many-labs-can-i-create-under-hello-same-subscription"></a>¿Laboratorios cuántos puedo crear en hello misma suscripción?
No hay ningún límite específico en número de Hola de prácticas que se pueden crear por suscripción. Sin embargo, los recursos de hello utilizados son limitados por la suscripción. Puede leer sobre hello [cuotas y límites impuestos en las suscripciones de Azure](../azure-subscription-service-limits.md) y [cómo tooincrease estos límites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-many-vms-can-i-create-per-lab"></a>¿Cuántas máquinas virtuales se pueden crear por laboratorio?
No hay ningún límite específico en número de Hola de máquinas virtuales que se pueden crear por laboratorio. Sin embargo, los recursos de hello utilizados son limitados por la suscripción (por ejemplo, los núcleos VM, direcciones IP públicas, etcetera.). Puede leer sobre hello [cuotas y límites impuestos en las suscripciones de Azure](../azure-subscription-service-limits.md) y [cómo tooincrease estos límites](https://azure.microsoft.com/blog/azure-limits-quotas-increase-requests).

## <a name="how-do-i-share-a-direct-link-toomy-lab"></a>¿Cómo se puede compartir un laboratorio de toomy vínculo directo?
tooshare un vínculo directo a los usuarios de tooyour laboratorio, puede realizar Hola siguiendo el procedimiento:

1. Examinar toohello laboratorio Hola portal de Azure.
2. Copiar dirección URL de laboratorio de Hola desde el explorador y compartirlo con los usuarios de laboratorio.

> [!NOTE]
> Si los usuarios de laboratorio son los usuarios externos con un [cuenta Microsoft](#what-is-a-microsoft-account) y que no pertenecen a Active directory de la compañía tooyour, es posible que reciba un error al navegar por el vínculo de toohello proporcionado. Si recibe un error, indíqueles tooclick su nombre en la esquina superior derecha de Hola de Hola portal de Azure y el directorio de hello seleccione donde existe el laboratorio de Hola de hello **Directory** sección del menú de Hola.
>
>

## <a name="what-is-a-microsoft-account"></a>¿Qué es una cuenta Microsoft?
Una cuenta de Microsoft es lo que se utiliza para casi todo lo que hace con servicios y dispositivos de Microsoft. Es una dirección de correo electrónico y una contraseña que utilizas toosign en tooSkype, Outlook.com, OneDrive, Windows Phone y Xbox LIVE: significa que los archivos, fotografías, contactos y configuración puede seguir tooany dispositivo.

> [!NOTE]
> Cuenta de Microsoft usa toobe denominada "Windows Live ID".
>
>


**Solución de problemas**
## <a name="my-artifact-failed-during-vm-creation-how-do-i-troubleshoot-it"></a>Mi artefacto produjo errores durante la creación de la máquina virtual. ¿Cómo se soluciona este problema?
Consulte demasiado[cómo toodiagnose errores de artefactos en los laboratorios de desarrollo y pruebas](devtest-lab-troubleshoot-artifact-failure.md) toolearn modo tooobtain registra con respecto a los artefactos error.

## <a name="why-isnt-my-existing-virtual-network-saving-properly"></a>¿Por qué mi máquina virtual existente no se guarda correctamente?
Una posibilidad es que el nombre de la red virtual contenga puntos. Si es así, pruebe a quitar Hola puntos o reemplazarlos con guiones y vuelva a intentar guardar Hola red virtual de nuevo.

## <a name="why-do-i-get-a-parent-resource-not-found-error-when-provisioning-a-vm-from-powershell"></a>¿Por qué obtengo un error "No se encuentra el recurso primario" al aprovisionar una máquina virtual desde PowerShell?
Cuando un recurso es un recurso de tooanother primario, recurso primario de hello debe existir antes de crear el recurso de hello secundario. Si no existe, recibirá un error **ParentResourceNotFound**. Si no especifica una dependencia en el recurso primario de hello, recurso de hello secundario podría implementarse antes que la primaria de Hola.

Las máquinas virtuales son recursos secundarios en un laboratorio en un grupo de recursos. Cuando se usa Azure Resource Manager plantillas toodeploy a través de PowerShell, nombre de grupo de recursos de hello proporcionada en hello script de PowerShell debe ser nombre de grupo de recursos de Hola de laboratorio Hola. Para más información, vea, [Solución de errores comunes de implementación de Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-common-deployment-errors#parentresourcenotfound).

## <a name="where-can-i-find-more-error-information-if-a-vm-deployment-fails"></a>¿Dónde puedo encontrar más información sobre errores relativos a la implementación de VM?
Errores de implementación de máquina virtual se capturan en los registros de actividad de Hola. Puede encontrar registros de actividad de las máquinas virtuales a través de hello laboratorio **registros de auditoría** o **diagnóstico de máquina Virtual** en menú de recursos de hello en la hoja de máquinas virtuales del laboratorio de hello (hoja de hello muestra después de seleccionar Hola VM desde **Mis equipos virtuales** lista).

Error de implementación de Hola se produce en ocasiones, antes de que comience Hola implementación de VM - por ejemplo, cuando se supera el límite de la suscripción de Hola para un recurso creado con hello VM. En este caso, se capturan los detalles del error hello en el nivel de laboratorio hello **registros de actividad** que se puede buscar en parte inferior de Hola de hello **directivas y configuración** configuración. Para obtener más información sobre el uso de la actividad inicia sesión en Azure, consulte [vista actividad registra acciones de tooaudit en recursos](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-audit).

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]
