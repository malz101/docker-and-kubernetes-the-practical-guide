#The tag of the base image to use. The base image to use for any subsequent instructions that follows.
#nodejs as a base image
FROM node:14 

WORKDIR /app

#copy the package.json file in the working directory
COPY package.json zscaler_root_ca_cert.pem /app/

#The proxy at my employer (ZScaler) was causing issues (as it acts as a MITM, that is, it did ssl inspection, causing certification verification issues)
#This fix basically tells npm and node-gyp to use the check against the regular CAs, but also allow this certificate when it comes across it
# RUN export NODE_EXTRA_CA_CERTS="/app/zscaler_root_ca_cert.pem"
#the fix above didn't work

# RUN set NODE_TLS_REJECT_UNAUTHORIZED=0

# RUN npm restart
RUN npm config set strict-ssl false

#run the npm install command to install all the dependencies the application needs
RUN npm install

#copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>
COPY . .

#Define the network ports that this container will listen on at runtime
EXPOSE 3000

CMD [ "node", "app.mjs" ]