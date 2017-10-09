---
title: aaaExtend tooAzure de grupos de disponibilidad AlwaysOn local | Documentos de Microsoft
description: "Este tutorial usa recursos creados con el modelo de implementación clásica de Hola y describe cómo toouse Hola a Asistente para agregar una réplica en SQL Server Management Studio (SSMS) tooadd una réplica del grupo de disponibilidad AlwaysOn en Azure."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 7ca7c423-8342-4175-a70b-d5101dfb7f23
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/31/2017
ms.author: mikeray
ms.openlocfilehash: 51fe117b40d69706b35f30101538a7a36116e128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="extend-on-premises-always-on-availability-groups-tooazure"></a>Extender tooAzure de grupos de disponibilidad AlwaysOn local
Los grupos de disponibilidad AlwaysOn proporcionan alta disponibilidad para los grupos de la base de datos mediante la incorporación de réplicas secundarias. Estas réplicas permiten la conmutación por error en bases de datos en caso de error. También pueden ser utilizado toooffload leer las cargas de trabajo o las tareas de copia de seguridad.

Puede ampliar tooMicrosoft de grupos de disponibilidad local Azure aprovisionamiento uno o más máquinas virtuales de Azure con SQL Server y, a continuación, agregarlos como réplicas tooyour grupos de disponibilidad local.

Este tutorial se da por supuesto que tiene Hola siguientes:

* Una suscripción de Azure activa. Puede [suscribirse a una evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Un grupo de disponibilidad AlwaysOn local existente. Para más información sobre los grupos de disponibilidad, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).
* Conectividad entre Hola local de red y la red virtual de Azure. Para obtener más información acerca de cómo crear esta red virtual, vea [conexión de crear un sitio a sitio con Hola portal de Azure (clásica)](../../../vpn-gateway/vpn-gateway-howto-site-to-site-classic-portal.md).

> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

## <a name="add-azure-replica-wizard"></a>Asistente para agregar una réplica de Azure
Esta sección muestra cómo hello toouse **Asistente para agregar réplica de Azure** tooextend su tooinclude de solución de grupo de disponibilidad AlwaysOn Azure réplicas.

> [!IMPORTANT]
> Hola **Asistente para agregar réplica de Azure** solo es compatible con las máquinas virtuales creadas con el modelo de implementación de hello clásico. Nuevas implementaciones de máquina virtual deben utilizar el modelo de administrador de recursos más recientes de Hola. Si está usando máquinas virtuales con el Administrador de recursos, debe agregar manualmente hello Azure réplica mediante commmands de Transact-SQL (no mostrado aquí). Este asistente no funcionará en el escenario de administrador de recursos de Hola.

1. En SQL Server Management Studio, expanda **Alta disponibilidad AlwaysOn** > **Grupos de disponibilidad** > **[Nombre del grupo de disponibilidad]**.
2. Haga clic con el botón derecho en **Réplicas de disponibilidad** y luego en **Agregar réplica**.
3. De forma predeterminada, Hola **tooAvailability Asistente para grupo de agregar una réplica** se muestra. Haga clic en **Siguiente**.  Si ha seleccionado hello **no volver a mostrar esta página** opción final Hola de página de Hola durante un inicio anterior de este asistente, esta pantalla no aparecerá.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742861.png)
4. Será necesario tooconnect tooall existente las réplicas secundarias. Puede hacer clic en **Conectar...** junto a cada réplica o puede hacer clic en **Conectar todo...** en la parte inferior de Hola de pantalla de bienvenida. Después de la autenticación, haga clic en **siguiente** tooadvance toohello siguiente pantalla.
5. En hello **especificar réplicas** página, aparecen varias pestañas a través de la parte superior de hello: **réplicas**, **extremos**, **preferencias de copia de seguridad**, y **Escucha**. De hello **réplicas** , haga clic en **Agregar réplica de Azure...** toolaunch Hola Asistente para agregar réplica de Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742863.png)
6. Seleccione un certificado de administración de Azure existente desde el almacén de certificados de Windows local Hola si ha instalado uno antes. Seleccione o escriba el Id. de Hola de una suscripción de Azure si ha usado uno antes. Puede haga clic en descarga toodownload, instale un certificado de administración de Azure y descargar Hola lista de las suscripciones que usan una cuenta de Azure.
   
    ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742864.png)
