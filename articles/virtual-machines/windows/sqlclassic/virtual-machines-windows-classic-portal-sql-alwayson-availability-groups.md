---
title: "aaaConfigure siempre en el grupo de disponibilidad en máquinas virtuales de Azure (clásica) | Documentos de Microsoft"
description: Cree un grupo de disponibilidad AlwaysOn con Azure Virtual Machines. Este tutorial usa principalmente la interfaz de usuario de Hola y herramientas en lugar de secuencias de comandos.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 8d48a3d2-79f8-4ab0-9327-2f30ee0b2ff1
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: f428ad994a55378c281c959f4696fdcaf50632b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-group-in-azure-virtual-machines-classic"></a>Configuración de grupos de disponibilidad Always On en Azure Virtual Machines (implementación clásica)
> [!div class="op_single_selector"]
> * [Portal de Azure clásico: interfaz de usuario](../classic/portal-sql-alwayson-availability-groups.md)
> * [Clásico: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Antes de comenzar, considere que ahora puede completar esta tarea en un modelo de Azure Resource Manager. Se recomienda el modelo de Azure Resource Manager para las implementaciones nuevas. Consulte [Grupos de disponibilidad de SQL Server AlwaysOn en máquinas virtuales de Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT] 
> Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola. Azure tiene dos toocreate de modelos de implementación diferentes y trabajar con recursos: [Administrador de recursos y clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo explica cómo toouse Hola modelo de implementación clásica. 

Esta tarea con el modelo de hello Azure Resource Manager, consulte el toocomplete [grupos de disponibilidad de AlwaysOn de SQL Server en máquinas virtuales de Azure](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

Este tutorial to-end muestra cómo los grupos de disponibilidad tooimplement mediante el uso de SQL Server Always On ejecutar máquinas virtuales de Azure.

Al final de Hola de tutorial de hello, la solución SQL Server Always On en Azure constará de hello siguientes elementos:

* Una red virtual que contiene varias subredes, incluida una subred front-end y back-end
* Un controlador de dominio con un dominio de Active Directory (Azure AD)
* Dos máquinas virtuales que ejecutan SQL Server y subred de back-end de implementada toohello y dominio toohello unido a Azure AD
* Un clúster de conmutación por error de tres nodos con el modelo de quórum de mayoría de nodo de Hola
* Un grupo de disponibilidad que tiene dos réplicas de confirmación sincrónica de una base de datos de disponibilidad

Hola siguiente ilustración es una representación gráfica de la solución de Hola.

![Arquitectura de pruebas para grupos de disponibilidad en Azure](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC791912.png)

Tenga en cuenta que se trata de una de las posibles configuraciones. Por ejemplo, puede minimizar el número de Hola de máquinas virtuales para un grupo de disponibilidad de dos réplicas. Esta configuración se guarda en horas de proceso de Azure mediante el controlador de dominio de hello como testigo de recurso compartido de archivos de hello quórum en un clúster de dos nodos. Este método reduce Hola recuento de máquinas virtuales en uno de configuración se muestra de Hola.

Este tutorial se da por supuesto siguiente hello:

* Ya tiene una cuenta de Azure.
* Ya sabe cómo toouse Hola GUI en tooprovision de galería de máquina virtual de hello una máquina virtual clásica que ejecuta SQL Server.
* Ya tiene un conocimiento sólido de los grupos de disponibilidad AlwaysOn. Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Si le interesa utilizar los grupos de disponibilidad Always On con SharePoint, consulte también [Configuración de grupos de disponibilidad AlwaysOn de SQL Server 2012 para SharePoint 2013](https://technet.microsoft.com/library/jj715261.aspx).
> 
> 

## <a name="create-hello-virtual-network-and-domain-controller-server"></a>Crear red virtual de Hola y servidor de controlador de dominio
Comience con una nueva cuenta de prueba de Azure. Después de configurar la cuenta, debe tener en pantalla de inicio de Hola de hello portal de Azure clásico.

1. Haga clic en hello **New** situado en la esquina izquierda de saludo de la parte inferior de Hola de página de hello, como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Haga clic en nuevo en el portal de Hola](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665511.gif)
2. Haga clic en **servicios de red** > **red Virtual** > **creación personalizada**, tal y como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Crear red virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665512.gif)
3. Hola **crear una red VIRTUAL** diálogo cuadro, cree una nueva red virtual recorriendo las páginas de Hola y con la configuración de hello en hello en la tabla siguiente. 
   
   | Page | Settings |
   | --- | --- |
   | Detalles de red virtual |**NOMBRE = ContosoNET**<br/>**REGIÓN = Oeste de EE. UU.** |
   | Servidores DNS y conectividad VPN |None |
   | Espacios de direcciones de la red virtual |Configuración se muestra en la siguiente captura de pantalla de hello: ![Crear red virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784620.png) |
4. Crear máquina virtual de Hola que va a utilizar como controlador de dominio (DC) de Hola. Haga clic en **New** > **proceso** > **Máquina Virtual** > **de la galería**, tal y como se muestra en Hola siguiente captura de pantalla.
   
    ![de una máquina virtual](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784621.png)
5. Hola **crear una máquina VIRTUAL** diálogo cuadro, configure una nueva máquina virtual recorriendo las páginas de Hola y con la configuración de hello en hello en la tabla siguiente. 
   
   | Page | Settings |
   | --- | --- |
   | Seleccione el sistema operativo de máquina virtual de Hola |Windows Server 2012 R2 Datacenter |
   | Configuración de la máquina virtual |**FECHA DE LANZAMIENTO DE LA VERSIÓN** = (última)<br/>**NOMBRE DE MÁQUINA VIRTUAL** = ContosoDC<br/>**NIVEL**: ESTÁNDAR<br/>**TAMAÑO** = A2 (2 núcleos)<br/>**NUEVO NOMBRE de USUARIO** = AzureAdmin<br/>**NUEVA CONTRASEÑA** = Contoso!000<br/>**CONFIRMAR** = Contoso!000 |
   | Configuración de la máquina virtual |**SERVICIO EN LA NUBE**: Crear un nuevo servicio en la nube<br/>**NOMBRE DE DNS DEL SERVICIO EN LA NUBE** = un nombre de servicio en la nube único<br/>**NOMBRE DNS** = un nombre único (por ejemplo, ContosoDC123)<br/>**REGION/GRUPO DE AFINIDAD/RED VIRTUAL** = ContosoNET<br/>**SUBREDES DE LA RED VIRTUAL** = Back(10.10.2.0/24)<br/>**CUENTA DE ALMACENAMIENTO** = usar una cuenta de almacenamiento generada automáticamente<br/>**CONJUNTO DE DISPONIBILIDAD**: (Ninguno) |
   | Opciones de la máquina virtual |Usar predeterminados |

Después de configurar la nueva máquina virtual de hello, espere Hola máquina virtual toobe aprovisione. Este proceso tarda algún tiempo toofinish. Si hace clic en hello **Máquina Virtual** ficha hello Azure clásico portal, puede ver los Estados de ciclismo ContosoDC desde **iniciando (aprovisionamiento)** demasiado**detenido**, **a partir de**, **ejecución (aprovisionamiento)**y, finalmente, **ejecutando**.

servidor de DC de Hello ahora se aprovisionó correctamente. A continuación, configurará el dominio de Active Directory de hello en este servidor de controlador de dominio.

## <a name="configure-hello-domain-controller"></a>Configurar el controlador de dominio de Hola
Hola pasos, configura hello ContosoDC máquina como un controlador de dominio para corp.contoso.com.

1. En el portal de hello, seleccione hello **ContosoDC** máquina. En hello **panel** , haga clic en **conectar** tooopen un escritorio remoto (RDP) de archivos para el acceso de escritorio remoto.
   
    ![Conectar tooVritual máquina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784622.png)
2. Inicie sesión con su cuenta de administrador configurada (**\AzureAdmin**) y la contraseña (**Contoso!000**).
3. De forma predeterminada, Hola **el administrador del servidor** se debe mostrar el panel.
4. Haga clic en hello **agregar roles y características** vínculo en el panel de Hola.
   
    ![Explorador de servidores Agregar roles](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784623.png)
5. Haga clic en **siguiente** hasta llegar toohello **Roles de servidor** sección.
6. Seleccione hello **los servicios de dominio de Active Directory** y **servidor DNS** roles. Cuando se le solicite, agregue más características que requieran estos roles.
   
   > [!NOTE]
   > Recibirá una advertencia de validación que le indicará que no hay ninguna dirección IP estática. Si va a probar la configuración de hello, haga clic en **continuar**. Los escenarios de producción [usar PowerShell tooset Hola dirección IP estática del equipo de controlador de dominio de hello](../../../virtual-network/virtual-networks-reserved-private-ip.md).
   > 
   > 
   
    ![Diálogo Agregar roles](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784624.png)
7. Haga clic en **siguiente** hasta llegar a hello **confirmación** sección. Seleccione hello **reinicie el servidor de destino Hola automáticamente si es necesario** casilla de verificación.
8. Haga clic en **Instalar**.
9. Después de instalan características de hello, devolver toohello **el administrador del servidor** panel.
10. Seleccione Hola de nuevo **AD DS** opción en el panel izquierdo de Hola.
11. Haga clic en hello **más** vínculo en la barra de advertencia amarillo Hola.
    
     ![Cuadro de diálogo de AD DS en la máquina virtual del servidor DNS](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784625.png)
12. Hola **acción** columna de hello **todos los detalles de la tarea de servidor** cuadro de diálogo, haga clic en **promocionar este controlador de dominio de servidor tooa**.
13. Hola **Asistente para la configuración a los servicios de Active Directory dominio**, usar hello siguientes valores:
    
    | Page | Configuración |
    | --- | --- |
    | Configuración de la implementación |**Agregar un nuevo bosque** = seleccionado<br/>**Nombre del dominio raíz** = corp.contoso.com |
    | Opciones del controlador de dominio |**Password** = Contoso!000<br/>**Confirmar contraseña** = Contoso!000 |
14. Haga clic en **siguiente** toogo a través de Hola a otras páginas de Asistente de Hola. En hello **comprobación de requisitos previos** página, compruebe que ve el siguiente mensaje de Hola: **todas las comprobaciones de requisitos previos se realizaron correctamente**. Tenga en cuenta que debe revisar todos los mensajes de advertencia aplicables, pero es posible toocontinue con la instalación de Hola.
15. Haga clic en **Instalar**. Hola **ContosoDC** máquina virtual se reiniciará automáticamente.

## <a name="configure-domain-accounts"></a>Configuración de cuentas de dominio
pasos siguientes Hola configuran cuentas de Active Directory de Hola para su uso posterior.

1. Inicio de sesión de nuevo en toohello **ContosoDC** máquina.
2. En **Administrador del servidor**, haga clic en **Herramientas** > **Centro de administración de Active Directory**.
   
    ![Centro de administración de Active Directory](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784626.png)
3. Hola **centro de administración de Active Directory**, seleccione **corp (local)** en el panel izquierdo de Hola.
4. En el derecho de hello **tareas** panel, haga clic en **New** > **usuario**. Usar hello después de configuración:
   
   | Configuración | Valor |
   | --- | --- |
   | **Nombre** |Instalar |
   | **Usuario NombreDeCuentaSam** |Instalar |
   | **Password** |Contoso!000 |
   | **Confirmar contraseña** |Contoso!000 |
   | **Otras opciones de contraseña** |Seleccionado |
   | **La contraseña nunca expira** |Activado |
5. Haga clic en **Aceptar** toocreate hello **instalar** usuario. Esta cuenta será usado tooconfigure Hola conmutación por error hello y clúster de grupo de disponibilidad.
6. Crear dos usuarios adicionales, **CORP\SQLSvc1** y **CORP\SQLSvc2**, con hello mismos pasos. Estas cuentas se utilizarán para las instancias de SQL Server de Hola. A continuación, debe toogive **CORP\Install** Hola clústeres de conmutación por error de Windows tooconfigure permisos necesarios.
7. Hola **centro de administración de Active Directory**, haga clic en **corp (local)** en el panel izquierdo de Hola. Hola **tareas** panel, haga clic en **propiedades**.
   
    ![Propiedades de usuario CORP](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784627.png)
8. Seleccione **extensiones**y, a continuación, haga clic en hello **avanzadas** botón en hello **seguridad** ficha.
9. Hola **configuración de seguridad avanzada para corp** cuadro de diálogo, haga clic en **agregar**.
10. Haga clic en **Seleccionar una entidad de seguridad**, busque **CORP\Install** y, a continuación, haga clic en **Aceptar**.
11. Seleccione hello **leer todas las propiedades** y **crear objetos de equipo** permisos.
    
     ![Permisos de usuario Corp](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784628.png)
12. Haga clic en **Aceptar** y luego vuelva a hacer clic en **Aceptar**. Ventana de propiedades de corp Hola cerrar.

Ahora que ha configurado Active Directory y objetos de usuario de hello, creará tres máquinas virtuales de SQL Server y combinarlos toothis dominio.

## <a name="create-hello-sql-server-virtual-machines"></a>Crear Hola máquinas virtuales de SQL Server
Cree tres máquinas virtuales. Una es para un nodo de clúster y dos para SQL Server. toocreate de máquinas virtuales de hello, ir atrás toohello portal de Azure clásico, haga clic en **New** > **proceso** > **Máquina Virtual**  >  **De galería**. A continuación, use plantillas de hello en hello después toohelp de tabla para crear máquinas virtuales de Hola.

| Page | VM1 | VM2 | VM3 |
| --- | --- | --- | --- |
| Seleccione el sistema operativo de máquina virtual de Hola |**Windows Server 2012 R2 Datacenter** |**SQL Server 2014 RTM Enterprise** |**SQL Server 2014 RTM Enterprise** |
| Configuración de la máquina virtual |**FECHA DE LANZAMIENTO DE LA VERSIÓN** = (última)<br/>**NOMBRE DE LA MÁQUINA VIRTUAL** = ContosoWSFCNode<br/>**NIVEL**: ESTÁNDAR<br/>**TAMAÑO** = A2 (2 núcleos)<br/>**NUEVO NOMBRE de USUARIO** = AzureAdmin<br/>**NUEVA CONTRASEÑA** = Contoso!000<br/>**CONFIRMAR** = Contoso!000 |**FECHA DE LANZAMIENTO DE LA VERSIÓN** = (última)<br/>**NOMBRE DE MÁQUINA VIRTUAL** = ContosoSQL1<br/>**NIVEL**: ESTÁNDAR<br/>**TAMAÑO** = A3 (4 núcleos)<br/>**NUEVO NOMBRE de USUARIO** = AzureAdmin<br/>**NUEVA CONTRASEÑA** = Contoso!000<br/>**CONFIRMAR** = Contoso!000 |**FECHA DE LANZAMIENTO DE LA VERSIÓN** = (última)<br/>**NOMBRE DE MÁQUINA VIRTUAL** = ContosoSQL2<br/>**NIVEL**: ESTÁNDAR<br/>**TAMAÑO** = A3 (4 núcleos)<br/>**NUEVO NOMBRE de USUARIO** = AzureAdmin<br/>**NUEVA CONTRASEÑA** = Contoso!000<br/>**CONFIRMAR** = Contoso!000 |
| Configuración de la máquina virtual |**SERVICIO EN LA NUBE** = nombre DNS del servicio en la nube único creado anteriormente (por ejemplo, ContosoDC123)<br/>**REGION/GRUPO DE AFINIDAD/RED VIRTUAL** = ContosoNET<br/>**SUBREDES DE LA RED VIRTUAL** = Back(10.10.2.0/24)<br/>**CUENTA DE ALMACENAMIENTO** = usar una cuenta de almacenamiento generada automáticamente<br/>**CONJUNTO DE DISPONIBILIDAD** = Crear un conjunto de disponibilidad<br/>**NOMBRE DEL CONJUNTO DE DISPONIBILIDAD** = SQLHADR |**SERVICIO EN LA NUBE** = nombre DNS del servicio en la nube único creado anteriormente (por ejemplo, ContosoDC123)<br/>**REGION/GRUPO DE AFINIDAD/RED VIRTUAL** = ContosoNET<br/>**SUBREDES DE LA RED VIRTUAL** = Back(10.10.2.0/24)<br/>**CUENTA DE ALMACENAMIENTO** = usar una cuenta de almacenamiento generada automáticamente<br/>**CONJUNTO de disponibilidad** = SQLHADR (también puede configurar conjunto una vez creada la máquina de Hola de disponibilidad de Hola. Las tres máquinas deben asignarse conjunto de disponibilidad SQLHADR toohello.) |**SERVICIO EN LA NUBE** = nombre DNS del servicio en la nube único creado anteriormente (por ejemplo, ContosoDC123)<br/>**REGION/GRUPO DE AFINIDAD/RED VIRTUAL** = ContosoNET<br/>**SUBREDES DE LA RED VIRTUAL** = Back(10.10.2.0/24)<br/>**CUENTA DE ALMACENAMIENTO** = usar una cuenta de almacenamiento generada automáticamente<br/>**CONJUNTO de disponibilidad** = SQLHADR (también puede configurar conjunto una vez creada la máquina de Hola de disponibilidad de Hola. Las tres máquinas deben asignarse conjunto de disponibilidad SQLHADR toohello.) |
| Opciones de la máquina virtual |Usar predeterminados |Usar predeterminados |Usar predeterminados |

<br/>

> [!NOTE]
> configuración anterior de Hello sugiere máquinas virtuales de nivel estándar, porque las máquinas de nivel básico no admiten extremos con equilibrio de carga. Necesita extremos con equilibrio de carga toocreate más adelante un agente de escucha del grupo de disponibilidad. Además, los tamaños de máquina de Hola que se sugieren aquí están diseñados para las pruebas de los grupos de disponibilidad en máquinas virtuales de Azure. Para obtener el mejor rendimiento de hello en cargas de trabajo de producción, vea las recomendaciones de Hola para tamaños de máquina de SQL Server y la configuración de [prácticas recomendadas de rendimiento para SQL Server en máquinas virtuales Azure](../sql/virtual-machines-windows-sql-performance.md).
> 
> 

Después de hello tres las máquinas virtuales están completamente aprovisionadas, necesita toojoin les toohello **corp.contoso.com** máquinas de toohello de derechos administrativos CORP\Install dominio y grant. toodo, Hola uso siguiendo los pasos para cada una de las máquinas virtuales Hola tres.

1. En primer lugar, cambie la dirección del servidor DNS preferido de Hola. Descargar el directorio local de cada máquina virtual RDP archivo tooyour seleccionando la máquina virtual de hello en lista de Hola y haciendo clic en hello **conectar** botón. tooselect una máquina virtual, haga clic en cualquier pero la primera celda de hello en fila hello, como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Descargar archivo RDP de hello](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664953.jpg)
2. Abra Hola RDP archivo que descargó e inicie sesión en la máquina virtual de toohello mediante su cuenta de administrador configurada (**BUILTIN\AzureAdmin**) y la contraseña (**Contoso! 000**).
3. Después de iniciar la sesión, debería ver Hola **el administrador del servidor** panel. Haga clic en **servidor Local** en el panel izquierdo de Hola.
4. Haga clic en hello **dirección IPv4 asignada por DHCP, IPv6 habilitado** vínculo.
5. Hola **las conexiones de red** diálogo cuadro, haga clic en el icono de red de Hola.
   
    ![Cambiar servidor de DNS de máquina virtual preferido de Hola](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784629.png)
6. En la barra de comandos de hello, haga clic en **cambiar la configuración de Hola de esta conexión**. (Según el tamaño de saludo de la ventana, puede que tenga tooclick Hola doble flecha derecha toosee este comando).
7. Seleccione **Protocolo de Internet versión 4 (TCP/IPv4)** y luego haga clic en **Propiedades**.
8. Seleccione **Hola de uso después de direcciones de servidor DNS** y, a continuación, especifique **10.10.2.4** en **servidor DNS preferido**.
9. Hola **10.10.2.4** dirección es Hola que es un equipo virtual tooa asignado en la subred 10.10.2.0/24 de hello en una red virtual de Azure. La máquina virtual es **ContosoDC**. tooverify **ContosoDC**de dirección IP, utilice **nslookup contosodc** en la ventana de símbolo del sistema hello, como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Usar dirección IP de NSLOOKUP toofind para controlador de dominio](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC664954.jpg)
10. Haga clic en **Aceptar** > **cerrar** cambios de hello toocommit. Ahora puede unir máquina virtual de hello demasiado**corp.contoso.com**.
11. Nuevo en hello **servidor Local** ventana, haga clic en hello **WORKGROUP** vínculo.
12. Hola **nombre_equipo** sección, haga clic en **cambio**.
13. Seleccione hello **dominio** casilla de verificación, escriba **corp.contoso.com** en Hola cuadro de texto y, a continuación, haga clic en **Aceptar**.
14. Hola **la seguridad de Windows** diálogo cuadro, especifique las credenciales de hello para la cuenta de administrador de dominio predeterminado de hello (**CORP\AzureAdmin**) y la contraseña de hello (**Contoso! 000**).
15. Cuando vea el mensaje de "dominio de corp.contoso.com bienvenida toohello" Hola, haga clic en **Aceptar**.
16. Haga clic en **cerrar** > **reiniciar ahora** en el cuadro de diálogo de Hola.

