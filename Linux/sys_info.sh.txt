#!/bin/bash

echo "A Quick System Audit Script"
2021-11-22
echo "Machine Type Info:"
echo $MACHTYPE
echo -e "Uname info: $(uname -a) \n"
echo -e "IP Info: $(ip addr | grep inet | tail -2 | head -1) \n"
echo  "Hostname: $(hostname -s)" 
