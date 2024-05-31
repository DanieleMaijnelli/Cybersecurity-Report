# **Attack on DC-1 Virtual Machine**
This activity is based on the walkthrough that can be found at the following link.
https://www.hackingarticles.in/hack-the-lampsecurity-ctf-7-ctf-challenge/

### Preliminary information

- The attacking machine is a Kali VM in the same network of the target machine
- The target machine is a VM that can be downloaded at https://www.vulnhub.com/entry/lampsecurity-ctf7,86/
- The objective of the attack is: Gaining root privileges on the target machine
- The threat model is: The attacker can communicate with the target machine
- The attack will be described in terms of the MITRE ATT&CK framework.

### **Discovery**

The first phase consists in finding information about the target useful for obtaining initial access. For this phase I will use *nmap*, a network exploration tool installed by default on Kali. The first command to execute is *ip addr*, that allows to see the IP address of the attacker machine (192.168.56.101) and to obtain the network number (192.168.56.0/24). To obtain the IP address of the target machine, I execute *nmap 192.168.56.0/24*, a command that finds all tries to contact all the IP addresses in the network number specified and lists for each of them the reachable port numbers. This command allows to implement these two techniques of the attack.

##### Remote System Discovery 

The IP address of the target machine is 192.168.56.102.

##### Network Service Discovery

There are several ports reachable, the ones of interest to us are 80 and 8080, both used for HTTP traffic. By visiting on the browser the home page (URL: http://192.168.56.102), we can observe that there is not anything useful to continue the attack, so I try contacting the other port number (URL: http://192.168.56.102:8080).

## Tech



#### Building for source


Dillinger is very easy to install and deploy in a Docker container.

By default, the Docker will expose port 8080, so change this within the
Dockerfile if necessary. When ready, simply use the Dockerfile to
build the image.

```sh
cd dillinger
docker build -t <youruser>/dillinger:${package.json.version} .
```

This will create the dillinger image and pull in the necessary dependencies.
Be sure to swap out `${package.json.version}` with the actual
version of Dillinger.

Once done, run the Docker image and map the port to whatever you wish on
your host. In this example, we simply map port 8000 of the host to
port 8080 of the Docker (or whatever port was exposed in the Dockerfile):

```sh
docker run -d -p 8000:8080 --restart=always --cap-add=SYS_ADMIN --name=dillinger <youruser>/dillinger:${package.json.version}
```

> Note: `--capt-add=SYS-ADMIN` is required for PDF rendering.

Verify the deployment by navigating to your server address in
your preferred browser.