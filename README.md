This folder contains the flow(node-red flow) , which is used to get cargo token from misysboard; 

# Structure of the flow:

	-Input node("mb http in"): insightToken         => receive get reqeust
	-function node("function"): urlParameters       => parser the data from the get request return two object
	-Output node("mb http out"): insightTokenOutput => return the data from function node to iframe component
	
	

# Function Node:
Two requiremnt should be implemented at the function node :<br/>
 - get cargo token;<br/>
 - generate the return value;<br/>

## To get the cargo token :
  Now the cargo token is stored in the authTokens in the master authToken.<br/>
  In this flow, just get the another value of the authToken object only if the value of this object's "master" key is "master";

Attention:the logic can be changed if the structure of authToken object changes
## For the reutn value:<br/>
  The return value should be placed at msg.payload. <br/>
  two parameters :<br/>
 - One parameter is "schema", which contains one string of template, for example : "userName=$1&accessToken=$2";<br/>
 - One parameter is "data", which is one array. The data of this array is corresponding to the wildcard before.<br/>


# Output of this flow:

The output will release a "set_url" event to iframe. When iframe receives this event, it will generate a new url with data from this flow. 

# Configuration:
After the enviroment setup(this flow should be deployed automaticly), you should also configure the flow in the misysboard panel.

- First create one iframe. 
- Second in configuration panel, choose the link, then go to flow editor. 
- The order of the component should be:
    platform => this flow => iframe
- You need to configure all the link between different node. 
Most important is to configure the url for the link from flow to iframe.

