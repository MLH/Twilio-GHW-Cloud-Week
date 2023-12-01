# Getting started with Twilio at Global Hack Week

Hello hackers! Learn how to use REST APIs with Twilio during Global Hack Week by following the steps in this repository. You can submit the challenges at [https://ghw.mlh.io](https://ghw.mlh.io/). In this README, you will find instructions to follow for each challenge.

## Getting Help

If you have questions about Twilio or the Global Hack Week challenges, message us on the [MLH Discord](https://discord.mlh.io/).

# Challenges

## What is an API? What is a REST API?

An Application Programming Interface (API) is provided by a service owner so that others may use the features and functions enabled by the service. APIs describe how a consumer will make requests of the service, and what they will receive in return. [Read more](https://www.twilio.com/docs/glossary/what-is-an-api).

A REST API allows software programs to expose functionality and data to other programs over the Internet in a consistent format. Generally speaking, when people use the term REST API, they are referring to an API that is accessed via the HTTP protocol at a predefined set of URLs (uniform resource locators) representing the various resources with which interactions can occur. [Read more](https://www.twilio.com/docs/glossary/what-is-a-rest-api).

Twilio is an example of a REST API. Twilio's communication APIs let you do things like send text messages and emails, make phone calls, and stream video. You can see all of the things you can do with Twilio on the [Twilio docs](https://www.twilio.com/docs).

During Global Hack Week, you will learn how to use Twilio to:

- Inspect a phone number with Twilio Lookup
- Send one-time passcodes over SMS or WhatsApp with Twilio Verify
- Send and receive voice calls Twilio Voice

## Weeklong challenge: Get ready to hack with Twilio.

To complete the week's challenges, there's some setup we need to do first. Today you will:

- Create a Twilio account and receive complimentary free credits to start
- Install the Twilio command line interface
- Install `curl` to make requests to the Twilio API from the command line.

### Step 1: Create an account

If you don't already have a Twilio account, create one by visiting [this link](https://hackp.ac/ghwcloud-twilio).

- You should receive some free credits to start out with. 

### Step 2: Installing the Twilio CLI

The Twilio CLI makes it easy to use Twilio from our command line interface. We will use the Twilio CLI to test our Twilio services from anywhere in the world.

To install the CLI, follow [this guide](https://www.twilio.com/docs/twilio-cli/quickstart).

### Step 3: Installing `curl`

The last step today is to install `curl`. `curl` is a command line tool for getting data from URLs, and we'll use it to interact with the Twilio REST API.

You can learn more about `curl` [here](https://curl.se/).

To install `curl`, follow [this guide](https://everything.curl.dev/get).

`curl` comes pre-installed on Windows, and can be accessed through Powershell. Use `curl.exe` when giving commands, i.e. `curl.exe --version`.

### Step 4: Challenge complete! Time to submit.

You've completed the challenge, high five! To submit the challenge, type `curl --version` into your terminal, and submit a screenshot on the MLH day-of form! 

## Challenge 1: Lookup a phone number

You can learn a lot from a phone number. So Twilio built an API for that!

Today you will:

- Learn how to use curl to make HTTP requests.
- Build a curl request that will fetch phone number information using the Twilio API.

### Step 1: Check out the Twilio documentation on looking up a phone number

The [Twilio documentation for Lookup](https://www.twilio.com/docs/lookup/v2-api/caller-name) offers examples in several languages. This is useful if you are using the Twilio API from your favourite programming language, but it also has examples in curl, making it easy for us to test each endpoint from the command line.

In the code editor on the right of the page, select curl to bring up the example. It will look like this:

Let's break this down.

### Step 2: Understanding the curl command

Let's go through the example command bit by bit.

- `curl`: we're using the command curl! That bit is easy.
- `-X GET: -X` specifies the method for the request to the URL. By default, curl makes a GET request, to simply fetch the contents of the URL.
- `https://lookups.twilio.com/v2/PhoneNumbers/+14159929960`: this is the URL we are sending the request to, it is an endpoint on the Twilio API for making calls.
- `?Fields=caller_name`: this is a request parameter. The Lookup API can return all sorts of different data about a phone number, including line type, SIM swap status, and more. This request queries caller name data.
- `-u $TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN`: we can tell from the leading `$` that this is a variable that our command line will substitute when it makes the request. We will have to set this variable before we make the request, we'll deal with that in the next step! `-u` sets the authentication method. This is where we tell the Twilio API to make the request from our account. There are two variables here:
  - `TWILIO_ACCOUNT_SID`: This is the unique identifier for our account, kind of like a username.
  - `TWILIO_AUTH_TOKEN`: The auth token is kind of like the password for our account when we make an API request. You want to keep this secret!

Phew! That was a lot. Some of that might be confusing. Don't forget that you can ask questions, or ask for help, in the #twilio channel in the MLH Discord.

### Step 3: Building our curl request

We can use this example from the docs almost as is, there is just a couple of things we need to do:

1. Set our `TWILIO_ACCOUNT_SID` and `TWILIO_AUTH_TOKEN` variables.
2. [Optional] Replace the phone number in the URL.

It will be easier to edit the curl command if you copy it into a text editor.

To set your environment variables:

- Go to your [Twilio console](https://console.twilio.com/), and check out account info. Copy the account SID and auth token.
- Follow [this guide](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html) to set those as environment variables in your shell, for MacOS, Linux, and Windows.

To update the phone number in the URL:

- The example URL uses a phone number that starts with +1415... replace this with the number `+12127363100` (or your own phone number in [E.164 format](https://www.twilio.com/docs/glossary/what-e164)!).

Once you've done those two things, our curl request is ready to go!

### Step 4: Make the request

In a new terminal, paste the edited curl command, and press enter. You should see a response that includes the name of a famous building - what is it??

### Step 5: Challenge complete! Time to submit.

Congratulations on completing the challenge! To submit, take a screenshot of your command line output to show that you performed the lookup. Don't forget to submit your code to the [GHW Cloud Week Devpost page]! (https://global-hack-week-cloud.devpost.com)

## Challenge 2: Send and check a verification one-time passcode

[Verify](https://www.twilio.com/docs/verify/api) is Twilio's purpose built API for sending and checking one-time passcodes (OTPs). It's built on top of Twilio's SMS API, but manages a lot of complexity for you so you don't have to write as much code to make it work.

Today you will:

- Create a Verify Service
- Send a Verification over SMS or WhatsApp
- Check the Verification

### Step 1: Create a Verify Service

Head over to the [Verify section of the Twilio Console](https://www.twilio.com/console/verify/services) and click "create new". Name it whatever you'd like and enable at least the SMS or WhatsApp channel. Copy the Service SID that starts with "VA" to use in the next step.

### Step 2: Send a verification code

The [Twilio documentation for sending verifications](https://www.twilio.com/docs/verify/api/verification) has the following example code:

To prepare the request you'll need to:

1. Set our TWILIO_ACCOUNT_SID and TWILIO_AUTH_TOKEN variables.
2. Replace the To with our number.
3. Set the channel to either "sms" or "whatsapp"

It will be easier to edit the curl command if you copy it into a text editor.

To set your environment variables, follow the steps in Challenge 2 step 3.

To replace the number and the channel:

- Set the To number to your phone number.
- Add your Verification Service SID from step 1 to the URL
- The example uses "sms", change the channel to "whatsapp" if that's preferred.

Once you've done those things, our curl request is ready to go!

In a new terminal, paste the edited curl command, and press enter. You should receive a message with a 6 digit OTP.

### Step 3: Check the verification code

The [Twilio documentation for checking verifications](https://www.twilio.com/docs/verify/api/verification-check) has the following example code:

To prepare the request you'll need to:

1. Replace the To with our number used in the last step.
2. Replace the Code with the one you received in the last step.

It will be easier to edit the curl command if you copy it into a text editor. Once you've done those things, our curl request is ready to go!

In a new terminal, paste the edited curl command, and press enter. If the code is correct, you'll see a response that says "status: approved". If you provide the wrong code, the status will still be "pending".

### Step 4: Challenge complete! Time to submit.

Congratulations on completing the challenge! To submit, take a screenshot of your SMS or WhatsApp application to show you received the OTP and submit it to the GHW Cloud Week day-of form!

## Challenge 3: Install the Authy App

Twilio's Authy is a free application for 2FA. You can use it to protect your personal accounts with a strong second factor known as [TOTP](https://www.twilio.com/docs/glossary/totp).

### Step 1: Install the Authy App

Head over to the [Authy Downloads](https://authy.com/download/) page to install the application for iOS, Android or Desktop.

### Step 2: Set up 2FA on one of your online accounts

Authy can be used anywhere Google Authenticator can be used. Add 2FA to any online site that supports authenticator apps. Any site will do, but if you don't have something in mind, [add Authy 2FA to your GitHub account](https://github.com/settings/security).

### Step 3: Challenge complete! Time to submit.

You've completed challenge 4, high five! To submit, take a screenshot of your Authy app showing the site you added and submit to the GHW Cloud Week day-of form! (don't worry about sharing the code, it expires!).

## Challenge 4: Receive your first phone call using TwiML bins and Dev Phone.

[TwiML](https://www.twilio.com/docs/glossary/what-is-twilio-markup-language-twiml) (Twilio Markup Language) is a special markup language which you can use to program actions in Twilio.

Today you will:

- Buy two Twilio numbers
- Install the Dev Phone
- Create a TwiML bin to handle a phone call.
- Assign the TwiML bin to your Twilio number.
- Make a call using Dev Phone.

### Step 1: Buy Two Twilio numbers

With your free credit, you can now buy your first Twilio numbers! While Verify manages sender numbers for you, you need a Twilio number to send and receive generic calls or SMS.

We will buy two numbers:

- One number to use in our application.
- One number to test the other number, using the Dev Phone.

To buy a number, follow [this guide](https://support.twilio.com/hc/en-us/articles/223135247-How-to-Search-for-and-Buy-a-Twilio-Phone-Number-from-Console).

Buy a number with both SMS and Voice capabilities, so you can send/receive messages and phone calls. Phone numbers may not be available in your country, or may require extra identity documentation for your country. If this is the case, you can buy US numbers. This won't cost you any extra during testing, as we'll be using the Dev Phone to call/message the number, and not your local mobile number.

### Step 2: Installing the Dev Phone

The Dev Phone lets us test our Twilio applications using a Twilio number, rather than your own mobile number. This means you can test your applications using only your Twilio credit, from anywhere in the world.

To install the Dev Phone, follow [this guide](https://www.twilio.com/docs/labs/dev-phone).

### Step 3: Create a TwiML bin to handle a phone call

A TwiML bin is a container for TwiML. We can fill the bin with TwiML to program Twilio to do certain actions, and then connect the bin to our phone number. Follow the instructions [here](https://www.twilio.com/docs/serverless/twiml-bins/getting-started#create-a-new-twiml-bin) to create a new TwiML bin to respond to a phone call with "hello world".

### Step 4: Link your TwiML bin to your Twilio number

Now that we have some TwiML to say "hello world", we need to connect it to our phone number. Choose one of the two numbers you purchased in Challenge 1, and follow [this guide](https://www.twilio.com/docs/serverless/twiml-bins/getting-started#wire-your-twiml-bin-up-to-an-incoming-phone-call) to do that.

Remember which number you chose! In the next step, we will use the other number.

### Step 5: Test it using Dev Phone

Open your terminal and start the Dev Phone with `twilio dev-phone`.

After starting up, the terminal will tell you the address of the Dev Phone interface, usually https://localhost:3001. Go here in your browser to use the Dev Phone.

From here, you can select a phone number. Choose the number that you didn't use in the previous step. The Dev Phone will then show you a dialer to call a number. Enter your other phone number, the one with the TwiML bin, and hit call. You should hear "Hello World" spoken back to you.

### Step 6: Challenge complete! Time to submit.

You've completed Challenge 5, high five! To submit, take a screenshot of your Dev Phone call history and submit it to the GHW Cloud Week day-of form!

## Challenge 5: Make your first outbound phone call using curl.

Making an outbound phone call is a similar process to what we did in Challenge 2 to look up a phone number.

### Step 1: Building our curl request

The [Twilio documentation for making calls](https://www.twilio.com/docs/voice/make-calls) offers examples in several languages and tools. We can use this example from the docs almost as is, there is just a couple of things we need to do:

4. Set our TWILIO_ACCOUNT_SID and TWILIO_AUTH_TOKEN variables.
5. Replace the To and From numbers with our Twilio numbers.
6. Replace the Url with the URL of our TwiML bin.

It will be easier to edit the curl command if you copy it into a text editor.

To set your environment variables:

- Go to your [Twilio console](https://console.twilio.com/), and check out account info. Copy the account SID and auth token.
- Follow [this guide](https://www.twilio.com/blog/2017/01/how-to-set-environment-variables.html) to set those as environment variables in your shell, for MacOS, Linux, and Windows.

To replace the numbers:

- Set the To number to the Twilio phone number that you are using in the Dev Phone. NOT the number that we have used for the TwiML bin in earlier challenges.
- Set the From number to be the Twilio phone number that you have used for the TwiML bins in previous challenges.

To replace the URL:

- In Challenge 5 we set up a TwiML bin to say "hello world" when we called our phone number. We can reuse that TwiML bin for our outbound call, so that when we phone someone, it will say "hello world".
- In your [Twilio console](https://console.twilio.com/), find the TwiML bin you created previously. At the top of the page, you will see a url field. Copy this URL.
- Set the Url in our curl request to the TwiML bin URL.

Once you've done those three things, our curl request is ready to go!

### Step 2: Make the request

Make sure your Twilio Dev Phone is running and open it in your browser. In a new terminal, paste the edited curl command, and press enter. Your Dev Phone should ring and you should hear "hello world".

### Step 3: Challenge complete! Time to submit.

Congratulations on completing the Challenge 3! To submit, take a screenshot of your Dev Phone call log to show you received the call.

## Challenge 6: Deploy from the Twilio CodeExchange

CodeExchange makes it easy to get started with any app. It’s a searchable directory of customizable code samples, written by developers around the world, vetted by Twilio experts, and ready for you to use. We can’t wait to see what you build using CodeExchange code samples. Go ahead and get started by checking it out now. Pick one of the Applications and deploy it to your Twilio account. [Twilio CodeExchange](https://www.twilio.com/code-exchange?q=&f=serverless).

Don't forget to take a screenshot of your deployment and submit it to the GHW Cloud Week day-of form! 

# Frequently Asked Questions

## I have an existing account with Twilio credit, what do I do?

You can simply start a new account.  While signed in, head over to your [accounts summary page](https://hackp.ac/ghwcloud-twilio-accounts) and create a new account. This account will start out with the $15 free trial. 

## My Twilio account was suspended

Please contact a member of the MLH team on the GHW discord channel. 
