# Basic Phone Menu using PHP and the Vonage Voice API

This app uses the Vonage Voice API to demonstrate an interactive order status phone menu.

* Callers can search for orders by order ID.
* If the caller's number is found, they can get the status of their latest order.

## Prerequisites

You will need:

* At least one Vonage Virtual Number (Phone Number)
* [composer](http://getcomposer.org/) installed
* The [Vonage CLI](https://github.com/Vonage/vonage-cli) installed
* A public web server to host this web app, or [ngrok](https://ngrok.com) on
  your local development system.

## Installation

```sh
git clone https://github.com/Vonage-Community/sample-voice-php-phone-menu.git
cd php-phone-menu
composer install
```

## Configuration

Copy `config.php.dist` to `config.php`, and add public URL Vonage can use to
access the application. If you're using [ngrok](https://ngrok.com) you'll need
to know what subdomain will be used to expose your application.

## Setup

### Buy Numbers & Create Application

To run this application we need to buy 2 numbers, set up an application, and tie the numbers to this application.

1. create an application
```sh
voange apps create "Whisper System"
```

2. Add voice capabilities to the application
```sh
vonage apps capabilities update voice 00000000-0000-0000-0000-000000000000 --voice-inbound-url http://your.domain/answer_inbound --voice-event-url http://your.domain/event
```

3. Buy 2 numbers (run this command for each number):
```sh
vonage numbers buy US 16127779311
```

4. Link the numbers to the application ID (once for each number):

```sh
vonage apps numbers link 00000000-0000-0000-0000-000000000000 16127779311
```

### Running the App

Using the PHP development server:

```sh
php -S 0:8080 ./public/index.php
```

To expose the application to the public internet:

```sh
ngrok http 8080
```

Or you can configure a webserver to serve the app using `/public` as the webroot.

### Using the App

Call the virtual number to check order status over the phone. You can enter any
order ID as the system chooses a random status.

## More Information

For a more detailed writeup, see the
[tutorial on the Vonage Developer Portal](https://developer.vonage.com/en/voice/voice-api/guides/interactive-voice-response).
