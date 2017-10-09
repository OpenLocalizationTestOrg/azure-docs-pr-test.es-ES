---
title: "Tutorial de grupos de disponibilidad de servidor - máquinas virtuales de Azure - aaaSQL | Documentos de Microsoft"
description: "Este tutorial se muestra cómo toocreate un SQL Server grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 08a00342-fee2-4afe-8824-0db1ed4b8fca
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: 65b4210b0f851828a32a02053b03e4b8d469ba4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-vm-manually"></a>Configuración manual de grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure

Este tutorial se muestra cómo toocreate un SQL Server grupo de disponibilidad AlwaysOn en máquinas virtuales de Azure. todo el tutorial Hola crea un grupo de disponibilidad con una réplica de base de datos en dos servidores SQL Server.

**Estimación del tiempo**: tarda unos 30 minutos toocomplete una vez que se cumplen los requisitos previos de Hola.

diagrama de Hello muestra lo que crea en el tutorial de Hola.

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="prerequisites"></a>Requisitos previos

tutorial de Hola se da por supuesto que tiene conocimientos básicos de SQL Server siempre grupos de disponibilidad. Para más información, consulte [Información general de los grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).

Hello tabla siguiente enumeran los requisitos previos de Hola que necesita toocomplete antes de iniciar este tutorial:

|  |Requisito |Descripción |
|----- |----- |----- |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png) | Dos servidores SQL Server | - En un conjunto de disponibilidad de Azure <br/> - En un solo dominio <br/> - Con la característica Clústeres de conmutación por error instalada |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)| Windows Server | Recurso compartido de archivos para testigo de clúster |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Cuenta de servicio de SQL Server | Cuenta de dominio |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Cuenta de servicio Agente SQL Server | Cuenta de dominio |  
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Puertos de firewall abiertos | - SQL Server: **1433** para la instancia predeterminada <br/> - Punto de conexión de reflejo de la base de datos: **5022** o cualquier puerto disponible <br/> - Sondeo de Azure Load Balancer: **59999** o cualquier puerto disponible |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Agregar característica Clústeres de conmutación por error | Ambos servidores SQL Server necesitan esta característica |
|![Square](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/square.png)|Cuenta de dominio de la instalación | - Administrador local en cada servidor SQL Server <br/> - Miembro del rol fijo del servidor sysadmin de SQL Server para cada instancia de SQL Server  |