### <a name="add-hello-corpinstall-user-as-an-administrator-on-each-virtual-machine"></a>Agregar usuario de hello Corp\Install como un administrador en cada máquina virtual
1. Espere hasta que se reinicia la máquina virtual de hello y, a continuación, abra Hola RDP de archivos nuevo toosign en la máquina virtual de toohello con hello **BUILTIN\AzureAdmin** cuenta.
2. En **Administrador de servidores**, haga clic en **Herramientas** > **Administración de equipos**.
   
    ![Administración de equipos](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784630.png)
3. Hola **administración de equipos** cuadro de diálogo, expanda **usuarios y grupos locales**y, a continuación, haga clic en **grupos**.
4. Haga doble clic en hello **administradores** grupo.
5. Hola **propiedades de administradores de** diálogo cuadro, haga clic en hello **agregar** botón.
6. Escriba Hola usuario **CORP\Install**y, a continuación, haga clic en **Aceptar**. Cuando se le piden credenciales, usar hello **AzureAdmin** cuenta con hello **Contoso! 000** contraseña.
7. Haga clic en **Aceptar** tooclose hello **propiedades del Administrador de** cuadro de diálogo.

### <a name="add-hello-failover-clustering-feature-tooeach-virtual-machine"></a>Agregar máquina virtual de tooeach de agrupación en clústeres de conmutación por error de característica de Hola
1. Hola **el administrador del servidor** panel, haga clic en **agregar roles y características**.
2. Hola **agregar Roles y características Asistente**, haga clic en **siguiente** hasta llegar toohello **características** página.
3. Seleccione **Clústeres de conmutación por error**. Cuando se le solicite, agregue otras las características dependientes.
   
    ![Agregar la característica de agrupación en clústeres de conmutación por error toovirtual máquina](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784631.png)
