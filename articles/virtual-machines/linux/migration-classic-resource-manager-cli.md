---
title: "máquinas virtuales de aaaMigrate tooResource administrador mediante la CLI de Azure | Documentos de Microsoft"
description: "Este artículo le guía a través de migración de hello admitida por la plataforma de recursos de tooAzure clásico Administrador de recursos mediante CLI de Azure"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d6f5a877-05b6-4127-a545-3f5bede4e479
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: 0b11f4bb1b4658b3e88bf7629147ed953b678556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-cli"></a>Migrar recursos de IaaS de tooAzure clásico Administrador de recursos mediante la CLI de Azure
Estos pasos muestra cómo toouse interfaz de línea de comandos (CLI) de Azure comandos toomigrate infraestructura como un recurso de servicio (IaaS) de modelo de implementación de Azure Resource Manager de toohello modelo de implementación clásica de Hola. artículo de Hello requiere hello [CLI de Azure](../../cli-install-nodejs.md).

> [!NOTE]
> Todas las operaciones de hello descritas aquí son idempotentes. Si tiene un problema que no sea una característica no compatible o un error de configuración, se recomienda que vuelva a intentar Hola preparar, anular o confirmar la operación. plataforma de Hola, a continuación, intentará volver a la acción de Hola.
> 
> 

<br>
Este es un orden de hello tooidentify de diagrama de flujo en el que es necesario pasos toobe ejecutado durante un proceso de migración

