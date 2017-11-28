<!--author=SharS last changed: 12/01/15-->

#### <a name="to-enter-maintenance-mode"></a><span data-ttu-id="c0ce2-101">Para acceder al modo de mantenimiento</span><span class="sxs-lookup"><span data-stu-id="c0ce2-101">To enter Maintenance mode</span></span>
1. <span data-ttu-id="c0ce2-102">En el menú de la consola serie, seleccione la opción 1, **Iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-102">In the serial console menu, choose option 1, **Log in with full access**.</span></span>
2. <span data-ttu-id="c0ce2-103">Escriba la contraseña.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-103">Type the password.</span></span> <span data-ttu-id="c0ce2-104">La contraseña predeterminada es **Password1**.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-104">The default password is **Password1**.</span></span>
3. <span data-ttu-id="c0ce2-105">En el símbolo del sistema, escriba</span><span class="sxs-lookup"><span data-stu-id="c0ce2-105">At the command prompt, type</span></span>
   
     `Enter-HcsMaintenanceMode`
4. <span data-ttu-id="c0ce2-106">Verá un mensaje de advertencia que indica que el modo de mantenimiento interrumpe todas las solicitudes de E/S y detiene la conexión al Portal de Azure clásico. También se le solicitará la confirmación.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-106">You will see a warning message telling you that Maintenance mode will disrupt all I/O requests and sever the connection to the Azure classic portal, and you will be prompted for confirmation.</span></span> <span data-ttu-id="c0ce2-107">Escriba **Y** para acceder al modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-107">Type **Y** to enter Maintenance mode.</span></span>
   
    <span data-ttu-id="c0ce2-108">Ambos controladores se reiniciarán.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-108">Both controllers will restart.</span></span> <span data-ttu-id="c0ce2-109">Una vez completado el reinicio, aparecerá otro mensaje que indica que el dispositivo está en modo de mantenimiento.</span><span class="sxs-lookup"><span data-stu-id="c0ce2-109">When the restart is complete, another message will appear indicating that the device is in Maintenance mode.</span></span>

