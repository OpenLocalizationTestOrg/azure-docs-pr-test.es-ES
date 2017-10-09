En este artículo se describe un conjunto de prácticas demostradas de ejecuta una máquina virtual (VM) de Windows en Azure, seguridad, disponibilidad, facilidad de uso y tooscalability de atención de pago.

> [!NOTE]
> Azure cuenta con dos modelos de implementación diferentes: [Azure Resource Manager][resource-manager-overview] y el clásico. En este artículo se utiliza el Administrador de recursos, que Microsoft recomienda para las implementaciones nuevas.
>
>

No se recomienda usar una sola máquina virtual para cargas de trabajo críticas, ya que se crea un único punto de error. Para una mayor disponibilidad, implemente varias máquinas virtuales en un [conjunto de disponibilidad][availability-set]. Para más información, consulte el artículo sobre la [ejecución de varias máquinas virtuales en Azure][multi-vm].

## <a name="architecture-diagram"></a>Diagrama de la arquitectura

Aprovisionamiento de una máquina virtual en Azure implica más partes móviles haya que simplemente Hola propia máquina virtual. Existen elementos de proceso, red y almacenamiento.

> Un documento de Visio que incluye este diagrama de arquitectura está disponible para su descarga desde hello [centro de descarga de Microsoft][visio-download]. Este diagrama es en hello "Proceso - VM única" página.
>
>

![[0]][0]

* **Grupo de recursos.** Un [*grupo de recursos*][resource-manager-overview] es un contenedor que incluye recursos relacionados. Crear un recurso de recursos del grupo toohold Hola de esta máquina virtual.
* **Máquina virtual**. Puede aprovisionar una máquina virtual en una lista de imágenes publicadas o desde un archivo de disco duro virtual (VHD) que carga el almacenamiento de blobs de tooAzure.
* **Disco del sistema operativo.** disco de SO Hello es un disco duro virtual almacenado en [el almacenamiento de Azure][azure-storage]. Esto significa que persiste incluso si el equipo host de hello deja de funcionar.
* **Disco temporal.** Hello crear máquina virtual con un disco temporal (hello `D:` unidad de Windows). Este disco se almacena en una unidad física en el equipo de host de Hola. *No* se guarda en Azure Storage y podría desaparecer durante los reinicios y otros eventos del ciclo de vida de la máquina virtual. Use este disco solo para datos temporales, como archivos de paginación o de intercambio.
* **Discos de datos.** Un [disco de datos][data-disk] es un VHD persistente usado para los datos de la aplicación. Discos de datos se almacenan en el almacenamiento de Azure, como disco de SO Hola.
* **Red virtual y subred.** Cada máquina virtual de Azure se implementa en una red virtual, que se divide a su vez en subredes.
* **Dirección IP pública.** Una dirección IP pública es necesario toocommunicate con hello VM&mdash;por ejemplo a través de escritorio remoto (RDP).
* **Interfaz de red (NIC)**. Hola NIC permite hello toocommunicate de máquina virtual con la red virtual de Hola.
* **Grupo de seguridad de red (NSG)**. Hola [NSG] [ nsg] es la subred de toohello de tráfico de red usado tooallow o denegar. Puede asociar un NSG a una NIC individual o a una subred. Si se asocia con una subred, hello NSG reglas aplican las máquinas virtuales de tooall en esa subred.
* **Diagnóstico.** Registro de diagnóstico es fundamental para administrar y solucionar problemas de hello VM.

## <a name="recommendations"></a>Recomendaciones

Hola se siguen las recomendaciones se aplica para la mayoría de los escenarios. Sígalas a menos que tenga un requisito concreto que las invalide.

### <a name="vm-recommendations"></a>Recomendaciones de VM

Azure ofrece muchos tamaños de máquina virtual diferente, pero se recomienda Hola DS - y GS-series porque admiten estos tamaños de máquina [almacenamiento Premium][premium-storage]. Seleccione uno de estos tamaños de máquina a menos que tenga una carga de trabajo especializada, como puede ser el caso de la informática de alto rendimiento. Para más información, consulte el artículo sobre [tamaños de máquinas virtuales][virtual-machine-sizes].

Si va a mover un tooAzure de carga de trabajo existente, inicio con tamaño de máquina virtual de hello es hello tooyour de coincidencia más cercana en servidores locales. A continuación, Hola medir el rendimiento de la carga de trabajo real con respetar tooCPU, memoria y operaciones de entrada/salida de disco por segundo (IOPS) y ajustar el tamaño de hello si es necesario. Si necesita varias NIC para la máquina virtual, tenga en cuenta que el número máximo de Hola de NIC es una función de hello [tamaño de máquina virtual][vm-size-tables].   

