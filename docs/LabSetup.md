# Hands-on lab - Setup

**Contents**
- [**Setup**](LabSetup)
- [Exercise 1](LabExercise01)
- [Exercise 2](LabExercise02)
- [Exercise 3](LabExercise03)
- [Exercise 4](LabExercise04)
- [Exercise 5](LabExercise05)
- [Exercise 6](LabExercise06)
- [Cleanup](LabCleanup)

[Home](lab) | [Next](LabExercise01)

## Setup

### Task 1: Use Azure Shell as your development environment

1.  Go to the **Azure Portal** [https://portal.azure.com](https://portal.azure.com) and log into the provided Microsoft Azure subscription

1.  Launch the **Azure Cloud Shell** on a new tab in the same browser window by going to [https://shell.azure.com](https://shell.azure.com). 

    > If prompted to select a "Directory" pick the same one as the provided Microsoft Azure subscription.

    > If prompted to create a stroage account for the Cloud Shell do so in the provided Microsoft Azure subscription.

    > Be sure that your Cloud Shell is configured to use Bash.

2.  From inside the Azure Cloud Shell type these commands to configure Git running locally in the cloud shell. Be sure to replace with your name and email address.

    ```
    git config --global user.name "<your name>"
    git config --global user.email <your email>
    git config --global credential.helper store
    ```

### Task 2: Download the exercise files

1.  Using the Azure Cloud Shell, you can download the file by executing the following command inside the Cloud Shell window (all on one line):

    ```
    curl -o studentfiles.zip https://cloudworkshop.blob.core.windows.net/agile-continous-delivery/studentfiles.zip
    ```

2.  Extract the contents of the file to the new folder. Using the Azure Cloud Shell, you can execute the following command inside the Cloud Shell window:

    ```bash
    unzip studentfiles.zip
    ```

3.  When unzipped, there will be a new folder named **studentfiles**. Navigate to the newly created **studentfiles** directory.

    ```bash
    cd studentfiles
    ```
   
4.  Inside the **studentfiles** folder, there are two folders named **armtemplate** and **tailspintoysweb**. The workshop will refer to these folders throughout the exercises.

    >**Note**: Using the Azure Cloud Shell, you can load the integrated code editor at any time with the following command:

    ```
    code .
    ```

[Home](lab) | [Next](LabExercise01)