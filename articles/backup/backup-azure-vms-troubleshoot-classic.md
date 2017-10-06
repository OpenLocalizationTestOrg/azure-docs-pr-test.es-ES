---
title: "aaaTroubleshoot Azure errores en el portal clásico de copia de seguridad | Documentos de Microsoft"
description: "Solucionar problemas de copia de seguridad de Azure y la restauración de máquinas virtuales de Azure en el portal clásico de Hola."
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 117201fb-c0cd-4be4-b47f-abd88fe914cf
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 1/23/2017
ms.author: trinadhk;markgal;
ms.openlocfilehash: b9907f6fa57c631f5446c4d00f946a57c4efd72b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-virtual-machine-backup"></a>Solución de problemas de copia de seguridad de máquinas virtuales de Azure
> [!div class="op_single_selector"]
> * [Almacén de Servicios de recuperación](backup-azure-vms-troubleshoot.md)
> * [Almacén de copia de seguridad](backup-azure-vms-troubleshoot-classic.md)
>
>

Puede solucionar los errores detectados mientras mediante copia de seguridad de Azure con información aparece en hello tabla siguiente.

## <a name="discovery"></a>Detección
| Operación de copia de seguridad | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Detección |No se pudo toodiscover nuevos elementos - copia de seguridad de Microsoft Azure encontró y error interno. Espere unos minutos y vuelva a intentar la operación de Hola de nuevo. |Vuelva a intentar el proceso de detección de hello transcurridos 15 minutos. |
| Detección |No se pudo toodiscover nuevos elementos: detección de otra operación ya está en curso. Espere hasta que haya completado la operación de detección de hello actual. |None |

