# for Local create Local VM - t2.medium
- ** install the Node.js v21.7.3
# installs NVM (Node Version Manager)
- ** curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash

# download and install Node.js
- ** nvm install 21

# verifies the right Node.js version is in the environment
- ** node -v # should print `v21.7.3`

# verifies the right NPM version is in the environment
- ** npm -v # should print `10.5.0`

# for next 

------------

# next step is configure cloudinary.com
- ** signup with email 

- ** copy the env from web site :
import {v2 as cloudinary} from 'cloudinary';
          
cloudinary.config({ 
  cloud_name: 'dz68azvye', 
  api_key: '533988494384356', 
  api_secret: 'LzRMTWmumkVVOEkiTarGL5wfiZA' 
});


# and go to the https://www.mapbox.com/ and configure and get the mapbox_token from there.
# and go to the cloud database, https://cloud.mongodb.com/ and create cloud based database and get DB_URL provide below and give the SECRET any of name.




based on the above we need to configure below :



# After configuration, need to clone the repository to VM and NPM install.
# create vi .env file and provide the above configuration and run npm start, it will show database connected.
# After configuration conncted, copy the publicip of vm and http://18.206.154.225:3000/
# after configuration, you can check it.


# Yelp Camp Web Application

This web application allows users to add, view, access, and rate campgrounds by location. It is based on "The Web Developer Bootcamp" by Colt Steele, but includes several modifications and bug fixes. The application leverages a variety of technologies and packages, such as:

- **Node.js with Express**: Used for the web server.
- **Bootstrap**: For front-end design.
- **Mapbox**: Provides a fancy cluster map.
- **MongoDB Atlas**: Serves as the database.
- **Passport package with local strategy**: For authentication and authorization.
- **Cloudinary**: Used for cloud-based image storage.
- **Helmet**: Enhances application security.
- ...

## Setup Instructions

To get this application up and running, you'll need to set up accounts with Cloudinary, Mapbox, and MongoDB Atlas. Once these are set up, create a `.env` file in the same folder as `app.js`. This file should contain the following configurations:

```sh
CLOUDINARY_CLOUD_NAME=[Your Cloudinary Cloud Name]
CLOUDINARY_KEY=[Your Cloudinary Key]
CLOUDINARY_SECRET=[Your Cloudinary Secret]
MAPBOX_TOKEN=[Your Mapbox Token]
DB_URL=[Your MongoDB Atlas Connection URL]
SECRET=[Your Chosen Secret Key] # This can be any value you prefer
```

After configuring the .env file, you can start the project by running:
```sh
docker compose up
```

## Application Screenshots
![](./images/home.jpg)
![](./images/campgrounds.jpg)
![](./images/register.jpg)


---------------------
For Jenkins setup:
Plugin:
Nodejs
sonarqube
docker
docker pipelines
kubernetes
kubeernets cli
---------------------
