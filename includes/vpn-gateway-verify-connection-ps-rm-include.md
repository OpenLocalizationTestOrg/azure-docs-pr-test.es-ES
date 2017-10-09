<span data-ttu-id="f8d26-101">Puede comprobar que la conexión se realizó correctamente utilizando el cmdlet de hello 'Get-AzureRmVirtualNetworkGatewayConnection', con o sin '-Debug'.</span><span class="sxs-lookup"><span data-stu-id="f8d26-101">You can verify that your connection succeeded by using hello 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="f8d26-102">Hola de uso siguiente cmdlet de ejemplo, la configuración de hello valores toomatch sus propios.</span><span class="sxs-lookup"><span data-stu-id="f8d26-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="f8d26-103">Si se le solicita, seleccione 'A' en orden toorun 'All'.</span><span class="sxs-lookup"><span data-stu-id="f8d26-103">If prompted, select 'A' in order toorun 'All'.</span></span> <span data-ttu-id="f8d26-104">En el ejemplo de Hola, '-Name' hace referencia toohello nombre de conexión de Hola que desea tootest.</span><span class="sxs-lookup"><span data-stu-id="f8d26-104">In hello example, '-Name' refers toohello name of hello connection that you want tootest.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="f8d26-105">Cuando haya finalizado el cmdlet de hello, ver los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="f8d26-105">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="f8d26-106">En el siguiente ejemplo de Hola, estado de la conexión de hello muestra como "Conectado" y se pueden ver los bytes de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="f8d26-106">In hello example below, hello connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```