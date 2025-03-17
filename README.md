**NSS A1 Demo**

Instructions/Commands to run the programs... ->

**S I M P L E\
S U D O**

sudo tee /usr/local/bin/root_test_script.sh <<EOF
#!/bin/bash
echo “I am \$(whoami)…”
EOF

sudo tee /home/alice/test_sudo.sh <<EOF
#!/bin/bash
echo “I am \$(whoami)…”
EOF

sudo chmod 755 /usr/local/bin/root_test_script.sh
sudo chown root:root /usr/local/bin/root_test_script.sh

useradd -m alice

sudo chmod 755 /home/alice/test_sudo.sh
sudo chown alice:alice /home/alice/test_sudo.sh

./my_sudo /home/alice/test_sudo.sh

./my_sudo /usr/local/bin/root_test_script.sh

touch test
./my_sudo test

./my_sudo /etc/shadow

./my_sudo /etc/passwd


**L I N U X   A C C E S S   C O N T R O L   L I S T S**

useradd -m amit
useradd -m narender
useradd -m donald
useradd -m vladimir
useradd -m shahbaz
useradd -m benjamin

echo "amit:password" | chpasswd
echo "narender:password" | chpasswd
echo "donald:password" | chpasswd
echo "vladimir:password" | chpasswd
echo "shahbaz:password" | chpasswd
echo "benjamin:password" | chpasswd

mkdir /home/amit/my_acls

touch /home/amit/my_acls/file1.txt
touch /home/amit/my_acls/file2.txt
mkdir /home/amit/my_acls/subdirectory

chown amit:amit /home/amit/my_acls/file1.txt
chown narender:narender /home/amit/my_acls/file2.txt
chown donald:donald /home/amit/my_acls/subdirectory

ls -l /home/amit/my_acls/

ls -l setacl getacl fget fput my_cd create_dir my_ls

./setacl -u narender -p r-- /home/amit/my_acls/file1.txt

./getacl /home/amit/my_acls/file1.txt

su narender

./fget /home/amit/my_acls/file1.txt

./fput “Add info to the file…” /home/amit/my_acls/file1.txt

exit

./setacl -u donald -p --x /home/amit/my_acls/subdirectory

./getacl /home/amit/my_acls/subdirectory

su donald
./my_cd /home/amit/my_acls/subdirectory

exit

./create_dir /home/amit/my_acls/new_subdirectory

./my_ls /home/amit/my_acls
