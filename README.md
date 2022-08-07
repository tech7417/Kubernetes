## **Prerequisites**  **For kubernates**

**For installing Kubernetes in your system, here are a few prerequisites that need special attention. The hardware and software requirements are discussed below:**

### **Hardware requirements**

- **Master node with at least 2 GB memory. (Additional will be great)**
- **Worker node with 700 MB memory capacity.**
- **Your Mouse/Keyboard (monitor navigation)**

### **Software requirements**

- **Hype-V**
- **Docker Desktop**
- **Unique MAC address**
- **Unique product UUID for every node**

**Ensuring that there is a full range of connectivity between all the machines in the cluster is a must.**

### **Step 1: Install &amp; Setup Hyper-V**

1. **Your operating system should be Windows 10 (Enterprise, Pro, or Education), with**
2. **At least 4GB of RAM and CPU Virtualization support, though you should double-check that it&#39;s turned on in your BIOS settings.**

**To enable Hyper-V on your machine, follow the steps below:**

1. **Open the Control Panel.
 2. Select Programs from the left panel.**

![](RackMultipart20220807-1-480b94_html_68ed9e5091e07f2f.png)

**3. Next, go to Programs and Features, then Turn Windows Features On or Off.
 4. Examine Hyper-V and the Hypervisor Platform for Windows.**

![](RackMultipart20220807-1-480b94_html_ead4bf4d479cbffb.png)

![](RackMultipart20220807-1-480b94_html_644242279ac40a8a.png)

![](RackMultipart20220807-1-480b94_html_fba3e84d07055201.png)

1. **Select OK.**

- **Your system will now begin installing Hyper-V in the background; it may be necessary to reboot a few times until everything is properly configured. Don&#39;t hold your breath for a notification or anything! Verify that Hyper-V is installed successfully on your machine by running the following command as Administrator in PowerShell:**
- **Get-WindowsOptionalFeature -Online -FeatureName Microsoft-Hyper-V**
- **Once the state is shown as Enabled for above command in Power shell, we are good to go.**

![](RackMultipart20220807-1-480b94_html_756795c14209b7f.png)

### **Step 2: Download Docker for Windows and install it.**

### **Windows users can use Docker Desktop.**

### **Step 3: Install Kubernetes on Windows 10**

**To install Kubernetes,****  simply follow the on-screen instructions on the screen:**

**1. Right-click the Docker tray icon and select Properties.
 2. Select &quot;Settings&quot; from the drop-down menu.**

![](RackMultipart20220807-1-480b94_html_16fc123998bdca77.png)

**3. Select &quot;Kubernetes&quot; from the left panel.
 4. Check Enable Kubernetes and click &quot;Apply&quot;**

![](RackMultipart20220807-1-480b94_html_b0ede70f7a62da90.png)

**Docker will install additional packages and dependencies during the installation process. It may take between 5 and 10 minutes to install, depending on your Internet speed and PC performance. Wait until the message &#39;Installation complete!&#39; appears on the screen. The Docker app can be used after Kubernetes has been installed to ensure that everything is working properly. Both icons at the bottom left will turn green if both services (Docker and Kubernetes) are running successfully and without errors.**

### **Example.**

![](RackMultipart20220807-1-480b94_html_3fda0806a59aaaf1.png)

### **Step 4: Install Kubernetes Dashboard**

**The official web-based UI for managing Kubernetes resources is Kubernetes Dashboard. It isn&#39;t set up by default. Kubernetes applications can be easily deployed using the cli tool kubectl, which allows you to interact with your cloud and manage your Pods, Nodes, and Clusters. You can easily create or update Kubernetes resources by passing the apply argument followed by your YAML configuration file.**

**Use the following commands to deploy and enable the Kubernetes Dashboard.**

**1. Get the yaml configuration file from ** [**here**](https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-rc7/aio/deploy/recommended.yaml)**.
 2. Use this to deploy it**

