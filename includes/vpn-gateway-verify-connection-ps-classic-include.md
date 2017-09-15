<span data-ttu-id="41d84-101">Puede comprobar que la conexión se realizó correctamente mediante el cmdlet "Get-AzureVNetConnection".</span><span class="sxs-lookup"><span data-stu-id="41d84-101">You can verify that your connection succeeded by using the 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="41d84-102">Puede usar el siguiente ejemplo de cmdlet, configurando los valores para que coincidan con los tuyos.</span><span class="sxs-lookup"><span data-stu-id="41d84-102">Use the following cmdlet example, configuring the values to match your own.</span></span> <span data-ttu-id="41d84-103">Si el nombre de la red virtual contiene espacios, debe estar entre comillas.</span><span class="sxs-lookup"><span data-stu-id="41d84-103">The name of the virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="41d84-104">Cuando el cmdlet haya finalizado, consulte los valores.</span><span class="sxs-lookup"><span data-stu-id="41d84-104">After the cmdlet has finished, view the values.</span></span> <span data-ttu-id="41d84-105">En el ejemplo siguiente, en ConnectivityState aparece "Connected" y se pueden ver los bytes de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="41d84-105">In the example below, the Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : The connectivity state for the local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal