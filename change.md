# look for the target ip address

![Screenshot from 2025-05-21 10-33-34](https://github.com/user-attachments/assets/c67dcc95-eab3-4a14-918c-f58b520a0f2c)

![Screenshot from 2025-05-21 10-34-01](https://github.com/user-attachments/assets/c7a7adae-2d80-49ca-ae6c-3c7ee790974e)

As you can see we got the target ip address, it is online and is running windows.

# openports

#!/bin/bash

extractPorts() {
	ports="$(cat $1 | grep -oP '\d{1,5}/open' | awk '{print $1}' FS='/' | xargs | tr ' ' ',')"
	ip_address="$(cat $1 | grep -oP '^Host:.*\(\K[^)]+' | head -n 1 | awk '{print $2}')"
	echo -e "\n[*] Extracting information...\n" > extractPorts.tmp
	echo -e "\t[*] IP Address: $ip_address" >> extractPorts.tmp
	echo -e "\t[*] Open ports: $ports\n" >> extractPorts.tmp
	echo $ports | tr -d '\n' | xclip -sel clip
	echo -e "[*] Ports copied to clipboard\n" >> extractPorts.tmp
	cat extractPorts.tmp
	rm extractPorts.tmp
}

extractPorts "$@"
