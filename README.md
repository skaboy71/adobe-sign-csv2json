# adobe-sign-csv2json
#### PHP based script to get csv "form data" using Adobe Sign agreement ID
#### It converts CSV to JSON and returns as response data

This script was written in PHP using php cURL code as generated by [POSTMAN](https://www.getpostman.com/downloads/) as well as swiping the code from the Gist from @robflaherty as found here https://gist.github.com/robflaherty/1185299 .

### Requirements
* PHP Server running 5.6.40 - (May work with other 5.x versions but this has not been tested)
* Adobe Sign account allowing api access
* Adobe Sign ["integration key"](https://helpx.adobe.com/sign/kb/how-to-create-an-integration-key.html)

### Usage
Once you have this script installed on your php server you can POST to the page like below:

POST - URL `https://yourserver.yourdomain.com/formDataJson.php`

##### JSON Body
```JSON
{
	"agreement_id": "{{Adobe Sign agreement ID}}",
	"token": "{{integration key or oAuth access token}}",
	"sender_email": "{{'sender' email address}}",
	"shard": "{{Geo shared where account is on Adobe Sign}}"
}
```
### Response Example
In the example below there are 2 signers, each of which has a row in the CSV response from Adobe Sign. There are 7 params that are defaults returnd on all agreements. 
*  completed
*  email
*  role
*  first
*  last
*  title
*  company
*  agreementId

The remainder of the data is from the "columns" in the CSV corresponding to the fields on the form signed.
```JSON
{
	"completed": "2019-05-16 09:46:44",
	"email": "echosmusz1+na2main@gmail.com",
	"role": "SIGNER",
	"first": "Samuel",
	"last": "Tanenbaum",
	"title": "CEO",
	"company": "Some Test Company 1",
	"City": "Cityville",
	"St": "OK",
	"Zip": "46832",
	"agreementId": "CBJCHBCAABAAyDr*********_WsSl-Ch6OUFIeHzWJp1",
	"city1": "Cityville",
	"city2": "Townville",
	"largeField2": "A bunch of text in largefield2",
	"street": "123 South Main",
	"id": 0
}, {
	"completed": "2019-05-16 09:50:04",
	"email": "echosmusz1+npssender2@gmail.com",
	"role": "SIGNER",
	"first": "Jack",
	"last": "Johnson",
	"title": "Consultant",
	"company": "Some Test Company 2",
	"City": "Cityville",
	"St": "OK",
	"Zip": "46832",
	"agreementId": "CBJCHBCAABAAyDr*********_WsSl-Ch6OUFIeHzWJp1",
	"city1": "Cityville",
	"city2": "Townville",
	"largeField2": "A bunch of text in largefield2",
	"street": "123 South Main",
	"id": 1
}
```