Al realizar el aprovisionamiento Hola máquinas virtuales y otros recursos, debe especificar una región. Por lo general, elija una región más cercana a usuarios internos de tooyour o clientes. Sin embargo, no todos los tamaños de máquina virtual están disponibles en todas las regiones. Para más información, consulte los [servicios por región][services-by-region]. toosee una lista de tamaños de VM Hola disponibles en una región determinada, ejecute hello siguiente comando de la interfaz de línea de comandos (CLI) de Azure:

```
azure vm sizes --location <location>
```

Para más información sobre cómo elegir una imagen de máquina virtual publicada, consulte [Navegación y selección de las imágenes de máquina virtual Windows en Azure con Powershell o CLI][select-vm-image].

### <a name="disk-and-storage-recommendations"></a>Recomendaciones de discos y almacenamiento

Para un mejor rendimiento de la E/S de disco, se recomienda [Premium Storage][premium-storage], que almacena los datos en unidades de estado sólido (SSD). Costo se basa en el tamaño de Hola de disco aprovisionado Hola. Las E/S por segundo y el rendimiento también dependen del tamaño del disco, por lo que al aprovisionar un disco, debería tener en cuenta los tres factores (capacidad, E/S por segundo y rendimiento).

Cree cuentas de almacenamiento de Azure independiente para cada discos de duros virtuales (VHD) de VM toohold hello en tooavoid orden alcanzar los límites de IOPS de hello las cuentas de almacenamiento.

Agregue uno o más discos de datos. Cuando se crea un nuevo disco duro virtual, no tiene formato. Inicie sesión en el disco de hello VM tooformat Hola. Si tiene un gran número de discos de datos, tener en cuenta los límites de E/S total de Hola de cuenta de almacenamiento de Hola. Para más información, consulte [Límites de discos de máquinas virtuales][vm-disk-limits].

Cuando sea posible, instale aplicaciones en un disco de datos, no el disco de sistema operativo Hola. Sin embargo, algunas aplicaciones heredadas que tenga componentes tooinstall en hello unidad C:. En ese caso, puede [cambiar el tamaño de disco de SO hello] [ resize-os-disk] mediante PowerShell.

Para obtener el mejor rendimiento, cree una cuenta de almacenamiento separadas toohold registros de diagnóstico. Una cuenta de almacenamiento con redundancia local (LRS) estándar es suficiente para este tipo de registros.

### <a name="network-recommendations"></a>Recomendaciones de red

la dirección IP pública Hola puede ser dinámico o estático. valor predeterminado de Hello es dinámico.

* Reserva una [dirección IP estática] [ static-ip] si necesita una dirección IP fija que no cambiará &mdash; por ejemplo, si necesita toocreate una A registrar en DNS o necesita Hola lista segura del agregado tooa de toobe dirección IP.
* También puede crear un nombre de dominio completo (FQDN) para la dirección IP de Hola. A continuación, puede registrar un [registro CNAME] [ cname-record] en DNS que señala toohello FQDN. Para obtener más información, consulte [crear un nombre de dominio completo en el portal de Azure hello][fqdn].

Todos los NSG contienen un conjunto de [reglas predeterminadas][nsg-default-rules], incluida una que bloquea todo el tráfico de entrada de Internet. no se puede eliminar las reglas predeterminadas de Hello, pero pueden reemplazarlos con otras reglas. tooenable tráfico de Internet, crear reglas que permitan el tráfico entrante toospecific puertos &mdash; por ejemplo, el puerto 80 para HTTP.  

tooenable RDP, agregue una regla NSG que permita el tráfico entrante tooTCP puerto 3389.

## <a name="scalability-considerations"></a>Consideraciones sobre escalabilidad

Puede escalar una máquina virtual hacia arriba o hacia abajo por [cambiar el tamaño de la máquina virtual de hello](../articles/virtual-machines/windows/sizes.md). tooscale out horizontalmente, coloque dos o más máquinas virtuales en un conjunto detrás de un equilibrador de carga de disponibilidad. Para más detalles, consulte [Running multiple VMs on Azure for scalability and availability][multi-vm] (Ejecución de varias máquinas virtuales en Azure para escalabilidad y disponibilidad).

## <a name="availability-considerations"></a>Consideraciones sobre disponibilidad

