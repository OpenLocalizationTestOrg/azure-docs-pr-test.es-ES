<!--author=SharS last changed: 9/17/15-->

#### <a name="to-install-regular-hotfixes-via-windows-powershell-for-storsimple"></a><span data-ttu-id="b05f6-101">Para instalar revisiones regulares a través de Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="b05f6-101">To install regular hotfixes via Windows PowerShell for StorSimple</span></span>
1. <span data-ttu-id="b05f6-102">Conéctese a la consola serie del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="b05f6-102">Connect to the device serial console.</span></span> <span data-ttu-id="b05f6-103">Para más información, consulte [Paso 1: Conexión a la consola serie](../articles/storsimple/storsimple-update-device.md#step1).</span><span class="sxs-lookup"><span data-stu-id="b05f6-103">For more information, see [Step 1: Connect to the serial console](../articles/storsimple/storsimple-update-device.md#step1).</span></span>
2. <span data-ttu-id="b05f6-104">En el menú de la consola serie, seleccione la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="b05f6-104">In the serial console menu, select option 1, **Log in with full access**.</span></span> <span data-ttu-id="b05f6-105">Escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="b05f6-105">Type the password.</span></span> <span data-ttu-id="b05f6-106">La contraseña predeterminada es **Password1**.</span><span class="sxs-lookup"><span data-stu-id="b05f6-106">The default password is **Password1**.</span></span>
3. <span data-ttu-id="b05f6-107">En el símbolo del sistema, escriba:</span><span class="sxs-lookup"><span data-stu-id="b05f6-107">At the command prompt, type:</span></span>
   
    ```
    Start-HcsHotfix
    ```
   
    > [!IMPORTANT]
    >
    > <span data-ttu-id="b05f6-108">Este comando solo se aplica a las revisiones regulares.</span><span class="sxs-lookup"><span data-stu-id="b05f6-108">This command applies only to regular hotfixes.</span></span> <span data-ttu-id="b05f6-109">Este comando se ejecuta en un solo controlador, pero se actualizarán ambos controladores.</span><span class="sxs-lookup"><span data-stu-id="b05f6-109">You run this command on only one controller, but both controllers will be updated.</span></span>
    > <span data-ttu-id="b05f6-110">Es posible que observe una conmutación por error del controlador durante el proceso de actualización. Sin embargo, la conmutación por error no afectará a la disponibilidad o el funcionamiento del sistema.</span><span class="sxs-lookup"><span data-stu-id="b05f6-110">You may notice a controller failover during the update process; however, the failover will not affect system availability or operation.</span></span>

4. <span data-ttu-id="b05f6-111">Cuando se le solicite, proporcione la ruta de acceso a la carpeta compartida de red que contiene los archivos de la revisión.</span><span class="sxs-lookup"><span data-stu-id="b05f6-111">When prompted, supply the path to the network shared folder that contains the hotfix files.</span></span>
5. <span data-ttu-id="b05f6-112">Se le pedirá confirmación.</span><span class="sxs-lookup"><span data-stu-id="b05f6-112">You will be prompted for confirmation.</span></span> <span data-ttu-id="b05f6-113">Escriba **Y** para continuar con la instalación de la revisión.</span><span class="sxs-lookup"><span data-stu-id="b05f6-113">Type **Y** to proceed with the hotfix installation.</span></span>

