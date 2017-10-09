## <a name="understand-vm-reboots---maintenance-vs-downtime"></a>Información sobre los reinicios de máquinas virtuales: mantenimiento frente a tiempo de inactividad
Hay tres escenarios que pueden causar toovirtual máquina en Azure afectando: mantenimiento del hardware no planeada, tiempos de inactividad inesperados y el mantenimiento planeado.

* **Evento de mantenimiento de Hardware no planeado** se produce cuando hello plataforma Windows Azure predice ese hardware Hola o cualquier máquina física de la tooa asociados de componente plataforma, consiste en toofail. Cuando la plataforma de hello predice un error, emitirá un hardware no planeada mantenimiento eventos tooreduce Hola impacto toohello máquinas virtuales hospedadas en ese hardware. Azure utiliza toomigrate Hola máquinas virtuales de migración en vivo tecnología de hello errores máquina física de hardware tooa correcto. Migración en vivo es una máquina virtual de operación que solo las pausas Hola Máquina Virtual durante un breve periodo de conservación. Se mantienen las conexiones de red, memoria y archivos abiertos, pero rendimiento puede reducirse antes o después de los eventos de Hola. En casos donde no se puede usar la migración en vivo, Hola VM experimentará tiempos de inactividad inesperados, tal y como se describe a continuación.


* **Un tiempo de inactividad inesperado** rara vez se produce cuando se ha producido un error hardware de Hola o infraestructura física Hola subyacente de la máquina virtual de alguna manera. Entre estos podemos encontrar errores de la red local, errores de los discos locales u otras errores a nivel de bastidor. Cuando se detecta este error, hello plataforma Windows Azure migra automáticamente (apresurado) su tooa de máquina virtual correcto máquina física. Durante la Hola recuperación del procedimiento, máquinas virtuales experimentar tiempos de inactividad (reiniciar) y alguna pérdida de casos de la unidad temporal de Hola. Hola conectados SO y siempre se conservan los discos de datos. 

* **Planeada eventos de mantenimiento** son las actualizaciones periódicas realizadas por toohello Microsoft subyacente de la plataforma Windows Azure tooimprove confiabilidad general, el rendimiento y seguridad de infraestructura de plataforma de hello destinados a las máquinas virtuales. La mayoría de estas actualizaciones se realizan sin que las máquinas virtuales ni los servicios en la nube resulten afectados (consulte [Mantenimiento de conservación de máquinas virtuales](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/preserving-maintenance)). Aunque Hola plataforma Windows Azure intenta toouse VM preservar mantenimiento en todas las ocasiones posibles, hay algunos casos poco comunes cuando estas actualizaciones requieren un reinicio de la máquina virtual tooapply Hola necesario toohello subyacente infraestructura de actualizaciones. En este caso, puede realizar mantenimiento planificado de Azure con la operación de volver a implementar de mantenimiento mediante la realización de mantenimiento de Hola para sus máquinas virtuales en el período de tiempo adecuado de Hola. Para más información, consulte [Mantenimiento planeado de máquinas virtuales](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/planned-maintenance/).


impacto de hello tooreduce de tiempo de inactividad debido tooone o varios de estos eventos, se recomienda Hola seguir las prácticas recomendadas para las máquinas virtuales de alta disponibilidad:

* [Configure varias máquinas virtuales en un conjunto de disponibilidad para la redundancia]
* [Uso de Managed Disks para las máquinas virtuales de un conjunto de disponibilidad]
* [Usar eventos programados tooproactively respuesta tooVM afectar a eventos] (https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-scheduled-events)
* [Configure cada nivel de aplicación en conjuntos separados de disponibilidad]
* [Combinación de un equilibrador de carga con conjuntos de disponibilidad]

