# Jenkins-Pipeline-
Jenkins Pipeline 
Execute shell

#!/bin/bash
echo "------> Install node modules <------"
npm install
echo 'DATABASE_URL="mysql://root:Anil@112233@localhost:3306/fcm_prod_db"' > .env
echo 'JWT_SECRET_KEY="OKLABS"' >> .env
mysql -u root -pAnil@112233 fcm_prod_db -e "SET FOREIGN_KEY_CHECKS = 0; SELECT CONCAT('DROP TABLE IF EXISTS \`', table_name, '\`;') AS query FROM information_schema.tables WHERE table_schema = 'fcm_prod_db'; SET FOREIGN_KEY_CHECKS = 1;" | tail -n +2 | mysql -u root -pAnil@112233 fcm_prod_db

rm -rf ./prisma/migrations/
npx prisma migrate dev --name "m1"
pm2 restart ecosystem.config.js