Para una mayor disponibilidad, implemente varias máquinas virtuales en un conjunto de disponibilidad. Este procedimiento también ofrece un [Acuerdo de Nivel de Servicio][vm-sla] (SLA) superior.

La máquina virtual puede verse afectada por un [mantenimiento planeado][planned-maintenance] o un [mantenimiento no planeado][manage-vm-availability]. Puede usar [registros de reinicio de la máquina virtual] [ reboot-logs] toodetermine si reiniciar una máquina virtual se produjo por mantenimiento planificado.

Los VHD se almacenan en [Azure Storage][azure-storage], que se replica para su disponibilidad y durabilidad.

tooprotect contra la pérdida accidental de datos durante las operaciones normales (por ejemplo, debido al error de usuario), también debería implementar copias de seguridad en un momento, mediante [las instantáneas de blob] [ blob-snapshot] u otra herramienta.

## <a name="manageability-considerations"></a>Consideraciones sobre la manejabilidad

**Grupos de recursos.** Colocar recursos estrechamente asociadas que Hola de recurso compartido de ciclo de vida del mismo en Hola mismo [grupo de recursos][resource-manager-overview]. Grupos de recursos permiten toodeploy y el monitor de recursos como un grupo y se acumulan los costos por grupo de recursos de facturación. También se pueden eliminar recursos en conjunto, lo que resulta muy útil para implementaciones de prueba. Asigne a los recursos nombres descriptivos. Que hace que sea más fácil toolocate un recurso específico y comprender su rol. Consulte [Recommended Naming Conventions for Azure Resources][naming conventions] (Convenciones de nomenclatura recomendadas para los recursos de Azure).

**Diagnósticos de máquina virtual.** Habilite la supervisión y el diagnóstico, como las métricas básicas de estado, los registros de infraestructura de diagnóstico y los [diagnósticos de arranque][boot-diagnostics]. Los diagnósticos de arranque pueden ayudarle a diagnosticar un error de arranque si la máquina virtual entra en un estado de imposibilidad de arranque. Para más información, consulte [Habilitación de supervisión y diagnóstico][enable-monitoring]. Hola de uso [recopilación de registros de Azure] [ log-collector] toocollect de extensión de la plataforma Azure registra y cargarlos tooAzure almacenamiento.   

Hola siguiente comando CLI habilita los diagnósticos de:

```
azure vm enable-diag <resource-group> <vm-name>
```

**Detención de una máquina virtual.** Azure hace una distinción entre los estados "Detenido" y "Desasignado". Se le cobrará cuando Hola estado de la VM se detiene, pero no cuando Hola VM está desasignada.

Usar hello después toodeallocate de comando CLI una máquina virtual:

```
azure vm deallocate <resource-group> <vm-name>
```

Hola portal de Azure, Hola **detener** botón desasigna Hola máquina virtual. Sin embargo, si el apagado a través del Hola OS con la sesión iniciada, hello VM se detiene pero *no* cancela la asignación, por lo que se le cobrará todavía.

**Eliminación de una máquina virtual.** Si elimina una máquina virtual, no se eliminan Hola discos duros virtuales. Esto significa que puede eliminar con seguridad Hola VM sin perder datos. Sin embargo, se le seguirá cobrando por el almacenamiento. Hola toodelete VHD, elimine el archivo hello [almacenamiento de blobs][blob-storage].

la eliminación accidental de tooprevent, use un [bloqueo de recurso] [ resource-lock] toolock Hola recursos completo bloqueo o grupo de recursos individuales, como Hola VM.

## <a name="security-considerations"></a>Consideraciones sobre la seguridad

Use [Azure Security Center] [ security-center] tooget una vista central del estado de seguridad de Hola de los recursos de Azure. Centro de seguridad supervisa los posibles problemas de seguridad y proporciona una imagen completa del estado de seguridad de saludo de la implementación. El Centro de seguridad se configura por cada suscripción de Azure. Habilite la recolección de datos de seguridad tal como se describe en [Uso del Centro de seguridad]. Una vez que habilite la recolección, el Centro de seguridad busca automáticamente las VM creadas en esa suscripción.

**Administración de revisiones.** Si está habilitada esta opción, el Centro de seguridad comprueba si faltan actualizaciones críticas y de seguridad. Use [configuración de directiva de grupo] [ group-policy] en las actualizaciones automáticas del sistema de hello VM tooenable.

