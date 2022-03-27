# **ANSIBLE REFACTORING AND STATIC ASSIGNMENTS (IMPORTS AND ROLES)** #

This project concentrates on improving ansible codes through **REFACTORING** It also explore using  imports functionality in Ansible. 
Imports allow to effectively re-use previously created playbooks in a new playbook – it allows you to organize your tasks and reuse them when needed.

###  **Step 1**  – Jenkins job enhancement ###

Every new change in the codes creates a separate directory which is not very convenient when we want to run some commands from one place. Besides, 
it consumes space on Jenkins serves with each subsequent change. Let us enhance it by introducing a new Jenkins project/job – we will require Copy Artifact plugin.

1. Go to your Jenkins-Ansible server and create a new directory called ansible-config-artifact – we will store there all artifacts after each build.
~~~
sudo mkdir /home/ubuntu/ansible-config-artifact
~~~
2. Change permissions to this directory, so Jenkins could save files there 
~~~
chmod -R 0777 /home/ubuntu/ansible-config-artifact
~~~
3. Install copy artifacts plugin in Jenkins server

4. Create a new Freestyle project and name it save_artifacts.

This project will be triggered by completion of your existing ansible project. Configure it accordingly:

![](keep_builds.jpg)
![](build_trigger_stable.jpg)

6. The main idea of *save_artifacts* project is to save artifacts into **/home/ubuntu/ansible-config-artifact** directory. To achieve this, create a Build step and choose *Copy artifacts from other project*, specify *ansible* as a source project and **/home/ubuntu/ansible-config-artifact** as a target directory.

![](build_copy.jpg)

7. Test by making some change in README.MD file inside the ansible-config-mgt repository (right inside master branch).
If both Jenkins jobs have completed one after another – you shall see your files inside /home/ubuntu/ansible-config-artifact directory and it will be updated with every commit to your master branch.

Now your Jenkins pipeline is more neat and clean.

![](tree_artifacts.jpg)
