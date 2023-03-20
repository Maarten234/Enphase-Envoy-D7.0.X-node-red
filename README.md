# Enphase-Envoy-D7.0.X-node-red
Since firmware D7.0.X it is only possible to gain local access to the Enphase envoy IQ gateway once you've obtained a token via:

This flow is following the approach documented by H4nsie (https://github.com/H4nsie/EnphaseEnvoy/blob/main/plugin.py)

To use this flow you've to adjust the following nodes:
- Login credentials: provide your username and password you use to login to https://enlighten.enphaseenergy.com
- Envoy address: ip address of your Enphase envoy iq gateway
- sunrise sunset: provide the coordinates of your solar system such that it will only contact your envoy iq gateway between sunrise and sunset or delete this node

