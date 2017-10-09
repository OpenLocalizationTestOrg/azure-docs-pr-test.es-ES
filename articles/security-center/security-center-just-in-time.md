---
title: "obtener acceso aaaJust en la máquina virtual de tiempo en el centro de seguridad de Azure | Documentos de Microsoft"
description: "Este documento le guía a través de cómo justo a tiempo acceso VM en la Ayuda de Azure Security Center puede controlar acceso a tooyour Azure máquinas virtuales."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>Administrar el acceso a máquina virtual mediante Just-In-Time

Solo en la máquina virtual (VM) de tiempo acceso puede ser usado toolock hacia abajo el tráfico entrante tooyour máquinas virtuales de Azure, reduce la exposición tooattacks al proporcionar un acceso sencillo tooconnect tooVMs cuando sea necesario.

> [!NOTE]
> Hola justo a la característica de tiempo está en la vista previa y disponible en hello nivel estándar del centro de seguridad.  Vea [precios](security-center-pricing.md) toolearn más información acerca del centro de seguridad de los niveles de precios.
>
>

## <a name="attack-scenario"></a>Escenario de ataque

Fuerza bruta ataques normalmente los puertos de administración de destino como un tooa de acceso de medios toogain máquina virtual. Si se realiza correctamente, un atacante puede tomar el control sobre Hola VM y establecer un punto de apoyo en su entorno.

Ataque por fuerza bruta de una manera tooreduce exposición tooa es toolimit Hola cantidad de tiempo que un puerto está abierto. Los puertos de administración es no necesidad toobe abrir en todo momento. Solo necesitan toobe abiertos mientras el equipo está conectado toohello VM, por ejemplo tooperform tareas de administración o mantenimiento. Cuando se habilita justo a tiempo, el centro de seguridad usa [grupo de seguridad de red](../virtual-network/virtual-networks-nsg.md) reglas (NSG), que restringen acceso toomanagement puertos, por lo que no se destinen a los atacantes.

![Escenario Just-In-Time][1]

## <a name="how-does-just-in-time-access-work"></a>¿Cómo funciona el acceso Just-In-Time?

Cuando se habilita justo a tiempo, el centro de seguridad para bloquear el tráfico entrante tooyour máquinas virtuales de Azure mediante la creación de una regla de NSG. Seleccionar puertos hello en hello VM toowhich se bloqueará el tráfico entrante hacia abajo. Estos puertos se controlan mediante Hola justo a tiempo la solución.

Cuando un usuario solicita acceso tooa VM, el centro de seguridad comprueba que el usuario hello tiene [Control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md) permisos que conceden acceso de escritura para hello recursos de Azure. Si tienen permisos de escritura, se aprueba la solicitud de Hola y el centro de seguridad configura automáticamente los grupos de seguridad de red (NSG) de hello tooallow tráfico toohello administración puertos de entrada para la cantidad de Hola de tiempo especificado. Una vez transcurrido el tiempo de hello, centro de seguridad restaura el estado anterior de hello NSG tootheir.

> [!NOTE]
> En la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager. toolearn más sobre Hola clásico y modelos de implementación del Administrador de recursos, consulte [Azure Resource Manager frente a la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).
>
>

## <a name="using-just-in-time-access"></a>Uso del acceso Just-In-Time

Hola **en el acceso en tiempo de máquina virtual** icono hello **centro de seguridad** hoja muestra el número de Hola de máquinas virtuales configuradas para justo a tiempo acceso y Hola el número de solicitudes de acceso autorizado a realizadas en hello última semana.

Seleccione hello **en el acceso en tiempo de máquina virtual** hello y mosaico **en el acceso en tiempo de máquina virtual** abre la hoja.

![Icono Acceso a VM Just-In-Time][2]

Hola **en el acceso en tiempo de máquina virtual** hoja proporciona información sobre el estado de Hola de las máquinas virtuales:

- **Configurar** -máquinas virtuales que se han configurado toosupport solo en el acceso en tiempo de máquina virtual. datos de Hello presentados es para hello última semana e incluyen para cada número de Hola VM de las solicitudes aprobadas, la fecha del último acceso y la hora y último usuario.
- **Recomendado**: máquinas virtuales que pueden admitir el acceso a máquina virtual Just-In-Time pero que no se han configurado para ello. Se recomienda habilitar el control de acceso a máquina virtual Just-In-Time para estas máquinas virtuales. Vea cómo [habilitar el acceso a máquina virtual Just-In-Time](#enable-just-in-time-vm-access).
- **Sin recomendación** -razones que pueden provocar una máquina virtual no se recomienda toobe son:
  - Falta el NSG - Hola justo a tiempo la solución requiere un toobe NSG en su lugar.
  - Máquina virtual clásica: en la actualidad, el acceso a máquina virtual Just-In-Time de Security Center solo admite las máquinas virtuales que se han implementado mediante Azure Resource Manager. No se admite una implementación clásica Hola justo a tiempo la solución.
  - Otros: una máquina virtual está en esta categoría si Hola justo a tiempo solución está desactivada en la directiva de seguridad de Hola de suscripción de Hola o grupo de recursos de hello, o que hello VM no tiene una IP pública y no tiene un NSG en su lugar.

## <a name="configuring-a-just-in-time-access-policy"></a>Configurar una directiva de acceso Just-In-Time

Hola tooselect máquinas virtuales que desea tooenable:

1. En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **recomendado** ficha.

  ![Habilitar el acceso Just-In-Time][3]

2. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable. Esto coloca una máquina virtual de tooa siguiente marca de verificación.
3. Seleccione **Habilitar JIT en VM**.
4. Seleccione **Guardar**.

### <a name="default-ports"></a>Puertos predeterminados

Puede ver los puertos predeterminados de Hola que el centro de seguridad se recomienda habilitar justo a tiempo.

1. En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **recomendado** ficha.

  ![Mostrar los puertos predeterminados][6]

2. En **Máquinas virtuales**, seleccione una máquina virtual. Esto coloca una marca de verificación siguiente toohello VM y abre hello **configuración de acceso de VM de JIT** hoja. Esta hoja muestra los puertos predeterminados que Hola.

### <a name="add-ports"></a>Agregar puertos

De hello **configuración de acceso de VM de JIT** hoja, también puede agregar y configurar un puerto nuevo en el que desea tooenable Hola justo a tiempo la solución.

1. En hello **configuración de acceso de VM de JIT** hoja, seleccione **agregar**. Se abrirá hello **Agregar configuración de puerto** hoja.

  ![Configuración de puerto][7]

2. En **Agregar configuración de puerto** hoja, se identifica el puerto de hello, tipo de protocolo, tiempo de solicitud de direcciones IP de origen y el máximo permitido.

  Permiten direcciones IP de origen son Hola IP intervalos permitidos tooget acceso en una solicitud aprobada.

  Tiempo máximo de la solicitud es el período de tiempo máximo de Hola que se puede abrir un puerto específico.

3. Seleccione **Aceptar**.

## <a name="requesting-access-tooa-vm"></a>Solicitar acceso tooa VM

toorequest acceso tooa VM:

1. En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **configurado** ficha.
2. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable access. Esto coloca una máquina virtual de tooa siguiente marca de verificación.
3. Seleccione **Solicitar acceso**. Se abrirá hello **solicitar acceso** hoja.

  ![Tooa de acceso de solicitud de máquina virtual][4]

4. En hello **solicitar acceso** hoja, configurar para cada tooopen de puertos VM Hola junto con la dirección IP de origen de Hola Hola puerto está abierto tooand Hola período para qué hello puerto esté abierto. Puede solicitar puertos toohello solo de acceso que están configurados en hello solo en la directiva de tiempo. Cada puerto tiene un tiempo máximo permitido derivan Hola solo en la directiva de tiempo.
5. Seleccione **Open ports** (Abrir puertos).

## <a name="editing-a-just-in-time-access-policy"></a>Editar una directiva de acceso Just-In-Time

Puede cambiar la máquina virtual existente solo en la directiva de tiempo agregando y configurando un nuevo tooopen de puerto para esa máquina virtual, o al cambiar cualquier otro parámetro tooan relacionado ya protegida puerto.

En Ordenar tooedit existente solo en la directiva de tiempo de una máquina virtual, hello **configurado** ficha se utiliza:

1. En **máquinas virtuales**, seleccione una máquina virtual tooadd un tooby de puerto al hacer clic en puntos de hello tres dentro de la fila de Hola para esa máquina virtual. Se abrirá un menú.
2. Seleccione **editar** en el menú de Hola. Se abrirá hello **configuración de acceso de VM de JIT** hoja.

  ![Editar directiva][8]

3. En hello **configuración de acceso de VM de JIT** hoja, puede modificar la configuración existente de Hola de un puerto ya protegido haciendo clic en su puerto, o puede seleccionar **agregar**. Se abrirá hello **Agregar configuración de puerto** hoja.

  ![Agregar un puerto][7]

4. En **Agregar configuración de puerto** hoja identificar el puerto de hello, tipo de protocolo, direcciones IP de origen permitido y tiempo máximo de la solicitud.
5. Seleccione **Aceptar**.
6. Seleccione **Guardar**.

## <a name="auditing-just-in-time-access-activity"></a>Auditar la actividad del acceso Just-In-Time

Puede usar la búsqueda de registros para obtener información sobre las actividades de las máquinas virtuales. registros de tooview:

1. En hello **en el acceso en tiempo de máquina virtual** hoja, seleccione hello **configurado** ficha.
2. En **máquinas virtuales**, seleccione una información de tooview VM sobre haciendo clic en puntos de hello tres dentro de la fila de Hola para esa máquina virtual. Se abrirá un menú.
3. Seleccione **registro de actividad** en el menú de Hola. Se abrirá hello **registro de actividad** hoja.

![Seleccionar el registro de actividades][9]

Hola **registro de actividad** hoja proporciona una vista filtrada de las operaciones anteriores para esa máquina virtual junto con el tiempo, la fecha y la suscripción.

![Ver el registro de actividades][5]

Puede descargar información del registro de hello seleccionando **haga clic aquí toodownload todos los elementos de hello como CSV**.

Modificar filtros de Hola y seleccione **aplicar** toocreate una búsqueda y un registro.

## <a name="using-just-in-time-vm-access-via-powershell"></a>Usar el acceso a máquina virtual Just-In-Time mediante PowerShell

Hola toouse de orden justo a tiempo la solución a través de PowerShell, asegúrese de que tiene hello [más reciente](/powershell/azure/install-azurerm-ps) versión de PowerShell de Azure.
Una vez que lo hace, deberá hello tooinstall [más reciente](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12) centro de seguridad de Azure desde la Galería de PowerShell de Hola.

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>Configurar una directiva Just-In-Time para una máquina virtual

tooconfigure un solo en la directiva de tiempo en una VM específica, necesite toorun este comando en la sesión de PowerShell: Set-ASCJITAccessPolicy.
Siga Hola cmdlet documentación toolearn más.

### <a name="requesting-access-tooa-vm"></a>Solicitar acceso tooa VM

Hola tooaccess una VM específica que está protegido con justo a tiempo la solución, deberá toorun este comando en la sesión de PowerShell: ASCJITAccess invocar.
Siga Hola cmdlet documentación toolearn más.

## <a name="next-steps"></a>Pasos siguientes
En este artículo, ha aprendido cómo justo a tiempo acceso de VM en el centro de seguridad le ayuda a controlar el acceso tooyour Azure máquinas virtuales.

toolearn más información acerca del centro de seguridad, vea Hola recursos siguientes:

- [Configuración de directivas de seguridad](security-center-policies.md) : más información cómo tooconfigure las directivas de seguridad para los grupos de recursos y las suscripciones de Azure.
- [Administración de recomendaciones de seguridad](security-center-recommendations.md): conozca una serie de recomendaciones que le ayudarán a proteger los recursos de Azure.
- [Supervisión de estado de seguridad](security-center-monitoring.md) : Obtenga información acerca de cómo toomonitor Hola estado de los recursos de Azure.
- [Administrar y responder a alertas de toosecurity](security-center-managing-and-responding-alerts.md) : más información cómo toomanage y que responden las alertas de toosecurity.
- [Supervisión de soluciones de socios comerciales](security-center-partner-solutions.md) : Obtenga información acerca de cómo toomonitor Hola estado de mantenimiento de las soluciones de socios comerciales.
- [Preguntas más frecuentes del centro de seguridad](security-center-faq.md) : preguntas más frecuentes sobre el uso de servicio de Hola de búsqueda.
- [Blog de seguridad de Azure](https://blogs.msdn.microsoft.com/azuresecurity/) : encuentre entradas de blog sobre el cumplimiento y la seguridad de Azure.


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
