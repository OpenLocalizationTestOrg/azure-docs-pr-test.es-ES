---
title: "aaaPlanning para la migración de los recursos de IaaS de tooAzure clásico Resource Manager | Documentos de Microsoft"
description: "Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 78492a2c-2694-4023-a7b8-c97d3708dcb7
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 04/01/2017
ms.author: kasing
ms.openlocfilehash: 53c6f640425b69cae2ef10afb8c92b8ac4394267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="planning-for-migration-of-iaas-resources-from-classic-tooazure-resource-manager"></a>Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos
Mientras que el Administrador de recursos de Azure ofrece muchas características increíbles, resulta crítico tooplan espera su toomake del proceso de migración que todo se produzcan sin problemas. Dedicar tiempo a la planificación garantizará que no se planteen problemas al ejecutar las actividades de migración. 

> [!NOTE] 
> Hola instrucciones era muy contribuidos tooby hello Azure cliente asesoramiento team y arquitectos de soluciones de nube trabajar con los clientes en migración enviornments grandes. Por lo tanto este documento seguirá tooget actualizado a medida que nuevos patrones de éxito que surgen, por tanto, compruebe de tiempo tootime toosee si hay alguna recomendación nuevo.

Hay cuatro fases generales del proceso de migración de hello:

![Fases de migración](../media/virtual-machines-windows-migration-classic-resource-manager/plan-labtest-migrate-beyond.png)

## <a name="plan"></a>Plan

### <a name="technical-considerations-and-tradeoffs"></a>Consideraciones técnicas y compromisos

Dependiendo del tamaño de requisitos técnicos, regiones geográficas y las prácticas operativas, puede ser conveniente tooconsider:

1. ¿Por qué le interesa contar con Azure Resource Manager en su organización?  ¿Qué razones comerciales de Hola para una migración?
2. ¿Qué razones técnicas de hello para el Administrador de recursos de Azure?  ¿Qué (si existe) servicios adicionales de Azure le gustaría que tuviera tooleverage?
3. ¿Qué aplicación (o conjuntos de máquinas virtuales) se incluyen en la migración de hello?
4. ¿Los escenarios son compatibles con la API de migración de hello?  Hola de revisión [no admite características y configuraciones](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations).
5. ¿Los equipos operativos ahora admiten aplicaciones y máquinas virtuales tanto en el modelo clásico como en Azure Resource Manager?
6. ¿Cómo Azure Resource Manager cambia los procesos de creación de informes, la supervisión, la administración y la implementación de máquinas virtuales, en caso de que sea posible?  ¿Necesitan los scripts de implementación toobe actualizar?
7. ¿Qué es comunicaciones Hola pensado tooalert las partes interesadas (los usuarios finales, los propietarios de aplicaciones y los propietarios de infraestructura)?
8. ¿Según la complejidad Hola del entorno de hello, debe haber un período de mantenimiento donde la aplicación hello es tooend disponible a los usuarios y propietarios de tooapplication?  En su caso, ¿durante cuánto tiempo?
9. ¿Qué es partes interesadas tooensure del plan de aprendizaje de hello son conocimientos y expertos en el Administrador de recursos de Azure?
10. ¿Qué es la administración del programa Hola o el plan de administración de proyecto para la migración de hello?
11. ¿Cuáles son las escalas de tiempo de Hola para migración de Azure Resource Manager hello y otros relacionados con mapas de carreteras de tecnología?  ¿Están perfectamente alineados?

### <a name="patterns-of-success"></a>Patrones de éxito

Disponer de los clientes correcta detallados planes donde hello por encima de preguntas se explican, documentado y se rige.  Asegúrese de planes de migración de hello toosponsors comunicado ampliamente y las partes interesadas.  Adquiera conocimientos sobre las opciones de migración; se recomienda leer este documento de migración a continuación.

