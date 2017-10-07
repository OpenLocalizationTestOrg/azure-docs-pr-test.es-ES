---
title: "prácticas recomendadas de seguridad de máquina virtual de aaaAzure | Documentos de Microsoft"
description: "Este artículo proporciona una variedad de seguridad mejores prácticas toobe utilizado en máquinas virtuales ubicadas en Azure."
services: security
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 5e757abe-16f6-41d5-b1be-e647100036d8
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: yurid
ms.openlocfilehash: b03bcc75fde6d49897f9a7f6f15aec87456edd0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-vm-security"></a>Procedimientos recomendados de seguridad para las máquinas virtuales de Azure

En la mayoría de infraestructura como en los escenarios de servicio (IaaS), [máquinas virtuales (VM) Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/) es informática de carga de trabajo principal de Hola para las organizaciones que usan en la nube. Este hecho es especialmente evidente en [escenarios híbridos](https://social.technet.microsoft.com/wiki/contents/articles/18120.hybrid-cloud-infrastructure-design-considerations.aspx) donde tooslowly de las organizaciones desean migrar nube toohello de cargas de trabajo. En estos escenarios, siga hello [consideraciones generales de seguridad de la IaaS](https://social.technet.microsoft.com/wiki/contents/articles/3808.security-considerations-for-infrastructure-as-a-service-iaas.aspx)y aplicar tooall de prácticas recomendada de seguridad de las máquinas virtuales.

En este artículo se describen varios procedimientos recomendados de seguridad para las máquinas virtuales, todos derivados de nuestras experiencias directas y las de nuestros clientes con las máquinas virtuales.

prácticas recomendadas de Hola se basan en un consenso de opinión y funcionan con las funcionalidades actuales de la plataforma Azure y conjuntos de características. Dado que las opiniones y las tecnologías pueden cambiar con el tiempo, tenemos previsto tooupdate en este artículo se con regularidad tooreflect esos cambios.

Para cada procedimiento recomendado, artículo Hola explica:

* Es el procedimiento recomendado de Hola.
* Por eso es una buena idea tooenable lo.
* ¿Cómo puede obtener tooenable lo.
* ¿Qué puede ocurrir si se produce un error tooenable.
* Procedimiento recomendado de toohello de las alternativas posibles.

artículo de Hello examina Hola siguiendo los procedimientos recomendados de seguridad de máquina virtual:

* Autenticación de la máquina virtual y control de acceso
* Acceso de red y disponibilidad de máquinas virtuales
* Protección de los datos en reposo almacenados en máquinas virtuales mediante su cifrado
* Administrar las actualizaciones de la máquina virtual
* Administrar la posición de seguridad de la máquina virtual
* Supervisar el rendimiento de la máquina virtual

## <a name="vm-authentication-and-access-control"></a>Autenticación de la máquina virtual y control de acceso

Hola primer paso para proteger la máquina virtual es tooensure que sólo los usuarios autorizados están tooset capaz de nuevas máquinas virtuales. Puede usar [directivas de Azure Resource Manager](../azure-resource-manager/resource-manager-policy.md) tooestablish convenciones para los recursos de su organización, crear directivas personalizadas y aplicar estos tooresources directivas, como [grupos de recursos](../azure-resource-manager/resource-group-overview.md).

Las máquinas virtuales que pertenecen de forma natural grupo de recursos de tooa heredan sus directivas. Aunque se recomiendan este enfoque toomanaging las máquinas virtuales, puede también directivas de control de acceso tooindividual VM mediante [control de acceso basado en roles (RBAC)](../active-directory/role-based-access-control-configure.md).

Cuando se habilita el acceso VM de toocontrol RBAC y directivas de administrador de recursos, para ayudar a mejorar la seguridad general de máquina virtual. Se recomienda que consolidar las máquinas virtuales con hello ciclo de vida del mismo en hello mismo grupo de recursos. Mediante los grupos de recursos, puede implementar, supervisar y acumular los costos para sus recursos. tooenable usuarios tooaccess y configurar las máquinas virtuales, use un [enfoque de privilegios mínimos](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models). Y al asignar privilegios toousers, planear hello toouse siguiendo las funciones integradas de Azure:

- [Máquina virtual colaborador](../active-directory/role-based-access-built-in-roles.md#virtual-machine-contributor): puede administrar máquinas virtuales, pero no Hola virtual toowhich de cuenta de red o almacenamiento que están conectados.
- [Colaborador de máquina Virtual clásica](../active-directory/role-based-access-built-in-roles.md#classic-virtual-machine-contributor): puede administrar máquinas virtuales creadas con el modelo de implementación clásica de hello, pero no Hola virtual red o almacenamiento cuenta toowhich Hola conectadas las máquinas virtuales.
- [Administrador de seguridad](../active-directory/role-based-access-built-in-roles.md#security-manager): puede administrar los componentes y las directivas de seguridad, además de las máquinas virtuales.
- [Usuario de DevTest Labs](../active-directory/role-based-access-built-in-roles.md#devtest-labs-user): puede ver todo el contenido, así como conectar, iniciar, reiniciar y apagar las máquinas virtuales.

No comparta cuentas ni contraseñas entre los administradores ni reutilice contraseñas en diferentes cuentas de usuario o servicios, especialmente las de las redes sociales u otras actividades no administrativas. Idealmente, debe utilizar [Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooset de plantillas de las máquinas virtuales con seguridad. Con este enfoque, puede reforzar las opciones de implementación y aplicar la configuración de seguridad a lo largo de la implementación de Hola.

Es posible que las organizaciones que no apliquen el control de acceso a los datos mediante funcionalidades como RBAC estén concediendo más privilegios de los necesarios a sus usuarios. Datos de usuario inadecuado acceso toocertain directamente pueden poner en peligro esos datos.

## <a name="vm-availability-and-network-access"></a>Acceso de red y disponibilidad de máquinas virtuales

Si la máquina virtual ejecuta aplicaciones críticas que necesitan toohave alta disponibilidad, recomendamos encarecidamente que use varias máquinas virtuales. Para una mejor disponibilidad, debe crear al menos dos máquinas virtuales en hello [conjunto de disponibilidad](../virtual-machines/windows/tutorial-availability-sets.md).

[El equilibrador de carga Azure](../load-balancer/load-balancer-overview.md) también requiere que las VM de equilibrio de carga pertenezcan toohello mismo conjunto de disponibilidad. Si deben tener acceso a estas máquinas virtuales de hello Internet, debe configurar un [equilibrador de carga a través de Internet](../load-balancer/load-balancer-internet-overview.md).

Cuando las máquinas virtuales están expuesto toohello Internet, es importante que [controlar el flujo de tráfico de red con grupos de seguridad de red (NSG)](../virtual-network/virtual-networks-nsg.md). Dado que los NSG pueden ser toosubnets aplicado, se puede minimizar el número de Hola de NSG agrupar los recursos de subred y, a continuación, aplicando los NSG toohello subredes. intención de Hello es un nivel de aislamiento de red, lo que puede hacer configurando correctamente hello toocreate [seguridad de red](../best-practices-network-security.md) capacidades en Azure.

También puede usar la característica de hello just-in-time (JIT) de acceso de VM de Azure Security Center toocontrol quién tiene acceso remoto tooa VM específica y durante cuánto tiempo.

Las organizaciones que no aplican restricciones de acceso de red tooInternet orientada a las máquinas virtuales es exponen a riesgos de toosecurity, por ejemplo, un ataque por fuerza bruta de protocolo de escritorio remoto (RDP).

## <a name="protect-data-at-rest-in-your-vms-by-enforcing-encryption"></a>Protección de los datos en reposo almacenados en máquinas virtuales mediante su cifrado

El [cifrado de los datos en reposo](https://blogs.microsoft.com/cybertrust/2015/09/10/cloud-security-controls-series-encrypting-data-at-rest/) es un paso obligatorio en lo que respecta a la privacidad de los datos, el cumplimiento y la soberanía de los datos. [Cifrado del disco Azure](../security/azure-security-disk-encryption.md) permite a los administradores de TI tooencrypt Windows y discos de máquina virtual de IaaS de Linux. Cifrado del disco combina características de BitLocker de Windows estándar del sector de Hola y cifrado del volumen de tooprovide de hello Linux dm crypt característica hello OS y discos de datos de Hola.

Puede aplicar el cifrado de disco toohelp proteger su datos toomeet sus requisitos de seguridad y cumplimiento organizativos. Su organización debe considerar el uso de cifrado toohelp mitigar los riesgos relacionados toounauthorized acceso a los datos. También se recomienda cifrar las unidades de disco antes de escribir los datos confidenciales toothem.

Ser seguro tooencrypt su tooprotect de volúmenes de datos de máquina virtual estos en rest en su cuenta de almacenamiento de Azure. Proteger las claves de cifrado de Hola y el secreto mediante [el almacén de claves de Azure](https://azure.microsoft.com/en-us/documentation/articles/key-vault-whatis/).

Las organizaciones que no se exija el cifrado de datos son más problemas de integridad toodata expuesto. Por ejemplo, los usuarios no autorizados o no autorizados pueden robar datos contenidos en las cuentas en peligro u obtener codificada en ClearFormat de toodata de acceso no autorizado. Además de realizar en estos riesgos, toocomply con las normativas del sector, las empresas deben demostrar que está ejercitando diligencia y utilizando la seguridad correcto controla tooenhance su seguridad de los datos.

toolearn más información acerca del cifrado del disco, consulte [cifrado de disco de Azure para Windows y las máquinas virtuales de Linux IaaS](azure-security-disk-encryption.md).


## <a name="manage-your-vm-updates"></a>Administrar las actualizaciones de la máquina virtual

Dado que las máquinas virtuales de Azure, como ocurre con todas local las máquinas virtuales, está previsto toobe administrada por el usuario, Azure no inserción toothem de actualizaciones de Windows. Sin embargo, son recomienda habilitada por la configuración de Windows Update automática de tooleave Hola. Otra opción es toodeploy [Windows Server Update Services (WSUS)](https://technet.microsoft.com/windowsserver/bb332157.aspx) u otro producto de administración de actualizaciones adecuado en otra máquina virtual o de forma local. WSUS y Windows Update mantienen actualizadas las máquinas virtuales. También se recomienda que realice un análisis tooverify de producto que están toodate todas las máquinas virtuales de IaaS.

Imágenes estándar proporcionadas por Azure son tooinclude actualizado de forma rutinaria hello más reciente de ida y vuelta de actualizaciones de Windows. Sin embargo, no hay ninguna garantía de que las imágenes de hello es actuales durante la implementación. Es posible que haya un retraso pequeño (de no más de unas cuantas semanas) después de que las versiones sean públicas. Buscar e instalar las actualizaciones de Windows deben ser el primer paso de Hola de cada implementación. Esta medida es especialmente importante tooapply al implementar imágenes que proceden de usted o su propia biblioteca. Las imágenes que se proporcionan como parte de hello Azure Marketplace se actualizan automáticamente de forma predeterminada.

Las organizaciones que no aplican directivas de actualización de software son más toothreats expuesto que aprovecha las vulnerabilidades conocidas, previamente fijas. Además de arriesgar esas amenazas, toocomply con las normativas del sector, las empresas deben demostrar que está ejercitando diligencia y usar toohelp de controles de seguridad correctas garantizar la seguridad de Hola de su carga de trabajo que se encuentra en la nube de Hola.

Es importante tooemphasize que prácticas recomendadas para centros de datos tradicionales de actualización de software y IaaS de Azure tienen muchas similitudes. Por lo tanto, le recomendamos que evalúe su actual tooinclude de las directivas de actualización de software las máquinas virtuales.

## <a name="manage-your-vm-security-posture"></a>Administrar la posición de seguridad de la máquina virtual

Las amenazas evolucionan y proteger las máquinas virtuales requiere a una completa funcionalidad de supervisión que puede rápidamente detectar amenazas, evitar que los recursos de tooyour de acceso no autorizado, desencadenan alertas y reducir los falsos positivos. estado de seguridad de Hola para una carga de trabajo compone de todos los aspectos de seguridad de Hola de máquina virtual, de acceso de red de toosecure de administración de actualización.

postura de seguridad de hello toomonitor de su [Windows](../security-center/security-center-virtual-machine.md) y [máquinas virtuales de Linux](../security-center/security-center-linux-virtual-machine.md), use [Azure Security Center](../security-center/security-center-intro.md). En el centro de seguridad de Azure, proteger las máquinas virtuales aprovechando las ventajas de hello siguientes capacidades:

* Aplicar la configuración de seguridad del sistema operativo con las reglas de configuración recomendadas
* Identificar y descargar las actualizaciones críticas y de seguridad del sistema que puedan faltar
* Implementar recomendaciones de protección antimalware del punto de conexión
* Validar el cifrado del disco
* Evaluar y corregir las vulnerabilidades
* Detectar amenazas

Security Center puede supervisar activamente si hay posibles amenazas, que se mostrarán en **Alertas de seguridad**. Las amenazas correlacionadas se agregan en una única vista denominada **Incidente de seguridad**.

toounderstand cómo el centro de seguridad puede ayudar a identificar posibles amenazas en las máquinas virtuales que se encuentran en Azure, vea Hola después de vídeo:

<iframe src="https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Security-Center-in-Incident-Response/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

Las organizaciones que no exigen una postura de seguridad seguro para sus máquinas virtuales siguen sin tener en cuenta posibles intentos por parte de controles de seguridad de los usuarios no autorizados toocircumvent establecido.

## <a name="monitor-vm-performance"></a>Supervisar el rendimiento de la máquina virtual

El abuso de los recursos puede ser un problema cuando los procesos de las máquinas virtuales consumen más recursos de los que deberían. Problemas de rendimiento con una máquina virtual pueden provocar una interrupción tooservice, lo que infringe el principio de seguridad de Hola de disponibilidad. Por esta razón, es imperativo toomonitor acceso de VM no solo reactivamente, mientras se está produciendo un problema, pero también de forma preventiva, con respecto al rendimiento de línea de base, medido durante el funcionamiento normal.

Al analizar los [archivos de registro de diagnóstico de Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/), puede supervisar los recursos de la máquina virtual e identificar posibles problemas que podrían poner en peligro la disponibilidad y rendimiento. Hola extensión de diagnósticos de Azure proporciona capacidades de supervisión y diagnóstico en las máquinas virtuales basadas en Windows. Para habilitar estas capacidades, incluida la extensión de hello como parte del programa Hola a [plantilla de Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).

También puede usar [Monitor Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md) toogain visibilidad en estado del recurso.

Las organizaciones que no supervisar el rendimiento de la máquina virtual son no se puede toodetermine si no hay algunos cambios en los patrones de rendimiento normal o anómala. Si Hola VM consume más recursos que normal, una anomalía de este tipo podría indicar un ataque potencial de un recurso externo o un proceso en peligro ejecutado en hello VM.