4. Haga clic en **siguiente**y, a continuación, haga clic en **instalar** en hello **confirmación** página.
5. Cuando Hola **agrupación en clústeres de conmutación por error** finalizada la instalación de características, haga clic en **cerrar**.
6. Cierre la sesión de máquina virtual de Hola.
7. Repita los pasos Hola de esta sección para todos los servidores de tres: **Nodowsfccontoso**, **ContosoSQL1**, y **ContosoSQL2**.

Hola ahora se aprovisionan máquinas virtuales de SQL Server y en ejecución, pero cada uno tiene opciones predeterminadas de Hola para SQL Server.

## <a name="create-hello-failover-cluster"></a>Crear el clúster de conmutación por error de Hola
En esta sección, creará el clúster de conmutación por error de Hola que hospedará el grupo de disponibilidad de Hola que creará más adelante. Por ahora, debe haber hecho Hola después tooeach de máquinas virtuales de hello tres que va a utilizar en el clúster de conmutación por error de hello:

* Máquina virtual de hello totalmente aprovisionado en Azure
* Se unió al dominio de toohello de máquina virtual de Hola
* Agregar **CORP\Install** toohello grupo de administradores locales
* Característica de agrupación en clústeres de conmutación por error de hello agregada

Todos estos son los requisitos previos en cada máquina virtual para poder unir clúster de conmutación por error de toohello.

