---
title: Access HANA applications with IP address
description: This tutorial shows how to access applications running on HANA using the system's IP address instead of host names.  
tags: [  tutorial>beginner, tutorial>how-to, products>sap-hana\,-express-edition ]
---
## Prerequisites  
 - Proficiency: beginner
 - Setup: HANA express edition and applications installed

## How-To Details
If you want to skip modifying `/etc/hosts` and access applications running on HANA using your system's IP address, follow along with the tutorial.

### Time to Complete
**10 Min**.

---

1. Run the command, `xs apps` to check whether applications are configured to be accessed by host names. If you see an       output similar to the below image, go to step 2.

    ![xs apps before output](beforechange.png)

2. Run the command, `/sbin/ifconfig` to get the IP address of your system. Take a note of it for step 2.

    ![ifconfig command](ifconfig.png)

3. In the file, **/hana/shared/HXE/global/hdb/custom/config/xscontroller.ini**, add the following lines:

   ```
   [communication]

   default_domain = <YOUR_IP_ADDRESS_FROM_STEP_1>

   routing_mode = ports
   ```

   For example, if the IP address in step 1 is **10.172.248.172**, the file would look as follows after the edit:

   ![xs apps before output](changedfile.png)

4. Restart the database using the command `HDB stop && HDB start`.

5. Log in to XSA Services.
   * If you are asked for the *API_URL*, enter **https://hxehost:39030**.
   * If you are asked for the *SPACE*, select **SAP**.

6. If you run the command, `xs apps` you should see an output similar to the image below.

   ![xs apps after output](afterchange.png)

7. To ensure that applications could be accessed using the system's IP address, go to https://(YOUR_IP_ADDRESS_FROM_STEP_1):53075 from a web browser. It should open the log in page for Web IDE.


## Next Steps
 - Go to the [`SAP HANA, express edition tutorials page`](http://go.sap.com/developer/topics/sap-hana-express.tutorials.html)
