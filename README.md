# Enphase Envoy D7.0.X node-red
Since firmware D7.0.X it is only possible to gain local access to the Enphase envoy IQ gateway once you've obtained a token from Enphase.

This flow is following the approach documented by H4nsie (https://github.com/H4nsie/EnphaseEnvoy/blob/main/plugin.py)

To use this flow you've to adjust the following 3 nodes:
- Login credentials: _provide your username and password you use to login to https://enlighten.enphaseenergy.com_
- Envoy address: _ip address of your Enphase envoy iq gateway_
- sunrise sunset: _provide the coordinates of your solar system such that it will only contact your envoy iq gateway between sunrise and sunset or delete this node_ (The current coordinates refer to a random location in the Atlantic ocean)

# How does it work
The flow has been devided in 3 blocks.
1. **Read envoy using sessionId**<br>Every minute it starts the flow to request information from the envoy gateway. Only when the response has changed to the previous call it will send the retrieved information to a debug node. To contact the envoy a sessionId is needed. When the sessionId is invalid the hppt request response code does not equal 200 and a new sessionId will be requested using block 2.
2. **Login to Envoy with token to obtain sessionId**<br>Login to the envoy iq gateway using a token provided by Enphase to generate a new sessionId. When successfull it will continu requesting data from the envoy (see block 1.). When the token is not valid the http request response code does not match 200 and block 3. is started to request a new token.
3. **Obtain token from Enphase**<br>This block consists out of 4 steps:
     - Retrieve serial number of the envoy iq gateway by accessing the publicly available site http://&lt;envoy&gt;/info.xml
     - Obtain a sessionId from enphaseenergy.com by logging in using your login credentials
     - Request a new token using the obtained sessionId for enphaseenergy.com, serial number and username
     - Save token into memory
  
    Go back to block 2. to login to the envoy using the new obtained token


If you see a message in your debug window stating: "json parse error" don't worry, this indicates that the sessionId used in block 1. is invalid. The flow will automatically go to block 2. to obtain a new sessionId or if needed a new token from enphaseenergy.com using block 3.
