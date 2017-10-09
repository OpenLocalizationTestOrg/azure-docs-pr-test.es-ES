
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, hello following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="a9eb7-101">los costos de toosave, puede pausar y reanudar proceso recursos a petición.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-101">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="a9eb7-102">Por ejemplo, si no va a usar base de datos de Hola durante la noche de Hola y fines de semana, puede pausar en esos momentos y reanudar durante el día de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-102">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="a9eb7-103">Que no cobra por a Dwu mientras la base de datos de hello está detenida.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-103">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="a9eb7-104">Al pausar una base de datos:</span><span class="sxs-lookup"><span data-stu-id="a9eb7-104">When you pause a database:</span></span>

* <span data-ttu-id="a9eb7-105">Recursos de proceso y memoria se devuelven toohello grupo de recursos disponibles en el centro de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="a9eb7-105">Compute and memory resources are returned toohello pool of available resources in hello data center</span></span>
* <span data-ttu-id="a9eb7-106">Los costos DWU son cero durante Hola de pausa de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-106">DWU costs are zero for hello duration of hello pause.</span></span>
* <span data-ttu-id="a9eb7-107">El almacenamiento de datos no se ve afectado y sus datos permanecen intactos.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="a9eb7-108">Almacenamiento de datos SQL cancela todas las operaciones de ejecución o en cola.</span><span class="sxs-lookup"><span data-stu-id="a9eb7-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

