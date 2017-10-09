---
title: "clúster de aaaSet la híbrida de HPC Pack en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Microsoft HPC Pack y Azure tooset una copia de seguridad un pequeño, híbrida alto rendimiento informático () clúster de HPC"
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a>Configuración de un clúster híbrido de informática de alto rendimiento (HPC) con nodos de proceso de Azure a petición y Microsoft HPC Pack
Use Microsoft HPC Pack 2012 R2 y Azure tooset seguridad un pequeño, híbrida informática de alto rendimiento clúster (HPC). clúster de Hello mostrado en este artículo está formado por un nodo principal de HPC Pack local y algunos nodos implementar a petición en un Azure servicio en la nube de proceso. A continuación, puede ejecutar trabajos de proceso en clúster híbrido de Hola.

![Clúster híbrido de HPC][Overview] 

Este tutorial muestra un enfoque suele llamar clúster "ráfaga toohello en la nube," aplicaciones de proceso intensivo de toorun toouse escalable, en la demanda de recursos de Azure.

En este tutorial se supone que no cuenta con experiencia previa con los clústeres informáticos o con HPC Pack. Está previsto toohelp solo implementar un clúster de cálculo híbrido rápidamente con fines de demostración. Para las consideraciones y toodeploy pasos clúster HPC Pack híbrido a mayor escala en un entorno de producción o toouse HPC Pack 2016, vea hello [obtener instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493). Para otros escenarios de HPC Pack, incluida la implementación automatizada de clústeres en máquinas virtuales de Azure, consulte [Opciones de clúster de HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="prerequisites"></a>Requisitos previos
* **Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos.
* **Un equipo local que ejecuta Windows Server 2012 R2 o Windows Server 2012** -usar este equipo como nodo principal de Hola Hola del clúster de HPC. Si todavía no tiene Windows Server, puede descargar e instalar una [versión de evaluación](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).
  
  * equipo de Hello debe ser tooan Unidos a un dominio de Active Directory. Para fines de prueba, puede configurar el equipo del nodo principal de Hola como un controlador de dominio. tooadd Hola rol de servidor Servicios de dominio de Active Directory y promocionar el equipo del nodo principal Hola como un controlador de dominio, consulte la documentación de Hola para Windows Server.
  * toosupport HPC Pack, sistema operativo de hello debe instalarse en uno de estos idiomas: inglés, japonés o chino (simplificado).
  * Compruebe que estén instaladas las actualizaciones importantes y esenciales.
* **HPC Pack 2012 R2** - [descargar](http://go.microsoft.com/fwlink/p/?linkid=328024) paquete de instalación de hello para la versión más reciente de hello libre de cargo y copia Hola archivos toohello equipo del nodo principal. Elija archivos de instalación de hello mismo idioma que la instalación de Windows Server.

    >[!NOTE]
    > Si desea toouse HPC Pack 2016 en lugar de HPC Pack 2012 R2, se necesita configuración adicional. Vea hello [obtener instrucciones detalladas](http://go.microsoft.com/fwlink/p/?LinkID=200493).
    > 
* **Cuenta de dominio** -se debe configurar esta cuenta con permisos de administrador local en el nodo principal de hello tooinstall HPC Pack.
* **Conectividad TCP en el puerto 443** de hello tooAzure de nodo principal.

## <a name="install-hpc-pack-on-hello-head-node"></a>Instalar HPC Pack en el nodo principal de Hola
En primer lugar, debe instalar Microsoft HPC Pack en un equipo local con Windows Server. Este equipo se convierte en del nodo principal del clúster de Hola Hola.

1. Inicie sesión en el nodo principal de toohello con una cuenta de dominio que tenga permisos de administrador local.

2. Iniciar Hola Asistente para la instalación de HPC Pack ejecutando Setup.exe desde archivos de instalación de HPC Pack Hola.

3. En hello **el programa de instalación de HPC Pack 2012 R2** pantalla, haga clic en **nueva instalación o agregar nuevas características de instalación de existente tooan**.

    ![Instalación de HPC Pack 2012][install_hpc1]

4. En hello **página del acuerdo de usuario de Software de Microsoft**, haga clic en **siguiente**.

5. En hello **Seleccionar tipo de instalación** página, haga clic en **crear un nuevo clúster HPC mediante la creación de un nodo principal**y, a continuación, haga clic en **siguiente**.

6. Asistente de Hello ejecuta varias pruebas previas a la instalación. Haga clic en **siguiente** en hello **reglas de instalación** página si se superan todas las pruebas. En caso contrario, revise la información de hello proporcionada y realice los cambios necesarios en su entorno. A continuación, ejecutar pruebas de hello nuevo o si es necesario iniciar Hola Asistente para la instalación de nuevo.
7. En hello **configuración de base de datos de HPC** página, asegúrese de que **nodo principal** está seleccionada para todas las bases de datos HPC y, a continuación, haga clic en **siguiente**. 

    ![Configuración de la base de datos][install_hpc4]

8. Aceptar selecciones de predeterminado en hello las páginas restantes del Asistente para saludo. En hello **instalar los componentes necesarios** página, haga clic en **instalar**.
   
    ![Instalación][install_hpc6]

9. Una vez finalizada la instalación de hello, desactive la opción **iniciar el Administrador de clúster de HPC** y, a continuación, haga clic en **finalizar**. (El Administrador de clústeres HPC se inicia en un paso posterior).
   
    ![Finalizar][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a>Preparar Hola suscripción de Azure
Realizar Hola siguiendo los pasos de hello [portal de Azure](https://portal.azure.com) con su suscripción de Azure. Después de completar estos pasos, puede implementar nodos de Azure desde el nodo principal de hello en local. 
  
  > [!NOTE]
  > Anote también el Id. de la suscripción de Azure, ya que lo necesitará más adelante. Encuentra el Id. de hello en **suscripciones** en el portal de Hola.
  > 

### <a name="upload-hello-default-management-certificate"></a>Cargar certificado predeterminado de administración de Hola
HPC Pack se instala un certificado autofirmado en el nodo principal de hello, denominado certificado de administración de Azure de HPC de Microsoft predeterminado hello, que puede cargar como un certificado de administración de Azure. Este certificado se proporciona para pruebas y conexión de las implementaciones de prueba de concepto toosecure Hola entre hello Azure y el nodo principal.

1. Desde el equipo de nodo principal de hello, inicie sesión en toohello [portal de Azure](https://portal.azure.com).

2. Haga clic en **Suscripciones** > *nombre_de_la_suscripción*.

3. Haga clic en **Certificados de administración** > **Cargar**.4. Busque en el nodo principal de Hola para hello archivo C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer. Luego, haga clic en **Cargar**.

   
Hola **administración de Azure de HPC predeterminado** certificado aparece en la lista de Hola de certificados de administración.

### <a name="create-an-azure-cloud-service"></a>Crear un servicio en la nube de Azure
> [!NOTE]
> Para obtener el mejor rendimiento, crear servicio en la nube hello y cuenta de almacenamiento de hello (en un paso posterior) en hello misma región geográfica.
> 
> 

1. En el portal de hello, haga clic en **servicios (clásico) en la nube** > **+ agregar**.

2.  Escriba un nombre DNS para el servicio de hello, elija un grupo de recursos y una ubicación y, a continuación, haga clic en **crear**.


### <a name="create-an-azure-storage-account"></a>Creación de una cuenta de Azure Storage
1. En el portal de hello, haga clic en **cuentas de almacenamiento (clásica)** > **+ agregar**.

2. Escriba un nombre para la cuenta de hello y seleccione hello **clásico** modelo de implementación.

3. Elija un grupo de recursos y una ubicación y deje los valores predeterminados de las demás opciones. A continuación, haga clic en **Crear**.

## <a name="configure-hello-head-node"></a>Configurar el nodo principal de Hola
Administrador de clústeres HPC toodeploy toouse nodos de Azure y los trabajos de toosubmit, en primer lugar realizar algunos pasos de configuración de clúster necesarios.

1. En el nodo principal de hello, inicie el Administrador de clúster de HPC. Si hello **Seleccionar nodo principal** aparece el cuadro de diálogo, haga clic en **equipo Local**. Hola **lista de tareas de implementación** aparece.

2. En **Tareas de implementación necesarias**, haga clic en **Configurar la red**.
   
    ![Configuración de la red][config_hpc2]

3. En el Asistente para configuración de red de hello, seleccione **todos los nodos solo en una red empresarial** (topología 5). Esta configuración de red es más sencillo para fines de demostración de hello.
   
    ![Topología 5][config_hpc3]
   
4. Haga clic en **siguiente** tooaccept valores predeterminados Hola restantes páginas del Asistente para saludo. A continuación, en hello **revisión** , haga clic en **configurar** configuración de red de toocomplete Hola.

5. Hola **lista de tareas de implementación**, haga clic en **proporcione las credenciales de instalación**.

6. Hola **credenciales de instalación** cuadro de diálogo, escriba hello las credenciales de cuenta de dominio de Hola que usa tooinstall HPC Pack. y, a continuación, haga clic en **Aceptar**. 
   
    ![Credenciales de instalación][config_hpc6]
   
7. Hola **lista de tareas de implementación**, haga clic en **configurar Hola denominación de nuevos nodos**.

8. Hola **especificar serie de nombres de nodo** diálogo cuadro, acepte el predeterminado de hello nomenclatura serie y haga clic en **Aceptar**. Complete este paso, aunque hello nodos de Azure que agregue en este tutorial se asignan automáticamente.
   
    ![Nomenclatura de nodos][config_hpc8]
   
9. Hola **lista de tareas de implementación**, haga clic en **crear una plantilla de nodo**. Más adelante en el tutorial de hello, usar clúster de toohello Hola nodos plantilla tooadd nodos de Azure.

10. En Hola Asistente Crear plantilla de nodo, haga lo Hola siguientes:
    
    a. En hello **Elegir tipo de plantilla de nodo** página, haga clic en **plantilla de nodo de Windows Azure**y, a continuación, haga clic en **siguiente**.
    
    ![Plantilla de nodo][config_hpc10]
    
    b. Haga clic en **siguiente** nombre de plantilla predeterminado de tooaccept Hola.
    
    c. En hello **proporcionan información de suscripción** página, escriba el identificador de suscripción de Azure (está disponible en la información de cuenta de Azure). Luego, en **Certificado de administración**, busque **Default Microsoft HPC Azure Management**. A continuación, haga clic en **Siguiente**.
    
    ![Plantilla de nodo][config_hpc12]
    
    d. En hello **proporcionar información del servicio** página, servicio de nube seleccione hello y cuenta de almacenamiento de Hola que creó en el paso anterior. A continuación, haga clic en **Siguiente**.
    
    ![Plantilla de nodo][config_hpc13]
    
    e. Haga clic en **siguiente** tooaccept valores predeterminados Hola restantes páginas del Asistente para saludo. A continuación, en hello **revisión** , haga clic en **crear** plantilla de nodo de toocreate Hola.
    
    > [!NOTE]
    > De forma predeterminada, Hola nodos de Azure plantilla incluyen la configuración para toostart (aprovisionar) y los nodos de hello detener manualmente, mediante el Administrador de clúster de HPC. Opcionalmente, puede configurar una programación toostart y detener Hola automáticamente los nodos de Azure.
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a>Agregar nodos de Azure toohello clúster
Ahora use clúster de toohello Hola nodos plantilla tooadd nodos de Azure. Agregar clúster de hello nodos toohello almacena su información de configuración para que pueda iniciar (aprovisionar) usarlas en cualquier momento en el servicio de nube de Hola. Su suscripción solo obtiene cobra por nodos de Azure después de que se ejecutan instancias de Hola Hola del servicio en nube.

Siga estos pasos tooadd dos pequeños los nodos.

1. En el Administrador de clústeres HPC, haga clic en **Administración de nodos** (llamada **Administración de recursos** en versiones recientes de HPC Pack) > **Agregar nodo**.
   
    ![Agregar nodo][add_node1]

2. En Hola Asistente para agregar nodos, en hello **Seleccionar método de implementación** página, haga clic en **nodos de agregar Windows Azure**y, a continuación, haga clic en **siguiente**.
   
    ![Agregar un nodo de Azure][add_node1_1]

3. En hello **especificar nuevos nodos** página, plantilla de nodo de Azure Hola select que creó anteriormente (llamado de forma predeterminada **plantilla predeterminada de AzureNode**). A continuación, especifique **2** nodos de tamaño **pequeño** y, a continuación, haga clic en **Siguiente**.
   
    ![Especificar los nodos][add_node2]
   
4. En hello **finalización Hola Asistente para agregar nodos** página, haga clic en **finalizar**.
    
     Ahora aparecerán dos nodos llamados **AzureCN-0001** y **AzureCN-0002** en el administrador de clústeres de HPC. Ambos están en hello **no implementado** estado.
   
    ![Nodos agregados][add_node3]

## <a name="start-hello-azure-nodes"></a>Iniciar Hola nodos de Azure
Si desea toouse recursos de clúster de hello en Azure, use el Administrador de clústeres de HPC toostart (aprovisionar) Hola nodos de Azure y ponen en línea.

1. Haga clic en Administrador de clústeres de HPC, **administración de nodos** (denominado **administración de recursos** en las versiones actuales de HPC Pack), y seleccione Hola nodos de Azure.

2. Haga clic en **Inicio** y, luego, en **Aceptar**.
   
   ![Iniciar los nodos][add_node4]
   
    nodos de Hello transición toohello **Provisioning** estado. Hola de vista aprovisionamiento Hola de tootrack registro aprovisionamiento de progreso.
   
    ![Aprovisionar nodos][add_node6]

3. Después de unos minutos, hello nodos de Azure finalizar el aprovisionamiento y se encuentran en hello **Offline** estado. En este estado, instancias de rol de hello están ejecutando pero aún no pueden aceptar trabajos del clúster.

4. tooconfirm que Hola instancias de rol se está ejecutando, Hola portal de Azure, haga clic en **servicios en la nube (clásico)** > *your_cloud_service_name*.
   
   Debería ver dos **HpcWorkerRole** instancias (nodos) que se ejecutan en el servicio de Hola. HPC Pack automáticamente también implementa dos **HpcProxy** instancias de comunicación de toohandle (tamaño medio) entre el nodo principal de Hola y Azure.

   ![Instancias en ejecución][view_instances1]

5. nodos de Azure de hello toobring toorun en línea clúster trabajos, seleccione Hola nodos, menú contextual y, a continuación, haga clic en **poner en conexión**.
   
    ![Nodos desconectados][add_node7]
   
    Administrador de clústeres HPC indica que los nodos de hello en hello **Online** estado.

## <a name="run-a-command-across-hello-cluster"></a>Ejecutar un comando en el clúster de Hola
instalación de hello toocheck, use Hola HPC Pack **clusrun** comando toorun un comando o una aplicación en uno o más nodos del clúster. Como ejemplo sencillo, use **clusrun** tooget configuración de IP Hola Hola nodos de Azure.

1. En el nodo principal de hello, abra un símbolo del sistema como administrador.

2. Escriba el siguiente comando de hello:
   
    `clusrun /nodes:azurecn* ipconfig`

3. Si se le solicita, escriba la contraseña de administrador del clúster. Debería ver la salida del comando siguiente de toohello similar.
   
    ![clusrun][clusrun1]

## <a name="run-a-test-job"></a>Ejecución de un trabajo de prueba
Ahora, envíe un trabajo de prueba que se ejecuta en el clúster de hello híbrido. Este ejemplo es un trabajo simple de barrido paramétrico (un tipo de cálculo intrínsecamente paralelo). En este ejemplo se ejecuta subtareas que agregar una tooitself entero mediante hello **establecer /a** comando. Todos los nodos Hola Hola clúster contribuyen toofinishing Hola subtareas para números enteros de 1 too100.

1. En el Administrador de clústeres HPC, haga clic en **Administración de trabajos** > **Nuevo trabajo de barrido paramétrico**.
   
    ![Nuevo trabajo][test_job1]

2. Hola **nuevo trabajo de barrido paramétrico** cuadro de diálogo **línea de comandos**, tipo `set /a *+*` (sobrescribiendo la línea de comandos de hello predeterminada que aparece). Deje los valores predeterminados para hello restantes de la configuración y, a continuación, haga clic en **enviar** trabajo de hello toosubmit.
   
    ![Barrido paramétrico][param_sweep1]

3. Cuando finaliza el trabajo de hello, haga doble clic en hello **mi tarea de barrido** trabajo.

4. Haga clic en **tareas vista**y, a continuación, haga clic en una salida de hello calculado tooview subtarea de esa subtarea.
   
    ![Resultados de la tarea][view_job361]

5. toosee qué nodo realiza el cálculo de hello esa subtarea, haga clic en **asignar nodos**. (Su clúster podría mostrar un nombre de nodo diferente).
   
    ![Resultados de la tarea][view_job362]

## <a name="stop-hello-azure-nodes"></a>Detener Hola nodos de Azure
Después de probar clúster hello, detener tooyour cuenta de hello nodos de Azure tooavoid cobros innecesarios. Este paso detiene el servicio de nube de Hola y quite instancias de rol de Azure de Hola.

1. En el Administrador de clústeres HPC, en **Administración de nodos** (llamada **Administración de recursos** en versiones anteriores de HPC Pack), seleccione los dos nodos de Azure. Luego, haga clic en **Detener**.
   
    ![Detener los nodos][stop_node1]

2. Hola **nodos detener Windows Azure** cuadro de diálogo, haga clic en **detener**. 
   
3. nodos de Hello transición toohello **detener** estado. Después de unos minutos, el Administrador de clústeres de HPC muestra que son nodos de hello **no implementado**.
   
    ![Nodos no implementados][stop_node4]

4. Hola a tooconfirm que instancias de rol de hello ya no se ejecutan en Azure, en haga clic en de portal, Azure **servicios (clásico) en la nube** > *your_cloud_service_name*. No hay instancias se implementan en el entorno de producción de hello. 
   
    Con esto finaliza el tutorial de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Examinar la documentación de Hola para [HPC Pack](https://technet.microsoft.com/library/cc514029).
* Consulte tooset de una implementación de clúster de HPC Pack a mayor escala, híbrida [tooAzure instancias de rol de trabajo con Microsoft HPC Pack en ráfagas](http://go.microsoft.com/fwlink/p/?LinkID=200493).
* Para otro toocreate de formas de un clúster de HPC Pack en Azure, incluido con plantillas de Azure Resource Manager, consulte [opciones de clúster HPC con Microsoft HPC Pack en Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png