Antes de comenzar el tutorial de hello, necesita demasiado[completar los requisitos previos para la creación de grupos de disponibilidad AlwaysOn en máquinas virtuales Azure](virtual-machines-windows-portal-sql-availability-group-prereq.md). Si estos requisitos previos ya se ha completado, puede saltar demasiado[crear clúster](#CreateCluster).


<!--**Procedure**: *This is hello first “step”. Make titles H2’s and short and clear – H2’s appear in hello right pane on hello web page and are important for navigation.*-->

<a name="CreateCluster"></a>
##Crear clúster Hola

Después de Hola se completan los requisitos previos, Hola primer paso es toocreate un clúster de conmutación por error de Windows Server que incluye dos servidores SQL Server y un servidor testigo.  

1. RDP toohello primer servidor de SQL Server con una cuenta de dominio que es un administrador de servidores SQL Server y servidor de testigo de Hola.

   >[!TIP]
   >Si ha seguido hello [documento de requisitos previos](virtual-machines-windows-portal-sql-availability-group-prereq.md), crea una cuenta llamada **CORP\Install**. Utilice esta cuenta.

2. Hola **el administrador del servidor** panel, seleccione **herramientas**y, a continuación, haga clic en **Administrador de clústeres de conmutación por error**.
3. En el panel izquierdo de hello, haga clic en **Administrador de clústeres de conmutación por error**y, a continuación, haga clic en **crear un clúster de**.
   ![Crear clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/40-createcluster.png)
4. En el Asistente para crear clúster de Hola, cree un clúster de un nodo recorriendo las páginas Hola con la configuración de hello en hello en la tabla siguiente:

   | Page | Configuración |
   | --- | --- |
   | Antes de empezar |Usar predeterminados |
   | Seleccionar servidores |Hola de tipo nombre del primer servidor SQL Server en **escriba el nombre de servidor** y haga clic en **agregar**. |
   | Advertencia de validación |Seleccione **no. no requieren soporte técnico de Microsoft para este clúster y, por tanto, no desea validación de hello toorun las pruebas. Al hacer clic en siguiente, continuar con la creación de clúster de hello**. |
   | Punto de acceso para administrar Hola clúster |Escriba un nombre de clúster, por ejemplo **SQLAGCluster1** en **Nombre del clúster**.|
   | Confirmación |Use los valores predeterminados a menos que use Espacios de almacenamiento. Vea la nota de Hola que sigue a esta tabla. |

### <a name="set-hello-cluster-ip-address"></a>Establecer la dirección IP del clúster Hola

1. En **Administrador de clústeres de conmutación por error**, desplácese hacia abajo demasiado**recursos principales de clúster** y expanda detalles del clúster Hola. Debería ver dos hello **nombre** hello y **dirección IP** recursos de hello **error** estado. Hello recurso de dirección IP no se puede poner en conexión clúster Hola se asigna Hola igual de direcciones IP como máquina de hello propiamente dicha, por lo tanto, es una dirección duplicada.

2. Hola contextual error **dirección IP** recurso y, a continuación, haga clic en **propiedades**.

   ![Propiedades de clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/42_IPProperties.png)

3. Seleccione **dirección IP estática** y especifique una dirección de subred donde hello SQL Server en el cuadro de texto de dirección de hello disponible. A continuación, haga clic en **Aceptar**.
4. Hola **recursos principales de clúster** sección, haga clic en el nombre de clúster y haga clic en **poner en conexión**. Después espere hasta que ambos recursos estén en línea. Cuando el recurso de nombre de clúster de Hola se pone en línea, actualiza el servidor de DC de hello con una nueva cuenta de equipo de AD. Utilice este hello toorun de cuenta de AD más tarde el servicio de clúster del grupo de disponibilidad.

### <a name="addNode"></a>Agregar Hola otro toocluster de SQL Server

Agregar Hola otro clúster de SQL Server toohello.

1. En el árbol del explorador de hello, haga clic en el clúster de Hola y haga clic en **agregar nodo**.

    ![Agregar nodo toohello clúster](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/44-addnode.png)

1. Hola **Asistente para agregar nodos**, haga clic en **siguiente**. Hola **seleccionar servidores** página, agregue Hola segundo servidor SQL Server. Nombre del servidor de tipo hello en **escriba el nombre de servidor** y, a continuación, haga clic en **agregar**. Cuando haya terminado, haga clic en **Siguiente**.

1. Hola **advertencia de validación** página, haga clic en **No** (en un escenario de producción debería realizar pruebas de validación de hello). A continuación, haga clic en **Siguiente**.

8. Hola **confirmación** página si usa espacios de almacenamiento, desactive Hola casilla **agregar todo el almacenamiento apto toohello clúster.**

   ![Agregar nodo de confirmación](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/46-addnodeconfirmation.png)

    >[!WARNING]
   >Si utiliza espacios de almacenamiento y no desactive **agregar todo el almacenamiento apto toohello clúster**, Windows separa los discos virtuales de Hola durante el proceso de agrupación en clústeres de Hola. Como resultado, que no aparecen en el Administrador de discos o en el explorador hasta que se quiten los espacios de almacenamiento de Hola de clúster de Hola y volver a adjuntar con PowerShell. Espacios de almacenamiento agrupa varios discos en grupos de toostorage. Para obtener más información, consulte el artículo sobre [espacios de almacenamiento](https://technet.microsoft.com/library/hh831739).

1. Haga clic en **Siguiente**.

1. Haga clic en **Finalizar**

   El Administrador de clústeres de conmutación por error se muestra que el clúster tiene un nuevo nodo y las listas en hello **nodos** contenedor.

10. Cerrar sesión de escritorio remoto de Hola.

### <a name="add-a-cluster-quorum-file-share"></a>Agregar un recurso compartido de cuórum de clúster

En este ejemplo, clúster de Windows hello utiliza un toocreate de recurso compartido de archivo un quórum de clúster. Este tutorial utiliza un cuórum de mayoría de recurso compartido de archivos y nodo. Para más información, consulte [Descripción de las configuraciones de cuórum en un clúster de conmutación por error](http://technet.microsoft.com/library/cc731739.aspx).

1. Conectar el servidor de miembro de testigo de recurso compartido de archivos de toohello con una sesión de escritorio remoto.

1. En **Administrador del servidor**, haga clic en **Herramientas**. Abra **Administración de equipos**.

1. Haga clic en **Carpetas compartidas**.

1. Haga clic con el botón derecho en **Recursos compartidos** y, a continuación, haga clic en **Nuevo recurso compartido...**

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Use **crear un Asistente para carpetas compartidas** toocreate un recurso compartido.

1. En **ruta de acceso de carpeta**, haga clic en **examinar** y busque o cree una ruta de acceso de carpeta compartida de Hola. Haga clic en **Siguiente**.

1. En **nombre, descripción y configuración** Compruebe el nombre del recurso compartido de Hola y ruta de acceso. Haga clic en **Siguiente**.

1. En **Permisos de la carpeta compartida**, establezca **Personalizar permisos**. Clic en **Personalizado...**

1. En **Personalizar permisos**, haga clic en **Agregar...**

1. Asegúrese de que ese clúster de Hola Hola cuenta usada toocreate tiene control total.

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/50-filesharepermissions.png)

1. Haga clic en **Aceptar**.

1. En **Permisos de la carpeta compartida**, haga clic en **Finalizar**. Haga clic de nuevo en **Finalizar**.  

1. Cierre la sesión de servidor hello

### <a name="configure-cluster-quorum"></a>Configuración del cuórum de clúster

A continuación, establezca el quórum del clúster Hola.

1. Conectar toohello primer nodo del clúster con Escritorio remoto.

1. En **Administrador de clústeres de conmutación por error**, haga clic en el clúster de hello, seleccione demasiado**más acciones**y haga clic en **configurar opciones de quórum de clúster...** .

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/52-configurequorum.png)

1. En **Asistente para configurar quórum de clúster**, haga clic en **Siguiente**.

1. En **seleccionar la opción de configuración de quórum**, elija **seleccionar testigo de quórum de hello**y haga clic en **siguiente**.

1. En **Seleccionar el testigo de quórum**, haga clic en **Configurar un testigo de recurso compartido de archivos**.

   >[!TIP]
   >Windows Server 2016 admite un testigo en la nube. Si elige este tipo de testigo, no necesita ningún testigo de recurso compartido de archivos. Para más información, consulte [Implementación de un testigo en la nube para un clúster de conmutación por error](http://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness). Este tutorial usa un testigo de recurso compartido de archivos, que es compatible con los sistemas operativos anteriores.

1. En **testigo del recurso compartido de archivo de configuración**, ruta de acceso de tipo hello para el recurso compartido de Hola que creó. Haga clic en **Siguiente**.

1. Compruebe la configuración de hello en **confirmación**. Haga clic en **Siguiente**.

1. Haga clic en **Finalizar**

recursos principales de clúster Hola se configuran con un testigo de recurso compartido de archivos.

## <a name="enable-availability-groups"></a>Habilitación de grupos de disponibilidad

A continuación, habilite hello **grupos de disponibilidad AlwaysOn** característica. Siga estos pasos para ambos servidores SQL Server.

1. De hello **iniciar** pantalla, inicie **Administrador de configuración de SQL Server**.
2. En el árbol del explorador de hello, haga clic en **Services de SQL Server**, a continuación, haga clic en hello **SQL Server (MSSQLSERVER)** de servicio y haga clic en **propiedades**.
3. Haga clic en hello **alta disponibilidad de AlwaysOn** y, después, seleccione **habilitar los grupos de disponibilidad AlwaysOn**, como se indica a continuación:

    ![Habilitación de grupos de disponibilidad AlwaysOn](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/54-enableAlwaysOn.png)

4. Haga clic en **Apply**. Haga clic en **Aceptar** en el cuadro de diálogo emergente de Hola.

5. Reinicie el servicio de SQL Server de Hola.

Repita estos pasos en hello en otro servidor SQL Server.

<!-----------------
## <a name="endpoint-firewall"></a>Open firewall for hello database mirroring endpoint

Each instance of SQL Server that participates in an Availability Group requires a database mirroring endpoint. This endpoint is a TCP port for hello instance of SQL Server that is used toosynchronize hello database replicas in hello Availability Groups on that instance.

On both SQL Servers, open hello firewall for hello TCP port for hello database mirroring endpoint.

1. On hello first SQL Server **Start** screen, launch **Windows Firewall with Advanced Security**.
2. In hello left pane, select **Inbound Rules**. On hello right pane, click **New Rule**.
3. For **Rule Type**, choose **Port**.
1. For hello port, specify TCP and choose an unused TCP port number. For example, type *5022* and click **Next**.

   >[!NOTE]
   >For this example, we're using TCP port 5022. You can use any available port.

5. In hello **Action** page, keep **Allow hello connection** selected and click **Next**.
6. In hello **Profile** page, accept hello default settings and click **Next**.
7. In hello **Name** page, specify a rule name, such as **Default Instance Mirroring Endpoint** in hello **Name** text box, then click **Finish**.

Repeat these steps on hello second SQL Server.
-------------------------->

## <a name="create-a-database-on-hello-first-sql-server"></a>Crear una base de datos en hello primer servidor SQL Server

1. Archivo RDP de inicio hello toohello primer servidor de SQL Server con un dominio de la cuenta que es miembro de sysadmin rol fijo de servidor.
1. Abra SQL Server Management Studio y conéctese toohello primer servidor SQL Server.
7. En el **Explorador de objetos**, haga clic con el botón derecho en **Bases de datos** y luego en **Nueva base de datos**.
8. En **Nombre de base de datos**, escriba **MyDB1** y después haga clic en **Aceptar**.

### <a name="backupshare"></a> Creación de un recurso compartido de copia de seguridad

1. En Hola el primer servidor de SQL Server en **el administrador del servidor**, haga clic en **herramientas**. Abra **Administración de equipos**.

1. Haga clic en **Carpetas compartidas**.

1. Haga clic con el botón derecho en **Recursos compartidos** y, a continuación, haga clic en **Nuevo recurso compartido...**

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/48-newshare.png)

   Use **crear un Asistente para carpetas compartidas** toocreate un recurso compartido.

1. En **ruta de acceso de carpeta**, haga clic en **examinar** y busque o cree una ruta de acceso de carpeta compartida de hello base de datos copia de seguridad. Haga clic en **Siguiente**.

1. En **nombre, descripción y configuración** Compruebe el nombre del recurso compartido de Hola y ruta de acceso. Haga clic en **Siguiente**.

1. En **Permisos de la carpeta compartida**, establezca **Personalizar permisos**. Clic en **Personalizado...**

1. En **Personalizar permisos**, haga clic en **Agregar...**

1. Asegúrese de que Hola SQL Server y Agente SQL Server las cuentas de servicio para ambos servidores tienen control total.

   ![Nuevo recurso compartido](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/68-backupsharepermission.png)

1. Haga clic en **Aceptar**.

1. En **Permisos de la carpeta compartida**, haga clic en **Finalizar**. Haga clic de nuevo en **Finalizar**.  

### <a name="take-a-full-backup-of-hello-database"></a>Realizar copia de seguridad de base de datos de hello una completa

Necesita tooback seguridad Hola nueva base de datos tooinitialize Hola cadena de registros. Si no se realiza una copia de seguridad de base de datos nueva hello, no pueden incluirse en un grupo de disponibilidad.

1. En **Explorador de objetos**, haga clic en la base de datos de hello, seleccione demasiado**tareas...** , haga clic en **copia de seguridad**.

1. Haga clic en **Aceptar** tootake una ubicación de copia de seguridad de toohello de copia de seguridad completa de forma predeterminada.

## <a name="create-hello-availability-group"></a>Crear grupo de disponibilidad de hello
Ya estás listo tooconfigure un grupo de disponibilidad mediante Hola siguiendo los pasos:

* Crear una base de datos en hello primer servidor SQL Server.
* Realice una copia de seguridad completa y una copia de seguridad del registro de transacciones de base de datos de Hola
* Hola de restauración completa y toohello de las copias de seguridad de registro segundo SQL Server con hello **NORECOVERY** opción
* Crear grupo de disponibilidad de hello (**AG1**) con réplicas secundarias legibles, confirmación sincrónica y conmutación automática por error

### <a name="create-hello-availability-group"></a>Crear grupo de disponibilidad de hello:

1. En la sesión de escritorio remoto toohello primer servidor SQL Server. En el **Explorador de objetos** de SSMS, haga clic con el botón derecho en **Alta disponibilidad de AlwaysOn** y en **Asistente para nuevo grupo de disponibilidad**.

    ![Iniciar el Asistente para nuevo grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/56-newagwiz.png)

2. Hola **Introducción** página, haga clic en **siguiente**. Hola **especificar el nombre de grupo de disponibilidad** página, escriba un nombre para hello grupo de disponibilidad, por ejemplo **AG1**, en **nombre del grupo de disponibilidad**. Haga clic en **Siguiente**.

    ![Asistente para nuevo grupo de disponibilidad, especificar el nombre del grupo](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/58-newagname.png)

3. Hola **seleccionar bases de datos** , seleccione la base de datos y haga clic en **siguiente**.

   >[!NOTE]
   >base de datos de Hello cumple los requisitos previos de Hola para un grupo de disponibilidad dado que ha realizado al menos una copia de seguridad completa en la réplica principal pretendida de Hola.

   ![Asistente para nuevo grupo de disponibilidad, seleccionar bases de datos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/60-newagselectdatabase.png)
4. Hola **especificar réplicas** página, haga clic en **agregar una réplica**.

   ![Asistente para nuevo grupo de disponibilidad, especificar réplicas](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/62-newagaddreplica.png)
5. Hola **conectar tooServer** cuadro de diálogo. Nombre del tipo hello del segundo servidor de hello en **nombre del servidor**. Haga clic en **Conectar**.

   Nuevo en hello **especificar réplicas** página, ahora debería ver segundo servidor de hello enumerado en **réplicas de disponibilidad**. Configurar réplicas de hello como se indica a continuación.

   ![Asistente para nuevo grupo de disponibilidad, especificar réplicas (completo)](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/64-newagreplica.png)

6. Haga clic en **extremos** toosee de base de datos de hello extremo de reflejo para este grupo de disponibilidad. Hola uso mismo número de puerto que usó al configurar hello [regla de firewall para los puntos de conexión de creación de reflejo de la base de datos](virtual-machines-windows-portal-sql-availability-group-prereq.md#endpoint-firewall).

    ![Asistente para nuevo grupo de disponibilidad, seleccionar sincronización de datos iniciales](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/66-endpoint.png)

8. Hola **seleccionar sincronización de datos iniciales** , seleccione **completa** y especifique una ubicación de red compartida. Para la ubicación de hello, usar hello [recurso compartido de copia de seguridad que creaste](#backupshare). En el ejemplo de Hola fue así, **\\\\\<primer servidor SQL Server\>\Backup\**. Haga clic en **Siguiente**.

   >[!NOTE]
   >Sincronización completa toma una copia de seguridad completa de base de datos de hello en la primera instancia de SQL Server de Hola y restaurarlo toohello segunda instancia. Para bases de datos grandes, no se recomienda la sincronización completa porque puede llevar mucho tiempo. Puede reducir este tiempo manualmente tomando una copia de seguridad de base de datos de Hola y restaurarlo con `NO RECOVERY`. Si ya se restaure la base de datos de hello con `NO RECOVERY` en hello segundo SQL Server antes de configurar el grupo de disponibilidad de hello, elija **solo unión**. Elija si desea que copia de seguridad de hello tootake después de configurar el grupo de disponibilidad de hello, **omitir la sincronización de datos inicial**.

    ![Asistente para nuevo grupo de disponibilidad, seleccionar sincronización de datos iniciales](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/70-datasynchronization.png)

9. Hola **validación** página, haga clic en **siguiente**. Esta página debería ser similar toohello después de imagen:

    ![Asistente para nuevo grupo de disponibilidad, validación](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/72-validation.png)

    >[!NOTE]
    >Hay una advertencia para la configuración de agente de escucha de hello porque no ha configurado un agente de escucha del grupo de disponibilidad. Puede omitir esta advertencia porque en máquinas virtuales de Azure crear agente de escucha de hello después de crear el equilibrador de carga de Azure Hola.

10. Hola **resumen** página, haga clic en **finalizar**, a continuación, espere mientras el Asistente de hello configura Hola nuevo grupo de disponibilidad. Hola **progreso** página, puede hacer clic en **detalles más** tooview Hola detallada progreso. Una vez que haya finalizado el Asistente de hello, inspeccionar hello **resultados** tooverify de página que Hola grupo de disponibilidad se creó correctamente.

     ![Asistente para nuevo grupo de disponibilidad, resultados](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/74-results.png)
11. Haga clic en **cerrar** Asistente de hello tooexit.

### <a name="check-hello-availability-group"></a>Hola de comprobación de grupo de disponibilidad

1. En el **Explorador de objetos**, expanda **Alta disponibilidad de AlwaysOn** y después expanda **Grupos de disponibilidad**. Ahora debería ver Hola nuevo grupo de disponibilidad de este contenedor. Haga clic en grupo de disponibilidad de Hola y haga clic en **Mostrar panel**.

   ![Mostrar panel de grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/76-showdashboard.png)

   Su **panel AlwaysOn** debe tener un aspecto similar toothis.

   ![Panel de grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/78-agdashboard.png)

   Puede ver réplicas hello, modo de conmutación por error de Hola de cada estado de sincronización hello y de réplica.

2. En **Administrador de clústeres de conmutación por error**, haga clic en el clúster. Seleccione **Roles**. nombre de grupo de disponibilidad de Hello utilizado es un rol en clúster de Hola. Ese grupo de disponibilidad no tiene una dirección IP para las conexiones de cliente porque no ha configurado un agente de escucha. Después de crear un equilibrador de carga de Azure que va a configurar el agente de escucha de Hola.

   ![Grupo de disponibilidad en el administrador de clústeres de conmutación por error.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/80-clustermanager.png)

   > [!WARNING]
   > No intente toofail sobre Hola grupo de disponibilidad desde el Administrador de clústeres de conmutación por error de Hola. Todas las operaciones de conmutación por error deben realizarse desde el **Panel AlwaysOn** de SSMS. Para obtener más información, consulte [restricciones sobre el uso Hola Administrador de clústeres de conmutación por error con grupos de disponibilidad](https://msdn.microsoft.com/library/ff929171.aspx).
    >

En este punto, tiene un grupo de disponibilidad con réplicas en dos instancias de SQL Server. Puede mover Hola grupo de disponibilidad entre instancias. No se puede conectar toohello grupo de disponibilidad aún porque no tiene un agente de escucha. En máquinas virtuales de Azure, el agente de escucha de hello requiere un equilibrador de carga. Hola siguiente paso es toocreate equilibrador de carga de hello en Azure.

<a name="configure-internal-load-balancer"></a>

## <a name="create-an-azure-load-balancer"></a>Creación de un equilibrador de carga de Azure

En Azure Virtual Machines, un grupo de disponibilidad de SQL Server necesita un equilibrador de carga. equilibrador de carga de Hello contiene la dirección IP de hello para el agente de escucha del grupo de disponibilidad de Hola. En esta sección se resume cómo toocreate Hola equilibrador de carga de hello portal de Azure.

1. Hola portal de Azure, vaya toohello grupo de recursos donde los servidores SQL Server y haga clic en **+ agregar**.
2. Busque **Equilibrador de carga**. Elegir el equilibrador de carga de hello publicado por Microsoft.

   ![Grupo de disponibilidad en el administrador de clústeres de conmutación por error.](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/82-azureloadbalancer.png)

1.  Haga clic en **Crear**.
3. Configurar Hola parámetros para el equilibrador de carga de hello siguientes.

   | Configuración | Campo |
   | --- | --- |
   | **Name** |Usar un nombre de texto para el equilibrador de carga de hello, por ejemplo **sqlLB**. |
   | **Tipo** |Interno |
   | **Red virtual** |Usar el nombre de Hola de hello red virtual de Azure. |
   | **Subred** |Usar el nombre de Hola de subred de Hola que Hola máquina virtual está en.  |
   | **Asignación de dirección IP** |Estática |
   | **Dirección IP** |Use una dirección disponible en la subred. |
   | **Suscripción** |Use Hola misma suscripción que la máquina virtual de Hola. |
   | **Ubicación** |Use Hola misma ubicación que la máquina virtual de Hola. |

   Hola portal de Azure, hoja debe tener este aspecto:

   ![Cree un equilibrador de carga](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/84-createloadbalancer.png)

1. Haga clic en **crear**, equilibrador de carga de toocreate Hola.

equilibrador de carga de hello tooconfigure, deberá toocreate un grupo back-end, un sondeo, conjunto Hola equilibrio de carga y reglas. Haga lo siguiente en hello portal de Azure.

### <a name="add-backend-pool"></a>Agregar grupo de back-end

1. Hola portal de Azure, vaya tooyour grupo de disponibilidad. Puede que tenga el equilibrador de carga de toorefresh Hola vista toosee Hola recién creado.

   ![Buscar equilibrador de carga en el grupo de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/86-findloadbalancer.png)

1. Haga clic en el equilibrador de carga de hello, haga clic en **grupos back-end**y haga clic en **+ agregar**. Configure el grupo de back-end de hello como sigue:

   | Configuración | Descripción | Ejemplo
   | --- | --- |---
   | **Name** | Escribir un nombre de texto | SQLLBBE
   | **Asociado a** | Elegir de la lista | Conjunto de disponibilidad
   | **El conjunto de disponibilidad** | Usar un nombre de conjunto de disponibilidad de Hola que la VM de SQL Server se encuentran en | sqlAvailabilitySet |
   | **Máquinas virtuales** |Hola dos nombres de VM de Azure SQL Server | sqlserver-0, sqlserver-1

1. Nombre del tipo hello para el grupo de servidores de hello back-end.

1. Haga clic en **+ Agregar máquina virtual**.

1. Para un conjunto de disponibilidad de hello, elija disponibilidad Hola establece ese Hola servidores SQL Server están en.

1. Para máquinas virtuales, incluir tanto de hello servidores SQL Server. No incluya el servidor de testigo de recurso compartido de archivos de Hola.

1. Haga clic en **Aceptar** grupo back-end de toocreate Hola.

### <a name="set-hello-probe"></a>Sondeo de Hola de conjunto

1. Haga clic en el equilibrador de carga de hello, haga clic en **sondeos de estado**y haga clic en **+ agregar**.

1. Establecer sondeo de estado de hello como sigue:

   | Configuración | Descripción | Ejemplo
   | --- | --- |---
   | **Name** | Texto | SQLAlwaysOnEndPointProbe |
   | **Protocolo** | Elija TCP | TCP |
   | **Puerto** | Cualquier puerto no utilizado | 59999 |
   | **Intervalo**  | los intentos de cantidad de Hola de tiempo entre el sondeo en segundos |5 |
   | **Umbral incorrecto** | Hola número de errores de sondeo consecutivos que debe realizarse para una toobe de máquina virtual que se considera incorrecto  | 2 |

1. Haga clic en **Aceptar** sondeo de estado de tooset Hola.

### <a name="set-hello-load-balancing-rules"></a>Establecer reglas de equilibrio de carga de Hola

1. Haga clic en el equilibrador de carga de hello, haga clic en **reglas de equilibrio de carga**y haga clic en **+ agregar**.

1. Establecer como se indica a continuación de las reglas de equilibrio de carga de Hola.
   | Configuración | Descripción | Ejemplo
   | --- | --- |---
   | **Name** | Texto | SQLAlwaysOnEndPointListener |
   | **Frontend IP address** (Dirección IP de front-end) | Elija una dirección |Usar una dirección Hola que creó cuando creó el equilibrador de carga de Hola. |
   | **Protocolo** | Elija TCP |TCP |
   | **Puerto** | Usar el puerto de hello para la instancia de SQL Server de Hola | 1433 |
   | **Puerto back-end** | Este campo no se utiliza cuando la IP flotante está establecida para Direct Server Return | 1433 |
   | **Sondeo** |nombre de Hola que especificó para la sonda de Hola | SQLAlwaysOnEndPointProbe |
   | **Persistencia de la sesión** | Lista desplegable | **None** |
   | **Tiempo de espera de inactividad** | Tookeep minutos abrir una conexión TCP | 4 |
   | **IP flotante (Direct Server Return)** | |Enabled |

   > [!WARNING]
   > Direct Server Return se establece durante la creación. No se puede modificar.

1. Haga clic en **Aceptar** equilibrio de carga de tooset Hola.

## <a name="configure-listener"></a>Configurar el agente de escucha de Hola

Hola toodo de lo siguiente es un agente de escucha de grupo de disponibilidad en el clúster de conmutación por error de hello tooconfigure.

> [!NOTE]
> Este tutorial muestra cómo se direccionan toocreate un agente de escucha único - con una IP de ILB. toocreate uno o varios agentes de escucha con una o varias direcciones IP, consulte [equilibrador de carga y el agente de escucha de Create Availability Group | Azure](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

## <a name="set-listener-port"></a>Configuración del puerto del agente de escucha

En SQL Server Management Studio, establezca el puerto de escucha de Hola.

1. Inicie SQL Server Management Studio y conéctese toohello de réplica principal.

1. Navegue demasiado**alta disponibilidad de AlwaysOn** | **grupos de disponibilidad** | **los agentes de escucha del grupo de disponibilidad**.

1. Ahora debería ver el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error. Haga clic en nombre de agente de escucha de Hola y haga clic en **propiedades**.

1. Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (1433 pasaba Hola valor predeterminado), a continuación, haga clic en **Aceptar**.

Ahora tiene un grupo de disponibilidad de SQL Server en Azure Virtual Machines que se ejecuta en el modo de Resource Manager.

## <a name="test-connection-toolistener"></a>Toolistener de conexión de prueba

conexión de Hola tootest:

1. RDP tooa SQL Server que se encuentra en hello mismo virtual de red, pero no no réplica Hola propio. Puede usar Hola a otro servidor SQL Server en clúster de Hola.

1. Use **sqlcmd** conexión de utilidad tootest Hola. Por ejemplo, Establece la siguiente secuencia de comandos de hello un **sqlcmd** réplica principal de conexión toohello a través de agente de escucha de hello con autenticación de Windows:

    ```
    sqlcmd -S <listenerName> -E
    ```

    Si el agente de escucha de hello usa un puerto distinto de hello predeterminado (1433) de puerto, especifique el puerto hello en la cadena de conexión de Hola. Por ejemplo, hello siguiente comando sqlcmd conecta tooa escucha en el puerto 1435:

    ```
    sqlcmd -S <listenerName>,1435 -E
    ```

Hola conexión SQLCMD conecta automáticamente toowhichever instancia de réplica principal de Hola de hosts de SQL Server.

> [!TIP]
> Asegúrese de que especifica el puerto de hello está abierto en firewall de Hola de ambos servidores SQL Server. Ambos servidores requieren una regla de entrada para el puerto TCP que usa hello. Consulte [Agregar o editar regla de firewall](http://technet.microsoft.com/library/cc753558.aspx) para más información.
>
>



<!--**Notes**: *Notes provide just-in-time info: A Note is “by hello way” info, an Important is info users need toocomplete a task, Tip is for shortcuts. Don’t overdo*.-->


<!--**Procedures**: *This is hello second “step." They often include substeps. Again, use a short title that tells users what they’ll do*. *("Configure a new web project.")*-->

<!--**UI**: *Note hello format for documenting hello UI: bold for UI elements and arrow keys for sequence. (Ex. Click **File > New > Project**.)*-->

<!--**Screenshot**: *Screenshots really help users. But don’t include too many since they’re difficult toomaintain. Highlight areas you are referring tooin red.*-->

<!--**No. of steps**: *Make sure hello number of steps within a procedure is 10 or fewer. Seven steps is ideal. Break up long procedure logically.*-->


<!--**Next steps**: *Reiterate what users have done, and give them interesting and useful next steps so they want toogo on.*-->

## <a name="next-steps"></a>Pasos siguientes

- [Agregar un equilibrador de carga de tooa de dirección IP para un segundo grupo de disponibilidad](virtual-machines-windows-portal-sql-ps-alwayson-int-listener.md#Add-IP).
