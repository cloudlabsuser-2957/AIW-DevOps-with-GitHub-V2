# Lab 1: Continuous Integration and Continuous Deployment with GitHub Actions

### Estimated Duration: 140 Minutes

## Overview

In this lab, you are going to set up the local infrastructure using .NET. There are three parts of the application you will be working with: carts, products, and ui. You will deploy the infrastructure to the cloud using GitHub Actions. You will also build automation in GitHub for updating and republishing our workflows when the code changes.

## Objectives

You will be able to complete the following tasks:

- Task 1: Access the lab files
- Task 2: Set up Local Infrastructure
- Task 3: Create the Project Repo
- Task 4: Build and push using GitHub Actions
- Task 5: Editing the GitHub Workflow File using Codespace

## Task 1: Access the lab files

In this task, you'll access and explore the code repository of the web app using Visual Studio Code. Visual Studio Code is a cross-platform, lightweight but powerful source code editor.

1. From the VM desktop, double-click on the **Visual Studio Code** desktop icon to open the application.

   ![](media/2dg4.png "New Repository Creation Form")
   
1. In **Visual Studio Code**, go to the **Menu bar (1)**, select **File (2)**, and then click **Open Folder (3)** to open a folder from the file system.

   ![](media/devops1.3.png)

1. In the **Open Folder** tab, navigate to the following path `C:\Workspaces\lab\aiw-devops-with-github-lab-files` **(1)** to open your local GitHub repository and click on **Select Folder (2)**.

   ![](media/ex-1-1.png)
    
1. If you see the prompt asking, Do you trust the authors of the files in this folder?, check the box labeled **Trust the authors of all files in the parent folder lab** **(1)**, then click the **Yes, I trust the authors** button **(2)** to proceed and enable all features for the folder in Visual Studio Code. 

   ![](media/ex-1-2.png)
   
1. You'll see the lab files in Visual Studio Code and explore the code files.

   ![](media/ex_1_g_0.png)

## Task 2: Set up Local Infrastructure

In this task, you will set up the local infrastructure using NET. You'll be working with three Docker images: fabrikam-init, fabrikam-api, and fabrikam-web.
   
1. In **Visual Studio Code**, open a new terminal by clicking on the **Menu bar (1)**, selecting **Terminal (2)**, and then choosing **New Terminal (3)**.

   ![](media/L1T2S1-0501.png "New Repository Creation Form")
   
1. Click on the **Drop-down** **(1)** button next to PowerShell and select **Command Prompt** **(2)**  from the list. A new Command Prompt terminal will be opened.   

   ![](media/L1T2S2-0501.png)
   
1. Navigate to the **Environment (1)** details pane, click on **Service Principal Details (2)**, and copy the following values:

   - **Application ID (Client ID)**
   - **Secret Key (Client Secret)**
   - **Tenant ID (Directory ID)**  
   
      ![](media/L1T2S3-0501.png)
   
1. Update the **Application Id (Client Id)**, **Client Secret**, and **Tenant ID** in the command mentioned below. Run it in the terminal.

   ```pwsh
   az login --service-principal -u <clientId> -p <clientSecret> --tenant <tenantId>
   ```

   ![](media/L1T2S4-0501.png)

   >**Note:** Open Notepad, make the necessary updates to the command, then copy and paste the updated command into the terminal for execution.

1. Run the below-mentioned command to navigate to `ContosoTraders.Api.Products` folder.

   ```pwsh
   cd C:\Workspaces\lab\aiw-devops-with-github-lab-files\src\ContosoTraders.Api.Products
   ```
   
   ![](media/upd-2dgn48.png)   
   
1. Run the below command to set the secret path.

   ```pwsh
   dotnet user-secrets set "KeyVaultEndpoint" "https://contosotraderskv<inject key="DeploymentID" />.vault.azure.net/"
   ```  

   ![](media/upd-2dgn49.png)
   
1. Run the below-mentioned command to build and host the carts locally.

   ```pwsh
   dotnet build && dotnet run --no-build
   ```  

   ![](media/L1T2S7-0501.png) 
   
   >**Note:** Please wait for 2 - 3 minutes for the build to complete.
   
1. Keep the terminal running. Open a new browser tab and try accessing the application using localhost port. You'll be able to see the output similar to the screenshot mentioned below.

   ```pwsh
   https://localhost:62300/swagger
   ```  

   ![](media/ex_1_g_1.png)     
   
   > **Note:** If you are not able to access the application, click on **Advanced** under Your connection isn't private.
       
    ![](media/localhost1.png) 
   
   Then click on **Continue to localhost (unsafe)** to access the application.

      ![](media/localhost2.png)   
   
