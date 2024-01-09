# Exporting TIAPortal to a SQL Database
This repository will teach you how to program a VBScript to export data from TIA portal V17 into a SQL Database. This example uses Microsoft's SQL Server Management Studio (SMSS), but I've had success writing data to MySQL 8.2 as well, it just requires a different driver setup. 

<b>Requirements:</b>
  - TIA Portal V17 and applicable licenses.
  - Microsoft SQL Server Management Studio Express

<b>Creating the TIA Portal Program</b>
I won't go too much into detail on creating a TIA Portal program because this guide isn't designed to teach you how to program in TIA Portal. However, for this example, I created 8 tags, 4 to used to store the value and 4 to read the values. The logic is extremely simple, data is moved from one tag to the next. 

For devices, I used a CPU-1512C-1 PN PLC networked to a TP1900 Comfort Panel HMI. I used the basic network settings and everything is simulated through PLCSim. PLC tags are linked to the HMI and the VBScirpt to export the data is stored on the HMI in the Scripts tab. 

![image](https://github.com/hackerdan13/TIAPortaltoSQLDatabase/assets/147435983/a5e56f4e-b6c3-4c76-ac45-723e446e6a83)
![image](https://github.com/hackerdan13/TIAPortaltoSQLDatabase/assets/147435983/1f899962-ecdd-4a70-a416-d8a3adb6abcb)
![image](https://github.com/hackerdan13/TIAPortaltoSQLDatabase/assets/147435983/aecb7c4d-ef1f-4d51-8d12-7fd73eeadffc)
![image](https://github.com/hackerdan13/TIAPortaltoSQLDatabase/assets/147435983/2c59d35c-d221-4e4a-a40f-7c3f6c966b55)

To setup the HMI screen, I linked the input values to sliders and the input_read values to I/O fields. I then used a button with an event set to run when pressed to initiate the VBScript. 

![image](https://github.com/hackerdan13/TIAPortaltoSQLDatabase/assets/147435983/2e902645-8075-4c5e-b41e-b7a7475e4986)

This should be all you need on the TIA portal side, aside from the VBScript. 

<b>Preparing the ODBC Driver and the SQL Server</b>
Once you have your program built, you are going to want to create the SQL Database and table that the data is going to into. Start with creating a database within SMSS, you can accomplish this by either creating a new query and typing in the function: 
CREATE DATABASE <i>database_name</i> 
or 
right clicking on the Databases tab in SMSS and selecting "New Database"

Once the database has been created, you are going to want refresh the server so that it shows up. You can now create a table within SMSS, make sure the number of columns corresponds to the number of tags you are going to be exporting, for example, we have 4 tags we are going to be exporting. It is also important to make sure the data type matches the tag or you will run into errors when you export the data. To create a table use the following command in a query:
CREATE TABLE <i>database_name</i>.dbo.(<i>column_name</i> <i>DATA_TYPE</i>, ....)

<h2>WORK IN PROGRESS!</h2>
