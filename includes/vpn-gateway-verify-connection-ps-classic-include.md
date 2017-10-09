<span data-ttu-id="6663c-101">Puede comprobar que la conexión se realizó correctamente mediante el cmdlet de hello 'Get-AzureVNetConnection'.</span><span class="sxs-lookup"><span data-stu-id="6663c-101">You can verify that your connection succeeded by using hello 'Get-AzureVNetConnection' cmdlet.</span></span>

1. <span data-ttu-id="6663c-102">Hola de uso siguiente cmdlet de ejemplo, la configuración de hello valores toomatch sus propios.</span><span class="sxs-lookup"><span data-stu-id="6663c-102">Use hello following cmdlet example, configuring hello values toomatch your own.</span></span> <span data-ttu-id="6663c-103">nombre de Hola de red virtual de hello debe estar entre comillas si contiene espacios.</span><span class="sxs-lookup"><span data-stu-id="6663c-103">hello name of hello virtual network must be in quotes if it contains spaces.</span></span>

  ```powershell
  Get-AzureVNetConnection "Group ClassicRG ClassicVNet"
  ```
2. <span data-ttu-id="6663c-104">Cuando haya finalizado el cmdlet de hello, ver los valores de hello.</span><span class="sxs-lookup"><span data-stu-id="6663c-104">After hello cmdlet has finished, view hello values.</span></span> <span data-ttu-id="6663c-105">En el ejemplo de Hola a continuación, muestra el estado de conectividad de hello como 'Conectado' y puede ver los bytes de entrada y salida.</span><span class="sxs-lookup"><span data-stu-id="6663c-105">In hello example below, hello Connectivity State shows as 'Connected' and you can see ingress and egress bytes.</span></span>

        ConnectivityState         : Connected
        EgressBytesTransferred    : 181664
        IngressBytesTransferred   : 182080
        LastConnectionEstablished : 1/7/2016 12:40:54 AM
        LastEventID               : 24401
        LastEventMessage          : hello connectivity state for hello local network site 'RMVNetLocal' changed from Connecting to
                                    Connected.
        LastEventTimeStamp        : 1/7/2016 12:40:54 AM
        LocalNetworkSiteName      : RMVNetLocal