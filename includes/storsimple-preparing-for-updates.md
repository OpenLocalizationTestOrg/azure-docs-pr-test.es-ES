<!--author=jgerend last changed: 03/16/16-->

## <a name="preparing-for-updates"></a><span data-ttu-id="26ffe-101">Preparación de las actualizaciones</span><span class="sxs-lookup"><span data-stu-id="26ffe-101">Preparing for updates</span></span>
<span data-ttu-id="26ffe-102">Necesitará hello tooperform siguiendo los pasos antes de examinar y aplique la actualización de hello:</span><span class="sxs-lookup"><span data-stu-id="26ffe-102">You will need tooperform hello following steps before you scan and apply hello update:</span></span>

1. <span data-ttu-id="26ffe-103">Tome una instantánea de nube de los datos del dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="26ffe-103">Take a cloud snapshot of hello device data.</span></span>
2. <span data-ttu-id="26ffe-104">Asegúrese de que la IP fijas del controlador sean enrutable y pueden conectarse toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="26ffe-104">Ensure that your controller fixed IPs are routable and can connect toohello Internet.</span></span> <span data-ttu-id="26ffe-105">IP fijas serán tooyour dispositivo de tooservice usa las actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="26ffe-105">These fixed IPs will be used tooservice updates tooyour device.</span></span> <span data-ttu-id="26ffe-106">Puede probarlo mediante la ejecución de hello siguientes cmdlet en cada controlador de interfaz de Windows PowerShell de hello de dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="26ffe-106">You can test this by running hello following cmdlet on each controller from hello Windows PowerShell interface of hello device:</span></span>
   
     `Test-Connection -Source <Fixed IP of your device controller> -Destination <Any IP or computer name outside of datacenter network> `
   
    <span data-ttu-id="26ffe-107">**Resultados de ejemplo para la conexión de prueba cuando IP fijas puedan conectarse toohello Internet**</span><span class="sxs-lookup"><span data-stu-id="26ffe-107">**Sample output for Test-Connection when fixed IPs can connect toohello Internet**</span></span>

        Controller0>Test-Connection -Source 10.126.173.91 -Destination bing.com

        Source      Destination     IPV4Address      IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200
        HCSNODE0  bing.com        204.79.197.200

        Controller0>Test-Connection -Source 10.126.173.91 -Destination  204.79.197.200

        Source      Destination       IPV4Address    IPV6Address
        ----------------- -----------  -----------
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200
        HCSNODE0  204.79.197.200  204.79.197.200

<span data-ttu-id="26ffe-108">Después de haber completado correctamente estas comprobaciones previas manuales, puede continuar tooscan e instalar actualizaciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="26ffe-108">After you have successfully completed these manual pre-checks, you can proceed tooscan and install hello updates.</span></span>

