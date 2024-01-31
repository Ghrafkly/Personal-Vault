Use the ACS Code of Conduct and other similar frameworks to support your position




### **Topic**
Root-kits

### **Stakeholders**
| Hosts              | Users     | Bad Actors |
| ------------------ | --------- | ---------- |
| Game Companies     | Players   | Cheaters   |
| Software Companies | Clients   | Piracy     |
| Companies          | Employees | Hackers    |
| Governments        | Citizens  | Hackers           |

### General Purpose/Uses
* To give privileged access to machines that installed the root-kit. Allows full control of said systems
* Usually malicious
* Masks its existence, very hard to detect
* Removal can be difficult, if not impossible
* Used for spying
* Can be installed on anything digital
	* Computers
	* Power transformers
	* Phones
	* Speakers
* Does not require internet access
	* In certain cases, it could be installed on a machine that does not have access to the internet and reconfigure it so the rootkit can access the internet while the machine and use can't.

### Types of Rootkits
* User-mode
	* Runs in ring 3
	* Can modify the standard behaviour of programs
* Hypervisor
	* Runs in ring 1
	* Creates a virtual machine, where the rootkit can intercept all hardware and software calls made between the system and user
* Kernel-mode
	* Runs in ring 0
	* Highest operating system privileges
		* Can be thought of as exceeding administrator access
		* Can subvert, or cloak itself from anti-virus software and other virus detection techniques
		* Even if it is detected, can be very difficult if not impossible to remove
	* Can modify the operating system itself
	* Unrestricted security access
	* Is much more complex, bugs are more often to occur
		* Can result in 'good rootkits' becoming vectors for attacks i.e. Sony BMG Copy Protection Rootkit
	* No part of a system that has a kernel-mode rootkit installed can be trusted
	* To combat kernel-level rootkits, operating systems like Windows now implement mandatory signing of all kernel-level drivers. Makes it harder for rootkits to operate undetected and without oversight
* Firmware/Hardware rootkits
	* Highly undetectable
	* In cases of hardware rootkits, the hardware itself will have to be removed. This can be difficult as it might not be as something as easy as the motherboard or CPU, but a small section inside of them. Best practice is to dispose of the effected devices completely

### Famous Examples
* Stuxnet
	* Designed by US and Israel intelligence agencies around 2010 to disable to Iranian Nuclear Program. 
		* Would check if the system was connected to certain models of PLC's (programmable logic controller), then would modify the PLC parameters to spin the uranium enriching centrifuges at irregular speeds. This would damage or even destroy the centrifuge.
		* As the attack was ongoing, Stuxnet would have the PLC tell the computer that nothing was wrong, allowing it to operate undetected until it was too late.
		* The facility targeted was Natanz. It is expected that centrifuges become damaged, and at a facility like Natanz there would be an expectation of around 800 centrifuges being rendered inoperable a year. However, due to Stuxnet this number was around 2000.
	* Exploited zero-day exploits in Windows
	* Accidentally spread to computers outside of the original air-gapped system
	* First known large-scale cyberweapon
	* Kernel and user mode root-kits
	* Discovered as it unexpectedly spread beyond the Natanz facility. While it is not clear how this occurred, the US believed that this was due to modifications made to the code by the Israelis. Alternatively, it may have spread due to weak cyber-security practices at Natanz.
	* Stuxnet still exists, but due to a decade of cyber security improvements it no longer poses a threat.

### **Advantages**
* Can limit a foe's ability to develop technology i.e. Stuxnet
* Prevents cheating, helps to maintain the integrity of online games
* Can be used in anti-virus to better detect and remove viruses

### **Disadvantages**
* Weak implementation of anti-virus rootkits can result in making the user more susceptible to cyber attacks i.e. Sony BMG Copy Protection Rootkit
* Usually used by malicious parties to gain access to computers
	* This can allow them to easily gain access to private and/or secure information
* Can be hijacked to turn it malicious

