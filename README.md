## UPDATE - This script doesn't work anymore, due to changes in the Instagram API
**Instagram has made changes in their API that require developers to apply to get permissions to use functionalities publicly.**
The default is now to work in a sandboxed version of the API. The developers will only be able to access their own or fellow testers/developers accounts without submitting their apps for review.
Basicly it means that you will not be able to grow a following, because the script will only be able to interact with your account.

[Read more about the new sandbox here](https://www.instagram.com/developer/sandbox/)

# Instagram-growth

Grow your Instagram follower base using this script.
This will use your own account to get real followers that interact with the tags your choose.

![](https://raw.githubusercontent.com/doefler/Instagram-growth/master/img/cover.png)

Follow me @doefler on twitter to know about updates on this scipt.
Please let me know if you would like any other cool features or how this script works for you.
https://twitter.com/doefler

Have a look at instagrams api to better understand how the script works.
https://instagram.com/developer/

I developed this script for growing the awareness around https://artboost.com
Thought it would nice to share it with the world and help other startups.
So they can survive with minimal marketing budget.

I don't support this automatic bot behavior myself and neither does instagram.
Use this script at your own risk!!!

The script does not save any information about which images get liked, what user get followed and so on.
That means that it can possibly keep acting on the same items over and over again.
Feel free to edit the script to behave more intelligent in that sense and save a record of the actions in a database.

You might get an error like this:
`The maximum number of requests per hour has been exceeded. You have made 46 requests of the 30 allowed in the last hour.`
Then wait a while before running the script again.

#### Best practices for gaining instagram followers
http://austenallred.com/user-acquisition/book/chapter/instagram/



#### The script requires
* A server running PHP
* The PHP curl module

#### Getting started
* Download the script to your server
* Edit the config file (config.php)
* Select the tags you want the script to explore
* Automatic commenting
* Get an access token from instagram
* Setup as cronjob (optional)
* Check the requirements for setting up curl

## Setup
### Download the script to your server
Download the files to a folder on your server.
You need both the config.php and instagram-growth.php file before it can run you need to update the config.php file.

### Edit the config file (config.php)
You need to configure all the fields. And replace the UPPERCASE text with your own information
I already provided a default setup.
To get your access_token see the guide below.
```PHP
$conf = array(
	'username' => 'YOUR_USERNAME',
	'access_token' => 'YOUR_ACCESS_TOKEN',
	'debugging' => true,
	'like' => array(
		'do' => true,
		'min_likes' => 20,
		'max_likes' => 0
		),
	'follow' => array(
		'do' => true,
		'min_likes' => 50,
		'max_likes' => 0,
		'like_recent' => array(
				'do' => true,
				'count' => 3
			)
		),
	'comment' => array(
		'do' => false,
		'min_likes' => 80,
		'max_likes' => 0
		)
);
```
Set `'debugging' => false` if you are not interested in seeing an output of what the script does.
It can be useful to see if you test it in the browser.
#### Like parameters
Choose when and if the script should like images

| Like  		| Desciption	| Possible values	|
| ------------- | ------------- | ------------- |
| do			| Should this action be performed  | `true`/`false`  |
| min_likes     | If you only want to like when the images has more than a certain amount of likes already  | `0` = no limit / `20` = more than 20 likes  |
| max_likes     | The opposite of min_likes. This limits the action to perfom only on images that has less than a certain amount of likes  | `0` = no limit / `20` = less than 20 likes  |

#### Follow parameters
Choose when and if the script should follow the user that uploaded an image

| Follow  		| Desciption	| Possible values	|
| ------------- | ------------- | ------------- |
| do			| Should this action be performed  | `true`/`false`  |
| min_likes     | If you only want to follow users when the images has more than a certain amount of likes  | `0` = no limit / `20` = more than 20 likes  |
| max_likes     | The opposite of min_likes. This limits the action to perfom only on images that has less than a certain amount of likes  | `0` = no limit / `20` = less than 20 likes  |
| like_recent     | If enabled, the script likes the selected amount of recent images by the followed user  | do:`true`/`false` AND count: `3` = likes the 3 most recent images  |

#### Comment parameters
Choose when and if the script should comment on the image.
This feature could quickly feel like a bot for the user. 
But it does use a random comment generating feature.
Set `'do' => true` if you want to try it. And don't forget to configure the "hello" and "praise" texts in the config file.

| Comment  		| Desciption	| Possible values	|
| ------------- | ------------- | ------------- |
| do			| Should this action be performed  | `true`/`false`  |
| min_likes     | If you only want to comment on images when they has more than a certain amount of likes  | `0` = no limit / `20` = more than 20 likes  |
| max_likes     | The opposite of min_likes. This limits the action to perfom only on images that has less than a certain amount of likes  | `0` = no limit / `20` = less than 20 likes  |


### Select the tags you want the script to explore
Exclude the hashtag itself "#" when you write your tags.
Be aware that the more tags you add, the longer time the script will take to perform.
```PHP
$tags = array(	
	'TAG_1',
	'TAG_2',
	'TAG_3',
);
```
### Automatic commenting
If you want the script to comment on your behalf you should change the predefined texts to something that makes sense to your customers.
Make sure to change the UPPERCASE text to your information.
```PHP
$hello = array(	
	'Hey',
	'Hello',
	'Hey there',
	'Hi',
);

$praise = array(	
	', your picture is really nice',
	', you should visit on YOUR_WEBSITE',
	', cool stuff',
	', have you seen YOUR_BRAND_NAME?',
);
```
The script will automaticly add the users name between between the "hello" and "praise" text.
For example a generated comment could be something like:
"Hi Mark Anders your picture is really nice"

### Get an access token from instagram
Get new token at https://apigee.com/console/instagram
And follow the guide below.

#### Step 1
Start by authenticating the console by signing in with your own instagram
Click "OAuth 2" in the dropdown box
![](https://raw.githubusercontent.com/doefler/Instagram-growth/master/img/get-authentication.png)
Then click the "Sign in with Instagram" button
![](https://raw.githubusercontent.com/doefler/Instagram-growth/master/img/signin-with-instagram.png)
#### Step 2
Select a one of the urls from the pull out menu on the left
Run this request by clicking the orange "Send" button on the right
![](https://raw.githubusercontent.com/doefler/Instagram-growth/master/img/select-a-url-to-run.png)
#### Step 3
Your access token for the config can now be found in the left window with the headline "Request"
Copy the value of the access_token and insert into the config.php file (Be aware that it extends to the right behind the vertical window divider).
![](https://raw.githubusercontent.com/doefler/Instagram-growth/master/img/select-the-access-token.png)


### Cronjob (optional)
Run this script periodically with a cronjob.
Add a cronjob in linux

Great intro to setting up a cronjob from linux command line
Open the cronjob editor in linux shell
```
$ crontab -e
```
Run the script once an hour at xx:00 o'clock
```
0 * * * * SCRIPT_TO_RUN
```
The code to run the script
```
php /PATH_TO_SCRIPT/instagram-growth.php
```
To prevent the code from waiting for the output of the script we add a little something to the end of it
```
php /PATH_TO_SCRIPT/instagram-growth.php > /dev/null 2>/dev/null &
```
In the end the code for the crontab looks like this
```
0 * * * * php /PATH_TO_SCRIPT/instagram-growth.php > /dev/null 2>/dev/null &
```

#### Save and close
If using `vi` editor press esc to switch to the command mode, then type `:wq` to write (w) and quit (q) and press Enter.
If using `nano` editor press CTRL + x, then press y for yes and provide a filename before pressing Enter.

A great guide on how to do other settings with the cronjob
http://www.cyberciti.biz/faq/how-do-i-add-jobs-to-cron-under-linux-or-unix-oses/



## Requirements
### Curl

Install the curl module for PHP using the package manager
```
sudo apt-get install php5-curl
```
You will need to restart the server afterwards
```
sudo service apache2 restart
```
Reference
http://askubuntu.com/questions/9293/how-do-i-install-curl-in-php5
