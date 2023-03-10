# FROM python:3.10-slim-buster 1

# Inside Container
# Make a new folder inside container 
# WORKDIR /backend-flask  2

# Outside Container -> Inside Container
# This contains the libraries want to install to run the app 
# COPY requirements.txt requirements.txt. 3

# Inside Container 
# install the python libraries used for the app
# RUN pip3 install -r requirements.txt. 4

# Outside Container -> Inside Container
# . means everyrhing in the current directory
# first period . /backend-flask (outside container)
# second period . /backend-flask (inside container)
# COPY . .   5

# Set Environment Variables
# Inside Container and will remain set when the container is running
# ENV FLASK_ENV=development.  6

# EXPOSE ${PORT}  7 

# CMD (Command)
# python3 -m flask run --host=0.0.0.0 --port=4567
# CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"] 8
# CMD ["./backend.sh"]

# Multi-stage build
# Build stage

FROM python:3.10-slim-buster AS build
WORKDIR /backend-flask 
COPY requirements.txt requirements.txt 
RUN pip3 install --user --no-cache-dir -r requirements.txt 
COPY . .

# Production-ready Stage 
FROM python:3.10-slim-buster AS final 
WORKDIR /backend-flask 
COPY --from=build /root/.local /usr/local 
COPY . .  
ENV FLASK_ENV=production 
EXPOSE ${PORT}
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
