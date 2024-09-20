# DataBase

เนื่องจากทำบน container

docker run --name mongodb-container -d -p 27017:27017 mongo


![Screenshot from 2024-09-20 18-53-32](https://github.com/user-attachments/assets/dc1eba5f-277c-428c-a260-359fbfc9fd79)

# เชื่อมต่อ 

docker run --name express-container --link mongodb-container -d -p 3000:3000
