---
title: "aaaCreate un agente de escucha de grupo de disponibilidad de SQL Server en máquinas virtuales de Azure | Documentos de Microsoft"
description: Instrucciones paso a paso para crear un agente de escucha en un grupo de disponibilidad AlwaysOn para SQL Server en Azure Virtual Machines
services: virtual-machines
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: monicar
ms.assetid: d1f291e9-9af2-41ba-9d29-9541e3adcfcf
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/01/2017
ms.author: mikeray
ms.openlocfilehash: c6a44dc5c7c18b572c2bf5772b4651b7210aacbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-load-balancer-for-an-always-on-availability-group-in-azure"></a>Configuración de un equilibrador de carga para un grupo de disponibilidad AlwaysOn en Azure
Este artículo explica cómo un equilibrador de carga para un grupo de disponibilidad AlwaysOn de SQL Server en Azure virtual toocreate máquinas que se ejecutan con el Administrador de recursos de Azure. Un grupo de disponibilidad requiere un equilibrador de carga cuando hay instancias de SQL Server de hello en máquinas virtuales de Azure. equilibrador de carga de Hello almacena la dirección IP de hello para el agente de escucha del grupo de disponibilidad de Hola. Si un grupo de disponibilidad abarca varias regiones, cada región necesitará su propio equilibrador de carga.

toocomplete esta tarea, deberá toohave un grupo de disponibilidad de SQL Server implementado en máquinas virtuales de Azure que se ejecutan con el Administrador de recursos. Las máquinas virtuales de SQL Server debe pertenecer toohello mismo conjunto de disponibilidad. Puede usar hello [plantilla Microsoft](virtual-machines-windows-portal-sql-alwayson-availability-groups.md) tooautomatically crear grupo de disponibilidad de hello en el Administrador de recursos. Esta plantilla crea automáticamente un equilibrador de carga interno. 

Si lo prefiere, puede [configurar manualmente un grupo de disponibilidad](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md).

En este artículo, es necesario que los grupos de disponibilidad ya estén configurados.  

Temas relacionados:

* [Configuración de Grupos de disponibilidad AlwaysOn en la máquina virtual de Azure (GUI)](virtual-machines-windows-portal-sql-alwayson-availability-groups-manual.md)   
* [Configuración de una conexión entre dos redes virtuales mediante Azure Resource Manager y PowerShell](../../../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)

A la vez a través de este artículo, cree y configure un equilibrador de carga en hello portal de Azure. Una vez completado el proceso de hello, configure hello toouse Hola dirección IP del equilibrador de carga de hello para el agente de escucha del grupo de disponibilidad de Hola.

## <a name="create-and-configure-hello-load-balancer-in-hello-azure-portal"></a>Cree y configure el equilibrador de carga de Hola Hola portal de Azure
En esta parte de la tarea hello, Hola siguientes:

1. Hola portal de Azure, crear equilibrador de carga de Hola y configurar la dirección IP de Hola.
2. Configurar grupo de back-end de Hola.
3. Crear el sondeo de Hola. 
4. Establecer reglas de equilibrio de carga de Hola.

> [!NOTE]
> Si son instancias de SQL Server de hello en varios grupos de recursos y regiones, realizar cada paso dos veces, una vez en cada grupo de recursos.
> 
> 

### <a name="step-1-create-hello-load-balancer-and-configure-hello-ip-address"></a>Paso 1: Crear el equilibrador de carga de Hola y configurar la dirección IP de Hola
En primer lugar, cree el equilibrador de carga de Hola. 

1. Hola portal de Azure, abra el grupo de recursos de Hola que contiene máquinas virtuales de SQL Server de Hola. 

2. En el grupo de recursos de hello, haga clic en **agregar**.

3. Busque **equilibrador de carga** y, a continuación, en resultados de búsqueda de hello, seleccione **equilibrador de carga**, que se publica mediante **Microsoft**.

4. En hello **equilibrador de carga** hoja, haga clic en **crear**.

