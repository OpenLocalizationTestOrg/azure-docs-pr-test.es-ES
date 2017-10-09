Puede comprobar que la conexión se realizó correctamente utilizando el cmdlet de hello 'Get-AzureRmVirtualNetworkGatewayConnection', con o sin '-Debug'. 

1. Hola de uso siguiente cmdlet de ejemplo, la configuración de hello valores toomatch sus propios. Si se le solicita, seleccione 'A' en orden toorun 'All'. En el ejemplo de Hola, '-Name' hace referencia toohello nombre de conexión de Hola que desea tootest.

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. Cuando haya finalizado el cmdlet de hello, ver los valores de hello. En el siguiente ejemplo de Hola, estado de la conexión de hello muestra como "Conectado" y se pueden ver los bytes de entrada y salida.
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```