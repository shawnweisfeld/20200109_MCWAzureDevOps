# Hands-on lab - Exercise 4

**Contents**
- [Setup](LabSetup)
- [Exercise 1](LabExercise01)
- [Exercise 2](LabExercise02)
- [Exercise 3](LabExercise03)
- [Exercise 4](LabExercise04)
- [Exercise 5](LabExercise05)
- [Exercise 6](LabExercise06)
- [Cleanup](LabCleanup)

[Last](LabExercise03) | [Home](lab) | [Next](LabExercise05)

## Exercise 4: Create Azure DevOps release pipeline

Duration: 30 Minutes

In this exercise, you will create a release pipeline in Azure DevOps that performs automated deployment of build artifacts to Microsoft Azure. The release pipeline will deploy to three stages: dev, test, and production.

### Task 1: Create a release definition

1.  Select **Releases** on the left-hand navigation. This will bring up the Releases screen. 

    ![A screen that shows the left-side navigation. Releases is highlighted.](./assets/lab-images/stepbystep/media/image84.png "Releases")

2.  Choose the **New pipeline** button to begin the creation of a new release pipeline.

    ![On the Releases screen, the New pipeline button is highlighted.](./assets/lab-images/stepbystep/media/image85.png "Releases screen")

3.  Then, you'll need to select the template that matches the pipeline you are building. Since we are deploying an Azure App Service, select **Azure App Service deployment** from the list of templates and choose the **Apply** button.

    ![A screen that shows choosing Azure App Service deployment.](./assets/lab-images/stepbystep/media/image85a.png "Select a template")

4.  This will present you with the New release pipeline editor which allows you to manage your release stages. A stage is a logical and independent concept that represents where you want to deploy a release generated from a release pipeline. Often times, this is considered an environment. Let's start by giving this stage a name. Change the value "Stage 1" in the editor to "dev" and then select the "X" in the top-right corner to close the panel and save the name change.

    ![A screen that shows Stage details. The Stage name is highlighted. The X is also highlighted.](./assets/lab-images/stepbystep/media/image86.png "Stage")

5.  A release consists of a collection of artifacts in your CD/CD process. An artifact is any deployable component of your application. When authoring a release pipeline, you link the appropriate artifact sources to your release pipeline. In this step, we will connect the artifacts from our previously created build pipeline to this newly created release pipeline. Select the "+ Add" button next to "Artifacts" or the "+ Add an artifact" icon inside the "Artifacts" box. Both buttons perform the same action.

    ![+ Add and + Add an artifact are highlighted in this step.](./assets/lab-images/stepbystep/media/image87.png "New release pipeline")

6.  The Add an artifact panel will display several configurations for linking to an artifact. In the **Source (build pipeline)** dropdown list, select **TailspinToys**. In the **Default version** field, select **Latest**. The panel fields will adjust to show additional details based on your selection. The default values will produce a new release when future builds successfully complete. Select the **Add** button.

    ![On the Add an artifact screen, TailspinToys is highlighted in the Source (build pipeline) field, and the Add button is highlighted at the bottom.](./assets/lab-images/stepbystep/media/image88.png "Add an artifact")

7.  Now, it is time to begin configuring specific tasks to perform our deployment during the dev stage. To navigate to the task editor, select the **Task** menu item and then select the **dev** stage.

    ![In the menu, the Tasks item is highlighted.](./assets/lab-images/stepbystep/media/image89.png "New release pipeline")

8.  This brings up the task editor and opens a panel with configuration details for the dev stage we created earlier. The configuration items set here will be made available to the tasks in this stage.

9.  On this panel, we first need to configure the necessary details to connect the task to Azure for deployment. Let's first start by connecting to our Azure subscription. Select your Azure subscription from the "Azure subscription" dropdown and then choose the **Authorize** button to login and authenticate to the selected subscription.

    ![On the panel, Azure subscription is highlighted along with the Authorize button.](./assets/lab-images/stepbystep/media/image89b.png "Parameters")

10. Then, in the "App service name field" select the one that begins with **tailspintoys-dev-**.

    ![On the panel, App service name is highlighted.](./assets/lab-images/stepbystep/media/image89c.png "Service connections")

11. Now, let's configure the task specific details. Select the "Deploy Azure App Service" task to bring up the configuration panel for task.

    ![On the screen, Deploy Azure App Service is highlighted.](./assets/lab-images/stepbystep/media/image89d.png "Deploy Azure App Service")

12. In a previous exercise, we created a deployment slot for the web app. Deployment slots are actually live apps with their own hostnames. App content and configuration elements can be swapped between two deployment slots, including the production slot. In the "Azure App Service Deploy" panel, locate the **Deploy to Slot or App Service Environment** checkbox and set it to checked.

    ![On the panel, Deploy to slot is highlighted.](./assets/lab-images/stepbystep/media/image89e.png "Azure App Service Deploy")

13. The checkbox will trigger the panel to update with additional configuration items. In the **Resource group** dropdown, select the appropriate resource group you created in the previous exercise. In the **Slot** dropdown, select **staging**.

    ![On the panel, Resource group and Slot are highlighted.](./assets/lab-images/stepbystep/media/image89f.png "Deployment slot configuration")

