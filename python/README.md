# TIL Python
> Take a look at random python things I've interesting [over here](https://github.com/phase7/til#python)

> And Django things [here](https://github.com/phase7/til#django)

### Check network status and when it comes back
My internet is often down and I wanted to check when if network is available so I've made the following script.
```python3
#!/usr/bin/env python3
from subprocess import run
from time import sleep

def main():
    for i in range(200):
        print ("try", i+1)
        run(["ping -c 10 8.8.8.8"], shell=True)
    sleep(4)

if __name__ == "__main__":
	try:
		main()
	except KeyboardInterrupt:
		print("\nExitting...")
		quit()
```
*it checks for connection with Google's DNS server 8.8.8.8 and shows the output on console. Pressing Ctrl + C exits the program nicely*

### Menial tasks I need to do everytime I boot my PC
*Following script takes care of small tasks I need to do when I log in*
```python3
#!/usr/bin/env python3
#checkin if nano backup works, a second time
from subprocess import run

def main():
	commands = [\
	"killall -v mintreport-tray tumblerd nm-applet mintUpdate xfce4-power-manager",
	"sudo apt-get update && sudo apt-get -y upgrade"\
	]
	for x in commands:
		run(x, shell=True)


if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\n\tExitting...")
        quit()
```
