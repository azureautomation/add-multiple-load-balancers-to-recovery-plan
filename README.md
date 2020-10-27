Add multiple load balancers to recovery plan
============================================

            

    .DESCRIPTION         This runbook will attach an existing load balancer to the vNics of the virtual machines, in the Recovery Plan during failover.                 
 This will create a Public IP address for the failed over VM(s).                 


Pre-requisites        


All resources involved are based on Azure Resource Manager (NOT Azure Classic)


- A Load Balancer(s) with a backend pool       


- A complex Automation Variable, containing the VMGUID for each VM, ResourceGroupName for the Load Balancer(s) and the Load Balancer(s) name.        Example:               


$RPdetails = @{'6949b3a9-ae82-5e90-882c-30e48dffdcd8'=@{'ResourceGroupName'='knlb';'LBName'='knextlb'};'6dce5d61-2416-546c-9bcd-c1bc79a5a678'=@{'ResourceGroupName'='knlb';'LBName'='knintlb'}}
        $myASRobject = New-Object -TypeName PSObject -Property $RPdetails
        $ASRVariable = $myASRobject | ConvertTo-Json


New-AzureRmAutomationVariable -Name <recoveryPlanName> -ResourceGroupName <automationResourceGroup> -AutomationAccountName <automationAccountName> -Value $ASRVariable -Encrypted $false 




 
The following AzureRm Modules are required        - AzureRm.Profile        - AzureRm.Resources        - AzureRm.Compute        - AzureRm.Network           
                How to add the script?         Add this script as a post action in boot up group where you need to associate the VMs with the existing Load Balancer       
         




        
    
TechNet gallery is retiring! This script was migrated from TechNet script center to GitHub by Microsoft Azure Automation product group. All the Script Center fields like Rating, RatingCount and DownloadCount have been carried over to Github as-is for the migrated scripts only. Note : The Script Center fields will not be applicable for the new repositories created in Github & hence those fields will not show up for new Github repositories.
