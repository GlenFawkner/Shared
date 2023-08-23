#Confirm following packages are installed. 
sudo apt-get update
sudo apt-get install curl
sudo apt-get install libplist-utils
sudo apt-get install apt-transport-https
sudo apt-get install gpg
sudo apt-get install ntp

#Configure repo source 
curl -o microsoft.list https://packages.microsoft.com/config/ubuntu/20.04/prod.list
sudo mv ./microsoft.list /etc/apt/sources.list.d/microsoft-prod.list

#Install decryption key 
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/

#Update 
sudo apt-get update

#Install Defender
sudo apt-get install mdatp

#Download onboarding script from the Defender console
#Activate endpoint
python3 MicrosoftDefenderATPOnboardingLinuxServer.py

#Test endpoint 
mdatp connectivity test
mdatp definitions update
mdatp health

#Configured endpoint as desired 
https://yongrhee.wordpress.com/2021/05/21/mde-for-linux-sample-mdatp_managed-json/