**. kubectl apply -f .\recommended.yaml**

**Copy Code**

**3. Run the following command to see if it&#39;s up and running.:**

**kubectl.exe get -f .\recommended.yaml.txt**

**Copy Code**

![](RackMultipart20220807-1-480b94_html_b3dc40c19733ff2b.png)

### **Step 5: Access the dashboard**

**The dashboard can be accessed with tokens in two ways: the first is by using the default token created during Kubernetes installation, and the second (more secure) method is by creating users, giving them permissions, and then receiving the generated token. We&#39;ll go with the first option for the sake of simplicity.**

**1. Run the following command PowerShell (not cmd)**

**((kubectl -n kube-system describe secret default | Select-String &quot;token:&quot;) -split &quot; +&quot;)[1]**

**Copy Code**

**2. Copy the generated token
 3. Run**

**kubectl proxy.**

**Copy Code**

**4. Open the following link on your browser: **

**http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/**

**Copy Code**

**5. Select
 Token &amp; paste the generated token
 6. Sign In**

**Finally**

![](RackMultipart20220807-1-480b94_html_c9d3fcbf87b93462.png)

**You&#39;ll be able to see the dashboard and your cloud resources if everything is set up correctly. You can then do almost all of the &quot;hard&quot; work without having to deal with the CLI every time. You may occasionally get your hands dirty with the command line, but if you don&#39;t understand Docker and Kubernetes or don&#39;t have the time to manage your own cloud, it&#39;s better to stick with some PaaS providers that can be quite expensive.**

## **Kubernetes Uninstallation Process**

**The procedures for uninstalling cert-manager on Kubernetes are outlined below. Depending on which method you used to install cert-manager - static manifests or helm - you have two options.**

**Warning:****  To uninstall cert-maneger, follow the same steps as you did to install it, but in reverse. Whether cert-manager was installed from static manifests or helm, deviating from the following process can result in issues and potentially broken states. To avoid this, make sure you follow the steps outlined below when uninstalling.**

**Step 1:****  Before continuing, make sure that all user-created cert-manager resources have been deleted. You can check for any existing resources with the following command:**

**$ kubectl get Issuers,ClusterIssuers,Certificates,CertificateRequests,Orders,Challenges --all-namespaces**

**Copy Code**

**After you&#39;ve deleted all of these resources, you can uninstall cert-manager by following the steps outlined in the installation guide.**

**Step 2:****  Using regular manifests to uninstall.**

1. **Uninstalling from a regular manifest installation is as simple as reversing the installation process and using the delete command.**

**kubectl.**

**Copy Code**

**2. Delete the installation manifests using a link to your currently running version vX.Y. Z like so:**

**$ kubectl delete -f https://github.com/jetstack/cert-manager/releases/download/vX.Y.Z/cert-manager.yaml**

**Copy Code**

**Step 3:****  Uninstalling with Helm.**

**1. Uninstalling cert-manager from a Helm installation is as simple as reversing the installation process and using the delete command on both the server and the client. kubectl and helm.**

**$ helm --namespace cert-manager delete cert-manager**

**Copy Code**

**2. Next, delete the cert-manager namespace:**

**$ kubectl delete namespace cert-manager**

**Copy Code**

**3. Finally, delete the cert-manger  **** CustomResourceDefinitions **** using the link to the version vX.Y.Z you installed:**

**$ kubectl delete -f https://github.com/jetstack/cert-manager/releases/download/vX.Y.Z/cert-manager.crds.yaml**

**Copy Code**

**The namespace is in the process of being terminated.**

**The namespace may become stuck in a terminating state if it is marked for deletion without first deleting the cert-manager installation. This is usually because the APIService resource is still present, but the webhook is no longer active and thus no longer reachable.**

**4. To fix this, make sure you ran the above commands correctly, and if you&#39;re still having problems, run:**

**$ kubectl delete apiservice v1beta1.**