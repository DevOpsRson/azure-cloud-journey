### Step 1: Theory & Context (60 Mins)

# Topic: Azure Resource Hierarchy, Control Plane & Authentication Model.


    The Hierarchy:  Management Groups -> Subscriptions -> Resource Groups -> Resources.

    Control Plane vs. Data Plane:
    
    Control Plane (Azure Resource Manager / ARM): The management layer used to create, update, and delete resources, or assign permissions.
    Data Plane: The actual function of the resource (e.g., querying data inside a SQL database or executing code on a VM).
    
    Authentication & Access Model
    
    This establishes identity and permissions applied to that hierarchy.
    Authentication (Entra ID / Microsoft Entra): Verifying who you are (users, service principals, managed identities).
    Authorization (RBAC & Azure Policy): Verifying what you can do.
    Azure RBAC: Grants permissions (e.g., Contributor, Reader) applied at a specific level of the resource hierarchy. Permissions trickle down (Management Group $\rightarrow$ Subscription $\rightarrow$ Resource Group $\rightarrow$ Resource).
    Azure Policy: Enforces rules and standards across your hierarchy (e.g., "No public IP addresses allowed in this Resource Group").

### Step 2: Hands-on Execution (120 Mins)


    1. Install Azure CLI on your local terminal
    2. Authenticate using 
        Bash
        az login
    3. Verify Subscription Details
        Bash
        az account show --output table


    4. Create Your Day 1 Resource Group
        We will create a dedicated Resource Group in the westeurope
        region to host all your practice deployments for this week.

            az group create \
        --name rg-cloud-roadmap-dev-001 \
        --location westeurope \
        --tags Environment=Dev Project=CloudRoadmap Owner=Engineer

    OR
        
        # Set variables
        RG_NAME="rg-azure-roadmap-dev-001"
        LOCATION="westeurope"

        # Create the Resource Group
        az group create --name $RG_NAME --location $LOCATION --output 
        table


    5. Verify Resource Group Creation

        az group show \
        --name rg-cloud-roadmap-dev-001 \
        --query "{Name:name, Location:location, Status:properties.provisioningState}" \
        --output table

    OR 

        Query Azure Resource Manager (ARM) to confirm the resource group is active:
        az group show --name $RG_NAME --output table

    6. Intentional Error & Debug Test:
    Run an invalid command intentionally to inspect how Azure Resource Manager (ARM) returns API error codes:

        az group show --name rg-does-not-exist

    7. Resource Teardown Drill (End-of-Session Protocol):
    (Run this at the end of your 4-hour session to keep costs at €0):

        az group delete --name rg-cloud-roadmap-dev-001 --yes --no-wait

# Step 3: Portfolio & Articulation (60 Mins) / Daily Knowledge Check & Core Takeaways

    A.  GitHub Commit:
        
    Create a file named day01_resource_groups.sh in VS Code containing the scripts above, commit it, and push it to your azure-cloud-journey repository.

    B.  The 3-Minute Elevator Pitch:

    Stand up, set a 3-minute timer on your phone, and deliver this out loud to an empty room:

     "What is the architectural difference between a Subscription and a Resource Group in Azure?"

    "Why do enterprise platforms enforce strict resource group naming conventions and tagging strategies?"

    "How does the Azure CLI communicate with the Azure Resource Manager (ARM) REST API under the hood?"

# NOTE: End-of-Day Reporting Protocol
Once you complete your 4-hour session, post your Day 1 Standup Report here:

    What got built: (Paste the link to your GitHub commit or CLI output)

    Where you got stuck: (Any error messages or CLI friction you encountered)

    Speech Summary: (Write 3 sentences summarizing how you answered the presentation prompt out loud)
