Puede conectarse tooa máquina virtual que está implementado tooyour red virtual mediante la creación de una máquina virtual tooyour de conexión a Escritorio remoto. Hello tooinitially de mejor manera comprueba que puedes conectarte tooyour VM es tooconnect por utilizar IP privadas de su dirección, en lugar del nombre del equipo. De este modo, se prueban por toosee si puede conectarse, no si la resolución de nombres está configurada correctamente.

1. Busque la dirección IP privada de Hola. Puede encontrar la dirección IP privada de Hola de una máquina virtual de varias maneras. A continuación, se muestran los pasos de Hola Hola portal de Azure y PowerShell.

  - Portal de Azure: ubicar la máquina virtual en hello portal de Azure. Ver las propiedades de Hola de hello máquina virtual. se muestra la dirección IP privada de Hola.

  - PowerShell - tooview de ejemplo de Hola utilice una lista de las máquinas virtuales y las direcciones IP privadas de los grupos de recursos. No es necesario toomodify en este ejemplo antes de usarlo.

    ```powershell
    $VMs = Get-AzureRmVM
    $Nics = Get-AzureRmNetworkInterface | Where VirtualMachine -ne $null

    foreach($Nic in $Nics)
    {
      $VM = $VMs | Where-Object -Property Id -eq $Nic.VirtualMachine.Id
      $Prv = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAddress
      $Alloc = $Nic.IpConfigurations | Select-Object -ExpandProperty PrivateIpAllocationMethod
      Write-Output "$($VM.Name): $Prv,$Alloc"
    }
    ```

2. Compruebe que está conectado tooyour red virtual mediante la conexión VPN de Hola.
3. Abra **conexión a Escritorio remoto** escribiendo "RDP" o "Conexión a Escritorio remoto" en el cuadro de búsqueda de hello en la barra de tareas de hello, a continuación, seleccione conexión a Escritorio remoto. También puede abrir conexión a Escritorio remoto mediante el comando de 'mstsc' hello en PowerShell. 
4. En conexión a Escritorio remoto, escriba la dirección IP privada de Hola de hello VM. Puede haga clic en "Mostrar opciones" tooadjust adicionales configuración y luego conectarse.

### <a name="tootroubleshoot-an-rdp-connection-tooa-vm"></a>tootroubleshoot una tooa de conexión RDP VM

Si tiene problemas para conectarse a máquina virtual de tooa a través de la conexión VPN, compruebe Hola siguiente:

- Compruebe que la conexión VPN se ha establecido correctamente.
- Compruebe que se está conectando toohello dirección IP privada Hola máquina virtual.
- Si se puede conectar toohello VM con IP privada Hola de direcciones, pero no Hola nombre de equipo, compruebe que ha configurado DNS correctamente. Para más información acerca de cómo funciona la resolución de nombres para las máquinas virtuales, consulte [Resolución de nombres para las máquinas virtuales e instancias de rol](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).
- Para obtener más información acerca de las conexiones RDP, consulte [tooa de conexiones de escritorio remoto solucionar VM](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).