14. Now that we've completed the configuration for the "Deploy Azure App Service" task to deploy our application to Azure App Service deployment slot, we'll need a way to swap the staging slot with the production slot. To do that, we'll need to add an additional task to the dev stage. Select the **+** (plus sign) on the task list to create a new task.

    ![On the screen, the plus sign is highlighted.](./assets/lab-images/stepbystep/media/image89g.png "Task list")

15. This opens the "Add tasks" panel. Enter **App Service Manage** into the search box and press **Enter**. Then select the **Azure App Service Manage** task from the search results and select the **Add** button.

    ![On the panel, App Service Manage is entered into the search textbox and Azure App Service Manage is highlighted.](./assets/lab-images/stepbystep/media/image90.png "Add tasks")

16. After adding the new task, we now have two tasks for the dev stage. The new task now needs to be configured. Select the **Swap Slots:** task to open the task configuration panel.

    ![On the screen, the Swap Slots task is highlighted.](./assets/lab-images/stepbystep/media/image91.png "Task list")

17. In the "Azure App Service Manage" task panel there are a few configurations we need to set. First, locate the "Azure subscription" field and select the same subscription used in the "Deploy Azure App Service" task.

18. Locate the "App Service name" field, select the item that begins with **TailspinToysWeb-dev-** just like in the "Deploy Azure App Service" task. In the "Resource Group" field, select **TailspinToys-dev**. In the "Source Slot" field, select **staging**.

    ![On the panel, App Service name, Resource group, and Source Slot are all highlighted.](./assets/lab-images/stepbystep/media/image92.png "Swap Slots task configuration")

19. Let's wrap up this activity by giving our release pipeline a new name. Choose the existing "New release pipeline" name to begin editing it. Change the name to "TailspinToys Release".

    ![On the screen, TailspinToys Release name is highlighted.](./assets/lab-images/stepbystep/media/image92a.png "Release pipeline name change")

20. Select "Save" button at the top of the screen and confirm by clicking the "OK" button.

21. Congratulations! You have just created your first release pipeline.

### Task 2: Add test and production environments to release pipeline

1.  On the Pipeline tab, move your mouse over the dev stage and a select the **Clone** button to create a copy of the tasks from the dev stage. We will use the same steps to deploy to test with a few configuration changes.

    ![On the screen, the Clone button is highlighted.](./assets/lab-images/stepbystep/media/image96.png "Copy the deployment tasks")

2.  Select the newly created stage titled "Copy of dev" to bring up the stage configuration panel.

3.  Change the "Stage name" to **test** and then close the panel.

    ![On the panel, Stage name is highlighted.](./assets/lab-images/stepbystep/media/image96a.png "Stage configuration panel")

4.  Now, we will begin modifying the configuration specifics for the test stage. Select the "1 job, 2 tasks" link for the test stage.

    ![On the screen, 1 job, 2 tasks is highlighted.](./assets/lab-images/stepbystep/media/image97.png "Begin configuring the test stage")

5.  This opens the configuration panel for the stage and includes several pre-populated fields. Locate the **App service name** field and change the value to the app service that starts with **tailspintoys-test-**.

    ![On the panel, App service name is highlighted.](./assets/lab-images/stepbystep/media/image97a.png "Stage configuration panel")

6.  Select the "Deploy Azure App Service" task to bring up the task configuration panel. Notice the settings are the same as when we configured it for the dev stage because we cloned the dev stage to create the test stage. You may need to scroll down the panel to see additional fields.

7.  Locate the **Resource group** field and select the resource group you created earlier. Then, locate the **Slot** field and select **staging**.

    ![On the panel, Resource group and Slot are highlighted.](./assets/lab-images/stepbystep/media/image98.png "Task configuration panel")

8.  Now, select the "Swap Slots" task to bring up the task configuration panel. Locate the **App Service name** and select the app service that starts with **tailspintoys-test-**. Next, locate the **Resource group** field and change the value to the resource group you created earlier. Finally, locate the **Source Slot** field and set it to **staging**.

    ![On the panel, Display name, App Service name, Resource group, and Source Slot are highlighted.](./assets/lab-images/stepbystep/media/image99.png "Configure the Swap Slots task")

9.  Select the "Save" button at the top of the screen, and confirm by choosing the "OK" button.

10. Congratulations! You have just created a test stage and added it to your pipeline.

11. Repeat all of the steps in Task 2 to create a production stage being careful to enter "production" as a replacement for "test" and selecting "tailspintoys-production" instead of "tailspintoys-test" where applicable. Do not forget to configure to individual steps in the newly cloned production environment.

12. The final release pipeline should look like the screen shot below:

    ![On the screen, all three stages are shown: dev, test, and production.](./assets/lab-images/stepbystep/media/image100.png "The final release pipeline")

13. Now you will enable the continuous deployment trigger, so the release process automatically begins as soon as a build successfully completes. To do this, select the lightning bolt icon in the Artifacts window.

14. This will bring up the Continuous deployment trigger panel. Change the setting to "Enabled".

    ![On the screen, Continuous deployment artifact lightning bolt is highlighted and the Continuous deployment trigger is enabled.](./assets/lab-images/stepbystep/media/image101.png "Enable the continuous deployment trigger")

15. Select Save, and confirm your changes by clicking "OK". Then, close the panel.

Congratulations! You have completed the creation of a release pipeline with three stages.
