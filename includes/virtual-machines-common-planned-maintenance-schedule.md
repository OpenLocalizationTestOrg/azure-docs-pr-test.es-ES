

## <a name="multi-and-single-instance-vms"></a>Máquinas virtuales de instancia única o instancias múltiples
Muchos clientes que se ejecutan en el recuento de Azure se críticas que puede programar cuándo sus máquinas virtuales se someten a mantenimiento planeado debido a un tiempo de inactividad de toohello--unos 15 minutos, que se produce durante el mantenimiento. Puede utilizar control de toohelp de conjuntos de disponibilidad al mantenimiento planificado de recepción de máquinas virtuales aprovisionadas.

Hay dos configuraciones posibles para las máquinas virtuales que se ejecutan en Azure. Las máquinas virtuales se pueden configurar como instancia única o instancias múltiples. Si las máquinas virtuales están en un conjunto de disponibilidad, se configuran como instancias múltiples. Tenga en cuenta que incluso las máquinas virtuales únicas se pueden implementar en un conjunto de disponibilidad, que se tratarán como instancias múltiples. Si las máquinas virtuales NO están en un conjunto de disponibilidad, se configurarán como una instancia única.  Para obtener información detallada sobre los conjuntos de disponibilidad, consulte [Hola de administrar la disponibilidad de las máquinas virtuales de Windows](../articles/virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Hola de administrar la disponibilidad de las máquinas virtuales de Linux](../articles/virtual-machines/linux/manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Mantenimiento planeado actualiza la instancia de toosingle y máquinas virtuales de varias instancias se realizará por separado. Al volver a configurar su máquinas virtuales toobe de instancia única (si son varias instancias) o toobe varias instancias (si están instancia única), puede controlar cuando sus máquinas virtuales reciben mantenimiento planificado de Hola. Consulte [Mantenimiento planeado de máquinas virtuales Linux en Azure](../articles/virtual-machines/linux/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) o [Mantenimiento planeado de máquinas virtuales Windows en Azure](../articles/virtual-machines/windows/planned-maintenance.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para más detalles sobre el mantenimiento planeado de máquinas virtuales de Azure.

## <a name="for-multi-instance-configuration"></a>Para la configuración de instancias múltiples
Puede seleccionar tiempo Hola mantenimiento planificado afecta a las máquinas virtuales que se implementan en una configuración de conjunto de disponibilidad mediante la eliminación de estas máquinas virtuales de conjuntos de disponibilidad.

1. Envía un correo electrónico es tooyou siete días antes de hello planeada mantenimiento tooyour máquinas virtuales en una configuración de varias instancias. Hola identificadores de suscripción y nombres de máquinas virtuales de varias instancias de hello afectado se incluyen en el cuerpo Hola de correo electrónico de Hola.
2. Durante los siete días, puede elegir el tiempo de hello las instancias se actualizan mediante la eliminación de las máquinas virtuales de varias instancias en dicha región de su conjunto de disponibilidad. Este cambio en un reinicio, como Hola Máquina Virtual se traslada de un host físico, se producirá configuración destinada para el mantenimiento, tooanother host físico que no está destinada para el mantenimiento.
3. Puede quitar Hola VM de su conjunto de disponibilidad en hello portal de Azure.

   1. En el portal de hello, seleccione Hola VM tooremove de Hola conjunto de disponibilidad.  

   2. En **Configuración**, haga clic en **Conjunto de disponibilidad**.

      ![Selección del conjunto de disponibilidad](./media/virtual-machines-planned-maintenance-schedule/availabilitysetselection.png)

   3. En la disponibilidad de hello, establezca el menú desplegable, seleccione "No forma parte de un conjunto de disponibilidad."

      ![Eliminación del conjunto](./media/virtual-machines-planned-maintenance-schedule/availabilitysetwarning.png)

   4. En la parte superior de hello, haga clic en **guardar**. Haga clic en **Sí** tooacknowledge que esta acción reinicia Hola máquina virtual.

   >[!TIP]
   >Puede volver a configurar hello toomulti-instancia de VM más adelante seleccionando uno de los conjuntos de disponibilidad de hello enumerado.

4. Quitado de conjuntos de disponibilidad de las máquinas virtuales son hosts de instancia de tooSingle ha movido y no se actualizan durante Hola planeada mantenimiento tooAvailability establecer configuraciones.
5. Una vez completada la Hola actualización tooAvailability establecido, las máquinas virtuales (según tooschedule que se describen en el correo electrónico original de hello), debe agregar máquinas virtuales de hello en sus conjuntos de disponibilidad. Pase a ser parte de un conjunto de disponibilidad vuelve a configurar las máquinas virtuales de hello como varias instancias y da como resultado un reinicio. Normalmente, una vez completadas todas las actualizaciones de varias instancias a través de todo el entorno Azure hello, sigue el mantenimiento de instancia única.

También puede lograrse la eliminación de una máquina virtual de un conjunto de disponibilidad mediante Azure PowerShell:

```
Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Remove-AzureAvailabilitySet | Update-AzureVM
```

## <a name="for-single-instance-configuration"></a>Para la configuración de una instancia única
Puede seleccionar tiempo Hola mantenimiento planificado afecta a las máquinas virtuales en una configuración de instancia única mediante la adición de estas máquinas virtuales en conjuntos de disponibilidad.

Paso a paso

1. Envía un correo electrónico es tooyou siete días antes de hello planeada tooVMs de mantenimiento en una configuración de instancia única. Hola suscripción identificadores y nombres de máquinas virtuales de instancia única de hello afectado se incluyen en el cuerpo de saludo de correo electrónico de Hola.
2. Durante los siete días, puede elegir tiempo Hola su instancia reinicios mediante la adición de la disponibilidad de las máquinas virtuales de instancia única tooan establecido en esa misma región. Este cambio en un reinicio, como Hola Máquina Virtual se traslada de un host físico, se producirá configuración destinada para el mantenimiento, tooanother host físico que no está destinada para el mantenimiento.
3. Siga las instrucciones aquí tooadd existente de las máquinas virtuales en conjuntos de disponibilidad mediante hello portal de Azure y Azure PowerShell. (Consulte el ejemplo de Hola a Azure PowerShell que sigue estos pasos.)
4. Una vez que estas máquinas virtuales se vuelven a configurar como varias instancias, se excluyen de mantenimiento planificado de hello tooSingle instancia las máquinas virtuales.
5. Cuando haya completado la actualización de VM de instancia única de Hola (según tooschedule en correo electrónico original de hello), puede devolver las máquinas virtuales de hello toosingle-instancia mediante la eliminación de las máquinas virtuales de Hola de sus conjuntos de disponibilidad.

Agregar un tooan VM también conjunto de disponibilidad puede lograrse mediante PowerShell de Azure:

    Get-AzureVM -ServiceName "<VmCloudServiceName>" -Name "<VmName>" | Set-AzureAvailabilitySet -AvailabilitySetName "<AvSetName>" | Update-AzureVM

<!--Anchors-->



<!--Link references-->
[Virtual Machines Manage Availability]: virtual-machines-windows-tutorial.md
[Understand planned versus unplanned maintenance]: virtual-machines-manage-availability.md#Understand-planned-versus-unplanned-maintenance/
