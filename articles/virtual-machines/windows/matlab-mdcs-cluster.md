---
title: "aaaMATLAB agrupa en máquinas virtuales | Documentos de Microsoft"
description: "Usar máquinas virtuales de Microsoft Azure toocreate toorun de clústeres de servidor de cálculo distribuido MATLAB las cargas de trabajo MATLAB paralelos de proceso intensivo"
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Creación de clústeres de MATLAB Distributed Computing Server en Máquinas virtuales de Azure
Use Microsoft Azure virtual máquinas toocreate uno o clústeres de servidores de informática distribuida de más MATLAB toorun las cargas de trabajo MATLAB paralelos de proceso intensivo. Instale el software de servidor de cálculo distribuido MATLAB en un toouse de máquina virtual como una imagen base y use una plantilla de inicio rápido de Azure o un script de PowerShell de Azure (disponible en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy y administrar clústeres de Hola. Después de la implementación, conectar toohello clúster toorun las cargas de trabajo.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Información acerca de MATLAB y MATLAB Distributed Computing Server 
Hola [MATLAB](http://www.mathworks.com/products/matlab/) plataforma está optimizada para resolver problemas de ingeniería y científicos. Los usuarios MATLAB con simulaciones a gran escala y tareas de procesamiento de datos pueden usar paralelo MathWorks informática toospeed productos seguridad sus cargas de trabajo de proceso intensivo aprovechando las ventajas de clústeres de cálculo y los servicios de la cuadrícula. [Parallel Computing Toolbox](http://www.mathworks.com/products/parallel-computing/) permite a los usuarios de MATLAB usar las aplicaciones en paralelo y aprovechar las ventajas de los procesadores de núcleo múltiple, GPU y clústeres de proceso. [Servidor de cálculo distribuido MATLAB](http://www.mathworks.com/products/distriben/) permite MATLAB usuarios tooutilize muchos equipos en un clúster de cálculo.

Mediante el uso de máquinas virtuales de Azure, puede crear clústeres de servidor de cálculo distribuido MATLAB que tengan todas Hola mismo trabajo paralelo de toosubmit disponibles de mecanismos como clústeres locales, como trabajos interactivos, trabajos por lotes, tareas independientes, y tareas de comunicación. El uso de Azure junto con la plataforma MATLAB hello tiene muchos tooprovisioning ventajas en comparación con utilizando tradicional locales y en hardware: tamaños de un intervalo de máquina virtual, creación de clústeres a petición por lo que solo paga por los recursos de proceso de hello usa, y Hola capacidad tootest los modelos a escala.  

## <a name="prerequisites"></a>Requisitos previos
* **Equipo cliente** -necesitará un toocommunicate del equipo de cliente basada en Windows con hello clúster de servidor de cálculo distribuido MATLAB y Azure después de la implementación.
* **Azure PowerShell** -vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) tooinstall en el equipo cliente.
* **Suscripción de Azure** : si no tiene ninguna, puede crear una [cuenta gratuita](https://azure.microsoft.com/free/) en un par de minutos. En los clústeres más grandes, considere la posibilidad de una suscripción de pago por uso u otras opciones de compra.
* **Cuota de núcleos** -deberá tooincrease Hola core cuota toodeploy un clúster grande o más de un servidor de cálculo distribuido MATLAB. tooincrease una cuota, [abrir una solicitud de soporte al cliente en línea](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sin cargo.
* **Licencias MATLAB, Parallel Computing Toolbox y servidor de cálculo distribuido MATLAB** -secuencias de comandos de hello asumen que hello [MathWorks hospedado License Manager](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) se utiliza para todas las licencias.  
* **Software de servidor de cálculo distribuido MATLAB** -se instalará en una máquina virtual que se usará como imagen de máquina virtual base hello para el clúster de hello las máquinas virtuales.

## <a name="high-level-steps"></a>Pasos de alto nivel
toouse máquinas virtuales de Azure para los clústeres de servidor de cálculo distribuido MATLAB, hello siguientes pasos de alto nivel son necesarios. Instrucciones detalladas se encuentran en la documentación de Hola que acompaña a plantilla de inicio rápido de Hola y secuencias de comandos en [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Creación de una imagen de máquina virtual base**  

   * Descargue e instale el software MATLAB Distributed Computing Server en esta máquina virtual.

     > [!NOTE]
     > Este proceso puede tardar un par de horas, pero solo tiene toodo, una vez para cada versión de MATLAB que use.   
     >
     >
2. **Creación de uno o varios clústeres**  

   * Usar script de PowerShell de hello proporcionado o use Hola quickstart plantilla toocreate un clúster desde la imagen de máquina virtual base Hola.   
   * Administrar clústeres de hello mediante script de PowerShell de hello proporcionado que le permite toolist, pausar, reanudar y clústeres de eliminación.

## <a name="cluster-configurations"></a>Configuraciones de clústeres
Actualmente, plantilla y script de creación de clúster de hello permiten toocreate una sola topología de servidor de cálculo distribuido MATLAB. Si lo desea, cree uno o más clústeres adicionales en los que cada clúster tendrá un número diferente de máquinas virtuales de trabajo, usará diferentes tamaños de máquina virtual, etc.

### <a name="matlab-client-and-cluster-in-azure"></a>Clúster y cliente de MATLAB en Azure
nodo de cliente MATLAB Hello, un nodo programador de trabajos de MATLAB y servidor distribuido MATLAB informática "trabajo" nodos se configuran todos como máquinas virtuales de Azure en una red virtual, tal y como se muestra en hello siguiente figura.


* Hola toouse de clúster, conéctese al nodo de cliente de escritorio remoto toohello. nodo de cliente de Hello ejecuta a cliente MATLAB Hola.
* nodo de cliente Hello tiene un recurso compartido de archivos que puede tener acceso a todos los trabajadores.
* MathWorks hospedado License Manager se usa para comprobaciones de licencia de Hola para todo el software MATLAB.
* De forma predeterminada, se crea un trabajo de servidor de cálculo distribuido MATLAB por núcleo de trabajador de hello las máquinas virtuales, pero puede especificar cualquier número.

## <a name="use-an-azure-based-cluster"></a>Uso de un clúster de Azure
Al igual que con otros tipos de clústeres de servidor de cálculo distribuido MATLAB, deberá toouse Hola Administrador de clústeres de perfil en hello MATLAB cliente (en el cliente de hello VM) toocreate un perfil de clúster de programador de trabajos de MATLAB.

![Cluster Profile Manager](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones detalladas toodeploy y administrar clústeres de servidor de cálculo distribuido MATLAB en Azure, vea hello [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) repositorio que contiene plantillas de Hola y secuencias de comandos.
* Vaya toohello [MathWorks sitio](http://www.mathworks.com/) para obtener documentación detallada de MATLAB y servidor de cálculo distribuido MATLAB.
