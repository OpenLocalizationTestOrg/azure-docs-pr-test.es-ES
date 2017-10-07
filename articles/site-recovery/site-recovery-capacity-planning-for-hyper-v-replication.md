---
title: "herramienta de planificador de capacidad aaaRun Hola Hyper-V para la recuperación del sitio | Documentos de Microsoft"
description: "Este artículo describe cómo toorun Hola herramienta de planificación de capacidad de Hyper-V para Azure Site Recovery"
services: site-recovery
documentationcenter: na
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 2bc3832f-4d6e-458d-bf0c-f00567200ca0
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: b853598e5cd290c48b59794ba48eefc72ac8ded6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-hyper-v-capacity-planner-tool-for-site-recovery"></a>Ejecutar la herramienta de planificación de capacidad de Hyper-V de hello para la recuperación de sitio

Como parte de la implementación de Azure Site Recovery, deberá toofigure la replicación y los requisitos de ancho de banda. Planificador de capacidad de Hello Hyper-V para la recuperación del sitio ayuda a toodo, para la replicación de máquina virtual de Hyper-V.

Este artículo describe cómo toorun Hola herramienta de planificación de capacidad de Hyper-V. Esta herramienta debe utilizarse junto con la información de hello en [planear la capacidad de recuperación del sitio](site-recovery-capacity-planner.md).

## <a name="before-you-start"></a>Antes de comenzar
Se ejecuta la herramienta de hello en un nodo de servidor o clúster de Hyper-V en el sitio primario. servidores de host de Hyper-V de toorun Hola herramienta Hola necesita:

* Sistema operativo: Windows Server 2012 o 2012 R2
* Memoria: 20 MB (mínimo)
* CPU: sobrecarga del 5 por ciento (mínimo)
* Espacio en disco: 5 MB (mínimo)

Antes de ejecutar la herramienta de hello, deberá sitio primario de tooprepare Hola. Si replica entre dos sitios locales y desea que el ancho de banda de toocheck, necesita tooprepare también un servidor de réplica.

## <a name="step-1-prepare-hello-primary-site"></a>Paso 1: Preparar el sitio primario de Hola

1. En el sitio principal de hello, realice una lista de todos Hola máquinas virtuales de Hyper-V que desee tooreplicate y Hola clústeres Hyper-V hosts/en el que se encuentren. herramienta de Hello puede ejecutar para varios hosts independientes, o para un único clúster, pero no ambos juntos. También necesita toorun por separado para cada sistema operativo, por lo que debe reunir información sobre los servidores de Hyper-V como se indica a continuación:

   * Servidores independientes de Windows Server 2012
   * Clústeres de Windows Server 2012
   * Servidores independientes de Windows Server 2012 R2
   * Clústeres de Windows Server 2012 R2
2. Habilitar acceso remoto tooWMI en todos los hosts de Hyper-V de Hola y clústeres. Ejecute este comando en cada clúster de servidores, se establecen las reglas de firewall seguro toomake y permisos de usuario:

        netsh firewall set service RemoteAdmin enable
3. Habilite la supervisión del rendimiento en servidores y clústeres, de la siguiente forma:

   * Hola abrir Firewall de Windows con hello **seguridad avanzada** complemento, y, a continuación, siguiente de hello habilitar reglas de entrada: **acceso de red COM + (DCOM-IN)** y todas las reglas en hello **remota de registro de eventos Grupo de administración**.

## <a name="step-2-prepare-a-replica-server-on-premises-tooon-premises-replication"></a>Paso 2: Preparar un servidor de réplica (replicación de local tooon local)
Esto no es necesario toodo si replica tooAzure.

Se recomienda configurar un único host de Hyper-V como un servidor de recuperación, para que una máquina virtual ficticia pueda ancho de banda de toocheck tooit replicada.  Omita este paso, pero no será capaz de toomeasure ancho de banda a menos que lo haga.

