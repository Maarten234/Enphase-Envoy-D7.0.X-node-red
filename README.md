# Enphase Envoy D7.0.X node-red
Since firmware D7.0.X it is only possible to gain local access to the Enphase envoy IQ gateway once you've obtained a token from Enphase.

This flow is following the approach documented by H4nsie (https://github.com/H4nsie/EnphaseEnvoy/blob/main/plugin.py)

To use this flow you've to adjust the following 3 nodes:
- Login credentials: provide your username and password you use to login to https://enlighten.enphaseenergy.com
- Envoy address: ip address of your Enphase envoy iq gateway
- sunrise sunset: provide the coordinates of your solar system such that it will only contact your envoy iq gateway between sunrise and sunset or delete this node

The very 1st time you'll run this flow it will generate a json parse error when the node "api/v1/production/inverters" is called. This is due to the fact that the initial sessionId is incorrect. As a consequence a string is returned instead of a json object. This will not effect the performance of the flow. As the response code does not equal 200 the flow will try to login to the envoy gateway to obtain a sessionId. When this does not work it will try to obtain a token from enphaseenergy.com and consequentially login to the envoy gateway.
You'll see that every first call of the day the flow has to request a new sessionId from the envoy gateway and only when the token has expired it will ask for a new token.
