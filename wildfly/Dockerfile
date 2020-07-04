FROM jboss/wildfly

# Add Modules
ADD com/oracle/db/main/ojdbc10.jar /opt/jboss/wildfly/

# Add Config
ADD config/config.sh /opt/jboss/wildfly/
ADD config/cli.properties /opt/jboss/wildfly/bin/
ADD config/config-commands.cli /opt/jboss/wildfly/bin/

RUN echo ls -l /opt/jboss/wildfly/modules/system/layers/base

RUN echo ls -l /opt/jboss/wildfly/modules/system/layers/base/com

USER root

RUN chown -R jboss:jboss /opt/jboss/wildfly
RUN chmod +x /opt/jboss/wildfly/ojdbc10.jar
RUN chmod +x /opt/jboss/wildfly/bin/config-commands.cli
RUN chmod +x /opt/jboss/wildfly/bin/cli.properties
RUN chmod +x /opt/jboss/wildfly/config.sh


# Run CLI wildfly configuration 
RUN /opt/jboss/wildfly/config.sh


# Create admin user
RUN /opt/jboss/wildfly/bin/add-user.sh admin Protec2020 --silent

CMD ["/opt/jboss/wildfly/bin/standalone.sh", "-b", "0.0.0.0", "-bmanagement", "0.0.0.0" ]