7. Se rellena cada campo de página de hello con valores que será usado toocreate Hola Máquina Virtual (VM) de Azure que hospedará la réplica de Hola.
   
   | Configuración | Descripción |
   | --- | --- |
   | **Imagen** |Activar combinación Hola deseado del sistema operativo y SQL Server |
   | **Tamaño de VM** |Seleccione tamaño Hola de máquina virtual que mejor se adapte a sus necesidades empresariales |
   | **Nombre de VM** |Especifique un nombre único para hello nueva máquina virtual. Hola nombre debe contener entre 3 y 15 caracteres, puede contener solo letras, números y guiones y debe empezar por una letra y terminar por una letra o un número. |
   | **Nombre de usuario de máquina virtual** |Especifique un nombre de usuario que se convertirá en la cuenta de administrador de hello en hello VM |
   | **Contraseña de administrador de VM** |Especifique una contraseña para la nueva cuenta de hello |
   | **Confirm Password** |Confirmar contraseña de Hola de hello nueva cuenta |
   | **Virtual Network** |Especifique Hola ese Hola debe usar la nueva máquina virtual de red virtual de Azure. Para obtener más información sobre las redes virtuales, consulte [Información general sobre redes virtuales](../../../virtual-network/virtual-networks-overview.md). |
   | **Subred de red virtual** |Especificar la subred de red virtual de hello ese Hola que debe usar la nueva máquina virtual |
   | **Dominio** |Confirmar el valor previamente rellenado de hello para el dominio de hello es correcto |
   | **Nombre de usuario del dominio** |Especifique una cuenta que está en el grupo de administradores locales de hello en nodos de clúster local de Hola |
   | **Password** |Especificar contraseña hello para el nombre de usuario de dominio de Hola |
8. Haga clic en **Aceptar** configuración de implementación de toovalidate Hola.
9. A continuación se muestran las condiciones legales. Leer y haga clic en **Aceptar** si los acepta toothese términos.
10. Hola **especificar réplicas** vuelve a aparecer la página. Compruebe la configuración de hello para la nueva réplica de Azure hello en hello **réplicas**, **extremos**, y **preferencias de copia de seguridad** pestañas. Modificar configuración toomeet sus requisitos empresariales.  Para obtener más información sobre los parámetros de Hola que contienen estas pestañas, consulte [especificar la página de réplicas (disponibilidad asistente/Agregar réplica Asistente para nuevo grupo)](https://msdn.microsoft.com/library/hh213088.aspx). Tenga en cuenta que no se puede crear agentes de escucha mediante la pestaña de agente de escucha de Hola para grupos de disponibilidad que contienen réplicas de Azure. Además, si un agente de escucha ya se ha creado toolaunching anterior Hola asistente, recibirá un mensaje que indica que no se admite en Azure. Veremos cómo los agentes de escucha de toocreate Hola **crear un agente de escucha del grupo de disponibilidad** sección.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742865.png)
11. Haga clic en **Siguiente**.
12. Seleccionar método de sincronización de datos de hello desea toouse en hello **seleccionar sincronización de datos iniciales** página y haga clic en **siguiente**. Para la mayoría de los escenarios, seleccione **Sincronización de datos completos**. Para más información sobre los métodos de sincronización de datos, consulte [Página Seleccionar sincronización de datos iniciales (asistentes para grupos de disponibilidad AlwaysOn)](https://msdn.microsoft.com/library/hh231021.aspx).
13. Revisar los resultados de hello en hello **validación** página. Corrija los problemas pendientes y volver a ejecutar la validación de hello si es necesario. Haga clic en **Siguiente**.
    
     ![SQL](./media/virtual-machines-windows-classic-sql-onprem-availability/IC742866.png)
14. Revisar la configuración de hello en hello **resumen** página, a continuación, haga clic en **finalizar**.
15. comienza el proceso de aprovisionamiento de Hola. Cuando se complete correctamente el Asistente de hello, haga clic en **cerrar** tooexit fuera del Asistente de Hola.

> [!NOTE]
> Hello Asistente para agregar réplica de Azure crea un archivo de registro en Users\nombre Name\AppData\Local\SQL Server\AddReplicaWizard. Este archivo de registro puede ser usado tootroubleshoot no se pudo implementaciones de réplica de Azure. Si Hola asistente no puede ejecutar cualquier acción, se revierten todas las operaciones anteriores, incluye la eliminación de hello aprovisionado la máquina virtual.
> 
> 

## <a name="create-an-availability-group-listener"></a>Creación del agente de escucha del grupo de disponibilidad
Una vez creado el grupo de disponibilidad de hello, debe crear un agente de escucha para los clientes tooconnect toohello réplicas. Agentes de escucha dirigen Hola de tooeither de las conexiones entrantes principal o una réplica secundaria de solo lectura. Para más información sobre los agentes de escucha, consulte [Configuración de un agente de escucha con ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).

## <a name="next-steps"></a>Pasos siguientes
Hola de suma toousing **Asistente para agregar réplica de Azure** tooextend tooAzure de su grupo de disponibilidad AlwaysOn, también puede mover algunas cargas de trabajo de SQL Server tooAzure completamente. tooget iniciado, consulte [aprovisionamiento de una máquina Virtual de SQL Server en Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Para ver otros temas relacionados con toorunning SQL Server en máquinas virtuales de Azure, consulte [SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

