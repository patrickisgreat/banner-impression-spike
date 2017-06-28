# Research
[https://patrickisgreat.github.io/banner-impression-spike/](https://patrickisgreat.github.io/banner-impression-spike/)

## Relevant Links:
**Behavioral Data from the API: **
[ https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/behavioral_data_integration_best_practices.htm?search_text=tracking](%20https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/behavioral_data_integration_best_practices.htm?search_text=tracking)
**Sent Event Details: **
[https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieve_sentevent_details_for_job.htm?search_text=tracking](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieve_sentevent_details_for_job.htm?search_text=tracking)
**Open Event Details: **
[https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieving_open_events_details.htm?search_text=tracking](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieving_open_events_details.htm?search_text=tracking)
**Click Event Details: **
[https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieving_all_links_for_a_send.htm?search_text=tracking](https://developer.salesforce.com/docs/atlas.en-us.noversion.mc-apis.meta/mc-apis/retrieving_all_links_for_a_send.htm?search_text=tracking)


what are the fundamental pieces of this feature? What is the data we want and how can we get it with PHP or JavaScript.

We need the following:
1. Total number of impressions
2. How many people were sent that specific banner?
3. How many people opened and potentially saw that specific banner?
4. How many people clicked on that email?


* Sent Events
	```php
		<?php
		require('ET_Client.php');
		$myclient = new ET_Client();
		$sentevent = new ET_SentEvent();
		$sentevent->authStub = $myclient;
		$response = $sentevent->get();
		print_r($response);
		//for filtering by specific send
		$sentevent->props = array('SendID', 'EventDate');
		//________________//
		// for filtering by specific email
		$sentevent->filter = array('Property' => 'SubscriberKey', 'SimpleOperator' => 'equals', 'Value' => 'example@example.com');
	```
* Open Events
	```php
		<?php
		require('ET_Client.php');
		$myclient = new ET_Client();
		$openevent = new ET_OpenEvent();
		$openevent->authStub = $myclient;
		$response = $openevent->get();
		print_r($response);
		//for filtering by specific send
		$openevent->props = array('SendID', 'EventDate');
		//________________//
		//for filtering by email address
		$openevent->filter = array('Property' => 'SubscriberKey', 'SimpleOperator' => 'equals', 'Value' => 'example@example.com');
	```
* Click Events
		<?php
		require('ET_Client.php');
		$myclient = new ET_Client();
		$clickevent = new ET_ClickEvent();
		$clickevent->authStub = $myclient;
		$response = $clickevent->get();
		print_r($response);
		//for filtering by Specific Send
		$clickevent->props = array('SendID', 'EventDate');
		//________________//
		//for filtering by email address
		$clickevent->filter = array('Property' => 'SubscriberKey','SimpleOperator' => 'equals','Value' => 'example@example.com');
	```

TODO: 
* Get some idea of the UX. (conversations with Lisa + AJ)
	* Does the user see this per Banner ? If so where ?
	* Can they see a list of all banners data?
	* Do we want pretty graphs?
		* etc. etc…
* Stub out the Laravel Model to house this data.
* Alter a test template with the needed alias tags (ask Zach about this)
* Update LaravelEtApi package with sugar for the above method examples
* Figure out if an SFMC query exists to associate this click, send, and impression data to banners based on the aliases
	* If the query does not exist write it (again ask Z)
* Create DE to house queried data that mirrors Laravel model
* Build Laravel Controller for Impression Tracking
* Build out Vue Component with dataTable
* Build out blade including updates to primary / sub navs
