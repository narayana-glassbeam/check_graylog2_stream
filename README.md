check_graylog2_stream.sh
========================

check_graylog2_stream is a check script for nagios that verifies graylog2 streams.

The script checks for the last-alarm time of the specified stream and:

1. If the time is within the specified age (sec), a CRITICAL alarm is raised, otherwise OK.

2. By using the inversion option (-i), if the time is within the specified age (sec), an OK status is returned, otherwise a CRITICAL alarm is triggered.


Usage:

	./check_graylog2_stream.sh -g <graylog server url> -k <graylog api_key> -t <alarm age> -s <stream name> [-i]
	
Options:

	-i , --INVERT
   	 inverts exit code interpretation (default: OFF)

Examples:

	1. INVERT=OFF (default) --> will return CRITICAL if alarm is ON for more than 300 seconds :
	
	./check_graylog2_stream.sh -g http://graylog2.mycorp.com -k da1c06b0e21ffd5cb52bb6e4230fb3439f6b99e8 -t 300 -s My-Stream-Name      

	2. INVERT=ON (-i) --> will return CRITICAL if alarm is OFF for more than 300 seconds:
	
	./check_graylog2_stream.sh -i -g http://graylog2.mycorp.com -k da1c06b0e21ffd5cb52bb6e4230fb3439f6b99e8 -t 300 -s My-Stream-Name    

	3. If graylog behind https use -c opt:

	./check_graylog2_stream.sh -i -g https://graylog2.mycorp.com -k da1c06b0e21ffd5cb52bb6e4230fb3439f6b99e8 -t 300 -s My-Stream-Name -c

Requirements:
	The check_graylog2_stream script uses jshon command line that further requires jansson .

Installation:

	* Download and install jansson-2.4
		cd /usr/local/src
		wget http://www.digip.org/jansson/releases/jansson-2.4.tar.gz
		tar zxvf jansson-2.4.tar.gz
		cd jansson-2.4
		./configure
		make
		make install

	* Download and install jshon
		cd /usr/local/src/
		wget http://kmkeen.com/jshon/jshon.tar.gz
		tar zxvf jshon.tar.gz
		cd jshon-20120914
		make
		cp jshon /bin/

	* Update libs		
		cd /usr/local/lib
		ln -s /usr/local/lib/libjansson.so.4 /usr/lib/libjansson.so.4
		ldconfig

	* For debian users
		Install libjansson-dev by aptitude/apt-get and download and install jshon. Thats all.


Copyright 2013 Emind Systems Ltd - htttp://www.emind.co
This file is part of Emind Systems DevOps Tool set.
Emind Systems DevOps Tool set is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.
Emind Systems DevOps Tool set is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.
You should have received a copy of the GNU General Public License along with Emind Systems DevOps Tool set. If not, see http://www.gnu.org/licenses/.

[![githalytics.com alpha](https://cruel-carlota.pagodabox.com/d6cdf2b04c37fd42080405b5dca7b1ae "githalytics.com")](http://githalytics.com/emind-systems/check_graylog2_stream)