1. Navigate back to **VS Code** and stop the terminal by typing **Ctrl + C**. Run the below-mentioned command to navigate to `ContosoTraders.Api.Carts` folder. 
  
   ```pwsh
   cd C:\Workspaces\lab\aiw-devops-with-github-lab-files\src\ContosoTraders.Api.Carts
   ```
  
   ![](media/L1T2S9-0501.png)     
   
1. Run the below command to set the secret path.

   ```pwsh
   dotnet user-secrets set "KeyVaultEndpoint" "https://contosotraderskv<inject key="DeploymentID" />.vault.azure.net/
   ```

   ![](media/image101.png)
   
1. Run the below-mentioned command to build and host the carts locally.

   ```pwsh
   dotnet build && dotnet run --no-build
   ```    
  
   ![](media/2dg123.jpg) 
   
   >**Note:** Please wait for 2 - 3 minutes for the build to complete.

2. Once the script starts successfully, keep the terminal running. Do not close it, as the application will be running from this terminal session.

3. In the terminal output, you will see a **localhost URL** with a specific **port** number where the application is hosted.

4. Open a new tab in your web browser and **enter the localhost URL** shown in your terminal.

5. For example, if your application runs on port `62400`, you can access it using:

   https://localhost:62400/swagger

6. If your terminal shows a different port number, simply replace `62400` in the example URL with the port number displayed in your terminal.

7. After opening the URL in your browser, you should see the **application interface** similar to the screenshot shown below.

   ![](media/ex_1_g_2.png)
   
1. Navigate back to **VS Code** and stop the terminal by typing **Ctrl + C**.    
   
1. From the Windows taskbar, search for **Command Prompt** by typing **Command prompt (1)** in the search box, then click on **Command Prompt (2)** from the results to open it.

   ![](media/ex-1-3.png)    
   
1. Run the below-mentioned command to navigate to the `ContosoTraders.Ui.Website` folder. 
  
   ```pwsh
   cd C:\Workspaces\lab\aiw-devops-with-github-lab-files\src\ContosoTraders.Ui.Website
   ```
   ![](media/L1T2S15-0501.png) 
   
1. Run the below-mentioned command to install npm.

   ```pwsh
   npm ci
   ```    
  
   ![](media/2dg124.jpg) 
   
   >**Note:** Please wait until the installation completes. It will take around 10 - 15 minutes when you run npm install for the first time. In case the execution is stuck, please use **Ctrl + C** to stop the execution and retry the step.
   
1. Navigate back to **VS Code**, run the below-mentioned command to navigate to `ContosoTraders.Ui.Website` folder. 
  
   ```pwsh
   cd C:\Workspaces\lab\aiw-devops-with-github-lab-files\src\ContosoTraders.Ui.Website
   ```

1. Now run the following command to run ui of the application. This will automatically open a browser tab where you'll see the complete application running

   ```pwsh
   npm run start
   ```    
  
   ![](media/2dgn156.png) 
   
   >**Note:** It can take 5 - 10 minutes when you execute the command for the first time. You can continue with the next task and check on this step later.   

   > If you get errors such as "react is not recognized" or missing dependencies, reinstall the project packages: `npm ci`

   > If you see a caniuse-lite is outdated warning or error, run: `npx update-browserslist-db@latest`
   
   > After fixing the issue, run the application again: `npm run start`
   
## Task 3: Create the Project Repo

In this task, you'll access the GitHub Enterprise account and create a new repository to store the infrastructure.

1. In a new browser tab, go to `https://www.github.com/login`. and login using GitHub credentials.

1. To find the GitHub credentials, navigate to the **Environment (1)** tab in the lab environment and click on the **Licenses (2)** button. Copy the **GitHub UserEmail and GitHub Password (3)**, then save these credentials in **Notepad**. You will need them later during the GitHub login and device verification steps.

   ![](media/L1T3S2-0501.png)

1. Open a **Private window** in Microsoft Edge by clicking the three-dot menu **(1)** in the top-right and selecting **New InPrivate window (2)**.

   ![](media/ex-1-5.png)

1. In the new InPrivate window, go to `http://outlook.office.com/`.

   ![](media/ex-1-6.png)

1. Enter your **GitHub Username (1)** (as saved in Notepad) and click **Next (2)** to proceed.

   ![](media/ex-1-7.png)

1. Enter your **GitHub Password (1)** (as saved in Notepad) and click **Sign in (2)**.

   ![](media/ex-1-8.png)

