
<!--
includes/sql-data-warehouse-include-pause-description.md

Latest Freshness check:  2016-04-22 , barbkess.

As of circa 2016-04-22, the following topics might include this include:
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-powershell.md
articles/sql-data-warehouse/sql-data-warehouse-manage-scale-out-tasks-rest-api.md

-->
<span data-ttu-id="42bbc-101">Para ahorrar costos, puede pausar y reanudar recursos de proceso a petición.</span><span class="sxs-lookup"><span data-stu-id="42bbc-101">To save costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="42bbc-102">Por ejemplo, si no va a usar la base de datos durante la noche y los fines de semana, puede pausarla durante esas horas y reanudarla durante el día.</span><span class="sxs-lookup"><span data-stu-id="42bbc-102">For example, if you won't be using the database during the night and on weekends, you can pause it during those times, and resume it during the day.</span></span> <span data-ttu-id="42bbc-103">No se le cobrará por DWU mientras la base de datos se encuentre en pausa.</span><span class="sxs-lookup"><span data-stu-id="42bbc-103">You won't be charged for DWUs while the database is paused.</span></span>

<span data-ttu-id="42bbc-104">Al pausar una base de datos:</span><span class="sxs-lookup"><span data-stu-id="42bbc-104">When you pause a database:</span></span>

* <span data-ttu-id="42bbc-105">Los recursos de memoria y proceso se devuelven al grupo de recursos disponibles en el centro de datos</span><span class="sxs-lookup"><span data-stu-id="42bbc-105">Compute and memory resources are returned to the pool of available resources in the data center</span></span>
* <span data-ttu-id="42bbc-106">Durante la pausa, DWU no tiene costo alguno.</span><span class="sxs-lookup"><span data-stu-id="42bbc-106">DWU costs are zero for the duration of the pause.</span></span>
* <span data-ttu-id="42bbc-107">El almacenamiento de datos no se ve afectado y sus datos permanecen intactos.</span><span class="sxs-lookup"><span data-stu-id="42bbc-107">Data storage is not affected and your data stays intact.</span></span> 
* <span data-ttu-id="42bbc-108">Almacenamiento de datos SQL cancela todas las operaciones de ejecución o en cola.</span><span class="sxs-lookup"><span data-stu-id="42bbc-108">SQL Data Warehouse cancels all running or queued operations.</span></span>

