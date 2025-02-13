# Nagios module check_mailq_totemo

This is a nagios module, i.e. check script for monitoring mail queues on a Totemomail server.  
This script is designed to run on the Totemomail server itself, triggered by a nrpe call from the Nagios server.  
This script assumes, that Totemomail runs on a Linux host or Virtual Appliance.  

To control how alerts should be generated, there is a number of options that can be supplied.  

## Options
The following options can be supplied as arguments. They all have default values and they are optional.  

### `--rootdir`
Absolute directory where Totemomail is installed.  
Default is `/opt/totemomail`  

### `--age_w`
Threshold age of mail items (in minutes). If the age of mail items is older than the threshold age, they may be considered for a Warning alert.  
Default is "5" minutes.  

### `--age_c`
Threshold age of mail items (in minutes). If the age of mail items is older than the threshold age, they may be considered for a Critical alert.  
Default is "30" minutes.  

### `--items_w`
Threshold for number of items in mail queues. If the number of mail items is above theshold, they may be considered for a Warning alert.  
Default is "1" items.  

### `--items_c`
Threshold for number of items in mail queues. If the number of mail items is above theshold, they may be considered for a Critical alert.  
Default is "0" items.  

### `--debug`
Printing additional debug info in the output of this script.  
Use debug only when running script by hand. A Nagios server will not be able to interpret the result.  

### `--help`
Prints a help/usage info.  
  
  
## Examples
`check_mailq_totemo`  
Runs the script with default values. 
  
`check_mailq_totemo --rootdir /opt/trustmail`  
Runs the script with default values, with the Totemomail installation directory in "/opt/trustmail"  
  
`check_mailq_totemo --age_c 15`  
Runs the script with default values, but using the value of "`age_c`" of 15 minutes.  
  
  
## How alert state is determined
### CRITICAL
There are mail items older than "`age_c`" and the number of these items is bigger than or equal "`items_c`".  
### WARNING
There are mail items older than "`age_w`" and the number of these items is bigger than or equal "`items_w`".  
### UNKNOWN
`--rootdir` does not exist or is not a directory.  
Any other unknown error.  
### OK
There are no items in mail queues.  
The items that are in mail queues, are younger than "`age_w`".  
The items that are in mail queues, are older than "`age_w`", but the number of these items is smaller than "`items_w`".  
The items that are in mail queues, are older than "`age_c`", but the number of these items is smaller than "`items_c`".  

