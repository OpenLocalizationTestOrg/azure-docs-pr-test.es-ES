---
title: "solución de problemas de pila de Azure aaaMicrosoft | Documentos de Microsoft"
description: "Solución de problemas de Azure Stack."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a20bea32-3705-45e8-9168-f198cfac51af
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: e274e92bc12fd6b7a2594f2f21b69ff0b9de594b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-stack-troubleshooting"></a>Solución de problemas de Microsoft Azure Stack
Este documento proporciona información para solucionar problemas comunes de Azure Stack. 

Como Hola Kit de desarrollo de técnicas de pila de Azure se ofrece como un entorno de evaluación, no hay ningún oficial de soporte técnico de servicios de soporte técnico de Microsoft.  Si experimenta un problema no documentado, que seguro Hola de toocheck [foro de MSDN de Azure pila](https://social.msdn.microsoft.com/Forums/azure/home?forum=azurestack) para obtener más ayuda e información.  

recomendaciones de Hola para solucionar los problemas que se describen en esta sección se derivan de varios orígenes y que pueden o no pueden resolver el problema en particular. Los ejemplos de código se proporcionan tal cual y no se pueden garantizar los resultados esperados. Esta sección está sujeto toofrequent modificaciones y se implementan las actualizaciones como producto toohello de mejoras.

## <a name="deployment"></a>Implementación
### <a name="deployment-failure"></a>Error de implementación
Si experimenta un error durante la instalación, puede usar el uso de hello vuelva a ejecutar la opción de implementación Hola implementación script toorestart Hola de hello paso con errores.  


### <a name="at-hello-end-of-hello-deployment-hello-powershell-session-is-still-open-and-doesnt-show-any-output"></a>Al final de Hola de implementación de hello, sesión de PowerShell de hello todavía está abierta y no muestra ningún resultado
Este comportamiento resulta probablemente solo Hola de comportamiento de saludo predeterminado de una ventana de comandos de PowerShell, cuando se ha seleccionado. implementación de kit de desarrollo de Hello realmente se ha realizado correctamente pero se pausó la secuencia de comandos de hello al seleccionar ventana hello. Puede comprobar que este es el caso de hello buscando palabra Hola "select" en hello barra de título de ventana de comandos de Hola.  Presione toounselect clave Hola ESC que y mensaje de bienvenida de finalización se deben mostrar después de él.

## <a name="templates"></a>Plantillas
### <a name="azure-template-wont-deploy-tooazure-stack"></a>Plantilla de Azure no implementarán tooAzure pila
Asegúrese de que:

* plantilla de Hello debe usar un servicio de Microsoft Azure que ya está disponible o en la vista previa en la pila de Azure.
* API que se usan para un recurso específico Hello se admiten una instancia local de pila de Azure de Hola y que tiene como destino una ubicación válida ("local" en el kit de desarrollo de pila de Azure, vs Hola "UU" o "India Sur" en Azure).
* Revisar [este artículo](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/README.md) acerca de los cmdlets de hello AzureRmResourceGroupDeployment de prueba, que detectar pequeñas diferencias en la sintaxis de Azure Resource Manager.

También puede utilizar plantillas de la pila de Azure de hello ya incluidas en hello [repositorio de GitHub](http://aka.ms/AzureStackGitHub/) toohelp empezar a trabajar.

## <a name="virtual-machines"></a>Máquinas virtuales
### <a name="default-image-and-gallery-item"></a>Elemento de la galería e imagen predeterminada
Antes de implementar máquinas virtuales en Azure Stack, primero debe agregar un elemento de la galería y una imagen de Windows Server.

### <a name="after-restarting-my-azure-stack-host-some-vms-may-not-automatically-start"></a>Después de reiniciar el host de Azure Stack, algunas máquinas virtuales podrían no iniciarse automáticamente.
Después de reiniciar el host, puede observar que los servicios de Azure Stack no están disponibles de inmediato.  Esto es porque la pila de Azure [infraestructura de máquinas virtuales](azure-stack-architecture.md#virtual-machine-roles) y RPs tardar un poco toocheck coherencia, pero finalmente se iniciará automáticamente.

También puede observar a ese inquilino que máquinas virtuales no se inician automáticamente tras un reinicio del host del kit de desarrollo de hello pila de Azure.  Esto es un problema conocido y solo requiere unos toobring requieren pasos manuales en línea:

1.  En el host de kit de desarrollo de Azure pila hello, inicie **Administrador de clústeres de conmutación por error** de hello menú Inicio.
2.  Clúster de hello seleccione **Cluster.azurestack.local S**.
3.  Seleccione **Roles**.
4.  Las máquinas virtuales del inquilino aparecerán en el estado *guardado*.  Una vez que se ejecutan todas las máquinas virtuales de infraestructura, haga clic en las máquinas virtuales de inquilinos de Hola y seleccione **iniciar** tooresume Hola máquina virtual.

### <a name="i-have-deleted-some-virtual-machines-but-still-see-hello-vhd-files-on-disk-is-this-behavior-expected"></a>Han eliminado algunas máquinas virtuales, pero seguir viendo los archivos de disco duro virtual de hello en el disco. ¿Es normal este comportamiento?
Sí, es normal. Se diseñó así porque:

* Al eliminar una máquina virtual, no se eliminan los discos duros virtuales. Los discos son recursos separados en el grupo de recursos de Hola.
* Cuando se elimina una cuenta de almacenamiento, eliminación de hello es visible inmediatamente a través de Azure Resource Manager (portal, PowerShell) pero discos Hola puede contener todavía se conservan en almacenamiento hasta que se ejecuta la recolección de elementos no utilizados.

Si ve "huérfanas" discos duros virtuales, es importante tooknow si forman parte de la carpeta de Hola para una cuenta de almacenamiento que se eliminó. Si no se eliminó la cuenta de almacenamiento de hello, es normal que siguen estando disponibles.

Puede leer más acerca de cómo configurar la recuperación de umbral y a petición de retención de hello en [administrar cuentas de almacenamiento](azure-stack-manage-storage-accounts.md).

## <a name="storage"></a>Storage
### <a name="storage-reclamation"></a>Recuperación de almacenamiento
Puede tardar horas toofourteen tooshow capacidad reclamado seguridad en el portal de Hola. La recuperación de espacio depende de diversos factores, como el porcentaje de uso de archivos de contenedor internos en el almacén de blobs de bloque. Por lo tanto, dependiendo de cuántos datos se eliminan, no hay ninguna garantía de cantidad de Hola de espacio que se recupera cuando se ejecuta el recolector de elementos no utilizados.

## <a name="powershell"></a>PowerShell
### <a name="resource-providers-not-registered"></a>Proveedores de recursos no registrados
Cuando se conecta tootenant suscripciones con PowerShell, observará ese recurso Hola proveedores no se registran automáticamente. Hola de uso [módulo Connect](https://github.com/Azure/AzureStack-Tools/tree/master/Connect), u Hola ejecución siguiente comando de PowerShell (después de [instalar y conectar](azure-stack-connect-powershell.md) como inquilino): 
  
       Get-AzureRMResourceProvider | Register-AzureRmResourceProvider

## <a name="cli"></a>CLI

* sólo el modo interactivo de Hello CLI Hola `az interactive` comando no se admite todavía en la pila de Azure.
* lista de hello tooget de imágenes de máquina virtual disponibles en la pila de Azure, use hello `az vm images list --all` comando en lugar de hello `az vm image list` comando. Hola especificando `--all` opción se asegura de que la respuesta devuelve solo imágenes de Hola que están disponibles en su entorno de pila de Azure. 
* Alias de la imagen de máquina virtual que están disponibles en Azure pueden no ser aplicable tooAzure pila. Al utilizar imágenes de máquina virtual, debe utilizar parámetro URN todo de hello (canónica: UbuntuServer:14.04.3-LTS:1.0.0) en lugar de alias de la imagen de Hola. Y este URNmust coinciden con las especificaciones de la imagen de hello como derivadas de hello `az vm images list` comando.
* De forma predeterminada, CLI 2.0 utiliza "Standard_DS1_v2" como el tamaño de la imagen de máquina virtual de Hola de forma predeterminada. Sin embargo, este tamaño no está todavía disponible en la pila de Azure, por lo tanto, necesita toospecify hello `--size` parámetro explícitamente al crear una máquina virtual. Puede obtener Hola lista de tamaños de máquina virtual que están disponibles en la pila de Azure mediante hello `az vm list-sizes --location <locationName>` comando.


## <a name="windows-azure-pack-connector"></a>Conector de Windows Azure Pack
* Si cambia Hola contraseña de cuenta de hello azurestackadmin después de implementar el kit de desarrollo de la pila de Azure, ya no se puede configurar el modo de varias nube. Por lo tanto, no será posible tooconnect toohello entorno de Windows Azure Pack de destino.
* Después de configurar el modo de varias nubes:
    * Un usuario puede ver el panel de hello solo después de que restablecen la configuración del portal Hola. (En el portal de usuarios de hello, haga clic en icono de configuración del portal de hello (icono de engranaje en la esquina superior derecha de hello). En **Restaurar la configuración predeterminada**, haga clic en **Aplicar**).
    * títulos de panel de Hello podrán no aparecer. Si se produce este problema, debe volver a agregarlos manualmente.
    * Pueden que algunos iconos no se muestren correctamente cuando se agrega por primera toohello panel. toofix este problema, Explorador de Hola de actualización.



