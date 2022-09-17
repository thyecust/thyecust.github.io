# Netfilter

![Netfilter-packet-flow](https://user-images.githubusercontent.com/49089605/190861204-741b9e62-f414-4a44-90ab-a1cff4d66dd7.svg)

| Tables↓/Chains→              |	PREROUTING |	INPUT  |	FORWARD |	OUTPUT |	POSTROUTING |
| ---------------------------  | ----------  | --------|--------- |--------| ------------ |
|(routing decision)            |             |         |     		  |	✓      |             |	
|raw	                         | ✓           |         |			    | ✓      |             |	
|(connection tracking enabled) |	✓		       |	       |          | ✓      |             |	
|mangle	                       | ✓           |	✓     |	  ✓      |	✓	    |    ✓        |
|nat (DNAT)	                   | ✓           |         |        	|	 ✓     |             |	
|(routing decision)	           | ✓			     |         |          |  ✓     |             |	
|filter		                     |             |   ✓     | 	✓	      | ✓      |             |	
|security		                   |             |   ✓	   |  ✓       |	✓      |             |	
|nat (SNAT)	                   |	           |   ✓     |			    |         |    ✓       |
