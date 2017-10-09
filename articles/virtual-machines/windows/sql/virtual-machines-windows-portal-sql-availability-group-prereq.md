---
title: "grupos de aaaSQL disponibilidad del servidor - máquinas virtuales de Azure: requisitos previos | Documentos de Microsoft"
description: "Este tutorial muestra cómo agrupar los requisitos previos de hello tooconfigure para crear una disponibilidad AlwaysOn de SQL Server en máquinas virtuales de Azure."
services: virtual-machines
documentationCenter: na
authors: MikeRayMSFT
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: c492db4c-3faa-4645-849f-5a1a663be55a
ms.service: virtual-machines-sql
ms.devlang: na
ms.custom: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/09/2017
ms.author: mikeray
ms.openlocfilehash: eed0729ead25c7793bb17a04cd7fd996c7dc8c9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="complete-hello-prerequisites-for-creating-always-on-availability-groups-on-azure-virtual-machines"></a>Requisitos previos de hello completa para crear grupos de disponibilidad AlwaysOn en máquinas virtuales de Azure

Este tutorial muestra cómo toocomplete Hola requisitos previos para crear una [SQL Server Always On availability group en máquinas virtuales (VM) Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md). Cuando haya terminado de requisitos previos de hello, tendrá un controlador de dominio, dos VM de SQL Server y un servidor testigo en un único grupo de recursos.

**Estimación del tiempo**: es posible que tarde un par de horas de los requisitos previos de toocomplete Hola. Gran parte de este tiempo se invierte en crear máquinas virtuales.

Hello siguiente diagrama muestra lo que crea en el tutorial de Hola.

![Grupo de disponibilidad](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/00-EndstateSampleNoELB.png)

## <a name="review-availability-group-documentation"></a>Revisión de la documentación del grupo de disponibilidad

En este tutorial se da por supuesto que tiene conocimientos básicos de grupos de disponibilidad de SQL Server AlwaysOn. Si no está familiarizado con esta tecnología, consulte [Información general de los grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/ff877884.aspx).


