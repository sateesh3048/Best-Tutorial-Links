#Changing server port details
server.port=8081

# Setting datasource setting
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.defer-datasource-initialization=true

# h2 settings
spring.h2.console.enabled=true
spring.h2.console-path=/h2-console

# enable sql commands

#spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# log more sql

# To print binding parameters
logging.level.org.hibernate.SQL=debug
logging.level.org.hibernate.orm.jdbc.bind=trace 

# statistics and slow queries
logging.level.org.hibernate.stat=debug
logging.level.org.hibernate.SQL_SLOW=info

# 2nd Level Cache
logging.level.org.hibernate.cache=debug
