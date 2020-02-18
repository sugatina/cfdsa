#what is the base image we are using
FROM node:latest

#define some environment variables
#ENV APP_PORT=3000 APP_ROOT=/app
ENV APP_PORT=3000
ENV APP_ROOT=/app

#create the $APP_ROOT dir, if not exists, and cd to the dir
WORKDIR ${APP_ROOT}

#copy my files from computer into $APP_ROOT
#for directory, it will copy all the files recursively inside
#need to specify directory name for copy directory
ADD main.js .
ADD package-lock.json .
ADD package.json .
ADD public public
ADD views views

#install dependencies
#this will use package.json
#to run a command if the first command is successful, RUN npm install && echo "done"
RUN npm install
RUN npm audit fix

#configure healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

#before this line will be run during building
#this line onwards will be run only on runtime

#what port is the application using
#by default, it will be using tcp
#if using udp, EXPOSE ${APP_PORT}/udp
EXPOSE ${APP_PORT}

#how to run the program
ENTRYPOINT [ "node", "main.js" ]
#if there is any parameters to pass to the command above, add this command here: CMD [ "3000" ]