---
title: las cuentas de almacenamiento de Azure pila aaaManage | Documentos de Microsoft
description: "Obtenga información acerca de cómo toofind, administrar, recuperar y recuperar las cuentas de almacenamiento de Azure pila"
services: azure-stack
documentationcenter: 
author: AniAnirudh
manager: darmour
editor: 
ms.assetid: 627d355b-4812-45cb-bc1e-ce62476dab34
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 4/6/2017
ms.author: anirudha
ms.openlocfilehash: 350c92d6b5ce9b1582ede0256c4d3d23bdd94901
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-storage-accounts-in-azure-stack"></a>Administración de cuentas de almacenamiento en Azure Stack
Obtenga información acerca de cómo recuperar las cuentas de almacenamiento de toomanage en toofind de pila de Azure y recuperar la capacidad de almacenamiento en función de las necesidades del negocio.

## <a name="find"></a>Búsqueda de una cuenta de almacenamiento
Hola lista de cuentas de almacenamiento en región Hola se puede ver en la pila de Azure mediante:

1. En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.
2. Inicie sesión en toohello portal de administración de la pila de Azure como un operador en la nube (mediante las credenciales que proporcionó durante la implementación)
3. En el panel predeterminado de hello – encontró hello **administración región** lista y haga clic en la región de Hola que desee tooexplore. Por ejemplo, **(local**).
   
   ![](media/azure-stack-manage-storage-accounts/image1.png)
4. Seleccione **almacenamiento** de hello **proveedores de recursos** lista.
   
   ![](media/azure-stack-manage-storage-accounts/image2.png)
5. Ahora, en el módulo de administrador de proveedor de recursos de almacenamiento de hello: desplácese hacia abajo hasta hello **cuentas de almacenamiento** ficha y haga clic en él.
   
   ![](media/azure-stack-manage-storage-accounts/image3.png)
   
   página resultante Hello es la lista de Hola de cuentas de almacenamiento en dicha región.
   
   ![](media/azure-stack-manage-storage-accounts/image4.png)

De forma predeterminada, hello 10 primeros cuentas se muestran. Puede elegir toofetch más haciendo clic en hello **cargar más** vínculo Hola final de la lista de Hola.

OR

Si está interesado en una cuenta de almacenamiento determinado: puede **filtro y fetch Hola cuentas relevantes** solo.


**toofilter para las cuentas:**

1. Haga clic en **filtro** princip Hola de hoja de Hola.
2. En el módulo de filtro de hello, permite toospecify **nombre de la cuenta**, **Id. de suscripción** o **estado** lista de hello toofine optimización del almacenamiento de cuentas toobe muestra. Use esta información de la manera adecuada.
3. Haga clic en **Update**(Actualizar). lista de Hello debe actualizar en consecuencia.
   
    ![](media/azure-stack-manage-storage-accounts/image5.png)
4. filtro de Hola tooreset: haga clic en **filtro**, borrar las selecciones y actualizar.

cuadro de texto de búsqueda de Hello (de hello parte superior de hoja de lista de cuentas de almacenamiento de hello) le permite resaltar texto hello seleccionado en la lista Hola de cuentas. Esto es realmente útil en caso de hello al nombre completo de Hola o el identificador no está fácilmente disponible.

Puede usar texto sin formato aquí toohelp encontrar cuenta Hola que le interesen.

![](media/azure-stack-manage-storage-accounts/image6.png)

## <a name="look-at-account-details"></a>Examen de los detalles de la cuenta
Una vez que haya encontrado cuentas Hola que está interesado en Ver, puede hacer clic en hello cuenta determinada tooview algunos detalles. Una nueva hoja se abre con detalles de la cuenta de hello como: Hola tipo de cuenta de hello, la hora de creación, ubicación, etcetera.

![](media/azure-stack-manage-storage-accounts/image7.png)

## <a name="recover-a-deleted-account"></a>Recuperación de una cuenta eliminada
Es posible que en una situación donde debe toorecover una cuenta eliminada.

En la pila de Azure, hay un toodo de manera muy sencilla que:

