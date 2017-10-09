Puede comprobar que la conexión se realizó correctamente mediante el cmdlet de hello 'Get-AzureVNetConnection'.

1. Hola de uso siguiente cmdlet de ejemplo, la configuración de hello valores toomatch sus propios. nombre de Hola de red virtual de hello debe estar entre comillas si contiene espacios.

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. Cuando haya finalizado el cmdlet de hello, ver los valores de hello. En el ejemplo de Hola a continuación, muestra el estado de conectividad de hello como 'Conectado' y puede ver los bytes de entrada y salida.

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal