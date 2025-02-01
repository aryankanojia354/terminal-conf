Install MongoDB 7.0 (Latest Version)
Although MongoDB does not officially support Ubuntu 24.04, you can still install it using the repo for Ubuntu 22.04 (Jammy Jellyfish) since it's compatible.

Import the MongoDB public key:

bash
Copy
Edit
curl -fsSL https://pgp.mongodb.com/server-7.0.asc | sudo gpg --dearmor -o /usr/share/keyrings/mongodb-server-keyring.gpg
Add the MongoDB repository for Ubuntu 22.04:

bash
Copy
Edit
echo "deb [signed-by=/usr/share/keyrings/mongodb-server-keyring.gpg] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-7.0.list
Update the package list:

bash
Copy
Edit
sudo apt update
Install MongoDB:

bash
Copy
Edit
sudo apt install -y mongodb-org
Step 3: Start and Enable MongoDB
bash
Copy
Edit
sudo systemctl start mongod
sudo systemctl enable mongod
Step 4: Verify MongoDB Installation
Check if MongoDB is running:

bash
Copy
Edit
sudo systemctl status mongod
You should see "active (running)".

Step 5: Test MongoDB
Run the MongoDB shell:

bash
Copy
Edit
mongosh
If it connects, the installation was successful! 🎉