1. If you see the pop-up **Stay Signed in?**, select **No**.

   ![](media/ex-1-9.png)

1. Check your email inbox and copy the **Verification code** sent by GitHub.

   ![](media/ex-1-10.png)
   
1. On the **Device verification** pane, enter the **Device Verification Code (1)** that was emailed to you and click **Verify (2)**.

   ![](media/ex_1_g_3.png)
   
   > **Note:** If you see **Two-factor authentication (2FA) is required for your GitHub account** page next, click on **Remind me tomorrow**
   
      ![The `New Repository` creation form in GitHub.](media/2fagit.png "New Repository Creation Form")

1. In the upper-right corner of the GitHub dashboard, click on your **Profile (1)** icon and select **Repositories (2)** from the dropdown menu.

   ![](media/ex_1_g_4.png)
   
   ![](media/L1T3S10.2-0501.png)

1. Next to the search criteria, locate and select the **New** button.

   ![The `New Repository` creation form in GitHub.](media/ex_1_g_5_1.png "New Repository Creation Form")

1. On the **Create a new repository** screen, name the repository ```aiw-devops-with-github-lab-files``` **(1)**, select **Public (2)** and click on **Create repository (3)**  button.

   ![The `New Repository` creation form in GitHub.](media/L1T3S12-0501.png "New Repository Creation Form")
   
   >**Note:** If you observe any repository existing with the same name, please make sure you delete the Repo and create a new one. Please follow steps 13 to 17. Else, skip to step 18.

1. In the upper-right corner of the GitHub dashboard, click on your **Profile (1)** icon and select **Repositories (2)** from the dropdown menu.

   ![](media/ex_1_g_4.png)
   
   ![](media/L1T3S10.2-0501.png)

1. Using the search bar, search for **```aiw-devops-with-github-lab-files``` (1)** and **select (2)** to open it.

   ![The `New Repository` creation form in GitHub.](media/ex_1_g_5.png "New Repository Creation Form")

1. From the GitHub repository, click on the **Settings** tab.

   ![The `New Repository` creation form in GitHub.](media/2dg119.png "New Repository Creation Form")

1. In the settings page, scroll to the bottom of the page and select **Delete this repository**.

   ![The `New Repository` creation form in GitHub.](media/2dg120.png "New Repository Creation Form")

1. Are you absolutely sure? pop up window, Copy the **Repository name** **(1)**, paste it in the **Box** **(2)**, and cick on **I understand the consequences, delete this repository** **(3)**.

   ![The `New Repository` creation form in GitHub.](media/2dg121.png "New Repository Creation Form")

1. On the **Quick setup** screen, copy the **HTTPS** GitHub URL for your new repository, and **Save it** in a notepad for future use.

   ![](media/ex_1_g_7.png)
   
1. From the GitHub username, note down the **Unique-ID** present in the Username. You'll use this value in upcoming steps.

   ![](media/L1T3S19-0501.png) 
   
1. Navigate back to the **Visual Studio Code**, ensure the terminal is open. Click on the **drop-down arrow (1)** next to the terminal tab, then select **PowerShell (2)** to open a new PowerShell terminal session.

   ![](media/ex-1-11.png) 

1. In Visual Studio Code, run the following commands in the terminal to set your **Username** and **Email**, which Git uses for commits. Make sure to replace the GitHub account email and username.

   >**Note:** For the email format github_cloudlabsuser_xxx@xxx.com, the corresponding username will follow this format: github-cloudlabsuser-xxx or cloudlabsuser-xxx
   
     ```pwsh
     cd C:\Workspaces\lab\aiw-devops-with-github-lab-files
     git config --global user.email "you@example.com"
     git config --global user.name "Your UserName"
     ```
     
   ![](media/L1T3S21-0501.png) 
   
1.  Run the below mentioned command in the terminal. Make sure to replace <your_github_repository-url> with the value you copied in step 18 and Unique-ID in step 19.

    **Note:** This step is done to initialize the folder as a git repository, commit, and submit contents to the remote GitHub branch “main” in the lab files repository created in Step 1. 

      ```pwsh
      git init
      git add .
      git commit -m "Initial commit"
      git branch -M main
      git remote add <Unique-ID> <your_github_repository-url>
      git push -u <Unique-ID> main
      ```
     
1.  You are asked to authenticate your GitHub account. Select **Sign in with your browser**.

    ![](media/L1T3S23-0501.png)

1.  You will be prompted with a pop-up window to **Authorize Git Credential Manager**. Click on **Authorize git-ecosystem** to provide access.

    ![](media/L1T3S24-0501.png)

