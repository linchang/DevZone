#GetResponse Callback

version 1.0.0, 2012-11-06 [changelog](#changelog)

##GETTING STARTED

Callbacks allow external systems to be notified about GetResponse contact activities.

####Configuration

Callbacks can be managed using API [get_account_callbacks](https://github.com/GetResponse/DevZone/tree/master/API/README.md#get_account_callbacks), [set_account_callbacks](https://github.com/GetResponse/DevZone/tree/master/API/README.md#set_account_callbacks) and [delete_account_callbacks](https://github.com/GetResponse/DevZone/tree/master/API/README.md#delete_account_callbacks) methods.

####Parameters

Sample HTTP callback looks like this:

```
http://foo.bar/callback?action=open \
  &ACCOUNT_ID=A1&account_login=myaccount \
  &CAMPAIGN_ID=C1&campaign_name=mycampaign \
  &MESSAGE_ID=M1&message_name=My%20message&message_subject=Some%20subject \
  &CONTACT_ID=C1&contact_name=Friend&contact_email=friend@implix.com
```

All `*_ID` params are compatible with corresponding identifiers in [API](https://github.com/GetResponse/DevZone/tree/master/API/README.md).
So for example after receiving [open](#open) callback one may call [get_message](https://github.com/GetResponse/DevZone/tree/master/API/README.md#get_message) API method with `MESSAGE_ID` from callback
to fetch additional information about opened message. Those params are case-sensitive.

####Failures

Callback timeout is 4 seconds, not received callbacks ***are lost and will not be repeated***.

Make sure that target server is capable of handling expected amount of requests, especially when SSL URI is given which is more CPU-intensive.

##SUPPORT

The GetResponse Callback interface is created and maintained by the *GetResponse DevZone Team*.

If you run into an error or you have difficulties with using the DC please contact us using [this form](http://www.getresponse.com/feedback.html?devzone=yes) and we will provide all the support we can to solve your problems.

##CALLS

* [subscribe](#subscribe)
* [open](#open)
* [click](#click)
* [goal](#goal)
* [unsubscribe](#unsubscribe)

---

####subscribe<a name="subscribe"/>

_Params:_

* `action` - Always `subscribe`.
* `ACCOUNT_ID`
* `account_login`
* `CAMPAIGN_ID`
* `campaign_name`
* `CONTACT_ID`
* `contact_name` (optional)
* `contact_email`
* `contact_ip` (optional) - In case of double-optin this is the IP from confirmation link was clicked.
* `contact_origin` - One of `import`, `email`, `www`, `panel`, `leads`, `sale`, `api`, `forward`, `survey`, `iphone`.

---

####open<a name="open"/>

_Params:_

* `action` - Always `open`.
* `ACCOUNT_ID`
* `account_login`
* `CAMPAIGN_ID`
* `campaign_name`
* `MESSAGE_ID`
* `message_name`
* `message_subject`
* `CONTACT_ID`
* `contact_name` (optional)
* `contact_email`

---

####click<a name="click"/>

_Params:_

* `action` - Always `click`.
* `ACCOUNT_ID`
* `account_login`
* `CAMPAIGN_ID`
* `campaign_name`
* `MESSAGE_ID`
* `message_name`
* `message_subject`
* `LINK_ID`
* `link_url`
* `CONTACT_ID`
* `contact_name` (optional)
* `contact_email`

---

####goal<a name="goal"/>

_Params:_

* `action` - Always `goal`.
* `ACCOUNT_ID`
* `account_login`
* `CAMPAIGN_ID`
* `campaign_name`
* `GOAL_ID`
* `goal_profile`
* `goal_domain`
* `goal_name`
* `goal_url`
* `CONTACT_ID`
* `contact_name` (optional)
* `contact_email`
* `goal_param_0`
* `goal_param_1` (optional)
* `goal_param_2` (optional)
* `goal_param_3` (optional)
* `goal_param_4` (optional)
* `goal_param_5` (optional)

---

####unsubscribe<a name="unsubscribe"/>

_Params:_

* `action` - Always `unsubscribe`.
* `ACCOUNT_ID`
* `account_login`
* `CAMPAIGN_ID`
* `campaign_name`
* `CONTACT_ID`
* `contact_name` (optional)
* `contact_email`

Note that this callback is generated only when contact use unsubscribe link. Other removal reasons such as bounces of complaints are not reported through this callback.

##CHANGELOG<a name="changelog">

version 1.1.0, 2012-11-12

* goal params in [goal callback](#goal)

version 1.0.0, 2012-11-06

* initial release