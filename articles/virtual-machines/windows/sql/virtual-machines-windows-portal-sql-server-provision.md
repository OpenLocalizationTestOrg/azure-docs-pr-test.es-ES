---
title: "una máquina Virtual de SQL Server aaaProvision | Documentos de Microsoft"
description: "Crear y conectar tooa máquina de virtual de SQL Server en Azure mediante el portal de Hola. Este tutorial usa el modo de administrador de recursos de Hola."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 1aff691f-a40a-4de2-b6a0-def1384e086e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: infrastructure-services
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: acb52b180103d83715b51b46e2519211c8f0e362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-in-hello-azure-portal"></a>Aprovisionar una máquina virtual de SQL Server en hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
> 
> 

Este tutorial to-end muestra cómo toouse Hola tooprovision portal Azure una máquina virtual que ejecuta SQL Server.

la Galería de máquina virtual (VM) Azure Hola incluye varias imágenes que contienen Microsoft SQL Server. Con unos pocos clics, puede seleccionar uno de hello que imágenes de VM de SQL desde la Galería de Hola y aprovisionar en el entorno de Azure.

En este tutorial, aprenderá lo siguiente:

* [Seleccione una imagen de VM de SQL de la Galería Hola](#select-a-sql-vm-image-from-the-gallery)
* [Configurar y crear Hola VM](#configure-the-vm)
* [Abra Hola máquina virtual con Escritorio remoto](#open-the-vm-with-remote-desktop)
* [Conectarse de forma remota tooSQL Server](#connect-to-sql-server-remotely)

## <a name="select-a-sql-vm-image-from-hello-gallery"></a>Seleccione una imagen de VM de SQL de la Galería Hola

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) con su cuenta.

   > [!NOTE]
   > Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).

2. En el portal de Azure hello, haga clic en **nuevo**. Abre el portal de Hola Hola **New** ventana.

3. Hola **New** ventana, haga clic en **proceso** y, a continuación, haga clic en **ver todas**.

   ![Menú Nuevo proceso](./media/virtual-machines-windows-portal-sql-server-provision/azure-new-compute-blade.png)

4. En el campo de búsqueda de hello, escriba **SQL Server**, y presione ENTRAR.

5. A continuación, haga clic en hello **filtro** icono y seleccione **Microsoft** para el publicador de Hola. Haga clic en **realiza** en resultados de hello filtro ventana toofilter hello tooMicrosoft publicado imágenes de SQL Server.

   ![Ventana Azure Virtual Machines](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-blade2.png)

5. Revise las imágenes de SQL Server disponibles de Hola. Cada imagen identifica una versión de SQL Server y un sistema operativo.

6. Imagen de hello seleccione denominada **licencia gratuita: programador de SQL Server 2016 SP1 en Windows Server 2016**.

   > [!TIP]
   > edición para programadores de Hola se utiliza en este tutorial porque es una edición completa de SQL Server que está disponible para el desarrollo con fines de prueba. Solo paga por costo de Hola de hello VM en ejecución. Sin embargo, son toochoose libre cualquiera de hello imágenes toouse en este tutorial.

   > [!TIP]
   > Imágenes de VM de SQL incluyen los costos de licencia de Hola para SQL Server en hello por minuto de precios de hello VM que se crea (a excepción de las ediciones Developer y rápida de los Hola). SQL Server Developer es gratis para desarrollo y pruebas (no así para producción) y SQL Express es gratis para cargas de trabajo ligeras (menos de 1 GB de memoria, menos de 10 GB de almacenamiento). Hay otra opción toobring your-posee-licencia (BYOL) y pago solo para hello máquina virtual. Esos nombres de imagen tienen el prefijo {BYOL}. 
   >
   > Para más información sobre estas opciones, consulte [Pricing guidance for SQL Server Azure VMs](virtual-machines-windows-sql-server-pricing-guidance.md) (Orientación de precios de máquinas virtuales de SQL Server en Azure).

7. En **Seleccionar un modelo de implementación**, compruebe que la opción **Resource Manager** está seleccionada. El Administrador de recursos es hello recomendada el modelo de implementación de nuevas máquinas virtuales. 

8. Haga clic en **Crear**.

    ![Creación de una máquina virtual de SQL con Resource Manager](./media/virtual-machines-windows-portal-sql-server-provision/azure-compute-sql-deployment-model.png)

## <a name="configure-hello-vm"></a>Configurar Hola VM
Existen cinco ventanas en las que puede configurar una máquina virtual de SQL Server.

| Paso | Description |
| --- | --- |
| **Aspectos básicos** |[Configuración básica](#1-configure-basic-settings) |
| **Tamaño** |[Elección del tamaño de la máquina virtual](#2-choose-virtual-machine-size) |
| **Configuración** |[Configuración de características opcionales](#3-configure-optional-features) |
| **Configuración de SQL Server** |[Configuración de SQL Server](#4-configure-sql-server-settings) |
| **Resumen** |[Hola revisar resumen](#5-review-the-summary) |

## <a name="1-configure-basic-settings"></a>1. Configuración básica

En hello **Fundamentos** ventana, proporcionar Hola siguiente información:

* Escriba un nombre de máquina virtual único en **Nombre**.

* Seleccione **SSD** para tipo de disco de la máquina virtual para un rendimiento óptimo.

* Especifique un **nombre de usuario** para la cuenta de administrador local de hello en hello máquina virtual. Esta cuenta también se agrega toohello SQL Server **sysadmin** rol fijo de servidor.

* Proporcione una contraseña segura en **Contraseña**.

* Si tiene varias suscripciones, compruebe que es correcto para suscripción de Hola Hola nueva máquina virtual.

* Hola **grupo de recursos** , escriba un nombre para un nuevo grupo de recursos. O bien, toouse un grupo de recursos existente haga clic en **utilizar existente**. Un grupo de recursos es una colección de recursos relacionados de Azure (máquinas virtuales, cuentas de almacenamiento, redes virtuales, etc.).

  > [!NOTE]
  > El uso de un grupo de recursos resulta útil si solo está probando o aprendiendo sobre las implementaciones de SQL Server en Azure. Cuando termine con la prueba, elimine tooautomatically delete Hola VM de hello recursos grupo y todos los recursos asociados con ese grupo de recursos. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../../../azure-resource-manager/resource-group-overview.md).

* Seleccione un **ubicación** para hello región de Azure que hospedará esta implementación.

* Haga clic en **Aceptar** configuración de toosave Hola.

    ![Ventana Datos básicos de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-basic.png)

## <a name="2-choose-virtual-machine-size"></a>2. Elección del tamaño de la máquina virtual

En hello **tamaño** paso a paso, elija un tamaño de máquina virtual en hello **elegir un tamaño de** ventana. ventana Hello muestra inicialmente tamaños de máquina recomendada basados en imagen de Hola que seleccionó.

> [!IMPORTANT]
> Hola estimado costo mensual que se muestran en hello **elegir un tamaño de** ventana no incluye los costos de licencias de SQL Server. Este es el costo de Hola de hello VM independiente. Para Hola ediciones Express y Developer de SQL Server, este es el coste total estimado de Hola. Para otras ediciones, vea hello [máquinas virtuales de Windows página de precios](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) y seleccione la edición de destino de SQL Server. Consulte también hello [precios orientación para máquinas virtuales de Azure de SQL Server](virtual-machines-windows-sql-server-pricing-guidance.md).

![Opciones de tamaño de la máquina virtual de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-vm-choose-a-size.png)

Para las cargas de trabajo de producción, vea Hola recomienda tamaños de máquina y la configuración de [prácticas recomendadas de rendimiento para SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-performance.md). Si tiene un tamaño de la máquina que no aparece, haga clic en hello **todas las ver** botón.

> [!NOTE]
> Para más información sobre los tamaños de máquina virtual, consulte [Tamaños de máquina virtual](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Elija el tamaño de la máquina y haga clic en **Seleccionar**.

## <a name="3-configure-optional-features"></a>3. Configuración de características opcionales

En hello **configuración** ventana, configurar el almacenamiento de Azure, redes y la supervisión de la máquina virtual de Hola.

* En **Storage**, seleccione **Sí** en uso de **Managed Disks**.

   > [!NOTE]
   > Microsoft recomienda el uso de Managed Disks para SQL Server. El almacenamiento de identificadores de discos entre bastidores de hello administrado. Además, cuando las máquinas virtuales con discos administrados están en hello mismo conjunto de disponibilidad, Azure distribuye redundancia de tooprovide de recursos de almacenamiento de hello adecuado. Para más información, consulte [Introducción a Azure Managed Disks](../../../storage/storage-managed-disks-overview.md). Para obtener información específica acerca de Managed Disks en un conjunto de disponibilidad, consulte [Uso de Managed Disks para las máquinas virtuales de un conjunto de disponibilidad](../manage-availability.md).

* En **red**, puede aceptar valores de hello rellenado automáticamente. También puede hacer clic en cada característica toomanually configurar hello **red Virtual**, **subred**, **dirección IP pública**, y **degrupodeseguridaddered**. Por motivos de Hola de este tutorial, mantener valores predeterminados de Hola.

* Azure permite **supervisión** con hello misma cuenta de almacenamiento designado para hello VM de forma predeterminada. Puede cambiar estas opciones aquí.

* En **conjunto de disponibilidad**, puede dejar el valor predeterminado es hello **ninguno** para este tutorial. Si tiene previsto tooset los grupos de disponibilidad AlwaysOn de SQL, configurar Hola disponibilidad tooavoid cómo volver a crear Hola virtual machine.  Para obtener más información, consulte [administrar Hola disponibilidad de las máquinas virtuales](../manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Cuando haya terminado la configuración, haga clic en **Aceptar**.

## <a name="4-configure-sql-server-settings"></a>4. Configuración de SQL Server
En hello **configuración de SQL Server** ventana, configurar las opciones específicas y las optimizaciones para SQL Server. configuración de Hola que puede configurar para SQL Server siguientes Hola.

| Configuración |
| --- |
| [Conectividad](#connectivity) |
| [Autenticación](#authentication) |
| [Configuración de almacenamiento](#storage-configuration) |
| [Aplicación de revisiones automatizada](#automated-patching) |
| [Copia de seguridad automatizada](#automated-backup) |
| [Integración del Almacén de claves de Azure](#azure-key-vault-integration) |
| [R Services](#r-services) |

### <a name="connectivity"></a>Conectividad

En **conectividad SQL**, especifique el tipo de Hola de acceso que desee toohello de instancia de SQL Server en esta máquina virtual. Para fines de Hola de este tutorial, seleccione **público (internet)** Hola a tooallow conexiones tooSQL servidor desde equipos o servicios en internet. Con esta opción seleccionada, Azure configura automáticamente el firewall de Hola y tráfico de tooallow de grupo de seguridad de red de hello en el puerto 1433.

![Opciones de conectividad de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-connectivity-alt.png)

> [!TIP]
> De forma predeterminada, SQL Server escucha en un puerto conocido, **1433**. Para mayor seguridad, cambie el puerto de hello en hello toolisten de cuadro de diálogo anterior en un puerto no predeterminado, como 1401. Si lo hace, debe conectarse con ese puerto desde cualquiera de las herramientas de cliente, como SSMS.

tooconnect tooSQL Server a través de hello internet, también debe habilitar autenticación de SQL Server, que se describe en la sección siguiente Hola.

Si prefiere toonot habilitar conexiones toohello motor de base de datos a través de internet de Hola, elija una de las siguientes opciones de hello:

* **Local (dentro de la máquina virtual solo)** tooallow conexiones tooSQL Server únicamente desde dentro de hello máquina virtual.
* **Privada (dentro de la red Virtual)** tooallow conexiones tooSQL servidor desde equipos o servicios en hello misma red virtual.

En general, mejorar la seguridad eligiendo conectividad más restrictivo de Hola que permite a su escenario. Pero todas las opciones de hello son protegibles a través de las reglas del grupo de seguridad de red y la autenticación de Windows o SQL. Puede editar el grupo de seguridad de red después de Hola que se crea la máquina virtual. Para obtener más información, consulte [Consideraciones de seguridad para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-security.md).

> [!NOTE]
> imagen de máquina virtual de Hola para SQL Server Express edition no habilita automáticamente el protocolo de hello TCP/IP. Esto es verdad incluso para hello conectividad pública y privada opciones. Para la edición de Express, debe usar el Administrador de configuración de SQL Server demasiado[habilitar manualmente el protocolo TCP/IP hello](#configure-sql-server-to-listen-on-the-tcp-protocol) después de crear Hola máquina virtual.

### <a name="authentication"></a>Autenticación

Si la autenticación de SQL Server es necesaria, en **Habilitar** under **Habilitar**.

![Autenticación de SQL Server](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-authentication.png)

> [!NOTE]
> Si tiene previsto tooaccess SQL Server sobre Hola internet (es decir, hello las opciones de conectividad pública), debe habilitar la autenticación de SQL aquí. Acceso público toohello SQL Server requiere el uso de Hola de autenticación de SQL.
> 
> 

Si habilita la autenticación de SQL Server, especifique los valores de **Nombre de inicio de sesión** y **Contraseña**. Este nombre de usuario está configurado como un inicio de sesión de autenticación de SQL Server y un miembro de hello **sysadmin** rol fijo de servidor. Para más información sobre los modos de autenticación, consulte [Elegir un modo de autenticación](https://docs.microsoft.com/sql/relational-databases/security/choose-an-authentication-mode) .

Si no habilita la autenticación de SQL Server, puede usar la cuenta de administrador local de hello en la instancia de SQL Server de hello VM tooconnect toohello.

### <a name="storage-configuration"></a>Configuración de almacenamiento

Haga clic en **configuración de almacenamiento** requisitos de almacenamiento de toospecify Hola.

![Configuración de almacenamiento de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-storage.png)

> [!NOTE]
> Si ha configurado manualmente el almacenamiento de información de máquina virtual toouse estándar, esta opción no está disponible. La optimización del almacenamiento automático está disponible solo para Premium Storage.

> [!TIP]
> número de Hola de se detiene y los límites superiores de Hola de cada control deslizante es dependientes de tamaño de Hola de máquina virtual que seleccionó. Una máquina virtual más grande y más eficaz es capaz de tooscale más hacia arriba.

Puede especificar requisitos como operaciones de entrada/salida por segundo (IOPS), el rendimiento en MB/s y el tamaño de almacenamiento total. Configurar estos valores mediante Hola deslizante escalas. Puede cambiar estos valores de almacenamiento en función de la carga de trabajo. portal Hola calcula automáticamente el número de discos tooattach de Hola y configurar según estos requisitos.

En **almacenamiento optimizado para**, seleccione una de las siguientes opciones de hello:

* **General** es el valor predeterminado de Hola y es compatible con la mayoría de las cargas de trabajo.
* **Transaccional** procesamiento optimiza el almacenamiento de Hola para cargas de trabajo OLTP tradicionales de la base de datos.
* **Almacenamiento de datos** optimiza el almacenamiento de Hola para cargas de trabajo informes y análisis.

### <a name="automated-patching"></a>Aplicación de revisiones automatizada

**Automated patching** está habilitada de forma predeterminada. Aplicación de revisiones automatizada permite que el sistema de operativo de hello y SQL Server de revisión de tooautomatically de Azure. Especifique un día de semana de hello, la hora y la duración de una ventana de mantenimiento. Azure realiza la aplicación de revisión en esta ventana de mantenimiento. programación Hello de la ventana de mantenimiento utiliza la configuración regional VM de hello para el tiempo. Si no desea que el sistema de operativo de hello y SQL Server de revisión de Azure tooautomatically, haga clic en **deshabilitar**.  

![Aplicación de revisiones automatizada de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-patching.png)

Para más información, consulte [Aplicación de revisiones automatizadas para SQL Server en Azure Virtual Machines (implementación clásica)](virtual-machines-windows-sql-automated-patching.md).

### <a name="automated-backup"></a>Copia de seguridad automatizada

Habilite las copias de seguridad automáticas en todas las bases de datos en **Copia de seguridad automatizada**. La copia de seguridad automatizada está deshabilitada de forma predeterminada.

Al habilitar la copia de seguridad automatizada de SQL, puede configurar siguiente hello:

* El período de retención (días) de las copias de seguridad
* Toouse de cuenta de almacenamiento para las copias de seguridad
* La opción de cifrado y la contraseña de las copias de seguridad
* La copia de seguridad de bases de datos del sistema
* La configuración de la programación de copia de seguridad

Haga clic en de tooencrypt Hola copia de seguridad, **habilitar**. A continuación, especifique hello **contraseña**. Azure crea un certificado de las copias de seguridad de tooencrypt Hola y Hola utiliza especifica contraseña tooprotect ese certificado.

![Copia de seguridad automatizada de SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-autobackup2.png)

 Para obtener más información, vea [Copia de seguridad automatizada para SQL Server en Azure Virtual Machines](virtual-machines-windows-sql-automated-backup.md).

### <a name="azure-key-vault-integration"></a>Integración de Azure Key Vault

toostore secretos de seguridad de Azure para el cifrado, haga clic en **integración del almacén de claves de Azure** y haga clic en **habilitar**.

![Integración de Azure Key Vault con SQL](./media/virtual-machines-windows-portal-sql-server-provision/azure-sql-arm-akv.png)

Hello tabla siguiente enumeran Hola parámetros necesarios tooconfigure integración del almacén de claves de Azure.

| PARÁMETRO | Description | EJEMPLO: |
| --- | --- | --- |
| **Dirección URL del Almacén de claves** |ubicación de Hello del almacén de claves de Hola. |https://contosokeyvault.vault.azure.net/ |
| **Nombre de entidad de seguridad** |Nombre de la entidad de servicio de Azure Active Directory Esto se conoce también como Id. Este nombre también es que se hace referencia tooas hello identificador de cliente. |fde2b411-33d5-4e11-af04eb07b669ccf2 |
| **Secreto de entidad de seguridad** |Secreto de la entidad de seguridad de servicio de Azure Active Directory Este secreto también es que se hace referencia tooas hello secreto del cliente. |9VTJSQwzlFepD8XODnzy8n2V01Jd8dAjwm/azF1XDKM= |
| **Nombre de credencial** |**Nombre de la credencial**: integración de claves crea una credencial de SQL Server, lo que permite Hola VM toohave acceso toohello el almacén de claves. Elija un nombre para esta credencial. |mycred1 |

Para más información, consulte [Configuración de la integración de Azure Key Vault para SQL Server en Azure Virtual Machines](virtual-machines-windows-ps-sql-keyvault.md).

### <a name="r-services"></a>R Services

Tienes Hola opción tooenable [SQL Server R Services](https://msdn.microsoft.com/library/mt604845.aspx). Esto le permite análisis toouse avanzada con SQL Server 2016. Haga clic en **habilitar** en hello **configuración de SQL Server** ventana.

> [!NOTE]
> Para SQL Server 2016 Developer Edition, esta opción está deshabilitada incorrectamente por el portal de Hola. Para Developer Edition, debe habilitar manualmente R Services después de crear la máquina virtual.

![Habilitación de SQL Server R Services](./media/virtual-machines-windows-portal-sql-server-provision/azure-vm-sql-server-r-services.png)

Cuando termine de definir la configuración de SQL Server, haga clic en **Aceptar**.

## <a name="5-review-hello-summary"></a>5. Hola revisar resumen

En hello **resumen** ventana, revisión Hola resumen y haga clic en **compra** toocreate SQL Server, grupo de recursos especifican para esta máquina virtual.

Puede supervisar la implementación Hola de hello portal de Azure. Hola **notificaciones** situado en la parte superior de Hola de pantalla de bienvenida muestra el estado básico de implementación de Hola.

> [!NOTE]
> tooprovide, con una idea en la implementación de tiempo de espera, implementa una región de UU toohello de VM de SQL con la configuración predeterminada. Esta implementación de prueba tardó un total de minutos 26 toocomplete. Pero podría experimentar un tiempo de implementación más rápido o más lento en función de su región y de la configuración seleccionada.

## <a name="open-hello-vm-with-remote-desktop"></a>Abra Hola máquina virtual con Escritorio remoto

Usar hello siguiendo los pasos tooconnect toohello SQL Server virtual máquina con Escritorio remoto:

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Después de conectar la máquina virtual de SQL Server de toohello, puede iniciar SQL Server Management Studio y conectarse con la autenticación de Windows con sus credenciales de administrador local. Si ha habilitado la autenticación de SQL Server, también puede conectar con la autenticación de SQL con inicio de sesión SQL de Hola y la contraseña configurados durante el aprovisionamiento.

Acceso toohello máquina permite toodirectly cambio máquina y la configuración de SQL Server según sus requisitos. Por ejemplo, puede configurar el firewall de Hola o cambiar la configuración de SQL Server.

## <a name="enable-tcpip-for-developer-and-express-editions"></a>Habilitación de TCP/IP para las ediciones Developer y Express

Al aprovisionar una nueva VM de SQL Server, Azure no habilita automáticamente protocolo TCP/IP de hello para el programador de SQL Server y las ediciones Express. Hola a continuación se explica cómo toomanually habilitar TCP/IP para que puedan conectarse de forma remota mediante una dirección IP.

Hola a consecuencia del uso de pasos **Administrador de configuración de SQL Server** tooenable protocolo de hello TCP/IP para SQL Server Developer y las ediciones Express.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-toosql-server-remotely"></a>Conectarse de forma remota tooSQL Server

En este tutorial, seleccionamos **público** acceso de máquina virtual de Hola y **autenticación de SQL Server**. Estas conexiones de SQL Server configuración Hola configurada automáticamente máquinas virtuales tooallow desde cualquier cliente sobre Hola internet (suponiendo que disponen de inicio de sesión SQL correcta hello).

> [!NOTE]
> Si no ha seleccionado pública durante el aprovisionamiento, puede cambiar la configuración de conectividad SQL a través del portal de hello después de aprovisionar. Para más información, consulte [Cambio de la configuración de conectividad SQL](virtual-machines-windows-sql-connect.md#change).

Hola las secciones siguientes muestra cómo Hola a tooconnect tooyour instancia de SQL Server en la máquina virtual desde otro equipo en internet.

> [!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Pasos siguientes

Para obtener otra información acerca del uso de SQL Server en Azure, consulte [SQL Server en máquinas virtuales Azure](virtual-machines-windows-sql-server-iaas-overview.md) hello y [Frequently Asked Questions](virtual-machines-windows-sql-server-iaas-faq.md).