## <a name="register"></a>Registro
| Operación de copia de seguridad | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Registro |Número de discos de datos adjuntos límite de hello admitida la máquina virtual superado toohello: Desconecte algunos discos de datos en esta operación de Hola de máquina virtual y vuelva a intentarlo. Azure es compatible con copia de seguridad los discos de datos de too16 adjunta tooan máquina virtual de Azure para copia de seguridad |None |
| Registro |Copia de seguridad de Microsoft Azure encontró un error interno: espere unos minutos y vuelva a intentar la operación de Hola de nuevo. Si persiste el problema de hello, póngase en contacto con Microsoft Support. |Puede obtener este error debido a tooone de hello siguientes no admite configuración de máquina virtual en LRS Premium. <br> Se puede realizar copia de seguridad de las máquinas virtuales de almacenamiento premium mediante el almacén de servicios de recuperación. [Más información](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup) |
| Registro |Se ha producido un error en el registro porque se ha agotado el tiempo de espera de la operación de instalación del agente. |Compruebe si se admite la versión de SO de Hola de máquina virtual de Hola. |
| Registro |Error en la ejecución de comando: hay otra operación en curso en este elemento. Espere hasta que se complete la operación anterior de Hola |None |
| Registro |No se pueden usar máquinas virtuales con discos duros virtuales almacenados en Almacenamiento Premium para realizar copias de seguridad |None |
| Registro |Agente de máquina virtual no está presente en la máquina virtual de hello: instale Hola requisito previo, agente de máquina virtual y reinicie la operación de Hola. |[Obtenga más](#vm-agent) sobre la instalación de agente VM y cómo toovalidate Hola instalación del agente de máquina virtual. |

## <a name="backup"></a>Backup
| Operación de copia de seguridad | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Backup |No se pudo comunicar con el agente de máquina virtual de hello para el estado de la instantánea. La subtarea de VM instantánea agotó el tiempo de espera. -Vea solución de problemas de hello guía sobre cómo tooresolve esto. |Este error se produce si hay un problema con el agente de máquina virtual de Hola o toohello de acceso de red infraestructura de Azure está bloqueada de alguna manera. Aprenda más sobre cómo [depurar los problemas de las instantáneas de la máquina virtual](backup-azure-troubleshoot-vm-backup-fails-snapshot-timeout.md). <br> Si el agente de máquina virtual de hello no está causando problemas, a continuación, reinicie Hola máquina virtual. Hay veces en un estado incorrecto de la máquina virtual puede causar problemas y reiniciar Hola VM restablece esta "mal estado" |
| Backup |Error de copia de seguridad a un error interno: vuelva a intentar la operación de hello en unos minutos. Si persiste el problema de hello, póngase en contacto con Microsoft Support |Compruebe si hay un problema transitorio en el acceso al almacenamiento de máquinas virtuales. Compruebe [estado de Azure](https://azure.microsoft.com/en-us/status/) toosee si no hay ningún emitir relacionado toocompute / / red de almacenamiento en región de hello en curso. Por favor, se mitiga el problema de reintento Hola post de copia de seguridad. |
| Backup |No se pudo realizar la operación de hello como máquina virtual ya no existe. |No se puede realizar la copia de seguridad como hello VM configurada para copia de seguridad se ha eliminado. Detenga más copias de seguridad va tooProtected elementos vista, seleccione el elemento protegido y haga clic en detener la protección. Puede conservar los datos seleccionando la opción correspondiente. Más adelante, puede reanudar la protección de esta máquina virtual haciendo clic en Configurar la protección en la vista de elementos registrados. |
| Backup |Error tooinstall Hola extensión de servicios de recuperación de Azure en el elemento seleccionado de hello - agente de máquina virtual es un requisito previo para la extensión de servicios de recuperación de Azure. Instale a agente de máquina virtual de Azure de Hola y reinicie la operación de registro de hello |<ol> <li>Compruebe si se ha instalado correctamente el agente de máquina virtual de Hola. <li>Asegúrese de que Hola marca en la configuración de VM de Hola se ha establecido correctamente.</ol> [Obtenga más](#validating-vm-agent-installation) sobre la instalación de agente VM y cómo toovalidate Hola instalación del agente de máquina virtual. |
| Backup |Error en la ejecución del comando: otra operación está actualmente en curso en este elemento. Espere hasta que se complete la operación anterior de hello y, a continuación, vuelva a intentar |Se ejecuta un trabajo de copia de seguridad o restauración existente para hello VM y no se puede iniciar un nuevo trabajo mientras se ejecuta el trabajo existente de Hola. |
| Backup |Error en la instalación de la extensión con error de Hola "COM + no tootalk no se puede toohello Microsoft Distributed Transaction Coordinator |Normalmente, esto significa que no se está ejecutando el servicio COM + Hola. Para obtener ayuda acerca de cómo solucionar este problema, póngase en contacto con el servicio de soporte técnico de Microsoft. |
| Backup |Operación de instantánea no pudo con hello error de operación de VSS "esta unidad está bloqueada por el cifrado de unidad BitLocker. Debe desbloquear esta unidad en el Panel de Control. |Desactivar BitLocker para todas las unidades de VM de hello y observe si se ha resuelto el problema VSS de Hola |
| Backup |No se pueden usar máquinas virtuales con discos duros virtuales almacenados en Almacenamiento Premium para realizar copias de seguridad |None |
| Copia de seguridad |Máquina virtual de Azure no encontrada. |Esto sucede cuando hello máquina virtual principal se elimina, pero continúa de directiva de copia de seguridad de hello toolook para una copia de seguridad de máquina virtual tooperform. toofix este error: <ol><li>Volver a crear la máquina virtual de hello con hello mismo nombre y el mismo nombre de grupo de recursos [nombre del servicio en la nube,] <br>O BIEN <li> Desactive la protección para esta máquina virtual para que no se desencadenen las copias de seguridad subsiguientes. </ol> |
| Backup |Agente de máquina virtual no está presente en la máquina virtual de hello: instale Hola requisito previo, agente de máquina virtual y reinicie la operación de Hola. |[Obtenga más](#vm-agent) sobre la instalación de agente VM y cómo toovalidate Hola instalación del agente de máquina virtual. |

## <a name="jobs"></a>Trabajos
| Operación | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Cancelar trabajo |No se admite la cancelación para este tipo de trabajo: espere hasta que se complete el trabajo de Hola. |None |
| Cancelar trabajo |trabajo de Hello no está en un estado cancelable: espere hasta que se complete el trabajo de Hola. <br>OR<br> trabajo de Hello seleccionado no está en un estado cancelable: espere hello toocomplete de trabajo. |Con toda probabilidad, prácticamente se complete el trabajo de hello; Espere hasta que se complete el trabajo de Hola |
| Cancelar trabajo |No se puede cancelar el trabajo de hello porque no está en curso: solo se admite la cancelación en los trabajos que están en curso. Intente cancelar un trabajo que esté en curso. |Esto sucede debido a los estados transitorios tooa. Espere un minuto y vuelva a intentar la operación de cancelación Hola |
| Cancelar trabajo |Error toocancel Hola trabajo: espere hasta que finalice el trabajo. |None |

## <a name="restore"></a>Restauración
| Operación | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Restauración |Error en la restauración con error interno de nube |<ol><li>Toowhich de servicio de nube que está tratando de toorestore está configurado con la configuración de DNS. Puede consultar  <br>$deployment = Get-AzureDeployment -ServiceName "ServiceName" -Slot "Production"     Get-AzureDns -DnsSettings $deployment.DnsSettings<br>Si hay una dirección configurada, significa que se ha configurado DNS.<br> <li>Está tratando de nube servicio toowhich tooyou toorestore está configurado con la dirección IP reservada y las máquinas virtuales existentes del servicio en nube están en estado detenido.<br>Puede comprobar que un servicio en la nube tiene una IP reservada utilizando los siguientes cmdlets de PowerShell:<br>$deployment = Get-AzureDeployment -ServiceName "servicename" -Slot "Production" $dep.ReservedIPName <br><li>Está intentando toorestore una máquina virtual con las siguientes configuraciones de red especiales toosame del servicio en nube. <br>- Máquinas virtuales con la configuración del equilibrador de carga (interna y externa)<br>- Máquinas virtuales con varias direcciones IP reservadas<br>- Máquinas virtuales con varias NIC<br>Seleccione un nuevo servicio de nube en la interfaz de usuario de Hola o consulte demasiado[consideraciones de restauración](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations) para las máquinas virtuales con las configuraciones de red especiales</ol> |
| Restauración |nombre DNS de Hello seleccionado ya está en uso: especificar un nombre DNS diferente y vuelva a intentarlo. |Hello DNS nombre aquí hace referencia el nombre del servicio de nube toohello (normalmente terminan con. cloudapp.net). Esto es necesario toobe único. Si se produce este error, debe toochoose otro nombre de VM durante la restauración. <br><br> Este error se muestra solo toousers de hello portal de Azure. Hello operación de restauración a través de PowerShell se realiza correctamente porque solo restaura discos hello y no crea Hola máquina virtual. error de Hola se enfrentará cuando Hola máquinas virtuales se crea explícitamente por parte del usuario después de la operación de restauración de disco de Hola. |
| Restauración |Hola configuración de red virtual especificada no es correcta: especifique una configuración de red virtual diferente y vuelva a intentarlo. |None |
| Restauración |Hola especificado usa una dirección IP reservada, que no coincide con la configuración de Hola de máquina virtual de Hola que se están restaurando: especifique un servicio de nube diferente que no use una dirección IP reservada o elija otro toorestore de punto de recuperación de servicio en la nube. |None |
| Restauración |Servicio de nube ha alcanzado el límite del número de puntos de entrada final - operación de reintento de hello mediante la especificación de un servicio de nube diferente o mediante un extremo existente. |None |
| Restauración |Cuenta de almacenamiento de almacén y de destino de copia de seguridad se encuentran en dos regiones diferentes: asegúrese de que la cuenta de almacenamiento de hello especificada en la operación de restauración es Hola misma región de Azure como almacén de copia de seguridad de Hola. |None |
| Restauración |Cuenta de almacenamiento especificada para la operación de restauración de hello no es admitida - cuentas de almacenamiento solo básico o estándar con redundancia local o se admite la configuración de replicación con redundancia geográfica. Seleccione una cuenta de almacenamiento compatible |None |
| Restauración |Tipo de cuenta de almacenamiento especificada para la operación de restauración no está en línea: asegúrese de que la cuenta de almacenamiento de hello especificada en la operación de restauración está en línea |Esto puede ocurrir debido a un error transitorio en el almacenamiento de Azure o pagar tooan interrupción. Elija otra cuenta de almacenamiento. |
| Restauración |Ha alcanzado la cuota de grupo de recursos: elimine algunos grupos de recursos desde el portal de Azure o póngase en contacto con soporte técnico de Azure tooincrease Hola límites. |None |
| Restauración |La subred seleccionada no existe: seleccione una subred que exista |None |

## <a name="policy"></a>Directiva
| Operación | Detalles del error | Solución alternativa |
| --- | --- | --- |
| Creación de directiva |Error de directiva de Hola toocreate: reduzca hello toocontinue de opciones de retención con la configuración de directiva. |None |

## <a name="vm-agent"></a>Agente de máquina virtual
### <a name="setting-up-hello-vm-agent"></a>Cómo configurar Hola agente de máquina virtual
Por lo general, Hola agente de máquina virtual ya está presente en las máquinas virtuales que se crean a partir de hello Galería de Azure. Sin embargo, las máquinas virtuales que se migran desde los centros de datos local no tendrán Hola agente de VM instalado. Para que estas máquinas virtuales, Hola agente de máquina virtual debe toobe instalado explícitamente. Obtenga más información sobre [instalar agente de máquina virtual de hello en una máquina virtual existente](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx).

Para las máquinas virtuales de Windows:

* Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesitará la instalación de Hola de toocomplete de privilegios de administrador.
* [Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado.

Máquinas virtuales de Linux:

* Instale el [Agente de Linux](https://github.com/Azure/WALinuxAgent) desde Github.
* [Actualizar la propiedad de la máquina virtual de hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate que Hola agente está instalado.

### <a name="updating-hello-vm-agent"></a>Actualizar Hola agente de máquina virtual
Para las máquinas virtuales de Windows:

* Hola actualización de agente de máquina virtual es tan sencillo como Hola reinstalación [archivos binarios del agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Sin embargo, deberá tooensure que no se está ejecutando ninguna operación de copia de seguridad al Hola que agente de máquina virtual se está actualizando.

Máquinas virtuales de Linux:

* Siga las instrucciones de hello en [actualizar el agente de máquina virtual de Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

### <a name="validating-vm-agent-installation"></a>Validación de la instalación del agente de la máquina virtual
¿Cómo toocheck para Hola versión del agente de máquina virtual en máquinas virtuales de Windows:

1. Inicie sesión en toohello máquina virtual de Azure y desplazarse por las carpetas de toohello *C:\WindowsAzure\Packages*. Debería encontrar Hola WaAppAgent.exe archivo.
2. Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** campo de versión del producto de Hola de ficha debe ser 2.6.1198.718 o superior
