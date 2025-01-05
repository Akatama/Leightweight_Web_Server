# Lightweight_Web_Server

# Setup
First, you need to clone the project [here](https://github.com/Akatama/Geocoding-Web-Service) into the flask directory

Second, go to the root of the project and then run
```
sudo docker compose up --build -d --scale flask=2
```

Third, go to http://localhost/

# Tear down
Just run
```
sudo docker compose down
```

# Acknowledgements
Thanks to MaxineXiong for making the original version of the flask project.
You can see the original version of it [here](https://github.com/MaxineXiong/Geocoding-Web-Service)