1.  After you are prompted with the message **Aythentication Succeeded**, close the tab and continue with the next task.
   
    > **Note:** If you encounter any errors as shown below, please follow the steps outlined below.

    ![](media/ex_1_g_9.png)

    (i) Scroll up within the terminal to locate the highlighted link. Click on the link.

    ![](media/ex_1_g_10.png)

    (ii) Choose the **It's used in tests (1)** option. Then, select **Allow me to expose this secret (2)** to proceed.

    ![](media/ex_1_g_12.png)   

    (iii) After completing the previous step, navigate back to VS Code and execute the command `git push -u <Unique-ID> main` again. 

## Task 4: Build and push using GitHub Actions

In this task, you will build automation in GitHub for updating and republishing our Docker images when the code changes. You will create a workflow file using the GitHub interface and its GitHub Actions workflow editor. This will get you familiar with how to create and edit an action through the GitHub website.

1. From the Azure Portal dashboard, click on **Resource groups** from the navigation panel to view all available resource groups.

   ![](media/ex-1-19.png) 
   
1. Select **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group from the list.

   ![](media/L1TS1-0501.png)  
   
1. In the **contoso-traders** resource group, use the search bar to type **productsdb (1)**. From the filtered results, click **productsdb (2)** to open the SQL database resource.

   ![](media/L1T4S3-0501.png) 
   
1. On the **productsdb** SQL database page, expand **Settings** from the left-hand menu **(1)**, then select **Connection strings** **(2)**. Under the **ADO.NET** tab **(3)**, click the **copy icon** next to the **ADO.NET (SQL authentication)** connection string **(4)**, and paste it into Notepad for later use.

   ![](media/ex-1-21.png) 

1. Replace `{your_password}` with the ODL User Azure Password. Go to **Environment Details (1)**, click on **Azure credentials (2)**, and copy **Password (3)**.
   
   ![](media/ex-1-22.png)  
 
1. In your GitHub lab files repository, select the **Settings** tab from the lab files repository.

   ![](media/L1T4S6-0501.png)
   
1. Under **Security**, expand **Secrets and variables (1)** by clicking the drop-down and select **Actions (2)** blade from the left navigation bar. Select the **New repository secret (3)** button.

   ![](media/L1T4S7-0501.png)
    
1. Under the **Actions Secrets/New secret** page, enter the below-mentioned details. 

   - **Name:** Enter **SQL_PASSWORD (1)**
   - **Secret:** Paste the **ADO.NET (SQL authentication) (2)** which you copied in previous step.
   - Click on **Add secret (3)**.
   
      ![](media/ex-1-23.png)
      
1. Navigate to the **Environment (1)** tab and click on **Service Principal Details (2)**. From the list, copy the following fields:

   - **Subscription ID**
   - **Tenant ID (Directory ID)**
   - **Application ID (Client ID)**
   - **Secret Key (Client Secret)**

      ![](media/g_cor_1.png)
   
   - Replace the values that you copied below with JSON. You will be using them in this step.
   
      ```json
      {
         "clientId": "zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz",
         "clientSecret": "client-secret",
         "tenantId": "zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz",
         "subscriptionId": "zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz"
      }
      ```
   
1. Select **New repository secret** and under **Actions Secrets/New secret** page, enter the below mentioned details and Click on **Add secret (3)**.

   - **Name:** Enter **SERVICEPRINCIPAL (1)**
   - **Secret:** Paste the service principal details in json format **(2)**
   
      ![](media/L1T4S10-0501.png)    
   
1. Select **New repository secret** and under **Actions Secrets/New secret** page, enter the below mentioned details and Click on **Add secret** **(3)**.

   - **Name:** Enter **ENVIRONMENT (1)**
   - **Secret**:**<inject key="DeploymentID" enableCopy="false" /> (2)**
   
      ![](media/L1T4S11-0501.png)
   
1. From your GitHub repository, select the **Actions (1)** tab. Select the **contoso-traders-app-deployment (2)** workflow from the side blade, click on the  **drop-down (3)** next run Run workflow button, and select **Run workflow (4)**.

   ![](media/L1T4S12-0501.png)

1. Navigate back to the Actions tab and select the **contoso-traders-app-deployment** workflow. This workflow builds the docker image, which is pushed to container registry. The same image is pushed to the Azure container application.

   ![](media/2dgn124.png)
   
   ![](media/2dgn165.png)
   
   >**Note:** If the workflow **fails** due to **npm install** job, follow from step 14 - step 16. Else, continue from step 17. 
   
