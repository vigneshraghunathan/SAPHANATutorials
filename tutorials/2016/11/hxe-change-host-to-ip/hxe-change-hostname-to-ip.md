---
title: Access HANA applications with IP address
description: This tutorial shows how to access applications running on HANA using the system's IP address instead of host names.  
tags: [  tutorial>beginner, tutorial>how-to, products>sap-hana\,-express-edition ]
---
## Prerequisites  
 - Proficiency: beginner
 - Setup: HANA Express Edition (HXE) and applications installed

## How-To Details
if you want to access your applications by IP address and not by host name, follow along with the tutorial.

### Time to Complete
**10 Min**.

---

1. Run the command, `xs apps` to check whether applications are configured to be accessed by host names. If you see an output similar to the below image, go to step 2.

    ![xs apps before output](./beforechange.png)

2. Run the command, `/sbin/ifconfig` to get the IP address of your system. Take a note of it for step 3.

    ![ifconfig command](./ifconfig.png)

3. After taking a backup of the file **/hana/shared/HXE/global/hdb/custom/config/xscontroller.ini**, add the following lines:

   ```
   [communication]

   default_domain = <YOUR_IP_ADDRESS_FROM_STEP_1>

   routing_mode = ports
   ```

   For example, if the IP address in step 1 is **10.172.248.172**, the file would look as follows after the edit:

   ![xscontroller.ini file after step 3](./changedfile.png)

4. Restart the database using the command `HDB stop && HDB start`.

5. Log in to XSA Services.
   * If you are asked for the *API_URL*, enter **https://<YOUR_IP_ADDRESS_FROM_STEP_1>:39030**.
   * If you are asked for the SPACE, select the appropriate space. By default with HXE, apps use the SAP space.

6. If you run the command, `xs apps` you should see an output similar to the image below.

   ![xs apps after output](./afterchange.png)

7. To ensure that applications could be accessed using the system's IP address, go to https://(YOUR_IP_ADDRESS_FROM_STEP_1):(PORT_NUMBER_OF_WEBIDE) from a web browser. It should open the login page for Web IDE.

>Note: The command `xs apps` could be used to obtain **PORT_NUMBER_OF_WEBIDE** as shown below
>      ![webide port number](./webideport.png)


## Next Steps
 - Go to the [`SAP HANA, express edition tutorials page`](http://go.sap.com/developer/topics/sap-hana-express.tutorials.html)
