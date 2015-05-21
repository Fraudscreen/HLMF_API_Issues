# HLMF_API_Issues
Public issue tracker for HLMF API

##Raise an Issue with the API
[Raise an issue](https://github.com/Fraudscreen/HLMF_API_Issues/issues)

##How to use the API

Production API Client Link:
https://prod.project-thoth.co.uk:4433/cake/APIClient

REST API URL:
https://prod.project-thoth.co.uk:4433/cake/RestAPI/view.xml
Please note that the API currently uses a self signed SSL certificate, and does require to be provided with a User-Agent, Accept, and Content-Type HTTP headers. The structure of a POST request to the API is as follows, where every value is provided to the API as a Header Resource (to take advantage of the HTTPS encryption of the Header):

```
POST https://prod.project-thoth.co.uk:4433/cake/RestAPI/view.xml HTTP/1.1
Accept-Encoding: gzip,deflate
username: username here
clientCode: clientcode here
orgName: address details here
address1: address details here
address2: address details here
address3: address details here
city: address details here
county: address details here
postcode: address details here
translation: address details here
Accept: application/xml;
User-Agent: any valid user agent header
Content-Type: application/xml
Content-Length: 0
Host: prod.project-thoth.co.uk:4433
Connection: Keep-Alive
```

A response will be in the following format:
```
HTTP/1.1 200 OK
Date: Wed, 15 Apr 2015 10:16:45 GMT
Server: Apache
X-Powered-By: PHP/5.6.7
Set-Cookie: CAKEPHP=COOKIE NAME HERE; expires=Wed, 15-Apr-2015 14:16:45 GMT; Max-Age=14400; path=/; secure; HttpOnly
Content-Length: 138
Keep-Alive: timeout=15, max=100
Connection: Keep-Alive
Content-Type: application/xml; charset=UTF-8

<?xml version="1.0" encoding="UTF-8"?>
<response>
  <RestAPI>
    <RestAPI>
      <Code>Code Here</Code>
    </RestAPI>
  </RestAPI>
</response>
```

Where the XML returned is of this format:
```
<?xml version="1.0" encoding="UTF-8"?>
<response>
  <RestAPI>
    <RestAPI>
      <Code>Code Here</Code>
    </RestAPI>
  </RestAPI>
</response>
```

Any resource marked with address details here does not need to be included if blank or it can be submitted empty. Valid user agents can be found [here](http://www.useragentstring.com/pages/useragentstring.php). I recommend using any common browser user agent. To use the API and get a valid non-error response, the username and client code must be correct. Translation is a field that is included for future use, and currently serves no purpose, however it is recorded.

##Web Client Form layout
![APIScreenshot2](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot2.jpg)
Username and client code will determine who is using the REST API. They also form a basic type of user authentication, as you are unable to return anything meaningful from the API without using a valid username and client code. Organisation Name is the name of any UK business who has their name listed in the Royal Mail PAF data. Address 1 is a combination of the Street Name (Thoroughfare name and descriptor in PAF) or it is a Building Name. Address 2 is either the Street Name of a building that has a name or is is a Dependent Street (Dependent Thoroughfare name and descriptor). If an Address 3 is present this will change the format of the other 2 fields as follows:
* Building Name, Street, Dependent Street
* Sub Building Name, Building Name, Street

Please note that this is not a definitive list as to what can be entered in these fields, and any of the fields in a multi field address can be omitted providing there is enough detail there to distinguish it from another address in the postcode.

City is the city or town of an address, and County is the UK County that the town/city resides in. Postcode is a UK Postcode which are of a format allowed by Royal Mail, as specified by the following rules below (please note a postcode should have a space between the two parts):

### Postcode of Format AA11 1AA
Allowed characters are as follows with 1 being the first character and 8 being the last:

1. All letters except a Q, V, or X.
2. All letters except I, J and Z.
3. Any digit 0-9.
4. Any digit 0-9.
5. Space ONLY.
6. Any digit 0-9.
7. All letters except C, I, K, M, O and V.
8. All letters except C, I, K, M, O and V.

### Postcode of format AA1 1AA
Allowed characters are as follows with 1 being the first character and 7 being the last:

1. All letters except a Q, V, or X.
2. All letters except I, J and Z.
3. Any digit 0-9.
4. Space ONLY.
5. Any digit 0-9.
6. All letters except C, I, K, M, O and V.
7. All letters except C, I, K, M, O and V.

### Postcode of format A11 1AA
Allowed characters are as follows with 1 being the first character and 7 being the last:

1. All letters except a Q, V, or X.
2. Any digit 0-9.
3. Any digit 0-9.
4. Space ONLY.
5. Any digit 0-9.
6. All letters except C, I, K, M, O and V.
7. All letters except C, I, K, M, O and V.

### Postcode of format A1 1AA
Allowed characters are as follows with 1 being the first character and 6 being the last:

1. All letters except a Q, V, or X.
2. Any digit 0-9.
3. Space ONLY.
4. Any digit 0-9.
5. All letters except C, I, K, M, O and V.
6. All letters except C, I, K, M, O and V.

### Postcode of format A1A 1AA
Allowed characters are as follows with 1 being the first character and 6 being the last:

1. All letters except a Q, V, or X.
2. Any digit 0-9.
3. ONLY the letters A, B, C, D, E, F, G, H, J, K, P, S, T, U and W.
3. Space ONLY.
4. Any digit 0-9.
5. All letters except C, I, K, M, O and V.
6. All letters except C, I, K, M, O and V.

### Postcode Format of AA1A 1AA
Allowed characters are as follows with 1 being the first character and 8 being the last:

1. All letters except a Q, V, or X.
2. All letters except I, J and Z.
3. Any digit 0-9.
4. Only the letters A, B, E, H, M, N, P, R, V, W, X and Y.
5. Space ONLY.
6. Any digit 0-9.
7. All letters except C, I, K, M, O and V.
8. All letters except C, I, K, M, O and V.

Please note that the above does only shows the valid formats for postcodes, there will be postcodes that are do not exist that still follow the rules as above.

From this point onwards screeshots will be shown for the Web Client, but all responses will be the same for any other method of interaction.

## Normal Response
![APIScreenshot1](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot1.jpg)
Correct address details are entered and the API will respond with a Fraudscreen Household level code. This updates the Result text at the bottom of the screen and decodes the XML response from the REST API into the text displayed on the screen. 

## Error Responses

### 0 - An error has occurred
![APIScreenshot8](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot8.jpg)
Some sort of unexpected error has occurred when matching an address and a Fraudscreen Household level code cannot be returned. If a 0 occurs, this means there is a problem with the current build and this needs to be addressed, so this should be raised as an issue.

### -1 - Incorrect username
![APIScreenshot3](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot3.jpg)
The username that has been entered is incorrect or does not exist in the clients table of the machine. Currently the only valid username is FRD and anything else entered in this field will produce this error.

### -2 - Incorrect client code
![APIScreenshot4](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot4.jpg)
The client code that has been entered is incorrect or does not exist in the clients table of the machine. Currently the only valid client code is CAPC and anything else entered in this field will produce this error.

### -3 - Incorrect client code and username
![APIScreenshot5](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot5.jpg)
The client code and the username that were entered are both incorrect or do not exist in the clients table of the machine. Currently the only valid username is FRD and the only valid client code is CAPC; anything else entered in this field will produce this error.

### -4 - Entered fields are blank
![APIScreenshot6](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot6.jpg)
All fields entered into the API are blank, so no match is possible. This will be what you get if you try to visit the [REST URL](https://prod.project-thoth.co.uk:4433/cake/RestAPI/view.xml) directly in a browser.

### -5 - Incorrect postcode
![APIScreenshot7](https://github.com/Fraudscreen/HLMF_API_Production/blob/master/images/APIScreenshot7.jpg)
The postcode entered doe not follow the rules of a postcode or doesn't exist, so no code can be determined.