1. Si desea que toouse un nodo de clúster como réplica Hola configurar agente de réplicas de Hyper-V de:

   * En **Administrador del servidor**, abra **Administrador de clúster de conmutación por error**.
   * Conecta el clúster de toohello, resalte el nombre del clúster de Hola y haga clic en **acciones** > **configurar rol** Asistente para alta disponibilidad de hello tooopen.
   * En **Seleccionar rol**, haga clic en **Agente de réplicas de Hyper-V**. En el Asistente de hello escribe un **nombre NetBIOS** hello y **dirección IP** toobe utilizado como clúster de toohello de punto de conexión de hello (llamado un punto de acceso de cliente). Hola **agente de réplica de Hyper-V** se configurarán, lo que da lugar a un nombre de punto de acceso de cliente que debe tener en cuenta.
   * Compruebe que ese rol de agente de réplica de Hyper-V Hola se conecte correctamente y puede conmutar por error entre todos los nodos del clúster de Hola. toodo esto, haga clic con el rol de hello, seleccione demasiado**mover**y, a continuación, haga clic en **Seleccionar nodo**. Seleccione un nodo > **Aceptar**.
   * Si utiliza la autenticación basada en certificados, asegúrese de que cada nodo del clúster y punto de acceso de cliente de hello todos tienen instalado el certificado de Hola.
2. Habilite un servidor de réplica:

   * Para un clúster, abra Administrador de clústeres de error, conéctese toohello clúster y haga clic en **Roles** > Seleccionar rol > **configuración de replicación** > **habilitar este clúster como una réplica servidor**. Si utiliza un clúster como réplica hello, deberá rol de agente de réplica de Hyper-V de hello toohave presente en el clúster de hello en el sitio principal de Hola.
   * Para un servidor independiente, abra el Administrador de Hyper-V. Hola **acciones** panel, haga clic en **configuración de Hyper-V** para el servidor de hello desea tooenable y en **configuración de replicación** haga clic en **habilitarlo equipo como un servidor de réplica**.
3. Configure la autenticación:

   * En **autenticación y puertos**, seleccione cómo tooauthenticate Hola servidor principal y los puertos de autenticación de Hola. Si usa un certificado, haga clic en **Seleccionar certificado** tooselect uno. Usar Kerberos si hay hosts de Hyper-V principal y de recuperación de Hola Hola mismo dominio o en dominios de confianza. Use certificados si los dominios son diferentes o si la implementación es para un grupo de trabajo.
   * En **autorización y almacenamiento**, permitir **cualquier** autentica el servidor de réplica de servidor (principal) toosend replicación datos toothis.

     ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image1.png)
   * Ejecutar **netsh http show servicestate**, toocheck se está ejecutando ese agente de escucha de Hola para hello Protocolo/puerto que especificó:  
4. Configure los firewalls. Durante la instalación de Hyper-V, las reglas de firewall se crean tooallow tráfico en puertos predeterminados que hello (HTTPS en 443, Kerberos en 80). Habilite estas reglas como se indica:
  - Autenticación de certificados en clústeres (443): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"}}``
  - Autenticación Kerberos en clústeres (80): ``Get-ClusterNode | ForEach-Object {Invoke-command -computername \$\_.name -scriptblock {Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"}}``
  - Autenticación de certificados en un servidor independiente: ``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTPS Listener (TCP-In)"``
  - Autenticación Kerberos en un servidor independiente:``Enable-Netfirewallrule -displayname "Hyper-V Replica HTTP Listener (TCP-In)"``

## <a name="step-3-run-hello-capacity-planner-tool"></a>Paso 3: Ejecutar la herramienta de planificación de capacidad de Hola
Una vez que ha preparado su sitio primario y configurar un servidor de recuperación, puede ejecutar la herramienta de Hola.

1. [Descargar](https://www.microsoft.com/download/details.aspx?id=39057) herramienta Hola Hola Microsoft Download Center.
2. Ejecutar la herramienta de Hola desde uno de los servidores principales de hello (o uno de los nodos de Hola de clúster principal hello). Haga clic en el archivo .exe de hello y, a continuación, elija **ejecutar como administrador**.
3. En **antes de comenzar**, especificar durante cuánto tiempo desea toocollect datos. Se recomienda que ejecutar la herramienta de Hola durante la producción tooensure de horas que los datos sean representativo. Si solo está tratando de conectividad de red toovalidate, se pueden recopilar para solo un minuto.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image2.png)
4. En **detalles del sitio primario**, especifique el nombre del servidor de Hola o FQDN para un host independiente, o para un clúster de especificarlo Hola FQDN de cliente hello acepte punto, el nombre del clúster o cualquier nodo de clúster de hello y, a continuación, haga clic en **siguiente**. herramienta Hola detecta automáticamente el nombre de hello del servidor de saludo en que se está ejecutando. Hola herramienta recoge las máquinas virtuales que se pueden supervisar Hola servidores especificados.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image3.png)
5. En **detalles del sitio de réplica**si está replicando tooAzure, o si está replicando tooa centro de datos secundario y no ha configurado un servidor de réplica, seleccione **omitir pruebas de sitio de réplica**. Si desea replicar tooa centro de datos secundario y haya configurado por un tipo de réplica, introduzca FQDN del servidor independiente de Hola o punto de acceso de cliente de Hola de clúster de hello, en **servidor nombre (o) CAP de agente de réplica de Hyper-V**.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image4.png)
6. En **detalles de réplica extendido**, habilitar **Hola Skip comprueba que implican sitio de réplica extendido**. Estas pruebas son compatibles con Site Recovery.
7. En **tooReplicate de máquinas virtuales elija**, herramientas de hello conecta toohello servidor o clúster y muestra las máquinas virtuales y discos que se ejecuten en el servidor principal de hello, según la configuración de hello ha especificado en hello **detalles del sitio principal**  página. Tenga en cuenta que no se mostrarán las máquinas virtuales que ya estén habilitadas para la replicación o que no se estén ejecutando. Seleccione las máquinas virtuales de hello para el que desea que las métricas de toocollect. Seleccionar Hola discos duros virtuales automáticamente recopila los datos para las máquinas virtuales de hello demasiado.
8. Si ha configurado un servidor de réplica o un clúster, en **información de la red**, especificar si ha configurado, se utilizará entre los sitios principal y réplica de Hola y Hola seleccione certificados Hola aproximado ancho de banda WAN piensa autenticación de certificado.

    ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image5.png)
