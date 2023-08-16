#### Stage 1: Build the react application
FROM armdocker.rnd.ericsson.se/proj-ldc/common_base_os_release/sles:4.0.0-41 as build


# openssl req -nodes -new -x509 -keyout server.key -out server.cert

# Configure the main working directory inside the docker image. 
# This is the base directory used in any further RUN, COPY, and ENTRYPOINT 
# commands.
WORKDIR /app

# Copy the package.json as well as the package-lock.json and install 
# the dependencies. This is a separate step so the dependencies 
# will be cached unless changes to one of those two files 
# are made.
COPY package.json  ./
RUN zypper addrepo --gpgcheck-strict -f "https://arm.sero.gic.ericsson.se/artifactory/proj-ldc-repo-rpm-local/common_base_os/sles/4.0.0-41" CBO_REPO && zypper --gpg-auto-import-keys refresh -f && zypper install -l -y nodejs16 npm && zypper clean --all
RUN npm cache clean --force
RUN npm config set registry https://arm.seli.gic.ericsson.se/artifactory/api/npm/npm-remote/
RUN npm install
RUN npm install @eds/vanilla@3.15.0 --force --registry https://arm.rnd.ki.sw.ericsson.se/artifactory/api/npm/proj-eds-npm-local


# Copy the main application
COPY . ./

# If you are building your code for production
# RUN npm ci --only=production
RUN npm run build

# Expose port 3000 to the Docker host, so we can access it
# from the outside.
EXPOSE 3000


CMD [ "npm", "start" ]

