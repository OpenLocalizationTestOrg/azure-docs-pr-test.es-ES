---
title: "aaaSet una directiva de replicación para tooa de sitio secundario con Azure Site Recovery para la replicación Hyper-V | Documentos de Microsoft"
description: "Describe cómo tooset una directiva para la máquina virtual de Hyper-V replicación tooa sitio de VMM secundario con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5d9b79cf-89f2-4af9-ac8e-3a32ad8c6c4d
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 6d008e3bb3fa0b666e91678cf6de3693dd712ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy"></a>Paso 8: Configurar una directiva de replicación

Después de configurar [asignación de red](vmm-to-vmm-walkthrough-network-mapping.md), use este tooset artículo una directiva de replicación de Hyper-V máquina virtual (VM) replicación tooa sitio secundario, con [Azure Site Recovery](site-recovery-overview.md).

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="before-you-start"></a>Antes de comenzar

- Cuando se crea una directiva de replicación, todos los hosts mediante la directiva de hello debe haber Hola mismo sistema operativo. Hola nube de VMM puede contener hosts de Hyper-V que ejecutan versiones distintas de Windows Server, pero en este caso, se necesitan varias directivas de replicación.
- Puede realizar Hola la replicación inicial sin conexión.

## <a name="configure-replication-settings"></a>Configuración de las opciones de replicación

1. toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/vmm-to-vmm-walkthrough-replication/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva. Hello tipo de origen y de destino debe ser **Hyper-V**.
3. En **versión de host de Hyper-V**, seleccione el sistema operativo que se ejecuta en el host de Hola.
4. En **tipo de autenticación** y **puerto de autenticación**, especifique cómo se autentica el tráfico entre Hola principal y los servidores de host de Hyper-V de recuperación. Seleccione **Certificado** , a menos que tenga un entorno Kerberos activo. Azure Site Recovery configurará automáticamente los certificados para la autenticación de HTTPS. No es necesario toodo nada manualmente. De forma predeterminada, los puertos 8083 y 8084 (para certificados) se abrirá en Hola Firewall de Windows en los servidores de host de Hyper-V de Hola. Si selecciona **Kerberos**, se usará un vale de Kerberos para la autenticación mutua de los servidores de host de Hola. Observe que esta configuración solo es pertinente para servidores host de Hyper-V que se ejecutan en Windows Server 2012 R2.
5. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).
6. En **retención de punto de recuperación**, especifique en horas cuánto va un período de retención Hola para cada punto de recuperación. Equipos protegidos pueden ser recuperado tooany punto dentro de una ventana.
7. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola. Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. Si habilita las instantáneas coherentes con la aplicación, afectará al rendimiento de Hola de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.
8. En **Compresión de transferencia de datos**, especifique si se deben comprimir los datos replicados que se transfieren.
9. Seleccione **Eliminar réplica VM**, toospecify que Hola máquina virtual de réplica debe eliminarse si se deshabilita la protección para una VM de origen Hola. Si habilita a esta configuración, al deshabilitar la protección para el origen de hello máquina virtual se quita de la consola de Site Recovery hello, configuración de Site Recovery para hello VMM se quita de la consola VMM de Hola y Hola réplica se eliminó.
10. En **inicial del método de replicación**, si se está replicando a través de la red hello, especifique si toostart la replicación inicial de Hola o programarlo. ancho de banda de red toosave, conviene tooschedule que fuera de su horario ocupado. y, a continuación, haga clic en **Aceptar**.

     ![Directiva de replicación](./media/vmm-to-vmm-walkthrough-replication/gs-replication2.png)
11. Cuando se crea una nueva directiva automáticamente tiene asociadas con hello nube de VMM. En **Directiva de replicación**, haga clic en **Aceptar**. Puede asociar más nubes de VMM (hello y máquinas virtuales en ellos) con esta directiva de replicación en **replicación** > nombre de directiva > **asociar la nube de VMM**.

     ![Directiva de replicación](./media/vmm-to-vmm-walkthrough-replication/policy-associate.png)



## <a name="prepare-for-offline-initial-replication"></a>Preparación para la replicación inicial sin conexión

Para hacer la replicación sin conexión para la copia de datos iniciales de Hola. Para preparar esta operación, haga lo siguiente:

* En el servidor de origen de hello, especifique una ubicación de ruta de acceso de qué Hola llevará a cabo la exportación de datos. Asigne Control total para los permisos NTFS y recurso compartido de servicio VMM de toohello en la ruta de acceso de exportación de Hola. En el servidor de destino de hello, especifique una ubicación de ruta de acceso desde la que importación datos de Hola se producirá. Asignar Hola mismos permisos en esta ruta de acceso de importación.
* Si hello importar o se comparte la ruta de acceso de exportación, asignar la pertenencia de grupo administrador, usuario avanzado, operador de impresión u operador de servidor para la cuenta de servicio VMM hello en el equipo remoto hello en qué Hola compartido se encuentra.
* Si usas los hosts de tooadd ejecutar como cuentas, en hello importar y exportar las rutas de acceso, asigne lectura y permisos de escritura toohello cuentas de ejecución en VMM.
* Hola importar y exportar recursos compartidos no se deben encontrar en cualquier equipo que se usa como un servidor de host de Hyper-V, porque la configuración de bucle invertido no es compatible con Hyper-V.
* En Active Directory, en cada servidor de host de Hyper-V que contiene máquinas virtuales que desea tooprotect, habilitar y configurar la delegación restringida tootrust Hola remota los equipos en qué Hola importación y exportación en las rutas de acceso se encuentran, como se indica a continuación:
  1. En el controlador de dominio de hello, abra **equipos y usuarios de Active Directory**.
  2. En el árbol de consola de hello, haga clic en **DomainName** > **equipos**.
  3. Nombre del servidor de host de Hyper-V de Hola de contextual > **propiedades**.
  4. En hello **delegación** , haga clic en **confiar en este equipo para servicios solo de delegación toospecified**.
  5. Haga clic en **Usar cualquier protocolo de autenticación**.
  6. Haga clic en **Agregar** > **Usuarios y equipos**.
  7. Nombre del tipo hello del equipo de Hola que hospeda la ruta de acceso de exportación de hello > **Aceptar**. En la lista hello de servicios disponibles, mantenga presionada la tecla CTRL de Hola y haga clic en **cifs** > **Aceptar**. Repita para nombre de hello del equipo de hello esa ruta de acceso de importación de Hola de hosts. Repita según sea necesario para servidores host de Hyper-V adicionales.



## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 9: Habilitar replicación](vmm-to-vmm-walkthrough-enable-replication.md).
