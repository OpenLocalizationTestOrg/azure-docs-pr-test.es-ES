---
title: "aaaAzure Site Recovery solución de problemas de errores y problemas de replicación de Azure en Azure | Documentos de Microsoft"
description: "Solución de problemas y errores al replicar máquinas virtuales de Azure para la recuperación ante desastres"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Solución de problemas de replicación de máquinas virtuales de Azure a Azure

En este artículo se describen los problemas comunes de hello en Azure Site Recovery al replicar y recuperación de máquinas virtuales de Azure desde una región tooanother otra y se explica cómo tootroubleshoot ellos. Para obtener más información sobre las configuraciones admitidas, vea hello [matriz de compatibilidad para la replicación de máquinas virtuales de Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Problemas de cuota de recursos de Azure (código de error 150097)
La suscripción debe ser habilitado toocreate máquinas virtuales de Azure en la región de destino de Hola que planea toouse como la región de recuperación ante desastres. Además, debe tener su suscripción suficiente cuota habilitado toocreate máquinas virtuales de tamaño específico. De forma predeterminada, selecciona de Site Recovery Hola mismo tamaño para el destino de hello VM como Hola una VM de origen. Si el tamaño de búsqueda de coincidencias de hello no está disponible, tamaño más cercano posible de hello, se seleccionará automáticamente. Si no hay ningún tamaño coincidente que admita la configuración de la máquina virtual de origen, aparece este mensaje de error:

**Código de error** | **Causas posibles:** | **Recomendación**
--- | --- | ---
150097<br></br>**Mensaje**: no se pudo habilitar la replicación para la máquina virtual de hello VmName. | -La suscripción de que no puede ser el Id. habilitado toocreate todas las máquinas virtuales en la ubicación de región de destino de Hola.</br></br>-El identificador de suscripción podría no estar habilitado o no tiene suficiente cuota toocreate específico VM los tamaños de ubicación de región de destino de Hola.</br></br>-Un tamaño de máquina virtual de destino adecuado que coincida con el origen de hello recuento de VM NIC (2) no se encuentra para el Id. de suscripción de hello en ubicación de región de destino de Hola.| Póngase en contacto con [soporte de facturación de Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable creación de VM para hello necesario tamaños de máquina virtual en la ubicación de destino de Hola para su suscripción. Una vez habilitada, Hola de reintento no pudo realizar la operación.

### <a name="fix-hello-problem"></a>Corrija el problema de Hola
Puede ponerse en contacto con [soporte de facturación de Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable su máquinas virtuales de tamaños necesarios en la ubicación de destino de hello toocreate de suscripción.

Si la ubicación de destino de hello tiene una restricción de capacidad, deshabilite la replicación y habilitarla tooa otra ubicación que su suscripción no tiene suficiente cuota toocreate máquinas virtuales de tamaños de hello necesario.

## <a name="trusted-root-certificates-error-code-151066"></a>Certificados raíz de confianza (código de error 151066)

Si todos los certificados raíz de confianza de la últimos hello no están presentes en hello VM, puede producir un error en el trabajo "Habilitar la replicación". Sin certificados hello, Hola autenticación y autorización de servicio de recuperación de sitio de llamadas de hello VM producirá un error. aparece el mensaje de error de Hola Hola error "Habilitar la replicación" sitio trabajo de recuperación:

**Código de error** | **Causa posible** | **Recomendaciones**
--- | --- | ---
151066<br></br>**Mensaje**: error de configuración de Site Recovery. | Hola requiere certificados raíz de confianza que se usan para la autorización y autenticación no están presentes en la máquina de Hola. | -Para una máquina virtual con sistema operativo de Windows de hello, asegúrese de que Hola confianza raíz certificados están presentes en la máquina de Hola. Para más información, consulte [Configurar raíces de confianza y certificados no permitidos](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Para una máquina virtual ejecuta el sistema operativo de Linux de hello, siga las instrucciones de Hola para los certificados raíz de confianza publicados por el distribuidor de versión de sistema operativo de Linux Hola.

### <a name="fix-hello-problem"></a>Corrija el problema de Hola
**Windows**

Instale todas las actualizaciones de Windows más recientes de hello en hello VM para que todos los certificados raíz de confianza de hello están presentes en la máquina de Hola. Si se encuentra en un entorno desconectado, siga proceso de actualización de Windows estándar de hello en los certificados de hello tooget de organización. Si Hola requiere certificados no están presentes en hello VM, Hola llamadas toohello servicio Site Recovery se producirá un error por motivos de seguridad.

Siga Hola habitual administración de actualizaciones de Windows o el proceso de administración de actualización de certificado en su tooget organización todos los certificados raíz más recientes de Hola y revocación de certificados de hello actualiza la lista de hello las máquinas virtuales.

tooverify que Hola problema se resuelve, vaya toologin.microsoftonline.com desde un explorador en la máquina virtual.

**Linux**

Siga las instrucciones de hello indicadas por los certificados de raíz de confianza más recientes de Linux distribuidor tooget hello y lista de revocación de certificado más reciente de hello en hello máquina virtual.

Dado que SuSE Linux utiliza vínculos simbólicos toomaintain una lista de certificados, siga estos pasos:

1.  Inicie sesión con un usuario raíz.

2.  Ejecute este comando:

      ``# cd /etc/ssl/certs``

3.  toosee si el certificado de CA raíz de hello Symantec está presente o no, ejecute este comando:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Si no se encuentra el archivo hello, ejecute estos comandos:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  un vínculo simbólico con b204d74a.0 toocreate -> VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem, ejecute este comando:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Compruebe toosee si este comando tiene Hola después de salida. Si no es así, tiene un vínculo simbólico toocreate:

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Si un vínculo simbólico 653b494a.0 no está presente, use este toocreate comando un vínculo simbólico:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Conectividad saliente para direcciones URL o intervalos IP de Site Recovery (código de error 151037 o 151072)

Para toowork de replicación de Site Recovery, se requiere de hello VM toospecific conectividad saliente intervalos de direcciones URL o una dirección IP. Si la máquina virtual está detrás de un firewall o utiliza conectividad saliente toocontrol de grupo (NSG) reglas de seguridad de red, es posible que vea uno de estos mensajes de error:

**Códigos de error** | **Causas posibles:** | **Recomendaciones**
--- | --- | ---
151037<br></br>**Mensaje**: no se pudo tooregister máquina virtual de Azure con Site Recovery. | -Está utilizando el acceso de salida de NSG toocontrol en VM de Hola y Hola necesario IP intervalos no están en la lista blanca de acceso de salida.</br></br>-Está usando herramientas de firewall de terceros y Hola necesarios intervalos IP o direcciones URL no están en la lista blanca.</br>| -Si está usando conectividad de red saliente de firewall proxy toocontrol en hello VM, asegúrese de que Hola direcciones URL de requisitos previos o intervalos IP del centro de datos están en la lista blanca. Para más información, consulte las [instrucciones sobre el proxy de firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Si está usando conectividad de red saliente de NSG reglas toocontrol en hello VM, asegúrese de que los intervalos IP de centro de datos de requisitos previos de hello son en la lista blanca. Para más información, consulte la [instrucciones para los grupos de seguridad de red](https://aka.ms/a2a-nsg-guidance).
151072<br></br>**Mensaje**: error de configuración de Site Recovery. | Conexión no puede ser establecida tooSite extremos de servicio de recuperación. | -Si está usando conectividad de red saliente de firewall proxy toocontrol en hello VM, asegúrese de que Hola direcciones URL de requisitos previos o intervalos IP del centro de datos están en la lista blanca. Para más información, consulte las [instrucciones sobre el proxy de firewall](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>-Si está usando conectividad de red saliente de NSG reglas toocontrol en hello VM, asegúrese de que los intervalos IP de centro de datos de requisitos previos de hello son en la lista blanca. Para más información, consulte la [instrucciones para los grupos de seguridad de red](https://aka.ms/a2a-nsg-guidance).

### <a name="fix-hello-problem"></a>Corrija el problema de Hola
toowhitelist [Hola requiere direcciones URL](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) o hello [necesario intervalos IP](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), siga los pasos de Hola Hola [documento de guía de red](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Disco no encontrado en la máquina de hello (código de error 150039)

Un nuevo disco conectado toohello que VM debe inicializarse.

**Código de error** | **Causas posibles:** | **Recomendaciones**
--- | --- | ---
150039<br></br>**Mensaje**: el disco de datos de Azure (DiskName) (DiskURI) con el número de unidad lógica (LUN) (LUNValue) no estaba asignado tooa disco correspondiente está informando de dentro de la máquina virtual que tiene Hola Hola mismo valor LUN. | -Un nuevo disco de datos se adjunta toohello VM, pero no se ha inicializado.</br></br>-disco de datos de hello dentro de hello VM no informa correctamente valor LUN de hello en qué Hola disco estaba adjunto toohello VM.| Asegúrese de que se inicializan los discos de datos de hello y, a continuación, vuelva a intentar la operación de Hola.</br></br>En Windows: [Adjunte e inicialice un disco nuevo](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>En Linux: [Inicialice un nuevo disco de datos en Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Corrija el problema de Hola
Asegúrese de que se hayan inicializado los discos de datos de Hola y, a continuación, vuelva a intentar la operación de hello:

- En Windows: [Adjunte e inicialice un disco nuevo](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- En Linux: [Inicialice un nuevo disco de datos en Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Si persiste el problema de hello, póngase en contacto con el soporte técnico.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Hola toosee no se puede VM de Azure para la selección en "Habilitar la replicación"

Puede que no vea su máquina virtual de Azure para seleccionarla en [Habilitar la replicación: paso 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Este problema podría ser debido a la configuración de Site Recovery toostale encendidos Hola VM de Azure. configuración obsoletos Hola podría quedar en una máquina virtual de Azure en hello casos siguientes:

- Había habilitado la replicación por hello Azure VM mediante el uso de Site Recovery y, a continuación, eliminar almacén de Site Recovery de hello sin deshabilitar explícitamente la replicación en hello máquina virtual.
- Había habilitado la replicación por hello Azure VM mediante el uso de Site Recovery y, a continuación, elimina el grupo de recursos de Hola que contiene el almacén de Site Recovery Hola sin deshabilitar explícitamente la replicación en hello VM.

### <a name="fix-hello-problem"></a>Corrija el problema de Hola

Puede usar [quitar el script de configuración de ASR obsoleto](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) y quitar la configuración de Site Recovery obsoleto de hello en hello VM de Azure. Debería ver Hola VM en [habilitar la replicación: paso 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) después de quitar la configuración obsoletos Hola.


## <a name="next-steps"></a>Pasos siguientes
[Replicación de máquinas virtuales de Azure](site-recovery-replicate-azure-to-azure.md)
