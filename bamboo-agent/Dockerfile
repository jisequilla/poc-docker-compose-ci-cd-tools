FROM atlassian/bamboo-agent-base
USER root
RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install maven -y && \
    apt-get install git -y && \
    apt-get install curl dirmngr apt-transport-https lsb-release ca-certificates -y && \
    apt-get install chromium-browser -y && \
    apt-get install gconf-service libasound2 libatk1.0-0 libcairo2 libcups2 libfontconfig1 wget -y && \
    apt-get install libgdk-pixbuf2.0-0 libgtk-3-0 libnspr4 libpango-1.0-0 libxss1 fonts-liberation libappindicator1 libnss3 lsb-release xdg-utils -y && \
    apt-get install openjdk-11-jre openjdk-11-jdk -y

ENV JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64

ENV CHROME_BIN=/usr/bin/google-chrome

# install chrome
RUN wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
RUN dpkg -i google-chrome-stable_current_amd64.deb; apt-get -fy install

# instll Node 12
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN apt-get install nodejs -y && \
    apt-get install gcc g++ make -y 

# install npm cli adduser
RUN npm install -g npm-cli-adduser



USER ${BAMBOO_USER}
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.mvn3.Maven 3.6" /usr/share/maven
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.git.executable" /usr/bin/git
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.jdk.JDK 11" /usr/lib/jvm/java-11-openjdk-amd64
RUN ${BAMBOO_USER_HOME}/bamboo-update-capability.sh "system.builder.node.Node.js 12" /usr/bin/node
ADD settings.xml /usr/share/maven/conf/
RUN mkdir -p ${BAMBOO_USER_HOME}/tmp/deployments/jboss
#/opt/node-0.12/bin/node

# Configura npm registry Bamboo User
ENV NPM_USERNAME=bamboo
ENV NPM_PASSWORD=protec2020
ENV NPM_EMAIL=jrisequilla@minsait.com
ENV NEXUS_HOST=nexus
ENV NEXUS_PORT=8081

ADD .npmrc /home/bamboo

RUN npm config set registry http://${NEXUS_HOST}:${NEXUS_PORT}/repository/npm-group/
RUN npm config set package-lock false

#RUN npm-cli-adduser -u ${NPM_USERNAME} -p ${NPM_PASSWORD} -e ${NPM_EMAIL} -r http://${NEXUS_HOST}:${NEXUS_PORT}/repository/npm-group/

