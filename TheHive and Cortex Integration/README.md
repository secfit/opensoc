<br />
<div align="center">
  <h1 align="center">TheHive and Cortex Integration</h1>
</div>

Let consider the following scenarion : 
The Hive server : 192.168.1.10  , Version : 5.0.15-1
Cortex server : 192.168.1.15  , Version : 3.1.7-1

## Cortex side
### create API user
<img src="cortex_api_user.JPG">

### create API key
<img src="cortex_create_apikey.JPG">

### Get API key
<img src="cortex_api_key_reveal1.png">

taking this random API key from Cortex : `pRoZdXoWskJiWT2S+45r/mWoa287Dodis` JSONand go ahead to the Hive server

## The Hive side
### Test connnection between the Hive server and Cortex server by using this command
   ```sh
  curl -H 'Authorization: Bearer pRoZdXoWskJiWT2S+45r/mWoa287Dodis' http://192.168.1.15:9001/api/analyzer
  ```
You should get JSON response contain configured analyzer information <br>
NB : make sure tha the firewall rule opened on port 9001 <br>

On /etc/thehive/application.conf add the following line : 
   ```sh
  ## CORTEX configuration
# More information at https://github.com/TheHive-Project/TheHiveDocs/TheHive4/Administration/Connectors.md
# Enable Cortex connector
#play.modules.enabled += org.thp.thehive.connector.cortex.CortexModule # this for The Hive V4
scalligraph.modules += org.thp.thehive.connector.cortex.CortexModule # this for The Hive V5
 cortex {
  servers: [
    {
      name: "CORTEXBAS"                # Cortex name
      url: "http://192.168.1.15:9001" # URL of Cortex instance
      auth {
        type: "bearer"        
        key: "pRoZdXoWskJiWT2S+45r/mWoa287Dodis"                 # Cortex API key
      }
      wsConfig {}                  # HTTP client configuration (SSL and proxy)
    }
  ]
 }

  ```
