<span data-ttu-id="4df2e-101">Puede comprobar que la conexión se realizó correctamente mediante el uso del cmdlet "Get-AzureRmVirtualNetworkGatewayConnection", con o sin "-Debug".</span><span class="sxs-lookup"><span data-stu-id="4df2e-101">You can verify that your connection succeeded by using the 'Get-AzureRmVirtualNetworkGatewayConnection' cmdlet, with or without '-Debug'.</span></span> 

1. <span data-ttu-id="4df2e-102">Puede usar el siguiente ejemplo de cmdlet, configurando los valores para que coincidan con los tuyos.</span><span class="sxs-lookup"><span data-stu-id="4df2e-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="4df2e-103">Cuando se le pida, seleccione "A" para ejecutar "todo".</span><span class="sxs-lookup"><span data-stu-id="4df2e-103">If prompted, select 'A' in order to run 'All'.</span></span> <span data-ttu-id="4df2e-104">En el ejemplo, " -Name" hace referencia al nombre de la conexión que desea probar.</span><span class="sxs-lookup"><span data-stu-id="4df2e-104">In the example, '-Name' refers to the name of the connection that you want to test.</span></span>

  ```powershell
  Get-AzureRmVirtualNetworkGatewayConnection -Name MyGWConnection -ResourceGroupName MyRG
  ```
2. <span data-ttu-id="4df2e-105">Cuando el cmdlet haya finalizado, consulte los valores.</span><span class="sxs-lookup"><span data-stu-id="4df2e-105">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="4df2e-106">En el ejemplo siguiente, el estado de conexión aparece como "Conectado" y pueden verse los bytes de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="4df2e-106">In the example below, the connection status shows as 'Connected' and you can see ingress and egress bytes.</span></span>
   
  ```
  "connectionStatus": "Connected",
  "ingressBytesTransferred": 33509044,
  "egressBytesTransferred": 4142431
  ```