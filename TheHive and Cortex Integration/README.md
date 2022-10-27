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
You should get JSON response contain configured analyzer information
