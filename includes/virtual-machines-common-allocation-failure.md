
Si el problema de Azure no se trata en este artículo, visite hello [foros de Azure en MSDN y el desbordamiento de la pila](https://azure.microsoft.com/support/forums/). Puede publicar su problema en estos foros o too@AzureSupport en Twitter. Además, puede registrar una solicitud de soporte técnico de Azure seleccionando **obtener asistencia** en hello [soporte técnico de Azure](https://azure.microsoft.com/support/options/) sitio.

## <a name="general-troubleshooting-steps"></a>Pasos generales para solucionar problemas
### <a name="troubleshoot-common-allocation-failures-in-hello-classic-deployment-model"></a>Solucionar errores comunes de asignación en el modelo de implementación clásica de Hola
Estos pasos básicos pueden ayudar a resolver muchos errores de asignación en las máquinas virtuales.

* Cambiar el tamaño de hello VM tooa otro tamaño de VM.<br>
    Haga clic en **Examinar todo** > **Máquinas virtuales (clásico)** > su máquina virtual > **Configuración** > **Tamaño**. Para obtener instrucciones detalladas, consulte [cambiar el tamaño de máquina virtual de hello](https://msdn.microsoft.com/library/dn168976.aspx).
* Elimine todas las máquinas virtuales del servicio de nube de Hola y volver a crear las máquinas virtuales.<br>
    Haga clic en **Examinar todo** > **Máquinas virtuales (clásico)** > su máquina virtual > **Eliminar**. Luego, haga clic en **Nuevo** > **Compute** > [imagen de máquina virtual].

### <a name="troubleshoot-common-allocation-failures-in-hello-azure-resource-manager-deployment-model"></a>Solucionar errores comunes de asignación en el modelo de implementación de hello Azure Resource Manager
Estos pasos básicos pueden ayudar a resolver muchos errores de asignación en las máquinas virtuales.

* Detener (desasignar) todas las máquinas virtuales en hello mismo disponibilidad establecido, a continuación, reinicie cada uno de ellos.<br>
    toostop: haga clic en **grupos de recursos** > el grupo de recursos > **recursos** > su conjunto de disponibilidad > **máquinas virtuales** > la máquina virtual >  **Detener**.
  
    Después de detener todas las máquinas virtuales, seleccione Hola primera máquina virtual y haga clic en **iniciar**.

## <a name="background-information"></a>Información de contexto
### <a name="how-allocation-works"></a>Cómo funciona la asignación
servidores de Hello en centros de datos de Azure se dividen en clústeres. Normalmente, se intenta realizar una solicitud de asignación en varios clústeres, pero es posible que determinadas restricciones de solicitud de asignación de hello forzar la solicitud de hello plataforma Windows Azure tooattempt hello en un único clúster. En este artículo, nos referiremos toothis como "anclado tooa clúster". Diagrama 1 a continuación ilustra el caso en Hola de una asignación normal que se puede utilizar en varios clústeres. Diagrama 2 ilustra el caso de hello de una asignación que ha anclado tooCluster 2 ya que ese es donde se hospeda Hola existente CS_1 de servicio de nube o conjunto de disponibilidad.
![Diagrama de asignación](./media/virtual-machines-common-allocation-failure/Allocation1.png)

### <a name="why-allocation-failures-happen"></a>¿Por qué se producen errores de asignación?
Cuando una solicitud de asignación está anclado tooa clúster, hay una mayor probabilidad de errores toofind liberar recursos, puesto que el grupo de recursos disponibles de hello es menor. Además, si su solicitud de asignación está anclado tooa clúster pero tipo hello de recurso solicitado no es compatible con dicho clúster, se producirá un error en la solicitud incluso si el clúster de hello tiene liberar recursos. Diagrama 3 a continuación ilustra el caso en Hola donde una asignación anclada produce un error porque Hola candidato solo clúster no tiene recursos libres. Diagrama 4 muestra caso Hola donde una asignación anclada produce un error porque no es compatible con clúster candidato solo de Hola Hola solicitado tamaño de máquina virtual, aunque el clúster de hello tiene liberar recursos.

![Error de asignaciones ancladas](./media/virtual-machines-common-allocation-failure/Allocation2.png)

## <a name="detailed-troubleshoot-steps-specific-allocation-failure-scenarios-in-hello-classic-deployment-model"></a>Detallada solucionar problemas de escenarios de error de asignación concretos de pasos en el modelo de implementación clásica de Hola
Estos son los escenarios de asignación comunes que provocan un toobe de solicitud de asignación anclado. Nos dedicaremos a cada escenario más adelante en este artículo.

* Cambiar el tamaño de una máquina virtual o agregue las máquinas virtuales o servicio de nube existente de tooan de instancias de rol
* Reinicio de las VM detenidas (desasignadas) parcialmente.
* Reinicio de las VM detenidas (desasignadas) completamente.
* Implementaciones de ensayo o producción (solo plataforma como servicio).
* Grupo de afinidad (proximidad de la VM o el servicio).
* Red virtual basada en un grupo de afinidad

Cuando reciba un error de asignación, consulte si cualquiera de los escenarios de hello descritos tooyour error de aplicación. Errores de asignación de hello devuelto por el escenario correspondiente de hello plataforma Windows Azure tooidentify Hola usan. Si la solicitud está anclada, quite algunos de hello anclado restricciones tooopen los clústeres de toomore de solicitud, con lo que aumenta la posibilidad de Hola de éxito de asignación.

En general, siempre y cuando Hola error no indica "hello solicitado no se admite el tamaño de máquina virtual", puede siempre Reintentar en un momento posterior, que haya sido suficientes recursos liberado en hello clúster tooaccommodate su solicitud. Si problema Hola que ese Hola solicitado no se admite el tamaño de máquina virtual, pruebe un tamaño de máquina virtual diferente. En caso contrario, Hola única opción es hello tooremove fijar la restricción.

Dos escenarios de error comunes son grupos de tooaffinity relacionados. Hola anteriores, un grupo de afinidad era tooprovide usado cerca tooVMs/servicio instancias o estaba tooenable usado Hola creación de una red virtual. Con la introducción de Hola de redes virtuales regionales, grupos de afinidad ya no son necesario toocreate una red virtual. Con la reducción de Hola de latencia de red en la infraestructura de Azure, grupos de afinidad de hello recomendación toouse de proximidad VM/servicio ha cambiado.

Diagrama de 5 siguiente presenta taxonomía Hola de escenarios de asignación de hello (anclado).
![Taxonomía de asignaciones ancladas](./media/virtual-machines-common-allocation-failure/Allocation3.png)

> [!NOTE]
> error de Hello especificado en cada escenario de asignación es una forma abreviada. Consulte toohello [búsqueda de cadena de Error](#Error string lookup) para las cadenas de error detallado.
> 
> 

## <a name="allocation-scenario-resize-a-vm-or-add-vms-or-role-instances-tooan-existing-cloud-service"></a>Escenario de asignación: cambiar el tamaño de una máquina virtual o agregar rol o máquinas virtuales instancias de servicio en la nube tooan
**Error**

Upgrade_VMSizeNotSupported o GeneralError

**Causa de anclaje del clúster**

A solicitud tooresize una máquina virtual o agregar una máquina virtual o un servicio de nube existente de rol instancia tooan tiene toobe vuelve a intentar cada clúster original Hola que hospeda el servicio en la nube Hola. Crear un nuevo servicio de nube permite Hola plataforma Windows Azure toofind otro clúster que tiene recursos libres o admite el tamaño de la máquina virtual de Hola que solicitó.

**Solución alternativa**

Si el error de hello Upgrade_VMSizeNotSupported *, pruebe un tamaño de máquina virtual diferente. Si usa un tamaño diferente de la máquina virtual no es una opción, pero si es aceptable toouse una dirección IP virtual (VIP), diferentes de crear un nuevo toohost de servicio de nube Hola nueva máquina virtual y agregue Hola nueva nube servicio toohello red virtual regional donde hello las máquinas virtuales existentes se están ejecutando. Si su servicio de nube existente no usa una red virtual regional, puede crear una nueva red virtual para el nuevo servicio de nube hello y, a continuación, conecte su [red virtual toohello nueva red virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Si el error de hello es GeneralError *, es probable que Hola tipo de recurso (por ejemplo, un determinado tamaño de memoria virtual) es compatible con clúster de hello, pero Hola clúster no tiene recursos libres en el momento de Hola. Toohello similar por encima del escenario, agregar recursos de proceso de hello deseado por la creación de un nuevo servicio de nube (tenga en cuenta que el servicio de nube nuevo de hello tiene toouse una VIP diferente) y usar una red virtual regional tooconnect servicios en la nube.

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) parcialmente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación parcial indica que se detuvieron (desasignaron) una o varias VM de un servicio en la nube, pero no todas. Al detener (desasignar) una máquina virtual, Hola asociado se liberan los recursos. Por lo tanto, reiniciar esa VM detenida (desasignada) implica una nueva solicitud de asignación. Reiniciar las máquinas virtuales en un servicio de nube parcialmente desasignada es equivalente tooadding servicio de nube de máquinas virtuales tooan existente. solicitud de asignación de Hello tiene toobe vuelve a intentar cada clúster original Hola que hospeda el servicio en la nube Hola. Crear un servicio de nube diferente permite Hola plataforma Windows Azure toofind otro clúster que tiene el recurso gratuito o admite el tamaño de la máquina virtual de Hola que solicitó.

**Solución alternativa**

Si es aceptable toouse una VIP diferente, delete Hola detenido (desasignadas) las máquinas virtuales (pero tenga discos de hello asociado) y agregue hello las máquinas virtuales hacia atrás por un servicio de nube diferente. Use una red virtual regional tooconnect servicios en la nube:

* Si el servicio de nube existente usa una red virtual regional, basta con agregar toohello de servicio de nube nuevo Hola misma red virtual.
* Si su servicio de nube existente no usa una red virtual regional, crear una nueva red virtual para el nuevo servicio de nube hello y, a continuación, [conectar su red virtual toohello nueva red virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

## <a name="allocation-scenario-restart-fully-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) completamente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación completa indica que detuvo (desasignó) todas las VM de un servicio en la nube. las solicitudes de asignación de Hello toorestart que estas máquinas virtuales tienen toobe vuelve a intentar cada clúster original Hola que aloja el servicio de nube de Hola. Crear un nuevo servicio de nube permite Hola plataforma Windows Azure toofind otro clúster que tiene recursos libres o admite el tamaño de la máquina virtual de Hola que solicitó.

**Solución alternativa**

Si es aceptable toouse una VIP diferente, delete Hola original detenido (desasignadas) las máquinas virtuales (pero tenga discos de hello asociado) y eliminar Hola correspondiente servicio en la nube (proceso Hola asociado ya se liberan los recursos cuando detenida (desasignada) Hola máquinas virtuales). Volver a crear un nuevo Hola de tooadd de servicio de nube máquinas virtuales.

## <a name="allocation-scenario-stagingproduction-deployments-platform-as-a-service-only"></a>Escenario de asignación: implementaciones de ensayo o producción (solo plataforma como servicio).
**Error**

New_General* o New_VMSizeNotSupported*

**Causa de anclaje del clúster**

Hola implementación e implementación de producción de hello de un servicio de nube de almacenamiento provisional se hospeda en hello mismo clúster. Cuando se agrega la segunda implementación de hello, se intentará la solicitud de asignación correspondiente de Hola Hola mismo clúster que hospeda Hola primera implementación.

**Solución alternativa**

Eliminar la primera implementación de Hola y el servicio de nube original de Hola y volver a implementar el servicio en la nube Hola. Esta acción podría llegar primera implementación de hello en un clúster que tenga suficientes recursos libres toofit ambas implementaciones o en un clúster que admita tamaños de máquinas virtuales de Hola que solicitó.

## <a name="allocation-scenario-affinity-group-vmservice-proximity"></a>Escenario de asignación: grupo de afinidad (proximidad de la VM o el servicio)
**Error**

New_General* o New_VMSizeNotSupported*

**Causa de anclaje del clúster**

Cualquier recurso de proceso es el grupo de afinidad asignado tooan enlazado tooone clúster. Nuevas solicitudes de recursos de proceso en ese grupo de afinidad se intentan en hello mismo clúster donde se hospedan los recursos existentes de Hola. Esto es cierto si Hola nuevos recursos se crean a través de un nuevo servicio de nube o un servicio de nube existente.

**Solución alternativa**

Si no es necesario un grupo de afinidad, no lo use, o bien intente agrupar los recursos de proceso en varios grupos de afinidad.

## <a name="allocation-scenario-affinity-group-based-virtual-network"></a>Escenario de asignación: red virtual basada en un grupo de afinidad
**Error**

New_General* o New_VMSizeNotSupported*

**Causa de anclaje del clúster**

Antes de que se introdujeron redes virtuales regionales, eran tooassociate requiere una red virtual con un grupo de afinidad. Como resultado, los recursos de proceso que se colocan en un grupo de afinidad están enlazados por hello las mismas restricciones tal y como se describe en hello "escenario de asignación: grupo de afinidad (proximidad/servicio de máquinas virtuales)" sección anterior. recursos de proceso de Hello son tooone relacionados con clústeres.

**Solución alternativa**

Si no necesita un grupo de afinidad, cree una nueva red virtual regional para hello nuevos recursos que se va a agregar, y, a continuación, [conectar su red virtual toohello nueva red virtual existente](https://azure.microsoft.com/blog/vnet-to-vnet-connecting-virtual-networks-in-azure-across-different-regions/). Consulte más información sobre las [redes virtuales regionales](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/).

Como alternativa, puede [migrar la red virtual de red virtual basado en el grupo de afinidad tooa regional](https://azure.microsoft.com/blog/2014/11/26/migrating-existing-services-to-regional-scope/)y, a continuación, vuelva a agregar recursos de hello deseado.

## <a name="detailed-troubleshooting-steps-specific-allocation-failure-scenarios-in-hello-azure-resource-manager-deployment-model"></a>Escenarios de error de asignación concretos de pasos en el modelo de implementación de Azure Resource Manager Hola de solución de problemas detallada
Estos son los escenarios de asignación comunes que provocan un toobe de solicitud de asignación anclado. Nos dedicaremos a cada escenario más adelante en este artículo.

* Cambiar el tamaño de una máquina virtual o agregue las máquinas virtuales o servicio de nube existente de tooan de instancias de rol
* Reinicio de las VM detenidas (desasignadas) parcialmente.
* Reinicio de las VM detenidas (desasignadas) completamente.

Cuando reciba un error de asignación, consulte si cualquiera de los escenarios de hello descritos tooyour error de aplicación. Errores de asignación de hello devuelto por el escenario correspondiente de hello plataforma Windows Azure tooidentify Hola usan. Si la solicitud está anclado tooan clúster existente, quite algunos de hello anclado restricciones tooopen los clústeres de toomore de solicitud, con lo que aumenta la posibilidad de Hola de éxito de asignación.

En general, siempre y cuando Hola error no indica "hello solicitado no se admite el tamaño de máquina virtual", puede siempre Reintentar en un momento posterior, que haya sido suficientes recursos liberado en hello clúster tooaccommodate su solicitud. Si el problema de Hola que Hola solicitado no se admite el tamaño de máquina virtual, vea a continuación para soluciones alternativas.

## <a name="allocation-scenario-resize-a-vm-or-add-vms-tooan-existing-availability-set"></a>Escenario de asignación: cambiar el tamaño de una máquina virtual o Agregar conjunto de disponibilidad de las máquinas virtuales tooan existente
**Error**

Upgrade_VMSizeNotSupported* o GeneralError*

**Causa de anclaje del clúster**

Una solicitud tooresize una máquina virtual o agregar un tooan VM existente conjunto de disponibilidad tiene toobe vuelve a intentar cada clúster original Hola que hospeda el conjunto de disponibilidad existente Hola. Crear un nuevo conjunto de disponibilidad permite Hola plataforma Windows Azure toofind otro clúster que tiene recursos libres o admite el tamaño de la máquina virtual de Hola que solicitó.

**Solución alternativa**

Si el error de hello Upgrade_VMSizeNotSupported *, pruebe un tamaño de máquina virtual diferente. Si no es una opción con un tamaño distinto de la máquina virtual, detenga todas las máquinas virtuales en el conjunto de disponibilidad de Hola. Entonces, puede cambiar el tamaño de Hola de máquina virtual de Hola que asignará el clúster tooa de hello VM que admita Hola había deseado tamaño de máquina virtual.

Si el error de hello es GeneralError *, es probable que Hola tipo de recurso (por ejemplo, un determinado tamaño de memoria virtual) es compatible con clúster de hello, pero Hola clúster no tiene recursos libres en el momento de Hola. Si Hola VM puede formar parte de un conjunto de disponibilidad diferentes, cree una nueva máquina virtual en un conjunto de disponibilidad diferentes (Hola misma región). Esta nueva máquina virtual, a continuación, se puede agregar toohello misma red virtual.  

## <a name="allocation-scenario-restart-partially-stopped-deallocated-vms"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) parcialmente.
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación parcial indica que se detuvieron (desasignaron) una o varias VM de un conjunto de disponibilidad, pero no todas. Al detener (desasignar) una máquina virtual, Hola asociado se liberan los recursos. Por lo tanto, reiniciar esa VM detenida (desasignada) implica una nueva solicitud de asignación. Reiniciar las máquinas virtuales en un conjunto de disponibilidad parcialmente desasignada es equivalente tooadding tooan grupo de disponibilidad de las máquinas virtuales Set. solicitud de asignación de Hello tiene toobe vuelve a intentar cada clúster original Hola que hospeda el conjunto de disponibilidad existente Hola.

**Solución alternativa**

Detener todas las máquinas virtuales en la disponibilidad de hello establecer antes de reiniciar Hola primero. De esta forma se garantiza que hay un nuevo intento de asignación en marcha y que se puede seleccionar un nuevo clúster que tenga capacidad disponible.

## <a name="allocation-scenario-restart-fully-stopped-deallocated"></a>Escenario de asignación: reinicio de las VM detenidas (desasignadas) completamente
**Error**

GeneralError*

**Causa de anclaje del clúster**

La desasignación completa indica que detuvo (desasignó) todas las VM de un conjunto de disponibilidad. solicitud de asignación de Hello toorestart estas máquinas virtuales se aplicará a todos los clústeres que admiten Hola tamaño deseado.

**Solución alternativa**

Seleccione un nuevo tooallocate tamaño de máquina virtual. Si esto no funciona, vuelva a intentarlo más tarde.

## <a name="error-string-lookup"></a>Búsqueda de cadenas de error
**New_VMSizeNotSupported***

"Hola VM tamaño (o combinación de tamaños de máquina virtual) requerida por esta implementación no se puede aprovisionar debido a restricciones de la solicitud de toodeployment. Si es posible, intente reducir las restricciones como los enlaces de red virtual, implementación de servicio tooa hospedado con ninguna otra implementación en ella y tooa de afinidad diferente o un grupo con ningún grupo de afinidad o intente implementar tooa otra región. "

**New_General***

"Error de asignación; toosatisfy no se puede restricciones en la solicitud. Hello solicitado nueva implementación del servicio es grupo de afinidad tooan enlazado, se destina a una red virtual o hay una implementación existente en este servicio hospedado. Cualquiera de estas condiciones restringe Hola nueva implementación toospecific Azure recursos. Vuelva a intentarlo más tarde o pruebe a reducir el tamaño de la máquina virtual de Hola o el número de instancias de rol. O bien, si es posible, quite restricciones mencionado anteriormente de Hola o intente implementar tooa otra región."

**Upgrade_VMSizeNotSupported***

"Implementación de hello tooupgrade no se puede. Hola solicitado XXX de tamaño de máquina virtual no estén disponible en los recursos de hello admitir la implementación existente de Hola. Inténtelo más tarde, con otro tamaño de VM o con menos instancias de rol, o bien cree una implementación en un servicio hospedado vacío con un nuevo grupo de afinidad o sin enlazar ningún grupo de afinidad.

**GeneralError***

"el servidor de hello detectó un error interno. Vuelva a intentar la solicitud de hello." O "No se pudo tooproduce una asignación para el servicio de Hola".

