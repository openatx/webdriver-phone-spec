# webdriver-phone-spec
WebDriver spec protocol for smart phone testing draft. For iOS and Android

# Why make this project ?
One day I decide to make a phone manager platform and also decide to let this platform to support some REST API that can easily operate phone.

Then I google something relative, and found WebDriver spec, saddly this is decided for web testing, not for phone. Project [facebook/WebDriverAgent](https://github.com/facebook/WebDriverAgent) is a good project that can reference, make some extension for WebDriver spec. So I decide to write it out as a draft, that will guide that **phone manager platform** develop in a right direction.

# Reference
* Some are from [WebDriver spec](https://w3c.github.io/webdriver/webdriver-spec.html)
* [facebook/WebdriverAgent](https://github.com/facebook/WebDriverAgent) project

# Queries
This is list of most common endpoints with some query examples using curl with pre-set environment variables:

- `DEVICE_URL` set as device URL (eg. http://somehost/webdriver)
- `SESSION_ID` set as session id. Returned by start session command e.g. D15E12F6-CA23-4CD4-89F9-E5C5EA6F4FAD
- `JSON_HEADER='-H "Content-Type: application/json"'`

The RESTful API split into two part, session apis and without session apis.
## Without Session APIs
APIs do not need a app started.

### Get window size
`GET /windows/size`

### Send Key Event
```
$ curl -X POST -d '{"key": "HOME"}' $DEVICE_URL/keyevent
{
	"status": 0,
	"value": "keyevent: HOME"
}
```

Android `key` can be the following string.

- HOME
- EDIT
- BACK

more see [here](https://developer.android.com/reference/android/view/KeyEvent.html)

iOS got only `HOME` works

### Take screenshot
```
$ curl -X GET $DEVICE_URL/screenshot
{
	"status": 0,
	"value": "{base64 encoded data}"
}
```

## Session APIs
Create a session

`POST /session`

`GET /session`

`DELETE /session/{sessionId}`

# None WebDriver part
Most API reference [openstf REST API](https://github.com/openstf/stf/blob/master/doc/API.md)

## Authentication
TODO here.

## Get infomation about yourself
```
$ curl -H "Authorization: Bearer YOUR-TOKEN-HERE" /api/user
{
	"email": "someone@hostname.com",
	"name": "无名",
	"nickname": "unknown",
	"id": "https://login.netease.com/openid/unknown/"
}
```

## Use a device
Attempts to add a device under the authenticated user's control. This is analogous to pressing "Use" in the UI.

```
$ curl -X POST --data '{"serial":"EP7351U3WQ"}' /api/user/devices
{
	"success": true
}
```

## Stop using a device
```
$ curl -X DELETE /api/user/devices/{serial}
{
	"success": true
}
```

## Remote Connect
Allows you to retrieve the remote debug URL(i.e. an `adb connect` able address)

```
$ curl -X POST /api/devices/{serial}/remoteConnect
{
	"success": true,
	"description": "Device connected",
	"remoteConnectUrl": "10.0.0.1:5555"
}
```

Disconnect a remote debugging session.

```
$ curl -X DELETE /api/devices/{serial}/remoteConnect
{
	"success": true
}
```

## LICENSE
Under [GPL 3](LICENSE)