---
title: "aaaSet la alta disponibilidad para máquinas virtuales del Administrador de recursos de Azure | Documentos de Microsoft"
description: "Este tutorial muestra cómo agrupar toocreate una disponibilidad de AlwaysOn con máquinas virtuales de Azure en modo Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 64e85527-d5c8-40d9-bbe2-13045d25fc68
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: 6f0a253d3502259a487e66fd62d92e41c379a6b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-always-on-availability-groups-in-azure-virtual-machines-automatically-resource-manager"></a>Configuración automática de grupos de disponibilidad AlwaysOn en Azure Virtual Machines: Resource Manager

Este tutorial muestra cómo toocreate una disponibilidad de SQL Server grupo que usa máquinas virtuales del Administrador de recursos de Azure. tutorial de Hello usa Azure hojas tooconfigure una plantilla. Puede revisar la configuración predeterminada de hello, escriba la configuración necesaria y actualizar hojas de hello en el portal de Hola a medida que vaya a través de este tutorial.

todo el tutorial Hola crea un grupo de disponibilidad de SQL Server en Azure Virtual máquinas que incluyen hello siguientes elementos:

* Una red virtual que tiene varias subredes, incluida una subred front-end y back-end
* Dos controladores de dominio que tienen un dominio de Active Directory
* Dos máquinas virtuales que ejecutan SQL Server y subred de back-end de implementada toohello y toohello Unidos a un dominio de Active Directory
* Un clúster de conmutación por error de tres nodos con el modelo de quórum de mayoría de nodo de Hola
* Un grupo de disponibilidad que tiene dos réplicas de confirmación sincrónica de una base de datos de disponibilidad

Hola siguiente ilustración representa la solución completa de Hola.

![Arquitectura de pruebas para grupos de disponibilidad en Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/0-EndstateSample.png)

Todos los recursos de esta solución pertenecen tooa único grupo de recursos.

Antes de empezar este tutorial, confirme Hola siguiente:

