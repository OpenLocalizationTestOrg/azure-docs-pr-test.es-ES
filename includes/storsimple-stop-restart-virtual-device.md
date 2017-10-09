#### <a name="toostop-and-start-a-virtual-device"></a>toostop e inicie un dispositivo virtual
toostop un dispositivo virtual, haga clic en su nombre y, a continuación, haga clic en **apagado**. Mientras se está cerrando el dispositivo virtual hello, su estado es **detener**. Cuando se haya detenido el dispositivo virtual hello, su estado es **detenido**.

Usar hello después cmdlets toostop e iniciar un dispositivo virtual.

`Stop-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

`Start-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

#### <a name="toorestart-a-virtual-device"></a>toorestart un dispositivo virtual
Cuando se ejecuta un dispositivo virtual y desea toorestart, haga clic en su nombre y, a continuación, haga clic en **reiniciar**. Mientras se está reiniciando el dispositivo virtual hello, su estado es **reiniciando**. Cuando esté listo para toouse dispositivo virtual hello, su estado es **ejecutando**.

Usar hello siguiente cmdlet toorestart un dispositivo virtual.

`Restart-AzureVM -ServiceName "MyStorSimpleservice1" -Name "MyStorSimpleDevice"`