5. Hola **equilibrador de carga de crear** diálogo cuadro, configure el equilibrador de carga de hello como sigue:

   | Configuración | Valor |
   | --- | --- |
   | **Name** |Un nombre de texto que representa el equilibrador de carga de Hola. Por ejemplo, **sqlLB**. |
   | **Tipo** |**Interno**: mayoría de implementaciones de usa un equilibrador de carga interno, que permite a las aplicaciones dentro de hello mismo grupo de disponibilidad de red virtual tooconnect toohello.  </br> **Externo**: permite el grupo de disponibilidad de aplicaciones tooconnect toohello a través de una conexión a Internet pública. |
   | **Red virtual** |Seleccione Hola red virtual que Hola aceptadas de SQL Server se encuentran en. |
   | **Subred** |Seleccione subred Hola que son instancias de SQL Server de hello en. |
   | **Asignación de dirección IP** |**Estática** |
   | **Dirección IP privada** |Especifique una dirección IP disponible de la subred de Hola. Use esta dirección IP cuando se crea un agente de escucha en el clúster de Hola. En un script de PowerShell, más adelante en este artículo, use esta dirección para hello `$ILBIP` variable. |
   | **Suscripción** |Si tiene varias suscripciones, puede aparecer este campo. Seleccione la suscripción de Hola que desea tooassociate con este recurso. Normalmente se Hola a misma suscripción como todos los recursos de Hola Hola grupo de disponibilidad. |
   | **Grupos de recursos** |Seleccione el grupo de recursos de Hola que son instancias de SQL Server de hello en. |
   | **Ubicación** |Seleccione hello ubicación de Azure que son instancias de SQL Server de hello en. |

6. Haga clic en **Crear**. 

Azure crea equilibrador de carga de Hola. equilibrador de carga de Hello pertenece tooa de red específicas, subred, grupo de recursos y ubicación. Una vez Azure complete la tarea de hello, compruebe la configuración de equilibrador de carga de hello en Azure. 

### <a name="step-2-configure-hello-back-end-pool"></a>Paso 2: Configurar grupo de back-end de Hola
Llamadas Azure Hola grupo de direcciones de back-end *grupo back-end*. En este caso, el grupo de back-end de hello es direcciones Hola Hola dos instancias de SQL Server en el grupo de disponibilidad. 

1. En el grupo de recursos, haga clic en el equilibrador de carga de Hola que ha creado. 

2. En **Configuración**, haga clic en **Grupos de back-end**.

3. En **grupos back-end**, haga clic en **agregar** toocreate un grupo de direcciones de back-end. 

4. En **Agregar grupo back-end**, en **nombre**, escriba un nombre para el grupo de back-end de Hola.

5. En **Máquinas virtuales**, haga clic en **+ Agregar una máquina virtual**. 

6. En **elegir máquinas virtuales**, haga clic en **elegir un conjunto de disponibilidad**y, a continuación, especifique el conjunto de disponibilidad de Hola que máquinas virtuales de SQL Server de hello pertenecen a.

7. Una vez que haya elegido el conjunto de disponibilidad de hello, haga clic en **elegir máquinas virtuales de hello**, seleccione Hola dos máquinas virtuales que hospedan instancias de SQL Server de hello en grupo de disponibilidad de hello y, a continuación, haga clic en **seleccione**. 

8. Haga clic en **Aceptar** tooclose hojas de Hola para **elegir máquinas virtuales**, y **Agregar grupo back-end**. 

Azure actualiza la configuración de hello para el grupo de direcciones de back-end de Hola. Ahora, el conjunto de disponibilidad tiene un grupo de dos instancias de SQL Server.

### <a name="step-3-create-a-probe"></a>Paso 3: Elaboración de un sondeo
sondeo de Hello define cómo Azure comprueba que Hola instancias de SQL Server posee actualmente el agente de escucha del grupo de disponibilidad de Hola. Servicio de hello en función de la dirección IP de hello en un puerto que define al crear el sondeo de hello las comprobaciones de Azure.

1. Equilibrador de carga en hello **configuración** hoja, haga clic en **sondeos de estado**. 

2. En hello **sondeos de estado** hoja, haga clic en **agregar**.