* Ya tiene una cuenta de Azure. Si no tiene ninguna, [suscríbase para obtener una cuenta de prueba](http://azure.microsoft.com/pricing/free-trial/).
* Ya sabe cómo toouse Hola tooprovision GUI a una máquina virtual de SQL Server desde la Galería de máquinas virtuales de Hola. Para más información, consulte [Aprovisionamiento de una máquina virtual de SQL Server en Azure](virtual-machines-windows-portal-sql-server-provision.md).
* Ya tiene un conocimiento sólido de los grupos de disponibilidad. Para obtener más información, consulte [Grupos de disponibilidad AlwaysOn (SQL Server)](http://msdn.microsoft.com/library/hh510230.aspx).

> [!NOTE]
> Si le interesa utilizar los grupos de disponibilidad con SharePoint, consulte también [Configuración de grupos de disponibilidad AlwaysOn de SQL Server 2012 para SharePoint 2013](http://technet.microsoft.com/library/jj715261.aspx).
>
>

En este tutorial, usará hello Azure portal para:

* Elija Hola siempre en la plantilla desde el portal de Hola.
* Revise la configuración de la plantilla de Hola y actualizar algunos valores de configuración para su entorno.
* Supervisar Azure mientras crea todo el entorno de Hola.
* Conectar el controlador de dominio de tooa y, a continuación, tooa servidor que ejecuta SQL Server.

[!INCLUDE [availability-group-template](../../../../includes/virtual-machines-windows-portal-sql-alwayson-ag-template.md)]

## <a name="provision-hello-cluster-from-hello-gallery"></a>Clúster de hello aprovisionar desde la Galería de Hola
Azure proporciona una imagen de la Galería para toda la solución Hola. plantilla de Hola toolocate:

1. Inicie sesión en toohello portal de Azure con su cuenta.
2. Hola portal de Azure, haga clic en **+ nuevo** tooopen hello **New** hoja.
3. En hello **New** hoja, busque **AlwaysOn**.
   ![Buscar la plantilla de AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/16-findalwayson.png)
4. En los resultados de la búsqueda de hello, busque **clúster de SQL Server AlwaysOn**.
   ![Plantilla de AlwaysOn](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/17-alwaysontemplate.png)
5. En **Seleccionar un modelo de implementación,** elija **Resource Manager**.

### <a name="basics"></a>Aspectos básicos
Haga clic en **Fundamentos** y configurar Hola después de configuración:

* **Nombre de usuario administrador** es una cuenta de usuario que tenga permisos de administrador de dominio y es un miembro del rol de servidor fijo de sysadmin de SQL Server de hello en ambas instancias de SQL Server. Use **DomainAdmin**en este tutorial.
* **Contraseña** es Hola contraseña de cuenta de administrador de dominio de Hola. Utilice una contraseña compleja. Confirmar contraseña Hola.
* **Suscripción** suscripción Hola que Azure facturas toorun de implementa todos los recursos para el grupo de disponibilidad de Hola. Si su cuenta tiene varias suscripciones, puede especificar una suscripción distinta.
* **Grupo de recursos** es nombre Hola Hola grupo toowhich pertenecen todos los recursos de Azure que se crean mediante esta plantilla. Use **SQL-HA-RG**en este tutorial. Para más información, consulte [Información general de Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md#resource-groups).
* **Ubicación** es Hola donde tutorial Hola crea recursos Hola de región de Azure. Elija una región de Azure.

Hola siguiente captura de pantalla es una completa **Fundamentos** hoja:

![Aspectos básicos](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/1-basics.png)

Haga clic en **Aceptar**.

### <a name="domain-and-network-settings"></a>Configuración de red y dominio
Esta plantilla de la galería de Azure crea un dominio y controladores de dominio. También crea una red y dos subredes. plantilla de Hello no puede crear servidores en un dominio existente o red virtual. paso siguiente Hola configura Hola dominio y red.

En hello **configuración de red y dominio** hoja, revisión Hola valores preestablecidos para configuración de red y dominio de hello:

* **Nombre de dominio raíz de bosque** es nombre de dominio de Active Directory de Hola Hola ese clúster de hosts Hola. Para el tutorial de hello, utilice **contoso.com**.
* **Nombre de red virtual** es nombre de red de Hola para hello red virtual de Azure. Para el tutorial de hello, utilice **autohaVNET**.
* **Nombre de subred de controlador de dominio** es nombre de Hola de una parte de la red virtual de hello ese controlador de dominio de Hola de hosts. Utilice **subnet-1**. Esta subred usa el prefijo de dirección **10.0.0.0/24**.
* **Nombre de subred de SQL Server** es Hola nombre de una parte de la red virtual de Hola que servidores de Hola de hosts que ejecutan SQL Server y el archivo hello comparten testigo. Utilice **subnet-2**. Esta subred usa el prefijo de dirección **10.0.1.0/26**.

toolearn más información acerca de las redes virtuales en Azure, consulte [información general de red Virtual](../../../virtual-network/virtual-networks-overview.md).  

Hola **configuración de red y dominio** debe Hola tenga el aspecto siguiente captura de pantalla:

![Configuración de red y dominio](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/2-domain.png)

Si es necesario, puede cambiar estos valores. Para este tutorial, utilice Hola preestablece valores.

Revisar la configuración de hello y, a continuación, haga clic en **Aceptar**.

### <a name="availability-group-settings"></a>Configuración de grupos de disponibilidad
En **configuración del grupo disponibilidad**, revisión Hola valores preestablecidos para grupo de disponibilidad de Hola y Hola agente de escucha.

* **Nombre del grupo de disponibilidad** es nombre de recurso en clúster de Hola Hola grupo de disponibilidad. Use **Contoso-ag**en este tutorial.
* **Nombre de agente de escucha del grupo de disponibilidad** se usa por clúster de Hola y el equilibrador de carga interno de Hola. Los clientes que se conectan tooSQL Server pueden usar esta réplica nombre tooconnect toohello adecuados de la base de datos de Hola. Use **Contoso-listener** en este tutorial.
* **Puerto de escucha del grupo de disponibilidad** especifica el puerto TCP de Hola de agente de escucha de SQL Server de Hola. Para este tutorial, utilice el puerto predeterminado de hello, **1433**.

Si es necesario, puede cambiar estos valores. Para este tutorial, utilice Hola preestablece valores.  

![Configuración de grupos de disponibilidad](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/3-availabilitygroup.png)

Haga clic en **Aceptar**.

### <a name="virtual-machine-size-storage-settings"></a>Configuración de tamaño y almacenamiento de máquina virtual
En **tamaño de máquina virtual, la configuración de almacenamiento**, elija un tamaño de máquina virtual de SQL Server y revise Hola otros valores de configuración.

* **Tamaño de la máquina virtual de SQL Server** es el tamaño de Hola para máquinas virtuales que ejecutan SQL Server. Elija un tamaño de máquina virtual adecuado para la carga de trabajo. Si va a crear este entorno para el tutorial de hello, use **DS2**. Para las cargas de trabajo de producción, elija un tamaño de máquina virtual que puede admitir la carga de trabajo de Hola. Muchas cargas de trabajo de producción requieren **DS4** o superior. plantilla de Hello genera dos máquinas virtuales de este tamaño e instala a SQL Server en cada uno de ellos. Para más información, consulte [Tamaños de las máquinas virtuales Linux en Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!NOTE]
> Hola instala Azure Enterprise Edition de SQL Server. costo de Hello depende de la edición de Hola y el tamaño de la máquina virtual de Hola. Para más información sobre los costos actuales, consulte los [precios de máquinas virtuales](http://azure.microsoft.com/pricing/details/virtual-machines/#Sql).
>
>

* **Tamaño de máquina virtual de controlador de dominio** es el tamaño de la máquina virtual de Hola para hello controladores de dominio. Use **D2**en este tutorial.
* **Tamaño de máquina virtual de testigo del recurso compartido de archivo** es el tamaño de máquina virtual de hello para el testigo de recurso compartido de archivos de Hola. Use **A1**en este tutorial.
* **Cuenta de almacenamiento de SQL** es Hola nombre de cuenta de almacenamiento de Hola que contiene los datos de SQL Server de Hola y discos del sistema operativo. Use **alwaysonsql01** en este tutorial.
* **Cuenta de almacenamiento de controlador de dominio** es Hola nombre de cuenta de almacenamiento de Hola para hello controladores de dominio. Use **alwaysondc01**en este tutorial.
* **Tamaño de disco de datos de SQL Server** en TB es el tamaño de Hola de disco de datos de SQL Server de hello en TB. Especifique un número entre 1 y 4 Use **1** en este tutorial.
* **Optimización del almacenamiento** establece opciones de configuración de almacenamiento específica para las máquinas de virtuales de SQL Server hello en función de tipo de carga de trabajo de Hola. Todas las máquinas virtuales de SQL Server en este escenario usar almacenamiento premium con caché de host de disco de Azure solo tooread. Además, puede optimizar la configuración de SQL Server para cargas de trabajo de hello eligiendo una de estas tres opciones:

  * **Carga de trabajo general** no establece ninguna configuración específica.
  * **Procesamiento transaccional** establece las marcas de seguimiento 1117 y 1118.
  * **Almacenamiento de datos** establece las marcas de seguimiento 1117 y 610.

Use **Carga de trabajo general** en este tutorial.

![Configuración de almacenamiento del tamaño de VM](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/4-vm.png)

Revisar la configuración de hello y, a continuación, haga clic en **Aceptar**.

#### <a name="a-note-about-storage"></a>Una nota acerca de almacenamiento
Optimizaciones adicionales dependen de tamaño de Hola de discos de datos de SQL Server de Hola. Por cada terabyte de disco de datos, Azure agrega un almacenamiento premium adicional de 1 TB. Cuando un servidor requiere de 2 TB o más, plantilla de hello crea un grupo de almacenamiento en cada máquina virtual de SQL Server. Un grupo de almacenamiento es una forma de virtualización del almacenamiento donde varios discos son tooprovide configurado mayor capacidad, resistencia y el rendimiento.  plantilla de Hello, a continuación, crea un espacio de almacenamiento en bloque de almacenamiento de Hola y presenta un sistema de operativo de toohello de disco de datos único. plantilla de Hello designa este disco como disco de datos de Hola para SQL Server. plantilla de Hello optimiza bloque de almacenamiento de Hola para SQL Server mediante el uso de hello después de configuración:

* Tamaño de sección es hello intercalar la configuración de los discos virtuales Hola. Las cargas de trabajo transaccionales usan 64 KB. Las cargas de almacenamiento de datos utilizan 256 KB.
* La resistencia es simple (sin resistencia).

> [!NOTE]
> Almacenamiento de Azure premium es localmente redundante y mantiene tres copias de datos de hello en una única región, por lo que no se requiere resistencia adicional en el bloque de almacenamiento de Hola.
>
>

* Número de columnas es igual a número Hola de discos del bloque de almacenamiento de Hola.

Para información adicional sobre el espacio de almacenamiento y los bloques de almacenamiento, consulte:

* [Introducción a los espacios de almacenamiento](http://technet.microsoft.com/library/hh831739.aspx)
* [Copias de seguridad de Windows Server y bloques de almacenamiento](http://technet.microsoft.com/library/dn390929.aspx)

Para más información sobre los procedimientos recomendados para configurar SQL Server, consulte [Procedimientos recomendados para mejorar el rendimiento para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

### <a name="sql-server-settings"></a>Configuración de SQL Server
En **configuración de SQL Server**, revisar y modificar prefijo de nombre de máquina virtual de SQL Server de hello, la versión de SQL Server, la cuenta de servicio de SQL Server y la contraseña y Hola programación de mantenimiento de revisión automática SQL.

* **Prefijo de nombre de SQL Server** es toocreate usado un nombre para cada máquina virtual de SQL Server. Use **sqlserver** en este tutorial. Hello plantilla nombres Hola máquinas virtuales de SQL Server *sqlserver 0* y *sqlserver-1*.
* **Versión de SQL Server** es Hola versión de SQL Server. Use **SQL Server 2014**en este tutorial. También puede elegir **SQL Server 2012** o **SQL Server 2016**.
* **Nombre de usuario de cuenta de servicio de SQL Server** es el nombre de cuenta de dominio de Hola para hello servicio SQL Server. Use **sqlservice** en este tutorial.
* **Contraseña** contraseña Hola Hola cuenta de servicio de SQL Server.  Utilice una contraseña compleja. Confirmar contraseña Hola.
* **Programación de mantenimiento de aplicación de revisiones automatizada de SQL** identifica el día de hello de la semana de Hola que Azure revisa automáticamente Hola servidores de SQL Server. Escriba **Domingo** en este tutorial.
* **Hora de inicio de la aplicación de revisiones automatizada de SQL mantenimiento** es Hola hora del día para hello región de Azure cuando comienza la revisión automática.

> [!NOTE]
> Hola ventana para cada máquina virtual de la aplicación de revisiones se escalona una hora. Es una revisión a una máquina virtual solo en una interrupción de tooprevent de tiempo de los servicios.
>
>

![Configuración de SQL Server](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/5-sql.png)

Revisar la configuración de hello y, a continuación, haga clic en **Aceptar**.

### <a name="summary"></a>Resumen
En la página de resumen de hello, Azure valida la configuración de Hola. También puede descargar la plantilla de Hola. Resumen de hello de revisión. Haga clic en **Aceptar**.

### <a name="buy"></a>Comprar
Esta hoja final contiene las **condiciones de uso** y la **directiva de privacidad**. Revise esta información. Cuando esté listo para las máquinas virtuales de Azure toostart toocreate Hola y Hola a todos los otros recursos necesarios para el grupo de disponibilidad de hello, haga clic en **crear**.

Hola portal de Azure crea el grupo de recursos de Hola y todos los recursos de Hola.

## <a name="monitor-deployment"></a>Supervisión de la implementación
Supervisar el progreso de la implementación de Hola de hello portal de Azure. Un icono que representa la implementación de hello es toohello automáticamente anclado Azure panel del portal.

![Panel de Azure](./media/virtual-machines-windows-portal-sql-alwayson-availability-groups/11-deploydashboard.png)

## <a name="connect-toosql-server"></a>Conectar tooSQL Server
las nuevas instancias de Hola de SQL Server se ejecutan en máquinas virtuales que tengan las direcciones IP conectado a internet. Puede remoto escritorio (RDP) directamente tooeach máquina virtual SQL Server.

tooRDP tooa SQL Server, siga estos pasos:

1. Desde el panel del portal Azure de hello, compruebe que se ha realizado correctamente la implementación de Hola.
2. Haga clic en **Recursos**.
3. Hola **recursos** hoja, haga clic en **0 sqlserver**, que es el nombre del equipo Hola de una de las máquinas virtuales de Hola que ejecuta SQL Server.
4. En la hoja de Hola para **sqlserver 0**, haga clic en **conectar**. El explorador le preguntará si desea tooopen o guardar el objeto de conexión remota de Hola. Haga clic en **Abrir**.
5. **Conexión a Escritorio remoto** puede avisarle de que hello no se puede identificar el Editor de esta conexión remota. Haga clic en **Conectar**.
6. La seguridad de Windows le pide tooenter la dirección IP de credenciales tooconnect toohello del controlador de dominio principal de Hola. Haga clic en **Usar otra cuenta**. En **Nombre de usuario**, escriba **contoso\DomainAdmin**. Configurar esta cuenta cuando se establece el nombre de usuario de administrador de hello en plantilla Hola. Utilizar contraseñas complejas de Hola que eligió al configurar la plantilla de Hola.
7. **Escritorio remoto** puede avisarle de que el equipo remoto hello no se pudo autenticar due tooproblems con su certificado de seguridad. Muestra el nombre del certificado de seguridad de Hola. Si ha seguido el tutorial Hola, nombre de hello es **0.contoso.com sqlserver**. Haga clic en **Sí**.

Ahora está conectado con la máquina virtual RDP toohello SQL Server. Puede abrir SQL Server Management Studio, conectar la instancia predeterminada de toohello de SQL Server y compruebe que ese grupo de disponibilidad de hello está configurado.
