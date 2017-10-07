---
title: "Máquinas virtuales de Azure del explorador de servidores aaaAccessing | Documentos de Microsoft"
description: "Obtener una visión general del proceso de crear y administrar máquinas virtuales (VM) Azure en el Explorador de servidores en Visual Studio tooview."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a>Tener acceso a Máquinas virtuales de Azure desde el Explorador de servidores
Con el Explorador de servidores de Visual Studio puede mostrar información acerca de las máquinas virtuales hospedadas por Azure.

## <a name="accessing-virtual-machines-in-server-explorer"></a>Acceso a máquinas virtuales en el Explorador de servidores
Si tiene máquinas virtuales hospedadas por Azure, puede acceder a ellas en el Explorador de servidores. En primer lugar debe iniciar sesión tooyour tooview de suscripción de Azure los servicios móviles. toosign, abra el menú contextual Hola Hola nodos de Azure en el Explorador de servidores y elija **conectar tooMicrosoft Azure**.

### <a name="tooget-information-about-your-virtual-machines"></a>tooget información acerca de las máquinas virtuales
1. En el Explorador de servidores, elige una máquina virtual y, a continuación, elija Hola F4 clave tooshow la ventana de propiedades.
   
    Hello en la tabla siguiente muestra las propiedades que están disponibles, pero son todas de sólo lectura. toochange, usar hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885).
   
   | Propiedad | Description |
   | --- | --- |
   | Nombre DNS |Hola dirección URL con la dirección de Internet de la máquina virtual de Hola Hola. |
   | Environment |Para una máquina virtual, valor de Hola de esta propiedad siempre es producción. |
   | Nombre |nombre de Hola de máquina virtual de Hola. |
   | Tamaño |tamaño de Hola de máquina virtual de hello, que refleja la cantidad de Hola de memoria y espacio en disco que está disponible. Para obtener más información, consulte Procedimiento: creación de los tamaños de las máquinas virtuales. |
   | Estado |Los valores incluyen: Iniciando, Iniciado, Deteniéndose, Detenido y Recuperando estado. Si aparece recuperando estado, estado actual de hello es desconocido. valores de Hello para esta propiedad difieren de los valores de hello que se usan en hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885). |
   | SubscriptionID |Hola Id. de suscripción para su cuenta de Azure. También puede mostrar esta información en hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885) viendo las propiedades de Hola para una suscripción. |
2. Elija un nodo de extremo y, a continuación, ver hello **propiedades** ventana.
3. Hello tabla siguiente describen las propiedades disponibles Hola de puntos de conexión, pero son de solo lectura. tooadd o editar Hola puntos de conexión para una máquina virtual, use hello [portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=213885). 
   
   | Propiedad | Descripción |
   | --- | --- |
   | Nombre |Un identificador para el punto de conexión de Hola. |
   | Private Port |puerto de Hello para la aplicación de tooyour interno de acceso de red. |
   | Protocol |se utiliza el protocolo de Hola Hola capa de transporte para este punto de conexión, TCP o UDP. |
   | Public Port |puerto de Hola que se usa para acceso público tooyour aplicación. |

## <a name="next-steps"></a>Pasos siguientes
toolearn más sobre el uso de las funciones de Azure en Visual Studio, vea [usar Escritorio remoto con Roles de Azure](vs-azure-tools-remote-desktop-roles.md).