* [Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate desde tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Usar recursos de IaaS CLI toomigrate de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Revisión de los errores más comunes en la migración](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="pitfalls-tooavoid"></a>Tooavoid de riesgos

- Error tooplan.  pasos de la tecnología de Hola de esta migración se ha comprobado y resultado de hello es predecible.
- Presuponiendo que Hola API de migración de plataforma admitida tendrá en cuenta para todos los escenarios. Hola de lectura [no admite características y configuraciones](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) toounderstand qué escenarios se admiten.
- Ausencia de planificación de interrupciones potenciales de la aplicación para los usuarios finales.  Planear suficiente búfer tooadequately advertir a los usuarios finales de tiempo de aplicación potencialmente no está disponible.


## <a name="lab-test"></a>Análisis de laboratorio 

**Replicación del entorno y realización de una migración de prueba**
  > [!NOTE]
  > La replicación exacta de un entorno existente se ejecuta mediante una herramienta en la que ha contribuido la comunidad que no es compatible oficialmente con el Soporte técnico de Microsoft. Por lo tanto, es un **opcional** paso pero es hello toofind de manera mejor los problemas sin tocar los entornos de producción. Si no es una opción con una herramienta contribuyó a la Comunidad, conozca Hola validar/preparación/Abort simulacro recomendación siguiente.
  >
  
  Realizar una prueba de laboratorio de su escenario exacto (proceso, red y almacenamiento) es Hola mejor manera tooensure una migración sin problemas. Esto le ayudará a garantizar:

  - Un laboratorio completamente independiente o un tootest de entorno que no sea de producción existente. Se recomienda un laboratorio completamente independiente que se pueda migrar varias veces y que se pueda modificar de forma destructiva.  Las secuencias de comandos toocollect/hidrato metadatos de las suscripciones de hello real se enumeran a continuación.
  - Es una práctica de buena idea toocreate hello en una suscripción independiente. Hello razón es que laboratorio Hola se cierra varias veces, y tener un independiente, suscripción aislado reducirá las posibilidades de Hola que algo real obtendrá accidentalmente eliminó.

  Esto puede realizarse mediante hello AsmMetadataParser herramienta. [Aquí puede encontrar más información sobre esta herramienta](https://github.com/Azure/classic-iaas-resourcemanager-migration/tree/master/AsmToArmMigrationApiToolset).

### <a name="patterns-of-success"></a>Patrones de éxito

siguiente Hola eran problemas detectados en muchas de las migraciones más grandes de Hola. Esto no es una lista exhaustiva y debe hacer referencia a toohello [no admite características y configuraciones](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#unsupported-features-and-configurations) para obtener más detalles. Puede encontrarse o no con estos problemas técnicos, pero, de plantearse, podrá tener una experiencia más fluida si los soluciona antes de intentar realizar la migración.

- **Realice un simulacro validar/preparación/Abort** -trata quizás hello más importante paso tooensure clásico tooAzure el Administrador de recursos migración se realice correctamente. API de migración de Hello tiene tres pasos principales: validar, preparación y confirmación. Validar will leer el estado de saludo del entorno clásico y devuelven un resultado de todos los problemas. Sin embargo, como algunos problemas pueden existir en la pila del Administrador de recursos de Azure hello, validar no detecta todo el contenido. paso siguiente de Hello en proceso de migración, preparación le ayudará a exponer esos problemas. Preparar will mover Hola metadatos de clásico tooAzure el Administrador de recursos, pero no se confirmación Hola movimiento y se elimina ni cambia nada en hello lado clásico. Hola simulacro implica preparar la migración de hello, a continuación, anulando (**no confirmar**) preparar la migración de Hola. objetivo de Hello de simulacro valida/preparar/abort es toosee todos los metadatos de Hola de pila del Administrador de recursos de Azure hello, examinarlo (*mediante programación o en el Portal de*) y compruebe que todo lo que se migrará correctamente y trabajar con problemas técnicos.  También le permitirá hacerse una idea de la duración de la migración, a fin de que pueda planear el tiempo de inactividad.  Un validar/preparar/abort no hace que los tiempos de inactividad de usuario; por lo tanto, es el uso de tooapplication no provocan interrupciones.
  - estos artículos Hola necesitarán toobe resolver antes de simulacro hello, pero una prueba de simulacro hará que se vacíe también de forma segura estos pasos de preparación si se omiten. Durante la migración de enterprise, hemos encontrado una preparación para la migración de forma segura y muy valiosa tooensure Hola simulacro toobe.
  - Preparar cuando se ejecuta, el control de hello plano (operaciones de administración de Azure) se bloqueará para red virtual completa de hello, por lo que no se pueden realizar cambios tooVM metadatos durante validar/preparar/abort.  No obstante, en caso contrario, ninguna función de la aplicación (Escritorio remoto, uso de máquina virtual, etc.) se verá afectada.  Los usuarios de máquinas virtuales de hello no sabrá que simulacro Hola se está ejecutando.

- **VPN y circuitos ExpressRoute**. Actualmente no se pueden migrar las puertas de enlace de ExpressRoute con vínculos de autorización sin tiempos de inactividad. Para solucionar este problema de hello, consulte [ExpressRoute migrar circuitos y asociado redes virtuales de modelo de implementación de administrador de recursos de hello toohello clásico](../../expressroute/expressroute-migration-classic-resource-manager.md).

- **Las extensiones de VM** -extensiones de máquina Virtual son potencialmente Hola mayores obstáculos toomigrating máquinas virtuales en ejecución. La corrección de extensiones de máquina virtual puede tardar de 1 a 2 días, por lo que es necesario realizar la planificación teniendo esto en cuenta.  Un trabajo del agente de Azure es necesario tooreport back-estado de extensión de máquina virtual de máquinas virtuales en ejecución. Si el estado de hello vuelve a funcionar como no válidos para una máquina virtual en ejecución, Esto detendrá la migración. el propio agente Hello no necesita toobe en condiciones de funcionamiento tooenable migración, pero si existen extensiones de Hola de máquina virtual, a continuación, será necesario un agente de trabajo y conectividad a internet saliente (con DNS) para reenviar toomove de migración.
  - Si se pierde el servidor DNS de tooa de conectividad durante la migración, todas las extensiones de VM excepto BGInfo v1. \* necesita toofirst quitará de cada máquina virtual antes de preparar la migración y posteriormente volver a agregarla toohello back-VM después de la migración de Azure Resource Manager.  **Esto solo se aplica a las máquinas virtuales en ejecución.**  Si hello las máquinas virtuales se detiene desasignada, extensiones de máquina virtual no es necesario toobe quitado. **Nota:** muchas extensiones, como la supervisión de Security Center y Diagnósticos de Azure, se reinstalarán automáticamente después de la migración, por lo que su eliminación no plantea ningún problema.
  - Además, asegúrese de que los Grupos de seguridad de red no restringen el acceso saliente a Internet. Esto puede suceder con algunas configuraciones de Grupos de seguridad de red. Acceso a internet saliente (y DNS) es necesario para las extensiones de VM toobe migrado tooAzure el Administrador de recursos. 
  - Hay dos versiones de hello extensión BGInfo: v1 y v2.  Si Hola máquina virtual se creó mediante el portal clásico de Hola o PowerShell, Hola VM probablemente tendrá extensión v1 de hello en él. Esta extensión no necesita toobe quita y se omitirá (no se migran) por la migración de hello API. Sin embargo, si Hola clásico de máquina virtual se creó con el nuevo portal de Azure hello, probablemente tendrá versión Hola v2 basada en JSON de BGInfo, que puede ser migrado tooAzure el Administrador de recursos proporciona agente Hola funciona y tiene acceso a internet saliente (y DNS). 
  - **Opción de corrección 1**. Si sabe que las máquinas virtuales no tendrán saliente de internet tener acceso a un servicio DNS de trabajo y funciona a agentes de Azure en máquinas virtuales de hello, desinstale todas las extensiones de máquina virtual como parte de la migración de hello antes de preparar, volver a instalar las extensiones de VM de hello después de la migración. 
  - **Opción de corrección 2**. Si las extensiones de VM son demasiado grandes de un obstáculo, otra opción es tooshutdown/cancelar la asignación de todas las máquinas virtuales antes de la migración. Migrar Hola cancela la asignación de máquinas virtuales, y vuelva a iniciarlas en hello Azure Resource Manager lado. aquí la ventaja de Hello es que las extensiones de VM se migrarán. Hola inconveniente es que se perderán todos los públicos accesibles desde direcciones IP virtuales (Esto puede ser un elemento que no son de inicio), y obviamente hello las máquinas virtuales se apagará causando un impacto mayor en las aplicaciones de trabajo.

    > [!NOTE] 
    > Si se configura una directiva de Azure Security Center contra Hola máquinas virtuales que se está migradas en ejecución, directiva de seguridad de hello necesidades toobe detenido antes de quitar las extensiones, en caso contrario, seguridad de hello extensión de supervisión se reinstalará automáticamente en Hola VM después de quitarla.

- **Conjuntos de disponibilidad** : para una red virtual (vNet) toobe migrado tooAzure el Administrador de recursos, Hola máquinas virtuales de implementación (es decir, el servicio de nube) contenido clásico debe estar todas en un conjunto de disponibilidad u Hola máquinas virtuales de todos los no debe ser en cualquier conjunto de disponibilidad. Tener más de un conjunto de disponibilidad en servicio de nube de hello no es compatible con el Administrador de recursos de Azure y se detendrá la migración.  Además, no puede haber algunas máquinas virtuales en un conjunto de disponibilidad, y algunas máquinas virtuales no están en un conjunto de disponibilidad. tooresolve esto, se necesita tooremediate o reorganice el servicio en la nube.  Tenga esto en cuenta para realizar la planificación, ya que esta operación puede llevar bastante tiempo. 

- **Las implementaciones del rol Web o de trabajo** -servicios en la nube que contiene roles web y de trabajo no se pueden migrar tooAzure el Administrador de recursos. roles de web y de trabajo de Hello en primer lugar deben quitarse de red virtual de Hola para que pueda empezar la migración.  Una solución típica es toojust movimiento web/trabajo rol instancias tooa independiente clásico red virtual que también está vinculado tooan circuito de ExpressRoute o toomigrate Hola código toonewer PaaS App Services (esta discusión está más allá del ámbito de Hola de este documento). En primero Hola volver a implementar el caso, crear una nueva red virtual clásica, mover o volver a implementar hello web/trabajo roles toothat nueva red virtual y luego eliminar las implementaciones de Hola de red virtual de Hola que se va a mover. No se requiere ningún cambio de código. Hola nueva [intercambio de tráfico de red Virtual](../../virtual-network/virtual-network-peering-overview.md) capacidad puede ser usado toopeer Hola juntos clásico red virtual que contiene los roles de web y de trabajo de Hola y otras redes virtuales en Hola la misma región de Azure como Hola red virtual que se va a migrar (**después de que se complete la migración de red virtual como emparejar las redes virtuales no se pueden migrar**), por lo tanto, proporcionar a Hola mismas capacidades sin pérdida de rendimiento y no hay penalizaciones latencia/ancho de banda. Dada la adición de Hola de [intercambio de tráfico de red Virtual](../../virtual-network/virtual-network-peering-overview.md), las implementaciones del rol web o de trabajo ahora puede ser mitigadas fácilmente y no bloquean Hola migración tooAzure el Administrador de recursos.

- **Cuotas de Azure Resource Manager**: las regiones de Azure tienen cuota y límites independientes para el modelo clásico y Azure Resource Manager. Aunque en un escenario de migración no es consumido nuevo hardware *(nos estamos intercambiando las máquinas virtuales existentes de clásico tooAzure el Administrador de recursos)*, cuotas del Administrador de recursos de Azure sigue necesitan toobe en su lugar con capacidad suficiente antes de puede iniciar la migración. A continuación figuran límites principales de Hola que vimos causar problemas.  Abra un Hola de tooraise de vale de soporte técnico de cuota limita. 

    > [!NOTE]
    > Estos límites necesitan toobe produce en Hola la misma región como migra su toobe entorno actual.
    >

    - Interfaces de red
    - Equilibradores de carga
    - Direcciones IP públicas
    - Direcciones IP públicas estáticas
    - Núcleos
    - Grupos de seguridad de red
    - Tablas de ruta

    Puede comprobar las cuotas de Azure Resource Manager actual utilizando Hola siga los comandos con la versión más reciente de Hola de CLI de Azure 2.0.

    **Proceso***(núcleos y conjuntos de disponibilidad)*

    ```bash
    az vm list-usage -l <azure-region> -o jsonc 
    ```

    **Red***(redes virtuales, direcciones IP públicas estáticas, direcciones IP públicas, grupos de seguridad de red, interfaces, equilibradores de carga y tablas de rutas)*
    
    ```bash
    az network list-usages -l <azure-region> -o jsonc
    ```

    **Almacenamiento***(cuenta de almacenamiento)*
    
    ```bash
    az storage account show-usage
    ```

- **Límites de la API de Azure Resource Manager**: si tiene un entorno lo suficientemente grande (por ejemplo, > 400 máquinas virtuales en una red virtual), podría llegar a Hola predeterminado API límites para las escrituras de limitación (actualmente **1200 escrituras por hora**) en el Administrador de recursos de Azure. Antes de iniciar la migración, debe generar un tooincrease de incidencia de soporte técnico de este límite de su suscripción.

- **Aprovisionamiento superó el tiempo de espera de estado de VM** : si cualquier máquina virtual tiene el estado de Hola de **aprovisionamiento agotó**, este necesidades toobe resuelve previo a la migración. Hola única forma toodo se trata con el tiempo de inactividad por desaprovisionamiento/reaprovisionamiento Hola VM (delete, guarde el disco de Hola y vuelva a Hola VM). 

- **Estado de la VM de RoleStateUnknown** : Si detiene la migración debido tooa **estado desconocido de la función** error de mensajes, estudie Hola VM mediante el portal de Hola y asegúrese de que se está ejecutando. Este error suele desaparecer por sí solo (no se precisa de ninguna corrección) transcurridos unos minutos, suele ser de carácter transitorio y suele detectarse durante las operaciones de **inicio**, **detención** y **reinicio** de una máquina virtual. **Práctica recomendada:** vuelva a intentar la migración después de unos minutos. 

- **El clúster de Fabric no existe** : en algunos casos, determinadas máquinas virtuales no se pueden migrar por distintas razones poco comunes. Uno de estos casos conocidos es si Hola máquina virtual se creó recientemente (en hello última semana o más) y tooland un clúster de Azure que aún no está equipado para cargas de trabajo de Azure Resource Manager produjeron.  Obtendrá un error que dice **clúster fabric no existe** y hello VM no se pueden migrar. Esperando un par de días normalmente resolverá este problema en particular como clúster de hello pronto obtendrá Azure Resource Manager habilitado. Sin embargo, una solución inmediata es demasiado`stop-deallocate` Hola VM, a continuación, continuar con la migración e iniciar Hola VM realizar copias de seguridad en el Administrador de recursos de Azure después de migrar.

### <a name="pitfalls-tooavoid"></a>Tooavoid de riesgos

- No se abreviar y omitir las migraciones de simulacro valida/preparar/abort Hola.
- Más, si no todos, de los posibles problemas se detectarán durante los pasos de hello validar/preparar/abort.

## <a name="migration"></a>Migración

### <a name="technical-considerations-and-tradeoffs"></a>Consideraciones técnicas y compromisos

Ahora está listo porque haya repasado Hola presentan problemas conocidos con su entorno.

Para las migraciones real de hello, puede ser conveniente tooconsider:

1. Planificar y programar la red virtual de hello (unidad más pequeña de migración) con mayor prioridad.  Hola simples redes virtuales en primer lugar, y el progreso con hello más complicada redes virtuales.
2. La mayoría de los clientes tendrán entornos de producción y de no producción.  Programe la producción en última instancia.
3. **(OPCIONAL)**  Programe un tiempo de inactividad por mantenimiento con una gran cantidad de búfer en caso de que surjan problemas inesperados.
4. Comuníquese con los equipos de soporte y póngase de acuerdo con ellos en caso de que surjan problemas.

### <a name="patterns-of-success"></a>Patrones de éxito

orientación técnica de Hola de hello sección de prueba de laboratorio anterior debe tenerse en cuenta y mitiga migración real tooa anterior.  Con las pruebas oportunas, migración de hello es realmente un no evento.  Para entornos de producción, podría ser útil toohave soporte técnico adicional, como un socio de Microsoft de confianza o servicios Premier de Microsoft.

### <a name="pitfalls-tooavoid"></a>Tooavoid de riesgos

Pruebas no totalmente pueden causar problemas y retraso en la migración de Hola.  

## <a name="beyond-migration"></a>Después de la migración

### <a name="technical-considerations-and-tradeoffs"></a>Consideraciones técnicas y compromisos

Ahora que ya está en el Administrador de recursos de Azure, maximizar la plataforma de Hola.  Hola de lectura [información general del Administrador de recursos de Azure](../../azure-resource-manager/resource-group-overview.md) toofind out sobre ventajas adicionales.

Tooconsider cosas:

- Agrupación de migración de hello con otras actividades.  La mayoría de los clientes optan por una ventana de mantenimiento de la aplicación.  Si es así, puede querer toouse esta tooenable de tiempo de inactividad otras capacidades de Azure Resource Manager como cifrado y migración tooManaged discos.
- Volver a visitar Hola técnica y motivos empresariales para el Administrador de recursos de Azure; Habilitar Hola servicios adicionales disponibles solo en Azure Resource Manager que se aplican tooyour entorno.
- Modernice el entorno con servicios PaaS.

### <a name="patterns-of-success"></a>Patrones de éxito

Ser intencionados en qué servicios ahora desea tooenable en el Administrador de recursos de Azure.  Muchos clientes encontrar Hola debajo atractivas de sus entornos de Azure:

- [Control de acceso basado en rol](../../azure-resource-manager/resource-group-overview.md#access-control).
- [Plantillas de Azure Resource Manager para una implementación más sencilla y controlada](../../azure-resource-manager/resource-group-overview.md#template-deployment).
- [Etiquetas](../../azure-resource-manager/resource-group-using-tags.md).
- [Control de actividad](../../azure-resource-manager/resource-group-audit.md)
- [Directivas de recursos](../../azure-resource-manager/resource-manager-policy.md)

### <a name="pitfalls-tooavoid"></a>Tooavoid de riesgos

Recuerde que ¿por qué se inició este viaje de migración de clásico tooAzure el Administrador de recursos.  ¿Cuáles fueron razones comerciales que Hola original? ¿Ha conseguido razón empresarial de hello?


## <a name="next-steps"></a>Pasos siguientes

* [Información general de migración admitida por la plataforma de recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Técnica de fondo admitida por la plataforma de migración de clásico tooAzure el Administrador de recursos](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Planear la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Usar recursos de IaaS PowerShell toomigrate desde tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-ps.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Herramientas de la Comunidad para ayudar con la migración de los recursos de IaaS de tooAzure clásico Administrador de recursos](../windows/migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Revisión de los errores más comunes en la migración](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Hola de revisión más preguntas más frecuentes acerca de cómo migrar recursos de IaaS de tooAzure clásico Administrador de recursos](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