**Antimalware.** Si está habilitada esta opción, el Centro de seguridad comprueba si está instalado software antimalware. También puede utilizar el centro de seguridad tooinstall antimalware software desde dentro de Hola portal de Azure.

**Operaciones.** Use [el control de acceso basado en roles] [ rbac] (RBAC) toocontrol acceso toohello Azure recursos que implemente. RBAC le permite asignar toomembers de roles de autorización del equipo DevOps. Por ejemplo, rol de lector de hello puede ver recursos de Azure, pero no crear, administrar o eliminarlos. Algunos roles son tipos de recursos de Azure tooparticular específico. Por ejemplo, rol de colaborador de la máquina Virtual de hello puede reiniciar o cancelar la asignación de una máquina virtual, restablezca la contraseña de administrador de hello, crear una nueva máquina virtual y así sucesivamente. Otros [roles de RBAC integrados][rbac-roles] que pueden resultar útiles para esta arquitectura de referencia son, por ejemplo, el de [Usuario de DevTest Lab][rbac-devtest] y el de [Colaborador de la red][rbac-network]. Un usuario puede asignarse toomultiple roles, y puede crear roles personalizados para los permisos más granulares aún más.

> [!NOTE]
> RBAC no limita las acciones de Hola que puede realizar un usuario ha iniciado sesión en una máquina virtual. Esos permisos están determinados por el tipo de cuenta de hello en el sistema operativo invitado de Hola.   
>
>

contraseña de administrador local hello tooreset, ejecute hello `vm reset-access` comando de CLI de Azure.

```
azure vm reset-access -u <user> -p <new-password> <resource-group> <vm-name>
```

Use [registros de auditoría] [ audit-logs] toosee aprovisionamiento de acciones y otros eventos de máquina virtual.

**Cifrado de datos.** Considere la posibilidad de [cifrado del disco de Azure] [ disk-encryption] si necesita tooencrypt Hola OS y discos de datos.

## <a name="solution-deployment"></a>Implementación de la solución

Hay disponible una implementación de esta arquitectura de referencia en [GitHub][github-folder]. Incluye una red virtual, un grupo de seguridad de red y una única máquina virtual. toodeploy Hola arquitectura, siga estos pasos:

1. Haga clic en botón Hola siguiente y seleccione cualquier "Abrir vínculo en una nueva pestaña" o "Abrir vínculo en nueva ventana."  
   [![Implementar tooAzure](../articles/guidance/media/blueprints/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fmspnp%2Freference-architectures%2Fmaster%2Fguidance-compute-single-vm%2Fazuredeploy.json)
2. Una vez que ha abierto el vínculo de Hola Hola portal de Azure, debe especificar valores para algunas de las opciones de hello:

   * Hola **grupo de recursos** nombre ya está definido en el archivo de parámetros de hello, así que seleccione **crear nuevo** y escriba `ra-single-vm-rg` en el cuadro de texto de Hola.
   * Región de SELECT Hola de hello **ubicación** cuadro de lista desplegable.
   * No modifique hello **plantilla raíz Uri** o hello **parámetro raíz Uri** cuadros de texto.
   * Seleccione **windows** en hello **tipo de SO** cuadro de lista desplegable.
   * Revisar Hola términos y condiciones, haga clic en hello **muestro mi conformidad toohello términos y condiciones indicadas anteriormente** casilla de verificación.
   * Haga clic en hello **compra** botón.
3. Espere a que hello toocomplete de implementación.
4. archivos de parámetros de Hello incluyen una contraseña y el nombre de usuario administrador codificado de forma rígida y se recomienda encarecidamente que inmediatamente cambiar ambos ajustes. Haga clic en la máquina virtual denominada hello `ra-single-vm0 `Hola portal de Azure. A continuación, haga clic en **de restablecimiento de contraseña** en hello **soporte técnico y solución de problemas** hoja. Seleccione **de restablecimiento de contraseña** en hello **modo** a continuación, seleccione un nuevo cuadro de lista desplegable **nombre de usuario** y **contraseña**. Haga clic en hello **actualización** botón Hola de toopersist nuevo nombre de usuario y contraseña.

Para obtener información sobre otras formas toodeploy esta arquitectura de referencia, vea el archivo Léame de Hola Hola [Guía de la vm solo][github-folder]] carpeta de GitHub.

## <a name="customize-hello-deployment"></a>Personalizar la implementación de Hola
Si necesita toochange Hola implementación toomatch sus necesidades, siga las instrucciones de Hola Hola [Léame][github-folder].

