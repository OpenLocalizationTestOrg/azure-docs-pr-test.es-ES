---
title: aaaSQL Server Business Intelligence | Documentos de Microsoft
description: "En este tema usa recursos creados con el modelo de implementación clásica de Hola y describe las características de Business Intelligence (BI) de hello disponibles para SQL Server que se ejecutan en máquinas virtuales de Azure (VM)."
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: c681e7a7-eeda-48aa-bc35-6277f4828244
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/30/2017
ms.author: asaxton
ms.openlocfilehash: e3288f0835d6c4a19baeeea5f6b65fec16cd751f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="sql-server-business-intelligence-in-azure-virtual-machines"></a>Business Intelligence de SQL Server en Máquinas virtuales de Azure
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

la Galería de máquina Virtual de Microsoft Azure Hola incluye imágenes que contengan instalaciones de SQL Server. Hello SQL Server están las ediciones compatibles en imágenes de la Galería de Hola Hola mismos archivos de instalación puede instalar equipos tooon locales y máquinas virtuales. En este tema se resume Hola SQL Server Business Intelligence (BI) características instaladas en imágenes de Hola y pasos de configuración necesarios después de aprovisionar una máquina virtual. En este tema también se describen las topologías de implementación admitidas para las características de BI y los procedimientos recomendados.

## <a name="license-considerations"></a>Consideraciones de licencias
Hay dos maneras toolicense SQL Server en máquinas virtuales de Microsoft Azure:

1. Ventajas de la movilidad de licencias que forman parte de Software Assurance. Para obtener más información, consulte [Movilidad de Licencias a través de Software Assurance en Azure](https://azure.microsoft.com/pricing/license-mobility/).
2. Tarifa de pago por hora de máquinas virtuales de Azure con SQL Server instalado. Vea Hola sección "SQL Server" en [precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql).

Para obtener más información sobre las licencias y las tarifas actuales, vea [P+F sobre licencias de Máquinas virtuales](https://azure.microsoft.com/pricing/licensing-faq/%20/).

## <a name="sql-server-images-available-in-azure-virtual-machine-gallery"></a>Imágenes de SQL Server disponibles en la galería de máquinas virtuales de Azure
la Galería de máquina Virtual de Microsoft Azure Hola incluye varias imágenes que contienen Microsoft SQL Server. Hola instalado software en imágenes de máquina virtual de hello varía en función de la versión de Hola del sistema operativo de Hola y Hola de SQL Server. lista de Hola de imágenes disponibles en la Galería de máquina virtual de Azure Hola cambia con frecuencia.

<!--![SQL image in azure VM gallery](./media/virtual-machines-windows-classic-ps-sql-bi/IC741367.png)-->
![Imagen de SQL en la galería de máquinas virtuales de Azure](./media/virtual-machines-windows-classic-ps-sql-bi/vm-sql-images.png)

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Hello siguiente script de PowerShell devuelve Hola lista de imágenes de Azure que contienen "SQL Server" en hello ImageName:

    # assumes you have already uploaded a management certificate tooyour Microsoft Azure Subscription. View hello thumbprint value from hello "Subscriptions" menu in Azure portal.

    $subscriptionID = ""    # REQUIRED: Provide your subscription ID.
    $subscriptionName = "" # REQUIRED: Provide your subscription name.
    $thumbPrint = "" # REQUIRED: Provide your certificate thumbprint.
    $certificate = Get-Item cert:\currentuser\my\$thumbPrint # REQUIRED: If your certificate is in a different store, provide it here.-Ser  store is hello one specified with hello -ss parameter on MakeCert

    Set-AzureSubscription -SubscriptionName $subscriptionName -Certificate $certificate -SubscriptionID $subscriptionID

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2016"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2016*"} | select imagename,category, location, label, description

    Write-Host -foregroundcolor green "List of available gallery images where imagename contains 2014"
    Write-Host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
    get-azurevmimage | where {$_.ImageName -Like "*SQL-Server-2014*"} | select imagename,category, location, label, description

Para obtener más información sobre las ediciones y características admitidas por SQL Server, vea Hola siguiente:

* [Ediciones de SQL Server](https://www.microsoft.com/server-cloud/products/sql-server-editions/#fbid=Zae0-E6r5oh)
* [Características compatibles con las ediciones de SQL Server 2016 Hola](https://msdn.microsoft.com/library/cc645993.aspx)

### <a name="bi-features-installed-on-hello-sql-server-virtual-machine-gallery-images"></a>Características de BI instaladas en hello imágenes de la Galería de máquina Virtual de SQL Server
Hello tabla siguiente resume Hola características de Business Intelligence instaladas en imágenes de la Galería de máquina Virtual de Microsoft Azure comunes de Hola para SQL Server:

* SQL Server 2016 SP1 Enterprise
* SQL Server 2016 SP1 Standard
* SQL Server 2014 SP2 Enterprise
* SQL Server 2014 SP2 Standard
* SQL Server 2012 SP3 Enterprise
* SQL Server 2012 SP3 Standard

| Característica de BI de SQL Server | Instalado en la imagen de la Galería de Hola | Notas |
| --- | --- | --- |
| **Modo nativo de Reporting Services** |Sí |Instalada pero requiere configuración, incluida la dirección URL del Administrador de informes de Hola. Consulte la sección de hello [configurar Reporting Services](#configure-reporting-services). |
| **Modo de SharePoint de Reporting Services** |No |Hello imagen de la Galería de máquina Virtual de Microsoft Azure no incluye SharePoint o SharePoint archivos de instalación. <sup>1</sup> |
| **Minería de datos y multidimensional de Analysis Services (OLAP)** |Sí |Instancia de Analysis Services de hello instalado y configurado como predeterminada |
| **Tabular de Analysis Services** |No |Se admite en imágenes de SQL Server 2012, 2014 y 2016, pero no se instala de forma predeterminada. Instale otra instancia de Analysis Services. Consulte la sección de hello instalar otros servicios de SQL Server y características en este tema. |
| **Analysis Services PowerPivot para SharePoint** |No |Hello imagen de la Galería de máquina Virtual de Microsoft Azure no incluye SharePoint o SharePoint archivos de instalación. <sup>1</sup> |

<sup>1</sup> Para más información sobre SharePoint y las máquinas virtuales de Azure, consulte [Arquitecturas de Microsoft Azure para SharePoint 2013](https://technet.microsoft.com/library/dn635309.aspx) e [Implementación de SharePoint en máquinas virtuales de Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=34598).

![PowerShell](./media/virtual-machines-windows-classic-ps-sql-bi/IC660119.gif) Ejecute hello después tooget de comandos de PowerShell una lista de servicios instalados que contienen "SQL" en el nombre de servicio de Hola.

    get-service | Where-Object{ $_.DisplayName -like '*SQL*' } | Select DisplayName, status, servicetype, dependentservices | format-Table -AutoSize

## <a name="general-recommendations-and-best-practices"></a>Recomendaciones generales y prácticas recomendadas
* Hola mínimo tamaño recomendado para una máquina virtual es **A3** cuando se usa SQL Server Enterprise Edition. Hola **A4** tamaño de máquina virtual se recomienda para las implementaciones de SQL Server BI de Analysis Services y Reporting Services.
  
    Para obtener información sobre el tamaño actual de VM de hello, consulte [tamaños de máquina Virtual de Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Una práctica recomendada para la administración de discos es toostore archivos de datos, registro y copia de seguridad en las unidades excepto **C**: y **d.**:. Por ejemplo, cree los discos de datos **E**: y **F**:.
  
  * unidad de Hello almacenamiento en caché de directiva para la unidad predeterminada de hello **C**: no es óptima para trabajar con datos.
  * Hola **d.**: trata de una unidad temporal que se utiliza principalmente para el archivo de paginación de Hola. Hola **d.**: unidad no se conserva y no se guarda en el almacenamiento de blobs. Las tareas de administración, como un tamaño de máquina virtual de cambio toohello restablece hello **d.**: unidad. Se recomienda demasiado**no** usar hello **d.**: unidad para los archivos de base de datos, incluido tempdb.
    
    Para obtener más información sobre cómo crear y adjuntar discos, consulte [cómo tooAttach una máquina Virtual de disco de datos tooa](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* Detenga o desinstale servicios no tiene previsto toouse. Por ejemplo si solo se usa la máquina virtual de Hola para Reporting Services, detenga o desinstale Analysis Services y SQL Server Integration Services. Hello imagen siguiente es un ejemplo de servicios de Hola que se inician de forma predeterminada.
  
    ![Servicios de SQL Server](./media/virtual-machines-windows-classic-ps-sql-bi/IC650107.gif)
  
  > [!NOTE]
  > se requiere el motor de base de datos de SQL Server de Hello en hello admitida escenarios de BI. En una topología VM de servidor único, se requiere el motor de base de datos de hello toobe con Hola misma máquina virtual.
  
    Para obtener más información, vea el siguiente hello: [desinstalar Reporting Services](https://msdn.microsoft.com/library/hh479745.aspx) y [desinstalar una instancia de Analysis Services](https://msdn.microsoft.com/library/ms143687.aspx).
* Consulte **Windows Update** para ver nuevas "Actualizaciones importantes". imágenes de máquina Virtual de Microsoft Azure Hola se actualizan con frecuencia; Sin embargo, las actualizaciones importantes pueden estar disponibles en **Windows Update** después de que se actualizaron por última vez la imagen de máquina virtual de Hola.

## <a name="example-deployment-topologies"></a>Topologías de implementación de ejemplo
los siguientes Hola son implementaciones de ejemplo que usan máquinas virtuales de Microsoft Azure. topologías de Hello en estos diagramas son sólo algunas de las topologías posibles de Hola que puede usar con las características de BI de SQL Server y máquinas virtuales de Microsoft Azure.

### <a name="single-virtual-machine"></a>Máquina virtual única
Analysis Services, Reporting Services, el motor de base de datos de SQL Server y los orígenes de datos en una única máquina virtual.

![escenario de bi iass con 1 máquina virtual](./media/virtual-machines-windows-classic-ps-sql-bi/IC650108.gif)

### <a name="two-virtual-machines"></a>Dos máquinas virtuales
* Analysis Services, Reporting Services y Hola motor de base de datos de SQL Server en una única máquina virtual. Esta implementación incluye bases de datos del servidor de informes de Hola.
* Orígenes de datos en una segunda máquina virtual. Hello segunda VM incluye el motor de base de datos de SQL Server como origen de datos.

![escenario de bi iass con 2 máquinas virtuales](./media/virtual-machines-windows-classic-ps-sql-bi/IC650109.gif)

### <a name="mixed-azure--data-on-azure-sql-database"></a>Mezcla de Azure: datos en base de datos SQL de Azure
* Analysis Services, Reporting Services y Hola motor de base de datos de SQL Server en una única máquina virtual. Esta implementación incluye bases de datos del servidor de informes de Hola.
* El origen de datos es una base de datos SQL de Azure.

![escenarios de máquina virtual de bi iaas y AzureSQL como origen de datos](./media/virtual-machines-windows-classic-ps-sql-bi/IC650110.gif)

### <a name="hybrid-data-on-premises"></a>Híbrido: datos locales
* En esta implementación de ejemplo Hola motor de base de datos de SQL Server, Analysis Services y Reporting Services se ejecutan en una única máquina virtual. hosts de máquina virtual de Hola Hola bases de datos de servidor de informes. máquina virtual de Hello es tooan Unidos a un dominio local a través de redes virtuales de Azure, o alguna otra solución de túnel de VPN.
* El origen de datos es local.

![escenarios de máquina virtual de bi iaas y orígenes de datos locales](./media/virtual-machines-windows-classic-ps-sql-bi/IC654384.gif)

## <a name="reporting-services-native-mode-configuration"></a>Configuración del modo nativo de Reporting Services
imagen de galería de máquina virtual de Hola para SQL Server incluye el modo nativo de Reporting Services instalado, pero no está configurado el servidor de informes de Hola. pasos de Hello en esta sección configuran el servidor de informes de Reporting Services de Hola. Para obtener más información sobre cómo configurar el modo nativo de Reporting Services, consulte [Instalar el servidor de informes del modo nativo de Reporting Services (SSRS)](https://msdn.microsoft.com/library/ms143711.aspx).

> [!NOTE]
> Para consultar contenido similar que utiliza el servidor de informes de Hola de tooconfigure de secuencias de comandos de Windows PowerShell, consulte [tooCreate usar PowerShell un Azure VM con un modo de servidor de informes nativo](../classic/ps-sql-report.md).

### <a name="connect-toohello-virtual-machine-and-start-hello-reporting-services-configuration-manager"></a>Conecte toohello Máquina Virtual e inicie Hola Administrador de configuración de Reporting Services
Hay dos flujos de trabajo habituales para conectarse tooan Máquina Virtual de Azure:

* tooconnect en hello, haga clic en nombre de Hola de máquina virtual de hello y, a continuación, haga clic en **conectar**. Se abre una conexión a escritorio remota y se rellena automáticamente el nombre del equipo de Hola.
  
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-bi/IC650112.gif)
* Conectar máquina virtual de toohello con conexión de escritorio remoto de Windows. En la interfaz de usuario Hola de escritorio remoto de hello:
  
  1. Hola de tipo **nombre de servicio de nube** como nombre de equipo de Hola.
  2. Escriba dos puntos (:) y Hola número de puerto público que esté configurado para el extremo de escritorio remoto de hello TCP.
     
      Myservice.cloudapp.net:63133
     
      Para obtener más información, consulte [¿Qué es un servicio en la nube?](https://azure.microsoft.com/manage/services/cloud-services/what-is-a-cloud-service/).


**Inicie el Administrador de configuración de Reporting Services**

En **Windows Server 2012/2016**:

1. De hello **iniciar** , escriba **Reporting Services** toosee una lista de aplicaciones.
2. Haga clic con el botón derecho en el **Administrador de configuración de Reporting Services** y haga clic en **Ejecutar como administrador**.

En **Windows Server 2008 R2**:

1. Haga clic en **Inicio** y luego haga clic en **Todos los programas**.
2. Haga clic en **Microsoft SQL Server 2016**.
3. Haga clic en **Herramientas de configuración**.
4. Haga clic con el botón derecho en el **Administrador de configuración de Reporting Services** y haga clic en **Ejecutar como administrador**.

O:

1. Haga clic en **Iniciar**.
2. Hola **buscar programas y archivos** de diálogo, escriba **reporting services**. Si Hola VM ejecuta Windows Server 2012, escriba **reporting services** en pantalla de inicio de Windows Server 2012 de bienvenida.
3. Haga clic con el botón derecho en el **Administrador de configuración de Reporting Services** y haga clic en **Ejecutar como administrador**.
   
    ![buscar el administrador de configuración de ssrs](./media/virtual-machines-windows-classic-ps-sql-bi/IC650113.gif)

### <a name="configure-reporting-services"></a>Configurar Reporting Services
**Cuenta de servicio y dirección URL del servicio web:**

1. Comprobar hello **nombre del servidor** es el nombre del servidor local de Hola y haga clic en **conectar**.
2. Hola nota en blanco **nombre de base de datos del servidor de informes**. crea base de datos de Hello cuando finalice la configuración de Hola.
3. Comprobar hello **estado del servidor de informes** es **iniciado**. Si desea que el servicio de hello tooverify en el administrador del servidor de Windows, servicio de hello es hello **SQL Server Reporting Services** servicio de Windows.
4. Haga clic en **cuenta de servicio** y cambie la cuenta de hello según sea necesario. Si se usa la máquina virtual de hello en un entorno Unidos a un dominio no, Hola integrada **ReportServer** cuenta es suficiente. Para obtener más información sobre la cuenta de servicio de hello, consulte [cuenta de servicio](https://msdn.microsoft.com/library/ms189964.aspx).
5. Haga clic en **dirección URL del servicio Web** en el panel izquierdo de Hola.
6. Haga clic en **aplicar** valores predeterminados de tooconfigure Hola.
7. Hola Nota **direcciones URL del servicio de informe de servidor Web**. Tenga en cuenta que el puerto TCP de hello predeterminado es 80 y forma parte de la dirección URL de Hola. En un paso posterior, cree un punto de conexión de la máquina Virtual de Azure de Microsoft para el puerto de Hola.
8. Hola **resultados** panel, comprobar acciones de Hola se completó correctamente.

**Base de datos**

1. Haga clic en **base de datos** en el panel izquierdo de Hola.
2. Haga clic en **Cambiar base de datos**.
3. Compruebe que la opción **Crear una nueva base de datos del servidor de informes** está seleccionada y luego haga clic en Siguiente.
4. Compruebe el valor de **Nombre del servidor** y haga clic en **Probar conexión**.
5. Si el resultado de hello es **Probar conexión se realizó correctamente**, haga clic en **Aceptar** y, a continuación, haga clic en **siguiente**.
6. Es el nombre de base de datos de nota hello **ReportServer** hello y **modo de servidor de informes** es **nativo** , a continuación, haga clic en **siguiente**.
7. Haga clic en **siguiente** en hello **credenciales** página.
8. Haga clic en **siguiente** en hello **resumen** página.
9. Haga clic en **siguiente** en hello **del progreso y finalizar** página.

**Dirección URL del portal web o URL del Administrador de informes de 2012 y 2014:**

1. Haga clic en **dirección URL del Portal Web**, o **Report Manager URL** para 2014 y 2012, en el panel izquierdo de Hola.
2. Haga clic en **Apply**.
3. Hola **resultados** panel, comprobar acciones de Hola se completó correctamente.
4. Haga clic en **Salir**.

Para obtener información sobre los permisos del servidor de informes, consulte [Conceder permisos en un servidor de informes de modo nativo](https://msdn.microsoft.com/library/ms156014.aspx).

### <a name="browse-toohello-local-report-manager"></a>Examinar toohello el Administrador de informes local
configuración de hello tooverify, examinar tooreport manager en hello máquina virtual.

1. En hello VM, inicie Internet Explorer con privilegios de administrador.
2. Examinar toohttp://localhost/reports en hello máquina virtual.

### <a name="tooconnect-tooremote-web-portal-or-report-manager-for-2014-and-2012"></a>portal web de tooConnect tooRemote o el Administrador de informes de 2014 y 2012
Si quiere portal web de tooconnect toohello o el Administrador de informes de 2014 y 2012, en la máquina virtual de Hola desde un equipo remoto, cree una nueva máquina virtual extremo TCP. De forma predeterminada, servidor de informes de hello escucha las solicitudes HTTP en **el puerto 80**. Si configura toouse de direcciones URL de servidor hello informe un puerto diferente, debe especificar ese número de puerto en hello siguiendo las instrucciones.

1. Cree un extremo para hello Máquina Virtual de puerto TCP 80. Para obtener más información, vea Hola [extremos de máquina Virtual y los puertos de Firewall](#virtual-machine-endpoints-and-firewall-ports) sección en este documento.
2. Abrir el puerto 80 en firewall de la máquina virtual Hola.
3. Examinar el portal web de toohello o el Administrador de informes, con la máquina Virtual de Azure **nombre DNS** como nombre de servidor de hello en dirección URL de Hola. Por ejemplo:
   
    **Servidor de informes**: http://uebi.cloudapp.net/reportserver **Portal web**: http://uebi.cloudapp.net/reports
   
    [Configurar un firewall para el acceso del Servidor de informes](https://msdn.microsoft.com/library/bb934283.aspx)

### <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a>tooCreate y publicar informes toohello Máquina Virtual de Azure
Hello tabla siguiente resume algunas de hello opciones toopublish disponibles los informes existentes desde un servidor de informes de toohello de equipo local hospedado en hello Máquina Virtual de Microsoft Azure:

* **Generador de informes**: máquina virtual de hello incluye Hola click-una vez versión del generador de informes de Microsoft SQL Server para SQL 2014 y 2012. Hola de generador de informes de toostart primera vez en la máquina virtual de hello 2016 de SQL:
  
  1. Inicie el explorador con privilegios administrativos.
  2. Busque en la máquina virtual de hello, el portal web de toohello y seleccione hello **descargar** icono en la esquina superior derecha de Hola.
  3. Seleccione **Generador de informes**.
     
     Para obtener más información, consulte [Iniciar el Generador de informes](https://msdn.microsoft.com/library/ms159221.aspx).
* **SQL Server Data Tools**: VM: herramientas de datos de SQL Server está instalada en la máquina virtual de Hola y puede ser usado toocreate **proyectos de servidor de informes** e informes en la máquina virtual de Hola. Herramientas de datos de SQL Server puede publicar el servidor de informes de toohello Hola informes en la máquina virtual de Hola.
* **SQL Server Data Tools: remoto**: en el equipo local, cree un proyecto de Reporting Services en SQL Server Data Tools que contenga informes de Reporting Services. Configurar URL de servicio web de hello proyecto tooconnect toohello.
  
    ![propiedades del proyecto de ssdt para proyecto SSRS](./media/virtual-machines-windows-classic-ps-sql-bi/IC650114.gif)
* Crear una. Disco duro virtual unidad de disco duro que contiene los informes y, a continuación, carga y conectar una unidad de Hola.
  
  1. Cree una unidad de disco duro de .VHD en el equipo local que contenga los informes.
  2. Cree e instale un certificado de administración.
  3. Cargar tooAzure de archivo de disco duro virtual hello mediante el cmdlet Add-AzureVHD hello [crear y cargar un VHD de Windows Server tooAzure](../classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
  4. Adjunte la máquina virtual de hello disco toohello.

## <a name="install-other-sql-server-services-and-features"></a>Instalar otras características y servicios de SQL Server
Servicios de SQL Server adicionales tooinstall, como Analysis Services en modo tabular, ejecutan al Asistente para la instalación de hello SQL server. archivos de programa de instalación de Hello están en el disco local de la máquina virtual Hola.

1. Haga clic en **Inicio** y luego haga clic en **Todos los programas**.
2. Haga clic en **Microsoft SQL Server 2016**, **Microsoft SQL Server 2014** o **Microsoft SQL Server 2012** y luego haga clic en **Herramientas de configuración**.
3. Haga clic en el **Centro de instalación de SQL Server**.

O ejecute C:\SQLServer_13.0_full\setup.exe, C:\SQLServer_12.0_full\setup.exe o C:\SQLServer_11.0_full\setup.exe

> [!NOTE]
> Hola primera vez que ejecute el programa de instalación de SQL Server, el programa de instalación más archivos se pueden descargar y requieren un reinicio de máquina virtual de Hola y el reinicio del programa de instalación de SQL Server.
> 
> Si necesita toorepeatedly personalizar la imagen de hello seleccionada de hello Máquina Virtual de Microsoft Azure, considere la posibilidad de crear su propia imagen de SQL Server. La funcionalidad SysPrep de Analysis Services se habilitó con SQL Server 2012 SP1 CU2. Para más información, consulte [Consideraciones acerca de la instalación de SQL Server con SysPrep](https://msdn.microsoft.com/library/ee210754.aspx) y [Sysprep Support for Server Roles (Compatibilidad de Sysprep con roles de servidor)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).
> 
> 

### <a name="tooinstall-analysis-services-tabular-mode"></a>tooInstall modo Tabular de Analysis Services
Hola pasos de esta sección **resumir** Hola instalación de modo tabular de Analysis Services. Para obtener más información, vea Hola siguiente:

* [Instalar Analysis Services en modo tabular](https://msdn.microsoft.com/library/hh231722.aspx)
* [Modelado tabular (Tutorial de Adventure Works)](https://msdn.microsoft.com/library/140d0b43-9455-4907-9827-16564a904268)

**tooInstall modo Tabular de Analysis Services:**

1. En el Asistente para la instalación de SQL Server de hello, haga clic en **instalación** en Hola panel izquierdo y, a continuación, haga clic en **instalación independiente de nuevo SQL server o agregar la instalación existente de características tooan**.
   
   * Si ve hello **Buscar carpeta**, tooc:\SQLServer_13.0_full, c:\SQLServer_12.0_full o c:\SQLServer_11.0_full y, a continuación, haga clic en **Aceptar**.
2. Haga clic en **siguiente** de página de actualizaciones de producto de Hola.
3. En hello **tipo de instalación** página, seleccione **realizar una nueva instalación de SQL Server** y haga clic en **siguiente**.
4. En hello **rol de instalación** página, haga clic en **instalación de características de SQL Server**.
5. En hello **selección de características** página, haga clic en **Analysis Services**.
6. En hello **configuración de instancia** página, escriba un nombre descriptivo, como **Tabular** en **instancia con nombre** y **Id. de instancia** texto cuadros.
7. En hello **configuración de Analysis Services** página, seleccione **modo Tabular**. Agregue la lista de permisos administrativos de usuarios actuales de hello toohello.
8. Complete y cierre el Asistente para la instalación de SQL Server de Hola.

## <a name="analysis-services-configuration"></a>Configuración de Analysis Services
### <a name="remote-access-tooanalysis-services-server"></a>TooAnalysis de acceso remoto servidor de servicios
El servidor de Analysis Services solo admite la Autenticación de Windows. tooaccess Analysis Services de forma remota desde aplicaciones cliente como SQL Server Management Studio o SQL Server Data Tools, la máquina virtual de hello debe toobe tooyour Unidos a un dominio local mediante la red Virtual de Azure. Para obtener más información, consulte [Red virtual de Azure](../../../virtual-network/virtual-networks-overview.md).

Una **instancia predeterminada** de Analysis Services escucha en el puerto TCP **2383**. Abrir el puerto de hello en firewall de máquinas virtuales de Hola. Una instancia con nombre en clúster de Analysis Services también escucha en el puerto **2383**.

Para una **instancia con nombre** de Analysis Services, servicio SQL Server Browser Hola se requiere acceso de puerto toomanage. configuración predeterminada de SQL Server Browser de Hello es el puerto **2382**.

En el firewall de máquinas virtuales de hello, abra el puerto **2382** y cree un estático con el nombre de puerto de la instancia de Analysis Services.

1. puertos de tooverify que ya están en usar en hello VM y qué proceso está utilizando puertos de hello, ejecute hello siguiente comando con privilegios de administrador:
   
        netstat /ao
2. Use SQL Server Management Studio toocreate un estático Analysis Services con el nombre puerto de instancias mediante la actualización de 'Puerto' value en AS tabular propiedades generales de la instancia. Para obtener más información, vea Hola "Instancia con nombre o utilizar un puerto fijo para el valor predeterminado es" en [configurar Firewall de Windows de hello tooAllow acceso a Analysis Services](https://msdn.microsoft.com/library/ms174937.aspx#bkmk_fixed).
3. Reinicie la instancia tabular de Hola de hello servicio Analysis Services.

Para obtener más información, vea Hola **extremos de máquina Virtual y los puertos de Firewall** sección en este documento.

## <a name="virtual-machine-endpoints-and-firewall-ports"></a>Extremos de máquina virtual y puertos de firewall
Esta sección resume los puntos de conexión de máquina Virtual de Microsoft Azure tooopen toocreate y puertos en Firewall de máquina virtual de Hola. Hello tabla siguiente resumen hello **TCP** puertos toocreate puntos de conexión y hello tooopen de puertos en firewall de máquinas virtuales de Hola.

* Si está utilizando una sola máquina virtual y hello dos elementos siguientes son verdaderas, no es necesario toocreate extremos de máquina virtual y no es necesario tooopen puertos de hello en firewall de Hola Hola máquina virtual.
  
  * No conectarse de forma remota toohello características de SQL Server en VM de Hola. Establecimiento de una máquina virtual toohello de conexión a Escritorio remoto y tener acceso a características de SQL Server de hello localmente en hello VM no se considera una características de SQL Server toohello de conexión remota.
  * No unirse a dominio de hello VM tooan local a través de la red Virtual de Azure u otra solución túnel de VPN.
* Si máquina virtual de hello no está tooa Unidos a un dominio pero desea tooremotely conectar toohello características de SQL Server en la máquina virtual:
  
  * Abrir Hola puertos en firewall de Hola Hola máquina virtual.
  * Crear extremos de máquina virtual para hello indican puertos (*).
* Si máquina virtual de hello es dominio tooa combinadas mediante un túnel VPN como redes virtuales de Azure, los puntos de conexión de hello no son necesarios. Sin embargo, abra puertos de hello en firewall de Hola Hola VM.
  
  | Port | Tipo | Description |
  | --- | --- | --- |
  | **80** |TCP |Acceso remoto al servidor de informes (*). |
  | **1433** |TCP |SQL Server Management Studio (*). |
  | **1434** |UDP |SQL Server Browser. Esto es necesario cuando Hola VM en tooa Unidos a un dominio. |
  | **2382** |TCP |SQL Server Browser. |
  | **2383** |TCP |Instancia predeterminada de SQL Server Analysis Services e instancias con nombre en clúster. |
  | **Definida por el usuario** |TCP |Cree un estático Analysis Services con el nombre de puerto de la instancia de un número de puerto que desee y, a continuación, desbloquear el número de puerto de hello en firewall de Hola. |

Para obtener más información sobre la creación de puntos de conexión, vea Hola siguiente:

* Crear extremos:[cómo tooSet extremos tooa Máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
* SQL Server: Consulte Hola completar la configuración pasos tooconnect toohello sección "máquinas virtuales con SQL Server Management Studio" de [aprovisionamiento de una máquina Virtual de SQL Server en Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md).

Hello siguiente diagrama muestra hello puertos tooopen Hola VM firewall tooallow acceso remoto toofeatures y los componentes de hello máquina virtual.

![tooopen de puertos para aplicaciones bi en máquinas virtuales de Azure](./media/virtual-machines-windows-classic-ps-sql-bi/IC654385.gif)

## <a name="resources"></a>Recursos
* Revise la directiva de soporte técnico de Hola para software de servidor de Microsoft utilizado en el entorno de máquina Virtual de Azure Hola. Hola tema siguiente resume la compatibilidad con características como BitLocker, agrupación en clústeres de conmutación por error y equilibrio de carga de red. [Compatibilidad de software de servidor de Microsoft para máquinas virtuales Azure](http://support.microsoft.com/kb/2721672).
* [Información general sobre SQL Server en máquinas virtuales de Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md)
* [Máquinas virtuales](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Aprovisionamiento de una máquina virtual de SQL Server en Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md)
* [¿Cómo tooAttach una máquina Virtual de tooa de disco de datos](../classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Migrar un servidor en una máquina virtual de Azure de tooSQL de base de datos](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)
* [Determinar el modo de servidor de una instancia de Analysis Services de Hola](https://msdn.microsoft.com/library/gg471594.aspx)
* [Modelado multidimensional (Tutorial de Adventure Works)](https://technet.microsoft.com/library/ms170208.aspx)
* [Centro de documentación de Azure](https://azure.microsoft.com/documentation/)
* [Usar Power BI en un entorno híbrido](https://msdn.microsoft.com/library/dn798994.aspx)

> [!NOTE]
> [Envíe comentarios e información de contacto a través de Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback)

### <a name="community-content"></a>Contenido de la Comunidad
* [Administración de Base de datos SQL de Azure con PowerShell](http://blogs.msdn.com/b/windowsazure/archive/2013/02/07/windows-azure-sql-database-management-with-powershell.aspx)

