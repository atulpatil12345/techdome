# techdome
# go to techdome-backend and create the docker image 
docker build -t techdome-backend .
docker push techdom-backend (docker hub)
# go to techdome-frontend and create the docker image
docker build -t techdome-frontend
docker push techdom-frontend (docker hub)
# go to deployment folder and run docker compose 
docker compose up 