9. En **resumen**, compruebe la configuración de Hola y haga clic en **siguiente** toobegin recopilar métricas. Progreso de la herramienta y el estado se muestra en hello **calcular la capacidad** página. Cuando la herramienta de hello finaliza su ejecución, haga clic en **Ver informe** salida de hello tooview. De forma predeterminada, los informes y los registros se almacenan en **%systemdrive%\Users\Public\Documents\Capacity Planner**.

   ![](./media/site-recovery-capacity-planning-for-hyper-v-replication/image6.png)

## <a name="step-4-interpret-hello-results"></a>Paso 4: Interpretar los resultados de Hola

Estas son las métricas importantes de Hola. Puede pasar por alto las que no aparezcan aquí, porque no son relevantes para Site Recovery.

### <a name="on-premises-tooon-premises-replication"></a>La replicación local tooon local

* Impacto de la replicación en el proceso del host principal de hello, memoria
* Impacto de la replicación en hello principal, espacio en disco de almacenamiento de hosts de recuperación IOPS
* Ancho de banda total necesario para la replicación delta (Mbps)
* Ancho de banda de red observado entre host principal de Hola y Hola recuperación (Mbps)
* Sugerencia para el número ideal de Hola de transferencias paralelo activas entre dos hosts y clústeres de Hola

### <a name="on-premises-tooazure-replication"></a>Replicación de tooAzure local

* Impacto de la replicación en el proceso del host principal de hello, memoria
* Impacto de la replicación en el espacio de disco de almacenamiento del host principal de Hola, IOPS
* Ancho de banda total necesario para la replicación delta (Mbps)

## <a name="more-resources"></a>Más recursos
* Para obtener información detallada acerca de la herramienta de hello, lea el documento de Hola que acompaña a la descarga de la herramienta de Hola.
* Ver un tutorial de herramienta de hello en Keith Mayer [blog de TechNet](http://blogs.technet.com/b/keithmayer/archive/2014/02/27/guided-hands-on-lab-capacity-planner-for-windows-server-2012-hyper-v-replica.aspx).
* [Obtener resultados de hello](site-recovery-performance-and-scaling-testing-on-premises-to-on-premises.md) nuestra pruebas de rendimiento para la replicación de Hyper-V de locales tooon local

## <a name="next-steps"></a>Pasos siguientes

Cuando haya terminado de planear la capacidad, puede comenzar a implementar Site Recovery:

* [Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM](site-recovery-vmm-to-azure.md)
* [Replicar máquinas virtuales de Hyper-V (sin WMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Replicación de máquinas virtuales de Hyper-V entre sitios VMM](site-recovery-vmm-to-vmm.md)