## <a name="create-an-azure-account"></a>Crear una cuenta de Azure
Necesitará una cuenta de Azure. Puede [abrir una cuenta gratuita de Azure](/pricing/free-trial/?WT.mc_id=A261C142F) o [activar las ventajas que disfrutan los suscriptores de Visual Studio](/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

## <a name="create-a-resource-group"></a>Crear un grupo de recursos
1. Inicie sesión en toohello [portal de Azure](http://portal.azure.com).
2. Haga clic en  **+**  toocreate un nuevo objeto en el portal de Hola.

   ![Nuevo objeto](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-portalplus.png)

3. Tipo de **grupo de recursos** en hello **Marketplace** ventana de búsqueda.

   ![Grupos de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroupsymbol.png)
4. Haga clic en **Grupo de recursos**.
5. Haga clic en **Crear**.
6. En hello **grupo de recursos** hoja, en **nombre del grupo de recursos**, escriba un nombre para el grupo de recursos de Hola. Por ejemplo, escriba **sql-ha-rg**.
7. Si tiene varias suscripciones de Azure, compruebe que suscripción hello es Hola suscripción de Azure que desee toocreate grupo de disponibilidad de hello en.
8. Seleccione una ubicación. ubicación de Hello es hello región de Azure donde desea que el grupo de disponibilidad de toocreate Hola. Para este tutorial, vamos toobuild todos los recursos en una ubicación de Azure.
9. Compruebe que **toodashboard Pin** está activada. Este valor opcional coloca un acceso directo para el grupo de recursos de hello en hello Azure panel del portal.

   ![Grupos de recursos](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/01-resourcegroup.png)

10. Haga clic en **crear** grupo de recursos de toocreate Hola.

Azure crea un grupo de recursos de toohello de método abreviado de grupo de recursos de Hola y PIN en el portal de Hola.

## <a name="create-hello-network-and-subnets"></a>Crear subredes y red de Hola
Hola siguiente paso es redes de hello toocreate y subredes en el grupo de recursos de Azure Hola.

solución de Hello usa una red virtual con dos subredes. Hola [información general de red Virtual](../../../virtual-network/virtual-networks-overview.md) proporciona más información acerca de las redes en Azure.

red virtual de Hola de toocreate:

1. Hola portal de Azure, en el grupo de recursos, haga clic en **+ agregar**. Hola de Azure abre **todo** hoja.

   ![Nuevo elemento](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/02-newiteminrg.png)
2. Busque **red virtual**.

     ![Búsqueda de una red virtual](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/04-findvirtualnetwork.png)
3. Haga clic en **Red virtual**.
4. En hello **red Virtual** hoja, haga clic en hello **el Administrador de recursos** modelo de implementación y, a continuación, haga clic en **crear**.

    Hello tabla siguiente muestran valores de hello de red virtual de hello:

   | **Campo** | Valor |
   | --- | --- |
   | **Name** |autoHAVNET |
   | **Espacio de direcciones** |10.33.0.0/24 |
   | **Nombre de subred** |Administrador |
   | **Intervalo de direcciones de subred** |10.33.0.0/29 |
   | **Suscripción** |Especifique la suscripción de Hola que piensa toouse. El campo **Suscripción** está en blanco si solo tiene una suscripción. |
   | **Grupos de recursos** |Elija **utilizar existente** y seleccione el nombre de Hola Hola del grupo de recursos. |
   | **Ubicación** |Especifique Hola ubicación de Azure. |

   El intervalo de direcciones de subred y de espacio de direcciones puede ser diferente de la tabla de Hola. Dependiendo de su suscripción, el portal de hello sugiere un espacio de direcciones disponible y el intervalo de direcciones de subred correspondiente. Si no hay suficiente espacio de direcciones disponible, use otra suscripción.

   ejemplo de Hola usa Hola nombre de subred **administración**. Esta subred es Hola para controladores de dominio.

5. Haga clic en **Crear**.

   ![Configurar una red virtual Hola](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/06-configurevirtualnetwork.png)

Azure devuelve toohello panel del portal y le avisa cuando se crea la nueva red de Hola.

### <a name="create-a-second-subnet"></a>Cree una segunda subred.
Hello nueva red virtual tiene una subred, denominada **administración**. los controladores de dominio de hello usan esta subred. Hola VM de SQL Server use una segunda subred denominada **SQL**. tooconfigure esta subred:

1. En el panel, haga clic en el grupo de recursos de Hola que ha creado, **SQL-HA-RG**. Busque red hello en el grupo de recursos de hello en **recursos**.

    Si **SQL-HA-RG** no está visible, buscar, haga clic en **grupos de recursos** y filtrar por nombre de grupo de recursos de Hola.
2. Haga clic en **autoHAVNET** en la lista de Hola de recursos. Azure abre una hoja de configuración de red de Hola.
3. En hello **autoHAVNET** hoja de red virtual, en **configuración** , haga clic en **subredes**.

    Subred de hello tenga en cuenta que se han creado previamente.

   ![Configurar una red virtual Hola](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/07-addsubnet.png)
5. Cree una segunda subred. Haga clic en **+ Subred**.
6. En hello **Agregar subred** hoja, configure subred Hola escribiendo **sqlsubnet** en **nombre**. Azure especifica automáticamente un valor válido en **Intervalo de direcciones**. Compruebe que este intervalo de direcciones tiene al menos 10 direcciones. En un entorno de producción, puede que necesite más direcciones.
7. Haga clic en **Aceptar**.

    ![Configurar una red virtual Hola](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/08-configuresubnet.png)

Hello en la tabla siguiente resume las opciones de configuración de red hello:

| **Campo** | Valor |
| --- | --- |
| **Name** |**autoHAVNET** |
| **Espacio de direcciones** |Este valor depende de los espacios de direcciones disponibles de hello en su suscripción. Un valor típico es 10.0.0.0/16. |
| **Nombre de subred** |**admin** |
| **Intervalo de direcciones de subred** |Este valor depende de los intervalos de direcciones disponibles de hello en su suscripción. Un valor típico es 10.0.0.0/24. |
| **Nombre de subred** |**sqlsubnet** |
| **Intervalo de direcciones de subred** |Este valor depende de los intervalos de direcciones disponibles de hello en su suscripción. Un valor típico es 10.0.1.0/24. |
| **Suscripción** |Especifique la suscripción de Hola que piensa toouse. |
| **Grupo de recursos** |**SQL-HA-RG** |
| **Ubicación** |Especificar Hola la misma ubicación que eligió para el grupo de recursos de Hola. |

## <a name="create-availability-sets"></a>Creación de conjuntos de disponibilidad

Antes de crear máquinas virtuales, debe toocreate conjuntos de disponibilidad. Conjuntos de disponibilidad de reducen el tiempo de inactividad de Hola para eventos de mantenimiento planeado o no. Un conjunto de disponibilidad de Azure es un grupo lógico de recursos que Azure coloca en dominios de error y de actualización físicos. Un dominio de error garantiza que miembros de Hola Hola del conjunto de disponibilidad tienen recursos de red y de alimentación independientes. Un dominio de actualización se asegura de que los miembros del conjunto de disponibilidad de hello no inactivo por mantenimiento Hola mismo tiempo. Para obtener más información, consulte [administrar Hola disponibilidad de máquinas virtuales](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Necesita dos conjuntos de disponibilidad. Uno es Hola para controladores de dominio. en segundo lugar, Hello es para las máquinas virtuales de hello SQL Server.

toocreate una disponibilidad establecido, grupo de recursos de toohello y haga clic en **agregar**. Filtrar los resultados de hello escribiendo **conjunto de disponibilidad**. Haga clic en **conjunto de disponibilidad** en Hola resultados y, a continuación, haga clic en **crear**.

Configurar dos conjuntos de disponibilidad según los parámetros de toohello en hello en la tabla siguiente:

| **Campo** | Conjunto de disponibilidad del controlador de dominio | Conjunto de disponibilidad de SQL Server |
| --- | --- | --- |
| **Name** |adavailabilityset |sqlavailabilityset |
| **Grupos de recursos** |SQL-HA-RG |SQL-HA-RG |
| **Dominios de error** |3 |3 |
| **Dominios de actualización** |5 |3 |

Después de crear conjuntos de disponibilidad de hello, devuelve el grupo de recursos de toohello de Hola portal de Azure.

## <a name="create-domain-controllers"></a>Creación de controladores de dominio
Después de crear red hello, subredes, conjuntos de disponibilidad y un equilibrador de carga a través de Internet, está listo toocreate Hola máquinas Hola para controladores de dominio.

### <a name="create-virtual-machines-for-hello-domain-controllers"></a>Crear máquinas virtuales para hello controladores de dominio
toocreate y configurar controladores de dominio de hello, devolver toohello **SQL-HA-RG** grupo de recursos.

1. Haga clic en **Agregar**. Hola **todo** abre la hoja.
2. Escriba **Windows Server 2016 Datacenter**.
3. Haga clic en **Windows Server 2016 Datacenter**. Hola **Windows Server 2016 Datacenter** hoja, comprobar dicho modelo de implementación de hello es **el Administrador de recursos**y, a continuación, haga clic en **crear**. Hola de Azure abre **crear máquina virtual** hoja.

Repita Hola anteriores pasos toocreate dos máquinas virtuales. Nombre de dos máquinas virtuales que hello:

* ad-primary-dc
* ad-secondary-dc

  > [!NOTE]
  > Hola **dc de ad secundaria** es opcional, la máquina virtual tooprovide alta disponibilidad para los servicios de dominio de Active Directory.
  >
  >

Hello tabla siguiente muestra valores de hello para estos dos equipos:

| **Campo** | Valor |
| --- | --- |
| **Name** |Primer controlador de dominio: *ad-primary-dc*.</br>Segundo controlador de dominio: *ad-secondary-dc*. |
| **Tipo de disco de máquina virtual** |SSD |
| **Nombre de usuario** |DomainAdmin |
| **Password** |Contoso!0000 |
| **Suscripción** |*Su suscripción* |
| **Grupos de recursos** |SQL-HA-RG |
| **Ubicación** |*Su ubicación* |
| **Tamaño** |DS1_V2 |
| **Storage** | **Usar discos administrados** - **Sí** |
| **Red virtual** |autoHAVNET |
| **Subred** |admin |
| **Dirección IP pública** |*Mismo nombre que Hola VM* |
| **Grupo de seguridad de red** |*Mismo nombre que Hola VM* |
| **El conjunto de disponibilidad** |adavailabilityset </br>**Dominios de error**: 2</br>**Dominios de actualización**: 2|
| **Diagnóstico** |Enabled |
| **Cuenta de almacenamiento de información de diagnóstico** |*Se crea automáticamente* |

   >[!IMPORTANT]
   >Solo puede colocar una máquina virtual en un conjunto de disponibilidad al crearlo. No se puede cambiar la disponibilidad de hello establecer después de crea una máquina virtual. Vea [administrar Hola disponibilidad de máquinas virtuales](../manage-availability.md).

Azure crea hello las máquinas virtuales.

Después de crear máquinas virtuales de hello, configure el controlador de dominio de Hola.

### <a name="configure-hello-domain-controller"></a>Configurar el controlador de dominio de Hola
Hola pasos siguientes, configurar hello **dc de ad principal** máquina como un controlador de dominio para corp.contoso.com.

1. En el portal de hello, abra hello **SQL-HA-RG** grupo de recursos y seleccione hello **dc de ad principal** máquina. En hello **dc de ad principal** hoja, haga clic en **conectar** tooopen un RDP de archivos para el acceso de escritorio remoto.

    ![Conectar máquina virtual de tooa](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/20-connectrdp.png)
2. Inicie sesión con su cuenta de administrador configurada (**\DomainAdmin**) y la contraseña (**Contoso!0000**).
3. De forma predeterminada, Hola **el administrador del servidor** se debe mostrar el panel.
4. Haga clic en hello **agregar roles y características** vínculo en el panel de Hola.

    ![Administrador del servidor: Agregar roles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
5. Seleccione **siguiente** hasta llegar toohello **Roles de servidor** sección.
6. Seleccione hello **los servicios de dominio de Active Directory** y **servidor DNS** roles. Cuando se le pida, agregue características adicionales que son necesarias para estos roles.

   > [!NOTE]
   > Windows le advierte de que no hay ninguna dirección IP estática. Si va a probar configuración de hello, haga clic en **continuar**. Para escenarios de producción, establezca toostatic de dirección IP de hello en hello portal de Azure, o [usar PowerShell tooset Hola dirección IP estática del equipo de controlador de dominio de hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   >
   >

    ![Cuadro de diálogo Agregar roles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/23-addroles.png)
7. Haga clic en **siguiente** hasta llegar a hello **confirmación** sección. Seleccione hello **reinicie el servidor de destino Hola automáticamente si es necesario** casilla de verificación.
8. Haga clic en **Instalar**.
9. Características de hello finalicen toohello de instalación, y se devuelve **el administrador del servidor** panel.
10. Seleccione Hola de nuevo **AD DS** opción en el panel izquierdo de Hola.
11. Haga clic en hello **más** vínculo en la barra de advertencia amarillo Hola.

    ![Cuadro de diálogo de AD DS en hello VM del servidor DNS](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/24-addsmore.png)
12. Hola **acción** columna de hello **todos los detalles de la tarea de servidor** cuadro de diálogo, haga clic en **promocionar este controlador de dominio de servidor tooa**.
13. Hola **Asistente para la configuración a los servicios de Active Directory dominio**, usar hello siguientes valores:

    | **Page** | Configuración |
    | --- | --- |
    | **Configuración de la implementación** |**Incorporación de nuevos bosques**<br/> **Nombre del dominio raíz** = corp.contoso.com |
    | **Opciones del controlador de dominio** |**Contraseña de DSRM** = Contoso!0000<br/>**Confirmar contraseña** = Contoso!0000 |
14. Haga clic en **siguiente** toogo a través de Hola a otras páginas de Asistente de Hola. En hello **comprobación de requisitos previos** página, compruebe que ve el siguiente mensaje de Hola: **todas las comprobaciones de requisitos previos se realizaron correctamente**. Puede revisar los mensajes de advertencia aplicables, pero es posible toocontinue con la instalación de Hola.
15. Haga clic en **Instalar**. Hola **dc de ad principal** máquina virtual se reiniciará automáticamente.

### <a name="note-hello-ip-address-of-hello-primary-domain-controller"></a>Tenga en cuenta dirección IP de Hola Hola principal del controlador de dominio

Usar el controlador de dominio principal de Hola para DNS. Anote la dirección IP de controlador de dominio principal de Hola.

Dirección IP de controlador de dominio principal de tooget unidireccional hello es a través de hello portal de Azure.

1. En hello portal de Azure, abra el grupo de recursos de Hola.

2. Haga clic en controlador de dominio principal de Hola.

3. En el módulo de controlador de dominio principal de hello, haga clic en **interfaces de red**.

![Interfaces de red](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/25-primarydcip.png)

Anote la dirección IP privada de Hola para este servidor.

### <a name="configure-hello-virtual-network-dns"></a>Configurar una red virtual Hola DNS
Después de crear el primer controlador de dominio de Hola y habilitación de DNS en el primer servidor de hello, configure toouse de red virtual de hello este servidor para DNS.

1. Hola portal de Azure, haga clic en la red virtual de Hola.

2. En **Configuración**, haga clic en **Servidor DNS**.

3. Haga clic en **personalizada**y escriba la dirección IP privada de Hola Hola principal del controlador de dominio.

4. Haga clic en **Guardar**.

### <a name="configure-hello-second-domain-controller"></a>Configurar el segundo controlador de dominio Hola
Después de que se reinicie el controlador de dominio principal de hello, puede configurar el segundo controlador de dominio Hola. Este paso opcional es para lograr alta disponibilidad. Siga estos pasos tooconfigure Hola segundo controlador de dominio:

1. En el portal de hello, abra hello **SQL-HA-RG** grupo de recursos y seleccione hello **dc de ad-base de datos secundaria** máquina. En hello **dc de ad secundaria** hoja, haga clic en **conectar** tooopen un RDP de archivos para el acceso de escritorio remoto.
2. Inicie sesión en toohello VM mediante su cuenta de administrador configurada (**BUILTIN\DomainAdmin**) y la contraseña (**Contoso! 0000**).
3. Hola de cambio de preferencia dirección toohello dirección del servidor DNS del controlador de dominio de Hola.
4. En **centro de redes y recursos compartidos**, haga clic en la interfaz de red de Hola.
   ![Interfaz de red](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/26-networkinterface.png)

5. Haga clic en **Propiedades**.
6. Seleccione **Protocolo de Internet versión 4 (TCP/IPv4)** y haga clic en **Propiedades**.
7. Seleccione **Hola de uso después de direcciones de servidor DNS** y especifique la dirección de Hola Hola principal del controlador de dominio **servidor DNS preferido**.
8. Haga clic en **Aceptar**y, a continuación, **cerrar** cambios de hello toocommit. Ya estás toojoin capaz de hello VM demasiado**corp.contoso.com**.

   >[!IMPORTANT]
   >Si pierde el escritorio remoto de hello conexión tooyour después de cambiar la configuración de DNS de hello, vaya toohello Azure portal y reinicio hello las máquinas virtuales.

9. En el controlador de dominio secundario de hello toohello de escritorio remoto, abra **panel Administrador del servidor**.
10. Haga clic en hello **agregar roles y características** vínculo en el panel de Hola.

    ![Administrador del servidor: Agregar roles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
11. Seleccione **siguiente** hasta llegar toohello **Roles de servidor** sección.
12. Seleccione hello **los servicios de dominio de Active Directory** y **servidor DNS** roles. Cuando se le pida, agregue características adicionales que son necesarias para estos roles.
13. Características de hello finalicen toohello de instalación, y se devuelve **el administrador del servidor** panel.
14. Seleccione Hola de nuevo **AD DS** opción en el panel izquierdo de Hola.
15. Haga clic en hello **más** vínculo en la barra de advertencia amarillo Hola.
16. Hola **acción** columna de hello **todos los detalles de la tarea de servidor** cuadro de diálogo, haga clic en **promocionar este controlador de dominio de servidor tooa**.
17. En **configuración de implementación**, seleccione **agregar un dominio existente de dominio controlador tooan**.
   ![Configuración de la implementación](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/28-deploymentconfig.png)
18. Haga clic en **Seleccionar**.
19. Conectar con cuenta de administrador de hello (**CORP. CONTOSO.COM\domainadmin**) y la contraseña (**Contoso! 0000**).
20. En **seleccione un dominio del bosque de hello**, haga clic en el dominio y, a continuación, haga clic en **Aceptar**.
21. En **opciones del controlador de dominio**, utilice valores predeterminados de Hola y establecer una contraseña DSRM.

   >[!NOTE]
   >Hola **opciones de DNS** página puede avisarle de que no se puede crear una delegación para este servidor DNS. Puede pasar por alto esta advertencia en entornos de no producción.
22. Haga clic en **siguiente** hasta que el cuadro de diálogo de hello alcance hello **requisitos previos** comprobar. Luego haga clic en **Instalar**.

Después de hello servidor deja de cambios de configuración de hello, reinicie el servidor hello.

### <a name="add-hello-private-ip-address-toohello-second-domain-controller-toohello-vpn-dns-server"></a>Agregar hello toohello dirección IP privada toohello de controlador de dominio segundo servidor de DNS de VPN

Hola portal de Azure, en la red virtual, cambie Hola servidor DNS tooinclude Hola dirección IP del controlador de dominio secundario de Hola. Esto permite la redundancia de servicios DNS de Hola.

### <a name=DomainAccounts></a>Configurar cuentas de dominio de Hola

En pasos de hello, configure las cuentas de Active Directory de Hola. Hello tabla siguiente muestran las cuentas de hello:

| |Cuenta de instalación<br/> |sqlserver-0 <br/>Cuenta del servicio Agente SQL y SQL Server |sqlserver-1<br/>Cuenta del servicio Agente SQL y SQL Server
| --- | --- | --- | ---
|**Nombre** |Instalar |SQLSvc1 | SQLSvc2
|**Usuario NombreDeCuentaSam** |Instalar |SQLSvc1 | SQLSvc2

Usar hello siguiendo los pasos toocreate cada cuenta.

1. Inicie sesión en toohello **dc de ad principal** máquina.
2. En **Administrador del servidor**, seleccione **Herramientas** y, después, haga clic en **Centro de administración de Active Directory**.   
3. Seleccione **corp (local)** en el panel izquierdo de Hola.
4. En el derecho de hello **tareas** panel, seleccione **New**y, a continuación, haga clic en **usuario**.
   ![Centro de administración de Active Directory](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/29-addcnewuser.png)

   >[!TIP]
   >Establezca una contraseña compleja para cada cuenta.<br/> Para entornos de no producción, toonever de cuenta de usuario de conjunto Hola expiran.

5. Haga clic en **Aceptar** toocreate usuario de Hola.
6. Repita los pasos anteriores para cada uno de tres cuentas de Hola de Hola.

### <a name="grant-hello-required-permissions-toohello-installation-account"></a>Conceder permisos de hello necesario toohello cuenta de instalación
1. Hola **centro de administración de Active Directory**, seleccione **corp (local)** en el panel izquierdo de Hola. A continuación, en hello derecho **tareas** panel, haga clic en **propiedades**.

    ![Propiedades de usuario CORP](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/31-addcproperties.png)
2. Seleccione **extensiones**y, a continuación, haga clic en hello **avanzadas** botón en hello **seguridad** ficha.
3. Hola **configuración de seguridad avanzada para corp** cuadro de diálogo, haga clic en **agregar**.
4. Haga clic en **Seleccionar una entidad de seguridad**, busque **CORP\Install** y, a continuación, haga clic en **Aceptar**.
5. Seleccione hello **leer todas las propiedades** casilla de verificación.

6. Seleccione hello **crear objetos de equipo** casilla de verificación.

     ![Permisos de usuario Corp](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/33-addpermissions.png)
7. Haga clic en **Aceptar** y luego vuelva a hacer clic en **Aceptar**. Hola cerrar **corp** ventana Propiedades.

Ahora que has terminado de configurar Active Directory y objetos de usuario de hello, cree dos VM de SQL Server y una máquina virtual del servidor testigo. A continuación, unir todos los tres dominio de toohello.

## <a name="create-sql-server-vms"></a>Creación de las máquinas virtuales con SQL Server

Cree tres máquinas virtuales adicionales. solución de Hello requiere dos máquinas virtuales con instancias de SQL Server. Una tercera máquina virtual funciona como testigo. Windows Server 2016 puede usar un [testigo en la nube](http://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness). No obstante, para mantener la coherencia con los sistemas operativos anteriores, este documento usa una máquina virtual como testigo.  

Antes de continuar, tenga en cuenta Hola después deisign decisiones.

* **Almacenamiento: Azure Managed Disks**

   Para el almacenamiento de máquina virtual de hello, use discos de Azure administrados. Microsoft recomienda el uso de Managed Disks para máquinas virtuales de SQL Server. El almacenamiento de identificadores de discos entre bastidores de hello administrado. Además, cuando las máquinas virtuales con discos administrados están en hello mismo conjunto de disponibilidad, Azure distribuye redundancia de tooprovide de recursos de almacenamiento de hello adecuado. Para más información, consulte [Introducción a Azure Managed Disks](../managed-disks-overview.md). Para obtener información específica acerca de Managed Disks en un conjunto de disponibilidad, consulte [Uso de Managed Disks para las máquinas virtuales de un conjunto de disponibilidad](../manage-availability.md#use-managed-disks-for-vms-in-an-availability-set).

* **Red: direcciones IP privadas en producción**

   Para las máquinas virtuales de hello, este tutorial usa direcciones IP públicas. Esto permite establecer conexiones remotas directamente Hola a toohello máquina virtual a través de internet: facilita pasos de configuración. En entornos de producción, Microsoft recomienda sólo direcciones IP privadas en orden tooreduce Hola de vulnerabilidad de instancia de SQL Server de hello recurso de máquina virtual.

### <a name="create-and-configure-hello-sql-server-vms"></a>Crear y configurar las máquinas virtuales de hello SQL Server
A continuación, cree tres máquinas virtuales: dos de SQL Server y una para el nodo de clúster adicional. toocreate de máquinas virtuales de hello, vuelva atrás toohello **SQL-HA-RG** grupo de recursos, haga clic en **agregar**, buscar Hola correspondiente elemento de galería, haga clic en **Máquina Virtual**y, a continuación, Haga clic en **de la galería**. Utilice la información de Hola Hola después toohelp tabla crear máquinas virtuales de hello:


| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Seleccionar elemento de galería adecuado de Hola |**Windows Server 2016 Datacenter** |**SQL Server 2016 SP1 Enterprise en Windows Server 2016** |**SQL Server 2016 SP1 Enterprise en Windows Server 2016** |
| Configuración de máquina virtual: **Datos básicos** |**Nombre** = clúster-fsw<br/>**Nombre de usuario** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Suscripción** = su suscripción<br/>**Grupo de recursos** = SQL-HA-GR<br/>**Ubicación** = Su ubicación de Azure |**Nombre** = sqlserver-0<br/>**Nombre de usuario** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Suscripción** = su suscripción<br/>**Grupo de recursos** = SQL-HA-GR<br/>**Ubicación** = Su ubicación de Azure |**Nombre** = sqlserver-1<br/>**Nombre de usuario** = DomainAdmin<br/>**Password** = Contoso!0000<br/>**Suscripción** = su suscripción<br/>**Grupo de recursos** = SQL-HA-GR<br/>**Ubicación** = Su ubicación de Azure |
| Configuración de máquina virtual: **Tamaño** |**SIZE** = DS1\_V2 (1 núcleo, 3,5 GB) |**TAMAÑO** = DS2\_V2 (2 núcleos y 7 GB)</br>tamaño de Hello debe admitir el almacenamiento SSD (soporte de disco Premium. )) |**TAMAÑO** = DS2\_V2 (2 núcleos y 7 GB) |
| Configuración de máquina virtual: **Configuración** |**Storage**: use Managed Disks.<br/>**Red virtual** = autoHAVNET<br/>**Subred** = sqlsubnet(10.1.1.0/24)<br/>**Dirección IP pública** generada automáticamente.<br/>**Grupo de seguridad de red** = ninguno<br/>**Diagnósticos de supervisión** = habilitado<br/>**Cuenta de almacenamiento de diagnósticos** = usar una cuenta de almacenamiento generada automáticamente<br/>**Conjunto de disponibilidad** = sqlAvailabilitySet<br/> |**Storage**: use Managed Disks.<br/>**Red virtual** = autoHAVNET<br/>**Subred** = sqlsubnet(10.1.1.0/24)<br/>**Dirección IP pública** generada automáticamente.<br/>**Grupo de seguridad de red** = ninguno<br/>**Diagnósticos de supervisión** = habilitado<br/>**Cuenta de almacenamiento de diagnósticos** = usar una cuenta de almacenamiento generada automáticamente<br/>**Conjunto de disponibilidad** = sqlAvailabilitySet<br/> |**Storage**: use Managed Disks.<br/>**Red virtual** = autoHAVNET<br/>**Subred** = sqlsubnet(10.1.1.0/24)<br/>**Dirección IP pública** generada automáticamente.<br/>**Grupo de seguridad de red** = ninguno<br/>**Diagnósticos de supervisión** = habilitado<br/>**Cuenta de almacenamiento de diagnósticos** = usar una cuenta de almacenamiento generada automáticamente<br/>**Conjunto de disponibilidad** = sqlAvailabilitySet<br/> |
| Configuración de máquina virtual: **Configuración de SQL Server** |No aplicable |**Conectividad de SQL** = privado (dentro de la red virtual)<br/>**Puerto** = 1433<br/>**Autenticación SQL** = deshabilitar<br/>**Configuración de almacenamiento** = general<br/>**Aplicación de revisiones automatizada** = el domingo a las 2:00<br/>**Copia de seguridad automatizada** = deshabilitado</br>**Integración del Almacén de claves de Azure** = Deshabilitada |**Conectividad de SQL** = privado (dentro de la red virtual)<br/>**Puerto** = 1433<br/>**Autenticación SQL** = deshabilitar<br/>**Configuración de almacenamiento** = general<br/>**Aplicación de revisiones automatizada** = el domingo a las 2:00<br/>**Copia de seguridad automatizada** = deshabilitado</br>**Integración del Almacén de claves de Azure** = Deshabilitada |

<br/>

> [!NOTE]
> tamaños de máquina de Hello sugeridos están diseñados para probar los grupos de disponibilidad en máquinas virtuales de Azure. Para obtener el mejor rendimiento de hello en cargas de trabajo de producción, vea las recomendaciones de Hola para tamaños de máquina de SQL Server y la configuración de [prácticas recomendadas de rendimiento para SQL Server en máquinas virtuales de Azure](virtual-machines-windows-sql-performance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
>
>

Después de hello tres las máquinas virtuales están completamente aprovisionadas, necesita toojoin les toohello **corp.contoso.com** máquinas de toohello de derechos administrativos CORP\Install dominio y grant.

### <a name="joinDomain"></a>Unirse a dominio de hello servidores toohello

Está ahora toojoin capaz de Hola máquinas virtuales demasiado**corp.contoso.com**. Lo siguiente de Hola para VM de SQL Server de Hola y el archivo hello comparta servidor testigo:

1. Conectarse de forma remota la máquina virtual toohello con **BUILTIN\DomainAdmin**.
2. En **Administrador del servidor**, haga clic en **Servidor local**.
3. Haga clic en hello **WORKGROUP** vínculo.
4. Hola **nombre_equipo** sección, haga clic en **cambio**.
5. Seleccione hello **dominio** casilla de verificación y tipo **corp.contoso.com** en el cuadro de texto de Hola. Haga clic en **Aceptar**.
6. Hola **la seguridad de Windows** cuadro de diálogo emergente, especifique las credenciales de hello para la cuenta de administrador de dominio predeterminado de hello (**CORP\DomainAdmin**) y la contraseña de hello (**Contoso! 0000**).
7. Cuando vea el mensaje de "dominio de corp.contoso.com bienvenida toohello" Hola, haga clic en **Aceptar**.
8. Haga clic en **cerrar**y, a continuación, haga clic en **reiniciar ahora** en el cuadro de diálogo de hello emergente.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-cluster-vm"></a>Agregar usuario de hello Corp\Install como un administrador en cada máquina virtual de clúster

Después de cada máquina virtual se reinicia como un miembro de dominio de hello, agregar **CORP\Install** como miembro del grupo de administradores locales de Hola.

1. Espere hasta que se reinicie Hola VM e inicie el archivo RDP de hello nuevo desde toosign de controlador de dominio principal de hello en demasiado**sqlserver 0** mediante el uso de hello **CORP\DomainAdmin** cuenta.
   >[!TIP]
   >Asegúrese de que inicie sesión con la cuenta de administrador de dominio de Hola. En pasos anteriores de hello, usaba cuenta de administrador integrado Hola. Ahora que hello server está en el dominio de hello, usar la cuenta de dominio de Hola. En la sesión RDP, especifique *DOMINIO*\\*nombre de usuario*.

2. En **Administrador del servidor** seleccione **Herramientas** y después haga clic en **Administración de equipos**.
3. Hola **administración de equipos** ventana, expanda **usuarios y grupos locales**y, a continuación, seleccione **grupos**.
4. Haga doble clic en hello **administradores** grupo.
5. Hola **propiedades de administradores de** cuadro de diálogo, haga clic en hello **agregar** botón.
6. Escriba Hola usuario **CORP\Install**y, a continuación, haga clic en **Aceptar**.
7. Haga clic en **Aceptar** tooclose hello **propiedades del Administrador de** cuadro de diálogo.
8. Repita los pasos anteriores de hello en **sqlserver-1** y **clúster fsw**.

### <a name="setServiceAccount"></a>Configuración de las cuentas de servicio de SQL Server Hola

En cada VM de SQL Server, establezca la cuenta de servicio de SQL Server de Hola. Usar cuentas de Hola que creó cuando se [configurado las cuentas de dominio de hello](#DomainAccounts).

1. Abra el **Administrador de configuración de SQL Server**.
2. Haga clic en el servicio de SQL Server de hello y, a continuación, haga clic en **propiedades**.
3. Conjunto Hola cuenta y una contraseña.
4. Repita estos pasos en hello otras VM de SQL Server.  

Para los grupos de disponibilidad de SQL Server, cada VM de SQL Server debe toorun como una cuenta de dominio.

### <a name="create-a-sign-in-on-each-sql-server-vm-for-hello-installation-account"></a>Crear una inicio de sesión de en cada VM de SQL Server para la cuenta de instalación de Hola

Usar grupo de disponibilidad de hello instalación cuenta (CORP\install) tooconfigure Hola. Esta cuenta debe toobe un miembro de hello **sysadmin** rol fijo de servidor en cada máquina virtual de SQL Server. Hello pasos siguientes crea un inicio de sesión de cuenta de instalación de hello:

1. Conectar el servidor de toohello a través del protocolo de escritorio remoto (RDP) de Hola mediante hello  *\<MachineName\>\DomainAdmin* cuenta.

1. Abra SQL Server Management Studio y conéctese toohello la instancia local de SQL Server.

1. En **Explorador de objetos**, haga clic en **Seguridad**.

1. Haga clic con el botón derecho en **Inicios de sesión**. Haga clic en **Nuevo inicio de sesión**.

1. En **Inicio de sesión - Nuevo**, haga clic en **Buscar**.

1. Haga clic en **Ubicaciones**.

1. Escriba las credenciales de red de administrador de dominio de Hola.

1. Usar cuenta de instalación de Hola.

1. Establecer Hola inicio de sesión toobe un miembro de hello **sysadmin** rol fijo de servidor.

1. Haga clic en **Aceptar**.

Repita Hola anteriores pasos en hello otras VM de SQL Server.

## <a name="add-failover-clustering-features-tooboth-sql-server-vms"></a>Agregar tooboth de características de agrupación en clústeres de conmutación por error las máquinas virtuales de SQL Server

Hola tooadd características de agrupación en clústeres de conmutación por error, siga en ambas máquinas virtuales de SQL Server:

1. Conectar máquina virtual de SQL Server de toohello a través del protocolo de escritorio remoto (RDP) de Hola mediante hello *CORP\install* cuenta. Abra el **panel Administrador de servidores**.
2. Haga clic en hello **agregar roles y características** vínculo en el panel de Hola.

    ![Administrador del servidor: Agregar roles](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/22-addfeatures.png)
3. Seleccione **siguiente** hasta llegar toohello **características de servidor** sección.
4. En **Características**, seleccione **Clúster de conmutación por error**.
5. Agregue más características necesarias.
6. Haga clic en **instalar** características de hello tooadd.

Repita los pasos de hello en hello otras VM de SQL Server.

## <a name="a-nameendpoint-firewall-configure-hello-firewall-on-each-sql-server-vm"></a><a name="endpoint-firewall">Configurar el firewall de hello en cada máquina virtual de SQL Server

solución de Hello requiere Hola siguiendo los puertos TCP toobe abrir en firewall de hello:

- **Máquina virtual con SQL Server**:<br/>
   Puerto 1433 para una instancia predeterminada de SQL Server.
- **Sondeo de Azure Load Balancer:**<br/>
   Cualquier puerto disponible. A menudo, los ejemplos utilizan el 59999.
- **Punto de conexión de reflejo de la base de datos:** <br/>
   Cualquier puerto disponible. A menudo, los ejemplos utilizan el 5022.

Hola firewall puertos necesidad toobe abierto en ambos VM de SQL Server.

método Hello de la apertura de puertos de hello depende de la solución de firewall de Hola que usar. Hola próxima sección explica cómo hello tooopen puertos en Firewall de Windows. Abrir los puertos de hello necesario en cada uno de sus máquinas virtuales de SQL Server.

### <a name="open-a-tcp-port-in-hello-firewall"></a>Abrir un puerto TCP en firewall de Hola

1. En Hola primer servidor SQL Server **iniciar** pantalla, inicie **Firewall de Windows con seguridad avanzada**.
2. En el panel izquierdo de hello, seleccione **reglas de entrada**. En el panel derecho de hello, haga clic en **nueva regla**.
3. En **Tipo de regla**, elija **Puerto**.
4. Para el puerto de hello, especifique **TCP** y Hola de tipo adecuado de números de puerto. Vea el siguiente ejemplo de Hola:

   ![Firewall de SQL](./media/virtual-machines-windows-portal-sql-availability-group-tutorial/35-tcpports.png)

5. Haga clic en **Siguiente**.
6. En hello **acción** página, mantenga **Permitir conexión hello** seleccionada y, a continuación, haga clic en **siguiente**.
7. En hello **perfil** página, acepte la configuración predeterminada de hello y, a continuación, haga clic en **siguiente**.
8. En hello **nombre** página, especifique un nombre de regla (como **Azure LB sondeo**) en hello **nombre** cuadro de texto y, a continuación, haga clic en **finalizar**.

Repita estos pasos en Hola segunda VM de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

* [Creación de un grupo de disponibilidad de SQL Server AlwaysOn en máquinas virtuales de Azure](virtual-machines-windows-portal-sql-availability-group-tutorial.md)
