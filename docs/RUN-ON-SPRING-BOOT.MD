
## Run on Spring Boot


### Build the Accounts

1.  `$ cd daytrader-accountsapp`

2.  `$ mvn clean install`

    This command builds the Spring Boot executable WAR

### Start the Accounts

1.  `$ cd daytrader-accounts`

2.  `$ ./env/ext/bin/start_server.sh`

    This command runs the Spring Boot executable WAR
    
### Test the Accounts
                                 
1.  `mvn -Pci clean install`

    This command runs the integration tests 
    
### Stop the Accounts

1.  `$ ./env/ext/bin/stop_server.sh`

    This command stops the Spring Boot executable WAR
