# Backup-Restore-MSSQL-and-MSAS-DBs-to-from-Azure-Blob
Here we show you how to backup their PaaS MSSQL 2012 DB as well as their MSAS (Analysis Server) tabular DB (aka workspace DB) into Azure blob. We looked around and found:
• MSSQL
o You can back up a db to blob through
 GUI, T-SQL, Powershell
o All these three methods actually use objects Microsoft.SqlServer.Management.Smo.Server and Microsoft.SqlServer.Management.Smo.Backup, which allow you set up URL and credential.

• MSAS
o You can back up a workspace db (where all tabular models live) locally through
 GUI, Powershell
o All these two methods actually use objects Microsoft.AnalysisServices.Server and Microsoft.AnalysisServices.BackupInfo, which not allow you set up URL (only file or disk)
o However once a workspace db backed up locally with overwrite allowed option, one can copy it to Azure blob with cmdlet Set-AzureStorageBlobContent. Actually one piece of Powershell (*.ps1) can back up a Analysis Server workspace db to a single *.abf file and then copy this file to Azure blob.

We developed a Powershell script and attached here for sharing.

For restoring DB, SSMS provides the GUI for both MSSQL and MSAS. The task for us thus reduces to how to retrieve the backed up files (*.bak for MSSQL and *.abf for MSAS) from Azure Blob to the VM. We found AZCopy is a good tool for this purpose. Our steps are documented and attached here for sharing.