## <a name="configure-multiple-virtual-machines-in-an-availability-set-for-redundancy"></a>Configure varias máquinas virtuales en un conjunto de disponibilidad para la redundancia
aplicación de tooyour de redundancia de tooprovide, le recomendamos que agrupe dos o más máquinas virtuales en un conjunto de disponibilidad. Esta configuración garantiza que durante un evento de mantenimiento planeado o no, al menos una máquina virtual está disponible y cumple Hola 99,95% SLA de Azure. Para obtener más información, vea hello [SLA para las máquinas virtuales](https://azure.microsoft.com/support/legal/sla/virtual-machines/).

> [!IMPORTANT]
> Evite dejar una máquina virtual de instancia única sola en un conjunto de disponibilidad. En esta configuración, las máquinas virtuales no reciben la garantía del Acuerdo de Nivel de Servicio y sufrirán un tiempo de inactividad durante los eventos de mantenimiento planeado de Azure, excepto cuando solo una máquina virtual use [Azure Premium Storage](../articles/storage/common/storage-premium-storage.md). VM simples usando almacenamiento premium, se aplica Hola SLA de Azure.

Cada máquina virtual en el conjunto de disponibilidad se asigna un **Actualizar dominio** y un **dominio de error** por hello subyacente de la plataforma Windows Azure. Para un conjunto de disponibilidad determinado, cinco dominios de actualización no-configurables por el usuario se asignan de forma predeterminada (las implementaciones del Administrador de recursos, a continuación, pueden ser mayor tooprovide los dominios de actualización de too20) tooindicate grupos de máquinas virtuales y hardware físico subyacente que puede reiniciarse en hello mismo tiempo. Cuando más de cinco máquinas virtuales se configuran dentro de un único conjunto de disponibilidad, máquina virtual de la sexta Hola se coloca en hello mismo actualizar el dominio como máquina virtual de la primera hello, hello séptimo Hola al que mismo dominio de actualizaciones como Hola segunda máquina virtual por lo que en. orden de Hola de dominios de actualización que se está reiniciando no se puede continuar secuencialmente durante el mantenimiento planeado, pero solo una actualización de dominio se reinicia cada vez. Un dominio de actualización reiniciada recibe toorecover de 30 minutos antes de mantenimiento se inicia en un dominio de actualización diferentes.

Dominios de error definen grupo Hola de máquinas virtuales que comparten un conmutador de origen y de red común de energía. De forma predeterminada, máquinas virtuales de hello configuradas dentro de su conjunto de disponibilidad están separadas a través de dominios de error de toothree para las implementaciones del Administrador de recursos (dos dominios de error para clásico). Al mismo tiempo la colocación de las máquinas virtuales en un conjunto de disponibilidad no protege la aplicación de sistema operativo o errores específicos de la aplicación, lo limitar el impacto de Hola de posibles errores de hardware físico, las interrupciones de red o las interrupciones de energía.

<!--Image reference-->
   ![Dibujo conceptual de configuración del dominio de error y de dominio de actualización Hola](./media/virtual-machines-common-manage-availability/ud-fd-configuration.png)

## <a name="use-managed-disks-for-vms-in-an-availability-set"></a>Uso de Managed Disks para las máquinas virtuales de un conjunto de disponibilidad
Si actualmente está usando máquinas virtuales con discos no administrados, es muy recomendable [convertir máquinas virtuales en el conjunto de disponibilidad toouse administrado discos](../articles/virtual-machines/windows/convert-unmanaged-to-managed-disks.md).

[Discos administrados por](../articles/virtual-machines/windows/managed-disks-overview.md) proporcionar una mayor confiabilidad para conjuntos de disponibilidad al garantizar que los discos de Hola de máquinas virtuales en un conjunto de disponibilidad lo suficientemente aislados entre sí tooavoid puntos únicos de error. Para ello, coloque automáticamente discos hello en clústeres de almacenamiento diferente. Si se produce un error en un clúster de almacenamiento debido a un error toohardware o software, solo instancias de máquina virtual de hello con discos de esas marcas producirá un error.

![Dominios de error de disco administrado](./media/virtual-machines-common-manage-availability/md-fd.png)

> [!IMPORTANT]
> número de Hola de dominios de error para los conjuntos de disponibilidad administrada varía según la región - dos o tres por región. Hello tabla siguiente muestran el número de Hola por región

[!INCLUDE [managed-disks-common-fault-domain-region-list](managed-disks-common-fault-domain-region-list.md)]

Si tiene previsto toouse las máquinas virtuales con [sin administrar discos](../articles/virtual-machines/windows/about-disks-and-vhds.md#types-of-disks), siga por debajo de las prácticas recomendadas para las cuentas de almacenamiento donde se almacenan los discos duros virtuales (VHD) de máquinas virtuales como [blobs en páginas](https://docs.microsoft.com/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs#about-page-blobs).

1. **Mantener todos los discos (sistema operativo y datos) asociados a una máquina virtual en hello misma cuenta de almacenamiento**
2. **Hola de revisión [límites](../articles/storage/common/storage-scalability-targets.md) en número de Hola de discos no administrados en una cuenta de almacenamiento** antes de agregar la cuenta de almacenamiento de más discos duros virtuales tooa
3. **Utilice una cuenta de almacenamiento independiente para cada máquina virtual de un conjunto de disponibilidad.** No comparta cuentas de almacenamiento con varias máquinas virtuales en hello mismo conjunto de disponibilidad. Es aceptable para las máquinas virtuales en diferentes cuentas de almacenamiento de tooshare de conjuntos de disponibilidad si se siguen por encima de los procedimientos recomendados

## <a name="configure-each-application-tier-into-separate-availability-sets"></a>Configure cada nivel de aplicación en conjuntos separados de disponibilidad
Si las máquinas virtuales son todas las casi idénticas y servir Hola mismo propósito para la aplicación, es recomendable que configure un conjunto de disponibilidad para cada nivel de la aplicación.  Si coloca dos diferentes niveles en hello mismo conjunto de disponibilidad, todas las máquinas virtuales en hello misma capa de aplicación puede reiniciarse a la vez. Al configurar al menos dos máquinas virtuales en un conjunto de disponibilidad para cada nivel, se garantiza que al menos haya disponible una en cada nivel.

Por ejemplo, podría colocar todas las máquinas virtuales de hello en front-end de saludo de la aplicación que se ejecuta IIS, Apache, Nginx en un único conjunto de disponibilidad. Asegúrese de que solo las máquinas virtuales front-end se colocan en hello mismo conjunto de disponibilidad. De la misma manera, asegúrese de que solo las máquinas virtuales de niveles de datos se colocan en su propio conjunto de disponibilidad, por ejemplo, las máquinas virtuales replicadas de SQL Server o las de MySQL.

<!--Image reference-->
   ![Niveles de aplicación](./media/virtual-machines-common-manage-availability/application-tiers.png)

## <a name="combine-a-load-balancer-with-availability-sets"></a>Combinación de un equilibrador de carga con conjuntos de disponibilidad
Combinar hello [equilibrador de carga Azure](../articles/load-balancer/load-balancer-overview.md) con una disponibilidad establecido tooget Hola mayoría resistencia a la aplicación. Hola equilibrador de carga de Azure distribuye el tráfico entre varias máquinas virtuales. Para nuestro máquinas virtuales del nivel estándar, se incluye Hola equilibrador de carga de Azure. No todos los niveles de máquina virtual incluyen hello equilibrador de carga de Azure. Para obtener más información sobre el equilibrio de carga en máquinas virtuales, consulte [Equilibrio de carga de máquinas virtuales](../articles/virtual-machines/virtual-machines-linux-load-balance.md).

Si no se encuentra el equilibrador de carga de hello configurado toobalance tráfico entre varias máquinas virtuales, entonces cualquier evento de mantenimiento planificado afecta a Hola solo porción de tráfico máquina virtual, provocando una capa de aplicación de tooyour de interrupción. Colocar varias máquinas virtuales de hello mismo nivel en hello mismo equilibrador de carga y disponibilidad conjunto permite tráfico toobe continuamente atendido por al menos una instancia.


<!-- Link references -->
[Configure varias máquinas virtuales en un conjunto de disponibilidad para la redundancia]: #configure-multiple-virtual-machines-in-an-availability-set-for-redundancy
[Configure cada nivel de aplicación en conjuntos separados de disponibilidad]: #configure-each-application-tier-into-separate-availability-sets
[Combinación de un equilibrador de carga con conjuntos de disponibilidad]: #combine-a-load-balancer-with-availability-sets
[Avoid single instance virtual machines in availability sets]: #avoid-single-instance-virtual-machines-in-availability-sets
[Uso de Managed Disks para las máquinas virtuales de un conjunto de disponibilidad]: #use-managed-disks-for-vms-in-an-availability-set