Además, tenga en cuenta que Hola red virtual de Azure no se comportan en hello misma manera que una red local. Necesita toocreate clúster de Hola Hola siguiendo el orden:

1. Cree un clúster de nodo único en un nodo (**ContosoSQL1**).
2. Modificar tooan de dirección IP de clúster de hello dirección IP sin usar (**10.10.2.101**).
3. Ponga el nombre del clúster de hello en línea.
4. Agregar Hola otros nodos (**ContosoSQL2** y **Nodowsfccontoso**).

Usar hello siguiente pasos toocomplete las tareas de Hola que configurar totalmente el clúster de Hola.

1. Archivo RDP de hello abierto para **ContosoSQL1**y de inicio de sesión mediante el uso de la cuenta de dominio de hello **CORP\Install**.
2. Hola **el administrador del servidor** panel, haga clic en **herramientas** > **Administrador de clústeres de conmutación por error**.
3. En el panel izquierdo de hello, haga clic en **Administrador de clústeres de conmutación por error**y, a continuación, haga clic en **crear un clúster**, tal y como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Crear clúster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784632.png)
4. En el Asistente para crear clúster de Hola, cree un clúster de un nodo recorriendo las páginas de Hola y con la configuración de hello en hello en la tabla siguiente:
   
   | Page | Configuración |
   | --- | --- |
   | Antes de empezar |Usar predeterminados |
   | Seleccionar servidores |Escriba **ContosoSQL1** en **Especifique el nombre del servidor** y haga clic en **Agregar**. |
   | Advertencia de validación |Seleccione **no. no requieren soporte técnico de Microsoft para este clúster y, por tanto, no desea validación de hello toorun las pruebas. Al hacer clic en siguiente, continuar con la creación de clúster de hello**. |
   | Punto de acceso para administrar Hola clúster |Escriba **Cluster1** en **Nombre de clúster** |
   | Confirmación |Use los valores predeterminados a menos que use Espacios de almacenamiento. Vea la advertencia Hola sigue a esta tabla. |
   
   > [!WARNING]
   > Si utilizas [espacios de almacenamiento](https://technet.microsoft.com/library/hh831739), que agrupa varios discos en grupos de almacenamiento, debe borrar hello **agregar todo el almacenamiento apto toohello clúster** casilla de verificación de hello **confirmación** página. Si no desactiva esta opción, los discos virtuales Hola se desasociarán durante el proceso de agrupación en clústeres de Hola. Como resultado, también no aparecerán en el Administrador de discos o en el explorador hasta que los espacios de almacenamiento de Hola se quitan del clúster de Hola y volver a adjuntar mediante PowerShell.
   > 
   > 
5. En el panel izquierdo de hello, expanda **Administrador de clústeres de conmutación por error**y, a continuación, haga clic en **Cluster1.corp.contoso.com**.
6. En el panel central de hello, desplácese hacia abajo toohello **recursos principales de clúster** sección y expanda hello **nombre: Clutser1** detalles. Debería ver dos hello **nombre** hello y **dirección IP** recursos de hello **error** estado. Hello recurso de dirección IP no se puede conectar porque está asignado a clúster Hola Hola la misma dirección IP como máquina de hello, que es una dirección duplicada.
7. Hola contextual error **dirección IP** recurso y, a continuación, haga clic en **propiedades**.
   
    ![Propiedades de clúster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784633.png)
8. Seleccione **dirección IP estática**, especifique **10.10.2.101** en hello **dirección** cuadro de texto y, a continuación, haga clic en **Aceptar**.
9. Hola **recursos principales de clúster** sección, haga clic en **nombre: Cluster1**y, a continuación, haga clic en **poner en conexión**. Espere hasta que los recursos estén en línea. Cuando se trata de un recurso de nombre de clúster de hello en línea, servidor de DC de Hola se actualiza con una nueva cuenta de equipo de Active Directory. Se usará esta cuenta de Active Directory grupo de disponibilidad de Hola de toorun servicio en clúster más adelante.
10. Agregar Hola restantes clúster toohello de nodos. En el árbol del explorador de hello, haga clic en **Cluster1.corp.contoso.com**y, a continuación, haga clic en **agregar nodo**, tal y como se muestra en la siguiente captura de pantalla de Hola.
    
     ![Agregar nodo toohello clúster](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC784634.png)
11. Hola **Asistente para agregar nodos**, haga clic en **siguiente** en hello **seleccionar servidores** página, agregue **ContosoSQL2** y **Nodowsfccontoso**  toohello lista escribiendo el nombre del servidor hello en **escriba el nombre de servidor** y, a continuación, haga clic en **agregar**. Cuando haya terminado, haga clic en **Siguiente**.
12. En hello **advertencia de validación** página, haga clic en **n**, aunque en un escenario de producción, debe realizar pruebas de validación de Hola. A continuación, haga clic en **Siguiente**.
13. En hello **confirmación** página, haga clic en **siguiente** nodos de hello tooadd.
    
    > [!WARNING]
    > Si utilizas [espacios de almacenamiento](https://technet.microsoft.com/library/hh831739), que agrupa varios discos en grupos de almacenamiento, debe borrar hello **agregar todo el almacenamiento apto toohello clúster** casilla de verificación. Si no desactiva esta opción, los discos virtuales Hola se desasociarán durante el proceso de agrupación en clústeres de Hola. Como resultado, que también no aparecerán en el Administrador de discos o en el explorador hasta que se quitan los espacios de almacenamiento de Hola de clúster y volver a adjuntar con PowerShell.
    > 
    > 
14. Cuando se agregan nodos de hello toohello clúster, haga clic en **finalizar**. El Administrador de clústeres de conmutación por error debe mostrar ahora que el clúster tiene tres nodos y enumerarlos en hello **nodos** contenedor.
15. Cierre la sesión de la sesión de escritorio remoto de Hola.

## <a name="prepare-hello-sql-server-instances-for-availability-groups"></a>Preparar instancias de SQL Server de Hola para grupos de disponibilidad
En esta sección, hará lo Hola siga en ambos **ContosoSQL1** y **contosoSQL2**:

* Agregar un inicio de sesión para **NT AUTHORITY\System** con los permisos necesarios, establezca toohello instancia de SQL Server de forma predeterminada.
* Agregar **CORP\Install** como una instancia de SQL Server sysadmin rol toohello predeterminada.
* Abra firewall de hello para el acceso remoto de SQL Server.
* Habilitar Hola Always On característica de grupos de disponibilidad.
* Cambiar cuenta de servicio de SQL Server de hello demasiado**CORP\SQLSvc1** y **CORP\SQLSvc2**, respectivamente.

Estas acciones pueden realizarse en cualquier orden. No obstante, Hola pasos le guiará a través de ellos en orden. Siga los pasos de Hola para ambos **ContosoSQL1** y **ContosoSQL2**:

1. Si no se ha registrado fuera de sesión de escritorio remoto de hello para la máquina virtual de hello, hágalo ahora.
2. Archivos abierto Hola RDP para **ContosoSQL1** y **ContosoSQL2**e inicie sesión como **BUILTIN\AzureAdmin**.
3. Agregar **NT AUTHORITY\System** toohello inicios de sesión de SQL Server con los permisos necesarios. Abra **SQL Server Management Studio**.
4. Haga clic en **conectar** instancia de SQL Server de tooconnect toohello de forma predeterminada.
5. En el **Explorador de objetos**, expanda **Seguridad** y luego expanda **Inicios de sesión**.
6. Menú contextual hello **NT AUTHORITY\System** inicio de sesión y, a continuación, haga clic en **propiedades**.
7. En hello **elementos protegibles** página servidor local de hello, seleccione **Grant** para Hola los siguientes permisos y, a continuación, haga clic en **Aceptar**.
   
   * Modificar cualquier grupo de disponibilidad
   * Conectar SQL
   * Ver estado del servidor
8. Agregar **CORP\Install** como un **sysadmin** instancia de SQL Server de rol toohello predeterminada. En el **Explorador de objetos**, haga clic con el botón derecho en **Inicios de sesión** y luego en **Nuevo inicio de sesión**.
9. Escriba **CORP\Install** en **Nombre de inicio de sesión**.
10. En hello **Roles de servidor** página, seleccione **sysadmin**y, a continuación, haga clic en **Aceptar**. Después de crear el inicio de sesión de hello, puede verlo expandiendo **inicios de sesión** en **Explorador de objetos**.
11. una regla de firewall para SQL Server, en hello toocreate **iniciar** pantalla, abra **Firewall de Windows con seguridad avanzada**.
12. En el panel izquierdo de hello, seleccione **reglas de entrada**. En el panel derecho de hello, haga clic en **nueva regla**.
13. En hello **tipo de regla** página, haga clic en **programa** > **siguiente**.
14. En hello **programa** página, seleccione **esta ruta de acceso del programa**, tipo **%ProgramFiles%\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL\Binn\sqlservr.exe** en Hola cuadro de texto y, a continuación, haga clic en **siguiente**. Si está siguiendo estas instrucciones pero usa SQL Server 2012, directorio de SQL Server de hello es **MSSQL11. MSSQLSERVER**.
15. En hello **acción** página, mantenga **Permitir conexión hello** seleccionada y, a continuación, haga clic en **siguiente**.
16. En hello **perfil** página, acepte la configuración predeterminada de hello y, a continuación, haga clic en **siguiente**.
17. En hello **nombre** página, especifique un nombre de regla, como **SQL Server (regla de programa)**, Hola **nombre** texto cuadro, a continuación, haga clic en **finalizar**.
18. Hola tooenable **grupos de disponibilidad AlwaysOn** característica, en hello **iniciar** pantalla, abra **Administrador de configuración de SQL Server**.
19. En el árbol del explorador de hello, haga clic en **Services de SQL Server**, contextual hello **SQL Server (MSSQLSERVER)** de servicio y, a continuación, haga clic en **propiedades**.
20. Haga clic en hello **alta disponibilidad de AlwaysOn** ficha, seleccione **habilitar grupos de disponibilidad AlwaysOn**, tal y como se muestra en Hola siguiente captura de pantalla y, a continuación, haga clic en **aplicar**. Haga clic en **Aceptar** en Hola cuadro de diálogo y no cierre hello **propiedades** todavía el cuadro de diálogo. Se reiniciará el servicio de SQL Server de hello después de cambiar la cuenta de servicio de Hola.
    
     ![Habilitación de grupos de disponibilidad AlwaysOn](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665520.gif)
21. Hola toochange cuenta de servicio de SQL Server, haga clic en hello **iniciar sesión** , escriba **CORP\SQLSvc1** (para **ContosoSQL1**) o **CORP\SQLSvc2** () para **ContosoSQL2**) en **nombre-cuenta**, rellene y confirme la contraseña de hello y, a continuación, haga clic en **Aceptar**.
22. En el cuadro de diálogo de Hola que aparece, haga clic en **Sí** toorestart Hola servicio SQL Server. Una vez reiniciado Hola servicio SQL Server, cambia que realizó en hello **propiedades** entrarán en vigor de cuadro de diálogo.
23. Cierre la sesión de hello las máquinas virtuales.

## <a name="create-hello-availability-group"></a>Crear grupo de disponibilidad de Hola
Ya estás listo tooconfigure un grupo de disponibilidad. A continuación se resume lo que debe hacer:

* Crear una nueva base de datos (**MyDB1**) en **ContosoSQL1**.
* Realice una copia de seguridad completa y una copia de seguridad del registro de transacciones de base de datos de Hola.
* Restaurar Hola completa y copias de seguridad de registro demasiado**ContosoSQL2** con hello **NORECOVERY** opción.
* Crear grupo de disponibilidad de hello (**AG1**) con réplicas secundarias legibles, confirmación sincrónica y conmutación automática por error.

### <a name="create-hello-mydb1-database-on-contososql1"></a>Crear base de datos de hello MyDB1 en ContosoSQL1
1. Si todavía no está suscrito fuera de sesiones de escritorio remoto de Hola para **ContosoSQL1** y **ContosoSQL2**, hágalo ahora.
2. Archivo RDP de hello abierto para **ContosoSQL1**e inicie sesión como **CORP\Install**.
3. En el **Explorador de archivos**, en **\\C:**, cree un directorio denominado **backup**. Utilizará este directorio tooback y restaurar la base de datos.
4. Haga clic en nuevo directorio de hello, seleccione demasiado**compartir con**y, a continuación, haga clic en **personas concretas**, tal y como se muestra en la siguiente captura de pantalla de Hola.
   
    ![Creación de una carpeta de copia de seguridad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665521.gif)
5. Agregar **CORP\SQLSvc1**y, a continuación, asígnele el nombre hello **lectura/escritura** permiso. Agregar **CORP\SQLSvc2**y, a continuación, asígnele el nombre hello **lectura** permiso, como se muestra en Hola siguiente captura de pantalla y, a continuación, haga clic en **recurso compartido**. Cuando finalice el proceso de uso compartido de archivos de hello, haga clic en **realiza**.
   
    ![Concesión de permisos para la carpeta de copia de seguridad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665522.gif)
6. toocreate Hola base de datos, de hello **iniciar** menú Abrir **SQL Server Management Studio**y, a continuación, haga clic en **conectar** instancia de SQL Server de tooconnect toohello de forma predeterminada.
7. En el **Explorador de objetos**, haga clic con el botón derecho en **Bases de datos** y, después, haga clic en **Nueva base de datos**.
8. En **Nombre de base de datos**, escriba **MyDB1** y después haga clic en **Aceptar**.

### <a name="make-a-full-backup-of-mydb1-and-restore-it-on-contososql2"></a>Realización de una copia de seguridad completa de MyDB1 y restauración en ContosoSQL2
1. toomake una copia de seguridad completa del programa Hola a la base de datos, en **Explorador de objetos**, expanda **bases de datos**, haga clic en **MyDB1**, seleccione demasiado**tareas**, y a continuación, haga clic en **copia de seguridad**.
2. Hola **origen** sección, mantenga **tipo de copia de seguridad** establecido demasiado**completo**. Hola **destino** sección, haga clic en **quitar** tooremove Hola ruta de acceso predeterminada para el archivo de copia de seguridad de hello.
3. Hola **destino** sección, haga clic en **agregar**.
4. Hola **nombre de archivo** cuadro de texto, escriba  **\\ContosoSQL1\backup\MyDB1.bak**, haga clic en **Aceptar**y, a continuación, haga clic en **Aceptar** nuevo tooback la base de datos de Hola. Cuando finalice la operación de copia de seguridad de hello, haga clic en **Aceptar** nuevo cuadro de diálogo de tooclose Hola.
5. copia de seguridad de base de datos de hello, de registro de toomake una transacción **Explorador de objetos**, expanda **bases de datos**, haga clic en **MyDB1**, seleccione demasiado**tareas**y, a continuación, haga clic en **copia de seguridad**.
6. En **Tipo de copia de seguridad**, seleccione **Registro de transacciones**. Mantener hello **destino** archivo toohello de conjunto de ruta de acceso que especificada anteriormente y, a continuación, haga clic en **Aceptar**. Una vez finalizada la operación de copia de seguridad de hello, haga clic en **Aceptar** nuevo.
7. Hola toorestore completa y registro de transacciones las copias de seguridad **ContosoSQL2**, abra el archivo de hello RDP para **ContosoSQL2**e inicie sesión como **CORP\Install**. Dejar la sesión de escritorio remoto de Hola para **ContosoSQL1** abrir.
8. De hello **iniciar** menú Abrir **SQL Server Management Studio**y, a continuación, haga clic en **conectar** instancia de SQL Server de tooconnect toohello de forma predeterminada.
9. En el **Explorador de objetos**, haga clic con el botón derecho en **Bases de datos** y luego en **Restaurar base de datos**.
10. Hola **origen** sección, seleccione **dispositivo**y haga clic en el botón de puntos suspensivos hello **...** .
11. En **Seleccionar dispositivos de copia de seguridad**, haga clic en **Agregar**.
12. En la **ubicación del archivo de copia de seguridad**, escriba **\\ContosoSQL1\backup**, haga clic en **Actualizar**, a continuación, seleccione **MyDB1.bak** y haga clic en **Aceptar**, luego haga clic de nuevo en **Aceptar** . Ahora debería ver Hola copia de seguridad completa y copia de seguridad de registro de hello en hello **toorestore de conjuntos de copia** panel.
13. Vaya toohello **opciones** página, seleccione **RESTORE WITH NORECOVERY** en **estado de recuperación**y, a continuación, haga clic en **Aceptar** base de datos de toorestore Hola. Después de hello restaurar operación finalice, haga clic en **Aceptar**.

### <a name="create-hello-availability-group"></a>Crear grupo de disponibilidad de Hola
1. Vaya realizar copias de sesión de escritorio remoto de toohello para **ContosoSQL1**. En **Explorador de objetos** en SQL Server Management Studio, haga clic en **alta disponibilidad de AlwaysOn**y, a continuación, haga clic en **el Asistente para nuevo grupo de disponibilidad**, tal y como se muestra en hello captura de pantalla siguiente.
   
    ![Inicio del Asistente para nuevo grupo de disponibilidad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665523.gif)
2. En hello **Introducción** página, haga clic en **siguiente**. En hello **especificar el nombre de grupo de disponibilidad** página, escriba **AG1** en **nombre del grupo de disponibilidad**, a continuación, haga clic en **siguiente** nuevo.
   
    ![Asistente para nuevo grupo de disponibilidad: Especificación del nombre de grupo de disponibilidad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665524.gif)
3. En hello **seleccionar bases de datos** , seleccione **MyDB1**y, a continuación, haga clic en **siguiente**. base de datos de Hello cumple los requisitos previos de Hola para un grupo de disponibilidad dado que ha realizado al menos una copia de seguridad completa en la réplica principal pretendida de Hola.
   
    ![Asistente para nuevo grupo de disponibilidad: Selección de base de datos](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665525.gif)
4. en hello **especificar réplicas** página, haga clic en **agregar una réplica**.
   
    ![Asistente para nuevo grupo de disponibilidad: Especificación de réplicas](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665526.gif)
5. Hola **conectar tooServer** cuadro de diálogo, escriba **ContosoSQL2** en **nombre del servidor**y, a continuación, haga clic en **conectar**.
   
    ![Asistente para nuevo grupo de disponibilidad, conectar tooserver](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665527.gif)
6. En hello **especificar réplicas** página, ahora debería ver **ContosoSQL2** enumerados en **réplicas disponibles**. Configurar réplicas de hello tal y como se muestra en la siguiente captura de pantalla de Hola. Cuando haya terminado, haga clic en **Siguiente**.
   
    ![Asistente para nuevo grupo de disponibilidad: Especificación de réplicas (completo)](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665528.gif)
7. En hello **seleccionar sincronización de datos iniciales** , seleccione **solo unión**y, a continuación, haga clic en **siguiente**. Ya ha realizado la sincronización de datos manualmente cuando realiza copias de seguridad completa y de transacciones de hello en **ContosoSQL1** y las restauró en **ContosoSQL2**. Puede elegir no tooperform hello las operaciones de copia de seguridad y restauración en la base de datos y en su lugar, seleccione **completa** toolet Hola Asistente para nuevo grupo de disponibilidad realice la sincronización de datos automáticamente. Sin embargo, no se recomienda esta opción para bases de datos de gran tamaño como las que se encuentran en algunas empresas.
   
    ![Asistente para nuevo grupo de disponibilidad, seleccionar sincronización de datos iniciales](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665529.gif)
8. En hello **validación** página, haga clic en **siguiente**. Esta página debe ser similar toohello siguiente captura de pantalla. Hay una advertencia para la configuración de agente de escucha de hello porque no ha configurado un agente de escucha del grupo de disponibilidad. Puede omitir esta advertencia, ya que este tutorial no configura un agente de escucha. agente de escucha de tooconfigure Hola después de completar este tutorial, vea [configurar un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).
   
    ![Asistente para nuevo grupo de disponibilidad: Validación](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665530.gif)
9. En hello **resumen** página, haga clic en **finalizar**y, a continuación, espere mientras el Asistente de hello configura nuevo grupo de disponibilidad Hola. En hello **progreso** página, puede hacer clic en **detalles más** tooview Hola detallada progreso. Cuando finalice el Asistente de hello, inspeccionar hello **resultados** tooverify página ese grupo de disponibilidad de Hola se crea correctamente, tal y como se muestra en la siguiente captura de pantalla de hello y, a continuación, haga clic en **cerrar** tooexit Hola Asistente.
   
    ![Asistente para nuevo grupo de disponibilidad: Resultados](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665531.gif)
10. En el **Explorador de objetos**, expanda **Alta disponibilidad AlwaysOn** y después, expanda **Grupos de disponibilidad**. Ahora debería ver el nuevo grupo de disponibilidad hello en este contenedor. Haga clic con el botón derecho en **AG1 (principal)** y luego en **Mostrar panel**.
    
     ![Visualización del panel del grupo de disponibilidad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665532.gif)
11. Su **panel AlwaysOn** debe apariencia similar toohello uno Hola siguiente captura de pantalla. Puede ver las réplicas de hello, el modo de conmutación por error de Hola de cada réplica y el estado de sincronización de Hola.
    
     ![Panel del grupo de disponibilidad](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665533.gif)
12. Devolver demasiado**el administrador del servidor**, haga clic en **herramientas**y, a continuación, abra **Administrador de clústeres de conmutación por error**.
13. Expanda **Cluster1.corp.contoso.com** y expanda **Servicios y aplicaciones**. Seleccione **Roles** y tenga en cuenta que hello **AG1** se ha creado la función de grupo de disponibilidad. Tenga en cuenta que AG1 no tiene una dirección IP por qué base de datos, los clientes pueden conectarse toohello grupo de disponibilidad, porque no ha configurado un agente de escucha. Puede conectarse directamente toohello nodo principal para las operaciones de lectura y escritura y el nodo secundario de Hola para consultas de solo lectura.
    
     ![Grupo de disponibilidad en el administrador de clústeres de conmutación por error.](./media/virtual-machines-windows-classic-portal-sql-alwayson-availability-groups/IC665534.gif)

> [!WARNING]
> No intente toofail por grupo de disponibilidad Hola Hola Administrador de clústeres de conmutación por error. Todas las operaciones de conmutación por error deben realizarse desde el **Panel AlwaysOn** de SQL Server Management Studio. Para obtener más información, consulte [restricciones sobre el uso Hola Administrador de clústeres de conmutación por error con grupos de disponibilidad](https://msdn.microsoft.com/library/ff929171.aspx).
> 
> 

## <a name="next-steps"></a>Pasos siguientes
Ha implementado correctamente SQL Server AlwaysOn mediante la creación de un grupo de disponibilidad en Azure. tooconfigure un agente de escucha para este grupo de disponibilidad, consulte [configurar un agente de escucha ILB para grupos de disponibilidad AlwaysOn en Azure](../classic/ps-sql-int-listener.md).

Para obtener más información sobre el uso de SQL Server en Azure, consulte [SQL Server en Máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