1. From the GitHub browser tab, follow the steps given below and click on **Create codespace on main (3)**.

   - Click on **Code (1)**, 
   - Select the **Codespace (2)** tab

      ![](media/L1T4S14-0501.png)
 
      >**Note:** If prompted to **Install** an extension, please proceed with the installation and **Allow** any **Visual Studio** pop-ups that appear.

      > It will redirect you to the new tab of the browser, where the Visual Studio code will open on web. 
   
1. Run the below-mentioned commands in the **Terminal**. You'll set the node version to node 14.

   ```pwsh
   cd src
   cd ContosoTraders.Ui.Website
   nvm install 14
   nvm use 14
   npm i
   git add . 
   git commit -m "updated node version"
   git push
   ```
    
1. From your GitHub repository, select the **Actions (1)** tab. You'll see an Action named **Updated node version (2)** executing. Please wait until the execution completes.

   ![](media/2dgn160.png)
   
   ![](media/2dgn161.png)      

1. Navigate to the Azure Portal, click on **Resource groups** from the Navigate panel to see the resource groups.

    ![](media/GSS7.png)

1. Select **contoso-traders-<inject key="DeploymentID" enableCopy="false" />** resource group from the list.

    ![](media/L1TS1-0501.png)

1. Search for **ui2 (1)** and select **contosotradersui2<inject key="DeploymentID" enableCopy="false" /> (2)** storage account from the list.

    ![](media/E1T4S18.png)

1. On the storage account page, navigate to **Static website** **(1)** under **Data Management**, enable it by selecting **Enabled** **(2)**, enter **index.html** **(3)** as the index document name, and click **Save** **(4)** to apply the changes.

     >**Note:** If the settings are already enabled in the storage account, please proceed with the next steps.

     ![](media/E1T4S19.png)

1. Navigate back to the **contoso-traders-<inject key="DeploymentID" enableCopy="false" /> (1)** resource group and select **contoso-traders-cdn<inject key="DeploymentID" enableCopy="false" /> (2)** endpoint from the list of resources.

    ![](media/fnd1.png)

1. Copy the **Endpoint hostname** for **contoso-traders-ui2<inject key="DeploymentID" enableCopy="false" />** by clicking the **Copy** icon next to it.

    ![](media/fnd2.png)

1. Open a new browser tab, paste the **Endpoint hostname**, and verify that the **Contoso Traders** app loads successfully.

    ![](media/E1T4S22-1.png)

    
## Task 5: Editing the GitHub Workflow File using Codespace

The last task automated building and updating only one of the Docker images. In this task, we will update the workflow file with a more appropriate workflow for the structure of our repository. This task will end with a file named `docker-publish.yml` that will rebuild and publish Docker images as their respective code is updated.

1. From the GitHub browser tab, follow the steps given below and click on **Create codespace on main (3)**.

   - Click on **Code (1)**, 
   - Select the **Codespace (2)** tab

     ![](media/ex_1_g_13.png)
   
     >**Note:** In case you had created a  codespace in the  previous task. Click on the **+** button to create a new codespace.
   
1. You will be redirected to a new Codespace tab in your browser. This will open VSCode in the new tab of the browser. 
      
1. From the explorer side blade, navigate to **.github (1)** -> **workflows** **(2)** and select **contoso-traders-provisioning-deployment-old.yml** **(3)** file.

   ![](media/L1T5S3-0501.png) 

1. Remove the commands from lines **7 to 14** from the workflow file.

   ![](media/L1T5S4-0501.png)
   
   >**Note:** Press **CTRL + S**, to save the changes, if needed.

1. Using the terminal from Codespace, run the following commands to commit this change to your repo and to push the change to GitHub.

   ```pwsh
   git add .
   git commit -m "Updating app deployment"
   git push
   ```

   ![](media/L1T5S5-0501.png)
    
   > **Note:** This will update the workflow and will **not** run the "Update the ... Docker image" jobs.

1. Navigate back to the GitHub browser, select the **Actions (1)** tab, and review the **workflow (2)** in the **All workflows** section, created automatically for the changes made. Please wait until the execution completes.

   ![](media/lab1-laststepA.png)

   ![](media/lab1-laststepB.png)

## Summary

In this lab, you have imaged a sample application with carts, products, and UI components using .NET. You deployed the infrastructure to Azure using GitHub Actions. You also built automation in GitHub for updating and republishing our workflows when the code changes.

### You have successfully completed the Lab. Click on Next >> to proceed with the next Lab.

![](media/CICD---NEXT-PAGE.png)


