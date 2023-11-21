---
classoption:
- twocolumn
- nonumber
geometry:
- a4paper
- totalwidth=6.85in
- totalheight=9.92in
- top=0.63in
- left=0.71in
header-includes:
    \pagestyle{empty}
---
# AIleister Cryptley, a gpt-fueled sock puppeteer

Have you ever wondered how to make your sock puppet more fleshed out without any substantial work on your behalf? Now, with LLMs (large language models) to help you, it's easier than ever.

## The goal

Imagine that you are new to OSINT, and you've heard that at some point, it would be good for you to make a fake profile on social media for your investigations. However, you're a busy fellow. There's just no way you can handle an imagined persona. Incorporating posting on social media into your schedule might be a daunting task. But fret not! AIleister is here to help.

## The idea

Most of us know that the LLMs can talk about literally anything now. ChatGPT even passed the Turing test a few months back. We can use it to our advantage and make it say things for our sockpuppet. Introducing: AIleister Cryptley -- a cybersec occultist. He recently started sharing pieces of gpt-generated cybersec tips on Twitter. All by himself!

## The implementation

If we know what we want to do, the rest of the project is trivial. You can even ask chat-gpt to generate it for you (and tweak it a little). First, we need to get a chat-gpt tip. We can use the following function for that.
```python
def get_tip() -> Optional[str]:
  response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo-16k",
    messages=[
      {"role": "system", "content": 
      "You are a human knowledgeable in"
      "cybersecurity, programming and AI."},
      {"role": "user", "content":
      "Can you give me a tweet-length "
      "cybersecurity, programming or AI tip"
      "(or trivia)? It can also be a pun."}
    ]
  )
  return response.choices[0].message['content']
```

But, to use OpenAi's API (or Twitter API), we need API keys. By storing them in the environmental variables, we can easily access them!
```python
# Load environment variables
openai_api_key = os.getenv('OPENAI_API_KEY')
x_api_key = os.getenv('X_API_KEY')
x_api_secret_key = os.getenv('X_API_SEC')
x_access_token = os.getenv('X_ACC_TOKEN')
x_access_token_secret = os.getenv('X_ACC_TOKEN_SEC')
x_bearer_token = os.getenv('X_BEARER_TOKEN')

# Initialize OpenAI
openai.api_key = openai_api_key
```

Now, we want to post the tip. This can be done with the following piece of code.

```python
def post_to_twitter(message: str) -> None:
  client = tweepy.Client(
    consumer_key=x_api_key,
    consumer_secret=x_api_secret_key,
    access_token=x_access_token,
    access_token_secret=x_access_token_secret,
    bearer_token=x_bearer_token
  )
  client.create_tweet(text=message)
```
Finally, we can add some posting time randomization and finish the script.
```python
if __name__ == "__main__":
  if random.randint(1, 100) == 1:
    tip = get_tip()

  if tip:
    delay_minutes = random.randint(0, 60)
    time.sleep(delay_minutes * 60)
    post_to_twitter(tip)
```
## The wrap-up

There are several things to note.

* The part about getting the API keys and storing them in the environmental variables wasn't covered on this page. Luckily, it's not that complicated.

* Access to OpenAI API is *not* free (that's why the script uses a cheaper gpt-3.5 model).

* An extended version of the presented code can be found on my github (link in the footer). You can find the setup description and broader explanation/justification of the code in the README.

* The script runs have to be scheduled. You can use CRON (Linux/Mac) or Task Scheduler (Windows) to do that.

* AIleister Twittter can be found [here](https://twitter.com/ACryptley).

## The disclaimer

This page was not generated by AI (although the temptation was there).