### Ethics
- Ethic lenses
	* The Rights Lens
	* The Justice Lens
	* The Utilitarian Lens
	* The Common Good Lens
	* The Virtue Lens
	* The Care Ethics Lens
* ACS Code of Conduct
	* The Primacy of Public Interest
	* The Enhancement of Quality of Life
	* Honesty
	* Competence
	* Professional Development
	* Professionalism

### Flavour bits
"When searching for the advantages of rootkits, the top results were all why the were bad"

### My position
* Cyber-security is a constant race between attackers and defenders to find the next hack, and either exploit it or fix it. Due to this, cyber-security professionals have to remain proactive in developing tools, software, and techniques to protect against attackers. This means investigating and developing their own rootkits to research potential attack vectors, come up with novel solutions for defending, or even to use proactively against the attackers.
* The main issue comes from its increasing use in everyday computers and other similar devices. Hardware and software manufacturers like Microsoft, Apple, Samsung etc. are developing rootkits that come with your computers, phones, and other IoT devices. These rootkits are meant to provide better safety and security for users. In Apple's case, they also have a history of using hardware level rootkits to make third-party repairs very difficult, if not impossible. This forces users to have to buy a new phone, instead of fixing the small issue with their existing one.
* These rootkits can also be targets for attack as they provide very low-level access to the systems. If breached, the users device will be in control of malicious actors without them knowing. Even if they do discover the problem, they would have to dispose of the device.
* Rootkits are often used for anti-cheating software for online games. As they are a rootkit they will be running anytime your computer is on, not just when you are playing the game. While these anti-cheat rootkits are meant to be safe, they can be prone to bugs which could wreck havoc on the users system, or even be exploited by malicious parties


### **References**
| References                                                                                                                                                                                                                                                                       | In-text citation                |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- |
| Wikimedia Foundation. (2023, November 16). _Rootkit_. Wikipedia. https://en.wikipedia.org/wiki/Rootkit                                                                                                                                                                           | (Wikipedia, 2023)               |
| Shacklett, M. E., & Rosencrance, L. (2021, October 1). _What is a rootkit?_. Security. https://www.techtarget.com/searchsecurity/definition/rootkit                                                                                                                              | (Shacklett & Rosencrance, 2021) |
| Valve Corporation. (n.d.) *Rootkit Anti-Cheats*. Steam. https://store.steampowered.com/curator/31718523-Rootkit-Anti-Cheats/                                                                                                                                                     | (Steam, n.d.)                   |
| ENISA. (2022, November 29). _Rootkits_. https://www.enisa.europa.eu/topics/incident-response/glossary/rootkits                                                                                                                                                                   | (ENISA, 2022)                   |
| Moes, T. (2024, January). Rootkit Examples (2024): The 7 Worst Attacks of All Time. _Software Lab_. January 2024, https://softwarelab.org/blog/rootkit-examples/                                                                                                                 | (Moes, 2024)                    |
| Fruhlinger, J. (2022, August 31). _Stuxnet explained: The first known cyberweapon_. CSO Online. https://www.csoonline.com/article/562691/stuxnet-explained-the-first-known-cyberweapon.html#:~:text=Stuxnet%20is%20a%20powerful%20computer,about%20its%20design%20and%20purpose. | (Fruhlinger, 2022)              |
| Modine, A. (2008, October 10). _Organized crime tampers with European card swipe devices_. The Register® - Biting the hand that feeds IT. https://www.theregister.com/2008/10/10/organized_crime_doctors_chip_and_pin_machines/                                                  | (Modine, 2008)                  |
| Jeffreys, H. (2021, September 28). _IPhone 13 a repair nightmare - teardown and repair assessment_. YouTube. https://www.youtube.com/watch?v=8s7NmMl_-yg                                                                                                                         | (Jeffreys, 2021)                |
| Australian Computer Society. (n.d.). *ACS Code of Ethics*. ACS. https://www.acs.org.au/content/dam/acs/rules-and-regulations/Code-of-Ethics.pdf                                                                                                                                                                                                                                                                                 | (ACS, n.d.)                                |

