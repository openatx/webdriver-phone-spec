# webdriver-phone-spec
WebDriver for smart phone testing draft. For iOS and Android

# Why make this project ?
One day I decide to make a phone manager platform and also decide to let this platform to support some REST API that can easily operate phone.

Then I google something relative, and found WebDriver spec, saddly this is decided for web testing, not for phone. Project [facebook/WebDriverAgent](https://github.com/facebook/WebDriverAgent) is a good project that can reference, make some extension for WebDriver spec. So I decide to write it out as a draft, that will guide that **phone manager platform** develop in a right direction.

# Reference
* Some are from [WebDriver spec](https://w3c.github.io/webdriver/webdriver-spec.html)
* [facebook/WebdriverAgent](https://github.com/facebook/WebDriverAgent) project

# Details
The RESTful API split into two part, session apis and without session apis.

## Without Session APIs
### Get window size

`GET /windows/size`

### Send Key Event
`POST /keyevent`

params is only `key`, values must be string.

- HOME
- EDIT
- BACK 

iOS got only `HOME` works

### Take screenshot
`GET /screenshot`

The return value will be like

```json
{
	"status": 0,
	"format": "png", // default is png
	"value": {base64 encoded data}
}
```

## Session APIs
Create a session

`POST /session`

`GET /session`

`DELETE /session/{sessionId}`

## LICENSE
Under [GPL 3](LICENSE)