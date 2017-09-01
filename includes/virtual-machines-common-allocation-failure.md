
Si su problema con Azure no se trata en este artículo, visite los [foros de Azure en MSDN y Stack Overflow](https://azure.microsoft.com/support/forums/). Puede publicar su problema en ellos o en @AzureSupport en Twitter. También puede presentar una solicitud de soporte técnico de Azure; para ello seleccione **Obtener soporte técnico** en el sitio de [soporte técnico de Azure](https://azure.microsoft.com/support/options/) .

## <a name="general-troubleshooting-steps"></a>Pasos generales para solucionar problemas
### <a name="troubleshoot-common-allocation-failures-in-the-classic-deployment-model"></a>Solución de problemas de errores de asignación comunes en el modelo de implementación clásica
Estos pasos básicos pueden ayudar a resolver muchos errores de asignación en las máquinas virtuales.

* Cambie el tamaño de la máquina virtual por uno diferente.<br>
    Haga clic en **examinar todo** > **máquinas virtuales (clásicas)** > la máquina virtual > **configuración** > **tamaño**. Para información detallada, vea [Cambiar el tamaño de la máquina virtual](https://msdn.microsoft.com/library/dn168976.aspx).
* Elimine todas las máquinas virtuales del servicio en la nube y vuelva a crearlas.<br>
    Haga clic en **examinar todo** > **máquinas virtuales (clásicas)** > la máquina virtual > **eliminar**. Luego, haga clic en **Nuevo** > **Compute** > [imagen de máquina virtual].

### <a name="troubleshoot-common-allocation-failures-in-the-azure-resource-manager-deployment-model"></a>Solución de problemas de errores de asignación comunes en el modelo de implementación del Administrador de recursos de Azure
Estos pasos básicos pueden ayudar a resolver muchos errores de asignación en las máquinas virtuales.

* Detenga (desasigne) todas las máquinas virtuales que estén en el mismo conjunto de disponibilidad y, luego, reinícielas.<br>
    Para detener: haga clic en **grupos de recursos** > el grupo de recursos > **recursos** > su conjunto de disponibilidad > **máquinas virtuales** > la máquina virtual >  **Detener**.
  
    Una vez detenidas todas las máquinas virtuales, seleccione la primera y haga clic en **Iniciar**.

## <a name="background-information"></a>Información de contexto
### <a name="how-allocation-works"></a>Cómo funciona la asignación
Los servidores de los centros de datos de Azure están particionados en clústeres. Normalmente, se intenta una solicitud de asignación en varios clústeres, pero es posible que determinadas restricciones de la solicitud de asignación obliguen a la plataforma de Azure a intentar la solicitud en solo un clúster. En este artículo, nos referiremos a dicha solicitud como "anclada a un clúster". En el diagrama número 1 que puede ver a continuación, se ilustra el caso de una asignación normal que se intenta en varios clústeres; En el diagrama 2 se ilustra el caso de una asignación que está anclada al clúster 2, porque ahí es donde se hospeda el servicio en la nube CS_1 o el conjunto de disponibilidad.
![Diagrama de asignación](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>¿Por qué se producen errores de asignación?
Cuando una solicitud de asignación está anclada a un clúster, existe una posibilidad menor de encontrar recursos libres dado que el grupo de recursos disponible es más pequeño. Además, si la solicitud de asignación está anclada a un clúster pero el tipo de recurso que solicita no se admite en ese clúster, la solicitud dará error aunque el clúster tenga recursos libres. En el diagrama 3 a continuación se ilustra el caso en el que una asignación anclada da error porque el único clúster candidato no tiene recursos libres. En el diagrama 4 se ilustra el caso en el que una asignación anclada da error porque el único clúster candidato no admite el tamaño de VM solicitado, a pesar de que el clúster tiene recursos libres.

![Error de asignaciones ancladas](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-the-classic-deployment-model"></a>Pasos detallados para solucionar problemas de escenarios de errores de asignación específicos en el modelo de implementación clásica
A continuación se presentan los escenarios de asignación comunes que ocasionan que una solicitud de asignación quede anclada. Nos dedicaremos a cada escenario más adelante en este artículo.

* Cambio del tamaño de una VM o incorporación de VM o instancias de rol a un servicio en la nube existente.
* Reinicio de las VM detenidas (desasignadas) parcialmente.
* Reinicio de las VM detenidas (desasignadas) completamente.
* Implementaciones de ensayo o producción (solo plataforma como servicio).
* Grupo de afinidad (proximidad de la VM o el servicio).
* Red virtual basada en un grupo de afinidad

Cuando reciba un error de asignación, compruebe si alguno de los escenarios descritos se aplica en su caso. Use el error de asignación que devuelve la plataforma de Azure para identificar el escenario correspondiente. Si la solicitud está anclada, quite algunas de las restricciones de anclaje para abrir su solicitud a más clústeres y aumente así la posibilidad de que la asignación se realice correctamente.

En general, mientras el error no indique que "no se admite el tamaño de VM solicitado", siempre puede volver a intentarlo más adelante, cuando se hayan liberado suficientes recursos en el clúster para dar cabida a la solicitud. Si el problema tiene que ver con que el tamaño de la VM solicitado no se admite, pruebe con una VM diferente. De lo contrario, la única opción es quitar la restricción anclada.

Dos escenarios comunes de error están relacionados con los grupos de afinidad. Antes, un grupo de afinidad se usaba para proporcionar una estrecha proximidad a las VM o a las instancias de servicio, o bien para permitir la creación de redes virtuales. Con la introducción de las redes virtuales regionales, los grupos de afinidad ya no son necesarios para crear una red virtual. Al reducirse la latencia de red en la infraestructura de Azure, ha cambiado la recomendación de usar grupos de afinidad para la proximidad de las VM o servicios.

En el diagrama 5 a continuación se presenta la taxonomía de los escenarios de asignación (anclados).
![Taxonomía de asignaciones ancladas](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> El error que se muestra en cada escenario de asignación está en forma abreviada. Para ver las cadenas de error al detalle, consulte [Búsqueda de cadenas de error](#Error string lookup).
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-to-an-existing-cloud-service"></a>Escenario de asignación: cambio del tamaño de una VM o incorporación de VM o instancias de rol a un servicio en la nube existente.
**Error**

Upgrade_VMSizeNotSupported o GeneralError

**Causa de anclaje del clúster**

Las solicitudes para cambiar el tamaño de una VM o agregar una VM o una instancia de rol a un servicio en la nube existente se tienen que intentar realizar en el clúster original que hospeda dicho servicio en la nube. La creación de un nuevo servicio en la nube permite que la plataforma de Azure encuentre otro clúster que tenga recursos libres o uno que admita el tamaño de VM solicitado.

**Solución alternativa**

Si el error es Upgrade_VMSizeNotSupported *, pruebe con otro tamaño de máquina virtual. Si el uso de un tamaño de VM diferente no es una opción, pero es aceptable el uso de una dirección IP virtual (VIP) distinta, cree un nuevo servicio en la nube para hospedar la nueva VM y agréguelo a la red virtual regional donde se ejecutan las VM existentes. Aunque su servicio en la nube no use una red virtual regional, puede crear una nueva para el nuevo servicio en la nube y, después, conectar la [red virtual existente a la nueva red virtual](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Si el error es GeneralError*, es probable que el tipo de recurso (por ejemplo, un tamaño determinado de VM) sea compatible con el clúster pero que este no tenga recursos libres en ese momento. De forma parecida a como se ha indicado anteriormente, agregue el recurso de proceso deseado mediante la creación de un nuevo servicio en la nube (tenga en cuenta que el nuevo servicio en la nube tiene que usar otra dirección IP virtual) y use la red virtual regional para conectarse a los servicios en la nube.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) parcialmente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación parcial indica que se detuvieron (desasignaron) una o varias VM de un servicio en la nube, pero no todas. Al detener (desasignar) una VM, se liberan los recursos asociados. Por lo tanto, reiniciar esa VM detenida (desasignada) implica una nueva solicitud de asignación. Reiniciar las VM en un servicio en la nube desasignado parcialmente es equivalente a agregarlas a un servicio en la nube existente. Las solicitud de asignación se debe intentar realizar en el clúster original que hospeda el servicio en la nube. La creación de otro servicio en la nube permite a la plataforma de Azure encontrar otro clúster que tenga recursos libres o uno que admita el tamaño de máquina virtual solicitado.

**Solución alternativa**

Si es aceptable el uso de una dirección IP virtual diferente, elimine las VM detenidas (desasignadas), pero mantenga los discos asociados, y vuelva agregar las VM mediante un servicio en la nube diferente. Use una red virtual regional para conectarse a los servicios en la nube:

* Si el servicio en la nube existente usa una red virtual regional, agregue el nuevo servicio en la nube a la misma red virtual.
* Si el servicio en la nube no usa una red virtual regional, cree una nueva para el nuevo servicio en la nube y, seguidamente, [conecte la red virtual existente a la nueva red virtual](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) completamente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación completa indica que detuvo (desasignó) todas las VM de un servicio en la nube. Las solicitudes de asignación para reiniciar estas VM se deben intentar realizar en el clúster original que hospeda el servicio en la nube. La creación de un nuevo servicio en la nube permite que la plataforma de Azure encuentre otro clúster que tenga recursos libres o uno que admita el tamaño de VM solicitado.

**Solución alternativa**

Si es aceptable el uso de una dirección IP virtual diferente, elimine las VM originales detenidas (desasignadas), pero mantenga los discos asociados, y elimine el servicio en la nube correspondiente (los recursos de proceso asociados ya se liberaron cuando detuvo [desasignó] las VM). Cree un nuevo servicio en la nube para volver a agregar las VM.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Escenario de asignación: implementaciones de ensayo o producción (solo plataforma como servicio).
**Error**

New_General * o New_VMSizeNotSupported *

**Causa de anclaje del clúster**

Las implementaciones de ensayo y de producción de un servicio en la nube se hospedan en el mismo clúster. Cuando se agrega la segunda implementación, la solicitud de asignación correspondiente se intenta en el mismo clúster que hospeda la primera implementación.

**Solución alternativa**

Elimine la primera implementación y el servicio en la nube original y vuelva implementar el servicio en la nube. Esta acción puede conseguir la primera implementación en un clúster que tenga suficientes recursos libres para ajustarse a ambas implementaciones, o bien en un clúster que admita los tamaños de VM solicitados.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Escenario de asignación: grupo de afinidad (proximidad de la VM o el servicio)
**Error**

New_General * o New_VMSizeNotSupported *

**Causa de anclaje del clúster**

Cualquier recurso de proceso asignado a un grupo de afinidad está asociado a un clúster. Las nuevas solicitudes de recursos de proceso de ese grupo de afinidad se intentan llevar a cabo en el mismo clúster en el que están hospedados los recursos existentes. Esto es así con independencia de que los nuevos recursos se creen mediante un servicio en la nube nuevo o existente.

**Solución alternativa**

Si no es necesario un grupo de afinidad, no lo use, o bien intente agrupar los recursos de proceso en varios grupos de afinidad.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Escenario de asignación: red virtual basada en un grupo de afinidad
**Error**

New_General * o New_VMSizeNotSupported *

**Causa de anclaje del clúster**

Antes de que se presentaran las redes virtuales regionales, era necesario asociar una red virtual a un grupo de afinidad. Como consecuencia, los recursos de proceso colocados en un grupo de afinidad se rigen por las mismas restricciones que se han descrito en la sección anterior "Escenario de asignación: grupo de afinidad (proximidad de la VM o el servicio)". Es decir, los recursos de proceso están asociados a un clúster.

**Solución alternativa**

Si no necesita ningún grupo de afinidad, cree una red virtual regional para los recursos nuevos que vaya a agregar y, luego, [conecte la red virtual existente a la nueva red virtual](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

También puede [migrar la red virtual basada en un grupo de afinidad a una red virtual regional](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)y, después, volver a agregar los recursos deseados.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-the-azure-resource-manager-deployment-model"></a>Pasos detallados para solucionar problemas de escenarios de errores de asignación específicos en el modelo de implementación de Azure Resource Manager
A continuación se presentan los escenarios de asignación comunes que ocasionan que una solicitud de asignación quede anclada. Nos dedicaremos a cada escenario más adelante en este artículo.

* Cambio del tamaño de una VM o incorporación de VM o instancias de rol a un servicio en la nube existente.
* Reinicio de las VM detenidas (desasignadas) parcialmente.
* Reinicio de las VM detenidas (desasignadas) completamente.

Cuando reciba un error de asignación, compruebe si alguno de los escenarios descritos se aplica en su caso. Use el error de asignación que devuelve la plataforma de Azure para identificar el escenario correspondiente. Si la solicitud está anclada a un clúster existente, quite algunas de las restricciones de anclaje para abrir su solicitud a más clústeres y aumentar así la posibilidad de que la asignación se realice correctamente.

En general, mientras el error no indique que "no se admite el tamaño de VM solicitado", siempre puede volver a intentarlo más adelante, cuando se hayan liberado suficientes recursos en el clúster para dar cabida a la solicitud. Si el problema tiene que ver con que el tamaño de VM solicitado no se admite, consulte las posibles soluciones a continuación.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-to-an-existing-availability-set"></a>Escenario de asignación: cambio del tamaño de una VM o incorporación de VM o instancias de rol a un conjunto de disponibilidad existente.
**Error**

Upgrade_VMSizeNotSupported * o GeneralError *

**Causa de anclaje del clúster**

La solicitud para cambiar el tamaño de una VM o agregarla a un conjunto de disponibilidad existente se tiene que intentar en el clúster original que hospeda dicho conjunto. La creación de un nuevo conjunto de disponibilidad permite que la plataforma de Azure encuentre otro clúster que tenga recursos libres o uno que admita el tamaño de VM solicitado.

**Solución alternativa**

Si el error es Upgrade_VMSizeNotSupported *, pruebe con otro tamaño de máquina virtual. Si el uso de un tamaño de VM diferente no es una opción, detenga toda las VM del conjunto de disponibilidad. De esta forma podrá cambiar el tamaño de la máquina virtual que se asignará a un clúster que admita el tamaño deseado.

Si el error es GeneralError*, es probable que el tipo de recurso (por ejemplo, un tamaño determinado de VM) sea compatible con el clúster pero que este no tenga recursos libres en ese momento. Si la VM puede formar parte de un conjunto de disponibilidad diferente, cree una nueva en otro conjunto de disponibilidad (en la misma región). Esta nueva VM se puede agregar luego a la misma red virtual.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) parcialmente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación parcial indica que se detuvieron (desasignaron) una o varias VM de un conjunto de disponibilidad, pero no todas. Al detener (desasignar) una VM, se liberan los recursos asociados. Por lo tanto, reiniciar esa VM detenida (desasignada) implica una nueva solicitud de asignación. Reiniciar las VM en un conjunto de disponibilidad desasignado parcialmente es equivalente a agregarlas a uno conjunto de disponibilidad existente. Las solicitud de asignación se debe intentar realizar en el clúster original que hospeda el conjunto de disponibilidad.

**Solución alternativa**

Detenga todas las VM del conjunto de disponibilidad antes de reiniciar la primera de ellas. De esta forma se garantiza que hay un nuevo intento de asignación en marcha y que se puede seleccionar un nuevo clúster que tenga capacidad disponible.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) completamente
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación completa indica que detuvo (desasignó) todas las VM de un conjunto de disponibilidad. La solicitud de asignación para reiniciar estas VM se dirigirá a todos los clústeres que admitan el tamaño deseado.

**Solución alternativa**

Seleccione un nuevo tamaño de VM para asignar. Si esto no funciona, vuelva a intentarlo más tarde.

## <a name="error-string-lookup"></a>Búsqueda de cadenas de error
**New_VMSizeNotSupported***

El tamaño de VM (o la combinación de tamaños de VM) que se necesita en esta implementación no se puede aprovisionar debido a restricciones en las solicitudes de implementación. Si es posible, intente relajar las restricciones como los enlaces de red virtual, intente realizar la implementación en un servicio hospedado que no tenga ninguna otra implementación y en otro grupo de afinidad o sin grupo de afinidad, o bien intente realizar la implementación en otra región.

**New_General***

Error en la asignación: no se pudieron satisfacer las restricciones de la solicitud. La nueva implementación del servicio solicitada está enlazada a un grupo de afinidad, su destino es una red virtual o hay una implementación existente bajo este servicio hospedado. Todas estas condiciones restringen la nueva implementación a recursos específicos de Azure. Inténtelo de nuevo más tarde o pruebe a reducir el tamaño de la máquina virtual o el número de instancias de rol. También puede quitar, si es posible, las restricciones mencionadas o intentar realizar la implementación en otra región.

**Upgrade_VMSizeNotSupported***

No se puede actualizar la implementación. Es posible que el tamaño de la máquina virtual solicitada XXX no esté disponible entre los recursos que son compatibles con la implementación existente. Inténtelo más tarde, con otro tamaño de VM o con menos instancias de rol, o bien cree una implementación en un servicio hospedado vacío con un nuevo grupo de afinidad o sin enlazar ningún grupo de afinidad.

**GeneralError***

"Se produjo un error interno en el servidor. Vuelva a intentar realizar la solicitud" o "Error al producir una asignación para el servicio".

