# cr-ation-d-un-VPC-et-2-sous-r-seaux-public-priv-IGW-et-NAT-Gateway
création d’un réseau privé virtuel cloud  VPC et 2 sous réseaux public, privé, IGW et  NAT Gateway

Projet d'architecture réseau sécurisée sur AWS
Mise en place d'une infrastructure cloud isolée avec connectivité contrôlée

Objectifs du projet
Implémenter une architecture réseau AWS conforme aux bonnes pratiques

Isoler les ressources critiques dans un sous-réseau privé

Contrôler finement les flux entrants/sortants

Préparer le terrain pour des déploiements multi-tiers (web/app/DB)

🔧 Technologies clés
Service AWS	Usage
VPC	Isolation réseau
IGW	Connectivité Internet pour le subnet public
NAT Gateway	Accès Internet sécurisé depuis le subnet privé
Route Tables	Contrôle du trafic entre sous-réseaux

Spécifications techniques :

VPC : 10.0.0.0/16 (65 536 IPs)

Subnet Public : 10.0.0.0/24 (us-east-1a)

Subnet Privé : 10.0.1.0/24 (us-east-1b)

NAT Gateway : Elastic IP dédiée

🛠️ Guide d'implémentation
1. Création du VPC
bash
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=VPC1}]'
2. Configuration des sous-réseaux
Public :

bash
aws ec2 create-subnet --vpc-id vpc-123 --cidr-block 10.0.0.0/24 --availability-zone us-east-1a
Privé :

bash
aws ec2 create-subnet --vpc-id vpc-123 --cidr-block 10.0.1.0/24 --availability-zone us-east-1b
3. Déploiement des passerelles
Internet Gateway :

bash
aws ec2 create-internet-gateway --tag-specifications 'ResourceType=internet-gateway,Tags=[{Key=Name,Value=MyIGW}]'
NAT Gateway (nécessite une IP Elastic) :

bash
aws ec2 allocate-address
aws ec2 create-nat-gateway --subnet-id subnet-123 --allocation-id eipalloc-123
🔒 Bonnes pratiques implémentées
Isolation réseau : Séparation stricte public/privé

Haute disponibilité : Sous-réseaux multi-AZ

Security by Design : Aucun accès SSH direct au privé

Traçabilité : Tags AWS cohérents

📚 Ressources complémentaires
Guide AWS VPC

PDF du lab complet

🚀 Prochaines étapes
Automatisation avec Terraform

Intégration avec des services AWS (RDS, Lambda)

Mise en place de VPC Flow Logs

