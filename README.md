# Computer-Technician-Tracker
 
Credits to w3schools.com/ for thier CSS file. - https://www.w3schools.com/w3css/w3css_downloads.asp

Credits to @kreativekorp for this barcode generating script. https://github.com/kreativekorp/barcode

Successfully deployable in local host environment with XAMPP and phpMyAdmin.

Developed with Visual Studio Code, XAMPP and Edge (Chromium version). 

## Features
 
### 1. Index
Simple landing page with links to other pages plus disclaimers. 

### 2. Find details 
Enter hostname and be returned from `details` table hostname printed in code 128 barcode, make and model, serial number, windows key, windows key in code 128 barcode, status and list of past completed work. 

### 3. New computer
Input hostname, make and model, serial number, windows key and status to be added into `details` table.

### 4. New log - Backup
Enter hostname and check off work done, enter remarks and or enter Windows key to be added into `log` table with Window key being updated into `details` table. 

### 5. New log - Restore 
Enter hostname and check off work done, enter remarks and or enter Windows key to be added into `log` table with Window key being updated into `details` table. 

### 6. Update Status from Yellow to Green
With 1 button, change all computers with a status of yellow to have a status of green. 

## New log - Backup vs New log - Restore
The reason for the existence of 2 different new log is because of adoption of the concept of disk imaging. You do all steps on 1 computer, image the disk and restore the image on another laptop allowing the skipping of many steps on the other laptop.  

## Limitations

* For editing information and for viewing multiple rows of information from database at one time, database will need to be directly manipulated. 
* Refreshing page will resubmit the form. 

## Red, Yellow and Green Status
This program has been developed with the concept of working from home. Whereby a technician collects computers from a place and brings them home. At this stage, the computers can be marked with a status of red. By default, a new computer will have a status of red. Following the completion of either a new long - backup or a new long - restore, the status will change to yellow. Indicating that the computer is ready for delivery. After delivery of computer has taken place, status can be changed to green indicating that it is no longer in the hands of the technician. 

## My work is different. How can I edit the work list? 
There is unfortunatenly no front end interface to manipulate the work list. You will have to open `new-log-backup.php` and or `new-log-restore.php` file. Each work comprises of 2 lines of code. Example:
```
<input type="checkbox" name="work[]" value="Ubuntu Hostname set. ">
<label for="work[]">Ubuntu Hostname set. </label><br>
```
In this case, `Ubuntu Hostname set` is the work. You can use the template below to add your own work:
```
<input type="checkbox" name="work[]" value="INSERT_WORK_HERE ">
<label for="work[]">INSERT_WORK_HERE </label><br>
```
Replace `INSERT_WORK_HERE` with your own work. Do leave a space after the work for best results in database. 


## Database
The database this application links to comprises of 2 tables.

Create table SQL commands generated by `SHOW CREATE TABLE` command. 

### Log Table:
```
CREATE TABLE `log` (
  `LogID` int(11) NOT NULL AUTO_INCREMENT,
  `Hostname` varchar(10) NOT NULL,
  `Date` varchar(50) NOT NULL DEFAULT current_timestamp(),
  `Work` text NOT NULL,
  `Remarks` varchar(1000) NOT NULL,
  PRIMARY KEY (`LogID`),
  KEY `Hostname_Validity` (`Hostname`),
  CONSTRAINT `Hostname_Validity` FOREIGN KEY (`Hostname`) REFERENCES `details` (`Hostname`)
) ENGINE=InnoDB AUTO_INCREMENT=218 DEFAULT CHARSET=utf8mb4'
```


### Details Table: 
```
CREATE TABLE `details` (
  `ID` int(11) NOT NULL AUTO_INCREMENT,
  `Hostname` varchar(10) NOT NULL,
  `MakeAndModel` varchar(50) NOT NULL,
  `SerialNumber` varchar(50) NOT NULL,
  `WindowsKey` varchar(50) NOT NULL,
  `Status` varchar(10) NOT NULL,
  PRIMARY KEY (`ID`),
  UNIQUE KEY `Hostname` (`Hostname`),
  UNIQUE KEY `SerialNumber` (`SerialNumber`)
) ENGINE=InnoDB AUTO_INCREMENT=208 DEFAULT CHARSET=utf8mb
```

## Background
This application was developed after failure to find a suitable application that can allow for the work done progress on computers to be documented digitally easily. This application allows technicians to be able to work on multiple computer concurrently and not forget what they have and have not done. Website is smartphone friendly.  

## Screenshot of landing page
https://raw.githubusercontent.com/ahuckphin/Computer-Technician-Tracker/main/CTT.png
