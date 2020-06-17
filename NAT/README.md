créer la seconde machine

trouver son ip privée (via la connexion d'instance EC2 - qui ne marche pas ?!): 10.0.2.25

envoyer la clé privée de l'instance 2 depuis son pc vers l'instance 1 via sftp avec fillezilla

se connecter à E1 via putty
	* changer les droits sur le fichier de clé : chmod 400 S20KEYPAIR2EK.pem
	
	* se connecter à E2 avec : ssh -i "S20KEYPAIR2EK.pem" ec2-user@52.87.166.18
	after accepting the key fingerprint, connected to the machine !
	
	
Configure NAT
	* create a NAT security group
	* create an instance : look in AMI fiend for "nat" instance
	* associate the NAT security group to this instance
	* Disabling source/destination checks : Select the NAT instance, choose Actions, Networking, Change Source/Dest. Check
	
