Flowdock library
================

This library allows you to interact with the [Flowdock](https://www.flowdock.com/) API.

[![SensioLabsInsight](https://insight.sensiolabs.com/projects/e7e69bdb-dce1-4189-b3d8-ae3ee661dbc9/big.png)](https://insight.sensiolabs.com/projects/e7e69bdb-dce1-4189-b3d8-ae3ee661dbc9)

[![Build Status](https://travis-ci.org/mremi/Flowdock.svg?branch=master)](https://travis-ci.org/mremi/Flowdock)
[![Total Downloads](https://poser.pugx.org/mremi/flowdock/downloads.svg)](https://packagist.org/packages/mremi/flowdock)
[![Latest Stable Version](https://poser.pugx.org/mremi/flowdock/v/stable.svg)](https://packagist.org/packages/mremi/flowdock)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/mremi/Flowdock/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/mremi/Flowdock/?branch=master)
[![Code Coverage](https://scrutinizer-ci.com/g/mremi/Flowdock/badges/coverage.png?b=master)](https://scrutinizer-ci.com/g/mremi/Flowdock/?branch=master)

**Basic Docs**

* [Installation](#installation)
* [Push API](#push-api)
* [Contribution](#contribution)

<a name="installation"></a>

## Installation

Only 1 step:

### Download Flowdock using composer

Add Flowdock in your composer.json:

```js
{
    "require": {
        "mremi/flowdock": "dev-master"
    }
}
```

Now tell composer to download the library by running the command:

``` bash
$ php composer.phar update mremi/flowdock
```

Composer will install the library to your project's `vendor/mremi` directory.

<a name="push-api"></a>

## Push API

### Chat

```php
<?php

use Mremi\Flowdock\Api\Push\ChatMessage;
use Mremi\Flowdock\Api\Push\Push;

$message = ChatMessage::create()
    ->setContent('This message has been sent with mremi/flowdock PHP library')
    ->setExternalUserName('mremi')
    ->addTag('#hello-world');

$push = new Push('your_flow_api_token');

if (!$push->sendChatMessage($message, array('connect_timeout' => 1, 'timeout' => 1))) {
    // handle errors...
    $message->getResponseErrors();
}
```

You can also do it in your console, look at the help message:

```bash
$ bin/flowdock send-chat-message --help
```

Some arguments are mandatory:

```bash
$ bin/flowdock send-chat-message your_flow_api_token "This message has been sent with mremi/flowdock PHP library" mremi
```

Some options are available:

```bash
$ bin/flowdock send-chat-message your_flow_api_token "This message has been sent with mremi/flowdock PHP library" mremi --message-id=12 --tags="#hello" --tags="#world" --options='{"connect_timeout":1,"timeout":1}'
```

### Team Inbox

```php
<?php

use Mremi\Flowdock\Api\Push\Push;
use Mremi\Flowdock\Api\Push\TeamInboxMessage;

$message = TeamInboxMessage::create()
    ->setSource('source')
    ->setFromAddress('from.mremi@test.com')
    ->setSubject('subject')
    ->setContent('This message has been sent with mremi/flowdock PHP library');

$push = new Push('your_flow_api_token');

if (!$push->sendTeamInboxMessage($message, array('connect_timeout' => 1, 'timeout' => 1))) {
    // handle errors...
    $message->getResponseErrors();
}
```

You can also do it in your console, look at the help message:

```bash
$ bin/flowdock send-team-inbox-message --help
```

Some arguments are mandatory:

```bash
$ bin/flowdock send-team-inbox-message your_flow_api_token source "from.mremi@test.com" subject "This message has been sent with mremi/flowdock PHP library"
```

Some options are available:

```bash
$ bin/flowdock send-team-inbox-message your_flow_api_token source "from.mremi@test.com" subject "This message has been sent with mremi/flowdock PHP library" --from-name=mremi --reply-to="to.mremi@test.com" --project=project --format=html --link="http://www.flowdock.com/" --tags="#hello" --tags="#world" --options='{"connect_timeout":1,"timeout":1}'
```

...and more features coming soon...

<a name="contribution"></a>

## Contribution

Any question or feedback? Open an issue and I will try to reply quickly.

A feature is missing here? Feel free to create a pull request to solve it!

I hope this has been useful and has helped you. If so, share it and recommend
it! :)

[@mremitsme](https://twitter.com/mremitsme)