![Captura de pantalla que muestra los pasos de migración de Hola](../windows/media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-prepare-for-migration"></a>Paso 1: Preparación para la migración
Estas son algunas prácticas recomendadas que se recomienda evaluar migrar recursos de IaaS de tooResource clásico Manager:

* Lea hello [lista de configuraciones no admitidas o características](../windows/migration-classic-resource-manager-overview.md). Si tiene máquinas virtuales que usan configuraciones no admitidas o características, se recomienda que espere Hola característica/Configuración compatibilidad toobe anunciada. Como alternativa, puede quitar esa característica o salir de que la migración de configuración tooenable si se adapte a sus necesidades.
* Si han automatizado las secuencias de comandos que implementan la infraestructura y las aplicaciones de hoy en día, intente toocreate un programa de instalación de prueba similar con esos scripts para la migración. Como alternativa, puede configurar entornos de ejemplo mediante el uso de hello portal de Azure.

> [!IMPORTANT]
> Las puertas de enlace de la aplicación no se admiten actualmente para la migración de clásico tooResource Manager. toomigrate una red virtual clásica con una puerta de enlace de aplicaciones, quitar la puerta de enlace de hello antes de ejecutar una red de Hola de toomove de operación de preparación. Después de completar la migración de hello, vuelva a conectar la puerta de enlace de hello en el Administrador de recursos de Azure. 
>
>Conectar los circuitos tooExpressRoute en otra suscripción de puertas de enlace de ExpressRoute no se pueden migrar automáticamente. En tales casos, quite la puerta de enlace de ExpressRoute de hello, migrar la red virtual de Hola y vuelva a puerta de enlace de Hola. Vea [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../../expressroute/expressroute-migration-classic-resource-manager.md) para obtener más información.
> 
> 

## <a name="step-2-set-your-subscription-and-register-hello-provider"></a>Paso 2: Establecer la suscripción y registrar proveedor de Hola
Para escenarios de migración, necesita tooset del entorno para ambos clásico y Administrador de recursos. [Instale la CLI de Azure](../../cli-install-nodejs.md) y [seleccione la suscripción](../../xplat-cli-connect.md).

Cuenta de inicio de sesión tooyour.

    azure login

Seleccione Hola suscripción de Azure usando el siguiente comando de Hola.

    azure account set "<azure-subscription-name>"

> [!NOTE]
> El registro está paso de una sola vez pero necesita toobe realiza una vez antes de intentar la migración. Sin registrar verá Hola siguiente mensaje de error 
> 
> *BadRequest: Subscription is not registered for migration* (BadRequest: la suscripción no está registrada para la migración) 
> 
> 

Registrar con el proveedor de recursos de migración de hello mediante Hola siguiente comando. Tenga en cuenta que, en algunos casos, se agota el tiempo de espera de este comando. Sin embargo, el registro de hello será correcto.

    azure provider register Microsoft.ClassicInfrastructureMigrate

Espere cinco minutos para toofinish de registro de hello. Puede comprobar el estado de Hola de aprobación de hello usando el siguiente comando de Hola. Asegúrese de que RegistrationState sea `Registered` antes de continuar.

    azure provider show Microsoft.ClassicInfrastructureMigrate

Ahora cambie CLI toohello `asm` modo.

    azure config mode asm

## <a name="step-3-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Paso 3: Asegúrese de que tiene suficientes núcleos de máquina Virtual de Azure Resource Manager Hola región de Azure de su implementación actual o la red virtual
Para este paso deberá tooswitch demasiado`arm` modo. Hacer esto con el siguiente comando de Hola.

```
azure config mode arm
```

Puede usar Hola después CLI comando toocheck Hola cantidad actual de núcleos que tiene en el Administrador de recursos de Azure. toolearn más información acerca de las cuotas de núcleo, consulte [hello Azure Resource Manager y límites](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager)

```
azure vm list-usage -l "<Your VNET or Deployment's Azure region"
```

Una vez que haya terminado comprobar este paso, puede volver cambiar demasiado`asm` modo.

    azure config mode asm


## <a name="step-4-option-1---migrate-virtual-machines-in-a-cloud-service"></a>Paso 4: Opción 1: Migración de máquinas virtuales de un servicio en la nube
Hola obtención de una lista de servicios en la nube mediante el uso de hello siguiente comando y, a continuación, servicio de nube de Hola de selección que desea toomigrate. Tenga en cuenta que si hello las máquinas virtuales en el servicio de nube de Hola se encuentran en una red virtual o si tienen roles web y de trabajo, obtendrá un mensaje de error.

    azure service list

Ejecute hello siguientes comando tooget Hola nombre de la implementación de servicio en la nube Hola de resultados detallados de Hola. En la mayoría de los casos, nombre de la implementación de hello es Hola igual que el nombre del servicio de nube de Hola.

    azure service show <serviceName> -vv

En primer lugar, validar si puede migrar servicio en la nube hello mediante Hola siguientes comandos:

```shell
azure service deployment validate-migration <serviceName> <deploymentName> new "" "" ""
```

Preparar las máquinas virtuales de Hola Hola del servicio en nube para la migración. Tiene dos toochoose de opciones de.

Si desea toomigrate Hola máquinas virtuales tooa plataforma red virtual creada, utilice Hola siguiente comando.

    azure service deployment prepare-migration <serviceName> <deploymentName> new "" "" ""

Si desea tooan toomigrate existente de la red virtual en el modelo de implementación del Administrador de recursos de hello, utilice Hola siguiente comando.

    azure service deployment prepare-migration <serviceName> <deploymentName> existing <destinationVNETResourceGroupName> <subnetName> <vnetName>

Después de preparar Hola operación se realiza correctamente, puede buscar a través de estado de migración de hello resultados detallados tooget Hola de hello las máquinas virtuales y asegúrese de que se encuentran en hello `Prepared` estado.

    azure vm show <vmName> -vv

Comprobar la configuración de Hola para hello preparado recursos con CLI u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.

    azure service deployment abort-migration <serviceName> <deploymentName>

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.

    azure service deployment commit-migration <serviceName> <deploymentName>



## <a name="step-4-option-2----migrate-virtual-machines-in-a-virtual-network"></a>Paso 4: Opción 2: Migración de máquinas virtuales de una red virtual
Selección Hola red virtual que desea toomigrate. Tenga en cuenta que si la red virtual de hello contiene roles web y de trabajo o máquinas virtuales con las configuraciones no compatibles, obtendrá un mensaje de error de validación.

Obtener todas las redes virtuales de hello en la suscripción de hello mediante Hola siguiente comando.

    azure network vnet list

salida de Hello tendrá un aspecto similar al siguiente:

![Captura de pantalla de línea de comandos de hello con el nombre de toda la red virtual de hello resaltado.](../media/virtual-machines-linux-cli-migration-classic-resource-manager/vnet.png)

Hola ejemplo anterior, Hola **virtualNetworkName** es el nombre completo de hello **"Grupo classicubuntu16 classicubuntu16"**.

En primer lugar, validar si se puede migrar la red virtual de hello con hello siguiente comando:

```shell
azure network vnet validate-migration <virtualNetworkName>
```

Prepare la red virtual de Hola de su elección para la migración mediante Hola siguiente comando.

    azure network vnet prepare-migration <virtualNetworkName>

Comprobar la configuración de Hola para hello preparado las máquinas virtuales con CLI u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.

    azure network vnet abort-migration <virtualNetworkName>

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.

    azure network vnet commit-migration <virtualNetworkName>

## <a name="step-5-migrate-a-storage-account"></a>Paso 5: Migración de una cuenta de almacenamiento
Una vez que haya terminado la migración de máquinas virtuales hello, se recomienda que migre la cuenta de almacenamiento de Hola.

Preparar la cuenta de almacenamiento de Hola migración utilizando el siguiente comando de Hola

    azure storage account prepare-migration <storageAccountName>

Comprobar la configuración de Hola para hello preparado cuenta de almacenamiento con CLI u Hola portal de Azure. Si no está listo para la migración y desea que el estado anterior de toogo toohello atrás, usar hello siguiente comando.

    azure storage account abort-migration <storageAccountName>

Si configuración preparada hello es correcto, puede desplazarse hacia delante y confirmar recursos Hola usando el siguiente comando de Hola.

    azure storage account commit-migration <storageAccountName>

## <a name="next-steps"></a>Pasos siguientes

* [Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate desde tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Revisión de los errores más comunes en la migración](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
