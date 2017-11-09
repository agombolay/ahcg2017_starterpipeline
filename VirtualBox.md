### Install Virtual Box
* [PDF with installation instructions](https://github.com/agombolay/ahcg2017_starterpipeline/blob/master/VM_setup.pdf)

### Virtual Box Commands
* Log out of virtual box: logout or control-A-D
* Log in to virtual box: ssh vannberglab@localhost -p 10022
* Copy files to virtual box: scp yourfile vannberglab@localhost:~/
* Power on virtual box: vboxmanage startvm Ubuntu-64-DR-AHCG --type headless
* Power off virtual box (soft power off): vboxmanage controlvm Ubuntu-64-DR-AHCG poweroff soft
* Copy folders while logged in to box: scp -r agombolay3@gpuvannberg.biology.gatech.edu:/folder/ .
