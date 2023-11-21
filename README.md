
# Social Media Poster

## Overview
The Social Media Poster is a Python script designed to automatically fetch cybersecurity tips from ChatGPT and post them to Twitter.
It runs with a 1/100 chance each time it's executed and, if selected to run, will delay the posting by a random interval of 0 to 60 minutes.

## Prerequisites
- Python 3.x
- OpenAI API Key (for ChatGPT)
- Twitter API Credentials

## Installation
1. Clone the repository or download the script.
2. Install the required Python libraries:
   ```
   pip install openai tweepy
   ```
3. Set up your environment variables. This script requires the following variables:
   - `OPENAI_API_KEY`: Your OpenAI API key.
   - `TWITTER_API_KEY`: Your Twitter API key.
   - `TWITTER_API_SECRET_KEY`: Your Twitter API secret key.
   - `TWITTER_ACCESS_TOKEN`: Your Twitter access token.
   - `TWITTER_ACCESS_TOKEN_SECRET`: Your Twitter access token secret.

## Usage
1. Ensure all the required environment variables are set in your system.
2. Run the script using Python:
   ```
   python SocialMediaPoster.py
   ```
3. The script will log its activities, including the posting of tips and any errors, to a file named `cybersecurity_tips_log.txt`.

## Notes
- The script has a 1/100 chance of posting each time it's run, introducing an element of randomness in posting frequency.
- Before posting, the script will wait for a random duration between 0 and 60 minutes, making the posting time unpredictable.
- The Instagram posting functionality is dependent on having a business account and requires additional setup with the Instagram Graph API.

## Disclaimer
This script is provided for educational purposes. Ensure you comply with the terms of service of OpenAI and Twitter when using their APIs. 