1. Examinar la lista de cuentas de almacenamiento de toohello. Consulte [Búsqueda de una cuenta de almacenamiento](#find) en este tema para más información.
2. Busque esa cuenta determinada en la lista de Hola. Puede que necesite toofilter.
3. Comprobar hello *estado* de cuenta de hello. Debe indicar **Eliminada**.
4. Haga clic en la cuenta de hello que abre una hoja de detalles de cuenta de hello.
5. En esta hoja, busque Hola **recuperar** botón y haga clic en él.
6. Haga clic en **Sí** tooconfirm.
   
   ![](media/azure-stack-manage-storage-accounts/image8.png)
7. recuperación de Hello ahora está en *procesar... Espere* para un valor que indica que se realizó correctamente.
   También puede hacer clic en un icono de "campana" hello en parte superior de Hola Hola del portal de para ver las indicaciones de progreso.
   
   ![](media/azure-stack-manage-storage-accounts/image9.png)
   
   Una vez recuperado Hola cuenta se ha sincronizado correctamente, se puede usar de nuevo.

### <a name="some-gotchas"></a>Algunos gotchas
* La cuenta eliminada muestra un estado **fuera de retención**.
  
  Esto significa que cuenta Hola eliminado ha superado el período de retención de Hola y puede no ser recuperable.
* La cuenta eliminada no se muestra en la lista de cuentas de Hola.
  
  Esto podría significar que cuenta Hola eliminado ya ha sido recolectado. En este caso no se puede recuperar. Consulte [Reclamación de capacidad](#reclaim) en este tema.

## <a name="set-hello-retention-period"></a>Establecer el período de retención de Hola
configuración del período de retención Hola permite un toospecify de operador en la nube un período de tiempo en días (entre 0 y 9999 días) durante el que cualquier cuenta eliminada potencialmente puede recuperarse. Hello período de retención predeterminado se establece too15 días. Establecer valor de hello demasiado "0" significa que cualquier cuenta eliminada es inmediatamente fuera de retención y marcado para la recolección periódica.

**período de retención de Hola toochange:**

1. En un explorador de Internet, vaya a https://adminportal.local.azurestack.external.
2. Inicie sesión en toohello portal de administración de la pila de Azure como un operador en la nube (mediante las credenciales que proporcionó durante la implementación)
3. En el panel predeterminado de hello – encontró hello **administración región** lista y haga clic en la región de Hola que desee tooexplore: por ejemplo **(local**).
4. Seleccione **almacenamiento** de hello **proveedores de recursos** lista.
5. Haga clic en **configuración** en la hoja de configuración de hello tooopen superior Hola.
6. Haga clic en **configuración** a continuación, edite el valor de período de retención de Hola.

   Establezca Hola número de días y, a continuación, guárdelo.
   
   Este valor se hace efectivo inmediatamente y se aplica a toda la región.

   ![](media/azure-stack-manage-storage-accounts/image10.png)

## <a name="reclaim"></a>Reclamación de capacidad
Uno de los efectos secundarios de Hola de tener un período de retención es que una cuenta eliminada continúa tooconsume capacidad hasta que sale del período de retención de Hola. Como una nube puede que necesite un hello tooreclaim de manera Eliminar operador cuenta el espacio aunque el período de retención de hello no ha expirado todavía.

Puede recuperar la capacidad mediante el portal de Hola o PowerShell.

**capacidad de tooreclaim mediante Hola portal:**
1. Navegar por hoja de cuentas de almacenamiento de toohello. Consulte [Búsqueda de una cuenta de almacenamiento](#find).
2. Haga clic en **reclamar espacio** princip Hola de hoja de Hola.
3. Leer mensajes de bienvenida y, a continuación, haga clic en **Aceptar**.

    ![](media/azure-stack-manage-storage-accounts/image11.png)
4. Espere icono de campana de éxito notificación vea hello en el portal de Hola.

    ![](media/azure-stack-manage-storage-accounts/image12.png)
5. Actualice la página de cuentas de almacenamiento de Hola. cuentas de Hello eliminado ya no se muestran en lista de hello porque se hayan purgado.

Puede usar período de retención de PowerShell tooexplicitly invalidación hello y recuperar inmediatamente la capacidad.

**tooreclaim capacidad de uso de PowerShell:**   

1. Confirme que ha instalado y configurado Azure PowerShell. Si no es así, usar hello siguiendo las instrucciones: 
   * tooinstall Hola versión más reciente de PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/).
   Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).
2. Ejecute hello siguiente cmdlet:

> [!NOTE]
> Si ejecuta este cmdlet se eliminan definitivamente cuenta hello y su contenido. No se podrá volver a recuperar. Así que úselo con precaución.


        Clear-ACSStorageAccount -ResourceGroupName system.local -FarmName <farm ID>


Para obtener más información, consulte demasiado[documentación de powershell de la pila de Azure.](https://msdn.microsoft.com/library/mt637964.aspx)
 

## <a name="migrate-a-container"></a>Migración de un contenedor
Pagar toouneven almacenamiento usen los inquilinos, un operador en la nube puede encuentra uno o más subyacente inquilino compartido mediante el uso de más espacio que otras personas. Si esto ocurre, operador de hello en la nube puede intentar toofree un poco de espacio en el recurso compartido de hello acentuado migrando manualmente algunos recursos compartidos tooanother de contenedores de blob. 

Debe usar PowerShell toomigrate contenedores.
> [!NOTE]
>La migración de contenedores de blobs no admite la migración en vivo y actualmente es una operación sin conexión. Durante la migración y hasta que se complete blobs subyacente de hello en ese contenedor no se puede usar y están "sin conexión". 

**contenedores de toomigrate con PowerShell:**

1. Confirme que ha instalado y configurado Azure PowerShell. Si no es así, usar hello siguiendo las instrucciones:
    * tooinstall Hola versión más reciente de PowerShell de Azure y asociarlo con su suscripción de Azure, consulte [cómo tooinstall y configurar Azure PowerShell](http://azure.microsoft.com/documentation/articles/powershell-install-configure/). Para más información sobre los cmdlets de Azure Resource Manager, consulte [Uso de Azure PowerShell con Azure Resource Manager](http://go.microsoft.com/fwlink/?LinkId=394767).
2. Obtener nombre de granja de servidores de hello: 
      
      `$farm = Get-ACSFarm -ResourceGroupName system.local`
3. Obtener recursos compartidos de hello: 

   `$shares = Get-ACSShare -ResourceGroupName system.local -FarmName $farm.FarmName`

4. Obtener contenedores de Hola para un recurso compartido especificado. Observe que los parámetros count e intent son opcionales:
            
   `$containers = Get-ACSContainer -ResourceGroupName system.local -FarmName $farm.FarmName -ShareName $shares[0].ShareName -Count 4 -Intent Migration`  

   A continuación, examine $containers:

   `$containers`

    ![](media/azure-stack-manage-storage-accounts/image13.png)
5. Obtener Hola mejor destino recursos compartidos para la migración de contenedor de hello:

    `$destinationshares= Get-ACSSharesForMigration  -ResourceGroupName system.local -FarmName $farm.farmname -SourceShareName $shares[0].ShareName`

    A continuación, examine $destinationshares:

    `$destinationshares`

    ![](media/azure-stack-manage-storage-accounts/image14.png)
6. Comenzar la migración de un contenedor, tenga en cuenta que esto es una implementación asincrónica, por lo que uno puede todos los contenedores en un estado de Hola de recurso compartido y realizar un seguimiento con el Id. de trabajo devuelto Hola.

    `$jobId = Start-ACSContainerMigration -ResourceGroupName system.local -FarmName $farm.farmname -ContainerToMigrate $containers[1] -DestinationShareUncPath $destinationshares.UncPath`

    A continuación, examine $jobId:

   ```
   $jobId
   d1d5277f-6b8d-4923-9db3-8bb00fa61b65
   ```
7. Compruebe el estado del trabajo de migración de Hola por su identificador de trabajo. Cuando finalice la migración de contenedor de hello, MigrationStatus se establece demasiado "completado".

    `Get-ACSContainerMigrationStatus -ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image15.png)

8. Puede cancelar un trabajo de migración en curso. De nuevo, es una operación asincrónica, cuyo seguimiento se puede realizar mediante $jobid:

    `Stop-ACSContainerMigration-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId-Verbose`

    ![](media/azure-stack-manage-storage-accounts/image16.png)

    Puede comprobar estado de Hola de cancelación de la migración de Hola de nuevo:

    `Get-ACSContainerMigrationStatus-ResourceGroupName system.local -FarmName $farm.farmname -JobId $jobId`

    ![](media/azure-stack-manage-storage-accounts/image17.png)




  
  