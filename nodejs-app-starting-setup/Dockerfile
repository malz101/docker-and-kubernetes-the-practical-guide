FROM node

WORKDIR /app

COPY package.json .

#The proxy at my employer (ZScaler) was causing issues (as it acts as a MITM, that is, it did ssl inspection, causing certification verification issues)
#This fix basically tells npm and node-gyp to use the check against the regular CAs, but also allow this certificate when it comes across it
# RUN export NODE_EXTRA_CA_CERTS="/app/zscaler_root_ca_cert.pem"
#the fix above didn't work

RUN npm config set strict-ssl false

RUN npm install

#copies new files or directories from <src> and adds them to the filesystem of the container at the path <dest>
COPY . /app

#Define the network ports that this container will listen on at runtime
EXPOSE 80

CMD ["node", "server.js"]