## <a name="next-steps"></a>Pasos siguientes
Para una mayor disponibilidad, implemente dos o más máquinas virtuales detrás de un equilibrador de carga. Para más información, consulte el artículo sobre la [ejecución de varias máquinas virtuales en Azure][multi-vm].

<!-- links -->

[audit-logs]: https://azure.microsoft.com/en-us/blog/analyze-azure-audit-logs-in-powerbi-more/
[availability-set]:../articles/virtual-machines/windows/tutorial-availability-sets.md
[azure-cli]: /cli/azure/get-started-with-az-cli2
[azure-storage]: ../articles/storage/storage-introduction.md
[blob-snapshot]: ../articles/storage/storage-blob-snapshots.md
[blob-storage]: ../articles/storage/storage-introduction.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[cname-record]: https://en.wikipedia.org/wiki/CNAME_record
[data-disk]: ../articles/storage/storage-about-disks-and-vhds-windows.md
[disk-encryption]: ../articles/security/azure-security-disk-encryption.md
[enable-monitoring]: ../articles/monitoring-and-diagnostics/insights-how-to-use-diagnostics.md
[fqdn]:../articles/virtual-machines/windows/portal-create-fqdn.md
[github-folder]: http://github.com/mspnp/reference-architectures/tree/master/guidance-compute-single-vm
[group-policy]: https://technet.microsoft.com/en-us/library/dn595129.aspx
[log-collector]: https://azure.microsoft.com/en-us/blog/simplifying-virtual-machine-troubleshooting-using-azure-log-collector/
[manage-vm-availability]:../articles/virtual-machines/windows/manage-availability.md
[multi-vm]: ../articles/guidance/guidance-compute-multi-vm.md
[naming conventions]: ../articles/guidance/guidance-naming-conventions.md
[nsg]: ../articles/virtual-network/virtual-networks-nsg.md
[nsg-default-rules]: ../articles/virtual-network/virtual-networks-nsg.md#default-rules
[planned-maintenance]:../articles/virtual-machines/windows/planned-maintenance.md
[premium-storage]: ../articles/storage/storage-premium-storage.md
[rbac]: ../articles/active-directory/role-based-access-control-what-is.md
[rbac-roles]: ../articles/active-directory/role-based-access-built-in-roles.md
[rbac-devtest]: ../articles/active-directory/role-based-access-built-in-roles.md#devtest-labs-user
[rbac-network]: ../articles/active-directory/role-based-access-built-in-roles.md#network-contributor
[reboot-logs]: https://azure.microsoft.com/en-us/blog/viewing-vm-reboot-logs/
[resize-os-disk]:../articles/virtual-machines/windows/expand-os-disk.md
[Resize-VHD]: https://technet.microsoft.com/en-us/library/hh848535.aspx
[Resize virtual machines]: https://azure.microsoft.com/en-us/blog/resize-virtual-machines/
[resource-lock]: ../articles/resource-group-lock-resources.md
[resource-manager-overview]: ../articles/azure-resource-manager/resource-group-overview.md
[security-center]: https://azure.microsoft.com/en-us/services/security-center/
[select-vm-image]:../articles/virtual-machines/windows/cli-ps-findimage.md
[services-by-region]: https://azure.microsoft.com/en-us/regions/#services
[static-ip]: ../articles/virtual-network/virtual-networks-reserved-public-ip.md
[storage-account-limits]: ../articles/azure-subscription-service-limits.md#storage-limits
[storage-price]: https://azure.microsoft.com/pricing/details/storage/
[Uso del Centro de seguridad]: ../articles/security-center/security-center-get-started.md#use-security-center
[virtual-machine-sizes]: ../articles/virtual-machines/windows/sizes.md
[visio-download]: http://download.microsoft.com/download/1/5/6/1569703C-0A82-4A9C-8334-F13D0DF2F472/RAs.vsdx
[vm-disk-limits]: ../articles/azure-subscription-service-limits.md#virtual-machine-disk-limits
[vm-resize]:../articles/virtual-machines/linux/change-vm-size.md
[vm-sla]: https://azure.microsoft.com/support/legal/sla/virtual-machines
[vm-size-tables]: ../articles/virtual-machines/windows/sizes.md
[0]: ./media/guidance-blueprints/compute-single-vm.png "Arquitectura de una única máquina virtual Windows en Azure"
[readme]: https://github.com/mspnp/reference-architectures/blob/master/guidance-compute-single-vm
[blocks]: https://github.com/mspnp/template-building-blocks
