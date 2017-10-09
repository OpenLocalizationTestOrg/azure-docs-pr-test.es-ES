---
title: "aaaSet seguridad Hola origen y de destino para el sitio secundario tooa de Hyper-V replicación con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooset una copia de seguridad origen Hola y de destino cuando la replicación de máquinas virtuales de Hyper-V toosecondary VMM del sitio con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: fa7809f1-7633-425f-b25d-d10d004e8d0b
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 451cb4413ca5c09777a7faf512b1c8ea43e695f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-hello-replication-source-and-target"></a>Paso 6: Configurar origen de replicación de Hola y de destino


Después de crear servicios de recuperación de un almacén para Hyper-V replicación tooa sitio VMM secundario con [Azure Site Recovery](site-recovery-overview.md), use este artículo tooset el origen de Hola y ubicaciones de replicación de destino. 

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Instale hello Azure Site Recovery Provider en servidores VMM y detectar y registrar los servidores en el almacén de Hola.

1. Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/goals-source.png)
2. En **preparar origen**, haga clic en **+ VMM** tooadd un servidor VMM.

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source1.png)
3. En **Agregar servidor**, compruebe que **servidor de System Center VMM** aparece en **tipo de servidor** y ese servidor VMM Hola cumple hello [requisitos previos](#prerequisites).
4. Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.
5. Descargue la clave de registro de hello. Se le solicitará cuando ejecute el programa de instalación. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/vmm-to-vmm-walkthrough-source-target/set-source3.png)
6. Instale hello Azure Site Recovery Provider en servidor VMM de Hola. No es necesario tooexplicitly ninguna instalación adicional en los servidores de host de Hyper-V.


## <a name="install-hello-azure-site-recovery-provider"></a>Instalar hello Azure Site Recovery Provider

1. Ejecute el archivo de configuración de proveedor de hello en cada servidor VMM. Si VMM está implementado en un clúster, siguiente Hola Hola primera vez que instale:
    -  Instalar el proveedor de hello en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola.
    - A continuación, instale Hola proveedor en hello otros nodos. Los nodos del clúster deben ejecutarse todos Hola misma versión de Hola proveedor.
2. El programa de instalación ejecuta algunas comprobaciones de requisitos previos y las solicitudes de servicio VMM de permiso toostop Hola. Hola servicio VMM se reiniciará automáticamente cuando finaliza el programa de instalación. Si instala en un clúster VMM, está el rol de clúster de hello toostop solicitadas.
3. En **Microsoft Update**, puede participar en toospecify que están instaladas las actualizaciones del proveedor con arreglo a la directiva de Microsoft Update.
4. En **instalación**, acepte o modifique la ubicación de instalación predeterminada de Hola y haga clic en **instalar**.

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-location.png)
5. Una vez completada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![Ubicación de instalación](./media/vmm-to-vmm-walkthrough-source-target/provider-register.png)
6. En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor. Haga clic en *Siguiente*.

    ![Registro de servidor](./media/vmm-to-vmm-walkthrough-source-target/vaultcred.png)
7. En **conexión a Internet**, especifique cómo se proveedor Hola que se ejecuta en el servidor VMM Hola conecta tooAzure.

    ![Configuración de Internet](./media/vmm-to-vmm-walkthrough-source-target/proxydetails.png)

   - Puede especificar ese proveedor Hola debe conectarse directamente toohello internet, o a través de un servidor proxy.
   - Especifique la configuración de proxy si es necesario.
   - Si usa un proxy, una cuenta de ejecución de VMM (DRAProxyAccount) se crea automáticamente con hello especificada las credenciales del proxy. Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente. Hello configuración de la cuenta de ejecución puede modificarse en la consola VMM hello > **configuración** > **seguridad** > **cuentas de ejecución**. Reinicie los cambios de tooupdate de servicio VMM Hola.
8. En **clave de registro**, seleccione clave de Hola que descargó desde Azure Site Recovery y copió toohello servidor VMM.
9. configuración de cifrado de Hello sólo se utiliza al replicar las máquinas virtuales de Hyper-V en tooAzure de nubes VMM. Si replica tooa de sitio secundario no se utiliza.
10. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster especificar nombre de rol de clúster VMM Hola.
11. En **sincronizar metadatos de nube**, seleccione si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola.
12. Haga clic en **siguiente** toocomplete proceso de Hola. Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. servidor Hola se muestra en hello **servidores VMM** ficha en hello **servidores** página en el almacén de Hola.

    ![Server](./media/vmm-to-vmm-walkthrough-source-target/provider13.png)
13. Después de hello servidor está disponible en la consola de Site Recovery hello, en **origen** > **preparar origen** seleccione servidor VMM de Hola y en qué Hola Hyper-V host se encuentra en la nube Hola select. y, a continuación, haga clic en **Aceptar**.

También puede instalar el proveedor de Hola desde línea de comandos de hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Seleccione en la nube y el servidor VMM de destino de hello:

1. Haga clic en **preparar infraestructura** > **destino**y el servidor VMM de destino Hola seleccione desea toouse.
2. Se mostrarán las nubes en el servidor de Hola que se sincronizan con Site Recovery. Seleccione la nube de destino de Hola.

   ![Destino](./media/vmm-to-vmm-walkthrough-source-target/target-vmm.png)



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 7: configurar la asignación de red](vmm-to-vmm-walkthrough-network-mapping.md).