3. Configurar el sondeo de hello en hello **agregar sondeo** hoja. Hola de uso después de sondeo de hello tooconfigure de valores:

   | Configuración | Valor |
   | --- | --- |
   | **Name** |Un nombre de texto que representa el sondeo de Hola. Por ejemplo, **SQLAlwaysOnEndPointProbe**. |
   | **Protocolo** |**TCP** |
   | **Puerto** |Puede usar cualquier puerto que esté disponible. Por ejemplo, *59999*. |
   | **Intervalo** |*5* |
   | **Umbral incorrecto** |*2* |

4.  Haga clic en **Aceptar**. 

> [!NOTE]
> Asegúrese de que especifica el puerto de hello está abierto en firewall de Hola de las dos instancias de SQL Server. Ambas instancias requieren una regla de entrada para el puerto TCP que usa hello. Consulte [Agregar o editar regla de firewall](http://technet.microsoft.com/library/cc753558.aspx) para más información. 
> 
> 

Azure crea Hola sondeo y, a continuación, usa tootest qué instancia de SQL Server tiene el agente de escucha de hello para el grupo de disponibilidad de Hola.

### <a name="step-4-set-hello-load-balancing-rules"></a>Paso 4: Configurar reglas de equilibrio de carga de Hola
reglas de equilibrio de carga de Hello configurar cómo equilibrador de carga de hello enruta instancias de SQL Server toohello de tráfico. Para este equilibrador de carga, habilitar a direct server devuelto porque solo uno de dos instancias de SQL Server Hola pertenece recurso de agente de escucha de grupo de disponibilidad de Hola a la vez.

1. Equilibrador de carga en hello **configuración** hoja, haga clic en **reglas de equilibrio de carga**. 

2. En hello **reglas de equilibrio de carga** hoja, haga clic en **agregar**.

3. En hello **reglas de equilibrio de carga de agregar** hoja, configurar la regla de equilibrio de carga de Hola. Usar hello después de configuración: 

   | Configuración | Valor |
   | --- | --- |
   | **Name** |Un nombre de texto que representa las reglas de equilibrio de carga de Hola. Por ejemplo, **SQLAlwaysOnEndPointListener**. |
   | **Protocolo** |**TCP** |
   | **Puerto** |*1433* |
   | **Puerto back-end** |*1433*. Este valor se ignorará porque la regla usa **IP flotante (Direct Server Return)**. |
   | **Sondeo** |Usar el nombre de Hola de sondeo de Hola que creó para este equilibrador de carga. |
   | **Persistencia de la sesión** |**None** |
   | **Tiempo de espera de inactividad (minutos)** |*4* |
   | **IP flotante (Direct Server Return)** |**Enabled** |

   > [!NOTE]
   > Es posible que tenga tooscroll hacia abajo Hola hoja tooview todas las configuraciones de Hola.
   > 

4. Haga clic en **Aceptar**. 
5. Azure configura la regla de equilibrio de carga de Hola. Ahora equilibrador de carga de hello es tooroute configurado tráfico toohello SQL instancia del servidor que hospeda el agente de escucha de hello para el grupo de disponibilidad de Hola. 

En este momento, grupo de recursos de hello tiene un equilibrador de carga que se conecta tooboth máquinas de SQL Server. equilibrador de carga de Hello también contiene una dirección IP de hello SQL Server Always On disponibilidad escucha de grupo, por lo que cualquier máquina puede responder toorequests para grupos de disponibilidad de Hola.

> [!NOTE]
> Si las instancias de SQL Server se encuentran en dos regiones independientes, repita los pasos de Hola Hola otra región. Cada una de las regiones necesita su propio equilibrador de carga. 
> 
> 

## <a name="configure-hello-cluster-toouse-hello-load-balancer-ip-address"></a>Configurar la dirección IP del equilibrador de carga de hello clúster toouse Hola
paso siguiente Hello es agente de escucha de tooconfigure hello en clúster de Hola y ponga Hola el agente de escucha en línea. Hola siguientes: 

1. Crear Agente de escucha del grupo de disponibilidad de hello en clúster de conmutación por error de Hola. 

2. Ponga el agente de escucha de hello en línea.

### <a name="step-5-create-hello-availability-group-listener-on-hello-failover-cluster"></a>Paso 5: Crear el agente de escucha del grupo de disponibilidad de hello en clúster de conmutación por error de Hola
En este paso, se crea manualmente el agente de escucha del grupo de disponibilidad de hello en el Administrador de clústeres de conmutación por error y SQL Server Management Studio.

[!INCLUDE [ag-listener-configure](../../../../includes/virtual-machines-ag-listener-configure.md)]

### <a name="verify-hello-configuration-of-hello-listener"></a>Comprobar la configuración de Hola de agente de escucha de Hola

Si las dependencias y los recursos de clúster de hello estén configuradas correctamente, debe ser capaz de tooview agente de escucha hello en SQL Server Management Studio. tooset Hola puerto de escucha, Hola siguientes:

1. Inicie SQL Server Management Studio y, a continuación, conecte toohello de réplica principal.

2. Vaya demasiado**alta disponibilidad de AlwaysOn** > **grupos de disponibilidad** > **los agentes de escucha del grupo de disponibilidad**.  
    Ahora debería ver el nombre de agente de escucha de Hola que creó en el Administrador de clústeres de conmutación por error. 

3. Haga clic en nombre de agente de escucha de hello y, a continuación, haga clic en **propiedades**.

4. Hola **puerto** , especifique el número de puerto de hello para el agente de escucha del grupo de disponibilidad de hello mediante el uso de hello $EndpointPort que usó anteriormente (1433 pasaba Hola valor predeterminado) y, a continuación, haga clic en **Aceptar**.

Ahora tiene un grupo de disponibilidad en máquinas virtuales de Azure que se ejecutan con el modelo de Resource Manager. 

## <a name="test-hello-connection-toohello-listener"></a>El agente de escucha de prueba Hola conexión toohello
Probar la conexión de hello haciendo Hola siguiente:

1. Instancia de SQL Server tooa RDP que se encuentra en hello mismo virtual de red, pero no no réplica Hola propio. Este servidor puede ser Hola otra instancia SQL Server en clúster de Hola.

2. Use **sqlcmd** conexión de utilidad tootest Hola. Por ejemplo, Establece la siguiente secuencia de comandos de hello un **sqlcmd** réplica principal de conexión toohello a través de agente de escucha de hello con autenticación de Windows:
   
        sqlcmd -S <listenerName> -E

Hola conexión SQLCMD conecta automáticamente toohello instancia de SQL Server que hospeda la réplica principal de Hola. 

## <a name="create-an-ip-address-for-an-additional-availability-group"></a>Creación de una dirección IP para un grupo de disponibilidad adicional

Cada grupo de disponibilidad usa un agente de escucha independiente. Cada agente de escucha tiene su propia dirección IP. Use Hola misma dirección IP de hello toohold de equilibrador de carga para agentes de escucha adicionales. Después de crear un grupo de disponibilidad, agregar equilibrador de carga de toohello de dirección IP de hello y, a continuación, configure el agente de escucha de Hola.

tooadd un equilibrador de carga de tooa de dirección IP con hello portal de Azure, Hola siguientes:

1. En hello portal de Azure, abra el grupo de recursos de Hola que contiene el equilibrador de carga de hello y, a continuación, haga clic en el equilibrador de carga de Hola. 

2. En **Configuración**, haga clic en **Grupo de direcciones IP de front-end** y, después, en **Agregar**. 

3. En **agregar dirección IP de front-end**, asigne un nombre de front-end de Hola. 

4. Compruebe que hello **red Virtual** hello y **subred** se Hola igual Hola instancias de SQL Server.

5. Establecer la dirección IP de hello para el agente de escucha de Hola. 
   
   >[!TIP]
   >Puede establecer toostatic de dirección IP de Hola y escriba una dirección que no se utiliza actualmente en la subred de Hola. Como alternativa, puede establecer toodynamic de dirección IP de Hola y guardar el nuevo grupo de IP front-end Hola. Al hacerlo, Hola portal de Azure asigna automáticamente un grupo de toohello de direcciones IP disponible. A continuación, puede volver a abrir el grupo de direcciones IP de front-end de Hola y cambiar Hola asignación toostatic. 

6. Guarde la dirección IP de hello para el agente de escucha de Hola. 

7. Agregar un sondeo de estado mediante Hola después de configuración:

   |Configuración |Valor
   |:-----|:----
   |**Name** |Un sondeo de hello tooidentify de nombre.
   |**Protocolo** |TCP
   |**Puerto** |Un puerto TCP sin usar, que debe estar disponible en todas las máquinas virtuales. No se puede usar para ningún otro fin. No hay dos agentes de escucha pueden usar Hola mismo puerto de sondeo. 
   |**Intervalo** |Hola intervalo de tiempo entre el sondeo de los intentos. Usar valor predeterminado es hello (5).
   |**Umbral incorrecto** |número de Hola de umbrales consecutivos que deben fallar antes de una máquina virtual se considera incorrecto.

8. Haga clic en **Aceptar** sondeo de hello toosave. 

9. Cree una regla de equilibrio de carga. Haga clic en **Reglas de equilibrio de carga** y luego haga clic en **Agregar**.

10. Configurar Hola nuevo equilibrio de carga regla mediante el uso de hello después de configuración:

   |Configuración |Valor
   |:-----|:----
   |**Name** |Un saludo de tooidentify nombre cargar la regla de equilibrio. 
   |**Frontend IP address** (Dirección IP de front-end) |Seleccione la dirección IP de Hola que creó. 
   |**Protocolo** |TCP
   |**Puerto** |Usar el puerto de Hola que usan instancias de SQL Server de Hola. Una instancia predeterminada usa el puerto 1433, a menos que lo haya modificado. 
   |**Puerto back-end** |Hola uso mismo valor que **puerto**.
   |**Grupo de back-end** |grupo de Hola que contiene máquinas virtuales de hello con instancias de SQL Server de Hola. 
   |**Sondeo de estado** |Elija el sondeo de Hola que creó.
   |**Persistencia de la sesión** |None
   |**Tiempo de espera de inactividad (minutos)** |Valor predeterminado (4)
   |**IP flotante (Direct Server Return)** | habilitado

### <a name="configure-hello-availability-group-toouse-hello-new-ip-address"></a>Configurar Hola disponibilidad toouse Hola nueva dirección IP del grupo

toofinish configuración de clúster de hello, pasos de repetición Hola que seguir cuando realiza el primer grupo de disponibilidad Hola. Es decir, configure hello [Hola de toouse nueva dirección IP del clúster](#configure-the-cluster-to-use-the-load-balancer-ip-address). 

Después de haber agregado una dirección IP para el agente de escucha de hello, configurar grupo de disponibilidad adicional de hello haciendo Hola siguiente: 

1. Compruebe que el puerto de sondeo de Hola para nuevas direcciones IP Hola está abierto en ambas máquinas virtuales de SQL Server. 

2. [En el Administrador de clústeres, agregue el punto de acceso de cliente de hello](#addcap).

3. [Configurar recurso IP de hello para el grupo de disponibilidad de hello](#congroup).

   >[!IMPORTANT]
   >Cuando se crea la dirección IP de hello, use la dirección IP de Hola que agregó toohello equilibrador de carga.  

4. [Asegúrese de recurso de grupo de disponibilidad de SQL Server de hello depende del punto de acceso de cliente de hello](#dependencyGroup).

5. [Hacer que el acceso de cliente de hello elija recursos depende de la dirección IP de hello](#listname).
 
6. [Establecer parámetros de clúster de hello en PowerShell](#setparam).

Después de configurar Hola disponibilidad toouse Hola nueva dirección IP del grupo, configure el agente de escucha de hello conexión toohello. 

## <a name="next-steps"></a>Pasos siguientes

- [Configuración de un grupo de disponibilidad de SQL Server AlwaysOn en Azure Virtual Machines en regiones distintas](virtual-machines-windows-portal-sql-availability-group-dr.md)
