# How to open a file in the SAP Business Application Studio (BAS) editor with a simple command ("open &lt;file>").

You can open a file with basctl --open file://<AbsolutePath> as described here: https://answers.sap.com/questions/13305362/open-file-from-terminal-in-bas-ide.html.
  This is is however quite a lot to write, especially since only absolute paths like /home/user/project/&lt;projectname&gt;/package.json are accepted. So I added the following helper script:

Create file /home/bin/open:
```shell
    touch /home/bin/open
```	    
Open the newly created file:
```shell
    basctl --open file://home/bin/open
```	        
Insert within /home/bin/open:
```bash
	#!/bin/bash
	abspath=$(realpath $1) 
	basctl --open file://$abspath
```	
Grant the authorization to execute the script:
```shell
	chmod +x /home/bin/open
```		
Open .bashrc:
```shell
	basctl --open file://home/user/.bashrc
```
Append at the end of file /home/user/.bashrc:
```bash
	export PATH="/home/bin:$PATH"
```
Now you can open a file with the command open &lt;RelativePath&gt; or open &lt;AbsolutePath&gt; in the BAS editor, like:
```shell
    open package.json
```
